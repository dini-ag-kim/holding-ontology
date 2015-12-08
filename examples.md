# Examples {.unnumbered}

## A book series, fully held by a library {.unnumbered}

<div class="example">
The series is a document, consisting of multiple volumes

    $series a bibo:Periodical 
        dct:hasPart $volume1, $volume2, $volume3 .

    $volume1 a bibo:Book ; bibo:volume "1" .
    $volume2 a bibo:Book ; bibo:volume "2" .
    $volume3 a bibo:Book ; bibo:volume "3" .

One chapter in Volume 1

    $chapter3 a bibo:Document ;
        dct:isPartOf $volume1 .

A copy of the full series

    $librarycopies 
        holding:exemplarOf $series ;
        holding:heldBy $library ;
        ecpo:hasChronology [
            a ecpo:CurrentChronology ;
            ecpo:hasBeginVolumeNumbering "1"
        ] .

A particular copy of volume 1, located in the library

    $librarycopyofvolume1
        holding:exemplarOf $volume1 ;
        holding:narrowerExemplarOf $series ;
        holding:broaderExemplaOf $chapter3 .
</div>

## The same series, partially held by Alice {.unnumbered}

<div class="example">
A copy of volume 1 and 2

    $alicecopies 
        holding:exemplarOf $series ;  
            # alteratively: holdings:narrowerExemplarOf $series
        dct:hasPart $volume2, $volume3
        holding:heldBy $alice ;
        ecpo:hasChronology [
            a ecpo:CurrentChronology ;
            ecpo:hasBeginVolumeNumbering "1" ;
            ecpo:hasEndVolumeNumbering "2" 
        ] .

Alice`s copies of volume 1

    $alicescopyofvolume1
        holding:exemplarOf $volume1 ;
        holding:narrowerExemplarOf $series ;
        holding:narrowerExemplarOf $alicescopies .
</div>

## Offering a Service for an Item {.unnumbered}

<div class="example">
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
</div>