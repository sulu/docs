# Contacts REST Service

* Use abstract class RestController, which inherits from FOSRestController
* RestController provides a function called processPut
  * Implementes the basic flow of a PUT-Request (delete missing entries, update existing entries, add the rest of the entries)
  * Specific actions for delete, update and add are injected by callbacks
