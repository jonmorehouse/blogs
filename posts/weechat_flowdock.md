Getting Weechat up and running with Flowdock (Mac)
==================================================

I recently converted to Weechat, from irssi. For me, its easier, more intuitive and quicker to get up and running than irssi. While its fairly easy to get up and running with Freenode on weechat, getting SSL up and running while on OSX isn't quite as easy. Flowdock's IRC channel requires ssl connections.

I've used HipChat for a while, but recently converted to Flowdock because of their robust IRC channel (ssl, in house and not through bitlbee) and because its easy to connect to the services I need on a daily basis.

Install Weechat
---------------

For starters, lets get the latest weechat client and make sure we have access to a few different script types. We'll be doing this using homebrew.

<script src="https://gist.github.com/anonymous/9592645.js"></script>

Note that all weechat configuration lives in $HOME/.weechat. You can edit files directly there (though, make sure weechat isn't running as it writes these files at close). 

Create a ca-certificates file
-----------------------------

While Irssi allows you to use `/connect -SSL irc.flowdock.com 6697`, things aren't as easy on Weechat. You'll need to create a ca-certificates.crt file for connecting to SSL enabled servers. I followed this [tutorial](http://slowhash.com/2013/08/17/ca-certificates-crt-for-macosx/)

<script src="https://gist.github.com/anonymous/9592646.js"></script>

Basic configuration steps for running Flowdock on Weechat
---------------------------------------------------------

<script src="https://gist.github.com/anonymous/9592662.js"></script>

Check $HOME/.weechat/irc.conf
-----------------------------

If everything worked out, your irc.conf file should have a server entry similar to this:

<script src="https://gist.github.com/anonymous/9592669.js"></script>

You should now be able to connect to flowdock with `/connect flowdock` while in Weechat. You will automatically be sent to your first flow once connected.


