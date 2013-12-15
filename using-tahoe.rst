Using Tahoe
===========

.. toctree::

Before we start reading and writing files, we have to understand how Tahoe works fundamentally. The Tahoe grid stores a set of files and directories that are encrypted and don't have to be related to each other - they can be completely independent. In order to write or read a directory, you need to know the encryption key, which is used in the form of a 'writecap', which allows you to write to a file or directory, or a 'readcap', which allows you to read. That's all you need. It doesn't matter "where" in the grid the content is stored, because Tahoe locates content automatically.

Let's start using Tahoe by creating a directory to put some files in. Note that the Tahoe client is used via a web interface, which we can operate either through a web browser or by using a command-line tool that interacts with the web API. Let's use the web interface to start. Point your browser at ``http://localhost:3456`` (change the port if you set a different port in your configuration) and you should see the Tahoe Web UI (WUI), listing storage nodes in the grid and the connection status. Hopefully you've already connected to several storage nodes, indicated by green dots. To create a directory, click "Create a Directory" at the bottom of the left sidebar (you can leave it set to SDMF - we'll talk about SDMF vs. MDMF later).

You'll be taken to a directory listing (which is empty). And that's it, you've created your first object in the Tahoe grid. Make sure to bookmark this page or copy the writecap out of the URL (the URL is in the form /uri/<writecap>), because you'll need to know the writecap to access this directory again - since it's encrypted, the writecap is the only way to access it.

The web interface gives you convenient GUI access to file operations - note at the bottom of the page, there are forms that allow you to create subdirectories and add files to this writecap. Try it out now. Note that each directory or file you add has its own writecap, which when you're using the web interface you'll see in the URLs.

**A note on Tahoe etiquette:** The storage in the Tahoe grid is contributed by volunteers, and isn't unlimited. If you're going to store a lot of data in Tahoe, please also provide storage to the grid. The public test grid recommends contributing twice as much storage as you use, and making sure that that storage node is stable and publically accessible.