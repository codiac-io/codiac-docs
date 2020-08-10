# Codiac API Plugins

The Api platform is designed from the ground up with extensibility in mind, and below is a list of the plugins available from Codiac.

These plugins make light work of basic functionalities typical in a REST API.  They each ship with the Codiac Api Platform, and they get automatically scaffolded into your codiac project when you initialize as an `api`.

To configure your api to use these plugins, call them out fluently from your `Codiac` startup class using the `addPlugin()` method:

```Typescript
Codiac
  .addPlugin(MongoDbRepoPlugin)
  .addPlugin(SqlRepoPlugin)
  .addPlugin(ValidationPlugin)
  .addPlugin(OpenApiPlugin)
  .run(YourApiDefinition)
```

## Codiac Plugins

* [MongoDB Repo](./mongodb-repo-plugin.md)
* [Sql Repo](./sql-repo-plugin.md)
* [Validation](./validation-plugin.md)
* [Open API](./open-api-plugin.md)
