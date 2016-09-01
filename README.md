# sharder

When you try to install or update a package through RStudio, it finds a decent mirror in its internal network and
grabs the files from that. When you try to install or update a package through another IDE, or the REPL, or
any *other* mechanism, the defaults don't let you do that.

<code>sharder</code> is a service I've been developing for the CRAN administrators that geolocates the IPs of incoming
requests and directs them to a randomly-selected mirror in their country, with the ability to filter down to
https-supporting mirrors where available. The plan is to deploy it and have it act as an intermediary, so that
code>install.packages</code> logic will go:

1. If they've specified a mirror, use that:
2. If they haven't, query <code> sharder</code>;
3. If <code>sharder</code> can't find anything, *then* ask.

This should dramatically cut down the amount of time R programmers spend looking at 117-option menus in their terminal.
