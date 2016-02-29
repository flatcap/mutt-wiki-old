TLS-SNI Patch
=============

Negotiate with a server for a TSL/SSL certificate

Patch
-----

To check if Mutt supports “TLS-SNI”, look for “patch-tls-sni” in the
mutt version.

**Dependencies**
-   mutt-1.5.24
-   OpenSSL

Introduction
------------

The “TLS-SNI” patch adds support for TLS virtual hosting. If your mail
server doesn't support this everything will still work normally.

TLS supports sending the expected server hostname during the handshake,
via the SNI extension. This can be used to select a server certificate
to issue to the client, permitting virtual-hosting without requiring
multiple IP addresses.

This has been tested against Exim 4.80, which optionally logs SNI and
can perform vhosting.

To verify TLS SNI support by a server, you can use:

    openssl s_client -host <imap server> -port <port> -tls1 -servername <imap server>

Muttrc
------

None

See Also
--------

None

Known Bugs
----------

None

Credits
-------

-   Jeremy Katz \<katzj@linuxpower.org\>
-   Phil Pennock \<mutt-dev@spodhuis.demon.nl\>
-   Richard Russon \<rich@flatcap.org\>
