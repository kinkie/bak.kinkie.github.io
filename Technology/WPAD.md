# Web Proxy Auto Detection (WPAD)

## What is WPAD?

WPAD is an Internet Draft standard which attempts to enumerate the
discovery of web proxy autoconfiguration scripts. It has two main
deployment modes - DNS-based and DHCP-based - which can allow a network
administrator to provide proxy configuration scripts to clients without
explicit script path configuration in the User Agent (typically a web
browser.)

WPAD does not do much more than to allow the User Agent to discover a
[PAC or Proxy
Auto-Configuration](https://wiki.squid-cache.org/action/show/Technology/WPAD/Technology/ProxyPac#)
file.

This article is aimed at the network/system administrator who wishes to
configure automatic proxy detection on their network through WPAD. It is
not designed as a tutorial for implementation of the discovery process
in a User Agent. Please read the most recent expired draft to gather
more background information.

## When is WPAD useful?

WPAD has found use in ISP and Enterprise networks to integrate web
proxies into the network without resorting to transparent network
interception or enforcing configuration through technologies such as
Windows Active Directory Group Policy.

## WPAD Articles

  - [Fully Automatically Configuring Browsers for
    WPAD](https://wiki.squid-cache.org/action/show/Technology/WPAD/SquidFaq/ConfiguringBrowsers#head-5aa28de5e8308087a925cb7ef54ca070a16564d4)
    faq article

  - [Fully Automatically Configuring Browsers for WPAD with
    DHCP](https://wiki.squid-cache.org/action/show/Technology/WPAD/SquidFaq/ConfiguringBrowsers#head-8623ffc5e6a381ccfe77f17bbe29fa87c3cf9734)
    faq article

  - [WPAD
    DNS](https://wiki.squid-cache.org/action/show/Technology/WPAD/Technology/WPAD/DNS#)
    covers how User Agents can detect the existance of the proxy
    autoconfiguration file via DNS "Well Known Aliases"

## Other Articles and Information on WPAD

  - [](http://homepages.tesco.net/J.deBoynePollard/FGA/web-browser-auto-proxy-configuration.html)

  - [](http://www.wlug.org.nz/WPAD)

  - [](http://tools.ietf.org/wg/wrec/draft-ietf-wrec-wpad/)

  - [](http://blogs.msdn.com/wndp/articles/IPV6_PAC_Extensions_v0_9.aspx)

## WPAD-like functionality in other protocols

  - The Azereus Bittorrent client implements a WPAD-like Cache discovery
    protocol (JPC) to discover JPC-compatible caches. (Links?)

<!-- end list -->

  - [CategoryTechnologyIndex](https://wiki.squid-cache.org/action/show/Technology/WPAD/CategoryTechnologyIndex#)
    [CategoryTechnology](https://wiki.squid-cache.org/action/show/Technology/WPAD/CategoryTechnology#)
