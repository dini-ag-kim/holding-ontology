``` {.ditaa}
        +---------------------+                 +---------------+                 +-----------+
        |      Document       |<---exemplarOf---+               +----foaf:page--->| Document  |
        |     (abstract)      |                 |      Item     |                 | (Website) |
        |                     |-----exemplar--->|               |<---foaf:topic---+           |
        +------------------+--+                 +-------------+-+                 +-----------+
          ^                |                      ^           |
          |                |                      |           |
    foaf:primaryTopic      |              foaf:primaryTopic   |
          |                |                      |           |
          |        foaf:primaryTopicOf            |   foaf:primaryTopicOf
          |                |                      |           |
          |                v                      |           v
        +-+---------------------+             +---+-------------------+
        |      Document         |             |      Document         |
        | (Title Description)   |             | (Holding Description) |
        +-----------------------+             +-----------------------+
```