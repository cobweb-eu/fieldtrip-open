### Projects

A project is instance of fieldtrip open. It contains a theme and a list of plugins it wishes to enable.

### Theme ###

A fieldtrip theme contains two stylesheets:

* A jQuery Mobile theme, preferably create by [ThemeRoller](http://themeroller.jquerymobile.com/). The stylesheet will be found at: theme/css/jqm-style.css
* A stylesheet for overriding the [core stylesheet](https://github.com/edina/fieldtrip-open/blob/master/src/www/css/style.css). It will be found at: theme/css/style.css

### Plugins

The json file theme/plugins.json will define a list of plugins the project wishes to enable. The following is an example:

```
{
    "cordova": [
        "cordova-plugin-device.git",
        "cordova-plugin-geolocation.git",
        "cordova-plugin-camera.git",
        "cordova-plugin-media-capture.git",
        "cordova-plugin-media.git",
        "cordova-plugin-file.git",
        "cordova-plugin-console.git"
    ],
    "fieldtrip": {
        "offline-maps": "",
        "ft-sync", "1.0.1",
        "my-plugin": "git@github.com:gmh04/fieldtrip-plugins-test.git",
    }
}
```

#### Cordova

[Cordova plugins documentation](http://cordova.apache.org/docs/en/3.3.0/guide_hybrid_plugins_index.md.html#Plugin%20Development%20Guide_native_interfaces)

#### Fieldtrip

* offline-maps: will use the master branch of the plugin found at: [https://github.com/edina/fieldtrip-plugins](https://github.com/edina/fieldtrip-plugins).
* ft-sync: will install the plugin as a [bower](http://bower.io/) dependency.
* my-plugin: will use the master branch of the plugin found at the defined git repository.

For details on fieldtrip plugin development see [plugin development documentation](PLUGINS.md).

### Templates

All HTML in fieldtrip open is [templated](https://github.com/edina/fieldtrip-open/tree/master/src/templates) with the core providing bare bone templates and data json files as a starting point for a project. In addition, plugins can also provide templates and default data files for new pages that they wish to introduce to the app. It is the role of the project to provide the content of the main landing pages that diverge from the default layout.

#### Add New Button

A project can add a new button to the _Home_ page by adding an index.json to src/templates. The following json object adds a _Saved_ button that will open saved-maps.html when clicked:

```
{
    "body": {
        "section1": {
            "items": {
                "item2": {
                    "div": {"class": "ui-block-b"},
                    "a": {"href": "saved-maps.html"},
                    "img": {"src": "css/images/saved.png", "alt": "Save Map"},
                    "title": "Saved"
                }
            }
        }
    }
}
```

* section1: refers to the _Maps_ section of the _Home_ page
* item2: is the id of the button and should be unique if the button is new or the same if replacing an existing button
* ui-block-b: places the button in the second column of the section, see [JQM Grid Layout docs](http://api.jquerymobile.com/grid-layout/#Grid%20Layout)

A project can add a new button to the _Capture_ page by adding an capture.json in src/templates.

#### Add Header Button

A project can add a new button to the main header of the app by adding the following to the page json file where it should appear:

```
{
    "header": {
        "buttons" : {
            "exit": {
                "id": "home-exit",
                "data-role": "button",
                "data-inline": "true",
                "data-transition": "none",
                "value": "Exit"
            }
        }
    }
    ...
}
```

#### Add New Footer Tab

A project can add a new footer new tab, and landing page for the tab, by providing a footer.json in src/templates. The following json object adds a _Download_ tab that will open download.html when clicked:

```
{
    "download": {
        "name": "Download",
        "href": "download.html",
        "class": "download-button",
        "data-icon": "custom"
    }
}
```

#### Add Records Header Button

TODO

#### Generate HTML

The generate_html fabric task will need to be run after a change to templates or data files:

```
fab generate_html
```

### Examples

* [Basic Example](https://github.com/edina/fieldtrip-example)
* [Fieldtrip GB](https://github.com/edina/fieldtrip-gb)
* [COBWEB](https://github.com/edina/fieldtrip-cobweb)