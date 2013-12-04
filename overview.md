# Overview

## Relations between Documents, Items, Places, Services and Agents
``` {.ditaa}

   +------------------+                   +----------------------+
   |                  +----org:siteOf---->|                      +-----------------------------------+
   |   gr:Location    |                   |       foaf:Agent     |                                   |
   |                  |<---gr:hasPOS------|      (provider)      |                                 holds
   +------------------+                   |                      |<--------heldBy--------------+     |
            ^                             +------------------+---+                             |     |
            |                                 ^              |                                 |     |
            |                                 |       service:provides                         |     |
            |                                 |              |                                 |     |
   gr:availableAtorFrom             service:providedBy       |                                 |     |
            |                                 |              |                                 |     |
            |                                 |              v         daia:availableFor /     |     v
            |                            +----+--------------------+  daia:unavailableFor   +--+----------+
            +----------------------------+                         |<-----------------------+             |<----------------------+
        +--------------------------------+   dso:DocumentService   |                        |  frbr:Item  |                       |
        |                +-------------->|                         +----------------------->|             +------+             exemplar
        |                |               +----------------+--------+    daia:availableOf /  +-------------+      |            broaderExemplar
        |                |                    ^           |    ^        daia:unavailableOf                   exemplarOf       narrowerExemplar
        |                |                    |           |    |                                            broaderExemplarOf     |
   service:limitedBy service:limits    service:consumes   |    +---------dso:hasService---------------+    narrowerExemplarOf     |
        |                |                    |           |                                  +--------+------+   |                |
        |                |                    |  service:consumedBy                          |               |<--+                |
        v                |                    |           |                                  | bibo:Document |                    |
   +---------------------+-----+              |           v                                  |               +--------------------+
   |                           |           +--+-----------+----+                             +---------------+
   | service:ServiceLimitation |           |     foaf:Agent    |
   |                           |           |     (consumer)    |
   +---------------------------+           +-------------------+
```
