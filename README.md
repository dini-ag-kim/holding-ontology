holding-ont-dev
===============

development git for holding ontology

# Overview

## Relations between Documents, Items, Places, Services and Agents
``` {.ditaa}
   +------------------+                   +----------------------+
   |                  +----org:siteOf---->|                      +-----------------------------------+
   |     Location     |                   |         Agent        |                                   |
   |                  |<---gr:hasPOS------|      (provider)      |                                 holds
   +------------------+                   |                      |<--------heldBy--------------+     |
            ^                             +------------------+---+                             |     |
            |                                 ^              |                                 |     |
            |                                 |       service:provides                         |     |
            |                                 |              |                                 |     |
   gr:availableAtorFrom             service:providedBy       |                                 |     |
            |                                 |              |          dso:hasService /       |     |
            |                                 |              v         daia:availableFor /     |     v
            |                            +----+--------------------+  daia:unavailableFor   +--+----------+
            +----------------------------+                         |<-----------------------+             |<----------------------+
        +--------------------------------+         Service         |                        |     Item    |                       |
        |                +-------------->|                         +----------------------->|             +------+             exemplar
        |                |               +----------------+--------+    daia:availableOf /  +-------------+      |            broaderExemplar
        |                |                    ^           |             daia:unavailableOf /                 exemplarOf       narrowerExemplar
        |                |                    |           |             dso:hasDocument                     broaderExemplarOf     |
   service:limitedBy service:limits    service:consumes   |                                                narrowerExemplarOf     |
        |                |                    |           |                                  +---------------+   |                |
        |                |                    |  service:consumedBy                          |               |<--+                |
        v                |                    |           |                                  |    Document   |                    |
   +---------------------+-----+              |           v                                  |               +--------------------+
   |                           |           +--+-----------+----+                             +---------------+
   |     ServiceLimitation     |           |        Agent      |
   |                           |           |     (consumer)    |
   +---------------------------+           +-------------------+
```
