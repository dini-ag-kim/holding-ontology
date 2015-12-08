   +------------------+                   +----------------------+
   |                  +----org_siteOf---->|                      +-----------------------------------+
   |     Location     |                   |         Agent        |                                   |
   |                  |<---gr_hasPOS------|      (provider)      |                                 holds
   +------------------+                   |                      |<--------heldBy--------------+     |
            ^                             +------------------+---+                             |     |
            |                                 ^              |                                 |     |
            |                                 |       service_provides                         |     |
            |                                 |              |                                 |     |
   gr_availableAtorFrom             service_providedBy       |                                 |     |
            |                                 |              |                                 |     |
            |                                 |              v         daia_availableFor /     |     v
            |                            +----+--------------------+  daia_unavailableFor   +--+----------+
            +----------------------------+                         |<-----------------------+             |<----------------------+
        +--------------------------------+   dso_DocumentService   |                        |     Item    |                       |
        |                +-------------->|                         +----------------------->|             +------+             exemplar
        |                |               +----------------+--------+    daia_availableOf /  +-------------+      |             broaderExemplar
        |                |                    ^           |    ^        daia_unavailableOf                 exemplarOf          narrowerExemplar
        |                |                    |           |    |                                           broaderExemplarOf      |
service_limitedBy    service_limits    service_consumes   |    +--------------------------------------+    narrowerExemplarOf     |
        |                |                    |           |                   dso_hasService          |          |                |
        |                |                    |  service_consumedBy                          +--------+------+   |                |
        v                |                    |           |                                  |    Document   |<--+                |
   +---------------------+-----+              |           v                                  |               |                    |
   |                           |           +--+-----------+----+                             |               +--------------------+
   | service_ServiceLimitation |           |        Agent      |                             +---------------+
   |                           |           |     (consumer)    |
   +---------------------------+           +-------------------+