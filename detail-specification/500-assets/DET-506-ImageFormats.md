##![Assets](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/assets.png)DET-506 Image Formats

# Image Formats

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
        <name>640x480</name>
        <commands>
            <command>
                <action>resize</action>
                <parameters>
                    <parameter name="x">640</parameter>
                    <parameter name="y">480</parameter>
                </parameters>
            </command>
        </commands>

        <options>
            <option name="jpeg_quality">80</option>
            <option name="png_compression_level">6</option>
        </options>
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

            <xs:element type="commandsType" name="commands" minOccurs="0" maxOccurs="1"/>
            <xs:element type="optionsType" name="options" minOccurs="0" maxOccurs="1"/>
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

    <xs:complexType name="optionsType">
        <xs:sequence>
            <xs:element type="parameterType" name="option" maxOccurs="unbounded"/>
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
    '640x480' => array( // one format
        'name' => '', // name of the format
        'commands' => array( // commands to execute
            array(
                'action' => 'scale', // command name
                'parameters' => array( // command parameter
                    'x' => '640',
                    'y' => '480',
                )
            )
        ),
        'options' => array(
             'jpeg_quality' => 100,
             'png_compression_level' => 100
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

## Format Options

The options of a format will be redirected to the imagine library see the documentation. The following options are tested and they work properly with sulu.

* `jpeg_quality`: Quality of jpg-image output
* `png_compression_level`: Compression level of png images (higher value smaller images => slower rendering, lower value bigger images => faster rendering)

The default values of the options can be set in the app config:

```yml
sulu_media:
    format_manager:
        default_imagine_options:
            jpeg_quality: 80
            png_compression_level: 6
```

This is optional, if this is not set the default values of the library will be used.

## Handling Conflicts

If two themes have the same format, the commands and parameters from the first read will be used.  
So its important the name of the format reflect what the image converter does.


## Format Commands

### Resize

#### Parameters
 - x = width
 - y = height
 - retina (auto 2x 'x' and 'y')

### Scale

#### Parameters
 - x = width
 - y = height
 - retina (auto 2x 'x' and 'y')
 - mode (Imagine Thumbnail mode ('inset' or 'outbound'))
 
### Crop

#### Parameters
 - x = startpoint X
 - y = startpoint Y
 - w = width
 - h = height

## Change Path to Formats XML

For every theme you can change the path to the image-formats.xml relative to its theme path:

``` yml
# SULU Media configuration
sulu_media:
    format_manager:
        config_files:
            default: 'config/image-formats.xml'
            mytheme: 'config/sulu/formats.xml'
``` 
