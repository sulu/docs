# Template architecture

![Template architecture](https://raw.github.com/massiveart/sulu-docs/master/detail-specification/images/diagrams/structure_architecture.png)

* Devided in three sections
  * Structure
  * ContentTypes
  * Mapper

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

## ContentTypes

* ContentTypes are implemented as Services
* ID: sulu.content.type.<<name>>
* get method sets data from node to property
* set method gets data from property and set data to node
* two types:
  * SimpleContentType: complete save and read method to save data in a property of phpcr node
  * ComplexContentType: Extends ContainerAware for complex operations. To control the flow there are two types PRE_SAVE and POST_SAVE

## Mapper

* Provides a interface to read and write data
* Uses Structure
* Iterates over Properties
* Save data of pre_save properties before $session->save() and data of post_save after $session->save()
* To get the structure for a key it uses the Service 'sulu.content.structure' which (should) implement StructureFactoryInterface
* The read method returns a structure field with value

## Template-Reader
* Reads an template in XML format and returns structure as array
* Is available as service

## Template Example
* You can find an example for a template that the template reader can parse below
* There is also an xsd available. (Sulu/Bundle/ContentBundle/Xml/Template/Schema/template.xsdtemplate.xsd)

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

        <property name="images" type="imageSelection" minOccurs="0" maxOccurs="2">
            <params>
                <param name="minLinks" value="1"/>
                <param name="maxLinks" value="10"/>
            </params>
        </property>
    </properties>
</template>

```
