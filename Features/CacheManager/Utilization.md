# utilization report

The utilization report details statistics about the amount and type of
traffic through the Squid.

First shown are the statistics for several time periods, as detailed in
the section headers. These range from previous 5 minutes up to several
days. They show the KB/second throughput rates for each traffic type.

Finally the total statistics since Squid was started. This is an *all
time* report with absolute counts in bytes, KB, or seconds.

## What is server.other?

Other is a default category to track objects which don't fall into one
of the defined categories.

## What is the Max/Current/Min KB?

These refer to the size all the objects of this type have grown
to/currently are/shrunk to.

## What is the I/O section about?

These are histograms on the number of bytes read from the network per
read(2) call. Somewhat useful for determining maximum buffer sizes.

## Example Report

    Cache Utilisation:
    
    Last 5 minutes:
    sample_start_time = 1328057189.495655 (Wed, 01 Feb 2012 00:46:29 GMT)
    sample_end_time = 1328057489.497188 (Wed, 01 Feb 2012 00:51:29 GMT)
    client_http.requests = 2.146656/sec
    client_http.hits = 0.000000/sec
    client_http.errors = 0.000000/sec
    client_http.kbytes_in = 0.219999/sec
    client_http.kbytes_out = 0.559997/sec
    client_http.all_median_svc_time = 0.177113 seconds
    client_http.miss_median_svc_time = 0.177113 seconds
    client_http.nm_median_svc_time = 0.000000 seconds
    client_http.nh_median_svc_time = 0.000000 seconds
    client_http.hit_median_svc_time = 0.000000 seconds
    server.all.requests = 2.306655/sec
    server.all.errors = 0.000000/sec
    server.all.kbytes_in = 0.266665/sec
    server.all.kbytes_out = 0.469998/sec
    server.http.requests = 2.306655/sec
    server.http.errors = 0.000000/sec
    server.http.kbytes_in = 0.266665/sec
    server.http.kbytes_out = 0.469998/sec
    server.ftp.requests = 0.000000/sec
    server.ftp.errors = 0.000000/sec
    server.ftp.kbytes_in = 0.000000/sec
    server.ftp.kbytes_out = 0.000000/sec
    server.other.requests = 0.000000/sec
    server.other.errors = 0.000000/sec
    server.other.kbytes_in = 0.000000/sec
    server.other.kbytes_out = 0.000000/sec
    icp.pkts_sent = 0.000000/sec
    icp.pkts_recv = 0.000000/sec
    icp.queries_sent = 0.000000/sec
    icp.replies_sent = 0.000000/sec
    icp.queries_recv = 0.000000/sec
    icp.replies_recv = 0.000000/sec
    icp.replies_queued = 0.000000/sec
    icp.query_timeouts = 0.000000/sec
    icp.kbytes_sent = 0.000000/sec
    icp.kbytes_recv = 0.000000/sec
    icp.q_kbytes_sent = 0.000000/sec
    icp.r_kbytes_sent = 0.000000/sec
    icp.q_kbytes_recv = 0.000000/sec
    icp.r_kbytes_recv = 0.000000/sec
    icp.query_median_svc_time = 0.000000 seconds
    icp.reply_median_svc_time = 0.000000 seconds
    dns.median_svc_time = 0.028094 seconds
    unlink.requests = 0.000000/sec
    page_faults = 0.116666/sec
    select_loops = 73.239626/sec
    select_fds = 13.123266/sec
    average_select_fd_period = 0.000000/fd
    median_select_fds = -1.000000
    swap.outs = 0.000000/sec
    swap.ins = 0.000000/sec
    swap.files_cleaned = 0.000000/sec
    aborted_requests = 0.000000/sec
    syscalls.disk.opens = 0.000000/sec
    syscalls.disk.closes = 0.000000/sec
    syscalls.disk.reads = 0.000000/sec
    syscalls.disk.writes = 0.000000/sec
    syscalls.disk.seeks = 0.000000/sec
    syscalls.disk.unlinks = 0.000000/sec
    syscalls.sock.accepts = 2.313322/sec
    syscalls.sock.sockets = 0.166666/sec
    syscalls.sock.connects = 0.166666/sec
    syscalls.sock.binds = 0.000000/sec
    syscalls.sock.closes = 2.146656/sec
    syscalls.sock.reads = 4.453311/sec
    syscalls.sock.writes = 4.459977/sec
    syscalls.sock.recvfroms = 0.013333/sec
    syscalls.sock.sendtos = 0.006667/sec
    cpu_time = 1.632102 seconds
    wall_time = 300.001533 seconds
    cpu_usage = 0.544031%
    
    Last 15 minutes:
    sample_start_time = 1328056589.495302 (Wed, 01 Feb 2012 00:36:29 GMT)
    sample_end_time = 1328057489.497188 (Wed, 01 Feb 2012 00:51:29 GMT)
    client_http.requests = 0.715554/sec
    client_http.hits = 0.000000/sec
    client_http.errors = 0.000000/sec
    client_http.kbytes_in = 0.073333/sec
    client_http.kbytes_out = 0.186666/sec
    client_http.all_median_svc_time = 0.177113 seconds
    client_http.miss_median_svc_time = 0.177113 seconds
    client_http.nm_median_svc_time = 0.000000 seconds
    client_http.nh_median_svc_time = 0.000000 seconds
    client_http.hit_median_svc_time = 0.000000 seconds
    server.all.requests = 0.768887/sec
    server.all.errors = 0.000000/sec
    server.all.kbytes_in = 0.088889/sec
    server.all.kbytes_out = 0.156666/sec
    server.http.requests = 0.768887/sec
    server.http.errors = 0.000000/sec
    server.http.kbytes_in = 0.088889/sec
    server.http.kbytes_out = 0.156666/sec
    server.ftp.requests = 0.000000/sec
    server.ftp.errors = 0.000000/sec
    server.ftp.kbytes_in = 0.000000/sec
    server.ftp.kbytes_out = 0.000000/sec
    server.other.requests = 0.000000/sec
    server.other.errors = 0.000000/sec
    server.other.kbytes_in = 0.000000/sec
    server.other.kbytes_out = 0.000000/sec
    icp.pkts_sent = 0.000000/sec
    icp.pkts_recv = 0.000000/sec
    icp.queries_sent = 0.000000/sec
    icp.replies_sent = 0.000000/sec
    icp.queries_recv = 0.000000/sec
    icp.replies_recv = 0.000000/sec
    icp.replies_queued = 0.000000/sec
    icp.query_timeouts = 0.000000/sec
    icp.kbytes_sent = 0.000000/sec
    icp.kbytes_recv = 0.000000/sec
    icp.q_kbytes_sent = 0.000000/sec
    icp.r_kbytes_sent = 0.000000/sec
    icp.q_kbytes_recv = 0.000000/sec
    icp.r_kbytes_recv = 0.000000/sec
    icp.query_median_svc_time = 0.000000 seconds
    icp.reply_median_svc_time = 0.000000 seconds
    dns.median_svc_time = 0.028094 seconds
    unlink.requests = 0.000000/sec
    page_faults = 0.038889/sec
    select_loops = 74.120956/sec
    select_fds = 4.374435/sec
    average_select_fd_period = 0.000000/fd
    median_select_fds = -1.000000
    swap.outs = 0.000000/sec
    swap.ins = 0.000000/sec
    swap.files_cleaned = 0.000000/sec
    aborted_requests = 0.000000/sec
    syscalls.disk.opens = 0.000000/sec
    syscalls.disk.closes = 0.000000/sec
    syscalls.disk.reads = 0.000000/sec
    syscalls.disk.writes = 0.000000/sec
    syscalls.disk.seeks = 0.000000/sec
    syscalls.disk.unlinks = 0.000000/sec
    syscalls.sock.accepts = 0.771109/sec
    syscalls.sock.sockets = 0.055555/sec
    syscalls.sock.connects = 0.055555/sec
    syscalls.sock.binds = 0.000000/sec
    syscalls.sock.closes = 0.715554/sec
    syscalls.sock.reads = 1.484441/sec
    syscalls.sock.writes = 1.486664/sec
    syscalls.sock.recvfroms = 0.004444/sec
    syscalls.sock.sendtos = 0.002222/sec
    cpu_time = 1.800113 seconds
    wall_time = 900.001886 seconds
    cpu_usage = 0.200012%
    
    Last hour:
    (no values recorded yet)
    
    Last 8 hours:
    (no values recorded yet)
    
    Last day:
    (no values recorded yet)
    
    Last 3 days:
    (no values recorded yet)
    
    Totals since cache startup:
    sample_time = 1328057489.497188 (Wed, 01 Feb 2012 00:51:29 GMT)
    client_http.requests = 3505
    client_http.hits = 0
    client_http.errors = 3
    client_http.kbytes_in = 332
    client_http.kbytes_out = 900
    client_http.hit_kbytes_out = 0
    server.all.requests = 3500
    server.all.errors = 0
    server.all.kbytes_in = 437
    server.all.kbytes_out = 714
    server.http.requests = 3500
    server.http.errors = 0
    server.http.kbytes_in = 437
    server.http.kbytes_out = 714
    server.ftp.requests = 0
    server.ftp.errors = 0
    server.ftp.kbytes_in = 0
    server.ftp.kbytes_out = 0
    server.other.requests = 0
    server.other.errors = 0
    server.other.kbytes_in = 0
    server.other.kbytes_out = 0
    icp.pkts_sent = 0
    icp.pkts_recv = 0
    icp.queries_sent = 0
    icp.replies_sent = 0
    icp.queries_recv = 0
    icp.replies_recv = 0
    icp.query_timeouts = 0
    icp.replies_queued = 0
    icp.kbytes_sent = 0
    icp.kbytes_recv = 0
    icp.q_kbytes_sent = 0
    icp.r_kbytes_sent = 0
    icp.q_kbytes_recv = 0
    icp.r_kbytes_recv = 0
    unlink.requests = 0
    page_faults = 40
    select_loops = 133050
    cpu_time = 8.620538
    wall_time = 37.174004
    swap.outs = 0
    swap.ins = 0
    swap.files_cleaned = 0
    aborted_requests = 0
