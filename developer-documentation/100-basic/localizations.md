# Localizations
There is an own component dedicated to localizations. The main parts of a
localization are a country and language, which can be combined to a code.

So austrian german will consist of the language `de` and the country `at`,
and can therfore be combined to `de-at`.

Localizations are also nestable.

## Structure

### LocalizationProvider
Any bundle can offer localizations, by implementing the
`LocalizationProviderInterface` and registering the implementing class via the
`sulu.localization_provider`-tag, as e.g. the `WebspaceManager` did:

```xml
<service id="sulu_core.webspace.webspace_manager" class="%sulu_core.webspace.webspace_manager.class%">
            <tag name="sulu.localization_provider"/>
            <argument type="service" id="sulu_core.webspace.loader.xml"/>
            <argument type="service" id="logger"/>
            <argument type="collection">
                <argument key="config_dir">%sulu_core.webspace.config_dir%</argument>
                <argument key="cache_dir">%sulu.cache_dir%</argument>
                <argument key="debug">%kernel.debug%</argument>
                <argument key="cache_class">%sulu_core.webspace.cache_class%</argument>
                <argument key="base_class">%sulu_core.webspace.base_class%</argument>
            </argument>
        </service>
```

### LocalizationManager
The `LocalizationManager` collects all the languages from the registered 
`LocalizationProvider` and returns them in its `getLocalizations`-method.

### LocalizationController
There is also the LocalizationController, which returns all localizations as
JSON, when sending a request to `/admin/api/localizations`.
