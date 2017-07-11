# Git Repository Analysis
## Talks
* "Shadow of the Past - Analysis of Git Repositories", Dirk Mahler, Tuesday 28th March, [slides](https://jqassistant.org/wp-content/uploads/2017/04/Shadows-Of-The-Past-Analysis-of-Git-Repositories.pdf), [code](https://rgra.github.io)

## Content

### Speakers Inspiration
- "Your code as a crime scene" by Adam Tornhill

### Git Analysis
- version control systems like Git are tools we use in out everyday life as developers, so it should contain a lot of useful information
- certain actions you do with Git can tell you a lot(!) about the project/repository:
    - very **high chance count** of a certain file can mean structural problems in a project
    - **file coupling** (files that are being committed together most of the time) can mean different kinds of duplication you have to synchronize manually
        - a new developer will certainly not know about that coupling
    - packages/files that are 90-100% changed/owned by only one person
        - **clarifying experts** and people you can talk to when you have a problem in that 
        - what if that person leaves the project? -> **risk management**!
    - take that further and define domains -> **Ownership of functional/technical domains**
        - src/main/.../model/ -> Model-Domain owned 94% by Paul
        - src/main/.../ui/ -> UI-Domain owned 88% by Peter
        - guess who the right person is when you have a problem with the UI?
        - or who to ask when you have a UI problem in another project that needs assistance?
    - or look at **file-types**
        - clarifying experts on certain technologies
    - how often files are removed
        - if half of your commits remove files from the project it can mean that **you often rewrite/redo work**? -> unstable project
    - explore **temporal correlations**
        - risks during different stages of a release cycle
    - and basically anything you can imaging with the data Git provides you with
    
### Tools
- [jQAssistant](https://github.com/buschmais/jqassistant)
    - Tool to extract and summarize different information from Projects
- [jQAssistant Git-Plugin](https://github.com/kontext-e/jqassistant-plugins/blob/master/git/src/main/asciidoc/git.adoc)
    - Plugin for jQAssistant to extract information from Git Repositories
- [Neo4j](https://neo4j.com/)
    - Graph Database used to store extracted information