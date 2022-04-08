# nauty-pet

Canonical graph labelling.

Leverages [nauty and Traces](http://pallini.di.uniroma1.it/) to
find [canonical
labellings](https://en.wikipedia.org/wiki/Graph_canonization) for
[petgraph](https://github.com/petgraph/petgraph) graphs.

## Usage

Version 2.6 or 2.7 of the nauty and Traces library has to be
installed first and _linked to the same C library as this crate_.

Afterwards, add this to your Cargo.toml:
```toml
[dependencies]
nauty-pet = "0.4"
```

## Example

```rust
use petgraph::graph::UnGraph;
use nauty_pet::prelude::*;

// Two different vertex labellings for the tree graph with two edges
let g1 = UnGraph::<(), ()>::from_edges([(0, 1), (1, 2)]);
let g2 = UnGraph::<(), ()>::from_edges([(0, 1), (0, 2)]);

// There are two equivalent labellings
let automorphism_info = g1.clone().try_into_autom().unwrap();
assert_eq!(automorphism_info.grpsize(), 2.);

// The canonical forms are identical
let c1 = g1.into_canon();
let c2 = g2.into_canon();
assert!(c1.is_identical(&c2))
```

License: Apache-2.0
