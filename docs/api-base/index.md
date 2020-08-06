# Codiac Api Platform

A typescript Api framework for the NodeJs platform. 

[Getting Started](./getting-started)


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


### Keyboard-less Introduction

1. Design Strategies
    1. Impetus and Goals
    1. Searching and Projections
    1. RESTfulness and Beyond (standards implemented, list and batch operations)
    1. Repo Registry Strategy
    1. MongoDb Strategy
    1. Decoupling Strategy
    1. Event Sourcing Strategy
    1. HATEOAS Strategy

### Documentation

1. Basics: Architecture and Components
    1. The Host
    1. The ApiDef
    1. The EndpointDef
    1. Request and Response Contexts
    1. The Router
    1. Dependency Injection and the IOC Container
    1. The MongoDb Repo
    1. The Sql Repo
    1. The Repo Pattern: Registry, Repo, & RepoFor
    1. The Criteria object
    1. Filter Types (StringFilter, DataFilter, NumericFilter, DateRangeFilter)
    1. Projections
    1. The Validation Framework (automatics, canned, and custom validations)
    1. The OpenApi endpoint and its UI counterpart
1. Advanced: Architecture and Components
    1. Event Sourcing
    1. Creating Web Hooks
    1. Request Pipeline Plugins
1. Extending The System
    1. Roll Your Own Repo
    1. Roll Your Own Validation Framework
    1. Roll Your own endpoint set
    1. Roll Your Own Plugin
    1. Roll Your Own Swagger UI


