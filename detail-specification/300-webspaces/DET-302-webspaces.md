##DET-302 Webspaces

####Component diagram
![Webspace component diagram](https://raw.github.com/massiveart/sulu-docs/master/detail-specification/images/diagrams/Workspaces.png)

####General
#####XML
The webspaces will be configured in the `app/Resources/webspaces`-folder, with the following format:

```xml
<?xml version="1.0" encoding="utf-8"?>
<webspace xmlns="http://schemas.sulu.io/webspace/webspace"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://schemas.sulu.io/webspace/webspace http://schemas.sulu.io/webspace/webspace-1.0.xsd">

    <name>Sulu CMF</name>
    <key>sulu_io</key>
    
    <security>
        <system>sulu_io</system>
    </security>

    <localizations>
        <localization language="en" country="us" shadow="auto"/>
        <localization language="de" country="at"/>
        <localization language="de"/>
    </localizations>
    
    <theme>
        <key>default</key>
        <excluded>
            <template>overview</template>
        </excluded>
    </theme>

    <portals>
        <portal>
            <name>Sulu CMF AT</name>
            <key>sulucmf_at</key>
            <resource-locator>
                <strategy>tree</strategy>
            </resource-locator>

            <localizations>
                <localization language="de" country="at"/>
            </localizations>

            <environments>
                <environment type="prod">
                    <urls>
                        <url language="de" country="at">sulu.at</url>
                        <url redirect="sulu.at">www.sulu.at</url>
                    </urls>
                </environment>
                <environment type="dev">
                    <urls>
                        <url language="de" country="at">sulu.lo</url>
                        <url redirect="sulu.lo">sulu-redirect.lo</url>
                    </urls>
                </environment>
            </environments>
        </portal>
    </portals>
</webspace>


```
There will be a file for each webspace. It contains a root webspace node, which has some subnodes defining a name, a key, many localization (with a tree structure) and a list of all the portals. There is also an optional security section, which which can configure an security system. If the webspace is secured, only the users which have a role including this system can access the restricted area.

The webspace defines an area for all the content, and a portal is built on top of this content. Every webspace must also define which theme is used, and which templates of this theme should be included. 

A portal includes different localizations (which can also be configured in the xml). A portal also gets an own name and key, and defines the resource locator strategy. 
Every portal must also define a list of environments, which will be chosen by the environment variable (which is the type of each environment). Every environment defines its own urls, containing a pattern to describe language, country and segment (written in curly braces), or these values are defined in the url node, as you can see above.

The following table shows the valid placeholders in the URL:

| Placeholder    | Value
| -------------- | ---
| {localization} | The complete localization code, containing the language and country (e.g. `en-us` or `de-at`)
| {country}      | Only the country (e.g. `us` or `at`)
| {language}     | Only the language (e.g. `en` or `de`)

#####Interpreting
The `WebspaceManager` is a service, responsible for offering the workspaces and portals defined in the above described configuration files. Because it should not read the information on every request, it caches the information with the `PhpWebspaceCollectionDumper`. The `ConfigCache`-class offered by Symfony checks if the cache is fresh, and if not it writes a new class to the cache, using the `PhpWebspaceCollectionDumper`.
This class adds only some portals to the collection in the constructor, so that it can be instantiated and instantly used.  
For loading and parsing the XML Files there is the XmlFileLoader, which is a service and extends Symfony's `FileLoader`. Its `load`-Method returns a `Webspace`-Object, which is used by the `WebspaceManager`.
