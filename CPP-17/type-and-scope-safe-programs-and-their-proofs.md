---
title: CPP: Type-and-scope safe programs and their proofs
author: let-def (Frédéric Bour)
abstract: Jan 17 16:00
---

A tool to easy manipulation of binders in "type and scope" safe programs.

Assuming an encoding with a typed syntax.  Many transformation working with
binders have a similar structure (renaming, substitution, etc). `Kit` is a
first abstraction proposed by McBride (?) to automate these.

The author presents a more general `Semantics` abstraction (applying to
semantics too) generalizing `Kit`. It can handle renaming (`Semantics
Var Var`, ... from `Var` to `Var`), substitution (`Semantics Var Tm`, from var
to terms), normalization by evaluation (`Semantics Kr Kr`, one still has to
implement reification manually) ...
