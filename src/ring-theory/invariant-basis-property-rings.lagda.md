#  The invariant basis property of rings

```agda
module ring-theory.invariant-basis-property-rings where

open import elementary-number-theory.natural-numbers

open import foundation.identity-types
open import foundation.universe-levels

open import ring-theory.dependent-products-rings
open import ring-theory.isomorphisms-rings
open import ring-theory.rings

open import univalent-combinatorics.standard-finite-types
```

## Idea

A ring R is said to satisfy the invariant basis property if `R^m ≅ R^n` implies `m = n` for any two natural numbers `m` and `n`.

## Definition

```agda
invariant-basis-property-Ring :
  {l1 : Level} → Ring l1 → UU l1
invariant-basis-property-Ring R =
  (m n : ℕ) →
  iso-Ring (Π-Ring {I = Fin m} (λ i → R)) (Π-Ring {I = Fin n} (λ i → R)) →
  Id m n
```
