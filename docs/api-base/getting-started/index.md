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
**Check out some more info and examples:

* [Quickstart #1: (Quickest) Build a Custom Endpoint in < 10 mins](quickstart-1.md)
* [Quickstart #2: Database cruds in < 30 minutes](quickstart-2.md)
* [Quickstart #3: Extending Crud operations and custom data design in < 45 minutes](quickstart-3.md)
