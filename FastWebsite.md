
## How to get a fast website

The general categories:

  1. UX considerations.
  1. Technical steps.
  1. Stage magic.

UX considerations are topics like "how do I build my app's UI to feel fast."  Regardless of all the technical magic
in the world, if you make someone fill out a form one field at a time, and press a button for a full page swap
inbetween, then the site will "feel slow."  Oftentimes the biggest wins can be had with no technical adjustment at all,
by slightly tweaking the things we choose to build.

Technical steps are the meat of this document, though not the exclusive important part.  Primarily this is because it's
relatively straightforward to be specific and direct about a technical choice: 'do it like this,' as opposed to the UX
style of "try to avoid this circumstance" discussion.

Stage magic is the spit polish of the fast site world.  It is less necessary than the others, but seals the deal, so to
speak, on an application which feels "natively fast;" it can be used to pave over those handful of delays which can't
be hidden in other ways, with the notable exception of the initial load.  By stage magic, we refer to misdirection -
things such as animations, fades, and other frequently graphic behaviors that are meant to make time fills look like
artistic choices rather than unavoidable delays.

So.

Let's get specific.





### UX considerations

  1. An app that takes fewer steps to accomplish a goal feels faster before almost any other consideration.
    1. Remove steps from tasks.  Collate fields in a page, or remove them entirely.
    1. Compare JIRA to almost any other tracker.  Even when their servers are faster, their app seems slow, because
       all those actions' two-second delays add up.
    1. Delays with thought inbetween distract from original intent; break flow; cause forgetfulness and frustration.
    1. Ability to see live changes immediately, ideally without page replacements, yields the highest seeming of speed.
    1. Users tend to remember the single slowest piece.
      1. An app that runs reliably in 0.5 second will seem faster than an app which usually takes 0.1 second, but on
         occasion takes 3 seconds, even if on average it is far faster.
    1. It is usually enough to just let a user know something has begun.
      1. In many cases, it's enough to bring up a  spinner, change a background or font color, or switch back to a
         different view to let the user know something has happened.
      1. This implies preventing them from leaving the webpage until the action is legitimately completed (send
         a reply on gmail or facebook on a slow network then immediately try to clo)

  1. Make the front-side UI "feel fast"
    1. Get the browser to do its work efficiently
    1. Fight flashes of content like they're your mortal enemy
      1. This is really, really hard with fonts `:(`
        1. Minimize the use of novel font faces, even though they're amazingly impactful
        1. A handful of novel faces goes a long way
        1. Check your null hypothesis; don't remove fonts to remove them.  Sometimes the alternative is worse, eg images
           vs icon fonts
      1. Load-time flashes of content (which is, admittedly, most of them) are sometimes, not often, the right choice
      1. The weight of the choice is on whether waiting for the content to load before the initial show is worse
        1. Sometimes it's worse
      1. Sometimes fighting a flash of content just means having a better introduction of content
        1. Fade-in, animation, zoom, slide-in, etc each resolve the flash of content effect
    1. Fight browser, reaction, animation, and response lag at every level
      1. Sometimes this is subtle (some versions of Android browser introduce a click delay to wait for doubleclick, eg)





### Technical steps

  1. Do everything client-side where possible
    1. In modern dev this turns out to be nearly everywhere
    1. Route your page at the /client/ side; never reload

  1. Reduce the weight of the initial load
    1. Deliver assets from CDNs unless you want to compete with /that/ (pro tip: you don't)
    1. Bundled assets
      1. There are two bundles per tech: stuff you can't start without and stuff you can
      1. Most (sometimes all) JS goes in the first bucket
      1. Almost all CSS (retain enough to show the iso boot page) and basically all images go in the second
      1. Bundling usually obviates things like multiplexing subdomains, but other stuff exists for exotic situations
    1. Single up-front global load, no fractional load bullshit
    1. All images have pre-load dimensions to prevent layout thrash
    1. All fonts have sensible fallbacks
    1. Holy god get your caching and etags right
    1. Use HTTP2 (or SPDY or websockets or WebRTC or whatever) to reduce protocol impact

  1. Reduce the impact of the initial load
    1. Deliver an isomorphic materialized initial state
      1. THIS DOES NOT HAVE TO BE A CUSTOM ISOMORPHIC STATE
      1. Look at Facebook for an example.
        1. Facebook ships a static wall with placeholders, then fill it in with an AJAX
           call.
        1. This is the correct approach: prematerialized isomorphics allow dispatch without assembly, which is
           speed-critical, and is an enabler for better isomorphic experiences.
    1. This iso state *should* *not* wait for other resources, eg that enormous js bundle, to be visible
      1. That is, at a /minimum/, there should be a "now loading" screen - and there can probably be better
    1. Exception: don't change the behavior of anchors.  Instead mute them visually and make them not-work until
       the relevant scripts are loaded.
    1. In most cases if you have a choice between pre-generating and generating live, and it isn't about reducing
       what you send over the wire, generating live is usually faster than the network cost of pre-generation these days
       1. Yes, even on shitty phones

  1. Reduce the impact of hitting the server
    1. Hit the server as rarely as possible
    1. API calls that are batchable are glorious
    1. Comet and/or websockets?
    1. Minimize API lag
      1. API should not helpfully provide extra data because slow
      1. Consider whether you need API geo-distribution
        1. This can in turn come with extreme costs, like WAN db split brain, sync lag, and forcing business sharding

  1. Reduce the impact of an AJAX call
    1. Very few AJAX calls should block the UI
    1. In many cases a third-state (eg a loading spinner) is all you actually need





### Stage Magic
