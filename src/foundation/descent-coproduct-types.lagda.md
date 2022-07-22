---
title: Descent for coproduct types
---

```agda
module foundation.descent-coproduct-types where

open import foundation.cones-pullbacks
open import foundation.coproduct-types
open import foundation.dependent-pair-types
open import foundation.empty-types
open import foundation.equality-dependent-pair-types
open import foundation.equivalences
open import foundation.fibers-of-maps
open import foundation.functions
open import foundation.functoriality-coproduct-types
open import foundation.homotopies
open import foundation.identity-types
open import foundation.pullbacks
open import foundation.universe-levels
```

## Theorem

```agda
module _
  {l1 l2 l3 l1' l2' l3' : Level}
  {A : UU l1} {B : UU l2} {X : UU l3}
  {A' : UU l1'} {B' : UU l2'} {X' : UU l3'}
  (f : A' → A) (g : B' → B) (h : X' → X)
  (αA : A → X) (αB : B → X) (αA' : A' → X') (αB' : B' → X')
  (HA : (αA ∘ f) ~ (h ∘ αA')) (HB : (αB ∘ g) ~ (h ∘ αB'))
  where
  
  triangle-descent-square-fib-map-coprod-inl-fib :
    (x : A) →
    (fib-square αA h (triple f αA' HA) x) ~
      ( ( fib-square (ind-coprod _ αA αB) h
          ( triple
            ( map-coprod f g)
            ( ind-coprod _ αA' αB')
            ( ind-coprod _ HA HB))
          ( inl x)) ∘
      ( fib-map-coprod-inl-fib f g x))
  triangle-descent-square-fib-map-coprod-inl-fib x (pair a' p) =
    eq-pair-Σ refl
      ( ap (concat (inv (HA a')) (αA x))
        ( ap-comp (ind-coprod _ αA αB) inl p))

  triangle-descent-square-fib-map-coprod-inr-fib :
    (y : B) →
    (fib-square αB h (triple g αB' HB) y) ~
      ( ( fib-square (ind-coprod _ αA αB) h
          ( triple
            ( map-coprod f g)
            ( ind-coprod _ αA' αB')
            ( ind-coprod _ HA HB))
          ( inr y)) ∘
      ( fib-map-coprod-inr-fib f g y))
  triangle-descent-square-fib-map-coprod-inr-fib y ( pair b' p) =
    eq-pair-Σ refl
      ( ap (concat (inv (HB b')) (αB y))
        ( ap-comp (ind-coprod _ αA αB) inr p))

module _
  {l1 l2 l3 l1' l2' l3' : Level}
  {A : UU l1} {B : UU l2} {X : UU l3} {A' : UU l1'} {B' : UU l2'} {X' : UU l3'}
  (f : A → X) (g : B → X) (i : X' → X)
  where
  
  cone-descent-coprod :
    (cone-A' : cone f i A') (cone-B' : cone g i B') →
    cone (ind-coprod _ f g) i (A' + B')
  pr1 (cone-descent-coprod (pair h (pair f' H)) (pair k (pair g' K))) =
    map-coprod h k
  pr1
    ( pr2 (cone-descent-coprod (pair h (pair f' H)) (pair k (pair g' K))))
    ( inl a') = f' a'
  pr1
    ( pr2 (cone-descent-coprod (pair h (pair f' H)) (pair k (pair g' K))))
    ( inr b') = g' b'
  pr2
    ( pr2 (cone-descent-coprod (pair h (pair f' H)) (pair k (pair g' K))))
    ( inl a') = H a'
  pr2
    ( pr2 (cone-descent-coprod (pair h (pair f' H)) (pair k (pair g' K))))
    ( inr b') = K b'

  abstract
    descent-coprod :
      (cone-A' : cone f i A') (cone-B' : cone g i B') →
      is-pullback f i cone-A' →
      is-pullback g i cone-B' →
      is-pullback (ind-coprod _ f g) i (cone-descent-coprod cone-A' cone-B')
    descent-coprod (pair h (pair f' H)) (pair k (pair g' K))
      is-pb-cone-A' is-pb-cone-B' =
      is-pullback-is-fiberwise-equiv-fib-square
        ( ind-coprod _ f g)
        ( i)
        ( cone-descent-coprod (triple h f' H) (triple k g' K))
        ( α)
      where
      α : is-fiberwise-equiv
          ( fib-square (ind-coprod (λ _ → X) f g) i
          ( cone-descent-coprod (triple h f' H) (triple k g' K)))
      α (inl x) =
        is-equiv-left-factor
          ( fib-square f i (triple h f' H) x)
          ( fib-square (ind-coprod _ f g) i
            ( cone-descent-coprod (triple h f' H) (triple k g' K))
            ( inl x))
          ( fib-map-coprod-inl-fib h k x)
          ( triangle-descent-square-fib-map-coprod-inl-fib
            h k i f g f' g' H K x)
          ( is-fiberwise-equiv-fib-square-is-pullback f i
            ( triple h f' H) is-pb-cone-A' x)
          ( is-equiv-fib-map-coprod-inl-fib h k x)
      α (inr y) =
        is-equiv-left-factor
          ( fib-square g i (triple k g' K) y)
          ( fib-square
            ( ind-coprod _ f g) i
            ( cone-descent-coprod (triple h f' H) (triple k g' K))
            ( inr y))
            ( fib-map-coprod-inr-fib h k y)
            ( triangle-descent-square-fib-map-coprod-inr-fib
              h k i f g f' g' H K y)
            ( is-fiberwise-equiv-fib-square-is-pullback g i
              ( triple k g' K) is-pb-cone-B' y)
            ( is-equiv-fib-map-coprod-inr-fib h k y)

  abstract
    descent-coprod-inl :
      (cone-A' : cone f i A') (cone-B' : cone g i B') →
      is-pullback (ind-coprod _ f g) i (cone-descent-coprod cone-A' cone-B') →
      is-pullback f i cone-A'
    descent-coprod-inl (pair h (pair f' H)) (pair k (pair g' K)) is-pb-dsq =
        is-pullback-is-fiberwise-equiv-fib-square f i (triple h f' H)
          ( λ a → is-equiv-comp
            ( fib-square f i (triple h f' H) a)
            ( fib-square (ind-coprod _ f g) i
              ( cone-descent-coprod (triple h f' H) (triple k g' K))
              ( inl a))
            ( fib-map-coprod-inl-fib h k a)
            ( triangle-descent-square-fib-map-coprod-inl-fib
              h k i f g f' g' H K a)
            ( is-equiv-fib-map-coprod-inl-fib h k a)
            ( is-fiberwise-equiv-fib-square-is-pullback (ind-coprod _ f g) i
              ( cone-descent-coprod ( triple h f' H) (triple k g' K))
              ( is-pb-dsq)
              ( inl a)))

  abstract
    descent-coprod-inr :
      (cone-A' : cone f i A') (cone-B' : cone g i B') →
      is-pullback (ind-coprod _ f g) i (cone-descent-coprod cone-A' cone-B') →
      is-pullback g i cone-B'
    descent-coprod-inr (pair h (pair f' H)) (pair k (pair g' K)) is-pb-dsq =
        is-pullback-is-fiberwise-equiv-fib-square g i (triple k g' K)
          ( λ b → is-equiv-comp
            ( fib-square g i (triple k g' K) b)
            ( fib-square (ind-coprod _ f g) i
              ( cone-descent-coprod (triple h f' H) (triple k g' K))
              ( inr b))
            ( fib-map-coprod-inr-fib h k b)
            ( triangle-descent-square-fib-map-coprod-inr-fib
              h k i f g f' g' H K b)
            ( is-equiv-fib-map-coprod-inr-fib h k b)
            ( is-fiberwise-equiv-fib-square-is-pullback (ind-coprod _ f g) i
              ( cone-descent-coprod (triple h f' H) (triple k g' K))
              ( is-pb-dsq)
              ( inr b)))
```