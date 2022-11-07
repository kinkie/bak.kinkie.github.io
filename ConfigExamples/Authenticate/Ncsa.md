# Authenticate with NCSA httpd-style password file

**Warning**: Any example presented here is provided "as-is" with no
support or guarantee of suitability. If you have any further questions
about these examples please email the squid-users mailing list.

## Outline

In this example a squid installation will use NCSA to authenticate users
before allowing them to use the proxy.

## Usage

## The password file

Creating a new password file:

    htpasswd -c -nbm /etc/squid/passwords username password

Adding users:

    htpasswd -nbm /etc/squid/passwords username password

Deleting users:

    htpasswd -D -nbm /etc/squid/passwords username password

  - ![/\!\\](https://wiki.squid-cache.org/wiki/squidtheme/img/alert.png)
    The **m** option specifies MD5 encryption which is the default for
    htpasswd.

Squid helpers support DES, MD5 and SHA encryption of the passwords file.
Bcrypt requires additional support in the crypto libraries Squid is
built with so may or may not work.

## Squid Configuration File

Paste the configuration file like this:

    auth_param basic program /usr/lib/squid/basic_ncsa_auth /etc/squid/passwords
    auth_param basic children 5
    auth_param basic credentialsttl 1 minute

The basic auth ACL controls to make use of it are:

    acl auth proxy_auth REQUIRED
    
    http_access deny !auth
    http_access allow auth
    http_access deny all

[CategoryConfigExample](https://wiki.squid-cache.org/action/show/ConfigExamples/Authenticate/Ncsa/CategoryConfigExample#)
