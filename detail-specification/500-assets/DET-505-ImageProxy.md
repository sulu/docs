##![Assets](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/assets.png)DET-505 Image Proxy

#Image Proxy Objects

 - **Website Media Controller**
  - `+ getImageAction(url)`
 - **Format Manager**
   - `+ returnImage(id, format)`
   - `+ getMediaProperties(url)` : id, format
 - **Image Converter**
   - `+ convert(originalPath, format)`
 - **Format Cache**
   - `+ save(tmpPath, id, fileName, options)`
   - `+ purge(id, fileName, options)`
   - `+ getMediaUrl(media, format)` : url
   - `+ analyzeMediaUrl(url)` : id, format

#Process

![Assets database diagram](https://raw.github.com/massiveart/sulu-docs/master/detail-specification/images/diagrams/ImageProxy.png)
