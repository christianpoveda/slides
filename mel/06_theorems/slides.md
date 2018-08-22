% Teoremas y demostraciones
% Matemática estructural y lógica
% ISIS-1104

---
header-includes:
- \usepackage{examplep}
- \usepackage{bm}
- \newcommand{\then}{\Rightarrow}
---

## Contrapositiva

. . .

__Teorema:__
$$p \then q \equiv \lnot q \then \lnot p$$

. . .

__Demostración:__

. . .

\begin{align*}
    p \then q &\equiv \lnot p \lor q \tag{definición $\then$} \\
              &\equiv q \lor \lnot p \tag{conmutativad} \\
              &\equiv \lnot \lnot q \lor \lnot p \tag{doble negación} \\
              &\equiv \lnot q \then \lnot p \tag{definición $\then$} \\
\end{align*}

## Contrapositiva: caso de uso

. . .

Demuestre que
$$(p \then q) \land (\lnot p \then r) \land (r \then s) \then (\lnot q \then s)$$

. . .

__Demostración:__

. . .

::: incremental

- Usando contrapositiva con $p \then q$
$$\frac{(p \then q)}{\lnot q \then \lnot p} \tag{1}$$
- Usando silogismo hipotético entre $(1)$ y $\lnot p \then r$
$$\frac{(\lnot q \then \lnot p) \land (\lnot p \then r)}{\lnot q \then r} \tag{2}$$
- Usando silogismo hipotético entre $(2)$ y $r \then s$
$$\frac{(\lnot q \then r) \land (r \then s)}{\lnot q \then s}$$
:::

## Contrapositiva: ejercicio

. . .

Demuestre que
$$(p \then \lnot q) \land (r \then q) \land r \then \lnot p$$
\vspace*{165 pt}

## Moviendo hipótesis

. . .

__Teorema:__
$$p \then (q \then r) \equiv p \land q \then r$$

. . .

__Demostración:__

. . .

\begin{align*}
    p \land q \then r &\equiv \lnot (p \land q) \lor r \tag{definición $\then$} \\
                  &\equiv \lnot p \lor \lnot q \lor r \tag{De Morgan} \\
                  &\equiv \lnot p \lor (q \then r) \tag{definición $\then$} \\
                  &\equiv p \then (q \then r) \tag{definición $\then$} \\
\end{align*}

## Moviendo hipótesis: caso de uso

. . .

Demuestre que
$$(p \then q) \land (q \then r) \then (p \then r)$$

. . .

__Demostración:__

. . .

::: incremental

- Moviendo hipótesis
$$(p \then q) \land (q \then r) \then (p \then r) \equiv (p \then q) \land (q \then r) \land p \then r$$
- Usando Modus ponens
$$\frac{(p \then q) \land (q \then r) \land p \then r}{q \land (q \then r)}$$
- Usando Modus ponens
$$\frac{q \land (q \then r)}{r}$$
:::

## Moviendo hipótesis: ejercicio

. . .

Demuestre que
$$((p \then q) \then r) \then (p \then (q \then r))$$
\vspace*{165 pt}

## Doble implicación

. . .

__Teorema:__
$$(p \equiv q) \equiv (p \then q) \land (q \then p)$$

. . .

__Demostración:__

. . .

\begin{center}
  \begin{tabular}{ | c | c | c | c | c | c |}
    \hline
      $p$     & $q$     & $p \then q$ & $q \then p$ & $(p \then q) \land (q \then p)$ & $p \equiv q$ \\ \hline
      $True$  & $True$  & $True$      & $True$      & $True$                      & $True$  \\
      $True$  & $False$ & $False$     & $True$      & $False$                     & $False$ \\
      $False$ & $True$  & $True$      & $False$     & $False$                     & $False$ \\
      $False$ & $False$ & $True$      & $True$      & $True$                      & $True$  \\
    \hline
  \end{tabular}
\end{center}

## Doble implicación: caso de uso

. . .

Demuestre que
$p \land (p \equiv q) \then q$

. . .

__Demostración:__

. . .

::: incremental

- Usando doble implicación
$$\frac{p \land (p \equiv q)}{p \land (p \then q) \land (q \then p)} \tag{1} $$
- Usando simplificación en $(1)$
$$\frac{p \land (p \then q) \land (q \then p)}{p \land (p \then q)} \tag{2} $$
- Usando Modus Ponens en $(2)$
$$\frac{p \land (p \then q)}{q}$$
:::

## Doble implicación: ejercicio

. . .

Demuestre que
$$(\lnot p \equiv q) \equiv (p \equiv \lnot q)$$
\vspace*{165 pt}
