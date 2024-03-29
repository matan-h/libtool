# libtool


libtool is a Python library for creating a Python library,
and also manages versions and uploading to PyPi with twine

libtool runs in Python 3+ and only in Windows.
## Instructions
You need to make a
use_file.ini like this(see more options below):
```ini
[info]
# example with if...main that uses all imports from your library
test_file:test.py
# can also be test_file=your_test_file.py
author:test author
email=test.author@mail.com
description = description of the library
url=http://test.author.com
#dependencies
install_requires=mhyt,mhmovie
license:mit
```
and your test.py (Same as test_file above) like this:
```python
from my_test_library.file1 import plus
from my_test_library.file2 import minus
#
if __name__ == "__main__":
    plus(2,2)#4
    # ##############
    minus(11,1)#10
```
To create library from ini:
```
libtool c {your ini file}
#or
libtool create {your ini file}
```
And the libtool creates the following files automatically:

* setup.py
* __ init __.py
* License.txt 
* README.md

and the libtool will ask you if you want to edit readme.

To change version number(run version from the folder with setup.py):
```
libtool v
```
and the libtool ask "enter new version:".

To upload (Run upload from the folder with setup.py):
```
libtool upload
#or
libtool u
#you can add twine options e.g.
libtool u -r testpypi
```
Twine options [here](https://twine.readthedocs.io/en/latest/#twine-upload)

### Access from python
To access the libtool from a python file:

```python

from libtool import cmd

cmd.parse(["c", "use_file.ini"])
# or 
cmd.parse(["u", "-r testpypi"])
# and all commands
```
## Prerequisites
libtool depends on the python modules:

Markdown-Editor,
requests,
setuptools,
wheel
and twine

## Installing
To install with pip-
type in terminal:
```
(sudo) pip install libtool
```
if this doesn't work try:
```
pip install --upgrade setuptools wheel
```
if there is still an error please open an issue in [github issues](https://github.com/matan-h/libtool/issues).
## Additional options

To show help message:
```
libtool ?
#or
libtool help
```

Additional options for ini file (also in "info" section): 
```ini
#foldername with your library in it, then not all imports need
#to be in file
folder=foldername 
#can also be folder:foldername
#the version of the library
start_version:1.0.0
#cmd scripts or other files that you want in path, like in setuptools scripts.
#separate scripts with commas.
scripts:script1.cmd,script2.exe
```
Additional options for create library command: 
``` 
# to disable open editor to edit readme.md:
libtool c {your ini file} -e edit
# to disable create readme.md:
libtool c {your ini file} -e readme 
# to disable create setup.py:
libtool c {your ini file} -e setup
# to disable create __init__.py:
libtool c {your ini file} -e init
# to disable create licence.txt:
libtool c {your ini file} -e licence
# you can merge options
libtool c use_file.ini -e edit readme setup init licence
```
View examples [here](https://github.com/matan-h/libtool/tree/master/examples)

## Custom options
You can also set custom options using Python.
To create a library:
```python
from libtool.libtool_class import Library

l = Library(
    test_file="test.py",
    email="your.email@your_mail.com",
    description="only for test",
    url = "http://your.url.com",
    pylicense="mit",
    author="author",
    install_requires=["mhyt","mhmovie"],
    #and the additional options:
    folder="foldername",
    start_version="2.7.3",
    scripts=["script1.bat",]
)
#to create __init__.py
l.c_init()
#to create licence.txt
l.c_licence()
#to create setup.py
l.c_setup()
#to create readme.md
l.c_md()
#to edit readme.md
l.edit_md()
```
To change version:
```python
from libtool.up_version import UpVersion

UpVersion("my-sample-library")
```
To publish to PyPi:
```python
from libtool.pypi.up_pypi import up
up("my-sample-library")
#you can add twine options e.g.
up("my-sample-library","-r testpypi")
```
## Built With
* [Markdown-Editor](https://github.com/ncornette/Python-Markdown-Editor.git) - for editing markdown files
* [requests](https://requests.readthedocs.io) - for HTTP request.
* [setuptools](https://github.com/pypa/setuptools) - for setup.py
* [wheel](https://github.com/pypa/wheel) - build help for library
* [twine](https://twine.readthedocs.io/) - for publishing packages on PyPI
## Author
matan h
## License
This project is licensed under the MIT License.
### Created by
This library was created using [libtool](https://github.com/matan-h/libtool)

