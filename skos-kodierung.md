# Kodierung

Wie in der [Einleitung](skos-einleitung.md) erwähnt, wird SKOS im graph-basierten Datenmodell RDF kodiert. Wir verwenden für die Code-Schnipsel im folgenden Beispiel die RDF-Serialisierung [Turtle](https://format.gbv.de/rdf/turtle), weil diese am besten lesbar ist. 

## RDF/Turtle

In der einfachsten Form werden in Turtle die RDF-Tripel (Subjekt, Prädikat, Objekt) direkt hintereinander mit Leerzeichen getrennt in eine Zeile geschrieben und mit einem Punkt abgeschlossen. Hier ein allgemeines Beispiel (mit [DC Terms](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/)-Prädikaten statt SKOS):

Die folgenden beiden Tripel...

| Subjekt                         | Prädikat      | Objekt       |
| ------------------------------- | ------------- | ------------ |
| `<http://example.org/beispiel>` | `<http://purl.org/dc/terms/creator>` | `"Anne"`     |
| `<http://example.org/beispiel>` | `<http://purl.org/dc/terms/title>`   | `"Brückenbau"` |

werden in der einfachsten Form so kodiert:

```turtle
<http://example.org/beispiel> <http://purl.org/dc/terms/creator> "Anne" .
<http://example.org/beispiel> <http://purl.org/dc/terms/title> "Brückenbau" .
```

Zur besseren Lesbarkeit verwenden wir für die Prädikate ein Namensraum-Präfix und für mehrere Tripel mit gleichem Subjekt eine verkürzte Form (Prädikat-Objekt-Paare mit Semikolon getrennt und mit Leerzeichen eingerückt):

```turtle
@prefix dct: <http://purl.org/dc/terms/> .

<http://example.org/beispiel>
    dct:creator "Anne" ;
    dct:title "Brückenbau" .
```

Und wenn es mehrere Objekte zu einem Prädikat gibt – wie beispielsweise einen weiteren Tripel mit dem Autor `Tim` (`<http://example.org/beispiel>` `dct:creator` `"Tim"`) – dann nutzen wir zusätzlich die folgende verkürzte Form (mehrere Objekte mit Komma getrennt):

```turtle
@prefix dct: <http://purl.org/dc/terms/> .

<http://example.org/beispiel>
    dct:creator "Anne", "Tim" ;
    dct:title "Brückenbau" .
```

Zeilenumbrüche und Einrückungen dienen in RDF/Turtle übrigens nur der besseren Lesbarkeit, können also frei verwendet oder weggelassen werden.

## Beispiel Standard-Thesaurus Wirtschaft

Nun zu einem konkreten Beispiel für ein kontrolliertes Vokabular. Die Webseite zum Begriff [Kooperation im Standard-Thesaurus Wirtschaft](https://via.hypothes.is/https://zbw.eu/stw/version/latest/descriptor/19040-0/about.de.html) sieht wie folgt aus (auf die gelb markierten Wörter gehen wir gleich im Einzelnen ein):

![Screenshot Standard-Thesaurus-Wirtschaft zum Begriff Kooperation](images/stw-kooperation.png)

Zur Kodierung des Beispiels in SKOS mit RDF/Turtle sollte zunächst das Namensraum-Präfix für SKOS festgelegt definiert werden:

```turtle
@prefix skos: <http://www.w3.org/2004/02/skos/core#> .
```

Es folgen die markierten Elemente des Thesaurus-Eintrags.

### Identifier und Hauptbezeichnung

Der Eintrag "Kooperation / Cooperation" im Thesaurus hat den **Identifier** <http://zbw.eu/stw/descriptor/19040-0>. Dieser wird in SKOS als Ausgangspunkt genutzt (und nicht etwa der Name des Eintrags). Identifier müssen URIs sein, wobei die Verwendung von HTTP-URIs (beginnend mit `http://` oder `https://`) empfohlen wird.

Die Hauptbezeichnungen werden mit `skos:prefLabel` ergänzt. Verschiedenen **Sprachen** werden gemäß RDF/Turtle durch den Anhang `@de` bzw. `@en` festgelegt. Pro Sprache darf ein Eintrag nur eine Hauptbezeichnung haben.

```turtle
<http://zbw.eu/stw/descriptor/19040-0>
    skos:prefLabel "Cooperation"@en, "Kooperation"@de .
```

### Alternative Bezeichnungen

Alternative Bezeichnungen wie "Zusammenarbeit" werden mit `skos:altLabel` ergänzt.

```turtle
<http://zbw.eu/stw/descriptor/19040-0>
    skos:altLabel "Zusammenarbeit"@de .
```

### Unterbegriffe

Zur Abbildung von Hierarchien wird in SKOS das Paar `skos:broader` ("hat einen Oberbegriff") und `skos:narrower` ("hat einen Unterbegriff") verwendet. In der fertigen Datei sollten beide Richtungen angegeben sein, also hier im Beispiel:

- "Kooperation" hat den Unterbegriff (`skos:narrower`) "Forschungskooperation"
- "Forschungskooperation" hat den Oberbegriff (`skos:broader`) "Kooperation"

Wenn aber eine Software für die Erstellung des SKOS-Vokabulars verwendet wird, dann reicht es meist aus nur eine Richtung anzugeben, weil die andere Richtung dann automatisch von der Software ergänzt wird.

Da die Verlinkung in RDF grundsätzlich über URIs funktioniert, müssen statt den Bezeichnungen "Forschungskooperation", "Internationale Zusammenarbeit", "Öffentlich-private Partnerschaft" und "Unternehmenskooperation" die entsprechenden Identifier dieser Einträge verwendet werden. Die Unterbegriffe würden also wie folgt angegeben:

```turtle
<http://zbw.eu/stw/descriptor/19040-0>
    skos:narrower <http://zbw.eu/stw/descriptor/12036-5>,
                  <http://zbw.eu/stw/descriptor/18775-0>,
                  <http://zbw.eu/stw/descriptor/18822-3>,
                  <http://zbw.eu/stw/descriptor/19708-3> .
```

### Verwandte Begriffe

Falls mehrere Begriffe nicht in einer direkten Hierarchie zueinander stehen, sondern nur irgendwie miteinander verbunden sind, dann wird das Prädikat `skos:related` verwendet. Die Verbindung zu den drei verwandten Begriffen "Interoperabilität", "Kooperative Führung" und "Netzwerk" wird so angegeben:

```turtle
<http://zbw.eu/stw/descriptor/19040-0>
    skos:related <http://zbw.eu/stw/descriptor/12580-3>,
                 <http://zbw.eu/stw/descriptor/18657-6>, 
                 <http://zbw.eu/stw/descriptor/20402-3> .
```

### Notationen

Der Thesaurus-Eintrag des STW ist zusätzlich in eine Systematik eingeordnet. Die entsprechende Klasse in der Systematik ist wiederum ein SKOS-Eintrag mit der Bezeichnung "A.00 Allgemeinwörter". Die Zeichenkette "A.00" ist eine Notation, die als lokaler Identifier innerhalb der Systematik dient. In SKOS lassen sich Notationen mit `skos:notation` angeben:

```turtle
<http://zbw.eu/stw/thsys/70582> skos:notation "A.00" .
```

Wenn die Notation innerhalb eines Vokabulars dauerhaft eindeutig ist, wird sie in vielen Vokabularen auch als Bestandteil der entsprechenden Identifiern verwendet (so hat zum Beispiel in der Basisklassifikation der Eintrag mit der Notation "85.06" die URI <http://uri.gbv.de/terminology/bk/85.06>). Bei der Systematik des STW basieren die Identifier nicht auf den Notationen sondern auf internen ID-Nummern (in diesem Fall `70582`).

Für die Verknüpfung von Thesaurus-Einträgen mit Systemstellen einer zusätzlichen Systematik gibt es in SKOS kein Standard-Prädikat. Die Autor*innen des STW haben sich dazu entscheiden, die Beziehung mit `skos:broader` als Überordnung zu kodieren:

```turtle
<http://zbw.eu/stw/descriptor/19040-0>
    skos:broader <http://zbw.eu/stw/thsys/70582> .
```

Auf der Webseite werden die Verweise mit `skos:broader` unter zwei Überschriften ("Oberbegriffe" und "Thesaurus Systematik") gruppiert. Solch eine Gruppierung ist nicht Teil der SKOS-Kodierung sondern erfolgt wahrscheinlich in der Anzeige durch Analyse mit welcher Zeichenkette die Identifier anfangen (Oberbegriffe: `http://zbw.eu/stw/descriptor` und Thesaurus Systematik: `http://zbw.eu/stw/thsys`).

### Mappings zu anderen Vokabularen

Für Links ("Mappings") zu übereinstimmenden Einträgen in (anderen) Vokabulare gibt es in SKOS drei Prädikate (`skos:relatedMatch`, `skos:closeMatch` und `skos:exactMatch`) die sich nach Grad der Genauigkeiten unterscheiden. In diesem Beispiel gehen die Autor*innen in drei Fällen von einer exakten Übereinstimmung aus (`skos:exactMatch`). Der GND-Begriff "Innerbetriebliche Kooperation" ist dagegen spezifischer als der STW-Eintrag, so dass hier ein übergeordnetes Mapping verwendet wird (`skos:broadMatch`).

```turtle
<http://zbw.eu/stw/descriptor/19040-0>
    skos:exactMatch
        <http://aims.fao.org/aos/agrovoc/c_1855>,
        <http://dbpedia.org/resource/Cooperation>,
        <http://lod.gesis.org/thesoz/concept_10042918>,
        <https://d-nb.info/gnd/4032386-9> ;
    skos:broadMatch
        <https://d-nb.info/gnd/027061-0> .
```

Die Quellenangabe `(aus DBpedia)` steht nicht explizit in der SKOS-Datei. Wahrscheinlich erfolgt die Darstellung auf der Webseite auch hier wieder über eine Auswertung des Adressbestandteils im Identifier mit Hilfe einer Übersetzungstabelle, also beispielsweise `dbpedia.org` -> "(aus DBpedia)".

## Technischer Aufbau

Neben den im obigen Beispiel verwendeten Elementen bedarf es noch ein paar allgemeiner Angaben, um eine valide Datei mit dem SKOS-Vokabular zu erstellen.

Zunächst muss das Vokabular selbst mit `skos:ConceptScheme` definiert werden (auch wenn es wie hier im Beispiel nur einen Begriff enthält).

```turtle
<http://zbw.eu/stw>
    a skos:ConceptScheme ;
    skos:prefLabel "Standard-Thesaurus Wirtschaft" .
```

Weiterhin muss jeder Begriff als `skos:Concept` definiert und explizit dem Vokabular zugeordnet (`skos:inScheme`) werden:

```turtle
<http://zbw.eu/stw/descriptor/19040-0>
    a skos:Concept ;
    skos:inScheme <http://zbw.eu/stw> .
```

Und um die Identifier nicht immer vollständig wiederholen zu müssen, gibt es Abkürzungen. Dazu wird oft zu Beginn eine Basis-URL definiert:

```turtle
@base <http://zbw.eu/stw/descriptor/> .
```

## Vollständiges Beispiel

Unser obiges Beispiel könnte im Format RDF/Turtle also so aussehen:

```turtle
@base <http://zbw.eu/stw/descriptor/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix skos: <http://www.w3.org/2004/02/skos/core#> .

<http://zbw.eu/stw> a skos:ConceptScheme ;
    skos:prefLabel "Standard-Thesaurus Wirtschaft" .

<19040-0> a skos:Concept ;
    skos:prefLabel "Cooperation"@en, "Kooperation"@de ;
    skos:altLabel "Zusammenarbeit"@de ;
    skos:narrower <12036-5>, <18775-0>, <18822-3>, <19708-3> ;
    skos:related <12580-3>, <18657-6>, <20402-3> ;
    skos:exactMatch
        <http://aims.fao.org/aos/agrovoc/c_1855>,
        <http://dbpedia.org/resource/Cooperation>,
        <http://lod.gesis.org/thesoz/concept_10042918>, 
        <https://d-nb.info/gnd/4032386-9> ;
    skos:broadMatch
        <https://d-nb.info/gnd/027061-0> .
    skos:inScheme <http://zbw.eu/stw> .
```

Die vom Standard-Thesaurus Wirtschaft [angebotene Datei](https://zbw.eu/stw/version/latest/descriptor/19040-0/about.ttl) sieht im Übrigen noch etwas anders aus. Sie enthält noch weitere Informationen, die in der HTML-Darstellung nicht zu sehen sind (z.B. eine Nummer im Bibliothekskatalog `gbv:gvkppn` und interne Daten wie z.B. `zbwext:indexedItem`). Außerdem ist der Aufbau etwas technischer, weil die Datei generiert und nicht "von Hand" geschrieben wurde. So werden beispielsweise am Anfang viele Präfixe definiert, die für diesen konkreten Begriff gar nicht verwendet werden.
