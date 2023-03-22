# com.softalks.debug
Easy remote debugging for Python 3 under Linux & [Eclipse PyDev](https://www.pydev.org/)/[LiClipse](https://www.liclipse.com/)
## Requirements
To debug your module (after installing this component on your [pip](#pip)/[Kodi](#Kodi) environment) you will need to: 
* Set `__import__('com.softalks.debug')` as the first line of your module (if not done for any module loading previously)
* Set the environment variable PYDEVD to your Eclipse home (a [Launch Configuration](https://www.eclipse.org/forums/index.php/t/1093076) using `${eclipse.home}` is recomended)
* Define one or more breakpoints on your module using the PyDev Python editor
* Start the PyDev debug server (your module will only stop while the server is running)
* Run the proper use case of the program that loads your module
* Wait a few seconds until execution stops
* Execution should stop at line 29 of `debug.py`. Press F8 to jump to your first breakpoint
> All modules with a namespace starting by `com.softalks.` are debuggable by design. If your module or any previously loading module are using them you are free to ignore the first requirement

> The last requirement is a [candidate to disappear](https://github.com/hiebra/rpdb/issues/1) in the next version
## pip
> Under Ubuntu 22.04 ensure the environment variable `DEB_PYTHON_INSTALL_LAYOUT` has the value `deb_system` before using pip to install/uninstall this package (click [here](https://github.com/pypa/setuptools/issues/3269#issuecomment-1254507377) for details)
### Install
> To be able to install this package with pip you need to install `git` first

An example of installing a specific version (0.0.1):
```
pip3 install git+https://github.com/hiebra/rpdb.git@v0.0.1
```
You can also install it indirectly when referenced from a depending component's `pyproject.toml`:
```
[project]
...
dependencies = [
    "com.softalks.debug @ git+https://github.com/hiebra/rpdb@v0.0.1",
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
