# Grundlagen: Microservices

Der Begriff Microservice ist leider nicht einheitlich definiert, so
dass diese Broschüre zunächst Microservices und andere
grundlegenden Ideen darstellen muss.

## Independent-Systems-Architecture-Prinzipien (ISA) 

[ISA](http://isa-principles.org) (Independent Systems Architecture)
ist eine Sammlung von grundlegenden Prinzipien für Microservices. Sie
basiert auf Erfahrung mit Microservices in
vielen verschiedenen Projekten.

## Bedingungen

Bei den Prinzipien wird *"muss"* verwendet für Prinzipien, die unbedingt eingehalten werden
müssen. *"Sollte"* beschreibt Prinzipien, die viele Vorteile haben, aber
nicht unbedingt eingehalten werden müssen.

Die ISA-Prinzipien sprechen von einem *System*. Die IT-Landschaft
eines Unternehmens besteht aus vielen Systemen. Jedes System kann mit
einer anderen Architektur und daher mit anderen Prinzipien
implementiert sein.

## Prinzipien

1. Das System muss in *Module* unterteilt werden, die
*Schnittstellen* bieten. Der Zugriff auf andere Module ist nur über
diese Schnittstellen möglich. Module dürfen daher nicht direkt von den
Implementierungsdetails eines anderen Moduls abhängen wie z.B. dem
Datenmodellen in der Datenbank.

2. Module müssen *separate Prozesse, Container oder
virtuelle Maschinen* sein, um die Unabhängigkeit zu maximieren.

3. Das System muss zwei klar getrennte Ebenen von
Architekturentscheidungen haben:
   * Die *Makro-Architektur* umfasst Entscheidungen, die alle
   Module betreffen. Alle weiteren Prinzipien sind Teil der
   Makro-Architektur.
   * Die *Mikro-Architektur* sind jene Entscheidungen, die für
   jedes Modul anders getroffen werden können.

4. Die Wahl der *Integrations-Optionen* muss für das System begrenzt
und standardisiert sein. Die Integration kann mit synchroner oder
 asynchroner Kommunikation stattfinden und / oder auf Frontend-Ebene.

5. *Kommunikation* muss auf einige Protokolle wie REST oder
Messaging begrenzt sein. Auch Metadaten, z.B. zur Authentifizierung,
müssen standardisiert sein.

6. Jedes Modul muss seine *eigene unabhängige
Continuous-Delivery-Pipeline* haben. Tests sind Teil der
Continuous-Delivery-Pipeline, so dass die Tests der Module
unabhängig sein müssen.

7. *Betrieb* sollte standardisiert werden. Dies beinhaltet
Konfiguration, Deployment, Log-Analyse, Tracing, Monitoring und
Alarme. Es kann Ausnahmen vom Standard geben, wenn ein Modul sehr
spezifische Anforderungen hat.

8. *Standards* für Betrieb, Integration oder Kommunikation sollten auf
Schnittstellenebene definiert werden. Das Protokoll kann als REST
standardisiert sein, und Datenstrukturen können standardisiert
werden. Aber jedes Modul sollte frei sein, eine andere
REST-Bibliothek zu verwenden.

9. Module müssen *resilient* sein. Sie dürfen nicht ausfallen, wenn
andere Module nicht verfügbar sind oder Kommunikationsprobleme
auftreten. Sie müssen in der Lage sein, heruntergefahren zu werden,
ohne Daten oder Zustand zu verlieren. Es muss möglich sein, sie auf
andere Umgebungen (Server,  Netzwerke, Konfiguration usw.) zu
verschieben.

## Begründung

ISA zeigt, dass Microservices eine Art der Modularisierung sind
(Prinzip 1). Dadurch können Ideen wie
[Information Hiding](https://de.wikipedia.org/wiki/Datenkapselung_%28Programmierung%29)
oder High
[Cohesion](https://de.wikipedia.org/wiki/Koh%C3%A4sion_%28Informatik%29)
/ Low Coupling für Microservices übernommen werden. Neu ist bei
Microservices die Umsetzung als separate Container (Prinzip 2). Das
erlaubt mehr Freiheit bei der technischen Umsetzung der Module, die
jedoch mindestens so weit eingeschränkt werden muss, dass man noch von
einem Gesamtsystem sprechen kann (Prinzip 3). Also müssen Integration
(Prinzip 4) und Kommunikation (Prinzip 5) standardisiert sein, weil
das System sonst in mehrere Inseln zerfällt.

Unabhängiges Deployment ist ein Vorteil von Microservices und kann nur
mit eigener Continuous-Delivery-Pipeline sichergestellt werden
(Prinzip 6).

Die Standardisierung des Betriebs (Prinzip 7) erleichtert den Betrieb,
gerade bei einer großen Anzahl an Microservices. Aber die Standards
dürfen nicht die Technologie-Freiheit beschneiden und daher nur an der
Schnittstelle ansetzen (Prinzip 8). Ein Microservices-System wird
vielleicht nicht von Anfang an viele unterschiedliche Technologien
nutzen, aber man sollte sich die Möglichkeit dazu freihalten, um bei
der Weiterentwicklung besser aufgestellt zu sein.

Microservices sind ein verteiltes System. Das erhöht die
Wahrscheinlichkeit, dass ein Server, das Netzwerk oder ein
Microservice ausfällt. Daher ist Resilience (Prinzip 9)
unerlässlich. Außerdem können durch die Resilience Microservices auf
eine andere Umgebung verschoben werden, was für den Betrieb im Cluster
von Vorteil ist.

So ergeben die ISA-Prinzipien eine gute Grundlage für ein
Microservices-System.

Weitere Informationen, Links und eine ausführlichere Begründung finden
sich unter <http://isa-principles.org/>.

## Self-contained Systems

Die ISA-Prinzipien definieren wichtige Prinzipien für
Microservices, aber lassen bewusst Fragen offen wie beispielsweise die
Organisation, die fachliche Aufteilung oder ob Microservices eine UI
enthalten sollen oder nicht.

Self-contained Systems (SCS) sind ein Ansatz für Microservices, der
sich schon in vielen Projekten bewährt hat.  Alle wesentlichen
Informationen zu SCSs finden sich auf der Website
http://scs-architecture.org/ . Hier ein Überblick über die
Eigenschaften:

- Jedes SCS ist eine *autonome Web-Anwendung*. Der Code für die
  Darstellung der Web-Oberfläche ist in dem SCS enthalten. So kann
  ein SCS seine Funktionalitäten erbringen, ohne auf andere SCSs
  angewiesen zu sein.

- SCSs dürfen sich *keine UI teilen*. Schließlich soll ein SCS seine
  Features über seine eigene UI nutzbar machen.

- Ein SCS kann eine *optionale API* haben. Das ist aber nicht
  unbedingt notwendig, da das SCS bereits eine Web-Oberfläche für die
  Benutzer hat. Für mobile Clients oder andere SCSs kann der Zugriff
  über eine API aber nützlich sein.

- Das SCS enthält *Daten und Logik*. Ein Feature wird typischerweise
  Anpassungen in UI, Logik und Daten erfordern. Alle diese Änderungen
  können in einem SCS vorgenommen werden.

- Für ein SCS ist immer genau *ein Team* verantwortlich. Ein Team kann
  jedoch durchaus mehrere SCSs betreuen.

- Um eine enge Kopplung zu vermeiden, sollten SCSs sich *keinen
  fachlichen Code teilen*. Nur gemeinsamer technischer Code ist
  erlaubt. Als grobe Regel gilt: Nur Code, den man als Open Source
  veröffentlichen würde, darf zwischen SCS geteilt werden.

- Um die SCS weiter zu entkoppeln, sollten sich die SCS *keine
  Infrastruktur teilen*, also beispielsweise keine gemeinsame Datenbank
  nutzen. Aus Kostengründen können allerdings Kompromisse eingegangen
  werden.

- Die *Kommunikation* zwischen SCSs ist *priorisiert*:
  * Frontend-Integration hat die höchste Priorität.
  * Dann folgt asynchrone Kommunikation
  * und schließlich ist auch synchrone Kommunikation möglich.

    Dabei liegt der Fokus auf der Entkopplung und Resilience. Die
    höher priorisierten Kommunikationsarten helfen beim Erreichen
    dieser Ziele.

Die SCS-Idee hat sich in vielen Projekten schon bewährt. Die
[Links der Website](http://scs-architecture.org/links.html) geben
einen Eindruck von der Nutzung. Sie ist in Reinform nur für
Web-Anwendungen nutzbar, da zu jedem SCS eine Web-Oberfläche
gehört. Die konsequente Trennung in Systeme, die eine Fachlichkeit
implementieren und von einem Team entwickelt werden, ist aber auch für
andere Arten von Systemen sinnvoll.

## Fazit & Ausblick

Die Independent-Systems-Architecture (ISA) definiert die
Prinzipien, denen alle Microservice-Systeme entsprechen sollten,
während Self-contained Systems Best Practices definieren, die in
vielen Projekten erfolgreich eingesetzt worden sind.

Die weiteren Kapitel beschreiben technische Rezepte für die
Kommunikation zwischen Microservices und zwar in der Reihenfolge der
Prioritäten bei SCS: Frontend-Integration, asynchrone Kommunikation und
schließlich synchrone Kommunikation.
