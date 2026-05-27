A reverse proxy is a server that sits in front of one or more web servers,
intercepting requests from clients. This is different from a [Proxy Server](Proxy Server) where the proxy sits in front of clients. With a reverse proxy the requests to websites get intercepted at the network edge. The reverse proxy sever will then send requests to and recieve responses from the origin server.

Meaning in simple terms when you send a request to reach some web server,
without a reverse proxy you would reach that server through the internet
directly, now instead your requests hit the proxy server first which either
sends you to were you need to go or does something else.

The following are some of the major reasons behind a reverse proxy:
* Load balancing - If there is a popular website maybe one origin server cant
handle all incoming traffic. In such cases a reverse proxy can then be used to
route and distribute the load between many servers. Or if there is a failure of
a server then requests can be sent to some other server for a while etc.
* Protection from attacks - With a reverse proxy in place a website or service
dont need to reveal the ip of the origin servers. This makes it much harder for
attackers to overwhelm or overload their servers through ddos attacks.
* Caching - A reverse proxy can also cache content, resulting in faster
performance. For example, if a user in Paris visits a reverse-proxied website
with web servers in Los Angeles, the user might actually connect to a local
reverse proxy server in Paris, which will then have to communicate with an
origin server in L.A. The proxy server can then cache (or temporarily save) the
response data. Subsequent Parisian users who browse the site will then get the
locally cached version from the Parisian reverse proxy server, resulting in much
faster performance.
* SSL encryption - Encrypting and decrypting SSL or TLS communication for each
client can be computationally expensive for an origin server. A reverse proxy
can be configured to decrypt all incoming requests and encrypt all outgoing
responses, freeing up valuable resources on the origin server.
