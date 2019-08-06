---
title:  "Hydra Math Library - Introduction"
published: true
permalink: sdk_hydra_introduction
summary: "Introduction to the Hydra Math Library"
tags: [getting_started]
---

## Hydra Math Library

Kraken includes the Hydra Math Library.  This library consists of a set of
POD structures and methods to make it easier to work with values used in the Kraken Engine API.

All of the Hydra structures are POD (Plain Old Data).  This enables the most flexibility in passing them between threads, accessing them from memory mapped files, copying between GPU and CPU memory, and allocating them in large contiguous arrays.

Hydra functions only use stack allocations.  You can safely use them within performance sensitive cases (eg, realtime rendering loops), without risks associated with heap allocations.

The structures have only the default constructor and destructor.  No cycles are wasted on redundant initialization.  An `init()` method and variants are provided to explicitly initialize the members.

### Hydra Structures

#### Scalar Numbers
- [kraken::scalar](sdk_hydra_scalar)

#### Vectors
- [kraken::vector2](sdk_hydra_vector2)
- [kraken::vector2i](sdk_hydra_vector2i)
- [kraken::vector3](sdk_hydra_vector3)
- [kraken::vector4](sdk_hydra_vector4)

#### Matrices
- [kraken::matrix2](sdk_hydra_matrix2)
- [kraken::matrix2x3](sdk_hydra_matrix2x3)
- [kraken::matrix4](sdk_hydra_matrix4)

#### Quaternions
- [kraken::quaternion](sdk_hydra_quaternion)

#### Geometry
- [kraken::triangle3](sdk_hydra_triangle3)
- [kraken::aabb](sdk_hydra_aabb)
