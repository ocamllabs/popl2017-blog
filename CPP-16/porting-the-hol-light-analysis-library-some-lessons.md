---
title: CPP: Porting the HOL Light Analysis Library: Some Lessons
author: let-def (Frédéric Bour)
abstract: Jan 16 09:00
---

Port theorems and proofs from HOL Light.

# Statement

Problem: HOL Light proofs are low-level, unstructured.
Goal: having readable and general proofs.

Domain specific proofs: no time to learn the underlying theory everytime, translation has to be mostly oblivious to the actual objects.
Genericity in lack of dependent types: circumvent with a clever encoding, just sufficient for the purpose of these proofs.

# Approach

A. Translate HOL Light to text using Perl.
B. Try to find structure in the proof.
C. Reconstruct with Isabelle. 
D. Sometime get stuck: look for ideas, ...

# Proof rot

Avoiding "proof rot": keep obvious steps explicit, e.g x + 0 = x.

Isabelle applies heuristic, which may fail after update.
=> more risks of proof rot.
Hol, Coq: decision procedures, with (hopefully) well specified domain of applications.

Structure proofs + automation = clarity + easy maintenance.

# Sceptical mathematicians

Convincing sceptical mathematicians: easier with structured proofs.

Trusting the kernel: mathematicians don't like code.
Reading proofs with baby steps: doable, easy to see proof is tricial.

# Lessons: proofs should communicate ideas

Once formalised, math are easy to translate between formal systems.

Legible proof: easy to translate, maintenance and communication.
-> Keep links to ideas, e.g. refs to books.

Tooling is necessary for managing proof libraries.

# Q/A

Q: Having 100% automated proof tranlations?

A: You want to use feature of the richer target language (e.g
dependent types). Tooling alone can (hardly) solve that, translation
should be guided by humans.
Same in the other directions, translating to weaker language.
