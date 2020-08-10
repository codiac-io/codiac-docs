# Adding a Custom Endpoint

## Define your contracts

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

## Define your endpoint
  ***Inside the constructor of your api definition***, declare an endpoint definition and add it to the api:

  ```Typescript
      this.endpoints.push(
          new TypeSafeEndpointDef<myRequest, myResponse>("myRequest"
              , httpRestVerb.GET, "getSum")
              .WithHandler(req => { 
                  return new myResponse(req.partA + req.partB); 
              })
      );
  ```

##  Triggering Your Endpoint

  NOTE:  if you're firing an http `GET` method, the properties of your request contract are populated by name from the querystring parameters.  
  ```http
  GET http://127.0.0.1:1775/getSum?partA=5&partB=16
  ```

  Your endpoint should return your response object:
  ```json
  { sum: 21 }
  ```

## Adding Route Parameters

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

## Validate your input

  There are three steps to adding validation:
  1. Create a validator
  1. Fire it against the input
  1. Apply any failures or warnings to the response

