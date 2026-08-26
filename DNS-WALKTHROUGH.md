# What happens after someone types a website address

DNS is the part of the internet that turns a name a person can remember into the place a
browser should contact. A browser cannot send a request to `example.com` by itself; it
needs an IP address. DNS supplies that answer.

When someone enters my site address, the browser first checks whether it already knows the
answer. The operating system and the network's DNS resolver also keep short-lived caches.
If none of them has a usable cached answer, the resolver asks the DNS hierarchy. It starts
at a root nameserver, which points it toward the nameservers for the top-level domain such
as `.com`. A `.com` nameserver then points it toward the authoritative nameserver for the
specific domain. That authoritative server is where the domain's actual records live.

The resolver returns the matching record to the browser and caches it for the record's
TTL, or time to live. The browser can then connect to the returned host, negotiate HTTPS,
send an HTTP request, and receive the HTML, CSS, images, or other files that make up the
page. DNS finds the destination; it does not serve the page itself.

## Where a CNAME fits

A CNAME record makes one hostname an alias of another hostname. For example,
`www.example.com` could point to a hostname operated by a static host. The resolver then
continues resolving the target name until it reaches an address record. This lets the
hosting company change its infrastructure without asking every customer to replace an IP
address in DNS.

A CNAME is different from a redirect. DNS never tells the browser to visit a new URL; it
only helps it find the machine behind the name. An HTTP redirect happens later, after the
browser has already connected to a server.

## My current setup

My portfolio uses the free GitHub Pages address
[`https://krcgoktug.github.io`](https://krcgoktug.github.io). GitHub controls the
`github.io` domain and its DNS records, and Pages maps the `krcgoktug` hostname to my
public repository. I therefore do not manage a custom CNAME today. If I connect my own
domain later, I will add the record at my DNS provider, verify the domain in GitHub, and
wait for cached old answers to expire. GitHub will still serve the files; DNS will only
change how visitors find them.

The padlock is the next stage, not a DNS feature. Once the name resolves, GitHub Pages
presents a TLS certificate for the hostname. The browser checks that certificate before
sending the HTTPS request. A correct DNS answer can still lead to an HTTPS error if the
certificate does not cover the name, which is why both pieces have to be configured.
