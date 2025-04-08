---
title: "Crawler best practices"
abbrev: "cbcp"
category: info

docname: draft-illyes-cbcp-latest
submissiontype: independent
number:
date:
v: 3
# area: AREA
# workgroup: WG Working Group
keyword:
 - next generation
 - unicorn
 - sparkling distributed ledger

author:
 -
    fullname: Gary Illyes
    organization: Independent
    email: synack@garyillyes.com

normative:

informative:


--- abstract

TODO Abstract


--- middle

# Introduction

TODO Introduction

Having an expected behavior of utomatic clients (i.e. crawlers, bots), how their behavior
can be influenced, and how to identify them and opt out of their crawling processes is 
helpful for all parties involved. To help website owners, we propose inviting other 
crawler operators to conform to similar crawling policies, and create together a central 
website where website owners can look up well behaving crawlers. 

Note that while self declared research crawlers, including privacy and malware discovery 
crawlers, and contractual crawlers are welcome to add themselves to adopt these practices,
due to the nature of the relationship with sites they may exempt themselves from any of
the Crawler Code of Conduct policies with a rationale. 


# Good Practices

The following practices are employed by the vast majority of large scale crawlers on the
internet:

[TOC]

1. Crawlers must be easily identifiable through their user agent string.
2. Crawlers must support the Robots Exclusion Protocol.
3. Crawlers must not interfere with the normal operation of a site.
4. Crawlers must expose the IP ranges they're crawling from in a standardized format.
5. Crawlers must expose a page where they explain how the crawled data is used.


## Crawlers must support the Robots Exclusion Protocol

All well behaved crawlers must support the REP as defined in 
[RFC9309](https://www.rfc-editor.org/rfc/rfc9309.html#section-2.2.1) to allow site owners 
to opt out from crawling. 


## Crawlers must be easily identifiable through their user agent string

As stipulated in [RFC9309](https://www.rfc-editor.org/rfc/rfc9309.html#section-2.2.1)
(Robots Exclusion Protocol; REP), the HTTP request header `user-agent` should 
identify the crawler clearly, typically by including a URL that hosts the crawler's 
description. For example 
`User-Agent: Mozilla/5.0 (compatible; ExampleBot/0.1; +https://www.example.com/bot.html)`.
This is already a widely supported mechanism among crawler operators. 

To be compliant, crawler operators must specify identifiers unique for their crawlers 
within the case-insensitive user-agent, like "contains 'googlebot' and 'https://url/...'".


## Crawlers must not interfere with the normal operation of a site

Depending on a site's setup (computing resources, software efficiency) and its size, 
crawling may slow down the site or take it offline altogether. Crawler operators must 
ensure that their crawlers are equipped with back-out logic that rely on at least the 
standard signals defined by 
[RFC9110](https://www.rfc-editor.org/rfc/rfc9110#name-server-error-5xx), preferably also 
additional heuristics such as relative response time of the server.


## Crawlers must expose the IP ranges they use for crawling

To complement the REP, crawler operators should expose the IP ranges they allocated for
crawling in a standardized, machine readable format, and keep it reasonably up to date
(i.e. shouldn't get older than 7 days). 

The object containing the IP addresses must be linked from the page describing the crawler
and it must be also referenced in the metadata of the page for machine readability.
For example:


```
<link rel="help" href="https://example.com/crawlerips.json" />
```

## Crawlers must explain how the crawled data is used

Similar to section 
[Crawlers must be easily identifiable through their user agent string]() crawlers should 
explain how the data they crawled will be used. In 
practice this is generally done through the documentation page referenced in the `user-agent` of
the crawler. 


# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
