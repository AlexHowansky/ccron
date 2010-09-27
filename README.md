ccron - a centralized crontab manager
=====================================

Synopsis
--------

ccron is a tool that allows simple centralized management of a large number of crontabs spread over a large number of hosts. It maintains copies of all remote crontabs in a local and well-formed manner that is suitable for source control, and manages synchronization of local edits with the live remote crontabs.

Assumptions
-----------

It is assumed that the user running ccron already has shell access to each user account on each host that will be managed. Installation of this tool does not automatically grant access to any user's crontab, it merely makes managing them easier.

Installation
------------

Simply drop ccron somewhere in your path and run it without any arguments to initialize the configuration file. Edit the file as desired according to the notes therein.

Usage
-----

The general idea behind ccron is to take the text of all your various crontabs and store it locally in one place so that it can be operated on as a whole, with standard tools such as grep (to search for a specific command) or git (to track changes.) This is done by making a local copy of each remote crontab, using the local copy for editing operations, and then syncing the edited copy back to the remote host. So, we refer to the actual live and running crontab as "the remote crontab" and the local copy of it as "the local crontab."

To manage an existing remote crontab, it must first be imported into the local database. This is done with the `pull` command.

    ccron pull <user> <host>

To edit an existing local crontab or create a new empty local crontab, use the `edit` command.

    ccron edit <user> <host>

To list all the local crontabs, use the `list` command.

    ccron list

The list command can also take optional arguments to filter for a specfic host.

    ccron list <host>

To export a local crontab back to its remote host (so that it starts running), use the `push` command. If you have the autopush option enabled in your configuration file, a push will automatically be performed after an edit. The autopush behavior is more inline with how `crontab -e` works, but is disabled by default for safety.

    ccron push <user> <host>

To remove a local crontab without changing its remote counterpart (i.e., to simply stop managing it), use the `ignore` command.

    ccron ignore <user> <host>

To remove both a local crontab and its remote counterpart (i.e., so that it stops running), use the `drop` command.

    ccron drop <user> <host>
