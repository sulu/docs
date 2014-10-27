# Adding Cache Headers to Images

Cache Headers should be set in the vhost file of your Server Configuration.

Examples can be found [here](https://github.com/sulu-cmf/docs/blob/master/developer-documentation/000-foundation/vhost.md)

That the first request also has the correct Cache Headers you must set them in the parameters.yml.

``` yml
    format_manager.response_headers:
        Expires: "+1 month"
        Pragma: "public"
        Cache-Control: "public"
``` 
