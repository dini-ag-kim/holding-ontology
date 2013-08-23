# Overview

## Relations between Items and Descriptions

``` {.ditaa}
+---------------------+    exemplarOf   +-------+    foaf:page    +-----------+
|      Document       |<----------------+       +---------------->| Document  |
| (Title Description) |                 | Item  |                 | (Website) |
|                     |---------------->|       |<----------------+           |
+---------------------+     exemplar    +-------+    foaf:topic   +-----------+
                                            ^
                                            |
                                    foaf:primaryTopic /
                                    foaf:primaryTopicOf
                                            |
                                            v
                                 +-----------------------+
                                 |      Document         |
                                 | (Holding Description) |
                                 +-----------------------+
```

## Relations between Items, Places, Services and Agents
``` {.ditaa}
                                          +----------------------+
                                          |      foaf:Agent      |
                                          |      (provider)      +-----------------------------------+
   +------------------+                   | +------------------+ |                                   |
   |                  +----org:siteOf------>|                  | |                                   |
   |   gr:Location    |                   | | org:Organization | |                                   |
   |                  |<---gr:hasPOS------| |                  | |                                 holds
   +------------------+                   | +------------------+ |<--------heldBy--------------+     |
            ^                             |                      |                             |     |
            |                             +-----------+----------+                             |     |
            |                                         |                                        |     |
            |                                     gr:offers                                    |     |
            |                                      gr:seeks                                    |     |
   gr:availableAtorFrom                               |                                        |     |
            |                                         v                                        |     |
            |                            +-------------------------+                           |     v
            |                            |                         |                        +--+--------+
            |                            |        Offering         |   daia:availableFor /  |           |
            |                            | +---------------------+ |  daia:unavailableFor   |           |
            +----------------------------| |                     | |<-----------------------+           |
     +-------------------------------------+ dso:DocumentService |<-------dso:hasService----+ frbr:Item |
     |              +--------------------->|                     +------------------------->|           |
     |              |                    | +---------------------+ |    daia:availableOf /  |           |
     |              |                    |     ^                   |   daia:unavailableOf   |           |
     |              |                    +-----|-------------------+                        +-----------+
ssso:limitedBy   ssso:limits                   |           ^
     |              |                     ssso:consumes    |
     |              |                          |        gr:seeks
     v              |                          |           |
+-------------------+----+                  +--+-----------+----+
|                        |                  |     foaf:Agent    |
| ssso:ServiceLimitation |                  |     consumer)     |
|                        |                  +-------------------+
+------------------------+

```
