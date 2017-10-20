# Was sind Microservices?

Der Begriff Microservice ist leider nicht einheitlich definiert, so dass eine

## Independent Systems Architecture (ISA) Principles

[ISA](http://isa-principles.org) (Independent Systems Architecture)
ist eine Sammlung von Best Practices, die in vielen Projekten sehr gut
funktioniert haben. Es basiert auf Erfahrung insbesondere mit
Microservices und den Herausforderungen in Microservice-Projekten.

## Bedingungen

Die Prinzipien verwenden *muss* für Prinzipien, die unbedingt eingehalten werden
müssen. *Sollte* beschreibt Prinzipien, die viele Vorteile haben, aber
nicht unbedingt eingehalten werden müssen.

Die ISA-Prinzipien sprechen von einem *System*.  Die IT-Landschaft
eines Unternehmens besteht aus vielen Systemen. Jedes System kann mit
einer anderen Architektur und daher mit anderen Prinzipien
implementiert sein.

## Prinzipien

1. Das System muss in *Module* unterteilt werden, die
*Schnittstellen* bieten. Der Zugriff auf andere Module ist nur über
diese Schnittstellen möglich. Module dürfen daher nicht direkt von den
internen Datenmodellen eines anderen Moduls z.B. in
der Datenbank abhängen.

2. Module sollten *separate Prozesse, Container oder
virtuelle Maschinen*, um die Unabhängigkeit zu maximieren.

3. Das System muss zwei klar getrennte Ebenen von
Architekturentscheidungen haben:
   * Die *Makro-Architektur* umfasst Entscheidungen, die alle
   Module betreffen. Alle weiteren Prinzipien sind Teil der
   Makro-Architektur.
   * Die *Mikro-Architecture* sind jene Entscheidungen, die für
  jedes Modul anders getroffen werden können.

4. Die Wahl der *Integrations-Optionen* muss für das System begrenzt
und standardisiert sein.  Die Integration kann mit synchronen oder
 asynchrone Kommunikation stattfinden und / oder auf UI-Ebene.

5. *Kommunikation* muss auf eine einige Protokollen wie REST oder
Messaging begrenzt sein. Auch Metadaten, z.B. zur Authentifizierung
müssen standardisiert sein.

6. Jedes Modul muss seine *eigene unabhängige
Continuous-Delivery-Pipeline* haben. Tests sind Teil der
Continuous-Delivery-Pipeline, so dass die Tests der Module
unabhängig sein müssen.

7. *Betrieb* sollte standardisiert werden. Dies beinhaltet
Konfiguration, Deployment, Log-Analyse, Tracing, Monitoring und
Alarme. Es kann Ausnahmen vom Standard geben, wenn ein Modul sehr
spezifische Anforderungen hat.

8. *Standards* für Betrieb, Integration oder Kommunikation sollte auf
Schnittstellenebene definiert werden. Das Protokoll kann als REST
standardisiert sein und Datenstrukturen können standardisiert
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
jedoch mindestens soweit eingeschränkt werden muss, dass man noch von
einem Gesamtsystem sprechen kann (Prinzip 3). Also müssen Integration
(Prinzip 4) und Kommunikation (Prinzip 5) standardisiert sein, weil
das System sonst in mehrere Inseln zerfällt.

Unabhängiges Deployment ist ein Vorteil von Microservices und kann nur
mit eigener Continuous-Delivery-Pipeline sichergestellt werden
(Prinzip 6).

Die Standardisierung des Betriebs (Prinzip 7) erleichtert den Betrieb,
gerade bei einer großen Anzahl an Microservices. Aber die Standards
dürfen nicht die Technologie-Freiheit beschneiden und daher nur an der
Schnittstelle ansetzten (Prinzip 8). Ein Microservices-System wird
vielleicht nicht von Anfang an viele unterschiedliche Technologien
nutzen, aber man sollte sich die Möglichkeit dazu freihalten, um bei
der Weiterentwicklung besser aufgestellt zu sein.

Microservices sind ein verteiltes System. Das erhöht die
Wahrscheinlichkeit, dass ein Server, das Netzwerk oder ein
Microservices ausfällt. Daher ist Resilience (Prinzip 9)
unerlässlich. Außerdem können durch die Resilience Microservices auf
eine andere Umgebung verschoben werden, was für den Betrieb im Cluster
von Vorteil ist.

So ergeben die ISA-Prinzipien eine gute Grundlage für ein
Microservices-System.

Weitere Informationen, Links und eine ausführlichere Begründung finden
sich unter <http://isa-principles.org/>.

## Self-contained Systems
