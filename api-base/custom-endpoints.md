


6. Add your own custom endpoint

    First, you'll need to define what the request and response objects for this endpoint will look like:

    ```Typescript
    class myRequest {
        constructor(public partA: number, public partB: number)
        { }
    }
    ```

    ```Typescript
    class myResponse {
        constructor(public sum: number)
        { }
    }
    ```

    ***Inside the constructor of your api definition***, define your endpoint:
    ```Typescript
        this.endpoints.push(
            new TypeSafeEndpointDef<myRequest, myResponse>("myRequest"
                , httpRestVerb.GET, "getSum")
                .WithHandler(req => { 
                    return new myResponse(req.partA + req.partB); 
                })
        );
    ```

7.  Build, run and hit your new endpoint

    NOTE:  if you're firing an http "GET" method, the properties of your request contract are populated by name from the querystring parameters.  
    ```
    GET http://127.0.0.1:1775/getSum?partA=5&partB=16
    ```

    Your endpoint should return your response object:
    ```json
    { sum: 21 }
    ```

8.  Wanna try adding route parameters?

    Just add another route to your endpoint definition
    ```Typescript
        this.endpoints.push(
            new TypeSafeEndpointDef<myRequest, myResponse>("myRequest"
                , httpRestVerb.GET, "getSum")
                .WithRoute("add/:partA/to/:partB(/)")
                .WithHandler(req => { 
                    return new myResponse(req.partA + req.partB); 
                })
        );
    ```

    Now you can hit that endpoint without querystring parameters
    ```
    GET http://127.0.0.1:1775/add/5/to/16
    ```

9. Validate your input

    There are three steps to adding validation
    1. Create a validator
    1. Fire it against the input
    1. Apply any failures or warnings to the response


7. Create an entity type and add a full restful crud set for it 
