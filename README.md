# Einführung in SKOS am Beispiel von Open Educational Resources (OER)

von [Felix Lohmeier](https://felixlohmeier.de) und [Adrian Pohl](https://lobid.org/team/ap)

Diese Einführung soll die Nutzung der Beschreibungssprache **Simple Knowledge Organization System** (SKOS) für kontrollierte Vokabulare erleichtern. Wir diskutieren den Zweck und die Vorteile am Beispiel von [Open Educational Resources](https://de.wikipedia.org/wiki/Open_Educational_Resources) (OER).

Diese Seite beinhaltet einen theoretischen Überblick. Wer direkt praktisch einsteigen möchte, kann im [Tutorial](skos-tutorial.md) ein SKOS-Vokabular von Grund auf erstellen und veröffentlichen.

## Wozu kontrollierte Vokabulare?

Grob betrachtet bestehen alle Metadaten aus Elementen und zugehörigen Werten. Beispiel:

```yaml
title: Beispiel
creator: Anne
date: 2020-04-21
language: de
subject: Bauingenieurwesen
```

Um diese für Menschen gut lesbare Beschreibung konsistent innerhalb eines technischen Systems abzubilden, wird ein Metadatenschema definiert. Dieses legt fest, welche Elemente es gibt, ob diese verpflichtend oder optional sind und welche Inhaltstypen sie haben dürfen. Ein Schema könnte vereinfacht so aussehen:

```yaml
mandatory:
  - title: string
  - creator: string
optional:
  - date: ISO8601
  - language: ISO639-1
  - subject: string
```

Hier ist die Datumsangabe nach ISO 8601 (JJJJ-MM-TT) und die Sprachangabe nach ISO 639-1 (2-stellige Sprachkürzel) formatiert. Fehlerhafte Eingaben wie `2020-21-04 ` (Monat und Tag vertauscht) oder `dd` (nicht existentes Sprachkürzel) können bei der Eingabe vom System erkannt und mit einer Fehlermeldung quittiert werden. Im Element `subject` ist jede Zeichenkette (string) erlaubt, d.h. Schreibfehler wie `Bauingeneurwesen` oder ein ähnliches Wort wie `Bautechnik` werden vom System nicht als Problem erkannt.

Nehmen wir an, wir wollen auf einem Hochschulschriftenserver die Fachdisziplin eindeutig erfassen, damit in einer Recherche danach gefiltert werden kann und in einer internen Statistik die Schriften nach Fachdisziplin gezählt werden können. Dann bietet es sich an, im Metadatenschema für das Element `subject` eine Wortliste zu definieren, die alle an der Hochschule vertretenen Fachdisziplinen beinhaltet. Wie so ein kontrolliertes Vokabular mit SKOS kodiert werden kann, wird weiter unten erläutert.

Durch die begriffliche Kontrolle werden Schreibfehler, Bedeutungs- und Bezeichnungsvielfalt vermieden. Die dadurch erzeugte Einheitlichkeit fördert die Auffindbarkeit, Maschinenlesbarkeit und Nachnutzbarkeit der Metadaten.

## Kurzbeschreibung

Simple Knowledge Organization System (SKOS) ist eine Beschreibungssprache für kontrollierte Vokabulare (Thesauri, Klassifikationen, Taxonomien usw.). Ziel des Standards ist die einfache Veröffentlichung und Nutzung von kontrollierten Vokabularen als [Linked Open Data](https://de.wikipedia.org/wiki/Linked_Open_Data). SKOS wurde 2009 [vom W3C als Empfehlung verabschiedet](https://www.w3.org/TR/2009/REC-skos-reference-20090818/) und findet seitdem zunehmende Verbreitung als Austauschformat:

* Bedeutende allgemeine kontrollierte Vokabulare (z.B. Thesaurus der UNESCO oder der EU) und zahlreiche fachspezifische (z.B. Standard-Thesaurus Wirtschaft der ZBW oder Thesaurus Sozialwissenschaften von GESIS) wurden bereits als SKOS veröffentlicht (vgl. [Anwendungsbeispiele](skos-anwendungsbeispiele.md)).
* Die meisten aktuellen Thesaurus-Management-Systeme unterstützen SKOS. Es gibt außerdem zahlreiche Tools, welche die Veröffentlichung und Nutzung von Vokabularen als SKOS vereinfachen  (vgl. [Software](skos-software.md)).

SKOS wird im graph-basierten Datenmodell [Resource Description Framework](https://de.wikipedia.org/wiki/Resource_Description_Framework) (RDF) kodiert. Durch diese Form der Kodierung ist das Vokabular maschinenlesbar und web-kompatibel. SKOS unterstützt Mehrsprachigkeit, jeder Begriff erhält einen Identifier (URI) und Verknüpfungen mit externen Vokabularen im Web sind möglich. Als Datenformate stehen die Serialisierungen zur Verfügung, die auch RDF bietet, also [RDF/XML](RDF/XML), [N-Triples](https://format.gbv.de/rdf/ntriples), [Turtle](https://format.gbv.de/rdf/turtle), [JSON-LD](https://format.gbv.de/rdf/json-ld) und weitere.

## Verwendungszwecke

* Als Lehrende\*r können Sie vorhandene SKOS-Vokabulare nutzen, um Ihre Lehrmaterialien mit geeigneten fachspezifischen Schlagwörtern (z.B. [Standard-Thesaurus Wirtschaft](http://bartoc-skosmos.unibas.ch/STW/en/?clang=de)) zu beschreiben oder bestimmten Studienfächern (z.B. [Destatis-Systematik der Studienfächer](https://skohub.io/dini-ag-kim/hochschulfaechersystematik/heads/master/w3id.org/kim/hochschulfaechersystematik/scheme.html)) zuzuordnen.
* Als Betreiber\*in eines Hochschulrepositoriums können Sie vorhandene SKOS-Vokabulare nutzen, um die Materialien zu erschließen.
* Als Entwickler\*in einer Infrastruktur zum Erstellen, Publizieren oder Teilen von OER können Sie SKOS-Vokabulare einbetten oder sogar die Erstellung von SKOS-Vokabularen in der Software unterstützen, um Werte in Metadaten kontrolliert zu erfassen.

## Vorteile

* Die Maschinenlesbarkeit von SKOS-Vokabularen fördert die Auffindbarkeit der Lehrmaterialien und ermöglicht das automatische Laden von vertiefenden Informationen zu den Begriffen (Lookup).
* Durch die Veröffentlichung von SKOS-Vokabularen wird die Nachnutzung der Vokabulare erleichtert und damit langfristig mehr Einheitlichkeit erzielt oder zumindest der Arbeitsaufwand beim Erstellen von Vokabularen reduziert.
* Die Unterstützung von Mehrsprachigkeit fördert die Entwicklung von international genutzten Vokabularen.
* Die Kompatibilität zum Semantic Web ermöglicht Links zu Begriffen in externen SKOS-Vokabularen oder sogar Links zu externen Webressourcen.

## Weitere Inhalte dieser Einführung

* [Kodierung](skos-kodierung.md) in RDF/Turtle erklärt am Beispiel des Standard-Thesaurus Wirtschaft
* [Elemente](skos-elemente.md) von SKOS
* [Tutorial](skos-tutorial.md) zur Erstellung und Veröffentlichung eines kontrollierten Vokabulars
* [Anwendungsbeispiele](skos-anwendungsbeispiele.md)
* [Software](skos-software.md)
* [Literatur](skos-literatur.md)
* [Über diese Einführung](about.md)
