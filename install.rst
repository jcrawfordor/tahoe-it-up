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

In the Environment Variables dialogue, select "Path" in the list of System Variables and click Edit. In the "Variable value" box, add a colon (``;``) followed by ``C:\Python27`` (or the path for your version of python). Now click "OK" until you're all the way out.

Installing Tahoe
~~~~~~~~~~~~~~~~

Download the most recent .zip package (something like ``allmydata-tahoe-1.XX.X.zip``) from https://tahoe-lafs.org/source/tahoe-lafs/releases/. Decompress the ZIP package to a convenient location and open a command prompt and navigate to it. Run ``python setup.py build``, which will conveniently get all the dependencies you need. Note that the first time you build Tahoe it may ask you to close the command prompt window and open a new one, this is just because it needs to set some environment variables and the command prompt handles this in a dumb way. 

Once the build finishes, in the 'bin' subdirectory you'll have a ``tahoe.pyscript`` that is actually the Tahoe executable. Put this somewhere convenient; perhaps create a folder ``C:\tahoe``, move the contents of the bin subdirectory there, and add it to the path.

Linux
-----

From a Package
~~~~~~~~~~~~~~

On Linux, you should probably install Tahoe from your distribution's package repository. E.g.:

- On Debian and similar, ``apt-get install tahoe-lafs``
- On Arch Linux, ``yaourt -S tahoe-lafs``

From Source
~~~~~~~~~~~

If Tahoe is not packaged for your distribution, you would like the latest version, or you do not have privileged access, you can install Tahoe from source.

- Install the most recent 2.x version of Python (via your distribution package manager, etc)
- Download the most recent .tar.gz package (something like ``allmydata-tahoe-1.XX.X.tar.gz``) from https://tahoe-lafs.org/source/tahoe-lafs/releases/ and decompress it.
- In the decompressed directory, run ``./setup.py build``, which will obtain dependencies automatically
- Move the ``tahoe`` executable in 'bin' to a convenient location in your path.

OS X
----

It should be straightforward to build Tahoe from source on OS X the same way as on other platforms, but I do not have an OS X machine readily available on which to test. Give it a try:

- Install Python 2.x by a method of your choice.
- Download the most recent .tar.gz package (something like ``allmydata-tahoe-1.XX.X.tar.gz``) from https://tahoe-lafs.org/source/tahoe-lafs/releases/ and decompress it.
- In the decompressed directory, run ``./setup.py build``, which will obtain dependencies automatically
- Move the ``tahoe`` executable in 'bin' to a convenient location in your path.