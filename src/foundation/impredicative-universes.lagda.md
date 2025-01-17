#  Impredicative universes

```agda
module foundation.impredicative-universes where

open import foundation.propositions
open import foundation.small-types
open import foundation.universe-levels
```

## Idea

A universe `U` is impredicative if the type of propositions in `U` is `U`-small.

## Definition

```agda
is-impredicative-UU : (l : Level) → UU (lsuc l)
is-impredicative-UU l = is-small l (Prop l)
```
