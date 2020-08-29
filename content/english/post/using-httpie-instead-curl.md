+++
title = "Using httpie instead curl"
date = "2014-07-22"
draft = false
categories = ["SL", "english", "web performance"]
tags = ["english", "curl", "httpie", "SL", "debian"]
+++
![]( /images/httpie.png)

I love [curl][curl]. It's awesome to test many services like HTTP/HTTPS,
FTP, IMAP, etc. But, curl sometimes is hard to use for my customers. So, I
have recommended that they use the [httpie][httpie].

In my main job, I use curl/httpie to see HTTP headers and cache problems. Then,  
when I need to display evidence for my customers, I prefer to use httpie.

A simple example using only HTTP headers.

```
fike@klatoon:~/d$ curl -I https://fernandoike.com
HTTP/1.1 200 OK
Date: Tue, 22 Jul 2014 14:40:56 GMT
Server: Apache/2.2.22
Last-Modified: Thu, 31 May 2012 20:17:19 GMT
ETag: "c57c-b1-4c15ac12cd1c0"
Accept-Ranges: bytes
Content-Length: 177
Vary: Accept-Encoding
Content-Type: text/html

fike@klatoon:~/d$
```


```
fike@klatoon:~/d$ http --headers https://fernandoike.com
HTTP/1.1 200 OK
Accept-Ranges: bytes
Content-Encoding: gzip
Content-Length: 146
Content-Type: text/html
Date: Tue, 22 Jul 2014 14:20:57 GMT
ETag: "c57c-b1-4c15ac12cd1c0"
Last-Modified: Thu, 31 May 2012 20:17:19 GMT
Server: Apache/2.2.22
Vary: Accept-Encoding

fike@klatoon:~/d$
```

Easy and simple, right? But this isn't the most cool feature. The most cool httpie feature is the  STDOUT colorized.

{% img /images/httpie_test.png)

However, curl and httpie have a few differences. The curl option "-I" uses the
HEAD HTTP method and httpie use GET HTTP method. The HEAD HTTP method
can't work in all scenarios because a firewall, IPS or WAF can block this method.

For the curl to haave the same behavior as httpie and use GET HTTP method, it must
use more options:

```
fike@klatoon:~/d$ curl -s -D - https://fernandoike.com -o /dev/null

HTTP/1.1 200 OK
Date: Tue, 22 Jul 2014 15:10:24 GMT
Server: Apache/2.2.22
Last-Modified: Thu, 31 May 2012 20:17:19 GMT
ETag: "c57c-b1-4c15ac12cd1c0"
Accept-Ranges: bytes
Content-Length: 177
Vary: Accept-Encoding
Content-Type: text/html

fike@klatoon:~/d$
```

For add HTTP headers using curl, you have to use "-H" option. For example, to add
HTTP header to disable keep-alive connection.

```
fike@klatoon:~/d$ curl -H "Connection: close" -s -D - https://fernandoike.com -o /dev/null

HTTP/1.1 200 OK
Date: Tue, 22 Jul 2014 15:17:43 GMT
Server: Apache/2.2.22
Last-Modified: Thu, 31 May 2012 20:17:19 GMT
ETag: "c57c-b1-4c15ac12cd1c0"
Accept-Ranges: bytes
Content-Length: 177
Vary: Accept-Encoding
Connection: close
Content-Type: text/html

fike@klatoon:~/d$
```

And with httpie it's simpler...

```
fike@klatoon:~/d$ http --headers https://www.fernandoike.com "Connection: close"

HTTP/1.1 200 OK
Accept-Ranges: bytes
Connection: close
Content-Encoding: gzip
Content-Length: 16424
Content-Type: text/html
Date: Tue, 22 Jul 2014 15:22:58 GMT
ETag: "2010c-d3fb-4fdd68cfc0d40"
Last-Modified: Thu, 10 Jul 2014 13:10:37 GMT
Server: Apache/2.2.22
Vary: Accept-Encoding

fike@klatoon:~/d$
```

Another example:  adding HTTP headers if want identify if a URI is cacheable in a
CDN. This case was tested on a site that uses Akamai.

```
fike@klatoon:~/d$ curl -H "Pragma: akamai-x-cache-on" -s -D - https://www.bestbuy.com -o /dev/null

HTTP/1.1 200 OK
Server: Apache
Content-Length: 4663
Content-Type: text/html
ETag: "7a10c27a970af1daf4b526ed08cd28c0:1343841543"
Expires: Tue, 22 Jul 2014 15:25:00 GMT
Cache-Control: max-age=0, no-cache, no-store
Pragma: no-cache
Date: Tue, 22 Jul 2014 15:25:00 GMT
X-Cache: TCP_MEM_HIT from a201-20-244-37.deploy.akamaitechnologies.com (AkamaiGHost/6.16.2.1-13049459) (-)
Connection: keep-alive

fike@klatoon:~/d$
```

The same test with httpie.

```
fike@klatoon:~/d$ http --headers https://www.bestbuy.com "Pragma: akamai-x-cache-on"

HTTP/1.1 200 OK
Cache-Control: max-age=0, no-cache, no-store
Connection: keep-alive
Content-Encoding: gzip
Content-Length: 1658
Content-Type: text/html
Date: Tue, 22 Jul 2014 15:23:55 GMT
ETag: "7a10c27a970af1daf4b526ed08cd28c0:1343841543"
Expires: Tue, 22 Jul 2014 15:23:55 GMT
Pragma: no-cache
Server: Apache
Vary: Accept-Encoding
X-Cache: TCP_HIT from a201-20-244-37.deploy.akamaitechnologies.com (AkamaiGHost/6.16.2.1-13049459) (-)
```

If you want search about Akamai HTTP headers, go to [Stackoverflow link][stack].

In conclusion, if you need something more friendly, use httpie. But if you need run
more complex tests, curl is the tool.

P.S. Install httpie is simple a Debian like. Debian has official package.

```
#aptitude install httpie
```

[httpie]: https://httpie.org
[curl]: https://curl.haxx.se/
[stack]: https://stackoverflow.com/questions/8811741/whats-the-best-way-to-troubleshoot-akamai-headers-these-days
