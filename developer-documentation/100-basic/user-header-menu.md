# Security Bundle
This document is going to show you, how to install the user menu in your sulu application.

## UserDataInterface

To not limitate the way on how to secure your application, the UserDataInterface has to be implemented. 


Sulu\Bundle\AdminBundle\UserData;


## services.xml

then the implementation has to be registered as service within your application.
```
parameters:
    permissions:
    ...
    sulu_security.services.user_data_handler.class: Sulu\Bundle\SecurityBundle\Services\UserDataHandler
    
...
    
services:
    user.services.user_data:
      class: %sulu_security.services.user_data_handler.class%
      
```


you can also use another id than 'user.services.user_data', but then it has to be defined in the app config:

sulu_admin:
	user_data_service: {YOUR_ID}