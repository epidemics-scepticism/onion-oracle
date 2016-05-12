# onion-oracle
rendezvous circuit build-time as a timing oracle through Tor Browser

When Tor connects to an onion service, it builds a redezvous circuit. It fetches a descriptor from the appropriate Hidden Service Director{y,ies}, it picks an Introduction Point advertised on the descriptor and builds a circuit to it, it picks a Rendezvous Point and asks the Introduction Point to tell the onion service to meet it at the Rendezvous Point. Once both meet-in-the-middle at the Rendezvous point, the Tor client is ready to talk directly to the onion service. This process takes time to complete.

When a browser makes an XMLHTTPRequest, it only knows once the request is complete if it should actually do anything with the content, since this is defined in the CORS headers in the response to the XMLHTTPRequest.

By making an XMLHTTPRequest to an .onion service, we can measure the "time-to-fail", by making two requests and looking at how long it takes the first and second to fail. If the first took significantly longer to fail, we can determine that a rendezvous circuit had to be build for the request. If both requests took around the same time, then we may suspect that this is a sign that a circuit had already been built by the Tor process, that it had already made a connection to the onion service.
