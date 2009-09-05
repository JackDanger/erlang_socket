Socket.erl
=======

Provides a thin api around gen_tcp and ssl sockets allowing you to
flexibly work with socket with and without encryption.

Features:

  * listens on a port with either ssl encryption or plain tcp
  * handles asynchronous connection events via both protocols
  * encapsulates all the nasty bits of erlang socket options
  * allows easy upgrading of tcp connections via to_ssl_* functions
  * helps you apply reasonable default options to all sockets

Written by Jack Danger Canty (code@jackcanty.com)

Extracted from gen_smtp written by Andrew Thompson (andrew@hijacked.us)
