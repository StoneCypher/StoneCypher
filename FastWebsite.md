# On "fast" websites

Developers often focus on a single major topic

This document discusses John's belief on how best to approach these to afford a web application that customers are left
noticing performance differences in, by contrast to their other apps.



## Hedging

This document is to be understood as a document of opinion.  If something isn't directly cited, please understand it to
be something John believes.  The document will be written in tone of fact, because if everything in here is manually
hedged "I believe" or whatever, the document will triple in length and become unreadable.  ***Please allow this
paragraph to serve as proxy humility for the entire document; thanks***.

To that end, please also understand that I openly invite suggestions, recommendations, and rewrites.  Please submit them
on Github if you know how, in the hope of keeping things simple.



# Stance overview

There are essentially five major topics in website speed.

1. Local speed
1. Server speed
1. Network speed
1. Delivery speed
1. Perceived speed




# TL;DR

We need to make the site feel fast.  Local issues, like the JavaScript making poor algorithmic choices, can cause individual actions to feel slow.  Binding those actions to a webserver in the background is guaranteed to feel slow; putting it in the background with AJAX and third-state controls can ameliorate that.  The initial load should be fast, probably from CDN with a static pre-build if that's plausible.  Making sure delivery is fast is paramount.  Many small tricks, such as using animations to make lag feel like a design choice, can make big shifts.

The big wins will come from dispatching an entire site in a single load, then having all other loads after that be API hits and virtual page switches.  With a careful eye, this can render websites which verge on native apps for performance, without requiring extensive aggresive architectural changes like COMET.




## Justification

Retention.  Quality of user experience.  Perceived better-than wrt competition.  Factored into Panda.  Etc.



# Definitions, and cause for ranking

First let's go over what we're talking about,


## Local speed

Local



# Server speed
