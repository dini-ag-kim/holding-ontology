# Overview

## Examplar Relations between Documents and Items

``` {.ditaa}

     +--------+      exemplar      +------------+
     |  Item  |<-------------------|  Document  |
     |        |------------------->|            |
     +--------+     exemplarOf     +------------+
        | ^                                  |
        | |                                  |
        | |       broaderExemplar            |
        | +-----------------------------+    | dct:hasPart
        +-----------------------------+ |    |
                 broaderExemplarOf    | |    | 
                                      | |    |
                                      v |    v
     +--------+      exemplar      +------------+
     |  Item  |<-------------------|  Document  |
     |        |------------------->|            |
     +--------+     exemplarOf     +------------+
                                      | ^    |
                                      | |    |
                 narrowerExemplar     | |    | 
        +-----------------------------+ |    | dct:hasPart
        | ------------------------------+    |
        | |     narrowerExemplarOf           | 
        | |                                  |
        v |                                  v
     +--------+      exemplar      +------------+
     |  Item  |<-------------------|  Document  |
     |        |------------------->|            |
     +--------+     exemplarOf     +------------+

```

To give an example:

* Given a book series (a `Document`), a full shelve of books of the series
  (an `Item`) is an `exemplarOf` the series.
* A book of the series (a `Document`) has a copy of the book (an `Item`) 
  as `exemplar`.
* The copy (an `Item`) is a
  * a `narrowerExemplarOf` the series (as `Document`), and
  * a `broaderExemplarOf` a single chapter of the book (as `Document`).

## Relations between Items and descriptions

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
                               |        |  ecpo:hasChronology /   +-----------------+
+-----------+     gn:locatedIn |        |  ecpo:hasChronologyGap  |                 |
| Location  |<-----------------+  Item  +------------------------>| ecpo:Chronology |
+-----------+                  |        |                         |                 |
                               |        |                         +-----------------+
                               +--------+
```
