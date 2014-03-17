# Introduction

The **Holding Ontology** is a vocabulary to express (library) holdings in RDF.

This ontology deals with items and their relations to agents, documents and services. An item is a copy or exemplar of a document. Items are also referred to as holdings, but a holding is moreover the description of an agents inventory and access information for the item. Although this ontology derives the Item class from the FRBR Ontology, it does not imply the use of the FRBR model.

## Status of this document

This document is an early draft, created by a DINI AG KIM Working Group. See
<https://wiki.dnb.de/display/DINIAGKIM/Bestandsdaten+Gruppe> for more
resources.

## Namespaces and Ontology

The URI namespace of this ontology is `http://purl.org/ontology/holding#`. The
namespace prefix `holding` is recommeded.  The URI of this ontology as a whole
is <http://purl.org/ontology/holding>.

    @prefix holding: <http://purl.org/ontology/holding#> .
    @base            <http://purl.org/ontology/holding> .

The following namspace prefixes are used to refer to related ontologies:

    @prefix bf:      <http://bibframe.org/vocab/> .
    @prefix bibo:    <http://purl.org/ontology/bibo/> .
    @prefix cc:      <http://creativecommons.org/ns#> .
    @prefix daia:    <http://purl.org/ontology/daia/> .
    @prefix dct:     <http://purl.org/dc/terms/> .
    @prefix dso:     <http://purl.org/ontology/dso#> .
    @prefix ecpo:    <http://purl.org/ontology/ecpo#> .
    @prefix foaf:    <http://xmlns.com/foaf/0.1/> .
    @prefix frbr:    <http://purl.org/vocab/frbr/core#> .
    @prefix gr:      <http://purl.org/goodrelations/v1#> .
    @prefix org:     <http://www.w3.org/ns/org#> .
    @prefix owl:     <http://www.w3.org/2002/07/owl#> .
    @prefix rdac:    <http://rdaregistry.info/Elements/c/> .
    @prefix rdf:     <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
    @prefix rdfs:    <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix schema:  <http://schema.org/> .
    @prefix service: <http://purl.org/ontology/service#> .
    @prefix skos:    <http://www.w3.org/2004/02/skos/core#> .
    @prefix ssso:    <http://purl.org/ontology/ssso#> .
    @prefix vann:    <http://purl.org/vocab/vann/> .
    @prefix xsd:     <http://www.w3.org/2001/XMLSchema#> .

The Holding Ontology is defined in RDF/Turtle as following:

    <> a owl:Ontology ;
        dct:title "Holding Ontology"@en ;
        rdfs:label "Holding Ontology"@en ;
        vann:preferredNamespacePrefix "holding" ;
        vann:preferredNamespaceUri "http://purl.org/ontology/holding#" ;
        dct:modified "{GIT_REVISION_DATE}"^^xsd:date ;
        owl:versionInfo "{VERSION}" ;
        cc:license <http://creativecommons.org/licenses/by/3.0/> ;
        dct:creator "Carsten Klee", "Jakob Voß" 
    .

# Overview

| Classes<br>(defined by this ontology)| Classes<br>(defined by other ontologies) | Properties<br>(defined by this ontology) | Properties<br>(defined by other ontologies)|
|:---:|:---:|:---:|:---:|
| [Item]<br>[Agent]<br>[Document]| [DocumentService]<br>[Location]<br>[Chronology]| [collectedBy]<br>[heldBy]<br>[holds]<br>[exemplar]<br>[exemplarOf]<br>[broaderExemplar]<br>[broaderExemplarOf]<br>[narrowerExemplar]<br>[narrowerExemplarOf]<br>[label] | [availableFor]<br>[unavailableFor]<br>[providedBy]<br>[hasChronology]<br>[hasChronologyGap]<br>[availableAtOrFrom]<br>[hasStockKeepingUnit]<br>[siteOf]<br>[name] |

# Core Classes

The holding Ontology does not define classes on its own but makes usage of
classes defined in other Ontologies. See [References] for references to the
used onotologies.

## Item

[Item]: #item

An **Item** is a particular copy or exemplar of a document. The holding
ontology recommends to either use class [bf:HeldItem] from the [Bibframe Vocabulary], class [frbr:Item] from the [FRBR Ontology] or class [rdac:Item] from the [RDA Classes] vocabulary.

    holding:Item a owl:Class ;
        rdfs:label "Item"@en ;
        rdfs:comment "Use one of bf:HeldItem frbr:Item rdac:Item"@en ;
        owl:unionOf (bf:HeldItem frbr:Item rdac:Item) .

[frbr:Item]: http://purl.org/vocab/frbr/core#Item
[rdac:Item]: http://rdaregistry.info/Elements/c/Item
[bf:HeldItem]: http://bibframe.org/vocab/HeldItem

## Agent

[Agent]: #agent

An **Agent** is a person, organization, group or any other entity that can held
items and provide services. The holding ontology recommends to either use class
[foaf:Agent] from the [FOAF Ontology] or class [bf:Agent] from the [Bibframe Vocabulary].

    holding:Agent a owl:Class ;
        rdfs:label "Agent"@en ;
        rdfs:comment "Use one of bf:Agent or foaf:Agent"@en ;
        owl:unionOf (bf:Agent foaf:Agent) .

[foaf:Agent]: http://xmlns.com/foaf/0.1/Agent
[bf:Agent]: http://bibframe.org/vocab/Agent

## Document

[Document]: #document

A **Document** is a body of information used designed with the capacity (and
usually intent) to communicate.  A document may manifest symbolic, diagrammatic
or sensory-representational information.  Documents may include both abstract
works, such as "Romeo and Juliet", and more conrete entities, such as a
specific edition of a book.

The holding ontology recommends to either use class
[bibo:Document] from the [Bibliographic Ontology], class
[foaf:Document] from the [FOAF Ontology], class [bf:Work] or [bf:Instance] from the [Bibframe Vocabulary]. Some documents may
also be items ([Document] and [Item] are not disjoint).

    holding:Document a owl:Class ;
        rdfs:label "Document"@en ;
        rdfs:comment "Use one of bibo:Document, foaf:Document, bf:Work or bf:Instance"@en ;
        owl:unionOf (bibo:Document foaf:Document bf:Work bf:Instance) .

[bibo:Document]: http://purl.org/ontology/bibo/Document
[foaf:Document]: http://xmlns.com/foaf/0.1/Document
[bf:Work]: http://bibframe.org/vocab/Work
[bf:Instance]: http://bibframe.org/vocab/Instance

In the context of this ontology when talking about documents several kinds of documents are involved:

* the abstract document
* the document describing the title
* the document describing the holdings
* document as a website 

The reltions between an [Item] and different kinds of document is shown in this diagram:

`item-description-relation.md`{.include}

# Holding Relationships

## collectedBy

[collectedBy]: #collectedby

Relates an [Item] to an [Agent] who collected the item.

    holding:collectedBy a owl:ObjectProperty ;
        rdfs:label "held by"@en ;
        rdfs:comment "Relates an item to an agent who holds the item."@en ;
        rdfs:domain holding:Item ;
        rdfs:range holding:Agent ;
        rdfs:subPropertyOf holding:collectedBy .

## heldBy

[heldBy]: #heldby

Relates an [Item] to an [Agent] who holds the item.

    holding:heldBy a owl:ObjectProperty ;
        rdfs:label "held by"@en ;
        rdfs:comment "Relates an item to an agent who holds the item."@en ;
        rdfs:domain holding:Item ;
        rdfs:range holding:Agent ;
        owl:inverseOf holding:holds ;
        rdfs:seeAlso bf:heldBy ;
        rdfs:subPropertyOf holding:collectedBy .

## holds

[holds]: #holds

Relates an [Agent] to an [Item] which the [Agent] holds.

    holding:holds a owl:ObjectProperty ;
        rdfs:label "holds"@en ;
        rdfs:comment "Relates an agent to an item which the agent holds."@en ;
        rdfs:domain holding:Agent ;
        rdfs:range holding:Item ;
        owl:inverseOf holding:heldBy .


# Relations between abstract Documents and Items

The [exemplar] relation is used to state that a concrete [Item] is a copy of an abstract [Document]. Additional relations exist for items that only contain parts of a document and for items that contain multiple documents (for instance a collection that the document is part of). 

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
        rdfs:comment "Relates a document to an item that is an exemplar of the document. This property is similar to frbr:exemplar but does not refer to the class frbr:Manifestation."@en ;
        rdfs:domain holding:Document ;
        rdfs:range holding:Item ;
        owl:inverseOf holding:exemplarOf .

## exemplarOf

[exemplarOf]: #exemplarof

Relates an item to the document that is exemplified by the item.

    holding:exemplarOf a owl:ObjectProperty ;
        rdfs:label "is examplar of"@en ;
        rdfs:comment "Relates an item to the document that is exemplified by the item."@en ;
        rdfs:domain holding:Item ;
        rdfs:range holding:Document ;
        owl:inverseOf holding:exemplar .

## broaderExemplar

[broaderExemplar]: #broaderexemplar

Relates a document to an item that contains an exemplar of the document as part.

    holding:broaderExemplar a owl:ObjectProperty ;
        rdfs:label "broader exemplar"@en ;
        rdfs:comment "Relates a document to an item that contains an exemplar of the document as part."@en ;
        rdfs:domain holding:Document ;
        rdfs:range holding:Item ;
        owl:inverseOf holding:broaderExemplarOf .
    

## broaderExemplarOf

[broaderExemplarOf]: #broaderexemplarof

Relates an item to a document which is partly exemplified by the item.

    holding:broaderExemplarOf a owl:ObjectProperty ;
        rdfs:label "broader exemplar of"@en ;
        rdfs:comment "Relates an item to a document which is partly exemplified by the item."@en ;
        rdfs:domain holding:Item ;
        rdfs:range holding:Document ;
        owl:inverseOf holding:broaderExemplar .

## narrowerExemplar

[narrowerExemplar]: #narrowerexemplar

Relates an item to a document which is partly exemplified by the item.

    holding:narrowerExemplar a owl:ObjectProperty ;
        rdfs:label "narrower exemplar"@en ;
        rdfs:comment "Relates an item to a document which is partly exemplified by the item."@en ;
        rdfs:domain holding:Item ;
        rdfs:range holding:Document ;
        owl:inverseOf holding:narrowerExemplarOf .

## narrowerExemplarOf

[narrowerExemplarOf]: #narrowerexemplarof

Relates a document to an item that is an exemplar of a part of the document.

    holding:narrowerExemplarOf a owl:ObjectProperty ;
        rdfs:label "narrower exemplar of"@en ;
        rdfs:comment "Relates a document to an item that is an exemplar of a part of the document."@en ;
        rdfs:domain holding:Document ;
        rdfs:range holding:Item ;
        owl:inverseOf holding:narrowerExemplar .

# Relation between Items and Services

`item-offering-relation.md`{.include}

An [Item] may be available for a specific [DocumentService]. While an [Agent] provides a [DocumentService] for an [Item] this often implies an offer ([gr:Offering] and/or [schema:Offer]) to an unknown [Agent].

Thus

``` {.example}
$alicecopies
    daia:availableFor [
        a dso:Presentation ;
        gr:hasStockKeepingUnit "HB 17 Rg 500" ;
        service:providedBy <http://ld.zdb-services.de/resource/organisations/DE-1a> ;
    ] .
```

is a shortcut for

``` {.example}
<http://ld.zdb-services.de/resource/organisations/DE-1a>
    gr:offers [
        a gr:Offering ;
        gr:hasBusinessFunction [
            dso:Presentation;
            gr:hasStockKeepingUnit "HB 17 Rg 500" ;
        ] ;
        gr:includes $alicecopies
    ] .
```

## DocumentService

[DocumentService]: #documentservice

A **DocumentService** is a service that is related to one or more [documents](#document). The service involves a service provider (e.g.
a library) and an optional service consumer (e.g. a library patron). Both service provider and service consumer SHOULD be instances of [Agent]. The DocumentService class is defined by the [Document Service Ontology].

    dso:DocumentService a owl:Class ;
        rdfs:label "DocumentService" ;
        rdfs:isDefinedBy <http://purl.org/ontology/dso> .

## Location

[Location]: #location

A **Location** is a point or area of interest from which a particular [Item] or [DocumentService] is available. The property [availableAtorFrom] should be used to indicate the location of an offered [DocumentService] for an [Item]. The Location class is defined by [GoodRelations].

    gr:Location a owl:Class ;
        rdfs:label "Location"@en ;
        owl:equivalentClass schema:Place ;
        rdfs:isDefinedBy <http://purl.org/goodrelations/v1> .

## name

[name]: #name

When a [DocumentService] is offered for an [Item], this property is used to name the location where the [DocumentService] should be provided. The Location class is defined by [GoodRelations].

    gr:name a owl:AnnotationProperty ;
        skos:scopeNote "When a document service is offered for an item, this property is used to name the location where the document service should be provided."@en ;
        rdfs:isDefinedBy <http://purl.org/goodrelations/v1> .
 
## providedBy

[providedBy]: #providedby

Used to relate a [DocumentService] with an [Agent] who offered the service. This property is defined by the the [Service Ontology].

    service:providedBy a owl:AnnotationProperty ;
        skos:scopeNote "Used to relate a document service with an agent who offered the service." ;
        rdfs:isDefinedBy <http://purl.org/ontology/service> .

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
        rdfs:seeAlso schema:sku ;
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
        rdfs:domain holding:Item ;
        rdfs:range rdfs:Literal ;
        rdfs:seeAlso bf:label ;
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
$chapter3 a holding:Document ;
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
            a dso:Presentation ;
            gr:hasStockKeepingUnit "HB 17 Rg 500" ;
            service:providedBy <http://ld.zdb-services.de/resource/organisations/DE-1a> ;
            gr:availableAtOrFrom [
                a gr:Location ;
                gr:name "Leesesaal" ;
                org:siteOf <http://ld.zdb-services.de/resource/organisations/DE-1a>
            ]
        ] [
            dso:Loan ;
            gr:hasStockKeepingUnit "Zsn 70488" ;
            service:providedBy <http://ld.zdb-services.de/resource/organisations/DE-1a> ;
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
* [Service Ontology]
* [Schema.org]
* [Bibframe Vocabulary]
* [RDA Classes]

[Bibframe Vocabulary]: http://bibframe.org/
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
[Service Ontology]:  http://purl.org/ontology/service
[Schema.org]: http://schema.org
[schema:Offer]: http://schema.org/Offer
[gr:Offering]: http://purl.org/goodrelations/v1#Offering
[RDA Classes]: http://rdaregistry.info/Elements/c/
