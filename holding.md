# Introduction

The **Holding Ontology** is a vocabulary to express library holdings in RDF.

## Status of this document

This document is an early draft, created by a DINI AG KIM Working Group. See
<https://wiki.dnb.de/display/DINIAGKIM/Bestandsdaten+Gruppe> for more
resources.

## Namespaces and Ontology

The URI namespace of this ontology is ... The namespace prefix `...` is recommeded.
The URI of this ontology as a whole is ...

The following namspace prefixes are used to refer to related ontologies:

    @prefix foaf: <http://xmlns.com/foaf/0.1/> .
    @prefix owl:   <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix daia: <http://purl.org/ontology/daia/> .
    @prefix dso: <http://purl.org/ontology/dso#> .
    @prefix ssso: <http://purl.org/ontology/ssso#> .
    @prefix ecpo: <http://purl.org/ontology/ecpo#> .
    @prefix dcterms: <http://purl.org/dc/terms/> .

{OVERVIEW}

...

# Classes

## Agent

[Agent]: #agent

An **Agent** is a person, organization, group or any other entity that can held
items and provide services. The agent class is defined by the [FOAF Ontology].

    foaf:Agent a owl:Class ;
        rdfs:label "agent" ;
        rdfs:isDefinedBy <http://xmlns.com/foaf/0.1/> .

## Item

[Item]: #item

An **item** is a particular copy of a bibliographic resource that is held by an
[Agent]. Items are also referred to as holdings, but a holding can include more
information about items, such as inventory and access.


## Document

[Document]: #document

...

## DocumentService

[DocumentService]: #documentservice

A **DocumentService** is a service event that is related to one or more
[documents](#document). The service event involves a service provider (e.g.
a library) and an optional service consumer (e.g. a library patron). Both
service provider and service consumer SHOULD be instances of
[foaf:Agent](#Agent). The DocumentService class is defined by the [Document
Service Ontology].

    dso:DocumentService a owl:Class ;
        rdfs:label "DocumentService" ;
        rdfs:isDefinedBy <http://purl.org/ontology/dso> .

Typical document services within the scope of holdings ontology involve a loan
event ([dso:Loan]) and a presentation event ([dso:Presentation]). To express 
the availability of items for selected services, one SHOULD use the properties
[daia:availableFor] and [daia:unavailableFor] from the [DAIA Ontology].

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

# Object properties

## narrowerExemplar

...

## narrowerExemplarOf

...

## broaderExemplar

...

## broaderExemplarOf

...

## exemplar

...

## exemplarOf

...

## heldBy

...

## holds

...

# Datatype Properties

# Examples

...

``` {.example}

```

# References

## Normative References

...

## Informative References

* ISO 20775
* ...

[FOAF Ontology]: http://xmlns.com/foaf/spec/ 
[Document Service Ontology]: http://purl.org/ontology/dso
[DAIA Ontology]: http://purl.org/ontology/daia
[Enumeration and Chronology of Periodicals Ontology]: http://purl.org/ontology/ecpo


