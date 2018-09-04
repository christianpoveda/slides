% Traducciones de lenguaje natural
% Matemática estructural y lógica
% ISIS-1104

---
header-includes:
- \usepackage{examplep}
- \usepackage{bm}
- \newcommand{\then}{\Rightarrow}
---

## Un ejemplo

. . .

Verifiquemos la correctitud del siguiente argumento:

. . .

_"Si juego fútbol, quedo cansado. Voy a usar la lavadora si quedo cansado. No usé la lavadora. Luego, no jugué fútbol."_

. . .

- Primero, le asignamos __letras proposicionales__ a las afirmaciones __más básicas__:
\begin{align*}
    p &\equiv \text{Juego fútbol} \\
    q &\equiv \text{Quedo cansado} \\
    r &\equiv \text{Uso la lavadora} \\
\end{align*}

## Un ejemplo

. . .

::: incremental

- Luego, componemos cada una de las oraciones de nuestro argumento como __proposiciones__:
\begin{align*}
    \text{Si juego fútbol, quedo cansado} &\equiv p \then q \\
    \text{Voy a usar la lavadora si quedo cansado} &\equiv q \then r \\
    \text{No usé la lavadora} &\equiv \lnot r \\
    \text{No jugué fútbol} &\equiv \lnot p \\
\end{align*}
- Ahora unimos las proposiciones:
$$(p \then q) \land (q \then r) \land (\lnot r)\then (\lnot p)$$
- Para terminar, __verificamos__ si ésta proposición es una __tautología__ ya sea con una __tabla de verdad__ o con una __demostración__.
:::

## Algunas frases comunes

. . .

::: incremental

- $\lnot p$
    - No $p$
    - No es cierto $p$
- $p \land q$
    - $p$ y $q$.
    - $p$ pero $q$.
- $p \lor q$:
    - $p$ o $q$
- $p \then q$
    - Si $p$, entonces $q$.
    - $q$, si $p$.
    - $p$ implica $q$
- $p \equiv q$
    - $p$ es lo mismo que $q$
    - $p$ es equivalente a $q$
:::

## Ejercicio

. . .

Verifiquen la correctitud del siguiente argumento

_"En las noches, yo duermo o alucino. No estoy durmiendo. Yo veo elefantes rosados si alucino. Por lo tanto, veo elefantes rosados"_
\vspace*{165 pt}
