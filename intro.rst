What is Tahoe?
==============

.. toctree::

Tahoe, or Tahoe-LAFS, is short for the Tahoe Least Authority File System. What, you ask, is a least authority file system?

First, let's take a step back. Tahoe is a cloud file system, meaning that it takes your files and stores them "in the cloud" by putting them on other computers on the internet. These computers are simply the other members of whatever Tahoe grid you join that have their Tahoe clients set to provide storage nodes. This lets you store files on the cloud, similar to services like Dropbox, Google Drive, and the like. The difference between Tahoe and these services is the *least authority* part.

Tahoe implements the principle of least authority or principal of least privilege to the greatest extent possible. Essentially, Tahoe does not require that you actually trust the storage nodes at all. It uses encryption so that the storage nodes are not capable of reading your files, so you do not have to trust them not to be malicious. It uses fault-tolerance so that your data is not dependent on any one storage node, so you also do not have to trust storage nodes to reliably stay online (or to have reliable hard disks, etc).

The bottom line is that Tahoe allows you to build your own cloud storage service by banding together with a bunch of people on the internet that you don't have to trust, or even know at all. It uses your friends (or acquaintances or random contacts) to store your data in a way that is secure and reliable. Tahoe calls a group of people that have banded together this way a "grid," and chances are you're reading this document because you want to join such a grid, to use it for storage and, if you have the free space, maybe also to share storage with others. So, the first thing we'll do is install Tahoe on your computer.