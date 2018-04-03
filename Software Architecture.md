## Software Architecture
Persönliche Zusammenfassung der Vorlesung SWA FS 2018.

### Definition

Was genau unter der Disziplin Software Architektur verstanden wird ist nicht abschliessend definiert, es gibt verschiedene Sichtweisen welche folgend kurz zusammengefasst werden.  

* Architektur liefert Baupläne für Software. Diese werden so gemacht, dass deren Einhaltung zur Erreichung der relevanten Qualität führt. Baupläne helfen zudem den Entwicklungsprozess  zu organisieren.
* Architektur ist das Gesamtbild (Qualität), das alle Team-Mitglieder verbindet. Individuelle Entscheidungen der Mitglieder sind im Rahmen dieses Gesamtbildes möglich.
* Die Struktur der Architektur, ihre Komponenten und Beziehungen müssen auch im Code auffindbar sein.

### Erarbeitung / Ablauf

1. Ziele, Anforderungen und Qualitätsansprüche werden definieren
2. Entwurf der Architektur wird erarbeitet
3. Führt zu Lösungs-Strategien, grober Aufbau
4. Architektur wird umgesetzt
5. Führt zu Source-Code

### Nutzen

Software-Architektur heisst, über den Aufbau eines Systems nachzudenken ohne direkt detaillierten Source-Code zu schreiben. Es geht also im wesentlichen darum, Details zu abstrahieren und sich auf gröbere Strukturen zu konzentrieren. Konkret:

* **Schnittstellen**. Sollte man verstehen ohne die Implementation lesen zu müssen. Ermöglicht Arbeitsteilung im Team aber auch darüber hinaus. 
* **Einarbeitung**. Einfacher Zugang für neue Mitarbeiter (Top-Down). Heisst, welche Teile des Ganzen müssen im Detail verstanden werden?
* **Aufwandschätzungen**. Grosse Systeme/Aufgaben als Summe einzelner überschaubarer Teile ansehen. Schätzungen werden einfacher.
* **Qualität sichern**. Einhalten von Design-Patterns oder sonstigen Vorgaben.

### Box-and-Arrows

Software-Architektur bedeutet in den meisten Fällen, den Aufbau eines Systems aus mehreren **Komponenten** (*Components*) und deren **Interaktionen** (*Interactions*) zu beschreiben. Die Abstraktion als Box lässt offen wie diese im Inneren genau funktioniert. Beziehungen zwischen Komponenten lassen sich illustrieren - welche verwendet, benötigt welche? Welche sind gänzlich unabhängig? Solche Diagramme repräsentieren in der Regel Teilbereiche aus einer bestimmten Sichtweise (*View*). Um die gesammte Architektur verstehen zu können müssen meist mehrere Sichten betrachtet werden.  

![alt-text](images/box-arrow.png)

#### Beziehungstypen

Neben den üblichen Pfeiltypen wie Inheritance, Implementing oder Beziehung existieren:

* **Aggregation** "ist Teil von"  
 
  ![alt-text](images/aggregation.png)
  
* **Composition** "besteht aus"

  ![alt-text](images/composition.png)

### Sichten (*Views*)

In der Software-Architektur haben sich folgende Sichten etabliert.  
![alt-text](images/view-model.png)

#### Development View

Klassen sind Artefakte welche in der Regel durch einen Entwickler hergestellt werden. Daraus entstehende Diagramme (*Klassendiagramme*) gehören deswegen zur Development View.

* .class Files zur erstellung von Objekten
* Source-Dateien die durch den Entwickler hergestellt wurden

#### Logical View

Die Logical View beschäftigt sich mit den zur Laufzeit existierenden Strukturen. In der objektorientierten Programmierung wären dies Objekte. Betrachten man sehr kleine Systeme, so wären Objekte die Komponenten. Beziehungen zwischen diesen Objekten sind die Abhängigkeiten sowie der gegenseitige Aufruf von Operationen.

* Ein Software-System soll eine bestimmte Wirkung erzielen.
* Diese entsteht durch das Verhalten von Objekten und deren Interaktion.
* Der Computer selber enthält eine Objekt-Fabrik (*ClassLoader*) mit welchem neue Instanzen zur Laufzeit erstellt werden.

#### Low Representational Gap (LRG)

Die Kluft zwischen der Darstellung realer Dinge soll über alle Representations-Schichten möglichst minimal gehalten weren. Das *LRG* verlangt also im ersten Schritt die reale Welt in einem objektorientierten Modell abzubilden. Das entstandene Modell wird danach bestmöglich 1:1 in Software übertragen. Folgende Vorteile entstehen:

* Objekte und deren Zustände entsprechen möglichst realen Dingen
* Letztlich gibt es nur ein minimales Gap zwischen Real und Software
* Strukturen können einfacher verstanden werden (neue Mitarbeiter) 

### Domain Driven Design (DDD)

Ist eine Arbeitsmethode um unter anderem das Ziel des *LRG* zu erreichen. Der Entwurf ist getrieben durch die Anwendungs-Domäne. Reale Dinge werden als *Entitäten* erfasst, sammt deren Eigenschaften und Abhängigkeiten. Entitäten bilden dann unmittelbar *Komponenten* die sich in Software abbilden lassen.

#### Operationen Logical View

Fast jedes System benötigt bestimmte Abläufe zwischen dessen *Komponenten* um überhaupt funktionieren zu können. Pro *Komponente* könnte jede Operation gelistet werden die sinvoll erscheint bzw. grade einfällt. Dieses vorgehen wäre **Entitäten getrieben**, würde jedoch nur für sehr einfache Systeme Sinn machen bzw. nutzbar sein. Bei komplexen Systemen ist es wesentlich sinvoller nur jene Operationen zu definieren welche auch für das ausführen bestimmter Szenarien (**Szenarien getrieben**) notwendig sind.

#### Linguistisches Vorgehensmodell

Mit folgender Methode können Szenarien zur DDD-Modellen abgebildet werden. Dieses sollte aber sehr **vorsichtig** angewendet werden, Ausnahmen immer möglich!

* Nach Nomen suchen, Objekte daraus bilden
* Nach Verben suchen, Operationen daraus bilden

#### Communication Diagrams

UML Darstellungsmöglichkeit für ein sogn. Kommunikationsdiagram.  
**Tipp**: Szenario Nummer (z.B. 5.2) jeweils notieren.

![alt-text](images/communication-diagram.png)

## Entwurf in Arbeitsteilung umsetzen

#### Objektorientierte Analyse (OOA)

Analyse sowie modellierung der realen Welt (DDD / LRG) zur Analyse der notwentigen Objekte. Aus dieser OOA wird das OOD entwickelt.

#### Objektorientiertes Design (OOD)

Im OOD werden zusätzlich Aufgaben betrachtet welche in der realen Welt eigentlich nicht vorkommen, für die Umsetzung der Software aber notwendig sind. Ziel ist in der Logical View zu verstehen, welche Objekte zur Laufzeit der Software die relevante Wirkung erzeugen und wie diese Objekte dafür zusammenarbeiten.

#### Von Objekten zu Klassen (Development View)

Aus den Objekten der Logical View können die benötigten Klassen abgeleitet werden. Beziehungen benötigen dabei Instanzvariabeln, Interaktionen öffentliche Methoden. Ziel ist die gerade benötigten Klassen zu implementieren welche für das Szenario nötig sind - die Development View enthält nur jene Klassen die auch Architektur-relevant sind (z.B. Klassen hinter einer Facade/Factory nicht relevant).

#### Methodisches Vorgehen

1. Liste aller zu programmierenden Klassen erstellen, so dass:  
	- jedes Objekt von genau einer Klasse instanziert werden kann
	- gleichartige Objekte mit identischem Verhalten von derselben Klasse instanziert werden
	- jede Klasse mind. eines der benötigen Objekte instanziert.  
	**=> Objekte den Klassen zuordnen**
	
2. Für jeden eingehenden Pfeil, welcher eine Interaktion darstellt, wird eine entsprechende public Methode vorgesehen.  
	**Ergebnis:** vollständige Methoden-Signatur inkl. Rückgabewert und Parametern sowie zusätzlichen Informationen zum Verhalten.
	
3. Die so erstellten Grundgerüste können nun unabhängig ausprogrammiert und anschliessend zusammengefügt werden.
	