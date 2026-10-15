# ALRCC — Documento central del proyecto

*Algebraic Language for Representation of Quantum Circuits.* Punto de entrada único: aquí se recoge qué es el proyecto, dónde está cada cosa, el camino a seguir y los «inicios» recuperados de intentos anteriores.

Última actualización: 2026-10-15.

---

## 1. Objetivo

Parte del artículo publicado con el grupo de la Universidad de La Laguna
*Algebraic language for the efficient representation and optimization of quantum circuits* (Escánez-Expósito et al., *Physica Scripta* 100, 025107, 2025; PDF en `referencias/`) y lo amplía con un tratamiento basado en conjuntos de índices (controles $\Gamma$, targets $\Lambda$) para un número arbitrario de cúbits.

**Objetivo principal:** cálculo algebraico formal para circuitos cuánticos reversibles que permita expresar, comparar y **optimizar** circuitos de $n$ cúbits mediante reescritura simbólica.

**Nicho elegido (hipótesis H1):** lenguaje algebraico textual para la optimización simbólica de circuitos clásico-reversibles en contexto criptográfico, **complementario** a ZX-calculus (no competidor general).

| Técnicos | Aplicados |
|---|---|
| O1 Sintaxis formal (BNF) | O6 Prototipo en Mathematica |
| O2 Reglas de reescritura con terminación y confluencia | O7 Aplicación a códigos de corrección de errores |
| O3 *Soundness* respecto a la semántica matricial | O8 Aplicación a algoritmos criptográficos cuánticos |
| O4 Optimización de circuitos Toffoli | |
| O5 Entrelazamiento y mediciones | |

---

## 2. Mapa del repositorio

| Ruta | Contenido |
|---|---|
| `src/` | Fuentes LaTeX. `main.tex` (manuscrito), `critical_analysis.tex` (análisis crítico + plan), `presentation.tex` (beamer), `bibliography.bib`, `roadmap.bib` (papers del plan) |
| `entregas/` | PDF compilados: `main.pdf`, `critical_analysis.pdf`, `presentation.pdf` |
| `referencias/` | PDF de artículos (el de la ULL y los del plan de lectura) |
| `resumen-circuitos-cuanticos.md` | Resumen del chat sobre notación y la librería Mathematica |
| `PROYECTO.md` | Este documento |

Compilar desde `src/`: `latexmk -pdf main.tex`.

---

## 3. Hoja de ruta (recomendaciones R0–R8)

Fuente: `src/critical_analysis.tex`, sección «Recomendaciones prioritarias» (rev. 2, junio 2026).

| # | Recomendación | Estado |
|---|---|---|
| R0 | Corregir errores matemáticos de base: (a) conjugación $a_\gamma=\langle\gamma\|a\rangle$ en `notation.tex`; (b) ecuación de Hadamard; (c) casos intercambiados y abusos de tipo en `deutsch.tex`; (d) erratas en `ket.tex`, `pauli.tex`, normalización de $\|\pm\rangle$; (e) convención postfija y $a$/$\alpha$; (f) generalizar $\|a\rangle^k_\gamma$ a $\gamma$ estado arbitrario. *Días.* | Hecho (2026-10-15): todo el manuscrito pasa al convenio de Dirac (ket a la derecha); $a$/$\alpha$ unificados; $\ket{a}^{k_1\cdots k_l}_{b_1\cdots b_l}$ generalizado a estados arbitrarios; hipótesis de índices distintos añadidas; pruebas de `1-qubit-properties.tex` reescritas. |
| R1 | Declarar el nicho H1 desde el inicio | Pendiente |
| R2 | Sección de estado del arte comparando con ZX-calculus, PyZX, OpenQASM 3, Quipper | Pendiente (lectura en curso) |
| R3 | Formalizar el cálculo: BNF, semántica denotacional, reglas, *soundness* | Iniciado (2026-10-15): `src/syntax.tex` con BNF, buena formación, semántica $[\![\cdot]\!]$, unitariedad, equivalencia $\cong$ y regla de inversión de control. Falta el conjunto de reglas orientadas, terminación y confluencia |
| R4 | Resultado palanca: generalizar la reducción de controles (eq. `mainresult`) a $\Delta\subseteq\Gamma$ conjugados por $X_\Delta$ → cancelación en cascadas Toffoli | Pendiente |
| R5 | Lema de extensión lineal, lemas de factorización, lema de *phase kickback* (completa `deutsch.tex`) | Pendiente |
| R6 | Definición y propiedades de la medición | Pendiente |
| R7 | Prototipo (Mathematica `QuantumAlgebra/` o Python/SymPy) con exportación a Qiskit | Iniciado en otro chat; código **no localizado** |
| R8 | Correcciones editoriales (duplicación `qubit.tex`/`notation.tex`, reincorporar abstract/intro/sumador, completar o quitar `universal_gates.tex`) | Pendiente |

**Orden recomendado:** R0 en paralelo con R1 y R2 → R5a (extensión lineal) → R4.

---

## 4. Plan de lectura

Fuente: `src/critical_analysis.tex`, sección «Línea de trabajo». Referencias BibTeX en `src/roadmap.bib`.

Estado: ✅ leído · 📄 PDF en `referencias/` · ⬜ falta conseguir el PDF.

| Fase | Semana | Paper | Desbloquea | Estado |
|---|---|---|---|---|
| **1. Estado del arte** (2–3 sem) | 1–2 | Coecke & Duncan 2008, *Interacting quantum observables* | R2 | ✅ 📄 |
| | 1–2 | Backens 2014, *ZX-calculus is complete for stabilizer QM* | R3 | 📄 |
| | 2 | Kissinger & van de Wetering 2019, *PyZX* | R4 | ⬜ |
| | 2 | Hutsell & Greenwood 2009, *Efficient algebraic representation of quantum circuits* | R2 | ⬜ |
| | — | Nielsen & Chuang 2010, caps. 4–5 | — | ✅ |
| **2. Reescritura** (2 sem) | 3 | Baader & Nipkow 1998, *Term Rewriting and All That*, caps. 1–3 | R3 | ⬜ |
| | 3 | Abramsky & Coecke 2004, *Categorical semantics of quantum protocols* | R3 | ⬜ |
| | 3 | Selinger 2004, *Towards a quantum programming language* | R3 | ⬜ |
| **3. Optimización** (2–3 sem) | 4–5 | Jeandel, Perdrix & Vilmart 2018, *ZX complete for Clifford+T* | R3, R4 | ⬜ |
| | 5 | Maslov 2016, *Relative-phase Toffoli gates* | R4 | ⬜ |
| | 5–6 | Amy, Maslov, Mosca & Roetteler 2013, *Meet-in-the-middle* | R4 | ⬜ |
| | 6 | Cross et al. 2022, *OpenQASM 3* | R1 | ⬜ |
| **4. Alcance** (3–4 sem) | 7–8 | Selinger & Valiron 2006, *Quantum lambda calculus* | R6 | ⬜ |
| | 7–8 | Bichsel et al. 2020, *Silq* | R6 | ⬜ |
| | — | Perdrix & Wang 2016, *Supplementarity* | — | ⬜ |
| | 9 | Green et al. 2013, *Quipper* | R7 | ⬜ |
| **Añadidos** (vigilancia) | 2 | Cockett & Comfort 2018, *The category TOF* — competencia directa de H1 | R1, R2, R4 | ⬜ |
| | 3 | Clément, Heurtel, Mansfield, Perdrix & Valiron 2023, *A complete equational theory for quantum circuits* | R2, R3 | ⬜ |
| | 3 | Clément, Delorme & Perdrix 2023, *Minimal equational theories for quantum circuits* | R3 | ⬜ |

---

## 5. Vigilancia bibliográfica

Resúmenes semanales automáticos de arXiv en `notas/arxiv-semanal/` (rutina en la nube «ALRCC — resumen semanal de arXiv», sábados 08:00 UTC, push a master; gestionar en https://claude.ai/code/routines/trig_01NUAUyKrysKZsjKxrAE511f).

**arXiv.** `quant-ph` (filtrada con [SciRate](https://scirate.com) o por palabras clave), `cs.LO`, `cs.PL`, `cs.ET`; `cs.CR` filtrada por «quantum»; `math.CT` ocasional.
Palabras clave: `Toffoli`, `reversible circuit`, `circuit rewriting`, `equational theory`, `ZX-calculus`, `phase polynomial`, `T-count`, `multi-controlled`, `relative-phase`.

**Revistas.** Principales: *Quantum*, *ACM Trans. Quantum Computing*, *Logical Methods in CS*, *Math. Structures in CS*, *IEEE TCAD*. Secundarias: *PRX Quantum*, *npj QI*, *Quantum Sci. Technol.*, *Quantum Inf. Process.*, *IEEE TQE*.

**Congresos.** QPL (EPTCS) y Reversible Computation (LNCS) como clave; LICS, FSCD, POPL/PLDI; TQC, IEEE QCE, DAC/DATE/ICCAD; PQCrypto y Eurocrypt/Asiacrypt para O8.

**Autores y grupos.** ZX: Kissinger, van de Wetering, Backens, Perdrix, Vilmart, Jeandel, Carette. Teorías ecuacionales: Clément, Heurtel, Mansfield, Valiron. Toffoli/CNOT categórico: Cockett, Comfort. Optimización: Amy, Maslov, Mosca, Selinger, Ross, Wille, Burgholzer (MQT). Reversible: Heunen, Kaarsgaard. Criptografía: Jaques, Naehrig, Roetteler, Grassl, Langenberg.

**Alertas (configurar a mano).**
- [ ] Google Scholar: citas a Escánez-Expósito et al. 2025, Backens 2014 y Cockett & Comfort 2018.
- [ ] RSS de *Quantum* y de las categorías cs.LO y cs.ET de arXiv.
- [ ] Lista de publicaciones de [zxcalculus.com](https://zxcalculus.com).

---

## 6. Inicios recuperados

Cada vez que aparezca un intento anterior se añade una entrada aquí y se guarda en la carpeta que corresponda.

| Fecha | Origen | Qué aporta | Dónde está |
|---|---|---|---|
| 2024 | Comunicación JNIC 2024 (`reina2024ix`), *Optimización de circuitos cuánticos para la implementación de criptología cuántica* | Primer antecedente publicado | solo en `src/bibliography.bib` (falta PDF) |
| 2025 | Artículo con el grupo de la ULL, *Phys. Scr.* 100 025107 | Punto de partida publicado | `referencias/Algebraic language ….pdf` (falta entrada BibTeX) |
| 2026-05-26 | Traspaso del trabajo previo (git) | Manuscrito LaTeX en inglés | `src/*.tex` |
| 2026-05-30 | Roadmap y presentación (git) | `roadmap.bib`, `presentation.tex`, objetivos O1–O8 | `src/`, `entregas/presentation.pdf` |
| 2026-06-11 | Análisis crítico rev. 2 | Verificación matemática, R0–R8, **plan de lectura con plazos** | `src/critical_analysis.tex`, `entregas/critical_analysis.pdf` |
| 2026-06-13 | Traducción al español y revisión de notación/ket (git) | Avance de R0 | `src/notation.tex`, `src/ket.tex` |
| ? | Chat con Claude sobre la librería Mathematica | Notación adoptada (ket a la derecha, controles negativos $A^{\Gamma_1,\Gamma_0}_\Lambda$), estructura `QuantumAlgebra/`, tareas y código pendiente | `resumen-circuitos-cuanticos.md` |

---

## 7. Por localizar

- [ ] Librería Mathematica `QuantumAlgebra/` (`Core.wl`, `Gates.wl`, `Controlled.wl`, `Simplify.wl`, `Tests.wl`). No está en este equipo. → guardar en `mathematica/`.
- [ ] Otros chats o resúmenes de intentos anteriores. → guardar en `notas/`.
- [ ] PDF de los papers marcados ⬜ en el plan de lectura. → `referencias/`.
- [ ] Fecha y contexto del chat de Mathematica.
- [ ] Añadir a `src/bibliography.bib` la entrada del artículo de *Physica Scripta* 2025 (el análisis crítico cita como base `reina2024ix`, que es la comunicación de JNIC 2024).

---

## 8. Próximo paso

1. Revisar qué apartados de R0 quedan pendientes tras los commits de junio y cerrarlos.
2. Leer Backens 2014 (PDF ya disponible) para seguir con la Fase 1.
3. Seguir localizando inicios y apuntarlos en la sección 6.
