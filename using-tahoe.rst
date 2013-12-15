Using Tahoe
===========

.. toctree::

Before we start reading and writing files, we have to understand how Tahoe works fundamentally. The Tahoe grid stores a set of files and directories that are encrypted and don't have to be related to each other - they can be completely independent. In order to write or read a directory, you need to know the encryption key, which is used in the form of a 'writecap', which allows you to write to a file or directory, or a 'readcap', which allows you to read. That's all you need. It doesn't matter "where" in the grid the content is stored, because Tahoe locates content automatically.

The Web UI
----------

Let's start using Tahoe by creating a directory to put some files in. Note that the Tahoe client is used via a web interface, which we can operate either through a web browser or by using a command-line tool that interacts with the web API. Let's use the web interface to start. Point your browser at ``http://localhost:3456`` (change the port if you set a different port in your configuration) and you should see the Tahoe Web UI (WUI), listing storage nodes in the grid and the connection status. Hopefully you've already connected to several storage nodes, indicated by green dots. To create a directory, click "Create a Directory" at the bottom of the left sidebar (you can leave it set to SDMF - we'll talk about SDMF vs. MDMF later).

You'll be taken to a directory listing (which is empty). And that's it, you've created your first object in the Tahoe grid. Make sure to bookmark this page or copy the writecap out of the URL (the URL is in the form /uri/<writecap>), because you'll need to know the writecap to access this directory again - since it's encrypted, the writecap is the only way to access it.

The web interface gives you convenient GUI access to file operations - note at the bottom of the page, there are forms that allow you to create subdirectories and add files to this writecap. Try it out now. Note that each directory or file you add has its own writecap, which when you're using the web interface you'll see in the URLs.

**A note on Tahoe etiquette:** The storage in the Tahoe grid is contributed by volunteers, and isn't unlimited. If you're going to store a lot of data in Tahoe, please also provide storage to the grid. The public test grid recommends contributing twice as much storage as you use, and making sure that that storage node is stable and publically accessible.

Once you have created a writecap, you'll find that navigating it through the web interface is very easy: you can descend through directories, and download files to your local disk just by clicking on them. If you go back to the top level interface, you'll find that just as you can create directories (that aren't in another directory) you can also upload freestanding files, and download any file given its writecap (or readcap).

The command-line UI
-------------------

Tahoe also includes the command-line ``tahoe`` tool, which in addition to creating config skeletons also acts as a text UI to the web interface's API. If you spend most of your time in a shell you'll find this to be a much faster way to use Tahoe.

The command line tool introduces the convenient concept of "aliases". Since directories and files are freestanding in Tahoe, we always need to refer to at least the top level by writecap rather than by name (we can use the names of files and folders under a writecap, but we always need to specify the writecap at the top). Of course writecaps are quite long, so having to paste or type them all the time would mae working with Tahoe very frustrating. Instead, the command line tool lets us set short aliases to writecaps.

First, let's set the alias 'tahoe', which is a special alias because it's used as the default by most command line tools. We can set it with ``tahoe add-alias tahoe <writecap>``. Try running that with the writecap of the directory you created earlier - remember that writecaps start with ``URI:``, the first two parts before colons are important.

Now that you have a default alias set, run ``tahoe ls``. Just like the command ``ls``, this will list the contents of a directory in Tahoe. Without any arguments, it lists the contents of wherever the 'tahoe' alias points. You should see anything that you added through the web interface.

We can use ``tahoe put`` to upload files to the grid. ``tahoe put <file>`` will put the file in the grid without placing it anywhere. On the other hand, ``tahoe put <file> <name>`` will put the file in the grid as ``tahoe:<name>`` - that is, as a file by the name you specify in the directory that the 'tahoe' alias points to. Note that if you use '-' instead of a local file name, you can easily write STDIN to the Tahoe grid (try piping something to ``tahoe put``). You can even run ``tahoe put`` with no arguments at all and it will write the STDIN to an unlinked file in the grid, giving you the writecap for it after it finishes.

``tahoe mkdir`` can be used to make a directory. ``tahoe mkdir <name>`` will create a directory by the name specified in the directory specified by the 'tahoe' alias. We can, of course, nest directories as well: if there's a directory called 'mystuff', we can create a 'pictures' directory inside of it with ``tahoe mkdir mystuff/pictures``. We could put 'beach.jpg' in that directory with ``tahoe put beach.jpg mystuff/pictures/beach.jpg``. Make sense?

All of the file operations we would expect exist. ``tahoe mv`` moves files, ``tahoe rm`` removes them, and perhaps most importantly ``tahoe get`` reads them - ``tahoe get mystuff/pictures/beach.jpg`` will read that file to STDOUT, while ``tahoe get mystuff/pictures/beach.jpg beach.jpg`` will write it to the local file 'beach.jpg'.

You can also use ``tahoe backup`` to mirror an entire directory to Tahoe, and ``tahoe manifest`` to show a tree of a Tahoe directory. ``tahoe cp`` copies files, and ``tahoe ln`` creates links inside tahoe (just like Unix soft links).

You can also create additional aliases by running ``tahoe add-alias <name> <writecap>`` to add an alias to an existing location, or ``tahoe create-alias <name>`` to automatically create a new freestanding directory and set the alias specified to point to it. You can use aliases other than 'tahoe' (the default) by prefixing Tahoe paths with ``<alias>:``, e.g. ``public:mystuff/pictures/beach.jpg`` if you have an alias 'public'.

To recap, in general the Tahoe command line tool takes tahoe paths in the form of ``<alias>:<path>``. Alias is one of the aliases you've set or can be left off entirely, in which case the alias 'tahoe' is assumed. The path is a slash-seperated path rooted wherever the alias points.

Finally, you can always run ``tahoe --help`` to see a list of all commands, and any command with the ``--help`` option to see usage instructions (e.g. ``tahoe put --help`` to see how to use the put command).