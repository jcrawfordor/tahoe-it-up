Installing Tahoe
================

.. toctree::

Tahoe is written in Python, so you can get it running on pretty much any platform. Take a look at the section for your specific platform.

Note that Tahoe does not require privileged access. On any system with Python installed, you can build and run Tahoe in your own user account. On Linux, this will require building from source.

Windows
-------

Installing Tahoe on Redmond's operating system is pretty easy.

Installing Python
~~~~~~~~~~~~~~~~~

Obtain a recent version of Python from http://www.python.org/download/. Note that there are currently two stable branches of Python, 2.x and 3.x. Tahoe only supports 2.x, so choose the most recent Windows installer with a 2.x version number. Run the installer, and now you have Python.

One caveat: the Python installer does not add Python to the execution path, or at least it doesn't by default. Let's correct this real quick.

- In Windows 7, click Start, right click My Computer, and click Properties. This opens the System control panel. In the sidebar, click Advanced System Settings, and in the dialogue that appears click Environment Variables. 

- In Windows 8, just go to the start screen, search for "environment", and click "Edit the system environment variables."

In the Environment Variables dialogue, select "Path" in the list of System Variables and click Edit. In the "Variable value" box, add a colon (``;``) followed by ``C:\Python27`` (or the path for your version of python), followed by another colon, followed by ``C:\Python27\Scripts`` (this is where tools like ``easy_install`` are found). Now click "OK" until you're all the way out.

Installing Tahoe
~~~~~~~~~~~~~~~~

You can either install Tahoe from source, or install Python Setuptools and install it from the Python Package Index. The Setuptools approach is easier, but might get you a slightly older version.

From PyPI
.........

Install Python Setuptools by downloading the install script from https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py and running it. Once Setuptools is installed, in a command prompt run ``easy_install allmydata-tahoe``.

From Source
...........

Download the most recent .zip package (something like ``allmydata-tahoe-1.XX.X.zip``) from https://tahoe-lafs.org/source/tahoe-lafs/releases/. Decompress the ZIP package to a convenient location and open a command prompt and navigate to it. Run ``python setup.py build``, which will conveniently get all the dependencies you need. Note that the first time you build Tahoe it may ask you to close the command prompt window and open a new one, this is just because it needs to set some environment variables and the command prompt handles this in a dumb way. 

Once the build finishes, in the 'bin' subdirectory you'll have a ``tahoe.pyscript`` that is actually the Tahoe executable. Put this somewhere convenient; perhaps create a folder ``C:\tahoe``, move the contents of the bin subdirectory there, and add it to the path.

Linux
-----

From a Package
~~~~~~~~~~~~~~

On Linux, you should probably install Tahoe from your distribution's package repository. E.g.:

- On Debian and similar, ``apt-get install tahoe-lafs``
- On Arch Linux, ``yaourt -S tahoe-lafs``

From PyPI
~~~~~~~~~

Tahoe is available in the Python Package Index, if it's not in your distribution's repositories.

- Install the most recent 2.x version of Python along with Python Setuptools.
- Run ``easy_install allmydata-tahoe`` (or, if you have pip installed, ``pip install allmydata-tahoe``)

Note that if you do not have privileged access to the machine you're using, you can use pip with the ``--user`` option to install Tahoe to your account.

From Source
~~~~~~~~~~~

- Install the most recent 2.x version of Python (via your distribution package manager, etc)
- Download the most recent .tar.gz package (something like ``allmydata-tahoe-1.XX.X.tar.gz``) from https://tahoe-lafs.org/source/tahoe-lafs/releases/ and decompress it.
- In the decompressed directory, run ``./setup.py build``, which will obtain dependencies automatically
- Move the ``tahoe`` executable in 'bin' to a convenient location in your path.

OS X
----

You can install Tahoe on OS X using the same methods as for Linux.

From PyPI
~~~~~~~~~

- Install the most recent 2.x version of Python along with Python Setuptools (via the method of your choice)
- Run ``easy_install allmydata-tahoe`` (or, if you have pip installed, ``pip install allmydata-tahoe``)

From Source
~~~~~~~~~~~

- Install the most recent 2.x version of Python
- Download the most recent .tar.gz package (something like ``allmydata-tahoe-1.XX.X.tar.gz``) from https://tahoe-lafs.org/source/tahoe-lafs/releases/ and decompress it.
- In the decompressed directory, run ``./setup.py build``, which will obtain dependencies automatically
- Move the ``tahoe`` executable in 'bin' to a convenient location in your path.