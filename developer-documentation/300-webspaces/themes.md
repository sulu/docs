# Themes
## Stucture
The themes are split into two parts: one is responsible for the public part (`<bundle>/Resources/public/<theme>`) and one for twig-Templates (`<bundle>/Resources/themes/<theme>/`).

### Public
The public part contains all the images, javascripts, css files, and all the other files which should be delivered by the webserver.

There are the folders `css`, `fonts`, `images` and `js` in the `<bundle>/Resources/` (that's not a strict template, as you have to reference these file on your own anyway). 

However, there are some restrictions, which will be explained in the next sections:
Only use absolute paths from the `/web`-directory, because the files won't be referenced correctly otherwise. So you should use paths like `/bundles/<bundle>/...`.
Another restriction is that references on images or fonts won't be automatically copied by Symfony, so you have to execute `app/console assets:install` manually, if something about the assets has changes.

Addiotionally it is recommended to put other CSS or JS-Frameworks into the folder `/web/public`, which is the only place where relative urls are working.

### Templates
Put all the twig-Templates into the `templates` and `views` folder in the `<bundle>/Resources/themes/<theme>`-folder. The convention is that all templates defined in Sulu should have a reference to one of the twig-templates in the `templates`-folder, and all other twig-templates, like any blocks, go into the `views`-folder.

## Usage
Because we use [Assetic](http://symfony.com/doc/current/cookbook/assetic/asset_management.html) for Asset Management, all the assets should be at the newest version while you are developing in the `dev`-environment.
When you are in production you have to resolve all the assets with the `app/console assetic:dump --env=prod --no-debug`-command, otherwise all your asset references won't resolve.
