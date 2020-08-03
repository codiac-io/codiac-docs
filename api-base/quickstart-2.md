# Second Quickest Quickstart: Database cruds in < 30 minutes


## Before you begin:
If you havent already, create an api project as outlined in the [Getting Started tutorial](../README.md#gettingStarted)

Open up your favorite API client ([Postman](https://www.getpostman.com/) is a good one).

### Install MongoDB

Your API will need access to a database, and this tutorial uses [MongoDB](https://www.mongodb.com/).

#### EITHER:  Install MongoDB locally on your machine
* Download MongoDB Community Server from the [mongoDB download page](https://www.mongodb.com/download-center/community)
* Follow their [installation instructions](https://docs.mongodb.com/manual/administration/install-community/)


#### OR: Run the mongodb Docker image
* Be sure you have [Docker](https://www.docker.com/get-started) installed on your machine.
* Follow the [instructions on docker hub](https://hub.docker.com/_/mongo) for using the mongo image.

## Step 1: Wire Up Your Database

1. In the ```Bootstrap``` method of your API Definition, invoke the mongo initializer with "footwear" as the name for your database:

    ```Typescript
    this.useMongoDb("footwear");
    ```
    If the `footwear` db does not yet exist, it will be created on first use.
    You must, however, have a MongoDb instance running on your local machine listening on the default MongoDb port (aka: a connection string of ```mongodb://localhost:27017/footwear```)

    Or you can declare a MongoDb by calling out your own connection string:
    ```Typescript
    this.useMongoDb("footwear", "mongodb://localhost:27017/footwear");
    ```

## Step 2: Create Your Domain Entities

1. Create an entity (make it implement the `IDomainEntity` interface)
    ```Typescript
    export class shoe implements IDomainEntity
    {
        constructor(public size: number, public brand: string, public model: string, public id?: string) {
        }
    }
    ```
    Notice that the `id` is an optional parameter; it will need to be when you are creating a new entity and you want ids to be assigned automatically.

1. Create a search criteria object
    
    This class defines the search parameters that can be used to search on your entities.  The repo consumer will craft queries using this object.
    
    A simple way to approach this is to mirror the properties of your entity with filter properties on the criteria object:

    In this case: `StringFilter` for any `string` property and `NumericFilter` for any properties of type `number`. 

    ```Typescript
    export class shoeCriteria
    {
        constructor(public size?: NumericFilter, public brand?: StringFilter, 
            public model?: StringFilter, public id?: StringFilter) {
        }
    }
    ```

    In the code above you can see that for each property type on the entity, it is convenient to use a corresponding Filter type on the criteria object.  The Filter classes provide options for how to specify parameters and are already fully supported by the repo system (which means you wont need to manually write in support for them).
    
    Be sure also to **make all criteria properties optional**, because we want to allow our repo consumers to specify or omit parameters at their own discretion.  



## Step 3: Specify a Persistence Layer for your Domain Entities

On the back of your MongoDb declaration, chain a call to the fluent method `forCrudsOn()` to set up the data layer for each entity.

```Typescript
this.useMongoDb("footwear", "mongodb://localhost:27017/footwear")
    .forCrudsOn<footwearDomain.shoe>(footwearDomain.shoe)
    .forCrudsOn<footwearDomain.Vendor>(footwearDomain.Vendor);
```

## Step 3: Expose a CRUD Endpoint Set

1. Declare a crud endpoint set

    In the constructor of your own apiDef, add the following:
    ```Typescript
    this.addCrudsFor<footwearDomain.shoe,footwearDomain.shoeCriteria>(footwearDomain.shoe, footwearDomain.shoeCriteria, "/shoes", "/footgear");

    this.addCrudsFor<footwearDomain.Vendor,footwearDomain.VendorCriteria>(footwearDomain.Vendor, footwearDomain.VendorCriteria, "/vendors");
     ```

    For each entity here you are specifying its criteria object and one or more routes for the endpoint set.  
    
    This will produce a full set of RESTful crud endpoints in your api for each of these entities, accessible, respectively, through the urls:
    ```
    http://localhost:1775/shoes
    http://localhost:1775/footgear
    http://localhost:1775/vendors
    ```

## Step 4: Look at Your Endpoints  

Among the luxurious prizes you get with your new API, are BOTH:
* an [OpenAPI definition](https://www.openapis.org/) document to describe your endpoints, and 
    ```
    GET http://localhost:1775/openApi
    ```
    This will provide the openApi specification document in json.

...AND...

* a [Swagger UI](https://swagger.io/tools/swagger-ui/) page to view it in a visual, interactive format.  
Open this url in a browser:
    ```
    http://localhost:1775/swagger-ui
    ``` 


## Step 5: Consuming Your Endpoints


1. ### **CREATE**: Creating New Entities

    In short, you're just going to send up your entities in a POST.

    Set your list of new shoes as the body of the http request:
    ```json
    [
        {
            "brand": "Nike",
            "model": "Metcon 4",
            "gender": "M",
            "size": 11,
            "tags": [ "CrossTraining", "Sport" ]
        },
        {
            "brand": "New Balance",
            "model": "20v7 Minimus Cross Trainer",
            "gender": "F",
            "size": 10,
            "tags": [ "CrossTraining", "Sport", "Zero Drop" ]
        }        
    ]
    ```

    Then send it off as a post to the shoes endpoint:
    ```
    POST http://localhost:1775/shoes
    ```

    You'll get your new enities back as the `output` in the response, complete with the new unique id it was given by the system. 
    ```json
    {
        "success": true,
        "output": 
            [    
                {
                    "id": "123",
                    "brand": "Nike",
                    "model": "Metcon 4",
                    "gender": "M",
                    "size": 11,
                    "tags": [ "CrossTraining", "Sport" ]
                },
                {
                    "id": "456",
                    "brand": "New Balance",
                    "model": "20v7 Minimus Cross Trainer",
                    "gender": "F",
                    "size": 10,
                    "tags": [ "CrossTraining", "Sport", "Zero Drop" ]
                }
            ]
    }
    ```
    #### The Response Envelope:
    Take note that the response above includes not just your entity; it also contains some meta information about the transaction.  We call this object the "response envelope", and the built-in crud endpoints all use it. The response envelopes will typically provide you status on whether your request succeeded or failed, the associated error if it exists, and any validation failures if the request was rejected.  
    
    If your response was for a list of output entities, it will also include the `count` of entities returned, as well as any output paging counts (aka: `take`/`skip`/`countOverall`) if paging was specified in the request.  See [Response Envelopes](response-envelopes.md) for more info. 

1. ### **READ**: Searching on a Text Property

    Ok, pretend you're a web app, and you're searching for shoes.
    Let's start simple and fire off a request to the shoes endpoint to give us all the Nike brand shoes:
    ```
    GET http://localhost:1775/shoes?brand=Nike
    ```
    *NOTE: Default search behavior is NOT case-sensitive, so `?brand=Nike` will work just as well as `?brand=NIKE` or `brand=nike`*
    
    The properties of your criteria object *are* the supported querystring parameters, and in this case, we're doing a simple search for shoes with brand name of "Nike".  
    
    Congratulations, you just implicitly invoked the `Equals` operator.  But wait, there's more...
    
    Remember in our criteria object, we are using a [`StringFilter`](StringFilter.md) type for brand, so that also means we get to use some more interesting search operators for free, such as [StartsWith](StringFilter.md#StartsWith), [EndsWith](StringFilter.md#EndsWith), [Contains](StringFilter.md#Contains), [In](StringFilter.md#In), and [Pattern](StringFilter.md#Pattern).

    Let's use the StartsWith operator (`$sw`) to search for shoes with brands starting with the letter `"N"`  (eg: Nike or New Balance)

    ```Url
    /shoes?brand=$sw_N
    ```

    For more, see the [StringFilter operators](StringFilter.md) page.


1. ### Projections

    Ok, you got your shoes back, but currently your results contain each shoe record in its entirety:
    
    ```json
    [
        {
            "id": "123",
            "brand": "Nike",
            "model": "Metcon 4",
            "gender": "M",
            "size": 11,
            "tags": [ "CrossTraining", "Sport" ]
        },
        {
            "id": "456",
            "brand": "New Balance",
            "model": "20v7 Minimus Cross Trainer",
            "gender": "F",
            "size": 10,
            "tags": [ "CrossTraining", "Sport", "Zero Drop" ]
        }
    ]
    ```
    
    Suppose all you wanted was the `model` and `brand`?
    
    Enter [Projections](projections.md).
    
    Projections allow the API endpoint consumer to declare *in the request* what parts of the entities they want back.  
    
    *Support for projections is built-in, thus again preventing the API author from  writing custom code or adding redundant endpoints simply to accommodate varying representations of a given entity.*

    Projections get applied as headers in a request:

    ```http
    output-includes: "model,brand"
    ```
    
    When this http header is set in the request, a projection will be applied to each output entity that will pair it down to just the properties called out in the `output-includes` header. 

    If it was easier to simply exclude properties than to name each one to be included, you could use the `output-excludes` header:

    ```http
    output-excludes: "id,gender,size,tags"
    ```

    In both cases your entities will be returned like this:

    ```json
    [
        {
            "brand": "Nike",
            "model": "Metcon 4",
        },
        {
            "brand": "New Balance",
            "model": "20v7 Minimus Cross Trainer",
        }
    ]
    ```

1. ### **UPDATE**: Modifying Entities

    Let's change an existing entity. How about changing the gender and size of one of our shoes?  The Update part of CRUDs comes in two flavors:  `PATCH` and `PUT`
    
    #### Patch 

    We're going to use a `PATCH` http method with the route for that entity (in this case, that's the `/shoes` url suffixed with the `id` of the entity. `123` in this case).

    ```
    PATCH http://localhost:1775/shoes/123
    ```
    ...and then pass the properties that we are modifying as the body of the request

    ```json
    {
        "gender": "F",
        "size": 6,
    }
    ```
    #### PUT (ie: replace)

    That Patch was simple enough.  But doing so will leave the rest of the entity intact.  Suppose you want not just a few properties changed, but the *entire entity* replaced.  Now we're talking `PUT`  

    Use the `PUT` http method to **replace** an existing entity:
    ```
    PUT http://localhost:1775/shoes/123
    ```
    ...and pass your new incarnation of the entity (eg: a `shoe`) as the body of the request
    ```json
    {
        "id": "123",
        "brand": "Nike",
        "model": "Metcon 4",
        "gender": "F"
    }
    ```

    Notice that after you make this update, you wont see the `tags` and `size` properties leftover from the previously saved state of your entity; we've replaced the entity wholesale with what you just submitted in the `PUT`.

    These are simple single-entity examples, but you can also perform Patches and Puts on multiple entities at a time; you can apply a Patch by specifying criteria for which entities get the patch; and Patch will also allow you to perform more detailed operations on an entity such as modifying the contents of a list property (such as adding a tag to `shoe.tags`).

    See [Patch and Update](./patch-and-update.md) for more on modifying entities.

1. ### **DELETE**: Deleting Entities

    There are two ways to specify a delete: 
    * one at a time, using a unique identifier
    and
    * many at a time, using criteria  

    Deleting is a lot like searching: you specify what to delete using search criteria, and the endpoint will carry out the delete and return you the deleted entities.

    Let's delete our first shoe by its id.  The easiest way to do that is by appending the id onto the RESTful route and sending it off with a `DELETE` http method: 
    ```
    DELETE http://localhost:1775/shoes/123
    ```
    Your response should look like this:
    ```json
    {
        "success": true,
        "output": 
            {
                "id": "123",
                "brand": "Nike",
                "model": "Metcon 4",
                "gender": "M",
                "size": 11,
                "tags": [ "CrossTraining", "Sport" ]
            }
    }
    ```
    Notice that the output is not a json array `[]`, it's just the single entity itself.  That's because we used the route to a *single entity* delete endpoint.  
    
    Now let's delete using a criteria:
    ```json
    DELETE http://localhost:1775/shoes/

    {
        "brand": "New Balance"
    }
    ```

    This will delete ALL the "New Balance" entities in the system.  In our case, it's only the one (tho it is listed as an array of one because we hit the delete many endpoint):
    ```json
    {
        "success": true,
        "output": 
            [
                {
                    "id": "456",
                    "brand": "New Balance",
                    "model": "20v7 Minimus Cross Trainer",
                    "gender": "F",
                    "size": 10,
                    "tags": [ "CrossTraining", "Sport", "Zero Drop" ]
                }
            ]
    }
    ```

1. ### Validation

    All those saves and updates were designed to run successfully because the intention was to focus on how to invoke the CRUD actions, so we fed the API with good data.  Now that you know a bit about how to perform basic CRUDs, let's get real and take a look at protecting our data integrity with validation.

    #### Built-in validation

    There are a few forms of simple data validation that you get for free:
    * Property name enforcement
    * Native data type enforcement: (for properties of type `number` and `Date`)

    Any write request *(Create Update Delete aka: POST PATCH PUT DELETE)* will be rejected if the request violates one of these two types of validation.  

    Thus, if you send a malformed entity up for a patch, you're going to get a response showing that your request was rejected and some details as to why.

    So let's send up the following patch request; it contains both types of violations: 
    * a misspelled property name for `shoe.gender`
    * a string for `shoe.size` which is a numeric property
    ```
    PATCH http://localhost:1775/shoes/123
    ```
    ```json
    {
        "gemdr": "F",
        "size": "motorcycle",
    }
    ```
    Your response will be quite descriptive:
    ```
    http status: 422
    ```
    ```json
    {
        "success": false,
        "message": "Multiple validation failures.  See validation property for details.",
        "error": {  
            "stack": "Multiple validation failures.  See details"
        },
        "validation": {
            "failure": "Multiple validation failures.  See details",
            "details": [
                {
                    "candidate": "gemdr",
                    "failure": "No property exists with that name"
                },
                {
                    "candidate": "size",
                    "failure": "Value is not a number"
                }
            ]
        }
    }
    ```
    You'll see several ways to know how your request failed:
    * the [http status code 422](https://httpstatuses.com/422) will denote an invalid request
    * the `success` flag will be `false`
    * the `error` field will be populated with a validation error
    * the `validation` field will be populated with the breakdown of what failed.

    You'll see there is a summary message and a breakdown of each validation failure for you to use as you see fit.  Notice the `candidate` field in each validation detail, which includes the system name of the relevant property.  This value will describe the failure as well as help you link the error back a relevant data entry control. 


    MarkStartHere("We need to explicitly add a built-in validator")
    MarkStartHere("We need a custom validator")


    This is just to get you started - the validation features provide much more intensive capabilities.  You can learn about adding more validation rules in [custom validation](custom-validation.md).
    

1. ### Next Steps

    Ok, you've built a pretty functional RESTful crud API, but up to this point we've been using a pretty simple domain model.  Made sense so that you could get a bird's eye view of the toolset without getting your hands too dirty in the details.  
    
    But quality comes from attention to detail, so let's start getting a look at where we're gonna make our money:  customization.

    Our next tutorial, [Third-Most-Quickest Quickstart Tutorial: (Extending Crud operations and custom data design in < 45 minutes)](quickstart-3.md), will introduce you to some extensible and customizable features that empower you as you add your own flavor to your APIs.

    * Custom Validators
    * Custom Endpoint Handlers
    * Complex domain entity relationships 
    * Custom entity repos
    * Custom request and response pipeline middleware
    * Setting OpenAPI/Swagger content
    * Security and Access
    
      