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


```
<?xml version="1.0" ?>
<template xmlns="http://schemas.sulu.io/template/template"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://schemas.sulu.io/template/template http://schemas.sulu.io/template/template.xsd">

    <key>overview</key>

    <view>page.html.twig</view>
    <controller>SuluContentBundle:Default:index</controller>
    <cacheLifetime>2400</cacheLifetime>

    <properties>
        <property name="title" type="textLine" mandatory="true"/>
        <property name="url" type="resourceLocator" mandatory="true"/>
        <property name="article" type="textArea" mandatory="false"/>
        <property name="pages" type="smartContentSelection" mandatory="false"/>
        
        <block name="article" minOccurs="2" maxOccurs="10">
	           <properties>
                <property name="title" type="text_line"/>
				            <property name="article" type="text_area"/>
	           </properties>
        </block>

        <property name="images" type="imageSelection" minOccurs="0" maxOccurs="2">
            <params>
                <param name="minLinks" value="1"/>
                <param name="maxLinks" value="10"/>
            </params>
        </property>
    </properties>
</template>

```

## Block Content
The block content is a special property type in template xml structure. This parts will be handled with the BlockContentType. This Content Type creates a node property foreach child property (<blockname>-<propertyname>). if the property is multiple, it will create foreach property an array of values in the node property. To save and load content from phpcr the othe content types will be used, defined in each child property. Theoretical th block content can be used recursive, but our UI supports only on stage.

__Example (from above -> only block)__:
* sulu_locale:de-article-title = array ( 'Title 1' , 'Title 2' )
* sulu_locale:de-article-article = array ( 'Article 1' , 'Article 2' )

## Structure Manager
The structure manager uses the template-reader to retrieve a specific php-class from the cache and returns an object of the requested php-class. When the requested class-file does not exist it will be generated and placed in the specified cache direcotry. The constructor accepts an array with configuration options - the default values can be found below:

```
$this->options = array(
    'template_dir' => null,
    'cache_dir' => null,
    'debug' => false,
    'cache_class_prefix' => 'Template_Structure_',
    'base_class' => 'Structure.php'
);
```

The getStructure-metod actually retrieves the object from the requested class. The class-file as well as the template-file will be identified with the key-parameter.
