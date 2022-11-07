# IP Cache and FQDN Cache

## Introduction

The IP cache is a built-in component of squid providing Hostname to
IP-Number translation functionality and managing the involved
data-structures. Efficiency concerns require mechanisms that allow
non-blocking access to these mappings. The IP cache usually doesn't
block on a request except for special cases where this is desired (see
below).

## Data Structures

The data structure used for storing name-address mappings is a small
hashtable (*static hash\_table \*ip\_table*), where structures of type
*ipcache\_entry* whose most interesting members are:

    struct _ipcache_entry {
            char *name;
            time_t lastref;
            ipcache_addrs addrs;
            struct _ip_pending *pending_head;
            char *error_message;
            unsigned char locks;
            ipcache_status_t status:3;
    }

## External overview

Main functionality is provided through calls to:

  - `ipcache_nbgethostbyname(const char *name, IPH *handler, void
    *handlerdata)`
    
      - where *name* is the name of the host to resolve, *handler* is a
        pointer to the function to be called when the reply from the IP
        cache (or the DNS if the IP cache misses) and *handlerdata* is
        information that is passed to the handler and does not affect
        the IP cache.

  - `ipcache_gethostbyname(const char *name,int flags)`
    
      - is different in that it only checks if an entry exists in it's
        data-structures and does not by default contact the
        
        DNS, unless this is requested, by setting the *flags* to
        *IP\_BLOCKING\_LOOKUP* or *IP\_LOOKUP\_IF\_MISS*.

  - `ipcache_init()`
    
      - is called from *mainInitialize()* after disk initialization and
        prior to the reverse fqdn cache initialization

  - `ipcache_restart()`
    
      - is called to clear the IP cache's data structures, cancel all
        pending requests.
        
        Currently, it is only called from *mainReconfigure*.

## Internal Operation

Internally, the execution flow is as follows: On a miss,
*ipcache\_getnbhostbyname* checks whether a request for this name is
already pending, and if positive, it creates a new entry using
*ipcacheAddNew* with the *IP\_PENDING* flag set . Then it calls
*ipcacheAddPending* to add a request to the queue together with data and
handler. Else, *ipcache\_dnsDispatch()* is called to directly create a
DNS query or to *ipcacheEnqueue()* if all no DNS port is free.
*ipcache\_call\_pending()* is called regularly to walk down the pending
list and call handlers. LRU clean-up is performed through
*ipcache\_purgelru()* according to the *ipcache\_high* threshold.
