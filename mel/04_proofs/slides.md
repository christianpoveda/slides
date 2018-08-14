% Demostraciones en la lógica proposicional
% Matemática estructural y lógica
% ISIS-1104

---
header-includes:
- \usepackage{examplep}
- \usepackage{bm}
- \newcommand{\then}{\Rightarrow}
---


## Nombres, nombres everywhere

. . .

::: incremental

- Un __axioma__ es una proposición que se __asume__ cierta.
- Un __teorema__ es una proposición que se __demuestra__.
- Un __lema__ es un teorema __chiquito__.
- Una __demostración__ es una __derivación__.
:::

## Axiomas... y eso para qué?

. . .

Los axiomas que vamos a ver acá son equivalencias
$$LHS \equiv RHS$$

. . .

y se utilizan de la siguiente forma:
$$\text{Siempre que vea } LHS \text{ lo puedo reemplazar por } RHS$$
$$\text{Siempre que vea } RHS \text{ lo puedo reemplazar por } LHS$$

. . .

Es decir, son como __reglas de inferencia__ pero __bidireccionales__.

## Axiomas de la lógica proposicional

. . .

::: incremental

- Conmutatividad
\begin{align*}
    p \lor q &\equiv q \lor p \\
    p \land q &\equiv q \land p \\
\end{align*}
- Asociatividad
\begin{align*}
    (p \lor q) \lor r &\equiv q \lor (p \lor r) \\
    (p \land q) \land r &\equiv q \land (p \land r) \\
\end{align*}
- Absorción
\begin{align*}
    p \land (p \lor q) &\equiv p \\
    p \lor (p \land q) &\equiv p \\
\end{align*}
:::

## Axiomas de la lógica proposicional

. . .

::: incremental

- Distribución
\begin{align*}
    p \land (q \lor r) &\equiv (p \land q) \lor (p \land r) \\
    p \lor (q \land r) &\equiv (p \lor q) \land (p \lor r) \\
\end{align*}
- Todo o nada
\begin{align*}
    p \land \lnot p &\equiv False \\
    p \lor \lnot p &\equiv True \\
\end{align*}
- Identidad
\begin{align*}
    p \lor False &\equiv p \\
    p \land True &\equiv p \\
\end{align*}
:::

## Axiomas de la lógica proposicional

. . .

::: incremental

- Piso, techo
\begin{align*}
    p \land False &\equiv False \\
    p \lor True &\equiv True \\
\end{align*}
- Idempotencia
\begin{align*}
    p \land p &\equiv p \\
    p \lor p &\equiv p \\
\end{align*}
- Doble negación
$$ \lnot \lnot p \equiv p$$
:::

## Axiomas de la lógica proposicional

. . .

::: incremental

- Leyes de De Morgan
\begin{align*}
    \lnot (p \land q) &\equiv (\lnot p \lor \lnot q) \\
    \lnot (p \lor q) &\equiv (\lnot p \land \lnot q) \\
\end{align*}
:::

##
\begin{center}
    \includegraphics[height=0.75\paperheight]{images/orly.png}
\end{center}

## Ejemplo: Probando una equivalencia

. . .

Demuestre que $p \equiv (p \land q) \lor (p \land \lnot q)$

. . .

__Demostración:__

. . .

Tenemos dos opciones

. . .

- Partiendo de $p$ usar axiomas hasta llegar a $(p \land q) \lor (p \land \lnot q)$.

. . .

- Partiendo de $(p \land q) \lor (p \land \lnot q)$ usar axiomas hasta llegar a $p$.

. . .

Usualmente la segunda es más fácil.

## Ejemplo: Probando una equivalencia

. . .

::: incremental

- Partimos de
$$ (p \land q) \lor (p \land \lnot q) $$
- Usando distribución
$$(p \land q) \lor (p \land \lnot q) \equiv p \lor (q \land \lnot q)$$
- Usando todo o nada
$$p \lor (q \land \lnot q) \equiv p \lor False$$
- Usando identidad
$$p \lor False \equiv p$$
- Luego concluimos que
$$(p \land q) \lor (p \land \lnot q) \equiv p$$
:::

## Ejemplo: Probando una equivalencia

. . .

::: incremental

- Otra forma de escribir esta prueba es
\begin{align*}
    (p \land q) \lor (p \land \lnot q) & \equiv p \lor (q \land \lnot q) \tag{distribución} \\
    &\equiv p \lor False \tag{todo o nada} \\
    &\equiv p \tag{identidad} \\
\end{align*}
- Tras bastidores simplemente estamos mostrando que $p \equiv (p \land q) \lor (p \land \lnot q)$
es __verdadera__ sin importar que valores puedan llegar a tomar $p$ y $q$.
- Cuando una proposición es verdadera __siempre__, decimos que es una __tautología__.
:::

## Ejercicio: Probando otra equivalencia

. . .

- Ahora ustedes demuestren que $\lnot q \lor (p \land q) \equiv \lnot q \lor p$
\vspace*{165 pt}

##

\begin{center}
...que pasa cuando me piden probar algo que no es una equivalencia?
\end{center}

## Pruebas en general

. . .

::: incremental

- Pedir una demostración de $p$ es lo mismo que pedir una demostración de que $p$ es una __tautología__.
- En otras palabras, basta mostrar que a partir de $p$ puedo llegar a $True$.
$$p \equiv True$$
:::

## Ejemplo

. . .

Demuestre que $p \land (p \then q) \then q$

. . .

__Demostración:__
\begin{align*}
    p \land (p \then q) \then q &\equiv p \land (\lnot p \lor q) \then q \tag{def. $\then$} \\
    &\equiv (p \land \lnot p) \lor (p \land q) \then q \tag{distribución}\\
    &\equiv False \lor (p \land q) \then q \tag{todo o nada}\\
    &\equiv (p \land q) \then q \tag{identidad}\\
    &\equiv \lnot (p \land q) \lor q \tag{def. $\then$}\\
    &\equiv (\lnot p \lor \lnot q) \lor q \tag{De Morgan}\\
    &\equiv \lnot p \lor (\lnot q \lor q) \tag{asociatividad}\\
    &\equiv \lnot p \lor True \tag{todo o nada}\\
    &\equiv True \tag{piso, techo}\\
\end{align*}

## Ejercicio

. . .

- Ahora ustedes demuestren que $p \land q \then p$
\vspace*{165 pt}
