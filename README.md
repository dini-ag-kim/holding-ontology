holding-ont-dev
===============

development git for holding ontology

# Overview

## Relations between Documents, Items, Places, Services and Agents
``` {.ditaa}
                                              +----------------------------------------collects-----------------------------------------------------+
                                              |               +----------------------------------------------------------------------------------+  |
                                              |               |                                                                                  |  |
                                              |               v                                                +--------------+                  |  |
   +------------------+                   +---+------------------+                                             |              |                  |  |
   |                  +----org_siteOf---->|                      +------------------holds------------+-------->|   Holdings   |                  |  |
   |     Location     |                   |         Agent        |                                   |         | (Collection) |                  |  |
   |                  |<---gr_hasPOS------|      (provider)      |                                   |         |              |                  |  |
   +------------------+                   |                      |<--------heldBy--------------+     |         +------+-------+                  |  |
            ^                             +------------------+---+                             |     |                |                          |  |
            |                                 ^              |                                 |     |             contains                      |  |
            |                                 |       service_provides                         |     |                |                          |  |
            |                                 |              |                                 |     |                |                          |  |
   gr_availableAtorFrom             service_providedBy       |                                 |     |                |                          |  |
            |                                 |              |                                 |     |                |                          |  |
            |                                 |              v         daia_availableFor /     |     v                |                          |  |
            |                            +----+--------------------+  daia_unavailableFor   +--+----------+           |                          |  |
            +----------------------------+                         |<-----------------------+             |<----------+-----------+              |  |
        +--------------------------------+   dso_DocumentService   |                        |     Item    |                       |              |  |
        |                +-------------->|                         +----------------------->|             +------+             exemplar          |  |
        |                |               +----------------+--------+    daia_availableOf /  +-------------+      |             broaderExemplar   |  | 
        |                |                    ^           |    ^        daia_unavailableOf                 exemplarOf          narrowerExemplar  |  |
        |                |                    |           |    |                                           broaderExemplarOf      |              |  |
service_limitedBy   service_limits     service_consumes   |    +--------------------------------------+    narrowerExemplarOf     |              |  |
        |                |                    |           |                   dso_hasService          |          |                |              |  |
        |                |                    |    service_consumedBy                        +--------+------+   |                |              |  |
        v                |                    |           |                                  |               |<--+                |              |  |
   +---------------------+-----+              |           v                                  |    Document   |                    |              |  |
   |                           |           +--+-----------+----+                             |               +--------------------+              |  |
   | service_ServiceLimitation |           |        Agent      |                             +-----------+---+                                   |  |
   |                           |           |     (consumer)    |                                ^        |                                       |  |
   +---------------------------+           +-------------------+                                |        +---------------collectedBy-------------+  |
                                                                                                +---------------------------------------------------+

```
