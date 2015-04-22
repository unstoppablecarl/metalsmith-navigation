
# metalsmith-navigation [BETA]

  A Metalsmith plugin to generate navigation.

## Installation

    $ npm install metalsmith-navigation

## CLI Usage

  Install via npm and then add the `metalsmith-navigation` key to your `metalsmith.json` plugins.

```json
{
  "plugins": {
    "metalsmith-navigation": {
        navConfigs: {},
        navSettings: {},
    }
  }
}
```

## Javascript Usage

  Pass `options` to the markdown plugin and pass it to Metalsmith with the `use` method:

```js
var navigation = require('metalsmith-navigation');

// default values shown
var navConfigs = {

    // nav config name
    header: {

        /*
        * sortby function or property name
        * function example: function(navNode){ return navNode.getValueToSortBy(); }
        */
        sortBy: false,

        /*
        * if true nodes will be sorted by path before sortBy
        * if false the sorting will not be stable unless ALL nodes have a unique sort value
        */
        sortByNameFirst: true,

        /*
        * to be included in this nav config, a file's metadata[filterProperty] must equal filterValue
        * ex:
        *   navConfigs = {
        *       footer: {
        *           filterProperty: 'my_nav_group'
        *       }
        *   }
        *   file is only added to footer nav when files[path].my_nav_group == 'footer' OR files[path].my_nav_group.indexOf('footer') !== -1
        */
        filterProperty: false,

        /*
        * if false, nav name (navConfigs key) is used instead
        * ex:
        *   navConfigs = {
        *       footer: {
        *           filterValue: 'footer' // default value used if !navConfigs.footer
        *       }
        *   }
        * if files[path][filterProperty] is a string that equals or an array that contains filterValue it will be included
        */
        filterValue: false,

        /*
        * the file object property that breadcrumb array is assigned to on each file object
        * breadcrumbs not generated or set if false
        * typically only one navConfig should generate breadcrumbs, often one specifically for them
        */
        breadcrumbProperty: 'breadcrumb_path',

        /**
        * the file object property that the nav path is assigned to on each file object, not set if false
        */
        pathProperty: 'nav_path',

        /**
        * the file object property that an array of nav child nodes will be assigned to
        */
        childrenProperty: 'nav_children',

        /*
        * if a file and sibling dir have matching names the file will be used as the parent in the nav tree
        * ex: /foo /foo.html
        */
        mergeMatchingFilesAndDirs: true,

        /*
        * if ALL dirs should be included as nav nodes
        */
        includeDirs: false,
    },

    // ... any number of navConfigs may be created

};

// default values shown
var navSettings = {
    /*
    * metadata key all navs will be assigned to metatdata[navListProperty]
    * not set if false
    */
    navListProperty: 'navs',

    /*
    * if true, paths will be transformed to use metalsmith-permalinks
    * metalsmith-permalinks must be run before metalsmith-navigation
    */
    permalinks: false,
};

var nav = navigation(navConfigs, navSettings);

metalsmith.use(nav);

// OR use CLI syntax with single param

var settings = {
    navConfigs: navConfigs,
    navSettings: navSettings,
};
var nav = navigation(settings);
```

## License

  MIT