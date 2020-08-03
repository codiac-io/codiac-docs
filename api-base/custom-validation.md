# Custom Validation


Adding custom validation involves two steps:
* Step 1: [Create a `ValidationDef` for your entity.](#step1)
* Step 2: [Register your validationDef with the API](#step2)

## <a name="step1"></a>Step 1: Create a `ValidationDef` for your entity.

You will need to define an injectable class that will perform the actual validation against your entity type.

```Typescript
@injectable()
export class shoeValidator extends ValidatorDef<shoe>
{
    constructor() {
        super(shoe);
    }
}
```

Now let's add some constraints for this validator to enforce.  

### Property-Scoped Constraints
We're going to enforce that the property `shoe.size` must be greater than 1.  

There's fluent methods for this on the `ValidatorDef`.  In the constructor for your new validator class, use the `enforces()` fluent method, and then the `thatItMust()` fluent method to define the response message and logic of our new constraint:
```Typescript
this.enforces(s => s.size)
    .thatItMust("be greater than 1", (val) => val > 1);
```

Notice that the lambda expression returns a boolean.  Returning `false` will evoke a validation failure, and the caller will be notified of the constraint requirements by way of your "that it must" description.  Returning `true` will be interpreted as valid, and no error will be thrown.    

This particular constraint is a simple one and needs no more information to perform its job than the value of the property it is enforcing.  But often, enforcing a constraint requires that the whole entity be in context so that we can compare one or more of its properties.  To use the entity itself in your constraint, simply add the entity as an argument to your lambda expression:
```Typescript
this.enforces(s => s.size)
    .thatItMust("be set if the model is set", (val, ent) => (ent.model) ? val != null : true);
```

...and just for practice, lets add another property-scoped constraint limiting `brand` to 35 characters:

```Typescript
this.enforces(s => s.size)
    .thatItMust("be greater than 1", (val) => val > 1)
this.enforces(s => s.size)
    .thatItMust("be set if the model is set", (val, ent) => (ent.model) ? val != null : true);
this.enforces(s => s.brand)
    .thatItMust("Be 35 chars or less", (val,ent) => (!val || val.length<= 35));
```


### Entity-Scoped Constraints 

Perhaps the nature of the constraint is not relevant to one specific property, but is more applicable to an overall state of the entity itself?  This is called an Entity-Scoped Constraint, and we can define it using the `ensuresThatItMust()` fluent method.

For instance, lets say Reebok only offers specific size ranges for each gender, and we have to enforce Reebok female shoe sizes to run from 2 to 10 and male sizes from 6 to 14:

```Typescript
this.ensuresThatItMust("have a size compatible with its gender", s => {
    if (s.brand == "Reebok")
    {
        if (s.gender == "F") {
            return 2 <= s.size && s.size <= 10;
        } else {
            return 6 <= s.size && s.size <= 14;
        }
    }
    else
    {
        return true;
    }
});
```
The result of an entity-scoped constraint will not be bound to a single specific property, and will appear at the summary level in the validation response.


### Globally Scoped Constraints

What if, in order to validate your entity, you had to look not just at your entity itself, but the other existing entities?  

**For example**: say we are trying to save a new shoe, and need to validate that the SKU we gave it (Stock Keeping Unit) is unique in the system.  That is, we want to run a lookup against the database to see if that sku already exists.

Well first thing you'll need is an instance of a `shoe` repo to perform this query.  However, the arguments to the validation logic contain only the entity itself and the validation context object; where do we get the repo?

Constructor injection is the pattern you are looking for.  This is your validation class, so you get to define the constructor, and the constructor injection pattern is supported in full by this system.  

Thus, whatever you need to perform that validation, you can add as an injected constructor argument:

```Typescript
@injectable()
export class shoeValidator extends ValidatorDef<shoe>
{
    constructor(@inject(INTERFACES.IRepo) private repo: IRepo) {
        super(shoe);
    }
}
```
Now you can call it out inside your constraint logic using `this.repo`.  

Below we'll add a new constraint for the SKU, and use that repo instance to check for any duplicate SKUs.

```Typescript
this.enforces(s => s.sku)
    .thatItMust("not already exist on another entity", (sku, entity) => {
        let result = await this.repo.tryReadMany<shoe>(shoe, { "sku": sku });
        return (result.count == 0);
    });
```

So you can add whatever type of entity you like to your validation handlers.  The only requirement being that whatever you are injecting into your constructor, it must have been [registered with the API's IOC container](using-ioc.md) during the API bootstrapping. 

Extensibility, folks!

Now if you look closely at the constraint we just created for `shoe.sku`, you might notice that we only want this constraint firing during a `create` transaction, not in an `update` transaction.  The validation context will tell us what operation is being performed, so let's use the `IValidatorContext.operation` to specify that our new constraint on `shoe.sku` only applies to `create` transactions:

```Typescript
this.enforces(s => s.sku)
    .thatItMust("not already exist on another entity", (sku, entity, context) => {
        if (context.operation == "create")
        {
            let result = await this.repo.tryReadMany<shoe>(shoe, { "sku": sku });
            return (result.count == 0);
        } 
        return true;
    });
```

NOTE:  To keep the topic simple, we're not adding any error trapping or other bulletproofing to this constraint logic.  In the real woirld, you will likely be adding error checks to support a repo call that returned an exception.


### Built-in constraints

Call out a built-in constraint


### Validation context

Sometimes the operation being performed on the entity is relevant when determining which constraints apply.   The `validationContext` object provides your lambda expression with that information.

it contains the operation and the validator options 



## <a name="step2"></a>Step 2: Register your validationDef with the API 

in the constructor of your api definition, declare each the custom validator for your entity:

```Typescript
this.validateWith<shoe, shoeValidator>(shoe, shoeValidator)
```

Once your validator is registered by entity type, your crud endpoints will invoke it as needed.


