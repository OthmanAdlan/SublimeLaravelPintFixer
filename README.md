# Sublime Laravel Pint Fixer
This is a plugin for Sublime Text 3/4, to format PHP code through [Laravel Pint](https://laravel.com/docs/pint) command on any view.

ported from the Awesome SublimePhpCsFixer package of [@adael](https://github.com/adael)

# Features

* It works inside a temporal view (ie: on an new, non-saved file)
* Fast
* Easy
* Configurable through config file
* Tested on Windows, Linux, and Mac

# Configuration

You have to install `laravel/pint` (the actual package made by Laravel, not this plugin)

You can install `laravel/pint` package directly with composer by running:

    composer global require laravel/pint

Also you can create a config file as explained here https://laravel.com/docs/pint#configuring-pint

*for example in:* `$HOME/pint.json`

```js
{
    "preset": "laravel",
    "rules": {
        "simplified_null_return": true,
        "braces": false,
        "new_with_braces": {
            "anonymous_class": false,
            "named_class": false
        }
    }
}
```

If you've created a config file, you have to configure its path in the plugin's settings.

*In Menu -> Preferences -> Package Settings -> Laravel Pint Fixer -> Settings - user*

```js
{
    "config": "/path/to/pint.json"
}
```

When using multiple projects with different configurations, it's possible to
configure the path relative to the Sublime project folder:

```js
{
    "config": "${folder}/pint.json",
    "php": "${packages}/User/php",
    "path": "${packages}/User/pint"
}
```

It's also possible to specify multiple config paths. In that case, the first readable file is used:

```js
{
    "config": [
        "${file_path}/pint.json",
        "${folder}/pint.json",
        "/path/to/pint.json"
    ]
}
```

See [`extract_variables` in the Sublime API Reference](https://www.sublimetext.com/docs/3/api_reference.html#sublime.Window)
for the supported replacement variables. The value of the `${folder}` points
the path of the first project in Sublime API. Here, it's beforehand replaced
with the path of the project the target file belongs.

Please note:

* **`config` directive is excluding.**
* This plugin don't try to find the config file automatically. If you want to
create a config file, you have to specify its path in the plugin settings.

For more information see: https://laravel.com/docs/pint#configuring-pint

## Exclude files

Since all php files are passed directly to the laravel pint executable, a configured PhpCsFixer\\Finder gets ignored.
In order to exclude files from pint, you can use the "exclude" setting:

```js
{
    "exclude": [
        ".*[\\\\/]vendor[\\\\/].*", // vendor-path (used by Composer)
        ".*\\.phtml$" // files ending with ".phtml"
    ]
}
```

The exclude-filter uses python regular expressions.
For more information see: https://docs.python.org/2/library/re.html


### On Windows:

The plugin tries to find the executable in:

    %APPDATA%\composer\vendor\bin\pint.bat

If it isn't working, you can locate your composer global packages path by running:

    composer config -g home

### On Linux:

After installing larave/pint you have to specify the full path to the
executable in the configuration page.

The plugin tries to find the executable in:

    $HOME/.composer/vendor/bin/pint

However, if it isn't working, you can create a symbolic link to the pint executable

    ln -s $HOME/.composer/vendor/bin/pint $HOME/bin/pint


# Acknowledgements

I would like to thank to adael, sensiolabs and contributors for their awesome package.
It works flawlessly. All the work here belongs to them.

Check them at:
* https://github.com/adael
* https://github.com/FriendsOfPHP/PHP-CS-Fixer
* http://cs.sensiolabs.org/
