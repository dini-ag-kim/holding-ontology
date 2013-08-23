# Introduction

The **Holding Ontology** is a vocabulary to express library holdings in RDF.

## Status of this document

This document is an early draft, created by a DINI AG KIM Working Group. See
<https://wiki.dnb.de/display/DINIAGKIM/Bestandsdaten+Gruppe> for more
resources.

## Namespaces and Ontology

The URI namespace of this ontology is ... The namespace prefix `holding` is recommeded.
The URI of this ontology as a whole is ...

    @prefix holding: <http://example.org/#> .
    @base            <http://example.org/> .

The following namspace prefixes are used to refer to related ontologies:

    @prefix bibo: <http://purl.org/ontology/bibo/> .
    @prefix daia: <http://purl.org/ontology/daia/> .
    @prefix dct:  <http://purl.org/dc/terms/> .
    @prefix dso:  <http://purl.org/ontology/dso#> .
    @prefix ecpo: <http://purl.org/ontology/ecpo#> .
    @prefix foaf: <http://xmlns.com/foaf/0.1/> .
    @prefix frbr: <http://purl.org/vocab/frbr/core#> .
    @prefix owl:  <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix ssso: <http://purl.org/ontology/ssso#> .
    @prefix vann: <http://purl.org/vocab/vann/> .

The Holding Ontology is defined in RDF/Turtle as following:

    <> a owl:Ontology ;
        rdfs:label "Holding Ontology" ;
        vann:preferredNamespacePrefix "holding" .

{OVERVIEW}

...

# Classes

## Agent

[Agent]: #agent

An **Agent** is a person, organization, group or any other entity that can held items and provide services. The agent class is defined by the [FOAF Ontology].

    foaf:Agent a owl:Class ;
        rdfs:label "agent" ;
        rdfs:isDefinedBy <http://xmlns.com/foaf/0.1/> .

## Item

[Item]: #item

An **item** is a particular copy of a bibliographic resource that is held by an [Agent]. Items are also referred to as holdings, but a holding can include more information about items, such as inventory and access.

	holding:Item a a owl:Class ;
		rdfs:label "item"@en ;
		rdfs:isDefinedBy <>;

## Document

[Document]: #document

...

## DocumentService

[DocumentService]: #documentservice

A **DocumentService** is a service event that is related to one or more [documents](#document). The service event involves a service provider (e.g.
a library) and an optional service consumer (e.g. a library patron). Both service provider and service consumer SHOULD be instances of [foaf:Agent](#Agent). The DocumentService class is defined by the [Document Service Ontology].

    dso:DocumentService a owl:Class ;
        rdfs:label "DocumentService" ;
        rdfs:isDefinedBy <http://purl.org/ontology/dso> .

Typical document services within the scope of holdings ontology involve a loan event ([dso:Loan]) and a presentation event ([dso:Presentation]). To express the availability of items for selected services, one SHOULD use the properties [daia:availableFor] and [daia:unavailableFor] from the [DAIA Ontology].

[daia:availableFor]: http://purl.org/ontology/daia/availableFor 
[daia:availableOf]: http://purl.org/ontology/daia/availableOf 
[daia:unavailableFor]: http://purl.org/ontology/daia/unavailableFor 
[daia:unavailableOf]: http://purl.org/ontology/daia/unavailableOf 

[dso:Loan]: http://purl.org/ontology/dso#Loan
[dso:Presentation]: http://purl.org/ontology/dso#Presentation

## Chronology

[Chronology]: #chronology

A [Chronology] is the description of enumeration and chronology of a periodical. The Chronology class is defined by the [Enumeration and Chronology of Periodicals Ontology].

    ecpo:Chronology a owl:Class ;
        rdfs:label "Chronology" ;
        rdfs:isDefinedBy <http://purl.org/ontology/ecpo> .

To relate an [Item] to a [Chronology] use [ecpo:hasChronology] or [ecpo:hasChronologyGap]. To be more specific on the nature (current or closed) of a [Chronology] use [ecpo:CurrentChronology] or [ecpo:ClosedChronology]. To simply express the fact that an [Item] has a current chronology or a closed chronology without giving further information one MAY use [ecpo:Current] or [ecpo:Closed].

[ecpo:hasChronology]: http://purl.org/ontology/ecpo#hasChronology
[ecpo:hasChronologyGap]: http://purl.org/ontology/ecpo#hasChronologyGap
[ecpo:CurrentChronology]: http://purl.org/ontology/ecpo#CurrentChronology
[ecpo:ClosedChronology]: http://purl.org/ontology/ecpo#ClosedChronology
[ecpo:Current]: http://purl.org/ontology/ecpo#Current
[ecpo:Closed]: http://purl.org/ontology/ecpo#Closed

## Location

[Location]: #location

# Relations between Documents and Items

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

## narrowerExemplar

[narrowerExemplar]: #narrowerexemplar

Relates an Item to a Document which is partly exemplified by the Item.

    holding:narrowerExemplar a owl:ObjectProperty ;
        rdfs:label "narrower exemplar"@en ;
        rdfs:comment "Relates an Item to a Document which is partly exemplified by the Item."@en ;
        rdfs:domain frbr:Item ;
        rdfs:range bibo:Document ;
        owl:inverseOf holding:narrowerExemplarOf .

## narrowerExemplarOf

[narrowerExemplarOf]: #narrowerexemplarof

Relates a Document to an Item that is an exemplar of a part of the Document.

    holding:narrowerExemplarOf a owl:ObjectProperty ;
        rdfs:label "narrower exemplar of"@en ;
        rdfs:comment "Relates a Document to an Item that is an exemplar of a part of the Document."@en ;
        rdfs:domain bibo:Document ;
        rdfs:range frbr:Item ;
        owl:inverseOf holding:narrowerExemplar .

## broaderExemplar

[broaderExemplar]: #broaderexemplar

Relates a Document to an Item that contains an exemplar of the Document as part.

    holding:broaderExemplar a owl:ObjectProperty ;
        rdfs:label "broader exemplar"@en ;
        rdfs:comment "Relates a Document to an Item that contains an exemplar of the Document as part."@en ;
        rdfs:domain bibo:Document ;
        rdfs:range frbr:Item ;
        owl:inverseOf holding:broaderExemplarOf .
    

## broaderExemplarOf

[broaderExemplarOf]: #broaderexemplarof

Relates an Item to a Document which is partly exemplified by the Item.

    holding:broaderExemplarOf a owl:ObjectProperty ;
        rdfs:label "broader exemplar of"@en ;
        rdfs:comment "Relates an Item to a Document which is partly exemplified by the Item."@en ;
        rdfs:domain frbr:Item ;
        rdfs:range bibo:Document ;
        owl:inverseOf holding:broaderExemplar .

## exemplar

[exemplar]: #exemplar

Relates a Document to an Item that is an exemplar of the Document. This property is similar to frbr:exemplar but does not refer to the class frbr:Manifestation.

An exemplar should include all parts of a document but there may be gaps and
omissions. If an exemplar only includes parts of a documents that can be
identfied as other documents, one should better use property [narrowerExemplar].

    holding:exemplar a owl:ObjectProperty ;
        rdfs:label "has exemplar"@en ;
        rdfs:comment "Relates a Document to an Item that is an exemplar of the Document. This property is similar to frbr:exemplar but does not refer to the class frbr:Manifestation."@en ;
        rdfs:domain bibo:Document ;        
        rdfs:range frbr:Item ;
        owl:inverseOf holding:exemplarOf .

## exemplarOf

[exemplarOf]: #exemplarof

Relates an Item to the Document that is exemplified by the Item.

    holding:exemplarOf a owl:ObjectProperty ;
        rdfs:label "is examplar of"@en ;
        rdfs:comment "Relates an Item to the Document that is exemplified by the Item."@en ;
        rdfs:domain frbr:Item ;
        rdfs:range bibo:Document ;
        owl:inverseOf holding:exemplar .

# Relations between items, agents, and locations

## heldBy

[heldBy]: #heldby

Relates an Item to an Institution that holds the Item.

    holding:heldBy a owl:ObjectProperty ;
        rdfs:label "held by"@en ;
        rdfs:comment "Relates an Item to an Institution that holds the Item."@en ;
        rdfs:domain frbr:Item ;
        rdfs:range foaf:Organization ;
        owl:inverseOf holding:holds ;
        rdfs:subPropertyOf holding:collectedBy .    

## holds

[holds]: #holds

Relates an Institution to an Item which the Institution holds.

    holding:holds a owl:ObjectProperty ;
        rdfs:label "holds"@en ;
        rdfs:comment "Relates an Institution to an Item which the Institution holds."@en ;
        rdfs:domain foaf:Organization ;
        rdfs:range frbr:Item ;
        rdfs:subPropertyOf holding:inCollection ;
        owl:inverseOf holding:heldBy .

## label

[label]: #label

A call number, shelf mark or similar label of an item

	holding:label a owl:DatatypeProperty ;
		rdfs:label "label"@en ;
		rdfs:comment "A call number, shelf mark or similar label of an item"@en ;
		rdfs:domain holding:Item ;
		rdfs:range rdfs:Literal ;
		rdfs:subPropertyOf dct:identifier .
		

# Examples

## A book series, fully held by a library

``` {.example}

# The series is a document, consisting of multliple volumes
$series a bibo:Periodical 
    dcterms:hasPart $volume1, $volume2, $volume3 .

$volume1 a bibo:Book ; bibo:volume "1" .
$volume2 a bibo:Book ; bibo:volume "2" .
$volume3 a bibo:Book ; bibo:volume "3" .

# One chapter in Volume 1
$chapter3 a bibo:Document ;
    dcterms:isPartOf $volume1 .

# A copy of the full series
$librarycopies 
    holding:exemplarOf $series ;
    holding:heldBy $libray ;
    ecpo:hasChronology [
        a ecpo:CurrentChronology ;
        ecpo:hasBeginVolumeNumbering "1"        
    ] .

# A particular copy of volume 1, located in the library
$librarycopyofvolume1
    holding:exemplarOf $volume1 ;
    holding:narrowerExemplarOf $series ;
    holding:broaderExemplaOf $chapter3 .
```

## The same series, partially held by Alice

``` {.example}
# A copy of volume 1 and 2
$alicecopies 
    holding:exemplarOf $series ;  
        # alteratively: holdings:narrowerExemplarOf $series
    dcterms:hasPart $volume2, $volume3
    holding:heldBy $alice ;
    ecpo:hasChronology [
        a ecpo:CurrentChronology ;
        ecpo:hasBeginVolumeNumbering "1" ;
        ecpo:hasEndVolumeNumbering "2" 
    ] .

# Alice`s copies of volume 1
$alicescopyofvolume1
    holding:exemplarOf $volume1 ;
    holding:narrowerExemplarOf $series ;
    holding:narrowerExemplarOf $alicescopies .

```

# References

## Normative References

...

## Informative References

* ISO 20775
* [Enumeration and Chronology of Periodicals Ontology] (ECPO).
* ...

[FOAF Ontology]: http://xmlns.com/foaf/spec/ 
[Document Service Ontology]: http://purl.org/ontology/dso
[DAIA Ontology]: http://purl.org/ontology/daia
[Enumeration and Chronology of Periodicals Ontology]: http://purl.org/ontology/ecpo


