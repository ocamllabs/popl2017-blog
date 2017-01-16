---
title: CPP: Verifying a hash table and its iterator in higher-order separation logic
author: let-def (Frédéric Bour)
abstract: Jan 16 10:30
---

Proving the implementation of an OCaml hashtable 

Scheme:
- implement in OCaml with a functor from Key type
- use CFML to extract Coq representation
- prove properties on Coq representation

For this talk:
- hashtable is made of an array of bucket
- formalize adding values and iteration (fold and _cascade_, essentially a lazy stream where consumer is in control)

Formalization difficulty:
- assume mutable world
- formalize higher-order functions

CFML use a separation logic.
Specification of operations can require that the structure is read-only in certain scopes (e.g no mutation during iteration).

Specification using Hoare triplets: pre-condition, expression, post-condition.
Permissions/resources annotations can be associated to heap values.

# Formalizing fold

During fold:
- what is the order in which bindings are visited?
- can the table be read? can the table be written?

Allow a set of orders, formalized as a set of valid observations.
Use an encoding suggested by Filliatre and Pereira (two properties, permitted and complete to characterize valid orders).

Higher-order specification for fold (hashtable abstracted away): implication between hoare triplets.
Abstract the access permissions {read, write}.

Multiple bindings for the same key are permitted (abstract view of Hashtable is a function Key -> List Value).
Semi-deterministic specification:
- keys are visited in any order
- bindings for a given key are visited most recent first

Instance of fold specification on Hashtable disallow writing to Hashtable. Permissions express that the table must be in the same state at the end of the fold.

# Formalizing cascade (Java style iterator)

Java interface is awful:
- two methods, a partial one and one to test validity.
- unnecessarily mutable

Cascade: delayed list, `type 'a cascade = unit -> 'a head and 'a head = Nil | Cons of 'a of 'a cascade`.

Specification: we also need to protect concurrent modifications.
A cascade is invalidated by modification.
This is an hypothesis in Coq code. Not checked at runtime (not certified users of library could break assumptions).

Simplification: losing some generality, we assume cascades are duplicable (a cascade is persistent, the tail can be evaluated multiple times).
Easier to prove, although in complete generality this could also be abstracted over.

# Conclusion

- Nice specifications with vanilla separation logic.
- Easy to implement (15 man days), though lof of expertise needed
- In the future, make this approach more accessible 

# Q/A

Q: About specification language, INV used in Hoare triplets (among PRE and POST).

A: INV desugars to PRE and POST.

Q: So permission S specified twice in a POST condition?

A: Yes, this is allowed. Usage must be compatible.
