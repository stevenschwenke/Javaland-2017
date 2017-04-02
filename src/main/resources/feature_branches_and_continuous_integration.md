#Feature branches and continuous integration
##Talks
* "Müssen sich Feature-Branches und Continuous Integration widersprechen?", Steffen Schluff, Sebastian Damm. Charts should appear [here](http://www.oio.de/public/presentations/) but aren't yet.

##TL;DR
TODO Write a summary

##Continuous Integration
- term first used by Martin Fowler in 2000 (TODO Read that article)
- integrate every feature branch at least once a day into main line (if you use Gitflow, that would be develop)
- suggestion: "keep the number of your branches to a minimum", this suggestion is not up to date. Git was developed to make branching easier and there are a wide variety of tools out there to work effectively with branches.
- Martin Fowler 2009 new article to bring branching and CI together. However, he claims that feature branches don't work well with CI. Instead, he suggests using feature toggles. (TODO Read that article) (TODO specify feature toggles, maybe in another chapter. Important for software engineering course)
- alternative to feature toggles: Branch by abstraction: insert new abstraction layer to switch between new and old version
- slide 10: Checkin only possible after integration of baseline into own feature branch + green tests
- slide 17: feature branches and CI seem to be impossible to achieve together

##Modern solution
- slide 20: changes in mainline should be integrated ASAP in feature branches. Best case: every commit.
- slide 23: live demo with Atlassian Bamboo
- in Branch-config activate "Branch Updater"
- changes in mainline will be merged automatically into feature branch
- build: "Branch Integration Details"-pane
- automatically merged commits can be pulled from server. Named "Bamboo automatic branch merge".

##Advantages modules vs monolith


##Tasks
- Steven: research how Git history will look like if develop is merged into feature branches. Maybe squashing helps? Then in current project: "Integrate develop more often into feature branches!".
- Steven: in current project use Bamboo Branch Updater
- Steven: in current project create feature branches directly from JIRA, not via Git client => no typo possible + good naming conventions of feature-branches + no "rogue" feature branches ("We don't have a story for that but it's a good idea, that's why I'll code that into this new branch."). Write a separate article for that!
- Steven: in current project use branch updater to force a conflict. What happens?

- Steven organize migrating all knowledge from here to other places (workshops, articles, talks, ...). Goal is to delete this repository and all its contents.