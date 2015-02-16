# Media-Selection

```xml
<property name="images" type="media_selection">
    <tag name="sulu.search.field" role="image" index="false"/>
    <meta>
        <title lang="de">Bilder</title>
        <title lang="en">Images</title>
    </meta>

    <params>
        <param name="types" value="right"/>
        <param name="defaultDisplayOption" value="right"/>
        <param name="displayOptions" type="collection">
            <param name="left" value="false"/>
        </param>
    </params>
</property>
```

## Params

* `types` - optional (string): commaseperated list of selectable [media-types](https://github.com/sulu-cmf/docs/blob/master/detail-specification/500-assets/DET-508-MediaTypes.md)
* `defaultDisplayOption` - optional (string): default value of display options for add new page/snippet
* `displayOptions` - optional (boolean|collection of boolean): visibility of display options possible keys:
  * leftTop (default: true)
  * top (default: true)
  * rightTop (default: true)
  * left (default: true)
  * middle (default: false)
  * right (default: true)
  * leftBottom (default: true)
  * bottom (default: true)
  * rightBottom (default: true)
 
## View Parameters

|   Parameter   | Example                                                               |
|---------------|-----------------------------------------------------------------------|
| displayOption | `view.images.displayOption` or `view.block[key].images.displayOption` |
