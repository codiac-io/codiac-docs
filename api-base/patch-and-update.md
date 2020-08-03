# Patch and Update

Let's modify our entities.

You just have to ask yourself one question:  Do I want to replace the whole thing or just modify one or more of its properties?

* Use the [UPDATE](#update) endpoints to do a wholesale replacement of an entity
* Use the [PATCH](#patch) endpoints to modify one or more of its properties

## <A name="update"></A> Update 

### Update Single
Life with UPDATE is very simple.  Simply fire off a "PUT" request using the route for that shoe (the shoes url suffixed with the `id` of the entity. "123" in this case).

```
PUT http://localhost:1775/shoes/123
```
...and pass the entity (eg: a `shoe`) as the body of the request
```json
{
    "id": "123",
    "brand": "Nike",
    "model": "Metcon 4",
    "gender": "M",
    "size": 11,
    "tags": [ "CrossTraining", "Sport" ]
}
```

### Update Many
To replace several entities in a single request, fire a `PUT` request just as you did for updating the single, but **dont use the id suffix** in the route...
``` 
PUT http://localhost:1775/shoes/
```
...and pass an array of your entities in the body...
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
NOTE:  You can indeed send just a single entity to this endpoint, but remember that the endpoint is expecting you to send it a list, so you'll need to pass it as an array of one.

## <a name="patch"></a>Patch

Patch, like Update, modifies an existing entity.  However, UNLIKE Update, it changes ***only the properties you specify***, it does NOT perform a wholesale entity replacement. 

The API supports two different PATCH operations, determined by their corresponding `Content-Type` header:

### Merge Patch (Default)
```
Content-Type: application/json
```

The Merge patch is the simplest syntax, and as such, it's the default.  It operates just like Update, only you dont have to pass the entire entity (though you could if you like).  The request below will patch `shoe id:123` with new values for `size` and `gender`:
```
PATCH http://localhost:1775/shoes/123
```
```json
{
    "gender": "M",
    "size": 11
}
```

As defined in [RFC7386](https://tools.ietf.org/html/rfc7386), a Merge Patch is essentially a partial representation of the entity. The submitted JSON is "merged" with the current entity to create a new one, then the new one is saved. For more details on how to use Merge Patch, [see the RFC](https://tools.ietf.org/html/rfc7386).



### JSON Patch
    
```
Content-Type: application/json-patch+json
```

If you need to do something slightly more complicated than a merge patch will support, or if you are simply needing to follow a standard, you can use a JSON Patch.

As defined in [RFC6902](https://tools.ietf.org/html/rfc6902), a JSON Patch is a sequence of operations that are executed on the resource, e.g. 
```json
{"op": "add", "path": "/a/b/c", "value": [ "foo", "bar" ]}
```
So if we wanted to add the tag "Youth" to our shoe with `id:123`:
```
PATCH http://localhost:1775/shoes/123

Content-Type: application/json-patch+json
```
```json
{ "op": "add", "path": "tags", "value": "Youth" }
```

 For more details on how to use JSON Patch, [see the RFC](https://tools.ietf.org/html/rfc6902).

