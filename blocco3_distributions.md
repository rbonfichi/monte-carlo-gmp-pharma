# Block 3 — Simple Distributions

## Uniform(a,b)
Transform: `X = a + (b-a)U`.

## Exponential(λ)
CDF `F(x)=1-exp(-λx)` ⇒ inverse: `X = -log1p(-U)/λ`.

## Normal(μ,σ) via Box–Muller
```
Z1 = sqrt(-2*log(U1)) * cos(2*pi*U2)
Z2 = sqrt(-2*log(U1)) * sin(2*pi*U2)
X  = μ + σ Z
```

## Triangular(a,c,b)
Let `Fc=(c-a)/(b-a)`. Piecewise inverse:
```
if (U < Fc)  X = a + sqrt(U*(b-a)*(c-a))
else         X = b - sqrt((1-U)*(b-a)*(b-c))
```
