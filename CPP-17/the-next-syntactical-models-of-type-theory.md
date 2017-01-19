---
title: CPP: The Next 700 Syntactical models of type theory
author: let-def (Frédéric Bour)
abstract: Jan 17 15:00
---

When you beginning using a proof assistant, you are told that:
- functional extensionality doesn't hold
- same for Prop, equality between equalities, etc.

Even if it looks true... And the explanation is that you should admit.

# Syntactic models

Categorical models... are crazy complex.
But we already understand type theory, use compilers from type theory into itself as models.

Let's define [.] to rewrite terms to terms and [[.]] to rewrite types to types.

# What we can rewrite...

Inductive types: fully specified (because of dependent elimination),
no freedom to modify.

Negatives types, functions: lot of freedom, weaker elimination principles.

Interpret everything through [.] translation:

# Negating functional extensionality

Simple example to illustrate the idea:

Let's translate [(lam x, t)] to [(lam x, t), true] (and for
consistency [[A -> B]] to A -> B * Bool.

Let's introduce a second lam' that translates to [(lam x, t), false].
These behave like regular lambdas, (distinction cannot be observed by
elimination), yet the two can be trivially distinguished in the
translation.
So functional extensionality is independant.

# Applies same idea too...

Propositional extensionality, type extensionality, etc.

# Ad-hoc polymorphism

By representing coq in coq (encoding all terms to codes), we get a list of stratified inductive types. Then we can define functions that pattern matches on these (dependent functions ), to adjust their behavior.

# Q/A

Q: You explain that functional extensionality cannot be proven, but one can give intuition. What about explaining that TYPE in TYPE is inconsistent?

A: It's already possible to give intuition that this enables unbounded fixpoints. But one could translate TYPE in TYPE to a degenerate model where loops are obvious. However... What I am about to say is false, but I am more interested in consistent models.
