Handling Anonymous Clients
==========================

This document describes how EWP servers should declare that some of their
endpoints can handle anonymous clients.

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


Details
-------

It can make sense to allow some HTTP endpoints to be called by anonymous clients
(as opposed to making it available only to EWP members).

Note, that this specification does not currently define how servers should
handle [cross-origin resource sharing][cors]. Clients SHOULD NOT assume that
such servers allow external AJAX requests.


Making the request
------------------

In order to make an anonymous request, the client simply makes a regular
HTTP(S) request, without any client certificates nor signatures.

This kind of request is compatible with many other client authentication
methods, so that it can be served on the same URL along with them.


Security considerations
-----------------------

### When to use this method

This method is listed under "Client Authentication Methods" chapter, but
obviously it does not provide any authentication, nor protection against replay
attacks. It should be used only when the accessed resource doesn't contain any
confidential data and it can be accessed publicly.


### Main security questions

The [Authentication and Security][sec-intro] document
[recommends][sec-method-rules] that each client authentication method
specification explicitly answers the following questions:

> How the client's request must look like? How can the server detect that the
> client is using this particular method for authentication?

Request look like a regular HTTP request, with no extra headers, etc. The
server can deduce that this method is used, if it fails to detect that any of
the other methods supported by the server are used.

> How can the server verify which HEIs are covered by the requester?

No HEIs are covered by the requester. The request is anonymous.

> How can the server verify that the request has not been tampered with, nor
> replayed by a third party?

It cannot.

> Does it provide non-repudiation? Can a server provide a solid proof later
> on, that a particular request took place, and that it originated from a
> certain client?

No.


[develhub]: http://developers.erasmuswithoutpaper.eu/
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management/blob/stable-v1/README.md#statuses
[cors]: https://en.wikipedia.org/wiki/Cross-origin_resource_sharing
[sec-method-rules]: https://github.com/erasmus-without-paper/ewp-specs-sec-intro#rules
[sec-intro]: https://github.com/erasmus-without-paper/ewp-specs-sec-intro
