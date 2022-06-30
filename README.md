# hapi-easy-router

Haven't written any test 😔

Usage:
```javascript
  const EasyRouter = require("./index");
  const routerFactory = EasyRouter.makeRouter();
  const { GET, POST, PUT, PATCH, DELETE } = EasyRouter.Methods;

  const functionHandler = () => {};
  const objectHandler = {
    handler: functionHandler,

    // plugin "hapi-swagger"
    description: "Route description",

    // Joi validation
    validate: {
      params: Joi.object({
        id: Joi.number().required(),
      }),
      query: Joi.object({
        type: Joi.string(),
      }),
      payload: Joi.object({
        name: Joi.string(),
      }),
    }
  };

  // single route
  routerFactory.GET("/", functionHandler);
  routerFactory.POST("/items", functionHandler);
  routerFactory.GET("/items/{id}", objectHandler);
  routerFactory.PUT("/items/{id}", objectHandler);
  routerFactory.PATCH("/items/{id}", objectHandler);
  routerFactory.DELETE("/items/{id}", objectHandler);

  // group route with "users" prefix
  routerFactory.group("/users", [
    GET("/", functionHandler),
    POST("/", functionHandler),
  ]);

  // get all routes
  const routes = routerFactory.allRoutes();

  // set routes to server
  const server = await Glue.compose(Manifest, options);
  server.route(routes);
```
