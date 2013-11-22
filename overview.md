# Overview

## Relations between Items, Places, Services and Agents
``` {.ditaa}

   +------------------+                   +----------------------+
   |                  +----org:siteOf---->|                      +-----------------------------------+
   |   gr:Location    |                   |       foaf:Agent     |                                   |
   |                  |<---gr:hasPOS------|      (provider)      |                                 holds
   +------------------+                   |                      |<--------heldBy--------------+     |
            ^                             |                      |                             |     |
            |                             +-----------+----------+                             |     |
            |                                         |                                        |     |
            |                                  service:provides                                |     |
            |                                         |                                        |     |
   gr:availableAtorFrom                               |                                        |     |
            |                                         v                                        |     |
            |                            +-------------------------+                           |     v
            |                            |                         |                        +--+--------+
            |                            |                         |   daia:availableFor /  |           |
            |                            |                         |  daia:unavailableFor   |           |
            +----------------------------+                         |<-----------------------+           |
        +--------------------------------+   dso:DocumentService   |<-----dso:hasService----+ frbr:Item |
        |              +---------------->|                         +----------------------->|           |
        |              |                 |                         |    daia:availableOf /  |           |
        |              |                 |                         |   daia:unavailableOf   |           |
        |              |                 +-------------------------+                        +-----------+
   ssso:limitedBy   ssso:limits                ^           ^
        |              |                       |           |
        |              |                service:consumes   |
        v              |                       |        gr:seeks
   +-------------------+----+                  |           |
   |                        |               +--+-----------+----+
   | ssso:ServiceLimitation |               |     foaf:Agent    |
   |                        |               |     (consumer)    |
   +------------------------+               +-------------------+
```
