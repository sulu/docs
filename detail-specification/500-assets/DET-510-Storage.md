# Storage

The Media Storage save all documents.
There are 2 available types for storage:
 - local (documents are saved local)
 - flysystem (documents are saved in a flysystem adapter)

**Default Configuration:**

``` yml
sulu_media:
    storage:
        default: local
        adapters:
            local:
                type: local
                segments: 10
                uploadPath: %kernel.root_dir%/../uploads/media
```

## Using Flysystem

Sulu support flysystem over the [OneupFlysystemBundle](https://github.com/1up-lab/OneupFlysystemBundle). You need to [install](https://github.com/1up-lab/OneupFlysystemBundle/blob/master/Resources/doc/index.md) the Bundle first and add it to the AbstractKernel. 

**Configuration (app/config/config.yml)**

``` yml
sulu_media:
    storage:
        adapters:
            default: my_custom
            my_custom:
                type: flysystem
                fileSystem: my_mount_name
                
oneup_flysystem:
    adapters:
        my_adapter:
            local:
                directory: %kernel.root_dir%/cache/media
    filesystems:
        my:
            adapter: my_adapter
            mount: my_mount_name
 ```
 
## Create your own Storage Adapter

First check if there is no [flysystem adapter](https://github.com/1up-lab/OneupFlysystemBundle/blob/master/Resources/doc/index.md) you can use, else you can define your own service based on the `StorageInterface` and tag it with `sulu_media.storage_adapter` and an alias or create an own flysystem adapter.

## Multiple Storages

You can configured multiple storage adapters. It is possible to set the default storage adapter foreach collection.

Example Config:

``` yml
sulu_media:
    storage:
        adapters:
            local:
                type: local
                segments: 10
                uploadPath: %kernel.root_dir%/../uploads/media
            dropbox:
                type: flysystem
                fileSystem: my_mount_name

oneup_flysystem:
    adapters:
        my_adapter:
            local:
                directory: %kernel.root_dir%/cache/media
    filesystems:
        my:
            adapter: my_adapter
            mount: my_mount_name
```

# Format Cache
The Format Cache save thumbnail images is different formats.
Based on the installation it can return thumbnails for none image formats like PDFs.

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

If you use a reverse proxy cdn you can turn of image save:

``` yml
sulu_media:
    format_cache:
        save_image: false
```

Configurate the CDN domain for your production environment (app/config/website/config_prod.yml):

```  yml
framework:
    templating:
        assets_base_urls:
            http: ['http://cdn.sulu.io']
```

## Create your own Format Cache

You need define your own `sulu_media.format_cache` based on the `FormatCacheInterface`.
