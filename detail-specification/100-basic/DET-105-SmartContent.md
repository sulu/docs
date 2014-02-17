##![basic](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/basic.png)DET-105 SmartContent
#### Description
The smart content is responsible for delivering a subset of our pages, and enables the template developer to show so called overview pages.
Therefore a widtget from the husky-library is used, which offers settings for filtering the pages by data sources, tags, categories, and so on.
The template receives this configuration along with an array, which resolves the configuration into a set of pages.

![Smart Content UML Diagram](https://raw.github.com/massiveart/sulu-docs/master/detail-specification/images/diagrams/SmartContent.png)

This functionality is implemented in an own [content type](https://github.com/sulu-cmf/docs/blob/master/detail-specification/300-webspaces/DET-301-template-architecture.md#contenttypes), called SmartContent. The [ContentMapper](https://github.com/sulu-cmf/docs/blob/master/detail-specification/300-webspaces/DET-301-template-architecture.md#mapper) delegates these tasks to the SmartContent-ContentType.
The content type uses a `SmartContentContainer`, on which the configuration from the Sulu administration is set. The `SmartContentContainer` also contains a `getData`-method resolving the configuration into actual pages. The `config` and `data` attributes are exported with a magic getter, so that it is easy accessible in a Twig-Template. For this the `NodeRepository` and the `TagManager` has to be injected, which also requires them to be available in the smart content type.
The container also implements its own `serialize`-method, because the preview component serializes this object, which includes not serializable dependencies. At this moment also the configuration is resolved, since the non-serializabe dependencies are required for that.
The container calls the `NodeRepository`, which is capable of returning the pages for the given configuration.
