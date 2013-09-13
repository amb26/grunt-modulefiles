# grunt-local-module

> Builds local project modules. Usseful for breaking up a single project into several modular parts which can be assembled in various configurations.

## Getting Started
This plugin requires Grunt `~0.4.1`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-local-module --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-local-module');
```

## The "local_module" task

### Overview
In your project's Gruntfile, add a section named `local_module` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  local_module: {
    your_target: {
      options: {
        // Target-specific options go here.
      },
      src: []// Target-specific file lists go here.
    },
  },
})
```

The `local_module` task will look for json dependency files in your project matching the specified file pattern.
These json dependency files hold the name of the module, which other modules it depends on and which files it
includes. The included files and dependencies should all be listed in the order of their dependence.

```json
{
  moduleC: {
    files: ["file1.js", "file2.js"],
    dependencies: ["moduleA", "moduleB"]
  }
}

```

### Options

#### options.configProp
Type: `String`
Default value: `pkgfiles`

A string value reprsenting the path in the grunt config where the output should be stored.
This can later be accessed either through grunt.config.get(prop) or "<%= prop %>"

#### options.exclude
Type: `String or Array`
Default value: `[]`

Either an array or comma separated string listing the modules to be excluded from the set of depencies.

#### options.include
Type: `String or Array`
Default value: `null`

Either an array or comma separated string listing the modules to be included in the set of dependencies.
If the value is falesy the entire set of modules, minus exclusions (see option.exlude), will be used.

### Usage Examples

#### Default Options
In this example all of the modules specifed in the dependency files matching the given pattern are used to
construct the set of dependency files. The list of files is stored in the 'pkgfiles' config property.

```js
grunt.initConfig({
  local_module: {
    all: {
      src: ["**/*Dependencies.json"]
    }
  },
})
```

#### Custom Options
In this example the dependencies for "moduleA" and "moduleB" are included but those for "moduleC" and
"moduleD" are removed. The resulting set of dependency files is stored at "package.files" config property.

```js
grunt.initConfig({
  local_module: {
    some: {
      options: {
        exclude: ["moduleC", "moduleD"],
        include: "moduleA, moduleB",
        configProp: "package.files"
      },
      src: ["**/*Dependencies.json"]
    }
  },
})
```

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [Grunt](http://gruntjs.com/).

## Release History
_(Nothing yet)_
