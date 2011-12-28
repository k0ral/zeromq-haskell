This library provides Haskell bindings to 0MQ 3.1.x (http://zeromq.org).

Current status
--------------

This software currently has *beta* status, i.e. it had seen limited testing.

Version 0.1 - First release to provide bindings against 0MQ 3.1.x

This software requires 0MQ version 3.1.x.

Installation
------------

As usual for Haskell packages this software is installed best via Cabal
(http://www.haskell.org/cabal). In addition to GHC it depends on 0MQ of course.

Notes
-----

zeromq3-haskell mostly follows 0MQ's API. One difference though is that sockets
are parameterized types, i.e. there is not one socket type but when creating a
socket the desired socket type has to be specified, e.g. `Pair` and the
resulting socket is of type `Socket Pair`.
This additional type information is used to ensure that only options applicable
to the socket type can be set, hence `ZMQ_SUBSCRIBE` and `ZMQ_UNSUBSCRIBE` which
only apply to `ZMQ_SUB` sockets have their own functions (`subscribe` and
`unsubscribe`) which can only be used with sockets of type `Socket Sub`.

Other differences are mostly for convenience. Also one does not deal directly
with 0MQ messages, instead these are created internally as needed.

Finally note that `receive` is already used in a non-blocking way internally.
GHC's I/O manager is used to wait for data to be available, so from a client's
perspective `receive` appears to be blocking.

Differences to the 0MQ 2.1.x binding
------------------------------------

This library is based on the zeromq-haskell binding for 0MQ 2.1.x. Socket types
and options have been aligned with 0MQ 3.1.x and instead of using a big
`SocketOption` datatype, this library provides separate get and set functions for
each available option, e.g. `affinity`/`setAffinity`.

Examples
--------

The test folder contains some simple tests mostly mimicking the ones that come
with 0MQ.

Bugs
----

If you find any bugs or other shortcomings I would greatly appreciate a bug
report, preferably via http://github.com/twittner/zeromq-haskell/issues or
e-mail to toralf.wittner@gmail.com

