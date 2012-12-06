## Installing grunt

Grunt is now split into three parts: `grunt`, `grunt-cli` and `grunt-init`

1. `grunt` is the core library that gets installed locally to your project. It contains all the code and logic for running tasks, loading plugins, etc. Install locally, along with grunt plugins, per the [[Getting started]] guide.

2. `grunt-cli` is installed globally, giving you the `grunt` command in your shell. It doesn't do anything by itself, but will run a project's locally-installed grunt using the project's Gruntfile. Install globally, per the [[Getting started]] guide.  For more information about why this has changed, please read [npm 1.0: Global vs Local installation](http://blog.nodejs.org/2011/03/23/npm-1-0-global-vs-local-installation).

3. `grunt-init` has been broken into a separate [grunt-init](/gruntjs/grunt-init) utility that may be installed globally with `npm install -g grunt-init` and run with the `grunt-init` command.  In the coming months, [Yeoman](http://yeoman.io/) will completely replace grunt-init.  See the [grunt-init project page](/gruntjs/grunt-init) for more information.

## Pre-existing tasks and plugins
All `grunt-contrib-*` series plugins are grunt 0.4 ready.  However, it is highly unlikely that third party plugins written for grunt 0.3 will continue to work with 0.4 until they have been updated.  We are actively working with plugin authors to ensure this happens as swiftly as possible.

*The next major release will be focused on decoupling grunt's architecture so that plugins are not affected by future updates.  Please bear with us!*

## The Gruntfile
The Gruntfile filename has changed from `grunt.js` to `Gruntfile.js` or `Gruntfile.coffee` (transpiling to JS happens automatically).

See the "The Gruntfile" section of the [[Getting started]] guide for more information.

## Core Tasks are now Grunt Plugins
The eight core tasks that were included in grunt 0.3 are now separate grunt plugins. Each is a discreet npm module that must be installed as a plugin per the "Loading grunt plugins and tasks" section of the [[Getting started]] guide.

* concat → [grunt-contrib-concat](/gruntjs/grunt-contrib-concat) plugin
* init → stand-alone [grunt-init](/gruntjs/grunt-init) utility
* lint → [grunt-contrib-jshint](/gruntjs/grunt-contrib-jshint) plugin
* min → [grunt-contrib-uglify](/gruntjs/grunt-contrib-uglify) plugin
* qunit → [grunt-contrib-qunit](/gruntjs/grunt-contrib-qunit) plugin
* server → [grunt-contrib-connect](/gruntjs/grunt-contrib-connect) plugin
* test → [grunt-contrib-nodeunit](/gruntjs/grunt-contrib-nodeunit) plugin
* watch → [grunt-contrib-watch](/gruntjs/grunt-contrib-watch) plugin

Some task names have changed, and specifying options and files has been standardized in grunt 0.4, so be sure to see each plugin's documentation as linked above for the latest configuration details.

## Task configuration
The configuration format for grunt 0.4 has been standardized and greatly enhanced.

See the [[Configuring tasks]] guide as well as individual plugin documentation for more information.

## Alias task changes
When specifying an alias task, the list of tasks to run must now be specified as an array.

```js
// v0.3.x (old format)
grunt.registerTask('default', 'jshint nodeunit concat');
// v0.4.x (new format)
grunt.registerTask('default', ['jshint', 'nodeunit', 'concat']);
```

## Task arguments may now contain spaces
The aforementioned alias task change (task lists must be specified as an array) makes this possible. Just be sure to surround task arguments containing spaces with quotes when specifying them on the command line, so they can be properly parsed.

```shell
grunt my-task:argument-without-spaces "other-task:argument with spaces"
```

## Helpers
Grunt's helper system has been removed in favor of node `require`.  For a concise example on how to share functionality between gruntplugins, please see [grunt-lib-legacyhelpers](/gruntjs/grunt-lib-legacyhelpers).

## Configuration changes
`<% %>` style template strings specified as config data inside the Gruntfile are automatically expanded, see the [[grunt.template]] documentation for more information.

Directives have been removed, but their functionality has been retained. These replacements can be made:

* `'<config:prop.subprop>'` → `'<%= prop.subprop %>'`
* `'<json:file.json>'` → `grunt.file.parseJSON('file.json')`
* `'<file_template:file.js>'` → `grunt.template.process(grunt.file.read('file.js'))`

Instead of specifying a banner in a file list with `'<banner>'` or `'<banner:prop.subprop>'`, the [grunt-contrib-concat](/gruntjs/grunt-contrib-concat) and [grunt-contrib-uglify](/gruntjs/grunt-contrib-uglify) plugins each have a `banner` option.

Instead of stripping banners from files individually with `'<file_strip_banner:file.js>'`, the [grunt-contrib-concat](/gruntjs/grunt-contrib-concat) and [grunt-contrib-uglify](/gruntjs/grunt-contrib-uglify) plugins each have an option to strip/preserve banners.

## Troubleshooting tips

* If you have ever previously installed grunt 0.4.0 or any of the grunt-contrib plugins from npm, flush your npm cache with `npm cache clear` to ensure that you are pulling the latest, released versions.