---
title: The Mathematics of Computer Science
tags: math programming pl 
season : summer
content-type: article
---

# Introduction

# Content
The content of these posts will cover a variety of topics, not necessarily all to the same depth. The overall goal is to expose computer scientist, software engineers, or anyone who may just be curious, to the type of mathematics a university student would expect to encounter in an undergraduate degree, with particular applications to computer science. Obviously, this is a very wide spectrum of content, but it can be broken up as follows:

- Logic
- Discrete Mathematics
	- Abstract Algebra
	- Elementary Number Theory
- Calculus/Analysis
	- Numerical Analysis
- Geometry
	- Topology

It is obviously not expected for an individual person to be able to process all of these topics in a few blog posts, so included in these posts will be exercises to help build understanding. Sometimes, the applications will appear obvious, and other times, they will seem arcane. 

The genesis of this series of blog posts is motivated by my desire to understand homotopy type theory, and motivate others to understand it. While the name itself implies a heavy connection to computer science, it is also *very* mathematical in nature. It builds on many notions from topology, like, naturally, homotopy classes of loops and paths. While a strong knowledge of mathematics is not necessary to digest the basics of the field, it is useful.

Moreover, I am a firm believer that visual and geometric intutions are phenominal tools for understanding and communication. While I am by no means the sole believer of this idea, I have found that many math texts, even the more approachable ones, lack a visceral, visual intuition. While this series is by no means a replacement for a math degree, nor for traditional textbooks, it is meant to serve as a midground between either of these topics and computer scientists.

## Advanced Content

Beyond what is covered in a tradtional undergraduate mathematics degree, there are a number of advanced topics, which are particularly relevent to computer scientists. While the concepts are considered advanced for many undergraduate mathematicians, they are certainly still approachable to those who wish to learn. To enumerate a few we may explore, we have

* Mathematical Logic
* Algebraic Geometry
	* Gröbner Basis
* Category Theory
* Algebraic Topology

The applications of each of these are a bit more sparse than those listed above, which is understandable: advanced problems sometimes require advanced tools. Some of these fields may even seem familiar, like category theory to anyone who uses Haskell.

# A Warning on Methodology
This series of posts is *not* intended as an algorithmic cookbook. The topics covered are explored as topics in (traditionally) pure mathematics, and the development will be treated as such, with a skew in applications towards problems in computer science. While some problems and exercises addressed will be decidedly algorithmic in flavor (particularly numerical analysis and Gröbner basis), this is not something that is guarenteed throughout.

# Parting Thoughts
Mathematics is hard. Like, really really hard. It can often seem insurmountable; arcane problems with eldritch symbols and concepts only muttered about by old people in an Ivory Tower. 

This is how many people think of math, and its plainly wrong. Sure, there is *some* math like this, particularly a large portion of modern math can feel this way, but it really is just a matter of time and dedication. I am a firm believer that anyone one, given sufficient time, energy, and drive, can approach, digest, and learn to love and appriciate math in all of its beauty. 

It is unfortunate that (at least in the good ol' U.S. of A.) that students in K-12 tend to detest math, whether for its complexity or poor teaching. It does not need to be this way. Math is an inherently beautiful subject; rather than the study of arithmetic, mathematics is the study of structure. 

Structure can be anything: ways to manipulate things in 3-D space, fractals, symmetry, and more. Arithmetic naturally plays a role as well, but arithmetic is really just a special kind of structure (spoiler alert: its primarily field theory).

All this to say, the main goal of this series, beyond teaching interesting and insightful mathematics, is to show the inherent beauty of math to more people. If even one person walks away from these posts thinking "wow, I didn't know math could be this interesting", I will count that as a win.

# A Sneak Peak Into the Future
Finally, I offer a sneak peak into what comes next. As indicated by the uppermost list, logic is the first topic on the menu. We will develop the basic theory of boolean algebra, and using De Morgan's laws, derive all of the logical connectives we need, using only the equivalent of NAND and NOT gates.