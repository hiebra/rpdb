# com.softalks.debug
Easy remote debugging for Python 3 under Linux & [Eclipse PyDev](https://www.pydev.org/)/[LiClipse](https://www.liclipse.com/)
## Requirements
To debug your module (after installing this component on your [pip](#pip)/[Kodi](#Kodi) environment) you will need to: 
1. Set the environment variable PYDEVD to your Eclipse home directory (a Launch Configuration referencing `${eclipse.home}` is recomended)
1. Define one or more breakpoints on your module using the PyDev Python editor
1. Start the PyDev debug server (your module will only stop while the server is running)
1. If not done for any importing or imported module, add the line `__import__('com.softalks.debug')` at the start of your module 
1. Run the proper use case of the external program loading your module
1. Wait a few seconds until execution stops
1. Execution should pause at line 29 of `debug.py`. Press F8 to jump to your first breakpoint
> All modules with the namespace `com.softalks` are debuggable by design. If your module (or any loaded module importing yours) impots any module of that namespace, you can ignore the fourth requirement

> The last requirement will disappear, [if possible](https://github.com/hiebra/rpdb/issues/1), in a next version
## pip
> Under Ubuntu 22.04 ensure the environment variable `DEB_PYTHON_INSTALL_LAYOUT` has the value `deb_system` before using pip to install/uninstall this package (click [here](https://github.com/pypa/setuptools/issues/3269#issuecomment-1254507377) for details)
### Install
> To be able to install this package with pip you need to install `git` first

An example of installing a specific version (0.0.1):
```
pip3 install https://github.com/hiebra/rpdb/archive/refs/tags/v0.0.1.zip
```
To install the last one:
```
pip3 install https://github.com/hiebra/101-py/archive/refs/heads/main.zip
```
You can also install it indirectly by a reference from a depending component's `pyproject.toml`:
```
[project]
...
dependencies = [
    "com.softalks.debug @ https://github.com/hiebra/rpdb/archive/refs/tags/v0.0.1.zip"
]
```
### Uninstall
```
pip3 uninstall com.softalks.debug
```
## Kodi
To install this module in [Kodi](https://kodi.tv/) you need to:
* install (from zip file) this [addon repository](https://github.com/hiebra/repository.github/releases/latest)
* install any addon with an `addon.xml` declaring its dependency on this component like this:

  ```
  <import addon="script.module.debug.softalks.com" version="0.0.1"/>
  ```
  > Note that the addon attribute is not equal to the module name (it has been adapted to follow the Kodi naming guidelines). The version attribute is also different from the version tag: `0.0.1` instead of `v0.0.1`
