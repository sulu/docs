##![Assets](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/assets.png)DET-507 Image Converter

# Image Converter

The Image Converter runs a queue of commands defined for each formats.  
Look at [Image Formats](DET-506-ImageFormats.md "Image Formats") to define a new format.

## Image Converter Commands

### Resize

Resize the image into a specific format. If you don't want distort the image use `scale`

Parameters:
 - x: width in Pixel
 - y: height in Pixel
 
Example: 
```xml
<format>
    <name>50x50</name>
    <commands>
        <command>
            <action>resize</action>
            <parameters x="50" y="50" />
        </command>
    </commands>
</format>
```

### Scale

Resize and crop an image into a specific format.

Parameters:
 - x: width in Pixel
 - y: height in Pixel
 
Example: 
```xml
<format>
    <name>50x50</name>
    <commands>
        <command>
            <action>scale</action>
            <parameters x="50" y="50" />
        </command>
    </commands>
</format>
```
