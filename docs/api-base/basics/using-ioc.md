# Using IOC (Inversion of Control) in your API

In your ApiDef, in the bootstraop method, you can register types with the ioc container:

```Typescript
public Bootstrap(host: apiHost): void {
    host.ioc.bind<ICoolTool>(INTERFACES.ICoolTool).to<MyFavoriteCoolTool>(MyFavorioteCoolTool)
}
```