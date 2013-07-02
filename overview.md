# Overview

## Relation between Item and Item
``` {.ditaa}
                           +-----------+
                   +-------+           +-------+
narrowerExemplar / |       |   Item    |       | broaderExemplar /
narrowerExemplarOf |       |           |       | broaderExemplarOf
                   +------>|           |<------+
                           +-----------+

```

## Relation between Item and Documents
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

## Relation between Item, Agent and Service
``` {.ditaa}
                                          dso:hasService
                                 +----------------------------------+
                                 |                                  |
                                 |        daia:availableFor /       v
+------------+     heldBy   +----+----+   daia:unavailableFor  +---------------------+                   
|            |<-------------+         +----------------------->|                     |
|   Agent    |              |  Item   |                        | dso:DocumentService |
| (Provider) +------------->|         |<-----------------------+                     |
+-----+------+    holds     +---------+   daia:availableOf /   +---------------------+
      |                                   daia:unavailableOf        ^     ^                  
      |                                                             |     |
      |           ssso:provides                                     |     |
      +-------------------------------------------------------------+     |
                                                                          |
                                                                          |
+------------+                                                            |
|  Agent     |    ssso:consumes                                           |
| (Consumer) +------------------------------------------------------------+
+------------+
```

## Other Relations
``` {.ditaa}
                               +--------+
                               |        |  ecpo:hasChronology /   +------------+
+-----------+     gn:locatedIn |        |  ecpo:hasChronologyGap  |            |
| Location  |<-----------------+  Item  +------------------------>| Chronology |
+-----------+                  |        |                         |            |
                               |        |                         +------------+
                               +--------+
```
