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

This document describes best pratices for web crawlers.


--- middle

# Introduction

Automatic clients (i.e. crawlers, bots) are used to access web resources, e.g., for indexing
for search but more recently also for new use cases related to Artificial Intelligence (AI)
such as training models. With an increase in crawling activity, it is particular important 
that automatic clients having an expected behavior and respect contraint of the ressources
being crawled. This includes documenting how to identify them and how their behavior
can be influenced. As such, crawler operators are requested
to conform to crawling best pratices in this document.

To further help website owners,
it should in additon be considered to create together a central
website where website owners can look up well behaving crawlers.
Note that while self declared research crawlers, including privacy and malware discovery
crawlers, and contractual crawlers are welcome to add themselves to adopt these practices,
due to the nature of the relationship with sites they may exempt themselves from any of
the Crawler Code of Conduct policies with a rationale.


# Recommended Best Practices

The following best practices are should be followed and are already
applied by a vast majority of large scale crawlers on the Internet:

1. Crawlers must support and respect the Robots Exclusion Protocol.
2. Crawlers must be easily identifiable through their user agent string.
3. Crawlers must not interfere with the normal operation of a site.
4. Crawlers must support caching directives.
5. Crawlers must expose the IP ranges they are crawling from in a standardized format.
6. Crawlers must expose a page where they explain how the crawled data is used and how it can be blocked.


## Crawlers must respect the Robots Exclusion Protocol

Crawlers must support the REP as defined in
[RFC9309](https://www.rfc-editor.org/rfc/rfc9309.html#section-2.2.1) to allow site owners
to opt out from crawling. Further crawler must respect the restrictions provided
by the REP such as crawling delay and rate limits.

Especially if the website does not support REP, crawlers further need to respect the
meta robots tag in the HTTP header.


## Crawlers must be easily identifiable through their user agent string

As stipulated in [RFC9309](https://www.rfc-editor.org/rfc/rfc9309.html#section-2.2.1)
(Robots Exclusion Protocol; REP), the HTTP request header `user-agent` should
identify the crawler clearly, typically by including a URL that hosts the crawler's
description. For example:

`User-Agent: Mozilla/5.0 (compatible; ExampleBot/0.1; +https://www.example.com/bot.html)`.

This is already a widely supported mechanism among crawler operators.
To be compliant, crawler operators must specify identifiers unique for their crawlers
within the case-insensitive user-agent, like "contains 'googlebot' and 'https://url/...'".
Further, the name should be meaningful in identifying the crawler owner and purpose
as much as reasonable possible.


## Crawlers must not interfere with the normal operation of a site

Depending on a site's setup (computing resources, software efficiency) and its size,
crawling may slow down the site or take it offline altogether. Crawler operators must
ensure that their crawlers are equipped with back-out logic that rely on at least the
standard signals defined by
[RFC9110](https://www.rfc-editor.org/rfc/rfc9110#name-server-error-5xx), preferably also
additional heuristics such as relative response time of the server.

As such, crawlers should log already visited URL and how many requests they sent to a resource 
as well as the respective HTTP status codes in the responses,
especially if error occur, to avoid repeatedly crawling the same source.

Generally, crawlers should avoid multiple concurrent requests to the same resources
and use a crawling rate that is no higher than 1 request per second or as specified in
the REP protocol. Further, ressources should not be re-crawled more often than every 24 hours.
Ideally crawlers should limit the crawling depth and number of requests
per ressource to avoid loops.

Crwalers should not attempt to access restricted ressources that requires a login, used CAPTCHAs, or are behind paywalls.

Crawlers should only access content and by all means avoid to modify content by using
HTTP request other than GET such as POST, PUT, DELETE. Similarly crawlers should avoid
assessing Javascript content. 

## Crawlers must support caching directives

[RFC9111](https://www.rfc-editor.org/rfc/rfc9111) HTTP caching, which removes the need
of repeated access from crawlers to the same URI. 


## Crawlers must expose the IP ranges they use for crawling

To complement the REP, crawler operators should expose the IP ranges they allocated for
crawling in a standardized, machine readable format, and keep it reasonably up to date
(i.e. shouldn't get older than 7 days).

The object containing the IP addresses must be linked from the page describing the crawler
and it must be also referenced in the metadata of the page for machine readability.
For example:

```
&lt;link rel="help" href="https://example.com/crawlerips.json" /&gt;
```

## Crawlers must explain how the crawled data is used and the crawler can be blocked

Similar to section
[Crawlers must be easily identifiable through their user agent string]() crawlers should
also document their crawling policies publically and explain how the data they crawled will be used. In
practice this is generally done through the documentation page referenced in the `user-agent` of
the crawler. Further the documentation page should provide a contact address for the crawler owner.

The webpage should also provides an example REP file to block the crawler and a way to verify
REP files.


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
