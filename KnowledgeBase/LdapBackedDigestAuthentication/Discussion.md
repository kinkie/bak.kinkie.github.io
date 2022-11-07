See [Discussed
Page](https://wiki.squid-cache.org/action/show/KnowledgeBase/LdapBackedDigestAuthentication/Discussion/KnowledgeBase/LdapBackedDigestAuthentication#)

A basic authorization mechanism can be implemented using digest auth.

Similar to session helper with ACTIVE loging we can redirect all http
non-authorized traffic to a digest authenticated "LOGIN" by IP service.

It is much more secure then basic auth or a simple user password form.

The other option is to use ssl encrypted page for ip authorization.

\-- [Eliezer
Croitoru](https://wiki.squid-cache.org/action/show/KnowledgeBase/LdapBackedDigestAuthentication/Discussion/Eliezer%20Croitoru#)
