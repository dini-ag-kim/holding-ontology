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


