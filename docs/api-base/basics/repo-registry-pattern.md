# The Repo Registry Pattern

## TL;DR.


* The **generic repo pattern** can be employed to perform cruds against an entity model.

* The registry is a map of entity repos by entity type.  The registry decouples the concrete repos from the code that consumes them.  

### Implementation essentials

**At Startup:**
1) Declare a repo for each entity type
1) Register that repo for its entity type

**At runtime:**
1) As the registry for the repo mapped to a given entity type
1) Call the repo methods.

## Built in, customizeable, extensible, overrideable

An added benefit in that decoupling is the ability to decouple the database platform itself, so that you can employ multiple database platforms without any impact on the consumer.  That is, you can use MS Sql for one entity type and MongoDb for another, without any impact to the code consuming your repo.

You can use the built in repos, which are highly customizeable and extensible.  The repo patterns are extensible allowing you to build your own where you see fit.  And finally, you can completely override the use of the repo pattern altogether by writring custom endpoints if you want to approach your data access in an entirely different way.

