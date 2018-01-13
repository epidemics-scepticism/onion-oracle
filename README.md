# Update
Thought I'd update this just to add a notice here that Tor Buttons new approach to circuit isolation by first party domain means that this no longer works as well as it used to but you may still be able to time the HSDir descriptor fetch.

This still works if you're not using Tor Browser.

# Onion Oracle
#### or rendezvous circuit build time as an oracle through XHR

When Tor connects to an onion service, it builds a `Redezvous Circuit`. It fetches a descriptor from the appropriate `Hidden Service Director{y,ies}`, it picks an `Introduction Point` advertised on the descriptor and builds a circuit to it, it picks a `Rendezvous Point` and asks the `Introduction Point` to tell the onion service to meet it at the `Rendezvous Point`. Once both meet-in-the-middle at the `Rendezvous Point`, the Tor client is ready to talk directly to the onion service. This process takes time to complete.

When a browser makes an `XMLHTTPRequest`, it only knows once the request is complete if it should actually do anything with the content, since this is defined in the `CORS` headers in the response to the `XMLHTTPRequest`.

By making an `XMLHTTPRequest` to an onion service, we can measure the "time-to-fail".

By making *two* requests and comparing how long it takes the first and second to fail we can collect evidence that shows it is likely that the browser had already visted or is already visiting a certain onion service. If the first took significantly longer to fail, we can determine that a `Rendezvous Circuit` had to be build for the request, meaning that one did not already exist. If both requests took around the same time, then we may suspect that this is a sign that a `Rendezvous Circuit` had already been built by the Tor process.

###### Two measurements is a terrible sample set for any kind of side-channel attack, as such the real world impact and conclusions drawn from this method shouldn't be taken as anything but a curiosity.

## Mitigations
Use Tor Browser's 'New Identity' button, this will mean in future new circuits will be used thus removing any possible timing artifacts.
