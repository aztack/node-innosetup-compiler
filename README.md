node-innosetup-compiler
=======================

Node module to compile inno setup scripts (.iss)

This is a simple node wrapper of [Inno Setup](http://www.jrsoftware.org/isinfo.php) compiler: ISCC.exe

### OS Support

##### Windows

Works natively on windows

##### Linux & Mac OS X

Works if [wine](www.winehq.org) is installed

_Note for Mac OS X Users_:
If you get the following error `err:macdrv:process_attach Failed to start Cocoa app main loop`,
you main need to update wine to a more recent version (devel)
```
brew install wine --devel
```

### Usage

_All options are optional_

##### Command line

```shell
npm install -g innosetup-compiler
```

```shell
innosetup-compiler myscript.iss --gui --verbose --signtoolname=signtool --signtoolcommand='"path/to/signtool.exe" sign /f "C:\\absolute\\path\\to\\mycertificate.pfx" /t http://timestamp.globalsign.com/scripts/timstamp.dll /p "MY_PASSWORD" $f'
```

##### Node JS

```shell
npm install innosetup-compiler
```

```javascript
require("innosetup-compiler")("path/to/your/innoscript.iss", {
    gui: false,
    verbose: false,
    signtoolname: 'signtool',
    signtoolcommand: '"path/to/signtool.exe" sign /f "C:\\absolute\\path\\to\\mycertificate.pfx" /t http://timestamp.globalsign.com/scripts/timstamp.dll /p "MY_PASSWORD" $f'
}, function(error) {
    // callback
});
```

##### Grunt

```shell
npm install innosetup-compiler --save-dev
```

```javascript
grunt.loadNpmTasks('innosetup-compiler');
...
grunt.initConfig({
    ...
    "innosetup_compiler": {
        your_target: {
          options: {
            gui: false,
            verbose: false,
            signtoolname: 'signtool',
            signtoolcommand: '"path/to/signtool.exe" sign /f "C:\\absolute\\path\\to\\mycertificate.pfx" /t http://timestamp.globalsign.com/scripts/timstamp.dll /p "MY_PASSWORD" $f'
          },
          script: "path/to/your/innosetup/script.iss"
        }
    }
    ...
});
```

### Options

#### options.verbose
Default: `false`

Print full log output

#### options.gui
Default: `false`

Use Compil32.exe instead or ISCC.exe (GUI mode)

all other options are ignored in this case

#### options.signtoolname and options.signtoolcommand
Default: null

The name and command used to sign installer and uninstaller
See [Innosetup Signtool documentation](http://www.jrsoftware.org/ishelp/index.php?topic=setup_signtool)


### Credits

Thanks to Jordan Russell and Martijn Laan for their amazing work on Inno Setup