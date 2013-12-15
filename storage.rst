Providing Storage
=================

.. toctree::

You can contribute back to the grid you've joined by operating a storage node as well as a client. It's easy to add storage to an existing client node, but there are some prerequisites:

- You'll obviously need to have some disk space free, preferably a significant amount.
- You'll need to be able to accept incoming connections from other Tahoe nodes, which probably means configuring your router appropriately.

Incoming connections
--------------------

If your machine is connected directly to the public internet, Tahoe should be able to accept incoming connections without any additional configuration. If you're behind a firewall or NAT, though, you'll need to first add a port forward or firewall exception to allow incoming connections on some port (usually 8098) and then tell Tahoe how outside nodes can connect in. You can do this by adding two lines to the ``[node]`` stanza:

::

	tub.port = 8098
	tub.location = 123.45.67.89:8098

Where ``tub.port`` is the port that Tahoe should listen on for incomnig connections, and ``tub.location`` is a comma-seperated list of one or more hostnames and ports that other nodes can use to connect to you (so, your machine's public IP address or hostname and the incoming port).

Storage configuration
---------------------

Now, in ``~/.tahoe/tahoe.cfg``, add or find the ``[storage]`` stanza. You'll need to add two lines:

::

	enabled = true
	reserved_space = 2G
	expire.enabled = true
	expire.mode = age

Note the ``reserved_space`` directive. Rather than you setting how much space Tahoe can use, Tahoe will use all of the disk space available until there is only ``reserved_space`` free. Set this directive appropriately depending on how much space you want to use, knowing that Tahoe will use up to roughly <free space> - <reserved space>.

``expire.enabled`` enables garbage collection on your storage node, which will remove objects that are no longer used. ``expire.mode`` specifies what criteria should be used for removal.