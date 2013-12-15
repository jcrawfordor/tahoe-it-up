Client Configuration
====================

.. toctree::

Now that we have Tahoe installed, let's create and configure a client node. Client nodes allow you to access the Tahoe grid but do not offer storage - of course, it's easy to extend a client to offer storage later on.

First, run ``tahoe create-client`` to set up a skeleton Tahoe client configuration in ``~/.tahoe`` (``%USERPROFILE%\.tahoe`` on Windows). Open ``~/.tahoe/tahoe.cfg`` in a text editor, and we'll need to change a few lines:

nickname
	The nickname line sets a human-readable nickname that will be used to display your node to other users. Set it to whatever you'd like.
web.port
	Tahoe is accessed primarily via a web interface and a web API. You can change this line to bind it to a different port or interface. **Caution:** be careful about binding to an interface other than localhost. You don't want everyone on the internet to be able to connect to your "private" Tahoe node!
introducer.furl
	Tahoe is a distributed, peer-to-peer system, but your client needs some way to find peers in the first place. An 'introducer' node will accept direct connections and help you find the rest of the grid. Put in the value given to you by the grid you want to join, or, to join the public test grid, use ``pb://hckqqn4vq5ggzuukfztpuu4wykwefa6d@publictestgrid.dnsd.info:50213/introducer``.
helper.furl
	Writing to the tahoe grid is slower than reading from it, because when writing you need to send copies of the content to multiple storage nodes for redundancy. Unfortunately, many home internet connections have very slow upload speeds. Some users in your grid may offer helper nodes, which are nodes with fast uplinks that will distribute multiple copies for you so that you only need to upload one. If you have a slow upstream connection, you might want to set a helper node (ask the grid members if there are helpers available). If you have a good upstream connection, leave this blank to avoid unnecessary load on the volunteer helpers.

	An additional benefit to using a helper is that helpers will store partial uploads on disk, allowing you to resume an upload if, for example, you turn off your computer before an upload finishes. If you are not using a helper, incomplete uploads will have to restart from scratch.
shares.needed, shares.happy, shares.total
	These directives set how many redundant copies of your data you would like to have stored in the cloud. The defaults should provide suitable redundancy, or if you are joining a small grid you may want to set smaller values. Ask other grid members for the values they use.

We can leave the rest of the file as-is for now. Now that Tahoe is configured, run ``tahoe start`` to start the client running in the background.