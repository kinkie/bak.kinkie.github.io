The **Cache Manager** is the Squid internal subsystem that provides a
common way for registering, finding and triggering management actions.
It interfaces with the outside world through the normal Squid HTTP
server, responding requests made with the [cache\_object
scheme](https://wiki.squid-cache.org/action/show/CacheManager/CacheObjectScheme#)
or with the `/squid-internal-mgr` well-known URL path. Sometimes it is
confused with the [Cache Manager
CGI](https://wiki.squid-cache.org/action/show/CacheManager/CacheManagerCgi#).
This last one is just an external CGI application that reads data from
the Squid Cache Manager and presents in HTML.

A table with existing actions is maintained by the subsystem. For each
tuple it will bring up a unique name for the specific action, a short
description and a handler to be called when the item is invoked. Some
flags can be set too, like the one that indicates the requirement of a
password.

At the time of initialization only a few actions will be registered. The
most important of all is the **menu**, responsible for enumerating
current available actions in the table. After this initialization
various snippets of code will register different new handlers and
descriptions using the `Mgr::RegisterAction` API.

Internally, the handlers are C functions with a common prototype.

# See also

  - [CacheManagerObject](https://wiki.squid-cache.org/action/show/CacheManager/CacheManagerObject#)

  - [CacheObjectProtocol](https://wiki.squid-cache.org/action/show/CacheManager/CacheObjectProtocol#)

  - [CacheObjectScheme](https://wiki.squid-cache.org/action/show/CacheManager/CacheObjectScheme#)

  - [CacheManagerCgi](https://wiki.squid-cache.org/action/show/CacheManager/CacheManagerCgi#)
