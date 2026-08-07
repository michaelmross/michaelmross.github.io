# A cubic corollary: the three classes of one-cut (1,2) construction

A note about the Jacobian counterexample. *Self-contained. (Verified by [trichotomy.py](https://github.com/michaelmross/jacobian/blob/main/trichotomy.py).)*

---

## Statement

Consider the multiplication map Sym^1 x Sym^2 -> Sym^3, (L, Q) |-> L Q,
restricted to the resultant normalization {Res(L,Q) = 1} and cut by one
affine hyperplane condition D(LQ) = 1, where D is a constant-coefficient
differential operator of order 3. Call the resulting threefold V. Up to a
change of coordinates D is a product of three directional derivatives, and
its class is the partition of 3 recording root multiplicities: **(3)**,
**(2,1)** or **(1,1,1)**. Since PGL_2(C) is 3-transitive on P^1 and each class
has at most three distinct roots, each class is a single orbit — there are no
moduli in degree 3, so these are exactly three cases.

> **Proposition.** For the three cubic classes the variety V behaves as
> follows.
>
> | class | V | reason |
> |---|---|---|
> | **(3)** | not affine space of any dimension | a coordinate is a nonconstant UNIT on V |
> | **(2,1)** | isomorphic to C^3 | explicit polynomial parametrization with polynomial inverse |
> | **(1,1,1)** | not homeomorphic to C^3 | chi(V) = 0 while chi(C^3) = 1 |
>
> In the middle case the multiplication map transports to a self-map of C^3
> that is étale with constant Jacobian determinant and not injective: a
> counterexample to the Jacobian conjecture.

The three arguments are independent of one another and use three different
invariants — units, an explicit isomorphism, and the Euler characteristic.
Each is short.

## Relation to the literature

The construction is Tao's, from his digestion of the counterexample of
Alpöge with Claude Fable 5; the case (2,1) is his, verified there by an
explicit coordinate computation, and the counterexample is Alpöge's. What is
recorded here is a proof for the other two classes, which that account did
not need and does not contain, together with an inverse making the (2,1) case
self-contained. A companion note treats the analogous question for
Sym^1 x Sym^k with any number of cuts.

---

## Setup

Write L = a z + b w and Q = c z^2 + d z w + e w^2, so V lies in C^5 with
coordinates (a, b, c, d, e). Since L is linear, the resultant is evaluation
of Q at the root of L:

        Res(L, Q) = Q(b, -a) = a^2 e - a b d + b^2 c.

Normalizing each operator by its leading constant, the three classes give

        class (3)       [roots 0,0,0]        D(LQ) = a c
        class (2,1)     [roots 0,0,infinity] D(LQ) = a d + b c
        class (1,1,1)   [roots 0,1,infinity] D(LQ) = a d - a e + b c - b d

and in each case V = {Res = 1} ∩ {D(LQ) = 1}, of dimension 3.

---

## Class (2,1): the miracle (Tao's case)

The cut D(LQ) = 1 restricted to a = 0 gives b c = 1, and Res = 1 gives
b^2 c = 1; together b = c = 1. So b - 1 and c - 1 vanish on {a = 0} and are
divisible by a. Substituting b = 1 - a t and c = 1 + a s, solving the cut for
d and the resultant for e, and clearing the one residual denominator by
s = (3t - a u)/2, gives a polynomial parametrization

        b = 1 - a t
        c = 1 + 3 a t/2 - a^2 u/2
        d = -t/2 + a u/2 + 3 a t^2/2 - a^2 t u/2
        e = u + 4 t^2 - 2 a t u - 3 a t^3 + a^2 t^2 u

by (a, t, u) in C^3, satisfying both defining equations identically.

That alone gives only a morphism C^3 -> V. For an isomorphism the inverse
must be polynomial too, and it is: on V the parameters are recovered by

        t = a e - 2 b d,
        u = e(9 - 6 b c - 2 c) - 4 d^2 (3 b + 1),

alongside a itself. Both compositions are verified in `trichotomy.py` — the
inverse formulas return t and u exactly when evaluated on the
parametrization, and the parametrization applied to (a, t, u) returns the
original point modulo the ideal of V (tested by reduction against a Gröbner
basis). Hence **V ≅ C^3**.

Writing the multiplication map in these coordinates and dropping the
coefficient pinned by the cut gives a polynomial self-map of C^3 with

        det J = -1/2   (a nonzero constant),

and a tested fiber has three distinct preimages, so the map is not injective.
That is a Jacobian counterexample — Alpöge's, up to coordinates.

---

## Class (3): a nonconstant unit

Here the cut is simply

        a c = 1.

So a is invertible on V, with inverse c: **a is a unit**. It is not constant:
a Gröbner computation certifies 1 ∈ I + (a), so a vanishes nowhere on V, and
V ∩ {a = v} is nonempty for v = 1, 2, 3, so a attains at least three distinct
values.

The coordinate ring of C^n is a polynomial ring, whose units are exactly the
nonzero constants. A variety carrying a nonconstant unit is therefore not
isomorphic to affine space of any dimension. Hence V is not C^3. ∎

*(This argument is robust: it needs no smoothness, no dimension count, and no
information about the rest of V.)*

---

## Class (1,1,1): the Euler characteristic

Here the cut is a d - a e + b c - b d = 1. Decompose V by the value of a.

**Fiber over a = 0.** The equations become b^2 c = 1 and b(c - d) = 1, so

        c = 1/b^2,      d = 1/b^2 - 1/b,       b in C^*,   e free.

The fiber is C^* x C, with chi = 0.

**Fiber over a = t != 0.** The coefficient of e in the cut is -t, never zero,
so solve the cut for e. Substituting into Res = 1 leaves an equation that is
**linear in d**, with coefficient t(t - 2b).

* For b != t/2 the coefficient is nonzero, so d is determined and then e is:
  this piece is (C minus one point) x C in the coordinates (b, c), with
  chi = 0.
* For b = t/2 the coefficient vanishes and solvability forces the single
  value c = 4(t + 1)/(3 t^2), leaving d free: one copy of C, with chi = 1.

So every fiber over a != 0 has chi = 1.

**Assembly.** The Euler characteristic is additive over the decomposition
V = (V ∩ {a = 0}) ⊔ (V ∩ {a != 0}), and multiplicative across a family with
constant fiber Euler characteristic. Since chi(C^*) = 0,

        chi(V) = chi(C^*) · 1 + chi(fiber at 0) = 0 + 0 = 0.

But chi(C^3) = 1, and chi is a homeomorphism invariant of complex algebraic
varieties. Hence V is not isomorphic — nor even homeomorphic — to C^3. ∎

*(Sanity check: the same computation applied to the class (2,1) gives fiber
chi = 1 over a = 0 and over each a != 0, hence chi(V) = 0·1 + 1 = 1,
consistent with V ≅ C^3 as established above.)*

---

## Remarks

**The two negatives use different invariants, and neither is a fiber
argument.** An earlier attempt to settle these cases by classifying the
degenerate fiber V ∩ {a = 0} is invalid: V ≅ C^n does *not* imply that a
coordinate hyperplane section is affine space. (A hypersurface in C^n can be
C^* x C^{n-2}.) The unit certificate and the Euler characteristic are both
global.

**Scope.** By "self-contained" is meant mathematical self-containment: the
three arguments above use only the resultant identity, a Gröbner
certificate, and additivity of the Euler characteristic. They do not use the
machinery developed for the general statement — the apolarity dictionary, the
divisibility criterion (a degeneracy occurs at p exactly when the dual form
of the cut is divisible by the k-th power of the linear form of p), or the
count of consistent points on a degenerate line. That machinery is needed
only for arbitrary k and arbitrary numbers of cuts, and is treated
separately. (`trichotomy.py` likewise imports nothing from the rest of the
verification suite; it is a single file.)

**Where the trichotomy comes from.** The general analysis locates the
phenomenon in the multiplicity structure of the dual form: writing the cut operator through its dual
cubic form G, a degeneracy occurs at a point p of P^1 exactly when G is
divisible by the square of the linear form vanishing at p. For a cubic that
forces the class to be (3) or (2,1); the class (3) degenerates too far (the
cut row vanishes identically on the degenerate line, leaving no consistent
point), while (2,1) leaves exactly k - 1 = 1 consistent point — and one
point is what an affine miracle requires. The trichotomy is then the
statement that k - 1 = 1 precisely when k = 2. This is a reformulation
rather than a geometric insight, but it does locate the phenomenon in the
multiplicity structure of the dual form.

**Verification.** `trichotomy.py` re-derives every displayed formula, checks
the parametrization satisfies both defining equations identically, computes
det J and a fiber, certifies the unit by Gröbner basis, and re-runs the Euler
computation including the (2,1) sanity check.

## Provenance

Framework: T. Tao, "A digestion of the Jacobian conjecture counterexample"
(July 2026), on the counterexample of L. Alpöge with Claude Fable 5.

Note written in adversarial human-AI collaboration: Michael M. Ross (<michaelmross@cantab.net>)
with Claude Opus 5 Max (Anthropic) and GPT-5.6 Sol (OpenAI)
