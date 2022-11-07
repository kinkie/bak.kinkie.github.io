# Flow of a Typical Request

*NOTE: this information is a work in progress. Numbered entries have
been updated for Squid-3.*

1.  A client connection is accepted by the
    *Comm::[TcpAcceptor](/TcpAcceptor#)*,
    passed to *client-side socket support* and parsed,
    
      - or an internal Squid request is directly created via
        *clientBeginRequest*.

2.  if the traffic was intercepted, the Host: header validation is
    performed.

3.  The
    [http\_access](http://www.squid-cache.org/Doc/config/http_access#)
    controls are checked. The client-side-request builds an ACL state
    data structure and registers a callback function for notification
    when access control checking is completed.
    
      - authentication may be performed
    
      - deny\_info redirection may be performed

4.  ICAP REQMOD adaptation takes place.
    
      - an ICAP response may be produced with any HTTP status.

5.  URL-rewrite adaptation takes place.
    
      - an HTTP redirect may take place using 3xx HTTP status codes.

*the following information is outdated and seems to apply to Squid-2*

  - The client-side-request is forwarded up the client stream to
    *GetMoreData* which looks for the requested object in the cache, and
    or Vary: versions of the same. If is a cache hit, then the
    client-side registers its interest in the *StoreEntry*. Otherwise,
    Squid needs to forward the request, perhaps with an
    If-Modified-Since header.

  - The request-forwarding process begins with `protoDispatch`. This
    function begins the peer selection procedure, which may involve
    sending ICP queries and receiving ICP replies. The peer selection
    procedure also involves checking configuration options such as
    *never\_direct* and *always\_direct*.

  - When the ICP replies (if any) have been processed, we end up at
    *protoStart*. This function calls an appropriate protocol-specific
    function for forwarding the request. Here we will assume it is an
    HTTP request.

  - The HTTP module first opens a connection to the origin server or
    cache peer. If there is no idle persistent socket available, a new
    connection request is given to the Network Communication module with
    a callback function. The `comm.c` routines may try establishing a
    connection multiple times before giving up.

  - When a TCP connection has been established, HTTP builds a request
    buffer and submits it for writing on the socket. It then registers a
    read handler to receive and process the HTTP reply.

  - As the reply is initially received, the HTTP reply headers are
    parsed and placed into a reply data structure. As reply data is
    read, it is appended to the *StoreEntry*. Every time data is
    appended to the *StoreEntry*, the client-side is notified of the new
    data via a callback function. The rate at which reading occurs is
    regulated by the delay pools routines, via the deferred read
    mechanism.

  - As the client-side is notified of new data, it copies the data from
    the StoreEntry and submits it for writing on the client socket.

  - As data is appended to the *StoreEntry*, and the client(s) read it,
    the data may be submitted for writing to disk.

  - When the HTTP module finishes reading the reply from the upstream
    server, it marks the *StoreEntry* as *complete*. The server socket
    is either closed or given to the persistent connection pool for
    future use.

  - When the client-side has written all of the object data, it
    unregisters itself from the *StoreEntry*. At the same time it either
    waits for another request from the client, or closes the client
    connection.

# The Main Loop: comm\_select()

At the core of Squid is the `select(2)` system call. Squid uses
`select()` or `poll(2)` or `kqueue` or `epoll` or /dev/poll to process
I/O on all open file descriptors. Hereafter we'll only use *select* to
refer generically to either system call.

The `select()` and `poll()` system calls work by waiting for I/O events
on a set of file descriptors. Squid only checks for *read* and *write*
events. Squid knows that it should check for reading or writing when
there is a read or write handler registered for a given file descriptor.
Handler functions are registered with the `commSetSelect` function. For
example:

    commSetSelect(fd, COMM_SELECT_READ, clientReadRequest, conn, 0);

In this example, *fd* is a TCP socket to a client connection. When there
is data to be read from the socket, then the select loop will execute

    clientReadRequest(fd, conn);

The I/O handlers are reset every time they are called. In other words, a
handler function must re-register itself with `commSetSelect` if it
wants to continue reading or writing on a file descriptor. The I/O
handler may be canceled before being called by providing NULL arguments,
e.g.:

    commSetSelect(fd, COMM_SELECT_READ, NULL, NULL, 0);

These I/O handlers (and others) and their associated callback data
pointers are saved in the *fde* data structure:

    struct _fde {
            ...
            PF *read_handler;
            void *read_data;
            PF *write_handler;
            void *write_data;
            close_handler *close_handler;
            DEFER *defer_check;
            void *defer_data;
    };

*read\_handler* and *write\_handler* are called when the file descriptor
is ready for reading or writing, respectively. The *close\_handler* is
called when the filedescriptor is closed. The *close\_handler* is
actually a linked list of callback functions to be called.

In some situations we want to defer reading from a filedescriptor, even
though it has data for us to read. This may be the case when data
arrives from the server-side faster than it can be written to the
client-side. Before adding a filedescriptor to the *read set* for
select, we call *defer\_check* (if it is non-NULL). If *defer\_check*
returns 1, then we skip the filedescriptor for that time through the
select loop.

These handlers are stored in the *FD\_ENTRY* structure as defined in
`comm.h`. `fd_table[]` is the global array of *FD\_ENTRY* structures.
The handler functions are of type *PF*, which is a typedef:

``` 
    typedef void (*PF) (int, void *);
```

The close handler is really a linked list of handler functions. Each
handler also has an associated pointer `(void *data)` to some kind of
data structure.

`comm_select()` is the function which issues the select() system call.
It scans the entire `fd_table[]` array looking for handler functions.
Each file descriptor with a read handler will be set in the `fd_set`
read bitmask. Similarly, write handlers are scanned and bits set for the
write bitmask. `select()` is then called, and the return read and write
bitmasks are scanned for descriptors with pending I/O. For each ready
descriptor, the handler is called. Note that the handler is cleared from
the *FD\_ENTRY* before it is called.

After each handler is called, `comm_select_incoming()` is called to
process new HTTP and ICP requests.

Typical read handlers are `httpReadReply()`, `diskHandleRead()`,
`icpHandleUdp()`, and `ipcache_dnsHandleRead()`. Typical write handlers
are `commHandleWrite()`, `diskHandleWrite()`, and `icpUdpReply()`. The
handler function is set with `commSetSelect()`, with the exception of
the close handlers, which are set with `comm_add_close_handler()`.

The close handlers are normally called from `comm_close()`. The job of
the close handlers is to deallocate data structures associated with the
file descriptor. For this reason `comm_close()` must normally be the
last function in a sequence to prevent accessing just-freed memory.

The timeout and lifetime handlers are called for file descriptors which
have been idle for too long. They are further discussed in a following
chapter.
