# Einführung in SKOS für den Bereich Open Educational Resources (OER)

Diese Einführung soll die Nutzung der Beschreibungssprache **Simple Knowledge Organization System** (SKOS) für kontrollierte Vokabulare erleichtern und damit die Standardisierung von Metadaten im Bereich [Open Educational Resources](https://de.wikipedia.org/wiki/Open_Educational_Resources) (OER) unterstützen.

Dieses Dokument beinhaltet einen theoretischen Überblick. Wer direkt praktisch einsteigen möchte, kann im [Tutorial](skos-tutorial.md) ein SKOS-Vokabular von Grund auf erstellen und veröffentlichen.

## Kurzbeschreibung

Simple Knowledge Organization System (SKOS) ist eine Beschreibungssprache für kontrollierte Vokabulare (Thesauri, Klassifikationen, Taxonomien usw.). Ziel des Standards ist die einfache Veröffentlichung und Nutzung von kontrollierten Vokabularen als [Linked Open Data](https://de.wikipedia.org/wiki/Linked_Open_Data). SKOS wurde 2009 [vom W3C als Empfehlung verabschiedet](https://www.w3.org/TR/2009/REC-skos-reference-20090818/) und findet seitdem zunehmende Verbreitung als Austauschformat:

* Bedeutende allgemeine kontrollierte Vokabulare (z.B. Thesaurus der UNESCO oder der EU) und zahlreiche Fachspezifische (z.B. Standard-Thesaurus Wirtschaft der ZBW oder Thesaurus Sozialwissenschaften von GESIS) wurden bereits als SKOS veröffentlicht (vgl. [Anwendungsbeispiele](skos-anwendungsbeispiele.md)).
* Die meisten aktuellen Thesaurus-Management-Systeme unterstützen SKOS. Es gibt außerdem zahlreiche Tools, welche die Veröffentlichung und Nutzung von Vokabularen als SKOS vereinfacht  (vgl. [Software](skos-software.md)).

SKOS wird im graph-basierten Datenmodell [Resource Description Framework](https://de.wikipedia.org/wiki/Resource_Description_Framework) (RDF) kodiert. Durch diese Form der Kodierung ist das Vokabular maschinenlesbar und web-kompatibel. SKOS unterstützt Mehrsprachigkeit, jeder Wert erhält einen Identifier (URI) und Verknüpfungen mit externen Vokabularen im Web sind möglich. Als Datenformate stehen die Serialisierungen zur Verfügung, die auch RDF bietet, also [RDF/XML](RDF/XML), [N-Triples](https://format.gbv.de/rdf/ntriples), [Turtle](https://format.gbv.de/rdf/turtle), [JSON-LD](https://format.gbv.de/rdf/json-ld) und [HDT](https://format.gbv.de/rdf/hdt).

## Verwendungszwecke

* Als Lehrende/r können Sie vorhandene SKOS-Vokabulare nutzen, um Ihre Lehrmaterialien mit geeigneten fachspezifischen Schlagwörtern (z.B. [Standard-Thesaurus Wirtschaft](http://bartoc-skosmos.unibas.ch/STW/en/?clang=de)) zu beschreiben oder bestimmten Studienfächern (z.B. [Destatis-Systematik der Studienfächer](https://skohub.io/dini-ag-kim/hochschulfaechersystematik/heads/master/w3id.org/kim/hochschulfaechersystematik/scheme.html)) zuzuordnen.
* Als Betreiber/in eines Hochschulrepositoriums können Sie vorhandene SKOS-Vokabulare nutzen, um die Materialien zu erschließen. Für die Struktur der Hochschule mit allen ihren Instituten und Forschungsbereichen können Sie ein neues SKOS-Vokabular definieren und veröffentlichen.
* Als Entwickler/in einer Infrastruktur zum Erstellen, Publizieren oder Teilen von OER können Sie SKOS-Vokabulare einbetten oder sogar die Erstellung von SKOS-Vokabularen in der Software unterstützen, um Werte in Metadaten kontrolliert zu erfassen.

## Vorteile

* Die Maschinenlesbarkeit von SKOS-Vokabularen fördert die Auffindbarkeit der Lehrmaterialien und ermöglicht das automatische Laden von vertiefenden Informationen zu den Begriffen (Lookup).
* Durch die Veröffentlichung von SKOS-Vokabularen wird die Nachnutzung der Vokabulare erleichtert und damit langfristig mehr Einheitlichkeit erzielt oder zumindest der Arbeitsaufwand beim Erstellen von Vokabularen reduziert.
* Die Unterstützung von Mehrsprachigkeit fördert die Entwicklung von international genutzten Vokabularen.
* Die Kompatibilität zum Semantic Web ermöglicht Links zu Begriffen in externen SKOS-Vokabularen oder sogar Links zu externen Webressourcen.

## Technischer Aufbau

...

## Weitere Inhalte dieser Einführung

* [Tutorial](skos-tutorial.md) zur Erstellung und Veröffentlichung eines kontrollierten Mini-Vokabulars
* [Häufig gestellte Fragen](skos-faq.md) (FAQ)
* [Anwendungsbeispiele](skos-anwendungsbeispiele.md)
* [Software](skos-software.md)
* [Literatur](skos-literatur.md)
