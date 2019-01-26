# CQRS

> CQRS stands for **Command Query Responsibiity Segregation**.

Basically it means separating Query/Read methods and Command/Mutate methods.

### Benefits

- C and Q are decoupled and can have different architecture, and scale differently.

**But it also make system more complicated so use it with caution.**

>The interesting part is not the pattern itself but the architectual decisions can be made around it.

From [codebetter post](http://codebetter.com/gregyoung/2010/02/16/cqrs-task-based-uis-event-sourcing-agh/) and [CQRS](https://martinfowler.com/bliki/CQRS.html).

