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
