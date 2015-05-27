# Storage
The Media Storage save all documents.
There are currently 2 available types for storage:
 - local (documents are saved local)
 - s3 (documents are saved on s3 storage)

## Local Storage

**Config Parameters:**

``` yml
sulu_media:
    storage:
        local:
            path: "%kernel.root_dir%/../uploads/media" # path where the documents will be saved
            segments: 10 # folder segmentation size
```

## S3

Coming soon!

## Create your own Storage

You need define your own sulu_media.storage service.  
Define a service based on the StorageInterface.

# Format Cache
The Format Cache save thumbnail images is different formats.
Based on the installation it can return thumbnails for none image formats like PDFs.

There are currently 2 available types for storage:
 - local (thumbnails are saved local)
 - reverse_proxy (proxy requested the media controller which return the image in the right format)

## Local

Local format cache save the converted images under the public folder.

**Config Parameters** 

``` yml
sulu_media:
    format_cache:
        save_image: true # if true the image is saved and not converted for every request default is `true`
        segments: 20 # folder segmentation used for the image default is `10`
        path: '%kernel.root_dir%/../web/uploads/media' # where the images are saved in the public folder default is `%assetic.write_to%/uploads/media`
```

**Download**

Download from Local Storage supports 2 different Content-Disposition Types: attachment and inline.
If you want inline you need to add `inline` parameter to the url.

e.g.: `http://sulu.lo/media/1/download/media.jpg?v=1&inline=1`

Also you can download without increase the Downloadcounter by adding `no-count` parameter to the download url.

e.g.: `http://sulu.lo/media/1/download/media.jpg?v=1&no-count=1`

## Reverse Proxy

Coming soon!

## Create your own Format Cache

You need define your own sulu_media.format_cache service.  
Define a service based on the FormatCacheInterface.
