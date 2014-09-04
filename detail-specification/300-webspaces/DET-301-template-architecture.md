# Template architecture

![Template architecture](https://raw.github.com/massiveart/sulu-docs/master/detail-specification/images/diagrams/structure_architecture.png)

## Structure

* Holds information about Template
* Structure is a abstract class to cache the informations in symfony 2 cache
* Structure holds basic informations about the template
  * key ... unique template key
  * view ... twig template for rendering
  * controller ... controller to render template
  * cacheLifeTime ... how long the content can be cached
* A structure can hold a lot of Property
* To get a value of a Property:
  * $structure->getProperty('title')->getValue()
  * $structure->title
* To set a value of a Property:
  * $structure->getProperty('title')->setValue('test)
  * $structure->title = 'test';
* Property holds basic informations about the property
  * name ... property name
  * mandatory ... indicates whether a property is mandatory
  * multilingual ... indicate wether a property is multilingual
  * minOccurs & maxOccurs ... indicates the range of this property array
  * contentTypeName ... name of content Type
  * value ... value of property
* This classes are basic data - classes with less logic

## Template-Reader
The template-reader is able to parses a template in XML format and returns the structure as array. Therefore the load-method which accepts as the first parameter the path to the xml-file is used. This array will then be used to generate a cacheable php-class with the StructureManager.
The template-reader works according to the structure defined in the template.xsd-file in Sulu/Bundle/ContentBundle/Xml/Template/Schema/template.xsd.

### Template Example
You can find an example for a template that the template reader can parse below:


```xml
<?xml version="1.0" ?>
<template xmlns="http://schemas.sulu.io/template/template"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://schemas.sulu.io/template/template http://schemas.sulu.io/template/template.xsd">

    <key>overview</key>

    <view>page.{_format}.twig</view>
    <controller>SuluContentBundle:Default:index</controller>
    <cacheLifetime>2400</cacheLifetime>
    
    <meta>
        <title lang="de">Übersicht</title>
        <title lang="en">Overview</title>
    </meta>
    
    <properties>
        <property name="title" type="text_line" mandatory="true">
            <meta>
                <title lang="de">Titel</title>
                <title lang="en">Title</title>

                <placeholder lang="de">Playtzhalter für Titel</placeholder>
                <placeholder lang="en">Placeholder for title</placeholder>
            </meta>

            <tag name="sulu.node.name"/>
            <tag name="sulu.rlp.part" priority="1"/>
        </property>
        <property name="name" type="text_line" mandatory="true">
            <tag name="sulu.rlp.part" priority="2"/>
        </property>
        <property name="url" type="resource_locator" mandatory="true">
            <tag name="sulu.rlp.input"/>
        </property>
        <section name="content">
            <meta>
                <title lang="de">Inhalt</title>
                <title lang="en">Content</title>

                <info_text lang="de">Der Inhalt wird auf der Webseite dargestellt</info_text>
                <info_text lang="en">The content will be displayed on the website</info_text>
            </meta>
            <properties>
                <property name="article" type="text_editor" mandatory="true">
                    <meta>
                        <title lang="de">Artikel</title>
                        <title lang="en">Article</title>
                    </meta>
                </property>

                <block name="block" default-type="title" minOccurs="2" maxOccurs="10" mandatory="true">
                    <meta>
                        <title lang="de">Das ist ein Block</title>
                        <title lang="en">That´ a Block</title>

                        <info_text lang="de">Der Block kann verwendet werden um Eigenschaften zu gruppieren</info_text>
                        <info_text lang="en">The block can be used to group properties</info_text>
                    </meta>
                    <types>
                        <type name="title">
                            <properties>
                                <property name="title" type="text_line" mandatory="true">
                                    <meta>
                                        <title lang="de">Titel</title>
                                        <title lang="en">Title</title>
                                    </meta>

                                    <tag name="sulu.rlp.part" priority="3"/>
                                </property>
                            </properties>
                        </type>
                        <type name="title_text">
                            <properties>
                                <property name="title" type="text_line" mandatory="true">
                                    <meta>
                                        <title lang="de">Titel</title>
                                        <title lang="en">Title</title>
                                    </meta>

                                    <tag name="sulu.rlp.part" priority="3"/>
                                </property>
                                <property name="article" type="text_editor" mandatory="true">
                                    <meta>
                                        <title lang="de">Artikel</title>
                                        <title lang="en">Article</title>
                                    </meta>
                                </property>
                            </properties>
                        </type>
                    </types>
                </block>
            </properties>
        </section>
    </properties>
</template>
```

## Block Content
The block content is a special property type in template xml structure. This parts will be handled with the BlockContentType. This Content Type creates a node property foreach child property (<blockname>-<propertyname>). if the property is multiple, it will create foreach property an array of values in the node property. To save and load content from phpcr the othe content types will be used, defined in each child property. Theoretical th block content can be used recursive, but our UI supports only one stage.

__Example (from above -> only block)__:

* i18n:de-article-title = array ( 'Title 1' , 'Title 2' )
* i18n:de-article-article = array ( 'Article 1' , 'Article 2' )

### Types
Block Content allows to define Types to define diffrent manifestations. These types can have complete diffrent look and feel.

Each Instance of block have a implicity (hidden property) `type` these holds the name of the type. These type property allows to load the right properties for the instance and read and load data in the right structure.

__TODO Block diagramm__

## Sections
Secctions are used to visualy group Properties in the backend form.

## Meta
Each type of properties have a subnode named meta(data) which holds localized metadata like:

* Title (fallback name upper case)
* Information Text (fallback '')
* Placeholder (fallback '')

## Structure Manager
The structure manager uses the template-reader to retrieve a specific php-class from the cache and returns an object of the requested php-class. When the requested class-file does not exist it will be generated and placed in the specified cache direcotry. The constructor accepts an array with configuration options - the default values can be found below:

```php
$this->options = array(
    'template_dir' => null,
    'cache_dir' => null,
    'debug' => false,
    'cache_class_prefix' => 'Template_Structure_',
    'base_class' => 'Structure.php'
);
```

The getStructure-metod actually retrieves the object from the requested class. The class-file as well as the template-file will be identified with the key-parameter.

## Property - Tags
This feature resulting out of issue https://github.com/sulu-cmf/sulu/issues/76 .

Tags are saved in the template structure along with the property, and the Structure-Class has some methods to return all the properties with a given Tag or a method to return the property with the highest priority.

The `XMLFileLoader` has check if there is one property with the `sulu.node.name`-tag, and reject the configuration file with a warning, if there is none.

Tags should be namespaced as in the example, so that we don't get troubles with eventually usage of this feature in client projects.

Tags should also be able to receive a priority, like the `sulu.rlp.part`-tag in the example. The one using the tag can decide for what the priority is used (only use the property with a value and the highest priority on this tag, or use all of them and use the priority for sequencing). The `XMLFileLoader` checks the combination of name and priority of uniquess. Default priority is `1`.

Sulu will then never again ask hardcoded for the `title`-attribute anywhere, but use the structure to get the fields with the given tag instead.

For URL generation in form there are two needed tags in the tempalte:

* `sulu.rlp.part` : used as input for the gernation, if there are more than one, the parts will ne concated with rising priority
* `sulu.rlp.input` : the generated url will be placed in this property

## Reserved Property names
To keep prefixes short we decided to reserve internal names. For special installation, there is the posibility to add a internal prefix in config (```sulu_core.content.internal_prefix```).

## Internal structures
Internal structures are used for hide specific Structures in the UI. Internal structures are for example `internal-link`. These structures can be used to generate forms for system functionalities (link internal node settings).

## Twig-Template
To render a content you can define which twig template is used. in the definition in `<view>overview.{_format}.twig</view>` you can use the `{_format}` placeholder. the controller will place the requested format automatically in the template name (default is html).

Example:
`````
URL: http://sulu.lo/en
TWIG: overview.html.twig
---
URL: http://sulu.lo/en.html
TWIG: overview.html.twig
---
URL: http://sulu.lo/en.xml
TWIG: overview.xml.twig
````

### Preview
For preview rfa tags have to be used:

__Normal Property__
```
<h1 property="title">{{ content.title }}</h1>
```

__Block Property__
```
<div class="row" property="block" typeof="collection">
   {% for block in content.block %}
       <div class="col-lg-4" rel="block">
           {% if block.type == 'editor' %}
               <h2 property="title">{{ block.title|default('') }}</h2>

               <b>{{ block.type }}</b>
               {% autoescape false %}
               <div property="article">{{ block.article|default('') }}</div>
               {% endautoescape %}
           {% elseif block.type == 'title_only' %}
               <h1 property="title">{{ block.title|default('') }}</h1>
               <b>{{ block.type }}</b>
           {% endif %}
       </div>
   {% endfor %}
</div>
```

__Smart-Content__
```
<div property="smartcontent">
    {% for page in content.smartcontent %}
        <div class="col-lg-4">
            <h2>
                <a href="{{ content_path(page.webspaceKey, page.languageCode) }}">{{ page.title }}</a>
            </h2>
            {% autoescape false %}
            {{ page.article|slice(0, 50) }}
            {% endautoescape %}
        </div>
    {% endfor %}
</div>
```
