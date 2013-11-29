##DET-302 Portals

####Component diagram
![Portal component diagram](https://raw.github.com/massiveart/sulu-docs/master/detail-specification/images/diagrams/Workspaces.png)

####General
#####XML
The workspaces will be configured in the `app/Resources/workspaces`-folder, with the following format:

```xml
<?xml version="1.0" encoding="utf-8"?>
<workspace xmlns="http://schemas.sulu.io/workspace/workspace"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://schemas.sulu.io/workspace/workspace http://schemas.sulu.io/workspace/workspace-1.0.xsd">

    <name>Sulu CMF</name>
    <key>sulu_io</key>

    <localizations>
        <localization language="en" country="us" shadow="auto"/>
        <localization language="de" country="at"/>
        <localization language="de"/>
    </localizations>

    <portals>
        <portal>
            <name>Sulu CMF AT</name>
            <key>sulucmf_at</key>
            <resource-locator>
                <strategy>tree</strategy>
            </resource-locator>

            <theme>
                <key>default</key>
                <excluded>
                    <template>overview</template>
                </excluded>
            </theme>

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
</workspace>


```
There will be a file for each workspace. It contains a root workspace node, which has some subnodes defining a name, a key, many localization (with a tree structure) and a list of all the portals. The workspace defines an area for all the content, and a portal is built on top of this content. 

A portal includes different localizations (which can also be configured in the xml). A portal also gets an own name and key, and defines the resource locator strategy. Every portal must also define which theme is used, and which templates of this theme should be included. 
Every portal must also define a list of environments, which will be chosen by the environment variable (which is the type of each environment). Every environment defines its own urls, containing a pattern to describe language, country and segment (written in curly braces), or these values are defined in the url node, as you can see above.

#####Interpreting
The `WorkspaceManager` is a service, responsible for offering the workspaces and portals defined in the above described configuration files. Because it should not read the information on every request, it caches the information with the `PhpWorkspaceCollectionDumper`. The `ConfigCache`-class offered by Symfony checks if the cache is fresh, and if not it writes a new class to the cache, using the `PhpWorkspaceCollectionDumper`.
This class adds only some portals to the collection in the constructor, so that it can be instantiated and instantly used.  
For loading and parsing the XML Files there is the XmlFileLoader, which is a service and extends Symfony's `FileLoader`. Its `load`-Method returns a `Workspace`-Object, which is used by the `WorkspaceManager`.
