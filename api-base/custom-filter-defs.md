

# Custom Filter Types


Say you want to add a criteria property that, when set, invokes complex filtering logic for a read operation in an entity repo.   A custom filter is a way to accomplish this. 

## TL;DR

There are three steps to implementing a custom filter:

1. Create your class implementing `IFilter`.
2. Create its `IFilterDefBuilder` Class 
3. Register it with the repo plugin.
4. Use it in your criteria object as a property type or a property decorator.
4. (optional) Create a **custom deserializer** for it.



## The Scenario  
You're building a carnival api, and you want to add a criteria property to filter on the `UserProfile` entities that are allowed to ride a given roller coaster.  Let's name this new property: `canRide`.  

Now if there were a boolean property named `canRide` on your `UserProfile` entity, then we'd be done; the repo would take it from there.  

But not in this scenario: there is no property `canRide` on a user profile.  In fact, `canRide`  *really means*...
* ...is at least 42" tall  
* ...AND is not a pregnant female
* ...AND does not have a heart condition
* ...AND is not overdue on membership fees

So if our api receives a criteria object that looks like this:
```json
{
  "attraction": "greased-lightning",
  "canRide": true
}
```

...then the logic it needs to invoke is going to look something like this *(using MongoDb)*:
```json
{
  "height": { "$gt": 42 },
  "$not": { 
    "sex": "female",
    "pregnant": true
  },
  "medical": { 
    "$not": { 
      "$contains": "heart" 
    } 
  }
}
```

### So Create a Custom Filter for Your Custom Logic 

A filter is a class type that you apply to a property on a criteria object.  Let's make a `FastRollerCoasterFilter`

...as the property type:
```typescript
class UserProfileCriteria {
  
  public canRide?: FastRollerCoasterFilter; 
  
  public attraction: string;
} 
```
...or declared in a `filterWith` decorator 
```typescript
class UserProfileCriteria {

  public attraction: string;

  @filterWith(FastRollerCoasterFilter)
  public canRide?: boolean|; 
} 
```

A Custom filterDef will allow you to invoke unique query behaviors from a criteria property, without having to write a custom endpoint or repo.  

## How to Implement:

### Step 1: Create Your Own Filter Class

This is where you write general logic for the api platform. 

```typescript
class FastRollerCoasterFilter implements IFilter {
  constructor() {
  }
  public property?: string;
  public $not?: this;
}
```

### Step 2: Create its FilterDefBuilder Class

This is where you add support for your particular database platform. You'll need to implement `IFilterDefBuilder`.

The MongoDb Repo Plugin provdes a base class for you to extend: `MongoFilterDefBuilder`...
```typescript
class FastRollerCoasterFilterBuilder extends MongoFilterDefBuilder<FastRollerCoasterFilter> {

}
```

### Step 3: Register It with the Repo 

Declare your filter type from within your api's `bootstrap()` method...
```typescript
this.registerFilterType(FastRollerCoasterFilter, FastRollerCoasterFilterBuilder);
```

### Step 4: Use Custom Filter as a property type on a criteria class for your entity

There are two ways to use your custom filter type:

...as the property type:
```typescript
class UserProfileCriteria {
  
  public canRide?: FastRollerCoasterFilter; 
  
  public attraction: string;
} 
```
...or declared in a `filterWith` decorator 
```typescript
class UserProfileCriteria {

  public attraction: string;

  @filterWith(FastRollerCoasterFilter)
  public canRide?: boolean|; 
} 
```

### Step 5:  Custom Deserializers

Perhaps your custom filter type has a unique abbreviated string representation in a request that needs custom handling in order to translate it into a concrete instance off your filter. 

`StringFilter` does this, allowing an inbound request like 
```json
{ "favoriteColor": "$sw_gr" }
``` 
...to be deserialized into the following instance of `StringFilter`: 
```json
{ 
  "property": "favoriteColor",
  "$startsWith": "gr" 
}
``` 

 To apply a custom deserializer for your filter, you will need to register your deserializer with the api itself, so that it can use it when it encounters your filter during the inbound sequence of a request.

#### Create your Deserializer
So first, let's create a static method on the filter class for deserializing 

```typescript
class FastRollerCoasterFilterSerializer {
  public deserialize(value: string) {
    let instance = new FastRollerCoasterFilter();
    this.doSomethingUnique(value, instance); 
    return instance;
  }
}
```
*(NOTE: YES, you can instantiate a serializer class, too, instead of using a static method.  We're just trying to keep it simple and stay focused on the registration in the following step.  That's the required part)*

#### Register Your Deserializer With the Api

In the `bootstrap()` method of your api, tell the api itself how to deserialize an instance in a request: 

```typescript
Bootstrap(host: apiHost): void {
  ...
  api.registerFilterSerializerFor(FastRollerCoasterFilter, 
    x => new FastRollerCoasterFilterSerializer().deserialize(x)
  );
  ...
}
```

