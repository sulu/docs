# Snippets

Snippets enable you to define data structures which can be included as content
within pages.

## Defining Snippets

Snippets are a type of Structure. They are a subset (they implement some but
not all of the features) of normal Page structure and are defined in exactly
the same way.

Snippet definitions are located in `app/Resources/snippets` directory, the
following is an example snippet definition:

````xml
<?xml version="1.0" ?>

<template xmlns="http://schemas.sulu.io/template/template"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://schemas.sulu.io/template/template http://schemas.sulu.io/template/template-1.0.xsd"
          >

    <key>animal</key>

    <properties>
        <property name="title" type="text_line" mandatory="true">
            <meta>
                <title lang="de">Name</title>
                <title lang="en">Name</title>
            </meta>

            <tag name="sulu.search.field" role="title" />
        </property>

        <property name="description" type="text_editor">
            <meta>
                <title lang="de">Beschreibung</title>
                <title lang="en">Description</title>
            </meta>

            <tag name="sulu.search.field" role="description" />
        </property>
    </properties>
</template>
````

## Snippet content

Snippets can be used within pages with the Snippet content type. The
content type is `snippet` and is defined as follows within a page structure
template:

````xml
<?xml version="1.0" ?>

<template xmlns="http://schemas.sulu.io/template/template"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://schemas.sulu.io/template/template http://schemas.sulu.io/template/template-1.0.xsd"
          >

    <!-- ... -->

    <properties>

        <!-- ... -->

       <property name="animals" type="snippet">
            <meta>
                <title lang="de">Tiers</title>
                <title lang="en">Animals</title>
            </meta>
        </property>
    </properties>
</template>
````

This will allow the user to select one or more snippets to include in the page.

You can limit the choice of snippets to a single type by specifying the `snippetType`
parameter as follows:

````xml
<?xml version="1.0" ?>

<template xmlns="http://schemas.sulu.io/template/template"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://schemas.sulu.io/template/template http://schemas.sulu.io/template/template-1.0.xsd"
          >

    <!-- ... -->

    <properties>

        <!-- ... -->

       <property name="animals" type="snippet">
            <params>
                <param name="snippetType" value="animal" />
            </params>
            <meta>
                <title lang="de">Tiers</title>
                <title lang="en">Animals</title>
            </meta>
        </property>
    </properties>
</template>
````

Every snippet type have his own node before you can use a snippet you need to run the following command to create the snippet parent nodes:   
``` bash
app/console sulu:webspaces:init
```
