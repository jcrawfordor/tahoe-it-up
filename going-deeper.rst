Going Deeper
============

.. toctree::

Let's look a bit deeper in to a few parts of Tahoe that I have previously glossed over.

File and Directory Modes
------------------------

Earlier in the web interface you saw the option of SDMF vs MDMF when creating directories. You probably also saw the example of Immutable, SDMF, or MDMF when uploading files. These are all modes that Tahoe supports for file storage.

Immutable
	Immutable files are uploaded all at once and cannot be changed, they can only be read, moved, and removed once they have been uploaded. This is the default for files, but is usually not used for directories since it would prevent changing the contents of the directory.
SDMF
	Small Distributed Mutable File, or SDMF, allows the file to be changed but still requires that it be uploaded all at once. This means that in order to change a file you must read the while thing and then write the whole thing back. This is efficient for small files because it involves few operations, but inefficient for large files because it requires writing the entire file even if only a part has changed.
MDMF
	Medium Distributed Mutable File, or MDMF, breaks the file up in to chunks (128KiB by default) and allows individual chunks to be changed. This means that editing files only requires reuploading the chunks that have changed. This is more efficient for large files, but MDMF support was only implemented recently and is still experimental.

Caps
----

All objects in the Tahoe grid can be referred to by 'caps', which I have previously referred to always as 'writecaps'. 'Cap' is short for 'Capability', and a capability is a standard way of identifying a Tahoe object. Capabilities begin with ``URI:`` and then give a type, which could be ``DIR2`` for a mutable directory, ``CHK`` for immutable files, etc. Capabilities are usually referred to by one of these convenient names:

filecap
	A filecap is a capability that points to a file, which may be in any of the modes.
dircap
	A dircap points to a directory, which is really just a special type of file.
writecap
	A writecap is used to access a file or directory and grants the ability to write to that file or directory
readcap
	A readcap is used to access a file or directory but only allows reading - it grants read-only permission.
rootcap
	The term roocap is used less frequently to refer to a file or directory that is not inside of any other directory - so the only way to access it is by knowing the capability string. I have been referring to such rootcaps as "standalone", and you'll also see the term "unlinked" used to mean the same thing.

It's important to understand that there can be more than one capability that refers to an object - in the Tahoe terminology, a capability can be "diminished" to a capability that offers fewer functions. It's very common to diminish a writecap to a readcap, so that you can share the readcap with the public, allowing them to access a file but not change it.

FTP/SFTP Frontend
-----------------

The Tahoe client can act as an SFTP server to allow you to access a cap 'directly' using your SFTP client. This is disabled by default, but it's easy to enable.

First, we need to set up an accounts file that we'll use to specify FTP/SFTP users. Create a file at ``~/.tahoe/private/accounts``, and add one or more lines in the form ``<user> <password> <cap>``. The user and password (seperated by spaces) are what you'll type in to your client to authenticate, and the cap is a capability string that will be the "root" of the file system exposed by SFTP.

Now, run ``ssh-keygen`` to create an SSH keypair for the Tahoe client. When asked for a passphrase, leave it blank. When asked where to write the key, use ``~/.tahoe/private/ssh_host_rsa_key``.

Finally, open ``~/.tahoe/tahoe.cfg`` and add an ``sftpd`` stanza like this one:

::

	[sftpd]
	enabled = true
	port = tcp:8022:interface=127.0.0.1
	host_pubkey_file = private/ssh_host_rsa_key.pub
	host_privkey_file = private/ssh_host_rsa_key
	accounts.file = private/accounts

Note that you'll need to change the port line to bind to a different interface if you want to be able to connect from machines other than localhost.

Now start tahoe (or restart it) and you should be able to connect. There are some caveats to the SFTP interface, which you can read about at https://tahoe-lafs.org/trac/tahoe-lafs/wiki/SftpFrontend.