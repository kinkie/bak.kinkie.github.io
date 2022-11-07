# Squid on Ubuntu

## Pre-Built Binary Packages

Packages available for Squid on multiple architectures.

  - **Maintainer:** Luigi Gangitano

### Squid-4

Bug Reports: [](https://bugs.launchpad.net/ubuntu/+source/squid)

  - ![{i}](https://wiki.squid-cache.org/wiki/squidtheme/img/icon-info.png)
    Ubuntu 18.10 (Cosmic) or newer.

Install Procedure:

``` 
 aptitude install squid
```

### Squid-3.5

Bug Reports: [](https://bugs.launchpad.net/ubuntu/+source/squid)

  - ![{i}](https://wiki.squid-cache.org/wiki/squidtheme/img/icon-info.png)
    Ubuntu 18.04 (Bionic) or older.

Install Procedure:

``` 
 aptitude install squid
```

## [(see Debian)](https://wiki.squid-cache.org/action/show/KnowledgeBase/Ubuntu/KnowledgeBase/Debian)

Many versions of Ubuntu and Debian are routinely build-tested and
unit-tested as part of our
[BuildFarm](https://wiki.squid-cache.org/action/show/KnowledgeBase/Ubuntu/BuildFarm#)
and are known to compile OK.

  - ![/\!\\](https://wiki.squid-cache.org/wiki/squidtheme/img/alert.png)
    The Linux system layout differs markedly from the Squid defaults.
    The following ./configure options are needed to install Squid into
    the Debian / Ubuntu standard filesystem locations:

<!-- end list -->

    --prefix=/usr \
    --localstatedir=/var \
    --libexecdir=${prefix}/lib/squid \
    --datadir=${prefix}/share/squid \
    --sysconfdir=/etc/squid \
    --with-default-user=proxy \
    --with-logdir=/var/log/squid \
    --with-pidfile=/var/run/squid.pid

Plus, of course, any custom configuration options you may need.

  - ![{X}](https://wiki.squid-cache.org/wiki/squidtheme/img/icon-error.png)
    For Debian Jesse (8), Ubuntu Oneiric (11.10), or older **squid3**
    packages; the above *squid* labels should have a **3** appended.

  - ![{X}](https://wiki.squid-cache.org/wiki/squidtheme/img/icon-error.png)
    Remember these are only defaults. Altering squid.conf you can point
    the logs at the right path anyway without either the workaround or
    the patching.

As always, additional libraries may be required to support the features
you want to build. The default package dependencies can be installed
using:

    aptitude build-dep squid

This requires only that your sources.list contain the **deb-src**
repository to pull the source package information. Features which are
not supported by the distribution package will need investigation to
discover the dependency package and install it.

  - ![{i}](https://wiki.squid-cache.org/wiki/squidtheme/img/icon-info.png)
    The usual one requested is **libssl-dev** for SSL support.
    
      - ![/\!\\](https://wiki.squid-cache.org/wiki/squidtheme/img/alert.png)
        However, please note that
        [Squid-3.5](https://wiki.squid-cache.org/action/show/KnowledgeBase/Ubuntu/Squid-3.5#)
        is not compatible with OpenSSL v1.1+. As of Debian Squeeze, or
        Ubuntu Zesty the **libssl1.0-dev** package must be used instead.
        This is resolved in the
        [Squid-4](https://wiki.squid-cache.org/action/show/KnowledgeBase/Ubuntu/Squid-4#)
        packages.

### Init Script

The init.d script is part of the official Debain/Ubuntu packaging. It
does not come with Squid directly. So you will need to download a copy
from
[](https://alioth.debian.org/plugins/scmgit/cgi-bin/gitweb.cgi?p=pkg-squid/pkg-squid3.git;a=blob_plain;f=debian/squid.rc)
to /etc/init.d/squid

## Compile on A basic Ubuntu Server

@Eliezer

Squid can be built on a basic Ubuntu basic Server and it seems like an
enterprise OS to me. The only dependencies are "build-essential" and
"libltdl-dev" for squid to run as a forward proxy.

    sudo apt-get install build-essential libltdl-dev

For more then just forward proxy like ssl-bump or tproxy We need a bit
more testing.

Latest squid 3.3.8 builds and runs on ubuntu server 13.04.

# Troubleshooting

[CategoryKnowledgeBase](https://wiki.squid-cache.org/action/show/KnowledgeBase/Ubuntu/CategoryKnowledgeBase#)
[SquidFaq/BinaryPackages](https://wiki.squid-cache.org/action/show/KnowledgeBase/Ubuntu/SquidFaq/BinaryPackages#)
