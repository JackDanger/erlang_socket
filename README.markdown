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

Written by [Jack Danger Canty](http://jackcanty.com)

Extracted from [gen_smtp](http://github.com/Vagabond/gen_smtp) written by Andrew Thompson (andrew@hijacked.us)

![Socket Image](http://farm4.static.flickr.com/3192/2561854165_e4d74d95c2_m.jpg)
<small>image by [incurable hippie](http://www.flickr.com/photos/hippie/)</small>