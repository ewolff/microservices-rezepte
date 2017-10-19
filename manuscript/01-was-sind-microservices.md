# Was sind Microservices?

Der Begriff Microservice ist leider nicht einheitlich definiert, so dass eine

## Independent Systems Architecture (ISA) Principles

ISA (Independent Systems Architecture) ist eine Sammlung von Best Practices, die
in vielen verschiedenen Fällen sehr gut arbeiten. Es basiert auf
Erfahrung insbesondere mit Microservices und
[In sich geschlossene Systeme] (http://scs-architecture.org) und die
Herausforderungen in diesen Projekten.

## Bedingungen

Die Prinzipien verwenden * "muss" * für
Prinzipien, die nicht beeinträchtigt werden können und in der
System. * "Sollte" * Prinzipien umfassen, die viele Vorteile haben, aber
in einigen Fällen ausgelassen. Die hier beschriebenen Prinzipien sprechen von einem
System. Normalerweise enthält die IT-Landschaft eines Unternehmens viele
Systeme. Jedes System könnte mit einem anderen Prinzip aufgebaut sein
oder vielleicht sogar einen völlig anderen Ansatz.

## Prinzipien

1. Das System muss in * Module * unterteilt werden, die
    * Schnittstellen *. Der Zugriff auf andere Module ist nur über diese möglich
Schnittstellen. Module dürfen daher nicht direkt von den internen Daten abhängen
Darstellung eines anderen Moduls, z.B. in einer Datenbank. Der Rest von
Die Prinzipien definieren, wie
Module könnten implementiert werden und wie sie sich von anderen unterscheiden
Modularisierungsansätze.
   
2. Module sollten als * separate Prozesse, Container oder
    virtuelle Maschinen *, um die Unabhängigkeit zu maximieren.

3. Das System muss zwei klar getrennte Ebenen von Architekturentscheidungen haben:
   a) Die * Makro-Architektur * umfasst Entscheidungen, die alle
   Module. Alle weiteren Prinzipien sind Teil des Makro
   Die Architektur.
   b) Die * Micro Architecture * berücksichtigt Entscheidungen, die getroffen werden können
   individuell für jedes Modul.
   
4. Die Wahl der Optionen * integration * muss begrenzt und standardisiert werden
   für das System. Die Integration kann mit synchronen oder
   asynchrone Kommunikation und / oder auf der UI-Ebene.
   
5. * Kommunikation * muss eine begrenzte Anzahl von Protokollen wie REST oder
   Messaging. Auch Metadaten, z. zur Genehmigung muss
   standardisiert. Es könnte sinnvoll sein, für jedes Protokoll nur ein Protokoll zu verwenden.
   Integrationsoption.
   
6. Jedes Modul muss seine eigene * unabhängige kontinuierliche Lieferung haben
   Pipeline*. Tests sind Teil der Continuous-Delivery-Pipeline, so dass
   Module müssen unabhängig getestet werden.
   
7. * Operationen * sollten standardisiert werden. Dies beinhaltet Konfiguration,
   Bereitstellung, Protokollanalyse, Ablaufverfolgung, Überwachung und Alarmierung. Es könnte geben
   Ausnahmen vom Standard, wenn ein Modul sehr spezifisch ist.
   Anforderungen.
   
8. * Standards * für Operationen, Integration oder Kommunikation sollten
   erzwungen auf der Schnittstellenebene. I.e. das Protokoll kann
   standardisierte REST- und Datenstrukturen können standardisiert werden. Aber
   Jedes Modul sollte frei sein, eine andere REST-Bibliothek / Implementierung zu verwenden.
   
9. Module müssen * widerstandsfähig sein *. Sie müssen nicht verfügbar sein
   Module oder Kommunikationsprobleme. Sie müssen in der Lage sein, mit
   unerwartete Stillstände, ohne Daten oder Zustand zu verlieren. Es muss sein
   möglich, sie in andere Laufzeitumgebungen zu verschieben (Hosts,
   Netzwerke, Konfiguration usw.).


## Self-contained Systems
