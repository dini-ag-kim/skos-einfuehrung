# Einleitung

## Wozu kontrollierte Vokabulare?

Grob betrachtet bestehen alle Metadaten aus Elementen und zugehörigen Werten. Beispiel:

```yaml
title: Brückenbau
creator: Anne
date: 2020-04-21
language: de
subject: Bauingenieurwesen
```

Um diese für Menschen gut lesbare Beschreibung konsistent innerhalb eines technischen Systems abzubilden, wird ein **Metadatenschema** definiert. Dieses legt fest, welche Elemente es gibt, ob diese verpflichtend oder optional sind und welche Datentypen sie haben dürfen. Ein Schema könnte vereinfacht so aussehen:

| Element | verpflichtend | Datentyp |
|---------|---------------|----------|
| `title` | ja | Zeichenkette |
| `creator` | ja | Zeichenkette |
| `date` | nein | ISO 8601 |
| `language` | nein | ISO 639-1 |
| `subject` | nein  | Zeichenkette |

Hier ist die Datumsangabe nach ISO 8601 (JJJJ-MM-TT) und die Sprachangabe nach ISO 639-1 (2-stellige Sprachkürzel) formatiert. Fehlerhafte Eingaben wie `2020-21-04 ` (Monat und Tag vertauscht) oder `dd` (nicht existentes Sprachkürzel) können bei der Eingabe vom System erkannt und mit einer Fehlermeldung quittiert werden. Im Element `subject` ist jede Zeichenkette erlaubt, d.h. Schreibfehler wie `Bauigneurwesen` oder ein ähnliches Wort wie `Bautechnik` werden vom System nicht als Problem erkannt.

Nehmen wir an, wir wollen auf einem Hochschulschriftenserver die Fachdisziplin eindeutig erfassen, damit in einer Recherche danach gefiltert werden kann und in einer internen Statistik die Schriften nach Fachdisziplin gezählt werden können. Dann bietet es sich an, im Metadatenschema für das Element `subject` eine Wortliste zu definieren, die alle an der Hochschule vertretenen Fachdisziplinen beinhaltet. Eine Wortliste ist ein einfaches Beispiel für ein **kontrolliertes Vokabular**. Durch die begriffliche Kontrolle eines kontrollierten Vokabulars werden Schreibfehler, Bedeutungs- und Bezeichnungsvielfalt vermieden. Die dadurch erzeugte Einheitlichkeit fördert die Auffindbarkeit, Maschinenlesbarkeit und Nachnutzbarkeit der Metadaten.

Neben der Vereinheitlichung eigener Daten (hier Fachdisziplinen) helfen kontrollierte Vokabulare auch dabei um Daten aus verschiedenen Quellen eindeutig zusammenzuführen. So könnte im vorliegenden Beispiel die Autor*in statt als mehrdeutige Zeichenkette (vermutlich gibt es mehrere Personen mit dem Namen "Anne") mit einem Identifier aus der Gemeinsamen Normdatei (GND) oder dem Personen-Verzeichnis ORCID angegeben werden.

Wie ein Vokabular mit SKOS kodiert werden kann, wird [im folgenden Kapitel](skos-kodierung.md) anhand von Beispielen erläutert.

## Was ist SKOS?

Simple Knowledge Organization System (SKOS) ist ein Datenstandard für kontrollierte Vokabulare (Thesauri, Klassifikationen, Taxonomien usw.). Ziel des Standards ist die einfache Veröffentlichung und Nutzung von kontrollierten Vokabularen als [Linked Open Data](https://de.wikipedia.org/wiki/Linked_Open_Data). SKOS wurde 2009 [vom W3C als Empfehlung verabschiedet](https://www.w3.org/TR/2009/REC-skos-reference-20090818/) und findet seitdem zunehmende Verbreitung als Austauschformat:

- Bedeutende allgemeine kontrollierte Vokabulare (z.B. Thesaurus der UNESCO oder der EU) und zahlreiche fachspezifische (z.B. Standard-Thesaurus Wirtschaft der ZBW oder Thesaurus Sozialwissenschaften von GESIS) wurden bereits als SKOS veröffentlicht (siehe [Anwendungsbeispiele](skos-anwendungsbeispiele.md)).
- Die meisten aktuellen Thesaurus-Management-Systeme unterstützen SKOS. Es gibt außerdem zahlreiche Tools, welche die Veröffentlichung und Nutzung von Vokabularen als SKOS vereinfachen (siehe [Software](skos-software.md)).

SKOS basiert auf dem graph-orientierten Datenmodell [Resource Description Framework](https://de.wikipedia.org/wiki/Resource_Description_Framework) (RDF) und wird entsprechend den Regeln von RDF kodiert (siehe [Kodierung](skos-kodierung.md)). Dadurch ist das Vokabular maschinenlesbar und kompatibel mit den Grundlagen des (Semantic) Web. SKOS unterstützt Mehrsprachigkeit, jeder Begriff erhält einen Identifier (URI) und Verknüpfungen mit externen Vokabularen sind möglich. Als Datenformate stehen die Serialisierungen zur Verfügung, die auch RDF bietet, also [RDF/XML](RDF/XML), [N-Triples](https://format.gbv.de/rdf/ntriples), [Turtle](https://format.gbv.de/rdf/turtle), [JSON-LD](https://format.gbv.de/rdf/json-ld) und weitere.

## Verwendungszwecke

- Als Autor\*in oder Herausgeber\*in können sie SKOS nutzen um ihre Publikationen mit eindeutigen Begriffen statt mit freien, mehrdeutigen Schlagwörtern **inhaltlich zu beschreiben**. Beispielsweise können sie als Lehrende\*r ihre Lehrmaterialien geeigneten Einträgen aus vorhandenen SKOS-Vokabularen wie dem [Standard-Thesaurus Wirtschaft](https://zbw.eu/stw/) und der [Destatis-Systematik der Studienfächer](https://w3id.org/kim/hochschulfaechersystematik/scheme)) zuzuordnen.
- Wenn sie als als Herausgeber\*in oder Bibliothekar\*in eine Sammlung von Publikationen verwalten, beispielsweise ein Hochschulrepositorium, können sie die Materialien mit SKOS-Vokabularen **einheitlich erschließen**.
- Als Entwickler\*in von Infrastruktur und Software zum Erstellen, Publizieren oder Teilen von OER oder anderen Publikationen können Sie SKOS-Vokabulare einbetten oder sogar die Erstellung von SKOS-Vokabularen in der Software unterstützen, um Metadaten-Werte **kontrolliert zu erfassen**.

## Vorteile

- Die Maschinenlesbarkeit von SKOS-Vokabularen fördert die **Auffindbarkeit** von Lehrmaterialien und anderen Publikationen.
- Zu Begriffen können Definitionen und **vertiefende Informationen** nachgeschlagen werden.
- Durch die Veröffentlichung von SKOS-Vokabularen wird die **Nachnutzung der Vokabulare** erleichtert und damit langfristig mehr Einheitlichkeit erzielt oder zumindest der Arbeitsaufwand beim Erstellen von Vokabularen reduziert.
- Die Unterstützung von **Mehrsprachigkeit** fördert die Entwicklung von international genutzten Vokabularen.
- Die Kompatibilität zum Semantic Web ermöglicht **Verlinkung** zu Begriffen in anderen SKOS-Vokabularen und zu weiteren Webressourcen.

