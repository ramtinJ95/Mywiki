## Proxy server
A proxy server (sometimes called forward proxy) is a server that sits in front 
of a group of client machines. When those machines make requests to sites or service 
on the Internet the proxy intercepts those requests and communicates with the 
webservers on behalf of those clients.

There are a few reasons why someone would add this middleman complexity of a
forward proxy.

* If some org is using a firewall to limit access to internet in some way, then
  a forward proxy can be used to get around them, as a proxy lets the user
connect to the proxy rather than directly to the sites they are visiting.
* On the other hand proxies can also be setup to block a group of users from
accessing certain sites. for example a school network might be configured to
connect to the web through a proxy which enables content filtering rules,
refusing to forward responses from Facebook and other social media sites.
* In some cases regular internet users want to increse their anonymity online or
  if they live in a place where the government can impose serious consequences
to political dissidents. In such cases using a forward proxy to connect to a
website the IP adress used will be hard to trace back to a user instead the ip
of the proxy will be seen. 
