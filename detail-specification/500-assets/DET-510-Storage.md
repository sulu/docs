# Storage
The Media Storage save all documents. Which service is used can be defined in app/config/media/storage.yml
There are currently 3 available types for storage:
 - local (documents are saved local)
 - s3 (documents are saved local and s3 is used as reverse proxy)
 - custom (you need define your own sulu_media.storage service based on the StorageInterface)

# Format Cache
The Format Cache save thumbnail images is different formats.
Based on the installation it can return thumbnails for none image formats like PDFs.
Which service is used can be defined in app/config/media/format_cache.yml
There are currently 3 available types for storage:
 - local (thumbnails are saved local)
 - s3 (thumbnails are saved local and s3 is used as reverse proxy)
 - custom (you need define your own sulu_media.format_cache service based on the FormatCacheInterface)
