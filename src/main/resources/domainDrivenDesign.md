# Domain-Driven Design
## Talks
- "It's all about the domain, honey!", Carola Lilienthal, March 29th at ten, [slides](https://de.slideshare.net/cairolali/its-all-about-the-domain-honey)


## Content
### Subject-matter knowledge is the most important
- software is not a self purpose
- software is a mean to an end
- important question: for whom am I writing this piece of software?
- software is a reflection of a domain, thus you have to understand its concepts and transfer them into piece of software
- create a graphical model of the domain with entities and their relations

### Using Ubiquitous Language makes teamwork better
- the use of common language is important to express software, models etc.
- use the terminology of your customer in every possible way to avoid misunderstandings
- Ubiquitous Language is a process
    - it takes time to work out the key concepts and fitting terms
    - try to get employees of different involved departments together when working on common language 
    - you should experiment with alternative terms to develop the terminology
    - Ubiquitous Language changes and refines over time
- code needs permanent refactoring to fit Ubiquitous Language
- use a glossary

### Bounded Context is a central pattern in DDD
- entire domain is typically too big for one model, therefore it's split into separated models
    - every separated model should be small enough to assign it to a single team
    - these models are called "Bounded Contexts"
- every model has a context in which terms have a certain meaning
    - even simple terms like "customer" may be treated slightly different in single contexts
- every model has explicit boundaries
    - for example regarding the organisation of teams or the development of database schemas
    - it's like living in a box
    - however Bounded Contexts may affect each other
- examples for Bounded Contexts:
    - sales context
    - support context