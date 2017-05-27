# Reactive Domain Driven Design
## Talks
- "Reactive Domain Driven Design", Jochen Marder

## Content
- fundamentals DDD see workshop / content for software engineering course
- Akka + Vertx = Frameworks for DDD
- reactive manifest
    - responsive: zu jedem Zeitpunkt muss Anwendung erreichbar sein. Man muss damit leben, dass Teile der Anwendung nicht da sind und Requests nicht zurück kommen.
    - responsive = 
        - elastic -> Lastspitzen abfedern
        - resilience -> Damit umgehen können, dass Dinge ausfallen können (siehe oben)
 - Buch "Release It" hat das alles schon früh beschrieben => nochmal lesen
 - elastic + resilient durch message-driven erreichbar, nicht direkt irgendwelche Methoden aufrufen
 - Event = etwas, auf das man sich registrieren und horchen kann != Message-Driven (= Verarbeiter entscheidet, ob und wann etwas verarbeitet wird) => Unterschied noch nicht klar, belesen.
 - message driven unterbricht synch call chains = das, was ich als "normaler Java Entwickler" verstehe, z.B. 5 synchrone Aufrufe hintereinander, die jeweils fehlschlagen können
 - System.out.println ist blockierend => deshalb lähmen viele Log-Einträge Performance
 
### Vertx
- Einzelknoten-Fall ist der Sonderfall
- immer davon ausgehen, dass jeder Call zu einem anderen Knoten geht und nicht zurückkommt
- Verticle = 1 Knoten = kleinste Einheit
- Verticles reden (ausschließlich!) über Event-Bus (durch Kopieren von Objekten)
- Verbindung zu DDD: Handler == Aggregat

## Tasks
- organize slides
- Idee: UI, in der man per Clik Vertickles "abschießen" kann
