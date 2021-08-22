# Optimizing pytest runtime

In all these years as a software developer I have experienced that the throughput of any task in any piece of software is paramount for customers. If the software that you ship cannot scale and meet the necessary customer requirements, then there are chances that you might eventually loose that customer. Time and again as software developers we work on scaling the software better to satify such customer demands. But as software developers do invest enough time and thought to run our tests faster?

Writing tests is a mandatory requirement for all software developers. As developers we are expected write good tests which are robust, less brittle (less likely to break) and provide good code coverage. But do we think that our tests should run faster? Why should tests run faster anyways? If you haven't thought about these questions then probably slower tests haven't frustrated you as much as they annoy me. 

I treat slow tests as a form of technical debt which eventually catches up with a development team. Slow tests mean longer run times for a devops pipeline a
