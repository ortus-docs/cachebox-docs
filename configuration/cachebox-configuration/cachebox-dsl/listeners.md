# Listeners

This is an array of structures that you will use to define cache listeners. This is exactly the same as if you would be declaring ColdBox Interceptors, so order is very important. The order of declaration is the order that they are registered into their specific listening events and also the order in which they fire. The keys to declare for each structure are:

| Key            | Type               | Required | Default               | Description                                                                                                                                                                        |
| -------------- | ------------------ | -------- | --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| class          | instantiation path | true     | ---                   | The instantiation path of the listener object to register                                                                                                                          |
| **name**       | string             | false    | `listLast(class,".")` | The unique name used for this listener for registration purposes. If no name is provided, then we will use the last part of the instantiation path, which is usually the filename. |
| **properties** | struct             | false    | `{}`                  | A structure of name-value pairs of configuration data for the listener declared.                                                                                                   |
