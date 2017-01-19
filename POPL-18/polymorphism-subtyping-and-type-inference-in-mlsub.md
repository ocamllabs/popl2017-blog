---
title: POPL: Polymorphism, subtyping and type inference in MLsub
author: let-def (Frédéric Bour)
abstract: Jan 18 10:30
---

# Constraint graphs in type inference

Traditional unification: types are related by equality, constraint graph is
undirected.

Subtyping: we have to distinguish when terms are used as input and output, and
construct a directed graph relating the types.

# Type algebra

Consider a simple type language with variables, constants, arrows. For the
purpose of subtyping, we add unions (join), intersections (meet) type
operators, a record type for demonstrating interesting subtypes, and a
subtyping relation.

Classical approach to define subtyping was by case analysis. (If this type and
that type do that, ...). But this proof breaks when type system receives
extensions.

Take a more abstract approach to avoid this problem.
E.g. by case analysis, it is tempting to reduce { record } /\ (bool -> bool) to
bottom (no inhabitant). But what if a language comes with this feature (C++,
Python, ... have callable classes)? So just keep it as is.

# Polar types and biunification/bisubstitution

To implement these concepts: two mutually defined type algebras, for positive
(values being produced) and negative (values being consumed) use cases.

Bisubstitution and biunification generalize unification algorithms to this
system.
Good properties: construction ensures that constraint graph can always be
simplified, no need to keep separate type and constraints.

E.g.

'a -> 'b | 'a <= T-
(function from alpha to beta such that alpha is less than some negative type)

can be rewritten to:

('a /\ T-) -> 'b

Polar types guarantees that hard case don't occur.

# Q/A

Q: What if user manually annotate types with the hard cases that wouldn't occur otherwise?

A: Should be fine because the cases don't have useful meaning (user don't want that).
