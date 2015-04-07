##![Assets](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/assets.png)DET-507 Image Converter

# Image Converter

The Image Converter runs a queue of commands defined for each formats.  
Look at [Image Formats](DET-506-ImageFormats.md "Image Formats") to define a new format.

## Image Converter Commands

### Resize

Resize the image into a specific format. If you don't want distort the image use `scale`.

| Parameter  |   Type        |    Unit      | Description                |
|------------|---------------|--------------|----------------------------|
| x          | integer       |   Pixel      | Image width                |
| y          | integer       |   Pixel      | Image height               |
| retina     | StringBoolean | true/`false` | Multiplied width/height x2 |

Example: 
```xml
<format>
    <name>50x50</name>
    <commands>
        <command>
            <action>resize</action>
            <parameters>
                <parameter name="x">50</parameter>
                <parameter name="y">50</parameter>
                <parameter name="retina">true</parameter>
            </parameters>
        </command>
    </commands>
</format>
```

### Scale

Resize and crop an image into a specific format.

| Parameter  |   Type        |    Unit          | Description                                    |
|------------|---------------|------------------|------------------------------------------------|
| x          | integer       |     Pixel        | Image width                                    |
| y          | integer       |     Pixel        | Image height                                   |
| mode       | String        | inset/`outbound` | The image scale mode                           |
| retina     | StringBoolean | true/`false`     | Multiplied width/height x2                     |
| forceRatio | StringBoolean | `true`/false     | Force image ratio when image is smaller        |
 
Example: 
```xml
<format>
    <name>50x50</name>
    <commands>
        <command>
            <action>scale</action>
            <parameters>
                <parameter name="x">50</parameter>
                <parameter name="y">50</parameter>
                <parameter name="retina">true</parameter>
                <parameter name="forceRatio">true</parameter>
            </parameters>
        </command>
    </commands>
</format>
```


### Crop

Crop an image into a specific format

Parameters:
 - x: x-Coordinate to start crop
 - y: y-Coordinate to start crop
 - w: width of the image
 - h: height of the image
 
| Parameter  |   Type        |    Unit    | Description                                    |
|------------|---------------|------------|------------------------------------------------|
| x          | integer       |   Pixel    | Start position left for crop                   |
| y          | integer       |   Pixel    | Start position top for crop                    |
| w          | integer       |   Pixel    | Image width                                    |
| h          | integer       |   Pixel    | Image height                                   |
 
Example: 
```xml
<format>
    <name>50x50</name>
    <commands>
        <command>
            <action>scale</action>
            <parameters>
                <parameter name="x">50</parameter>
                <parameter name="y">50</parameter>
                <parameter name="w">100</parameter>
                <parameter name="h">100</parameter>
            </parameters>
        </command>
    </commands>
</format>
```
 
 
