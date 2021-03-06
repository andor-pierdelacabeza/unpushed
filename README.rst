============
``unpushed``
============
---------------------------------------------------------
Scan version control for uncommitted and unpushed changes
---------------------------------------------------------

This is fork of "uncommitted_" project originally created by Brandon Rhodes.

"unpushed" adds some features:

* support for checking branches for unpushed commits,
* desktop notification.

Preface from original author
============================

When working on one version-controlled project on my hard drive, I often
flip over quickly to another project to make a quick change.  By the end
of the day I have forgotten about that other change and often find it
months later when I enter that repository again.  I needed a way to be
alerted at the end of each day about any uncommitted changes sitting
around on my system.

Thus was born this "uncommitted" script: using either your system
*locate(1)* command or by walking a filesystem tree on its own, it will
find version controlled directories and print a report on the standard
output about any uncommitted changes still sitting on your drive.  By
running it from a *cron(8)* job you can make this notification routine.

Running "unpushed"
==================

By default "unpushed" uses the *locate(1)* command to scan for
repositories, which means that it can operate quickly even over very
large filesystems like my home directory::

    $ unpushed ~

But you should **be warned:** because the *locate(1)* database is only
updated once a day on most systems, this will miss repositories which
you have created since its last run.  To be absolutely sure to see all
current repositories, you should instead ask "unpushed" to search the
filesystem tree itself.  To do this on your "devel" directory, for
example, you would type this::

    $ unpushed -w ~/devel

Not only will the output of "-w" always be up-to-date, but it is usually
faster for small directory trees.  The default behavior of using
*locate(1)* (which can also be explicitly requested, with "-l") is
faster when the directory tree you are searching is very large.

Should you ever want a list of all repositories, and not just those with
uncommitted changes, you can use the "-a" option::

    $ unpushed -a ~

Also you can list exact files or braches was changed using the "-v" verbose
option::

    $ unpushed -v ~

You can always get help by running "unpushed" without arguments or
with the "-h" or "--help" options.

Desktop notification
====================

Application use system depended desktop notification facility. To show desktop
notification run this command::

    $ unpushed-notify ~

On Linux this is done through pynotify library. On OS X through pyobjc. On other systems this feature is
not implemented yet.

You can add this line to your crontab (*crontab -e*)::

    */10 18-20 * * *   unpushed-notify ~

This will show you notification about uncommitted and unpushed changes every
10 minutes starting from 6pm ending at 8pm.

Do not forget to add unpushed-notify to cron PATH!

Supported VCs
=============

At the moment, "unpushed" supports:

* `Mercurial`_ (.hg directories)
* `Git`_ (.git directories)
* `Subversion`_ (.svn directories)

Limitations
===========

* Only Linux libnotify is supported as notification facility

TODO
====

* Check svn existence before using it
* Check locate existence before using it

Changelog
=========

**1.2.0** (2017 Sep 25)

- Python 3 Migration

**1.1.0** (2012 May 22)

- Fix README markup
- Report untracked files separately
- Add -t option to ignore untracked files
- Show not pushed changesets in Mercurial. Thanks Guilherme Gondim for
  testing

**1.0.2** (2012 April 27)

- Fix setup script

.. _uncommitted: http://bitbucket.org/brandon/uncommitted
.. _Mercurial: http://mercurial.selenic.com/
.. _Subversion: http://subversion.tigris.org/
.. _Git: http://git-scm.com/
