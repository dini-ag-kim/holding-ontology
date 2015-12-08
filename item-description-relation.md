        +---------------------+                 +---------------+                 +-----------+
        |      Document       |<---exemplarOf---+               +----foaf_page--->| Document  |
        |     (abstract)      |                 |      Item     |                 | (Website) |
        |                     |-----exemplar--->|               |<---foaf_topic---+           |
        +------------------+--+                 +-------------+-+                 +-----------+
          ^                |                      ^           |
          |                |                      |           |
          |foaf_primaryTopic                   foaf_primaryTopicOf
          |                |                      |           |
          |                |                      |           |
          |                |                      |           |
          |                v                      |           v
        +-+---------------------+             +---+-------------------+
        |      Document         |             |      Document         |
        | (Title Description)   |             | (Holding Description) |
        +-----------------------+             +-----------------------+