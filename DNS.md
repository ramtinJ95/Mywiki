## DNS

The process of DNS resolution involves converting a hostname into a
computer-friendly OP addresss. In order to understadn the process behind the DNS
resolution, its important to learn about the diffrent hardware components a DNS
query must pass between. For the web broser the DNS lookup occurs "behind
the scenes" and reuqires no interaction from the users computer apart from the
intial request.

There are 4 DNS servers invovled in loading a webpage:
1. DNS recursor - The recursor can be thought of as a librarian who is asked to
   go find a particular book somewhere ina library. The DNS recursor is a server
   designer to recieve queries from client machines through applications such as
   web broswers. Typically the recursor is then responsible for making
   additional requests i order to satisfy the clients DNS query.
2. Root nameserver - the root server is the first step in translating(resolving)
   human readable host names into IP adresses. It can be thought of like an
   index that points to different racks of books - typcially it serves as a
   reference to other more specific locations.
3. TLD nameserver - the top level domain server can be thought of as a specific
   rack of books in a library. This nameserver is the next step in the serarch
   for a specific IP address and it hosts the last portion of a hostname (in
   example.com the TLD server is "com").
4. Authoritative nameserver - This final nameserver can be thought of as a
   dictionary on a rack of books, in which a specific name can be translated
   into its definition. The Authoritative nameserver is the last stop in the
   nameserver query. If the Authoritative nameserver has access to the requested
   record it will retunr the IP affess for the requested hostname back to the
   DNS recursor that made the initial request.

The following is an 8 step process that a DNS lookup goes through if nothing is
cached at any layer. This is unlikely but a good way to understand the flow of things.

1. A user types example.com into a web browser and the query travles into the
   internet and is recieved by a DNS recursive resolver.
2. The resolver then queries a DNS root nameserver.
3. The root server then responds to the resolved with the address of a top level
   domain DNS server (such as .com or .net) which stores the infromation for its
   domains. When searching for example.com our request is pointed toward the
   .com TLD.
4. The resolver then makes a request to the .com TLD.
5. The TLD server then responds with the IP address of the domain's nameserver,
   exmaple.com
6. Lastly the recursive resolver sends a query to the domain's nameserver.
7. The IP address for example.com is then returned to the resolver from the namerserver
8. The DNS resolver then responds to the web browser with the IP address of the
   domain requested intially.

Once the 8 steps of the DNS lookup have returned the IP address of example.com
the browser is able to make the request for the web page.
9. The browser makes a HTTP request to the IP address
10. The server at that IP returns the webpage to be rendered in the browser.

In a typical DNS lookup three types of queries occur. By using a combination of
these queries an optimized process for DNS resolution can result in a reduction
of distance traveled. In an ideal situation  cached record data will be
available, allowing a DNS name server to return a non-recursive query.
1. Recursive query - In a recursive query a DNS client requires that a DNS
   server (typically a DNS recursive resolver) will respond to the client with
   either the requested resource recourd or an error mesage if the resolver cant
   find the record.
2. iterative query - in this situation the DNS client will allow a DNS server to
   return the best answer it can. If the queried DNS server does not have a
   match for the query name, it will return a referral to a DNS server
   authoratitive for a lower level of the domain namespace. The DNS client will
   then make a query to the referral address. This process continues with
   additional DNS servers down the query chain until either an error or a
   timeout occures.
3. Non-recursive query - typically this will occur when a DNS resolver client
   queries a DNS server for a record that it has access to either because its
   authorative for the record or the record exists inside of its cache.
   Typically, a DNS server will cache DNS records to prevent additional
   bandwidth consumption and load on upstream servers.

## DNS cacheing
DNS cacheing invovles storing data closer to the requesting client so that the
DNS query can be resolved earlier and additional queries further down the DNS
lookup chain can be avoided, thereby improving load times and reducing
bandwidth/cpu consumption. DNS data can be cached in a variety of locations,
each of which will store DNS records for a set amount of time determined by a
time to live(ttl)


### Browser DNS caching

