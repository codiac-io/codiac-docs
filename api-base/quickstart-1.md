# Quickstart #1: (Quickest) Build a Custom Endpoint in < 10 mins

Let's try to learn to create an api with a custom endpoint in less than 10 minutes.

*(Ok, we all know you're never going to be building a stupid effing calculator endpoint in the real world; the point here is to learn how to add an endpoint that uses your own custom processing of its user input and returns a calculated result.)*

## Before you begin:
If you havent already, create an api project as outlined in the [Getting Started tutorial](../README#gettingStarted)

## Part 1: Create a custom endpoint

We're going to make an endpoint that adds two given numbers and returns the sum in the response.

### Add your own custom endpoint

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

***Inside the constructor of your api definition***, define your endpoint as a `TypeSafeEndpointDef<>`:
```Typescript
this.endpoints.push(
    new TypeSafeEndpointDef<myRequest, myResponse>("myRequest"
        , httpRestVerb.GET, "getSum")
        .WithHandler(req => { 
            return new myResponse(req.partA + req.partB); 
        })
);
```
The `TypeSafeEndpointDef` is an endpoint definition that enforces its request and response types, and supports all the basic core features of the system, such as routing, . 


###  Build, run and hit your new endpoint

NOTE: If you're firing an http "GET" method, the properties of your request contract are populated by name from the querystring parameters.  
```
GET http://127.0.0.1:1775/getSum?partA=5&partB=16
```

Your endpoint should return your response object:
```json
{ "sum": 21 }
```

###  Wanna try adding route parameters?

Just add another route to your endpoint definition using `.WithRoute()`
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

## Next Steps

[Quickstart #2](quickstart-2.md)
