# Adding a Cache Dir

*by Chris Robertson*

Adding a new drive to Squids cache directory set is a useful thing to
know. And simple as well.

Squid will handle the changes semi-automatically, but there are still a
few operations that need to be kicked off manually.

Assuming your disk is attached, your OS recognizes it and the disk is
formatted:

1.  Ensure the
    [cache\_effective\_user](http://www.squid-cache.org/Doc/config/cache_effective_user#)
    has write capability on the mount point

2.  Add a [cache\_dir](http://www.squid-cache.org/Doc/config/cache_dir#)
    directive to squid.conf referencing the new mount point

3.  Stop squid

4.  Run `squid -z` (as root or as the
    [cache\_effective\_user](http://www.squid-cache.org/Doc/config/cache_effective_user#))

5.  Start squid

# Downtime reduction hack

*by
[AmosJeffries](/AmosJeffries#)
and
[HenrikNordstrom](/HenrikNordstrom#)*

NP: this does not apply to large caches as there is no touching of the
existing cache\_dir anyway.

1.  Ensure the
    [cache\_effective\_user](http://www.squid-cache.org/Doc/config/cache_effective_user#)
    has write capability on the mount point

2.  Temporarily change squid.conf to use another
    [pid\_filename](http://www.squid-cache.org/Doc/config/pid_filename#).
    `squid -z` will abort early if it discovers another running squid
    instance

3.  Add a [cache\_dir](http://www.squid-cache.org/Doc/config/cache_dir#)
    directive to squid.conf referencing the new mount point

4.  Temporarily: comment out the existing
    [cache\_dir](http://www.squid-cache.org/Doc/config/cache_dir#)
    entries

5.  Run `squid -z -f ./squid.conf` (as root or as the
    [cache\_effective\_user](http://www.squid-cache.org/Doc/config/cache_effective_user#))

6.  Undo the temporary changes to
    [pid\_filename](http://www.squid-cache.org/Doc/config/pid_filename#)
    and pre-existing
    [cache\_dir](http://www.squid-cache.org/Doc/config/cache_dir#)

7.  Reconfigure the running squid with `squid -k reconfigure`
    
    ![{i}](https://wiki.squid-cache.org/wiki/squidtheme/img/icon-info.png)
    While the -z with existing ufs/aufs/diskd is harmless it's a
    destructive operation with for example coss
    [cache\_dirs](http://www.squid-cache.org/Doc/config/cache_dirs#) so
    commenting them out is important.

Back to the
[SquidFaq](/SquidFaq#)
