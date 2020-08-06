# MongoDb Repo Plugin

A highly functional data access layer for a MongoDb database.

## Features

* **Domain driven ORM** *supporting divergence between data model and domain.*
* **CRUD, Patch, and Upsert** *for single and multiple entities.*
* **Embedding and Cascading** *enabling full continuity for single-hit writes of parent and child entities.*
* **Read-optimized** *by placing the burden of joins and embedding into write operations.*
* **COTN** *smart defaults and optional DDL on demand for low-code implementation of typical scenarios.*  
* **Comppliant with Standard Codiac Interfaces** *enabling seamless use of multiple data source providers across a given domain*

## Getting Started

Add the plugin to your api startup script runner...
```Typescript
codiac
  .addPlugin(MongoDbRepoPlugin)
  .run(myApiDef);
```

Register the server address for your mongoDb in your api definition's `bootstrap()` method...
*NOTE:  The plugin will automatically  register mongodb with your api using  default values, so if you plan to take all the defaults, even this step is unnecessary.*
```Typescript
this.useMongoDb(host.appConfig["mongo-dbname"]||"localhost");
```
