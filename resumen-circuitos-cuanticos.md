# Notación algebraica para circuitos cuánticos

## Objetivo

Lenguaje algebraico formal para circuitos cuánticos con librería Mathematica que lo implemente. Meta final: descubrir reglas sistemáticas de optimización de circuitos.

---

## Decisiones de notación adoptadas

1. **Ket a la derecha:** $A_k|a\rangle$ (convenio Dirac estándar).
2. **Controles negativos:** $A^{\Gamma_1, \Gamma_0}_\Lambda$ donde $\Gamma_1$ activa en $|1\rangle$ y $\Gamma_0$ en $|0\rangle$.
3. **Equivalencia:** $A^{\Gamma_1, \Gamma_0}_\Lambda = X^{\Gamma_0} A^{\Gamma_0 \cup \Gamma_1}_\Lambda X^{\Gamma_0}$.

---

## Estructura de la librería Mathematica

```
QuantumAlgebra/
├── Core.wl        (* Kets, coeficientes, normalización *)
├── Gates.wl       (* Puertas estándar, $GateMatrix, HermitianQ *)
├── Controlled.wl  (* CNOT, CZ, CCNOT, SWAP, controles negativos *)
├── Simplify.wl    (* Productos, conmutación, involuciones *)
└── Tests.wl       (* Verificación de proposiciones del documento *)
```

---

## Tareas pendientes

1. Implementar `GatePower[name, k, n]` con simplificación automática para puertas hermitianas ($A^2 = I$).
2. Añadir `$GateMatrix` con matrices de puertas estándar (Id, X, Y, Z, H, S, T).
3. Añadir `HermitianQ[name]` que compara matriz con su adjunta.
4. Integrar reglas de potencias en `$PowerRules` dentro de Simplify.wl.

---

## Principios de implementación

- Separar representación semántica de presentación visual (`Format` con `TagSet`).
- Normalización mediante `$NormalizationRules` (no `TagSet`).
- Calcular adjunta al vuelo en lugar de almacenarla por instancia.

---

## Código pendiente de añadir a Gates.wl

```mathematica
(* === Matrices de puertas estándar === *)

$GateMatrix = <|
    Id -> {{1, 0}, {0, 1}},
    X -> {{0, 1}, {1, 0}},
    Y -> {{0, -I}, {I, 0}},
    Z -> {{1, 0}, {0, -1}},
    H -> {{1, 1}, {1, -1}} / Sqrt[2],
    S -> {{1, 0}, {0, I}},
    T -> {{1, 0}, {0, Exp[I Pi/4]}}
|>;

(* === Verificación de autoadjunta === *)

HermitianQ[name_] := With[
    {m = $GateMatrix[name]},
    If[MissingQ[m],
        False,
        ConjugateTranspose[m] === m
    ]
]

(* === Potencias de puertas === *)

GatePower[name_, k_, 0] := Gate[Id, k]
GatePower[name_, k_, 1] := Gate[name, k]
GatePower[name_, k_, 2] /; HermitianQ[name] := Gate[Id, k]
GatePower[name_, k_, n_Integer] /; HermitianQ[name] && n > 2 := 
    GatePower[name, k, Mod[n, 2]]
```

---

## Código pendiente de añadir a Simplify.wl

```mathematica
(* === Reglas de potencias en productos === *)

$PowerRules = {
    GateProduct[a___, Gate[name_, k_], Gate[name_, k_], b___] /; 
        HermitianQ[name] :> GateProduct[a, b],
    
    GateProduct[a___, Gate[name_, k_], Gate[name_, k_], Gate[name_, k_], b___] /; 
        HermitianQ[name] :> GateProduct[a, Gate[name, k], b]
};
```
