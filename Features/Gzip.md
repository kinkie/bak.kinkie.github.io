# Feature: Gzip compression / decompression in Squid

  - **Goal**: To make Squid capable of compressing or decompressing
    objects in transit.

  - **Status**: a partial 3rd-party solution exists, needs testing

  - **Version**: 3.1

  - **Developer**:

  - **More**: [3rd party eCAP
    module](https://wiki.squid-cache.org/action/show/Features/Gzip/ThirdPartyModules/EcapGzip#)

## Details

An
[eCAP](https://wiki.squid-cache.org/action/show/Features/Gzip/Features/eCAP#)
module developed by Constantin Rack at VIGOS to support gzip compression
of text/html cache *misses* is
[available](https://wiki.squid-cache.org/action/show/Features/Gzip/ThirdPartyModules/EcapGzip#).
That 3rd-party module has not been tested by the Squid Project.

An old, unfinished Squid v3.0
[patch](http://devel.squid-cache.org/projects.html#gzip) implements some
of the required functionality directly in Squid.

[CategoryFeature](https://wiki.squid-cache.org/action/show/Features/Gzip/CategoryFeature#)
