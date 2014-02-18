# DET 310 Navigation

## NavigationMapper Service
ID: sulu_website.navigation_mapper

__getNavigation__

* parent: parent page of navigation
* webspace: current webspace key
* language: current language code
* depth: depth of navigation (null infinity depth)
* preview: if true test pages are visible

__getMainNavigation__

same as __getNavigation__ without parent (parent is root page).

## NavigationItem

* Navigation is an array of NavigationItems
* NavigationItem contains
  * url: url to this page
  * title: title attribute
  * content: content node behind navigation item
  * children: sub NavigationItems
  
