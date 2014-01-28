# DET 308 PHPCR Structure

## Multilangual

Reffering to [PHPCR-ODM](https://doctrine-phpcr-odm.readthedocs.org/en/latest/reference/multilang.html?highlight=language#choosing-the-right-translation-strategy).

### Requirements

* Fallback on Property layer
* Query (Smart Content, Navigation??)
* Internal Links (Redirect??)

### Strategies

There are 2 Strategies for storing translations for pages:

* Attribute: Each property has one prefixed attribute for each language
* Child: Each language has one child with the translated properties

### Attribute

Global default language is de (set in configuation).

* title is multilingual
* name is not multilingual

Request language de:

```
{
	title: 'Titel',
	name: 'test name'
}
```

Request language en:

```
{
	title: 'title',
	name: 'test name'
}
```

Request for other language:

```
{
	title: 'Title',
	name: 'test name'
}
```

Example Structure:

```
.../page -> sulu_lang_de:title='Titel' sulu_lang_en:title='title' sulu_lang_fr:title='titre' name='test name'
    |-->/sub-page -> ...
    |-->/sub-page-1 -> ...
```

### Child

```
.../page -> name='test name'
    |-->/sulu_lang_de -> title='Titel'
    |-->/sulu_lang_en -> title='title'
    |-->/sulu_lang_fr -> title='titre'
    |-->/sub-page-1
    		   |-->...
    |-->/sub-page-2
    		   |-->...
```

## Multiwebspaces

To support multiwebspace in a single workspace the content / route tree will prefixed by webspace key.

Schema: 

```
/cmf/<webspace>/route
           |-->/content
```
