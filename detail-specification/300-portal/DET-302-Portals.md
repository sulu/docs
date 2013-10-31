##DET-001 Portals

####Component diagram
![Portal component diagram](https://raw.github.com/massiveart/sulu-docs/master/detail-specification/images/diagrams/PortalManager.png)

####General
#####XML
The portals will be configured in the `app/Resources/portal`-folder, with the following format:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<portal xmlns="http://schemas.sulu.io/portal/portal"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://schemas.sulu.io/portal/portal
                            http://schemas.sulu.io/portal/portal.xsd">
    <name>Sulu</name>
    <key>sulu</key>

    <languages>
        <language main="true" fallback="true">DE</language>
        <language>EN</language>
    </languages>

    <theme>
        <key>sulu</key>
        <excluded>
            <template>overview</template>
        </excluded>
    </theme>

    <environments>
        <environment type="prod">
            <urls>
                <url main="true">http://www.sulu.io</url>
                <url>http://sulu.io</url>
            </urls>
        </environment>
        <environment type="dev">
            <urls>
                <url main="true">http://dev.sulu.io</url>
            </urls>
        </environment>
    </environments>
</portal>
```
There will be a file for each portal. It contains a root portal node, which has some subnodes defining a name, a key, many languages (with defining main and fallback languages), the theme with the excluded templates, and different environments, which define the urls (also which one is the main url).

#####Interpreting
The `PortalManager` is a service, responsible for offering the portals defined in the above described configuration files. Because it should not read the information on every request, it caches the information with the `PhpPortalCollectionDumper`. The `ConfigCache`-class offered by Symfony checks if the cache is fresh, and if not it writes a new class to the cache, using the `PhpPortalCollectionDumper`.
This class adds only some portals to the collection in the constructor, so that it can be instantiated and instantly used.  

For loading and parsing the XML Files there is the XmlFileLoader, which is a service and extends Symfony's `FileLoader`. Its `load`-Method returns a `Portal`-Object, which is used by the `PortalManager`.
