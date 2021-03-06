# crxde-pipe

## CLI

Install `crxde-pipe` from sources:
```sh
$ git clone https://github.com/fortywinkz/crxde-pipe.git
$ cd crxde-pipe
$ npm install
$ npm link
```

Run:
```bash
crxde-pipe path/to/project/src
```

Enable debugging:
```bash
DEBUG=* crxde-pipe path/to/project/src
```
Also you can specify debugging target:
```bash
DEBUG=app:error crxde-pipe path/to/project/src
```
_For more information see [docs](#module_logger) and [debug](https://github.com/visionmedia/debug) project_

Options:
```bash
crxde-pipe -h

    Usage: crxde-pipe [options] <dir...>

    Options:

    -h, --help                    output usage information
    -V, --version                 output the version number
    -m, --match [regex]           Regex for matching CQ path
    -i, --ignore [regex]          Regex for excluding files from watching
    -I, --interval [ms]           Interval of watching
    -s, --server [host:port]      CQ (CRXDE) server
    -d, --dispatcher [host:port]  Dispatcher server
    -P, --preprocess              Enables preprocessors
```

## API


###Index

**Modules**

* [crxde-pipe](#module_crxde-pipe)
  * [crxde-pipe.pipe(paths, options)](#module_crxde-pipe.pipe)
* [logger](#module_logger)
  * [logger.log](#module_logger.log)
  * [logger.error](#module_logger.error)
  * [logger.preproc](#module_logger.preproc)
  * [logger.update](#module_logger.update)
  * [logger.create](#module_logger.create)
  * [logger.remove](#module_logger.remove)
* [preproc](#module_preproc)
  * [preproc.isFileCanBePreproc](#module_preproc.isFileCanBePreproc)
  * [preproc.preproc](#module_preproc.preproc)

**Classes**

* [class: CRXDE](#CRXDE)
  * [new CRXDE([options])](#new_CRXDE)
  * [cRXDE.pipe(paths, [options])](#CRXDE#pipe)
  * [cRXDE.preproc(path)](#CRXDE#preproc)
  * [cRXDE.add(path, type)](#CRXDE#add)
  * [cRXDE.update(path, resource)](#CRXDE#update)
  * [cRXDE.remove(path)](#CRXDE#remove)
  * [cRXDE.flush([path])](#CRXDE#flush)

**Typedefs**

* [type: Server](#Server)
 
<a name="module_crxde-pipe"></a>
###crxde-pipe
Expose a single function to pipe source files to CQ (CRXDE)

<a name="module_crxde-pipe.pipe"></a>
####crxde-pipe.pipe(paths, options)
Pipe source files to CQ (CRXDE)

**Params**

- paths `Array`  
- options `Object`  

**Returns**: [CRXDE](#CRXDE)  
<a name="module_logger"></a>
###logger
Expose logging targets

**Members**

* [logger](#module_logger)
  * [logger.log](#module_logger.log)
  * [logger.error](#module_logger.error)
  * [logger.preproc](#module_logger.preproc)
  * [logger.update](#module_logger.update)
  * [logger.create](#module_logger.create)
  * [logger.remove](#module_logger.remove)

<a name="module_logger.log"></a>
####logger.log
`app:log` Target for base logging

<a name="module_logger.error"></a>
####logger.error
`app:error` Target for logging errors

<a name="module_logger.preproc"></a>
####logger.preproc
`app:preproc` Target for logging preprocessing

<a name="module_logger.update"></a>
####logger.update
`crxde:update` Target for logging updates of file on CQ (CRXDE)

<a name="module_logger.create"></a>
####logger.create
`crxde:create` Target for logging uploads of file to CQ (CRXDE)

<a name="module_logger.remove"></a>
####logger.remove
`crxde:remove` Target for logging removal of file from CQ (CRXDE)

<a name="module_preproc"></a>
###preproc
Expose preprocessing functions

**Members**

* [preproc](#module_preproc)
  * [preproc.isFileCanBePreproc](#module_preproc.isFileCanBePreproc)
  * [preproc.preproc](#module_preproc.preproc)

<a name="module_preproc.isFileCanBePreproc"></a>
####preproc.isFileCanBePreproc
Checks if file could be preprocessed

**Params**

- path `string` - Path to file in file system  

**Returns**: `boolean`  
<a name="module_preproc.preproc"></a>
####preproc.preproc
Runs preprocessing

**Params**

- path `string` - Path to file in file system  

<a name="CRXDE"></a>
###class: CRXDE
**Members**

* [class: CRXDE](#CRXDE)
  * [new CRXDE([options])](#new_CRXDE)
  * [cRXDE.pipe(paths, [options])](#CRXDE#pipe)
  * [cRXDE.preproc(path)](#CRXDE#preproc)
  * [cRXDE.add(path, type)](#CRXDE#add)
  * [cRXDE.update(path, resource)](#CRXDE#update)
  * [cRXDE.remove(path)](#CRXDE#remove)
  * [cRXDE.flush([path])](#CRXDE#flush)

<a name="new_CRXDE"></a>
####new CRXDE([options])
Provides piping of source code to CQ (CRXDE)

**Params**

- \[options\] `Object` - Watching options  
  - match `RegExp` - Matches root path of CQ files. Default: `/jcr_root(.*)$/`  
  - ignore `RegExp` - Matches files which will be ignored from watching. Default: `/\.git|\.sass-cache|\.hg|\.idea|\.svn|\.cache|\.project|___jb__bak___|Thumbs.db$|ehthumbs.db$|Desktop.ini$|\$RECYCLE.BIN/`  
  - interval `number` - Watching interval. Default: `500`  
  - server <code>[Server](#Server)</code> - Server of CRXDE instance. Default: `{ host: 'localhost': port: 4502 }`  
  - dispatcher <code>[Server](#Server)</code> - Server of dispatcher instance. Needed for flushing a cache. Default: false  
  - auth `string` - Authentication data for CRXDE instance. Default: `admin:admin`  

<a name="CRXDE#pipe"></a>
####cRXDE.pipe(paths, [options])
Syncs files from source code to CQ (CRXDE)

**Params**

- paths `Array` - Watching paths  
- \[options\] `Object` - Watching options  

**Returns**: [CRXDE](#CRXDE)  
<a name="CRXDE#preproc"></a>
####cRXDE.preproc(path)
Runs preprocessing

**Params**

- path `string` - Path to file in file system  

<a name="CRXDE#add"></a>
####cRXDE.add(path, type)
Uploads a new file to CQ (CRXDE)

**Params**

- path `string` - Path to file (relative to root)  
- type `string` - Type of file (nt:file, nt:folder, etc.)  

**Returns**: [CRXDE](#CRXDE)  
<a name="CRXDE#update"></a>
####cRXDE.update(path, resource)
Updates a file on CQ (CRXDE)

**Params**

- path `string` - Path to file (relative to root)  
- resource `string` - Path to file in file system  

**Returns**: [CRXDE](#CRXDE)  
<a name="CRXDE#remove"></a>
####cRXDE.remove(path)
Removes a file from CQ (CRXDE)

**Params**

- path `string` - Path to file (relative to root)  

**Returns**: [CRXDE](#CRXDE)  
<a name="CRXDE#flush"></a>
####cRXDE.flush([path])
Flushes cache on CQ (CRXDE)

**Params**

- \[path\] `string` - Path to file (relative to root)  

**Returns**: [CRXDE](#CRXDE)  
<a name="Server"></a>
###type: Server
**Type**: `Object`  


*documented by [jsdoc-to-markdown](https://github.com/75lb/jsdoc-to-markdown)*
