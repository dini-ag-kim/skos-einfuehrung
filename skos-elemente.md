# Elemente von SKOS

Zusammenfassend eine Übersicht über alle in SKOS verwendeten Elemente:

## Konzepte

| Element                                                      | Beschreibung                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [skos:Concept](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#concepts) | Basisklasse für die Begriffe                                 |
| [skos:ConceptScheme](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#schemes) | Basisklasse für das Vokabular                                |
| [skos:hasTopConcept](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#schemes) | dieses Vokabular (skos:ConceptScheme) enthält folgende Begriffe auf der obersten Ebene ... |
| [skos:inScheme](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#schemes) | dieser Begriff gehört zu folgendem Schema ... ; muss für alle Begriffe im Schema gesetzt werden außer für diejenigen, bei denen skos:topConceptOf verwendet wird |
| [skos:topConceptOf](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#schemes) | dieser Begriff gehört zur obersten Ebene des folgenden Schemas ... |

```turtle
<http://zbw.eu/stw> a skos:ConceptScheme .
    skos:hasTopConcept <http://zbw.eu/stw/descriptor/19040-0> .

<http://zbw.eu/stw/descriptor/19040-0> a skos:Concept ;
    skos:topConceptOf <http://zbw.eu/stw> .

<http://zbw.eu/stw/descriptor/12036-5> a skos:Concept ;
    skos:inScheme <http://zbw.eu/stw> .
```

## Bezeichnungen

| Element                                                      | Beschreibung                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [skos:altLabel](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#labels) | Alternative Bezeichnung                                      |
| [skos:hiddenLabel](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#labels) | Weitere Bezeichnung für Indexierung und Suche (aber ungeeignet für die Anzeige) |
| [skos:notation](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#notations) | Notation mit explizitem Datentyp (RDF typed literal)         |
| [skos:prefLabel](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#labels) | Bevorzugte Bezeichnung                                       |

```turtle
<http://zbw.eu/stw> a skos:ConceptScheme ;
    skos:prefLabel "Standard-Thesaurus Wirtschaft" .

<http://zbw.eu/stw/descriptor/19040-0> a skos:Concept ;
    skos:prefLabel "Cooperation"@en, "Kooperation"@de ;
    skos:altLabel "Zusammenarbeit"@de ;
    skos:hiddenLabel "Zusammenwirken"@de ;
    skos:notation "33"^^ex:UDCNotation ;
    skos:inScheme <http://zbw.eu/stw> .
```

## Dokumentation

| Element                                                      | Beschreibung                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [skos:changeNote](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#notes) | Notiz für Bearbeiter/innen des Vokabulars zu kürzlich erfolgten Änderungen |
| [skos:definition](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#notes) | Kurzdefinition des Begriffs                                  |
| [skos:editorialNote](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#notes) | Notiz für Bearbeiter/innen des Vokabulars                    |
| [skos:example](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#notes) | Beispiel für die Verwendung des Begriffs                     |
| [skos:historyNote](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#notes) | historische Änderungen in der Bedeutung des Begriffs         |
| [skos:note](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#notes) | allgemeine Notiz                                             |
| [skos:scopeNote](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#notes) | Erläuterung zum Umfang der typischen Verwendung des Begriffs (von ... bis ...) |

```turtle
<http://zbw.eu/stw/descriptor/19040-0> a skos:Concept ;
    skos:changeNote "Beispiel ergänzt; FL 21.4.2020"@de ;
    skos:definition "Freiwillige Zusammenarbeit von Unternehmen, die rechtlich selbstständig bleiben"@de ;
    skos:editorialNote "Dieses Beispiel ist frei erfunden."@de ;
    skos:example "Einkaufsgemeinschaften im Handel"@de ;
    skos:historyNote "Anfang der 1970er Jahre neuer Erklärungsansatz durch Mesoökonomische Interaktionstheorie"@de ;
    skos:note "Die Nichtzusammenarbeit mit dem Schlechten gehört ebenso zu unseren Pflichten wie die Zusammenarbeit mit dem Guten (Mahatma Gandhi)"@de ;
    skos:scopeNote "Möglichst spezifischer indexieren."@de, "Use more specific descriptors whenever possible."@en .
```

## Relationen

| Element                                                      | Beschreibung                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [skos:broader](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#semantic-relations) | dieser Begriff hat folgende direkte Oberbegriffe ...         |
| [skos:broaderTransitive](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#semantic-relations) | wird technisch benutzt, um abgeleitete hierarchische Beziehungen zu definieren; üblicherweise bei Bedarf mit einem Reasoner generiert |
| [skos:narrower](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#semantic-relations) | dieser Begriff hat folgende direkte Unterbegriffe ...        |
| [skos:narrowerTransitive](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#semantic-relations) | wird technisch benutzt, um abgeleitete hierarchische Beziehungen zu definieren; üblicherweise bei Bedarf mit einem Reasoner generiert |
| [skos:related](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#semantic-relations) | dieser Begriff steht mit dem folgenden Begriff in Verbindung (assoziiert) ... |
| [skos:semanticRelation](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#semantic-relations) | wird aus den übrigen Relationen und Mappings (siehe externe Links unten) abgeleitet und üblicherweise nicht manuell verwendet |

```turtle
<http://zbw.eu/stw/descriptor/12036-5> a skos:Concept ;
    skos:broader <http://zbw.eu/stw/descriptor/19040-0> ;
    skos:narrower <http://zbw.eu/stw/descriptor/10897-5>, <http://zbw.eu/stw/descriptor/10923-2> ;
    skos:related <http://zbw.eu/stw/descriptor/10913-5>, <http://zbw.eu/stw/descriptor/18117-3> .
```

## Kollektionen

| Element                                                      | Beschreibung                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [skos:Collection](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#collections) | Sammlung von Begriffen; wird nur selten verwendet, wenn die Sammlung nicht selbst ein Begriff im Vokabular sein darf und eine zusätzliche Kategorisierungsebene benötigt wird |
| [skos:OrderedCollection](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#collections) | Sortierte Sammlung                                           |
| [skos:member](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#collections) | Die (unsortierte) Sammlung enthält folgende Mitglieder ...   |
| [skos:memberList](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#collections) | Die sortierte Sammlung enthält als erstes folgendes Mitglied ... (gefolgt von einem Element vom Typ rdf:List) |

```turtle
<http://zbw.eu/stw/descriptor/12668-3> a skos:Concept ;
    skos:prefLabel "Einkaufsgemeinschaft"@de .

<http://zbw.eu/stw/descriptor/10897-5> a skos:Concept ;
    skos:prefLabel "Fusion"@de .

<http://zbw.eu/stw/descriptor/10923-2> a skos:Concept ;
    skos:prefLabel "Kartell"@de .

_:dont-be-evil-fails a skos:Collection ;
    skos:prefLabel "Sammlung rechtmäßiger Unternehmenskooperation"@de ;
    skos:member <http://zbw.eu/stw/descriptor/12668-3> ;
    skos:member <http://zbw.eu/stw/descriptor/10897-5> .

_:b0 a skos:OrderedCollection ;
    skos:prefLabel "Unternehmenszusammenschlüsse sortiert nach Intensität"@de ;
    skos:memberList _:b1 .
_:b1 rdf:first <http://zbw.eu/stw/descriptor/10897-5> ;
    rdf:rest _:b2 .
_:b2 rdf:first <http://zbw.eu/stw/descriptor/10923-2> ;
    rdf:rest _:b3 .
_:b3 rdf:first <http://zbw.eu/stw/descriptor/12668-3> ;
    rdf:rest rdf:nil .
```

## Externe Links

| Element                                                      | Beschreibung                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [skos:broadMatch](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#mapping) | dieser Begriff hat folgenden Oberbegriff in einem anderen Vokabular .... |
| [skos:closeMatch](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#mapping) | dieser Begriff ähnelt folgendem Begriff in einem anderen Vokabular ... |
| [skos:exactMatch](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#mapping) | der gleiche Begriff in einem anderen Vokabular               |
| [skos:mappingRelation](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#mapping) | wird aus den Mappings abgeleitet und üblicherweise nicht manuell verwendet |
| [skos:narrowMatch](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#mapping) | dieser Begriff hat folgenden Unterbegriff in einem anderen Vokabular .... |
| [skos:relatedMatch](https://www.w3.org/TR/2009/REC-skos-reference-20090818/#mapping) | dieser Begriff steht mit dem folgenden Begriff in einem anderen Vokabular in Verbindung (assoziiert) ... |

```turtle
<http://zbw.eu/stw/descriptor/12036-5> a skos:Concept ;
    skos:exactMatch <https://d-nb.info/gnd/4078604-3> ;
	skos:narrowMatch <https://d-nb.info/gnd/4026844-5> ;
	skos:relatedMatch <https://d-nb.info/gnd/4133671-9> .
```
