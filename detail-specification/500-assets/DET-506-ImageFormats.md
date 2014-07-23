##![Assets](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/assets.png)DET-506 Image Formats

# Image Formats Concept

The image formats for each theme is configured in an own config.  
The themes are in src/Client/WebsiteBundle/Resources/themes.  
Every theme has his own config under theme_name/config called `image-formats.xml`.


A XML could be look like this:

``` xml
<?xml version="1.0" ?>
<formats xmlns="http://schemas.sulu.io/media/formats"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://schemas.sulu.io/media/formats http://schemas.sulu.io/media/formats-1.0.xsd">
    <format>
        <name>50x50</name>
        <commands>
            <command>
                <action>scale</action>
                <parameters>
                    <parameter name="x">50</parameter>
                    <parameter name="y">50</parameter>
                </parameters>
            </command>
        </commands>
    </format>
</formats>
```

XML Schema
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified"
           targetNamespace="http://schemas.sulu.io/media/formats" xmlns:xs="http://www.w3.org/2001/XMLSchema"
           xmlns="http://schemas.sulu.io/media/formats">

    <xs:complexType name="formatsType">
        <xs:sequence>
            <xs:element type="formatType" name="format" maxOccurs="unbounded" minOccurs="1"/>
        </xs:sequence>
    </xs:complexType>

    <xs:complexType name="formatType">
        <xs:sequence>
            <xs:element type="xs:string" name="name"/>
            <xs:element type="commandsType" name="commands" maxOccurs="unbounded" minOccurs="1"/>
        </xs:sequence>
    </xs:complexType>

    <xs:complexType name="commandsType">
        <xs:sequence>
            <xs:element type="commandType" name="command" maxOccurs="unbounded" minOccurs="1"/>
        </xs:sequence>
    </xs:complexType>

    <xs:complexType name="commandType">
        <xs:sequence>
            <xs:element type="xs:string" name="action"/>
            <xs:element type="parametersType" name="parameters"/>
        </xs:sequence>
    </xs:complexType>

    <xs:complexType name="parametersType">
        <xs:sequence>
            <xs:element type="parameterType" name="parameter" maxOccurs="unbounded"/>
        </xs:sequence>
    </xs:complexType>

    <xs:complexType name="parameterType">
        <xs:simpleContent>
            <xs:extension base="xs:string">
                <xs:attribute type="xs:string" name="name"/>
            </xs:extension>
        </xs:simpleContent>
    </xs:complexType>

    <xs:element name="formats" type="formatsType"/>
</xs:schema>
```

## Format Reader

In the MediaBundle a service reads all formats from the themes and the internal Sulu formats.  
The service outputs the data in this format:

``` php
array(
    array( // one format
        'name' => '50x50', // name of the format
        'commands' => array( // commands to execute
            array(
                'action' => 'scale', // command name
                'parameters' => array( // command parameter
                    'x' => '50',
                    'y' => '50',
                )
            )
        )
    )
)
```

## Sulu formats

Sulu itself have three formats:  
 - `50x50` - Preview in Collection
 - `150x100` - Preview for Collection
 - `170x170` - Content Type

This formats are configured in the SuluMediaBundle.  


## Handling Conflicts

If two themes have the same format, the commands and parameters from the first read will be used.  
So its important the name of the format reflect what the image converter does.
