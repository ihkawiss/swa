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

#### Beziehungstypen

Neben den üblichen Pfeiltypen wie Inheritance, Implementing oder Beziehung existieren:

* **Aggregation** "ist Teil von"
<img src="images/aggregation.png" height="50"/>
  
* **Composition** "besteht aus"
<img src="images/composition.png" height="50"/>

### Sichten (*Views*)

In der Software-Architektur haben sich folgende Sichten etabliert.  
<img src="images/view-model.png" height="180"/>

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

#### Learnings

- Paralleles Arbeiten ist deutlich schneller (time to market).
- Schnittstellen müssen genügend präzise definiert sein   
  **=>** Signatur, Parameter, Rückgabewerte, Naming, Verhalten (JavaDoc).
- Fehler in Klassen fallen erst bei Integration auf.
- Innerhalb der Klasse hat der Entwickler viel Freiheit (z.B. für Architektur nicht relevante Entscheide)
- Dokumentation der Architektur sowie dessen Verständnis helfen bei der Einarbeitung, um Code gezielt ändern zu können.

## SOLID Prinzipien

Folgende Entwurfsmuster haben zum Ziel - wartbare, flexible und verständliche Software zu produzieren.

#### Wiederverwendbarkeit

Die Entstehung von objektorientierten Programmiersprachen wie Java ist auf das Bedürfnis, die reale Welt abzubilden sowie Komponenten wieder zu verwenden (Änderbarkeit/Erweiterbarkeit), zurückzuführen. Es gibt verschiedene Arten wie Komponenten wiederverwendet werden können.

1. Vorhandene Klassen werden gemeinsam mit neuen Klassen verwendet.
2. Vorhandene Klassen werden verwendet um neue Objekte (z.B. neue Ausprägungen wie Buffet -> SuppenBuffet) zu instanzieren. 
3. Neue Klassen werden von vorhanden abgeleitet und überschreiben Notwendiges.

Die Möglichkeit des Erweiterns bzw. Anpassens kann jedoch schnell zu unübersichtlichen Systemen führen. Aus solchen Erfahrungen haben sich Entwurfsmuster entwickelt welche versuchen Chaos zu verhindern.

### Single Responsibility Principle

*Jede Klasse hat genau eine Verantwortung, d.h. nur eine Art von Änderungen in der Spezifikation soll die Klasse betreffen können.*

Ein Objekt bzw. eine Klasse welche mehr als eine Aufgabe übernimmt, muss immer dann angepasst werden, wenn eine der Aufgaben ändert. Hier besteht die Gefahr, dass sich Änderungen an einer Aufgabe aus Versehen auch auf einen anderen Aufgabenbereich auswirken. Speziell in Fällen, in welchen alte und neue Implementationen von Aufgaben weiter existieren, entstehen enorm viele mögliche Kombinationen. Sind Verantwortungen hingegen über mehrere Objekte/Klassen aufgeteilt, so stellt dies eine klare Abgrenzung der Zuständigkeit dar. Anpassungen an einer Aufgabe ändern so in der Regel auch nur das Verhalten der Zuständigen Klasse (grade mittels privater Sichtbarkeit von Ausprägungen).

**Verantwortungen notieren**  

Werden Verantwortungen eines Objekts beschrieben, immer klar und prägnant:

- **Kennt** *die Parameter der Simulation...*
- **Erzeugt** *das neue Objekt für den Fall xy...*
- **Koordiniert** *die Aktivierung sowie den Life-Cycle der Objekte xy...*
- **Speichert** *den aktuellen Status von xy...*
- **Steuert** *den Ablauf der in xy definierten Szenarien...*

**Hilfsfragen**

Folgende Fragen helfen zu entscheiden, ob eine Verantwortung als Einheit betrachtet oder besser aufgegliedert werden sollte.

- Wie gross ist die Chance, dass eine Lösung in einem Verantwortungsbereich in einem anderen (wieder-) verwendet wird?
- Wie wahrscheinlich/häufig treten Änderungen in den einzelnen Verantwortungen auf?
- Treten diese Änderungen unabhängig auf voneinander?
- Kann die Aufteilung in einer feineren Entwurfsstufe gemacht werden? (non-architectural design)

**Verwandte Prinzipien**

- Prinzip der hohen Kohäsion  
  Die von einem Objekt wahrgenommen Aufgaben sollen in engem Zusammenhang stehen.  
  
- Responsibillity-Driven Design (RDD)  
  Basierend auf einer Liste von Verantwortungen werden Objekte erstellt welche diese Wahrnehmen.  
  Ein solcher Entwurf ist also durch die Zuständigkeit getrieben.

#### Lehman's Law

Lehman untersuchte die Entwicklung von Software, speziell welche Kräfte neue Software voran treiben und welche diese bremsen.

- **S-TYPE**  
  Systeme welche bekannte Spezifikationen und dazugehörige Lösungen haben (z.B. Bubble Sort). 
  Richtigkeit des Systems lässt sich mit Sicherheit beurteilen.
  
- **P-TYPE**  
  Systeme welche zwar eine Spezifikation und womöglich eine theoretische Lösung besitzten, in der Praxis aber nicht so umgesetzt werden können.
  Korrektheit lässt sich nicht verifizieren. Beispiel: Schach Bot -> kombinatorische Komplexität zu hoch -> Heuristik.
  
- **E-TYPE**  
  "Real-World" Systeme, Business Systeme bei welchen die Spezifikationen vielleicht heute bekannt und richtig sind, morgen aber Andere sein können. Umgebung ändert sich, Bedürfnisse von Business und Personen ändern sich und sind nicht starr.
  
**Gesetzte**  

- Kontinuierliche Veränderung  
  Jede *real World* Software muss sich ändern oder wird weniger nützlich.
  
- Steigende Komplexität  
  Ein Softwaresystem wird mit voran schreitender Zeit komplexer. Mit hohen Kosten kann dies kurzfristig reduziert werden.
  
- Evolution grosser Anwendungen  
  Ist selbstregulierender Prozess. Messungen von Attributen, Zeit zwischen Releases, Fehlermeldungen etc. Liefern Indikatoren.
  
- Organisatorische Stabilität  
  Über die Lebenszeit einer Software gesehen ist der Entwicklungsaufwand ungefähr gleichbleibend.
  
- Beibehaltung der Ähnlichkeit  
  Über die Lebenszeit einer Software gesehen ist der inkrementelle Change je Release etwa konstant.
  
### Open / Closed Principle

*Klassen sollen offen für Änderungen des Verhaltens und zugleich geschlossen gegenüber Veränderun- gen am Code sein*

Gemäss dem Open / Closed Prinzip sollen bei Objekten Verhaltensänderungen möglich sein, ohne dass man ihren bestehenden Code anpassen - also bestehende Klassen nicht neu compilieren muss. So führt dieses Prinzip oft dazu, dass Fallunterscheidungen aufgelöst und mittels Vererbung gelöst werden. Mögliches Vorgehen:

- Aublauf in einer Methode festlegen, Aktivitäten in Methoden kapseln
- Nur die gewünschte Methode überschreiben, Ablauf bleibt gleich
- Ablauf überschreiben, Aktivitäten bleiben gleich
- Template Methods (leere Methoden die in Child überschrieben werden müssen)

**Grundsätzliche Regel**  

Methoden die nicht privat oder static sind sowie überschrieben werden können sollten:

- abstract oder
- final oder
- leer sein

### Liskov Substitution Principle

Das Prinzip sagt zusammengefasst aus, dass Subtypen einer Klasse keine breaking Changes einführen dürfen, so dass sich diese anders als deren Superklassen verhalten. Da Sub-Typen z.B. in Listen vom Super-Type gespeichert werden können gehen Anwender davon aus, dass sich diese Objekte auch gleich verhalten. Sie sollen also nich mehr erwarten und weniger liefern als Ihre Superklassen dies tun. So muss im Altag folgendes zur Erfüllung des Liskov Substitution Principle gegeben sein:

**Eine Unterklasse soll an die Stelle der Oberklasse treten können, ohne dass dabei Seiteneffekte auftreten.**

### Interface Segregation Principle

Das Prinzip sagt zusammengefasst aus, dass es besser ist viele Interfaces zu definieren als wenige. Konkret soll für jede von Objekten wahrzumenden Rollen ein Interface erstellt werden welches die nötigen Methoden definiert. Interfaces werde so zu Rollendefinitionen, das Implementieren dieser zur Aussage welche Rollen das Objekt wahrnimmt. Durch diese Trennung ist es z.B. einfach möglich einen PayingGuest der Kasse zu übergeben. Dem Buffet würde hingegen ein Guest vom Typ BuffetVisitingGuest übergeben. 

### Dependency Inversion Principle

Das Prinzip sagt zusammengefasst aus, dass man Variabeln und Parameter immer vom schwächst möglichen Typ definieren sollte, grade so dass keine Type-Casts notwendig sind. Hier gibt es einen Bezug auf das *Interface Segregation Principle*, eine Variable sollte mit genau den Rollen typisiert sein die ein ihr zugewiesenes Objekt haben muss. Der resultierende Code ist somit nicht von konkreten Objekten abhängig. Dieses Prinzip gilt auch für die Instanzierung von Objekten, welche wenn möglich von aussen eingefügt werden sollten (Dependecy Injection). Durch den Rollen-basierten Typ sind die Instanzen nicht an konkrete Implementierungen gebunden. Abstraktionen zur Schaffung von Unabhängigkeit sollten grundsätzlich mittels Interfaces und nicht abs- trakten Klassen als Typen formuliert werden.

## Teil 2

### Thread- vs. Event-Based Programmierung

Teil der Process-View ist die Planung sowie Darstellung nebenläufige Aktivitäten. Software-Systeme werden grade im ***RDD*** oft so geplant, dass der Fokus nicht auf eine feste Abfolge von Operationen gerichtig ist. Vielmehr steht die sinvolle Gruppierung von Objekten im Vordergrund. Damit aus den einzelnen Operationen eine nützbringende Teiloperation entsteht, müssen diese untereinander koordiniert werden. Diese Aufgabe kann an dedizierte Objekte übergeben werden (solange der Ablauf definierbar ist) - sogenannte Controller.  

**Controller früher:** Das Hauptprogramm, der Benutzer konnte lediglich reagieren.
**Controller heute:** Der Benutzer, das Programm reagiert auf dessen Eingaben/Signale.

#### Thread-Based

In der Thread-Based Programmierung wird ein Ablauf als feste Folge (übliche Kontrollstrukturen) von Einzelschritten programmiert. In einer Restaurant-Simmulation würde der Ablauf auf mehrere Threads verteilt, die gleichzeitig arbeiten. Dabei ist es nötig, Synchronizers sowie Warten zu implementieren - dies ist teuer und kann schnell zu Fehlern bzw. unerwünschten Interleavings führen. Thread basierte Programmierung kommen schnell an ihre Grenzen - Controller ausserhalb, Distributed Systems. Zwar sind Thread-Based Programme einfacher zu verstehen, können aber dennoch schnell unübersichtlich werden.

#### Event-Based

Grundmechanismus für die Event-Based Programmierung ist der Event Queue im Kernel (=> Java z.B. PriorityQueue<Node>(capacity, comparator)), welcher Events sequenziell abarbeitet. Durch diese Sequenzialisierung entfallen Mutex-Konstrukte sowie das damit zusammenhängende Fehlerpotential. Die Implementierung einer solchen Event Queue erfolgt nach dem Command Pattern. Ein Event wird also als Command-Objekt realisiert und kennt seine Routine (z.B. Event.handle()) welche auf kurze und atomare Operationen setzt anstatt nebenläufigen Threads.

```java
	private static Queue<Node> queue = new PriorityQueue<Node>();
	...
	public static
		while (!queue.isEmpty()) {
			Node n = queue.poll();
			if (now > n.dueTime) throw new IllegalStateException(); now = n.dueTime;
			n.event.handle(now);
	} }
	...
	private void welcomeGuest() {
		active = true;
		final CounterVisitingGuest g = q.getFirst(); EventQueue.schedule(new Event() {
			@Override
			public void handle(int time) { g.takePlate();
				if (q.length() > 0) welcomeGuest(); else active = false;
			}
		}, serviceDuration);
	}
```

### Modulare Programmierung

In komplexen Softwaresystemen ist die Anzahl Komponenten gross, die Architektur entsprechend unübersichtlich. Objekte bzw. Klassen sind die atomaren Grundpfeiler der objektorientierten Programmierung. Sie haben eine Identität und sind technisch in Speicherblöcken abgebildet. Damit Software-Systeme sinvoll gebaut werden können, ist es nötig Komponenten in Module gruppieren zu können. Module sind Einheiten die erlauben von inneren Details zu abstrahieren sowie diese zu verstecken - ohne dass andere Module betroffen sind.

#### Möglichkeiten
- Module im inneren überarbeiten, ohne das andere Module betroffen sind bzw. etwas mitbekommen.
- Module wiederverwenden in verschiedenen Systemen.
- Integrität der Kombination von Klassen sichern.
- Die einzelnen Module in Arbeitsteilung entwickeln.
- Zusätzliche Erweiterungen einfach möglich.
- Modulare Anforderungen/Produktlinie realisieren.
- Code Basis gliedern und Abhängigkeiten einschränken.

#### JAR Files

In Java können mittels JAR-Files Module gebildet und kombiniert werden. Eine Kombination wird gebildet, indem die benötigten JARs auf den ***Class Path*** gelegt werden. Benötigte Klassen werden durch den ***Class Loader*** dann in diesem gesucht. Dieses Gebilde führt jedoch zu einem grösseren Problem: **Klassen mit selbem Namen (FQN) können vorkommen, es wird jeweils jene Instanziert welche zuerst auf dem Class Path liegt.** Dies Führt dazu, dass verschiedene Kombinationen zu unterschiedlichem Verhalten führen können. Hinzu kommt, dass Information Hiding dadurch ebenso unzuverlässig wird (package private).

#### Sealed JARs

Bei grösseren Kombinationen wird es also praktisch unmöglich, den Class Path korrekt zu konfigurieren (Fehler nicht bekannt). Eine Abhilfe schaffen hier sogn. ***Sealed JARs***. Hierbei würde eine Exception geworfen, wenn mehrere JARs einen identischen Package-Namen enthalten. Dieser Mechanismus wird jedoch erst beim Kompillieren geprüft, also sehr spät im Entwicklungsprozess.

#### Java9 Module & ServiceLoader

Mit Java 9 können Module so definiert werden, dass exportierte **(Architektur)** und interne Klassen (irrelevant für Architektur) unterschieden werden. JARs werden hier ebenso wie Sealed JARs behandelt => Package-Namen müssen sich unterscheiden!   
Der Java ServiceLoader ermöglicht Implementationen zu injecten von bekannten Interfaces (entkopplung Module).

``` Java
module ch.fhnw.swa.mod.sim.basic {
	exports ch.fhnw.swa.mod.sim.eventbase; exports ch.fhnw.swa.mod.sim;
	exports ch.fhnw.swa.mod.sim.roles.restaurant; exports ch.fhnw.swa.mod.sim.roles.guests;
	requires transitive ch.fhnw.swa.mod.xyz;
}

module service.framework { 
	exports service.framework;
	uses service.framework.Service; // DI im framework mittels ServiceLoader.load(Service.class); 
}

module service.impl1 {
	requires service.framework;
	provides service.framework.Service with service.impl1.ServiceImpl;
}
```

### Modularer Entwurf

In der Software-Architektur sind Module (JARs, DLLs, SO, usw.) eine Gliederungseinheit - also Architektur-Komponenten. Module als Komponenten ermöglichen also, Systeme später einfacher anzupassen (Änderung, Varianten). Sie können als ganzes ausgetauscht, entfernt oder hinzugefügt werden. Zentrales Element hier ist das ***Information Hiding*** (package visibility, module discriptor).

#### Eigenschaften von Modulen

**Unit of Abstraction**  
Ein Modul abstrahiert mittels Information Hiding die Details seiner Implementierung. Es genügt, seine Schnittstelle zu verstehen.

**Unit of Analysis**  
Entwickler eines Moduls kennen dessen Implementierung und können Eigenschaften analysieren bzw. beurteilen. Information Hiding schliesst Einwirkungen Programmierer anderer Module aus.

**Unit of Compilation**  
Schützt Unit of Abstraction und Unit of Analysis mittels technischer Mittel. Alle Teile des Moduls müssen vorhanden sein und auf Konsistenz geprüft werden können. Kompilat ist ein vollständiges in sich zusammengehöriges Packet für dieses Modul.

**Unit of Delivery**  
Module werden immer als ein Ganzes ausgeliefert, nicht in einzelteilen. Die Auslieferung eines Moduls sollte immer Sinvoll sein (keine zwingende Kombinationen, sinvolle Konstellationen). Auch kommerzielle Punkte möglich - Lizenzen, Preis.

**Unit of Installation**  
Welche Komponenten (Module) werden zur Laufzeit verwendet? Speziell auch welche Version installiert wird -> sicherstellen von Unit of Abstraction und Analysis.

**Unit of Loading**  
Objekt-Strukturen sollen zur Laufzeit konsistent erstellt werden, so dass diese mit Erkenntnissen aus Unit of Analysis übereinstimmen. Es muss sichergestellt werden, dass genau dieselben Executables gemeinsam verwendet werden die auch der Compiler erzeugt hatte. Dieses letzte Glied soll sicherstellen, dass sich das System so verhält wie es vom Entwickler geplant wurde.

#### Methodisches Vorgehen

**1. Welche Module gibt es?**  
Zuerst muss geklärt werden, welche Module benötigt werden. Als Entwurfsmethode eignet sich RDD.

Entscheidungen kapseln nach **Parnas** (welche Notwendigkeiten für Änderungen werden erwartet?):

1. Liste erstellen, von Entwurfsentscheidungen, die schwer zu treffen sind oder man spätere Änderungen erwartet.
2. Für jede der notierten Entscheidungen soll ein Modul geplant werden.

**Scenario-based Software Engineering**  
Änderungs Szenarios beschreiben, die zu Änderungen von Anforderungen das System führen und eine Antwort der Entwickler benötigt.

**2. Welche Module sind von anderen abhängig?**  
Wenn ein Modul A von einem Modul B abhängig ist, heisst dass, dass mind. der öffentliche Teil vom Modul B vorhanden sein muss, damit A programmiert werden kann. Ansonsten kann A nicht verstanden noch kompiliert werden.

- Module dürfen nicht gegenseitig abhängig sein (A <=> B)
- Module dürfen nicht zyklisch Abhängig sein (A => B => C => A)
- Module dürfen nicht von noch nicht existierenden Modulen abhängig sein
- Module dürfen nicht von "geheimen" Modulen abhängig sein

**3. Wie genau arbeiten die Module zusammen?**  
Es muss überlegt werden, wie die Zusammenarbeit der Module aussehen muss, damit das resultierende System die Aufgaben erfüllen kann. Am besten kann dies mittels konkreter Szenarien beurteilt werden (spezifische Use Cases). Um darzustellen, welche Informationen zwischen den Modulen im Szenario ausgetauscht werden, eignet sich ein Sequenz-Diagramm. **Die Akteure sind jeweils die Module selbst!**

***Wichtig:   
Ein erstes Diagramm kann zwischen den Modulen gezeichnet werden. In einem zweiten Schritt muss dies aber so verfeinert werden, dass Module nur auf Objekte gerichtet Aktionen ausführen können (z.B. DAO, statische exportierte Klasse, usw.).***

**4. Wie kann das System gestartet werden?**
Module sind Komponenten der Development View. Es muss also definiert werden, wie Beziehungen zwischen Modulen etabliert werden können.

Es wird grundsätzlich zwischen 2 Fällen unterschieden:

1. Eine Klasse X im Modul A benötigt eine Klasse Y im Modul B. Klasse A.X importiert also Klasse B.Y.
	- B exportiert Y, A kann Y instanzieren mit ```new Y()```	- B exportiert eine Facotry für ```? implements IY```, A kann mit der Factory ein Y erzeugen. Factory muss bekannt sein
	
2. Eine Klasse X im Modul A benötigt eine Klasse Y im Modul B. Klasse A.X importiert aber B nicht!
	- Benötigte Beziehung muss zur Laufzeit etabliert werden (Dependency Injection)
	- Lösen mittels ServiceDescriptors und ServiceLoader von Java 9 Modulen

**5. Wie sehen die Schnittstellen der Module aus?**  
Aus den Schritte 1 bis 4 kann man ableiten, wie die Schnittstellen der Module gestaltet werden müssen. Jedes Modul muss darin die Klassen/Interfaces enthalten, welche im Schritt 3 und 4 von anderen Modulen benötigt werden.

### Schnittstellen

Module in einem System müssen gegenseitig interagieren können, hierzu ist es nötig Schnittstellen zu definieren. Damit Module z.B. in Arbeitsteilung entwickelt werden können, müssen diese Schnittstellen möglichst früh und detailliert definiert werden. Also wie die Kommunikation funktioniert (z.B. REST) aber auch welche Parameter, Rückgabewerte, Vor und Nachbedingungen gelten sollen.

**Was gehört zu einer Schnittstelle?** => alles was von aussen sichtbar ist!

Eine Schnittstelle kann also so definiert werden:  
- Der Ort, an dem zwei Module auseinandergeschnitten werden.
- Die Schnittmenge dessen, wass Modul A und Modul B voneinander wissen müssen um funktionieren zu können.

**Definition einer Schnittstelle**
Eine Schnittstelle muss auf drei Ebenenen definiert werden, so dass diese verstanden werden kann.

1. **Verbindungs-Technologie**: Wie werden die Operationen aktiviert, Parameter und Resultat übergeben?
2. **Syntax-Ebene**: Wie wird die Operation identifiziert, wie die Parameter?
3. **Semantik-Ebene**: Was bedeuten die Parameter und Resultate genau?

**In welchen Komponenten (Modulen) sind Schnittstellen definiert?**

1. **Angebotene Schnittstelle**: Die Schnittstelle wird von der Komponente Angeboten, welche auch die Funktionalität dafür implementiert. Beispiel: Library.
2. **Angeforderte Schnittstelle**: Eine Implementierung zur Schnittstelle wird von der Komponente angefordert, die auch die Schnittstelle definiert. Beispiel: Plug-In, Erweiterungsschnittstelle
3. **Standard Schnittstelle**: Die Schnittstelle wird in einer seperaten Komponente geführt, unabhängig von Aufrufer und Implementierer. Beispiel: JEE API

### Component Frameworks
Eine Standard-Schnittstelle ist die Basis für offene Systeme, so dass Software-Hersteller Komponenten bauen können ohne über weitere Lieferanten etwas wissen zu müssen. Weitere Personen können dann schlussendlich aus den Komponenten ein lauffähiges System bilden. Kostengünstig funktioniert dies jedoch nur dann, wenn die Komponenten auch die Spezifikation einhalten, da sie sonst zu viele Freiheiten hätten. Hier hilft es, die Standard-Schnittstelle mit minimaler Funktionalität auszustatten, die die Einhaltung der Standard-Schnittstelle sicherstellt. Dies wird **Component Framework** genannt.

Werden Schnittstellen zwischen Komponenten gebildet, so kann es passieren, dass die Komponent A mit Komponent B einwandfrei funktioniert, jedoch Komponent A mit Komponent C zu falschem Verhalten führt. Dies, da sich nicht alle Komponenten an die Spezifikation der Standard-Schnittstelle gehalten haben.

**Beispiel**
Die Klasse Visualizer sollte ein erhaltenes Array nicht verändern, da dieses schon durch den Algorithmus gemacht wurde.
VisualizerA hält sich an diese Spezifikation, die Daten werden korrekt angezeigt.
VisualizerB hält sich nicht an diese Spezifikation und verändert das Array (swap) bevor es gezeichnet wird.

**Methode zum Schnittstellenentwurf**  
1. Schreiben Sie eine einfache Standardschnittstelle auf
2. Erfinden Sie eine fehlerhalte Implementierung
3. Überarbeiten Sie die Standardschnittele so, dass diese Impl unmöglich wird.
4. Wiederholen Sie den Prozess ab 2.

Schnittstellen können also einen kleinen Anteil an ausführbarem Code enthalten, welcher die Einhaltung der Spezifikation erzwingt. Diese Anweisungen sind Teil des Vertrags, zwischen Hersteller und Lieferant und dürfen nicht einfach verändert werden. Konkret kann dies z.B. mit einer Komponente Framework gelöst werden.