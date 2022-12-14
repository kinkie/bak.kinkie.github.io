[MoinMoin](/MoinMoin#)
*DesktopEdition* is the easiest way to run moin, without much
installation and without separate server software (this is why its
built-in server is also called the *standalone server*).

It is intended as a local personal information manager.

# Installation

  - if you don't already have Python installed (Linux systems often have
    it by default, Mac OS X also, Windows usually needs manual
    installation), get it from [](http://python.org/)

  - download the moin distribution archive from
    [MoinMoinDownload](http://moinmo.in/MoinMoinDownload#)

  - unpack it (will give some moin-1.x.x directory)

If you prefer to work with a repository checkout instead of a release
archive, the procedure is like above, but you additionally have to
unpack the underlay pages:

  - `cd moin-1.x.x/wiki`

  - `tar xf underlay.tar`

# Running

  - `cd moin-1.x.x`

  - `./wikiserver.py` (or click on `wikiserver.py`)

  - now a fresh moin wiki will run on [](http://localhost:8080/)
    ![:)](https://wiki.squid-cache.org/wiki/squidtheme/img/smile.png)

  - you can terminate the wiki server either by using Ctrl-C or closing
    the window

# Wiki Server Configuration

If you need to use a configuration different from the standard
configuration you can edit the `wikiserverconfig.py` in the toplevel
directory, see the comments there.

![(\!)](https://wiki.squid-cache.org/wiki/squidtheme/img/idea.png) By
default, moin only listens on the localhost interface. Before opening it
to a wider audience, please check if the security settings of moin are
what you want. Especially the `DesktopEdition` and `acl_rights_*`
settings might need changes if you don't use it for personal use and on
localhost only.

# Wiki Server Logging Configuration

See `wikiserverlogging.conf`.

![(\!)](https://wiki.squid-cache.org/wiki/squidtheme/img/idea.png) You
maybe usually don't want to change that, but you *can* - e.g. if you
like to have more log output for debugging.

# Wiki Configuration

See the `wikiconfig.py` in the toplevel directory.
[HelpOnConfiguration](/HelpOnConfiguration#)
lists the configuration options. You maybe also want to look at the
sample config in the `wiki/config/` directory.

See also:
[HelpOnInstalling/StandaloneServer](/HelpOnInstalling/StandaloneServer#)
