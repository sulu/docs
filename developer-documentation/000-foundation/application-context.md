# Application Contexts
## General
* Set in the `AdminKernel` resp. `WebsiteKernel``
* Tells which kernel has started (`admin` or `website` as value)

## Service tag
* Use the `sulu.context`-tag with the `context`-attribute to register a service for one kernel only

```xml
<!-- This service will only be loaded in the website kernel -->
<service id="sulu.service1" class="...">
    <tag name="sulu.context" context="website"/>
</service>
<!-- This service will only be loaded in the admin kernel -->
<service id="sulu.service1" class="...">
    <tag name="sulu.context" context="admin"/>
</service>
<!-- This service will be loaded in both kernels-->
<service id="sulu.service1" class="...">
    
</service>
```
