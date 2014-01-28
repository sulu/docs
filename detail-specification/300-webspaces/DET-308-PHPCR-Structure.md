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

For translation fallbacks there will be an implementation for fallbacks configured in webspace xml!

__Example from PHPCR - ODM: Language strategie attribute__

![ODM Attribute strategy](https://raw2.github.com/sulu-cmf/docs/master/detail-specification/images/locale_attribute.png)

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

Request for other language (fallback choosen by language fallback chooser):

```
{
	title: 'Title',
	name: 'test name'
}
```

Example Structure:

```
.../page -> sulu_locale:de-title='Titel' sulu_locale:en-title='title' sulu_locale:fr-title-='titre' name='test name'
    |-->/sub-page -> ...
    |-->/sub-page-1 -> ...
```

### Child

__Example from PHPCR - ODM: Language strategie child__

![ODM child strategy](https://raw2.github.com/sulu-cmf/docs/master/detail-specification/images/locale_child.png)

```
.../page -> name='test name'
    |-->/sulu_locale:de -> title='Titel'
    |-->/sulu_locale:en -> title='title'
    |-->/sulu_locale:fr -> title='titre'
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

For the name of the node there are two possibilities:

* create node: take title in the current language
* update node & title changed: if the language is the default language rename it
* else do nothing