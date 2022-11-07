# index report

When an HTML template named **MGR\_INDEX** is installed in the
**templates/** error page directory this report will return its contents
after [macro
expansion](https://wiki.squid-cache.org/action/show/Features/CacheManager/Index/Features/CustomErrors#).

This allows creation of a scripted user interface for the cache manager
loaded from that template.

## Example JS reporting tool

[FrancescoChemolli](https://wiki.squid-cache.org/action/show/Features/CacheManager/Index/FrancescoChemolli#)
and
[AmosJeffries](https://wiki.squid-cache.org/action/show/Features/CacheManager/Index/AmosJeffries#)
have developed a javascript based tool using the MGR\_INDEX interface
which can be found at [](https://github.com/yadij/cachemgr.js)

It is worth noting that prettiness of the reporting tool GUI is affected
by the report format produced by your Squid. Most existing Squids have
rather basic text/plain outputs intended for the cachemgr.CGI tool. It
is hoped that future releases will be more flexible.
