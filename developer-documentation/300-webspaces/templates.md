# Templates
## Variables

| Variable    | Description
| ----------- | --------------------------------------------------------------------
| content.<property_name>     | Contains only the content of the page
| view.<property_name>        | Contains all the additional information provided by the content type
| extension.<property_name>        | Contains all the extension data (seo, excerpt ...)
| request.webspaceKey | Contains the key for the current webspace
| request.locale      | Contains the locale for the current request
| request.portalUrl | Contains the root URL to the current portal
| request.resourceLocatorPrefix | Contains the prefix for the current portal, useful for building relative links
| request.resourceLocator | Contains the resourcelocator to the current page
| request.analyticsKey | Contains the analytics-key for the current url
| uuid        | Contains the uuid of the currently display page
| template    | Contains the template key of the currently display page
| creator     | Contains the id of the creator of the current page
| changer     | Contains the id of the last changer of the current page
| created     | Contains the timestamp of the creation time
| changed     | Contains the timestamp of the latest change
| published     | Contains the timestamp of the publishing time
| urls     | Contains urls for all languages or null if no url exists for current page

