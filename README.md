# osay

A way to wrangle mobile telemetry

There's lots of articles telling developers they're doing telemetry wrong. While that may or may not
be true for a given project, you need a way to wrangle things in the meantime without tying code
firmly to a vendor platform.

Why not use the power of all these connected computers to make smart decisions about telemetry as
the data is emitted?

Highlights
----------

* Simple api, easy connections to existing and new systems
* On-device decisions
* Hot code deploy

Architecture
------------

Events
: things that happen
Contexts
: common data about the sender or session that one or more events may be associated with. Contexts
can be attached to the all events or to only events in a specific channel.
Channels
: places events flow to
Deciders
: what should be done with events

1. Events flow into channels -- generally one event type per channel.
2. Current context data is attached upon emission.
3. Channels are a stream of events with logic (deciders) attached to them.
4. Deciders can store, aggregate, and forward events. They can also be contacted later to trigger
   different outcomes or to update their logic.

Reasoning
---------

A typical telemetry flow is something like:

```
something happens -> emit event -> enrich and convert to target format -> batch -> send
```

No matter how events are defined (data class or dictionary/map), as a process of
converting to the target format, events are often split to key-value pairs and pushed into JSON and
similar formats. Osay events are fundamentally themselves key-value pairs so they can be easily
integrated into this flow. The intention is to provide a way to do this consistently across all
events, and also provide a place for on-device thinking to occur.



