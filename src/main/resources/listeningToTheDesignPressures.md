# Listening to the design pressures
## Talks
- "Listening to the design pressures", Martin Thompson (Real Logic) ([slides](https://www.doag.org/formes/pubfiles/8918470/docs/Events/2017/JavaLand%202017%20(28.03.2017)/vortraege/Architektur%20&%20Sicherheit/2017-ASEC-_-Keynote__Listening_to_the_Design_Pressures-Praesentation.pdf))

## content
- Quality attributes: 
    1. Execution (Service): security, performance, usability
    2. Evolution (Adaptability): testability, extensibility, maintainability
- in 2040 power usage of computation parks higher than power "production" of whole earth => performance matters!
- 2-3% of processing time for business logic, rest for infrastructure that has nothing to do with the real problem
- concurrency great for optimizing these problems, however bring additional complexity
- pipelines (sequential processing) better than concurrency because easier to understand, less "infrastructure pollution"
- hence: synchronous (hardware driver, desktop applications) vs asynchronous (everything web-related = "everything is request-response, everything can fail")
- "listen to your parents" / experts from the past. A lot of problems have been solved already, the solutions just have to be applied.
- "Do one thing at a time, and do it well. An interface should capture the minimum essentials of an abstraction."
- "put limitations to things": A bridge built for 20 people will fail if there used by significantly more than 20 people crossing it, so it's usage is limited. With software, the load will grow until crash. Why not put a limit to it?
- problem often seen: state change of object causes non-valid state of object. Bad! Same goes for methods: Don't change objects, then throw an exception and leave the objects in an invalid state. Either the method runs smoothly and produces valid states or it fails but changes nothing.
- "Resume driven development": picking up each latest cool framework
- observability: telemetry extremely underestimated in software. In Formula 1: real-time telemetry about every little detail of the car. However in most of our live systems just a couple of log statements, no "red button" that begins to flicker if something is starting to go wrong. Compared to the domain of Formula 1, we're flying blindly. "Observability" is an important quality metric. Logging simply isn't enough.
- structured vs unstructured data
- "Debugging is not taught at university" => how to use your IDE, how to read logs, how to create good logs, how to read a stacktrace, ...
- logging often serves multiple purposes:
    1. Errors
    1. Event Counts
    1. Business Journal
    1. Ad-hoc Debugging
- bad! Separate concerns:
    1. distinct error log with observation count, first and last timestamp, stacktrace on one simple, easy to reach and easy to read file / webpage / whatever
    1. counter-file like bytes send, bytes received, heartbeats received, ...
    1. business journal / audit trail / monitoring => frameworks can do that
    1. Ad-hoc debugging: [BTrace](https://github.com/btraceio/btrace)


## Tasks
- Steven: follow links to github repos and do something with it:
    - https://github.com/btraceio/btrace
    - https://github.com/real-logic/Aeron -> project with a lot of the mentioned techniques implemented - "Steal from it!"
- Add to software engineering course: "Debugging is not taught at university" => how to use your IDE, how to read logs, how to create good logs, how to read a stacktrace, ...