# <a name="gettingStarted"></a> Getting Started


1. ## Install the Prerequisites

    1. ### [Docker Desktop](https://www.docker.com/products/docker-desktop)

    1. ### [Codiac](http://codiac.io)

        ```
        npm i -g @codiac.io/codiac-cli
        ``` 
    1. ### [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
    1. ### [Node.js](https://nodejs.org/en/download/)

1. ## Create a new EMPTY git repo

    Also, you will be adding your own content, so you will not need to create it with a gitignore or a readme file *(though its ok if you do)*.

    ### GitHub:  
    [Creating a new repo](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/create-a-repo)

    ### Azure DevOps:  

    Either [with a new project](https://docs.microsoft.com/en-us/azure/devops/user-guide/sign-up-invite-teammates?view=azure-devops)  or [from an existing project](https://docs.microsoft.com/en-us/azure/devops/repos/git/create-new-repo?view=azure-devops)

    ### Bitbucket

    [Creating a new repo](https://support.atlassian.com/bitbucket-cloud/docs/create-a-git-repository/)


    ---
    Important:
    ---
    Be sure to copy the clone URL because you'll need it in the next step.
    ***


1. ## Create your Codiac API project

    1. Open a command line and navigate to the ***PARENT*** folder you like to use for development projects

        ```
        cd ~/dev
        ```

    1. Initialize a new project into that folder using your clone url

        We are going to use the optional `-t` parameter (aka: `--projectType`) to specify that we want to initialize as an `api` project type: 

        ```
        cod init -t api -c [your-clone-url] ./[target-folder]
        ```
        *Note: replace "`[your-clone-url]`" and "`[target-folder]`" in that example with the clone url for the new repo you just created and the folder into which you want to clone it.*

        This command will open your project into a new VSCode instance.  Give it a minute while installs all the npm packages for the api project type. 



<!-- 
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
-->


<!-- 1. ## Create an api definition

    in the `src` folder of your project there is an api definition class already created for you. 

    ```typescript
    class myApiDef extends apiDef 
    {
        constructor() {
            super();
        }
    }
    ``` -->
<!-- 
1. ## Create and start a host
    
    In your node starting point (eg: app.ts), create a new api host.
    To do so, you'll need to choose a local url and port for your api, and then declare them along with a new instance of your freshly minted api definition: 

    (in this example we're using ```localhost``` and port ```1775```)

    ```typescript
    const HOST = apiCore.apiHost.create(new myApiDef(), "127.0.0.1", 1775);
    ```

    You'll also need to tell node how to start it up...

    ```Typescript
    HOST.Start();
    ``` -->

1. ## Open the new project in VSCode

    Give it a minute while installs all the npm packages for the api project type.

    Open a command line window to the root of your new project folder. 


1. ## Set your Identity Tokens

    If you are going to be accessing private npm packages, 
    you'll need identity tokens for your package registry(ies) in order to build successfully.  In that case, set your identity tokens before building:
    ```
    cod identity --provider npm --token abc23pdq456e.etcetera.etcetera
    ```
    ---
    Note:  
    ---
    You can always get help on any command by calling it with the `--help` argument, eg:  `cod identity --help`
    ***

1. ## Build

    ```
    cod build
    ```
    NOTE: This command creates a new `Dockerfile` in your project root if you do not already have one.  If you want to regenerate your Dockerfile, just delete this file and run build again.

1. ## Run

    ### Bare-metal 
    *(just the api, without a container)*
        
    From the VSCode menus, select `Run > Start Debugging`, 
    or hit **`F5`**
    
    ### Container
    *(using Docker desktop)*
    ```
    cod run
    or
    cod run --port [1234]
    ```

    In both cases logs will write to your output window, and when the api has successfully bootstrapped itself, it will provide you the address at which to access it in the following log message:

    `apiHost listening on 0.0.0.0:5775...`



5. ## Verify the Run

    Verify it by **hitting a few of the built-in endpoints** using your favorite api client ([Postman's a good one](https://www.getpostman.com/))

    Version:
    ```
    GET http://127.0.0.1:1775/version
    ```

    openApi spec:
    ```
    GET http://127.0.0.1:1775/openApi
    ```


1. ## Check in your code

    Now that you've created your api, and verified that its a good build and run, it is a good time to put a stake in the ground and commit your code.

    You can do this with git, but the codiac CLI also provides you several source code commands to keep things simple.

    The example below uses the `stage` command with the `-c` (aka: `--commit`) argument to perform both the stage and commit in the same step.

    ```
    cod stage -A -c "Initial project creation"
    ```

    *See also: `commit`, `pull`, `push`, `branch`, `switch`, `status`, `merge`, `sync`*


6. ## Add a set of RESTful CRUD endpoints for an entity

    Let's say you have a "shoe" entity in your business domain, and you want to enable consumers of your api to create, read, update, and delete it (aka: CRUD).  
    
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

7. **Build and Run**

    ```
    cod build
    ```

    `VSCode > Run > Start Debugging`  or hit **`F5`**

    or 
    ```
    cod run
    ```


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


1. ## Check in your code

    ```
    cod stage -A -c "Added show cruds"
    ```

1. ## Publish your image

    ```
    cod publish
    ```


## Congratulations!

Hopefully your brain fired off a couple [Dopamine hits](https://www.amazon.com/dp/1591848016/ref=cm_sw_em_r_mt_dp_U_PRhVCb40VY80N) as you worked thru that quick implementation and watched it snap together.  And look at that, you have a fully functional, RESTful, standards-compliant API! 

Now that you've enjoyed your little moment of self-actualization, it's time to propel yourself even further:
**Check out some more info and examples:

* [Quickstart #1: (Quickest) Build a Custom Endpoint in < 10 mins](quickstart-1.md)
* [Quickstart #2: Database cruds in < 30 minutes](quickstart-2.md)
* [Quickstart #3: Extending Crud operations and custom data design in < 45 minutes](quickstart-3.md)
