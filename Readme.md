# Important

The current gem is released without updated plugins. If you encounter any errors, please fork the repository, update the plugin files and send a pull-request.

# jquery-datatables-rails

This gem packages the jQuery [DataTables](http://datatables.net/) plugin for easy use with the Rails 3.1+ asset pipleine.

It provides all the basic DataTables files, and a few of the extras.

## General Installation

1. Add to your Gemfile:

        gem 'jquery-datatables-rails', git: 'git://github.com/rweng/jquery-datatables-rails.git'

1. Install the gem:

        bundle install

1. Add the JavaScript to `application.js`:

        //= require dataTables/jquery.dataTables

1. Add the stylesheets to `application.css`:

        *= require dataTables/jquery.dataTables

## Upgrading from version before 1.12.2
All file names has changed for beeing compatible with the current DataTables project (v 1.10.). Please update the path to the files in your `application.js` and `application.css`. The new paths for bootstrap can be found below.
If you want to use the old dataTables (v.1.9.4) plese don't upgrade behind version 1.12.2. so your Gemfile contain this:
  ```
  gem 'jquery-datatables-rails', '~> 1.12.2'
  ```

## Twitter Bootstrap 2 Installation

1. Complete steps 1-3 of the General Installation
1. Add some more JavaScript to `application.js`:

        //= require dataTables/bootstrap/2/dataTables.bootstrap

1. Add this (and only this) stylesheet to `application.css`:

        *= require dataTables/bootstrap/2/dataTables.bootstrap

1. Initialize your datatables using one of these options:

```javascript
// For fluid containers
$('.datatable').dataTable({
  "sDom": "<'row-fluid'<'span6'l><'span6'f>r>t<'row-fluid'<'span6'i><'span6'p>>",
  "sPaginationType": "bootstrap"
});
```
```javascript
// For fixed width containers
$('.datatable').dataTable({
  "sDom": "<'row'<'span6'l><'span6'f>r>t<'row'<'span6'i><'span6'p>>",
  "sPaginationType": "bootstrap"
});
```


## Twitter Bootstrap 3 Installation

1. Complete steps 1-3 of the General Installation
1. Add some more JavaScript to `application.js`:

        //= require dataTables/bootstrap/3/dataTables.bootstrap


1. Add this (and only this) stylesheet to `application.css`:

        *= require dataTables/bootstrap/3/dataTables.bootstrap

1. Initialize your datatables using these option:

```javascript
$('.datatable').dataTable({
  "sPaginationType": "bootstrap"
});
```


## Zurb Foundation Installation

1. Complete steps 1-3 of the General Installation

1. Add some more JavaScript to `application.js`:

        //= require dataTables/foundation/dataTables.foundation

1. Add this (and only this) stylesheet to `application.css`:

        *= require dataTables/foundation/dataTables.foundation

1. Initialize your datatables using these option:

```javascript
$('.datatable').dataTable({
  "sPaginationType": "foundation"
});
```

## Responsive Installation

1. Complete steps 1-3 of the General Installation
1. Add the lodash gem to your application:

    ```
      gem 'lodash-rails'
    ```

1. Add some more JavaScript to `application.js`:

        //= require dataTables/bootstrap/3/dataTables.bootstrap
        //= require dataTables/responsive/datatables.responsive

1. Add this (and only this) stylesheet to `application.css`:

        *= require dataTables/bootstrap/3/jquery.dataTables.bootstrap
        *= require dataTables/responsive/datatables.responsive.css

1. Initialize your datatables using:

```coffeescript
  responsiveHelper = undefined
  breakpointDefinition =
    tablet: 1024
    phone: 480

  tableContainer = $('.datatable')
  tableContainer.dataTable

    sPaginationType: "bootstrap"
    # Setup for responsive datatables helper.
    bAutoWidth: false
    bStateSave: false

    fnPreDrawCallback: ->
      responsiveHelper = new ResponsiveDatatablesHelper(tableContainer, breakpointDefinition) unless responsiveHelper

    fnRowCallback: (nRow, aData, iDisplayIndex, iDisplayIndexFull) ->
      responsiveHelper.createExpandIcon nRow

    fnDrawCallback: (oSettings) ->
      responsiveHelper.respond()
```

1. To use see the author of responsive files and follow the instructions as described on [datatables-responsive]

## Plugins

Only a few plugins are currently available

* api
    * fnReloadAjax
    * fnGetColumnData
    * fnFilterOnReturn
    * fnSetFilteringDelay
* sorting
    * numbersHtml
* typeDetection
    * numberHtml

These files can be found in the [assets directory][assets].

## Extras

Only the official extras are available:

* AutoFill
* ColReorder
* ColVis
* FixedColumns
* FixedHeader
* KeyTable
* Scroller
* TableTools

To add an extra into your application, add its JS file to `application.js` using the following pattern:

    //= require dataTables/extras/dataTables.[ExtraName]

Additionally, you may need to add any associated CSS files. For instance the TableTools extra requires
you to add the following two lines to your `application.css` file:

    *= require dataTables/extras/dataTables.TableTools
    *= require dataTables/extras/dataTables.TableTools_JUI

TableTools also requires this to be included in 'application.js':

    //= require dataTables/extras/dataTables.ZeroClipboard.js

Make sure to also add it's initialization as described on [datatables extras' site][datatables_extras]

## Articles

[RailsCast #340 DataTables] Apr 11, 2012.

## Thanks

Thanks to Comanche for responsive support files [datatables-responsive]

[assets]: https://github.com/rweng/jquery-datatables-rails/tree/master/vendor/assets/javascripts/dataTables
[datatables_extras]: http://datatables.net/extras/
[datatables-responsive]: https://github.com/Comanche/datatables-responsive
[RailsCast #340 DataTables]: http://railscasts.com/episodes/340-datatables
