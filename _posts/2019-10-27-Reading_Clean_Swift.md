---
title: "Reading ‘Clean Swift’"
date: 2019-10-27
---

## Preface
The book start with bold statement, the architectures are same no matter variable is.
Author explains programming language has not that changed compared to the old, so architecture has not changed much too.

### Priority of work
1. Urgent & Important
2. Important
3. Urgent
4. Neither

### Paradigm
Structured, object-oriented, functional programming are old-paradigm. but they are useful nowadays and they are related.

Author tells about the history of Dijkstra.

Dijkstra want to use Euclidean hierarchy to figure complex programming problem. He found the 'goto' feature hinders modularity. So he made use case 'if/then/else' and 'do/while' for substitute 'goto' feature.

The 'proof' in Euclidean hierarchy were not used by most of programmer, instead they are using scientific method.
The 'disproof' is scientific method to proof they are not wrong.
From a programming standpoint, You can show there is a bug, but you cannot show there is not.

I think about TDD when i read the sentence above. Also i think BDD is a proof in Euclidean hierarchy.

### Object-Oriented Programming
What is the OOP? author asked.

He says the object, modeling of the real world is ambiguous definition and cannot understand where the goal it is.
I think object-oriented is a philosophy for understanding program easier.

Also he enumerates diverse definitions.

1. Encapsulation

Can encapsulate data and function in 'C' programming. Rather more OOP languages does not forcing to use it.

2. Inheritance

In other words, inheritance is redefinition of variables and functions. Also in 'C' we can archive inheritance.

3. Polymorphism

He says there is no difference using function pointer with v-table lookup and Polymorphism. But OOP provide this feature far better than using function pointer.

Using polymorphism, we can use plug-in architecture for making independent module. Nowadays, we prefer using protocol than override inheritance.
Also using dependency inversion we can inverse flow of control. And it makes we can make independent component.

### Functional Programming
Stateless is most important concept of functional programming. It solves the concurrency problem while using multi-thread programming.
We keep try to separate variable component and immutable component for containing concurrency problem without spreading.

### Event sourcing
Author says we can archive immutable application by using this.
Event sourcing is transaction based process like git. It store transaction not state. So application only CR not whole CRUD operation.

### SOLID
- SRP

In the module, SRP is a single purpose. Unlikely function, SRP is single job. It is matter of abstraction.

- OCP

We have to separate implementation by purpose. So we can isolate chain reaction from modification.
We have to prefer expanding not modifying.

- LSP

When using polymorphism, interface should not act differently.

- ISP

Do not include interface that module does not using.

- DIP

Dependence only abstraction is impossible. So we prefer stable abstraction for specific circumstance.
If concretion has lots of volatile, it is better to abstract for handle volatile.

### Conclusion
He simplify diverse concept of programming. I felt skeptic about that.
Every concept guide the way we programming. He says its restrict. Sure it is. For better way.
Also he says core concept of programming are sequence, selection, iteration, indirection. Sure it is.
