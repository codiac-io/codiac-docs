# Codiac API Base

A typescript Api framework for the NodeJs platform. 

[Get started!](#gettingStarted)

- **Extensible**: Injectable and configurable, with multiple layers at which to modify behaviors, from tweak a config setting, to overriding existing behaviors, to injecting a custom library, to wholesale custom coding an entire endpoint.
- **Intuitive**: BDFD, fluent, extensible, common practices
- **Lazy**: (aka: efficient, productive) Smart defaults allow COTN (Code Only The Nuance) development.
- **Testable**: Full decoupling and extensibility.  Endpoint definitions are not dependent on the platform and can therefore be instantiated, mocked, and executed without an http request.  Validation constraints, repos, loggers, and class mappers can be run out of the context of an endpoint, all with mocked dependencies.

## Features

### IOC
* *What are we going to use for this?*
* Typescript-ioc https://www.npmjs.com/package/typescript-ioc
* InversifyJS http://inversify.io/

### Security 
* JWT authentication
* Role-based authorization
### Class Mapping (via Automapper-ts)
### Validation framework
### Projections
* Supported at serialization, class mapping, and persistence layers.
### HATEOAS support
* Conventional default projection by composition
* HAL protocol for references on properties by aggregation 
### Persistence 
* Built in generic repo pattern with registry by entity type
* MongoDb repo
* Sql NHibernate repo
* Sql Dapper Orm repo
* EF repo?
### Search Support
1. EntityCriteria objects
1. PropertyCriteria objects
### Logging support


### Extensible Pipeline Pattern 

Bootstrap in your own custom request handling plugins


### Conventional CRUD Endpoints

*This is essentially a plugin*

*Include Route convention, response codes, request contract, response envelope.*

1. Create
    * Create Single
    * Create Many
1. Read
    * Read one by Id (ie: spec for one)
    * Read by Criteria  (provide optimized "count", aka: include ability to specify meta only - no output)
    * Exists by Id (ie: spec for one)
    * Exists by Criteria
1. Update
    * Update Single
    * Update Many
1. Patch
    * Patch Single
    * Patch Where
1. Delete
    * Delete Single
    * Delete Where



### Coming soon...
#### Telemetry support
#### Event-driven integration model
* Extensible bus client
* Enterprise Event model

#### Default api contracts 
(dynamic, matching endpoint's domain entity if not explicitly declared)


# <a name="gettingStarted"></a> Getting Started

1. **Set up a new Typescript project**

    A few typical gotchas we'd like to get out of the way.  Run these commands from inside your new project folder:

    1. You'll be using node with npm, so install npm and run 
        ```
        npm init
        ```
    1. Initialize Typescript
        ```
        tsc --init
        ```
    1. Set the following flags in your ```tsconfig.json```
        ```json
        "target": "es6",
        "experimentalDecorators": true,
        "emitDecoratorMetadata": true
        ```

1. **Install the nodejs_api package:**

    ```
    npm install @mfreydl/nodejs_api
    ```

1. **Create an api definition:**

    ```typescript
    class myApiDef extends apiDef 
    {
        constructor() {
            super();
        }
    }
    ```

1. **Create and start a host:**
    
    In your node starting point (eg: app.ts), create a new api host.
    To do so, you'll need to choose a local url and port for your api, and then declare them along with a new instance of your freshly minted api definition: 

    (in this example we're using ```localhost``` and port ```1775```)

    ```typescript
    const HOST = apiCore.apiHost.create(new myApiDef(), "127.0.0.1", 1775);
    ```

    You'll also need to tell node how to start it up...

    ```Typescript
    HOST.Start();
    ```

3. **Build and run**

5. Verify it by **hitting a few of the built-in endpoints** using your favorite api client ([Postman's a good one](https://www.getpostman.com/))

    Api Root:
    ```
    GET http://127.0.0.1:1775/
    ```

    Version:
    ```
    GET http://127.0.0.1:1775/version
    ```

    openApi spec:
    ```
    GET http://127.0.0.1:1775/openApi
    ```


6. **Add a set of RESTful CRUD endpoints for an entity**

    Let's say you have a "shoe" entity in your domain, and you want to enable consumers of your api to create, read, update, and delete it (aka: CRUD).  
    
    The ApiDef extensions make easy work of this, and you're going to need to tell them a few things about your shoe entity.

    a. Create a class for your shoe and be sure that it implements ```IDomainEntity```.  
    ```Typescript
    export class shoe implements IDomainEntity
    {
        constructor(public size: number, public brand: string, public model: string, public gender: string, id?: string) {
            this.id = id;
        }

        public id: string|undefined;
    }
    ```
    b. To enable searching on your entity, you'll need a criteria object that will enable your endpoint consumers parameterize their searches.
    ```Typescript
    export class shoeCriteria
    {
        constructor(public size?: number, public brand?: string, public model?: string, public gender?: string, public id?: string) {
        }
    }
    ```
    **CONVENTION**: Each property on the criteria object will apply to the corresponding property of that name on the domain entity.  

    **NOTE**: Notice the use of optional properties on the criteria object example... api consumers will set only the properties they want to search on, so you'll want your endpoints to be able to know when a given property is relevant.

    See [Searching and Criteria](docs/searching-and-criteria.md) for more on supporting searches. 

    Ok, now that you have your entity and its corresponding criteria object, you're ready to declare a set of CRUD endpoints for it.

    Open the **constructor** for your api definition and declare a crud set... 
    ```Typescript
    this.addCrudsFor<shoe,shoeCriteria>(shoe, "shoecriteria", "/shoes");
    ```
    As you can see, the ```addCruds``` method also wants you to declare the route *(```/shoes``` in this case)* in addition to the domain entity and its criteria. 

7. **Build and run**


8. **Now let's take a look at your new endpoints**

    *(NOTE: They are automatically documented on the swagger page of your api: GET http://127.0.0.1:1775/openApi)*

    * Create, CreateMany
        ```
        POST http://127.0.0.1:1775/shoes/new
        POST http://127.0.0.1:1775/shoes
        ```
    * Read, ReadMany
        ```   
        GET http://127.0.0.1:1775/shoes/{id}
        GET http://127.0.0.1:1775/shoes
        ```
    * Update, UpdateMany
        ```    
        PUT http://127.0.0.1:1775/shoes/{id}    
        PUT http://127.0.0.1:1775/shoes
        ```
    * Delete, DeleteWhere
        ```
        DELETE http://127.0.0.1:1775/shoes/{id}
        DELETE http://127.0.0.1:1775/shoes
        ```
    AND...

    * Patch, PatchWhere  (there are [3 diff types of patch](docs/patch-and-update.md) based on content-type header)
        ```    
        PATCH http://127.0.0.1:1775/shoes/{id}
        PATCH http://127.0.0.1:1775/shoes
        ```
    *(ok, so it's not just CRUD, it's CRUD-P....  Yay!)*


## Congratulations!

Hopefully your brain fired off a couple [Dopamine hits](https://www.amazon.com/dp/1591848016/ref=cm_sw_em_r_mt_dp_U_PRhVCb40VY80N) as you worked thru that quick implementation and watched it snap together.  And look at that, you have a fully functional, RESTful, standards-compliant API! 

Now that you've enjoyed your little moment of self-actualization, it's time to propel yourself even further:
**Check out some more info and examples in the [Documentation](docs/toc.md)...**
