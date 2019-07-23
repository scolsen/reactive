# Notes on the "Revised Report on the Propagator Model"

In their abstract, Sussman and Radul summarize the chief advantage to the propagator
model: that it enables the implementation of redundancy and diversity within a
system, presumably increasing the systems flexibility and adaptability–crucial
properties when changes are inevitably required. They go on to describe the
model itself:

> The Propagator Programming Model is built on the idea that the basic
> computational elements are autonomous machines interconnected by shared cells
> through which they communicate. Each machine continuously examines the cells
> it is interested in, and adds information to some based on computations it can
> make from information from the others. Cells accumulate information from the
> propagators that produce that information. The key idea here is additivity.
> New ways to make contributions can be added just by adding new propagators; if
> an approach to a problem doesn't turn out to work well, it can be identified
> by its premises and ignored, dynamically and without disruption.

The core of the model rests on a protocol for communication between propagators
and cells, and a number of capabilities cells must satisfy. As Sussman and Radul
list, cells must:

- add content
- collect currently accumulated content
- register propagators to notify when accumulated content changes

Importantly, cells must be omniminesic entities that "never forget" their
contents. Thus, any additions to a cell's content must be *merged* with its prior
contents.

A cell's merging operation must satisfy the following algebraic laws: 

- **commutative**
  `a merge b = b merge a`
- **associative**
  `a merge (b merge c) = (a merge b) merge c`
- **idempotent**
  `a merge a = a`

If the cell's merging procedure satisfies these laws, it forms an (algebraic)
semilattice.

Additionally,

> The behavior of propagators must be monotonic with respect to the lattice
> induced by the merge operation.

Note, that `merge` only induces a
[semilattice](https://en.wikipedia.org/wiki/Semilattice) (it is one binary operation,
whereas lattice's define two; additionally, the authors make no mention of
satisfying the law of absorption).

<!--TODO: Investigate the monotonicity requirement further; is it in respect to
orders induced on the semilattice? According to wikipedia, order-theoretic and
algebraic semilattice definitions can be used interchangeably, so these should
amount to the same thing. Another question: whether join or meet semilattice's
are more appropriate here.-->

In terms of the merge operation, the monotonicity requirement indicates that propagators cannot react sporadically to the accumulation of information in a cell. 
