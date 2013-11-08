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
    @prefix gr:   <http://purl.org/goodrelations/v1#> .
    @prefix org:  <http://www.w3.org/ns/org#> .
    @prefix owl:  <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix ssso: <http://purl.org/ontology/ssso#> .
    @prefix vann: <http://purl.org/vocab/vann/> .
    @prefix rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
    @prefix skos: <http://www.w3.org/2004/02/skos/core#> .
    @prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

The Holding Ontology is defined in RDF/Turtle as following:

    <> a owl:Ontology ;
        rdfs:label "Holding Ontology"@en ;
        vann:preferredNamespacePrefix "holding" .

# Overview

| Classes<br>(defined by other ontologies) | Properties<br>(defined by this ontology) | Properties<br>(defined by other ontologies)| Individuals |
|:---:|:---:|:---:|:---:|
| [Item]<br>[Agent]<br>[Document]<br>[DocumentService]<br>[Offering]<br>[Location]<br>[Chronology]| [heldBy]<br>[holds]<br>[inCollection]<br>[exemplar]<br>[exemplarOf]<br>[broaderExemplar]<br>[broaderExemplarOf]<br>[narrowerExemplar]<br>[narrowerExemplarOf]<br>[label] | [availableFor]<br>[unavailableFor]<br>[providedBy]<br>[hasChronology]<br>[hasChronologyGap]<br>[availableAtOrFrom]<br>[hasStockKeepingUnit]<br>[siteOf]<br>[name] | [Loan]<br>[Presentation] |

# Core Relationships

The holding Ontology does not define classes on its own but makes usage of classes defined in other Ontologies. See [Informative References] for references to the used onotologies.

## Item

[Item]: #item

An **Item** is a particular copy of a bibliographic resource that is held by an [Agent]. Items are also referred to as holdings, but a holding can include more information about items, such as inventory and access. The Item class is defined by the [FRBR Ontology] without implying the rest of the FRBR model.

    frbr:Item a owl:Class ;
        rdfs:label "Item"@en ;
        rdfs:isDefinedBy <http://purl.org/vocab/frbr/core> .

## Agent

[Agent]: #agent

An **Agent** is a person, organization, group or any other entity that can held items and provide services. The Agent class is defined by the [FOAF Ontology].

    foaf:Agent a owl:Class ;
        rdfs:label "Agent"@en ;
        rdfs:isDefinedBy <http://xmlns.com/foaf/0.1/> .

## heldBy

[heldby]: #heldby

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

Relates an [Agent] with an [Item] which the [Agent] holds.

    holding:holds a owl:ObjectProperty ;
        rdfs:label "holds"@en ;
        rdfs:comment "Relates an Institution to an Item which the Institution holds."@en ;
        rdfs:domain foaf:Agent ;
        rdfs:range frbr:Item ;
        rdfs:subPropertyOf holding:inCollection ;
        owl:inverseOf holding:heldBy .

## inCollection

[inCollection]: #incollection

TODO

## Document

[Document]: #document

A **Document** is a bounded physical representation of body of information designed with the capacity (and usually intent) to communicate. A document may manifest symbolic, diagrammatic or sensory-representational information. Documents may include both abstract works, such as "Romeo and Juliet", and more conrete entities, such as a specific edition of a book.

    bibo:Document a owl:Class ;
        owl:equivalentClass foaf:Document ;
        rdfs:label "Document"@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/bibo/> .

In the context of this ontology when talking about documents several kinds of documents are involved:

* the abstract document
* the document describing the title
* the document describing the holdings
* document as a website 

The reltions between an [Item] and different kinds of document is shown in this diagram:

`item-description-relation.md`{.include}

# Relations between abstract Documents and Items

The [exemplar] relation is used to state that a concrete [Item] is a copy of an abstract [Document]. Additional relations exist for Items that only contain parts of a document and for Items that contain multiple documents (for instance a collection that the document is part of). 

`item-doc-relation.md`{.include}

To give an example:

* Given a book series (a [Document]), a full shelve of books of the series
  (an [Item]) is an [exemplarOf] the series.
* A book of the series (a [Document]) has a copy of the book (an [Item]) 
  as [exemplar].
* The copy (an [Item]) is a
  * a [narrowerExemplarOf] the series (as [Document]), and
  * a [broaderExemplarOf] a single chapter of the book (as [Document]).

## exemplar

[exemplar]: #exemplar

Relates a [Document] to an [Item] that is an exemplar of the [Document]. This property is similar to frbr:exemplar but does not refer to the class frbr:Manifestation.

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

# Relation between Items and Services

`item-offering-relation.md`{.include}

## DocumentService

[DocumentService]: #documentservice

A **DocumentService** is a service that is related to one or more [documents](#document). The service involves a service provider (e.g.
a library) and an optional service consumer (e.g. a library patron). Both service provider and service consumer SHOULD be instances of [Agent]. The DocumentService class is defined by the [Document Service Ontology].

    dso:DocumentService a owl:Class ;
        rdfs:label "DocumentService" ;
        rdfs:isDefinedBy <http://purl.org/ontology/dso> .

## Offering

[Offering]: #offering

In the scope of holding ontology an **Offering** includes a [DocumentService] for an [Item] and optional a [Location] where the service takes place. The class Offering is defined by [GoodRelations].

    gr:Offering a owl:Class ;
        rdfs:label "Offering"@en ;
        rdfs:isDefinedBy <http://purl.org/goodrelations/v1> .

Typical offerings for document services within the scope of holding ontology involve a loan service ([dso:Loan]) and/or a presentation service ([dso:Presentation]) and are included in an offering for that document service.

## Presentation

[Presentation]: #presentation

A **Presentation** is an offering for a document service [dso:Presentation]. Use properties [availableFor] and [unavailableFor] from the [DAIA Ontology] to relate this offer with the [Item].

    holding:Presentation a owl:NamedIndividual ;
        rdf:type gr:Offering ;
        rdfs:label "Presentation"@en ;
        rdfs:comment "offering for a presentation service"@en ; 
        gr:includes [
            a dso:Presentation
        ] .

## Loan

[Loan]: #loan

A **Loan** is an offering for a document service [dso:Loan]. Use properties [availableFor] and [unavailableFor] from the [DAIA Ontology] to relate this offer with the [Item].

    holding:Loan a owl:NamedIndividual ;
        rdf:type gr:Offering ;
        rdfs:label "Loan"@en ;
        rdfs:comment "offering for a loan service"@en ; 
        gr:includes [
            a dso:Loan
        ] .

## Interloan

[Interloan]: #interloan

An **Interloan** is an offering for a document service [dso:Interloan]. Use properties [availableFor] and [unavailableFor] from the [DAIA Ontology] to relate this offer with the [Item].

    holding:Interloan a owl:NamedIndividual ;
        rdf:type gr:Offering ;
        rdfs:label "Interloan"@en ;
        rdfs:comment "offering for a interloan service"@en ; 
        gr:includes [
            a dso:Interloan
        ] .

## Location

[Location]: #location

A **Location** is a point or area of interest from which a particular [Item] or [DocumentService] is available. The property [availableAtorFrom] should be used to indicate the location of an offered [DocumentService] for an [Item]. The Location class is defined by [GoodRelations].

    gr:Location a owl:Class ;
        rdfs:label "Location"@en ;
        rdfs:isDefinedBy <http://purl.org/goodrelations/v1> .

## name

[name]: #name

When a [DocumentService] is offered for an [Item], this property is used to name the location where the [DocumentService] should be provided. The Location class is defined by [GoodRelations].

    gr:name a owl:AnnotationProperty ;
        skos:scopeNote "When a document service is offered for an item, this property is used to name the location where the document service should be provided."@en ;
        rdfs:isDefinedBy <http://purl.org/goodrelations/v1> .
 
## providedBy

[providedBy]: #providedby

Used to relate an [Offering] with an [Agent] who provides the service offered. This property is defined by the the [DAIA Ontology].

    daia:providedBy a owl:AnnotationProperty ;
        skos:scopeNote "Used to relate an offering with an agent who provides the service offered."@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/daia> .

## availableAtOrFrom

[availableAtOrFrom]: #availableatorfrom

This property is used to relate an Offering of a [DocumentService] for an [Item] with a [Location]. See [examples] for usage. This property is defined by [GoodRelations].

    gr:availableAtOrFrom a owl:AnnotationProperty ;
        skos:scopeNote "Used to relate a document service offered for an item with a location."@en ;
        rdfs:isDefinedBy <http://purl.org/goodrelations/v1> .

## hasStockKeepingUnit

[hasStockKeepingUnit]: #hasstockkeepingunit

This property is used as an identifier for the [Item] for which a [DocumentService] is offered. See [examples] for usage. This property is defined by [GoodRelations].

    gr:hasStockKeepingUnit a owl:AnnotationProperty ;
        skos:scopeNote "Used to identify the item for which a document service is offered."@en ;
        rdfs:isDefinedBy <http://purl.org/goodrelations/v1> .

## siteOf

[siteOf]: #siteOf

This property is used to relate a [Location] with an [Agent]. See examples for usage. This property is defined by the [Organization Ontology].

    org:siteOf a owl:AnnotationProperty ;
        skos:scopeNote "This property is used to relate a location with an agent."@en ;
        rdfs:isDefinedBy <http://www.w3.org/ns/org> .

## Chronology

[Chronology]: #chronology

A **Chronology** is the description of enumeration and chronology of a periodical. The Chronology class is defined by the [Enumeration and Chronology of Periodicals Ontology].

    ecpo:Chronology a owl:Class ;
        rdfs:label "Chronology"@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/ecpo> .

To relate an [Item] to a Chronology use [hasChronology] or [hasChronologyGap]. To be more specific on the nature (current or closed) of a Chronology use [CurrentChronology] or [ClosedChronology]. To simply express the fact that an [Item] has a current chronology or a closed chronology without giving further information one MAY use [Current] or [Closed].

## label

[label]: #label

A call number, shelf mark or similar label of an item

    holding:label a owl:DatatypeProperty ;
        rdfs:label "label"@en ;
        rdfs:comment "A call number, shelf mark or similar label of an item"@en ;
        rdfs:domain frbr:Item ;
        rdfs:range rdfs:Literal ;
        rdfs:subPropertyOf dct:identifier .
        

# Examples

[Examples]: #examples

## A book series, fully held by a library

``` {.example}

# The series is a document, consisting of multiple volumes
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

## Offering a Service for an Item

``` {.example}
$alicecopies
    daia:availableFor (
        [
            a holding:Presentation ;
            gr:hasStockKeepingUnit "HB 17 Rg 500" ;
            daia:providedBy <http://ld.zdb-services.de/resource/organisations/DE-1a> ;
            gr:availableAtOrFrom [
                a gr:Location ;
                gr:name "Leesesaal" ;
                org:siteOf <http://ld.zdb-services.de/resource/organisations/DE-1a>
            ]
        ] [
            holding:Loan ;
            gr:hasStockKeepingUnit "Zsn 70488" ;
            daia:providedBy <http://ld.zdb-services.de/resource/organisations/DE-1a> ;
        ]
    ) .
```

# References

## Normative References

...

## Informative References

* ISO 20775
* [Bibliographic Ontology]
* [DAIA Ontology]
* [DCMI Metadata Terms]
* [Document Service Ontology] (DSO)
* [Enumeration and Chronology of Periodicals Ontology] (ECPO).
* [FOAF Ontology]
* [FRBR Ontology]
* [GoodRelations]
* [Organization Ontology]

[Bibliographic Ontology]: http://purl.org/ontology/bibo/
[DAIA Ontology]: http://purl.org/ontology/daia
[DCMI Metadata Terms]: http://dublincore.org/documents/dcmi-terms/
[Document Service Ontology]: http://purl.org/ontology/dso
[Enumeration and Chronology of Periodicals Ontology]: http://purl.org/ontology/ecpo
[FOAF Ontology]: http://xmlns.com/foaf/spec/ 
[FRBR Ontology]: http://purl.org/vocab/frbr/core
[GoodRelations]: http://purl.org/goodrelations/v1
[Organization Ontology]: http://www.w3.org/ns/org
[availableFor]: http://purl.org/ontology/daia/availableFor 
[availableOf]: http://purl.org/ontology/daia/availableOf 
[unavailableFor]: http://purl.org/ontology/daia/unavailableFor 
[unavailableOf]: http://purl.org/ontology/daia/unavailableOf 
[dso:Loan]: http://purl.org/ontology/dso#Loan
[dso:Interloan]: http://purl.org/ontology/dso#Interloan
[dso:Presentation]: http://purl.org/ontology/dso#Presentation
[hasChronology]: http://purl.org/ontology/ecpo#hasChronology
[hasChronologyGap]: http://purl.org/ontology/ecpo#hasChronologyGap
[CurrentChronology]: http://purl.org/ontology/ecpo#CurrentChronology
[ClosedChronology]: http://purl.org/ontology/ecpo#ClosedChronology
[Current]: http://purl.org/ontology/ecpo#Current
[Closed]: http://purl.org/ontology/ecpo#Closed