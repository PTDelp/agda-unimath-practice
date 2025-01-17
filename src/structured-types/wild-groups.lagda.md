#  Wild groups

```agda
module structured-types.wild-groups where

open import foundation.cartesian-product-types
open import foundation.dependent-pair-types
open import foundation.binary-equivalences
open import foundation.universe-levels

open import structured-types.pointed-types
open import structured-types.wild-monoids
```

```agda
is-wild-group-Wild-Monoid :
  {l : Level} (M : Wild-Monoid l) → UU l
is-wild-group-Wild-Monoid M = is-binary-equiv (mul-Wild-Monoid M)

Wild-Group : (l : Level) → UU (lsuc l)
Wild-Group l = Σ (Wild-Monoid l) is-wild-group-Wild-Monoid
```
