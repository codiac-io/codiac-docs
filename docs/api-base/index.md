# Codiac Api Platform

## TL;DR

A framework for building Typescript APIs on the NodeJs platform. 


## The Impetus

I need a fast, easy to manage, scalable, extensible, container-ready API platform that isnt going to chew up all my time implementing things that arent unique.  And brought a versatile Object Oriented patterned approach to the Typescript/node stack.

COTN

OpenAPI

Domain Driven Design


**Extensible**: Injectable and configurable, with multiple layers at which to modify behaviors, from tweak a config setting, to overriding existing behaviors, to injecting a custom library, to wholesale custom coding an entire endpoint.


**Intuitive**: 
BDFD, fluent, extensible, common practices

**Lazy**: (aka: efficient, productive) Smart defaults allow COTN (Code Only The Nuance) development.

**Testable**: Full decoupling and extensibility.  Endpoint definitions are not dependent on the platform and can therefore be instantiated, mocked, and executed without an http request.  Validation constraints, repos, loggers, and class mappers can be run out of the context of an endpoint, all with mocked dependencies.


## Here's How

[Getting Started](./getting-started)




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



### Documentation

* [Tutorials](./getting-started/index.md)
    * [Getting Started](./getting-started/index.md)
    * [Quickstart 1](./getting-started/quickstart-1.md)
    * [Quickstart 2](./getting-started/quickstart-2.md)
    * [Quickstart 3](./getting-started/quickstart-3.md)

* [Basics: Architecture and Components](./basics/index.md)

  <!-- Here's what we currently have -->
    * [custom-endpoints](./basics/custom-endpoints.md)
    * [StringFilter](./basics/StringFilter.md)
    * [custom-filter-defs](./basics/custom-filter-defs.md)
    * [repo-registry-pattern](./basics/repo-registry-pattern.md)
    * [patch-and-update](./basics/patch-and-update.md)
    * [custom-validation](./basics/custom-validation.md)
    * [using-ioc](./basics/using-ioc.md)
    <!-- * [HATEOAS](./HATEOAS.md) -->
    <!-- * [response-envelopes](./response-envelopes.md) -->
    <!-- * [searching-and-criteria](./searching-and-criteria.md) -->
    <!-- * [projections](./projections.md) -->

<!-- Suggested in late 2018 
    * [The Host]()
    * [The ApiDef]()
    * [The EndpointDef]()
    * [Request and Response Contexts]()
    * [The Router]()
    * [Dependency Injection and the IOC Container]()
    * [The MongoDb Repo]()
    * [The Sql Repo]()
    * [The Repo Pattern: Registry, Repo, & RepoFor]()
    * [The Criteria object]()
    * [Filter Types (StringFilter, DataFilter, NumericFilter, DateRangeFilter)]()
    * [Projections](./projections.md)
    * [The Validation Framework (automatics, canned, and custom validations)]()
    * [The OpenApi endpoint and its UI counterpart]()
* [Advanced: Architecture and Components]()
    * [Event Sourcing]()
    * [Creating Web Hooks]()
    * [Request Pipeline Plugins]()
* [Concepts]()
    * [Impetus and Goals]()
    * [Searching and Projections]()
    * [RESTfulness and Beyond (standards implemented, list and batch operations)]()
    * [Repo Registry Strategy]()
    * [MongoDb Strategy]()
    * [Decoupling Strategy]()
    * [Event Sourcing Strategy]()
    * [HATEOAS Strategy]()
* [Extending The System]()
    * [Roll Your Own Repo]()
    * [Roll Your Own Validation Framework]()
    * [Roll Your own endpoint set]()
    * [Roll Your Own Plugin]()
    * [Roll Your Own Swagger UI]()
-->
* [Plugins](./plugins/index.md)
  * [MongoDB Repo](./plugins/mongodb-repo-plugin.md)
  * [Sql Repo](./plugins/sql-repo-plugin.md)
  * [Validation](./plugins/validation-plugin.md)
  * [Open API](./plugins/open-api-plugin.md)

