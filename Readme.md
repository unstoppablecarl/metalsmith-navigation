
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
        *   navConfigs key = 'footer'
        *   filterProperty = 'nav_group'
        *   files only added if files[path].nav_group == 'footer'
        */
        filterProperty: false,

        /*
        * if false nav name (navConfigs key) used instead
        * if files[path][filterProperty] equals or contains (string or array containing) filterValue
        * it will be included
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
        * if dirs should be included as nav nodes
        * has no effect if mergeMatchingFilesAndDirs = true
        */
        includeDirs: true,
    },

    // ...

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

var nav = navigation(navConfig, navSettings);

metalsmith.use(nav);
```

## License

  MIT