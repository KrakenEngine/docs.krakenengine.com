---
title:  "Hydra - kraken::vector2"
published: true
permalink: sdk_hydra_vector2
summary: "The Vector2 structure encapsulates a 2 dimensional vector with single precision floating point members."
---

### Members

```
union {
  struct {
    float x, y;
  };
  float c[2];
};
```


The `kraken::vector2` struct has two members, representing the `x` axis value and `y` axis value of a vector.  A `union` is provided to allow array-style access to these members using `c`.  `c[0]` can be used to access `x` while `c[1]` can be used to access `y`.

Like all Hydra structures, `kraken::vector2` is guaranteed to be [POD](https://en.cppreference.com/w/cpp/named_req/PODType).

`kraken::vector2` members are `float` values.  To work with `int` values, see [kraken::vector2i](sdk_hydra_vector2i).

Like all Hydra structures, the `kraken::vector2` members are guaranteed never to perform heap allocations.  All allocations will be stack-based.

### Initialization

The structures have only a default constructor and destructor.  No cycles are wasted on redundant initialization.

#### In-place initialization

An `init()` method and variants are provided to explicitly initialize (or reset) the members.

- `void init();`

  Sets `x` and `y` to `0.0`.

- `void init(float X, float Y);`

  Sets`x` to `X` and `y` to `Y`.

- `void init(float v);`

  Sets both `x` and `y` to `v`.

- `void init(float *v);`

  Sets `x` to `v[0]` and `y` to `v[1]`.

- `void init(const Vector2 &v);`

  Copies the `x` and `y` members from the passed in `v` to this intance's `x` and `y`.

#### Factory Methods

Static methods are provided to create initialized Vector2's.  These convenience functions allow for more compact code at call sites, where the structure may be initialized and used inline.

- `static Vector2 Create();`

  Returns a `Vector2` with `x` and `y` set to `0.0`.

- `static Vector2 Create(float X, float Y);`

  Returns a `Vector2` with `x` set to `X` and `y` set to `Y`.

- `static Vector2 Create(float v);`

  Returns a `Vector2` with `x` and `y` both set to `v`.

- `static Vector2 Create(float *v);`

  Returns a `Vector2` with `x` set to `v[0]` and `y` set to `v[1]`.

- `static Vector2 Create(const Vector2 &v);`

  Copies a `Vector2`.  Returns a `Vector2` with member values copied from `v`.

- `static Vector2 Min();`

  Returns a `Vector2` with `x` and `y` set to the lowest values that can be expressed with a `float`.

- `static Vector2 Max();`

  Returns a `Vector2` with `x` and `y` set to the largest values that can be expressed with a `float`.

- `static Vector2 Zero();`

  Returns a `Vector2` with `x` and `y` set to `0.0`.

- `static Vector2 One();`

  Returns a `Vector2` with `x` and `y` set to `1.0`.

