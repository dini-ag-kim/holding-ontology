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
                                          |      (provider)      +-------------------------------+
   +------------------+                   | +------------------+ |                               |
   |                  +----org:siteOf------>|                  | |                               |
   | geo:SpatialThing |                   | | org:Organization | |                               |
   |                  |<---org:hasSite------+                  | |                             holds
   +------------------+                   | +------------------+ |<--------heldBy----------+     |
            ^                             |                      |                         |     |
            |                             +-----------------+----+                         |     |
            |                                  ^            |                              |     |
            |                                  |            |                              |     |
         ev:place                       ssso:providedBy  ssso:provides                     |     v
            |                                  |            |                           +--+--------+
            |                                  |            v       daia:availableFor / |           |
            |                              +---+-----------------+ daia:unavailableFor  |           |
            +------------------------------+                     |<---------------------+           |
     +-------------------------------------+ dso:DocumentService |<---dso:hasService----+ frbr:Item |
     |              +--------------------->|                     +--------------------->|           |
     |              |                      +---------------------+   daia:availableOf / |           |
     |              |                                ^              daia:unavailableOf  |           |
     |              |                                |                                  +-----------+
ssso:limitedBy   ssso:limits                    ssso:consumes
     |              |                                |
     |              |                                |
     v              |                                |
+-------------------+----+                  +--------+-------+
|                        |                  |    foaf:Agent  |
| ssso:ServiceLimitation |                  |   (consumer)   |
|                        |                  +----------------+
+------------------------+

```
