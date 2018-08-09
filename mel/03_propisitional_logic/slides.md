% Lógica proposicional
% Matemática estructural y lógica 
% ISIS-1104

---
header-includes:
- \usepackage{examplep}
- \usepackage{bm}
---

# Lógica como sistema formal

## Lógica como lenguaje formal

. . .

::: incremental

- El alfabeto: 
$$A = \{\lnot, \land, \lor, (, ), p, q, r, s, ...\}$$
- La sintaxis:
\begin{align*}
    \PVerb{sentence} &\rightarrow \PVerb{atomic_sentence} \mid \PVerb{complex_sentence} \\
    \PVerb{atomic_sentence} &\rightarrow \bm{True} \mid \bm{False} \mid \bm{p} \mid \bm{q} \mid \bm{r} \mid \bm{s} \mid ... \\
    \PVerb{complex_sentence} &\rightarrow  \PVerb{unary_op}\ \PVerb{sentence} \\
    \PVerb{complex_sentence} &\rightarrow  \bm{(} \PVerb{sentence}\ \PVerb{binary_op}\ \PVerb{sentence} \bm{)}\\
    \PVerb{unary_op} &\rightarrow \bm{\lnot} \\
    \PVerb{binary_op} &\rightarrow \bm{\land} \mid \bm{\lor} \\
\end{align*}
:::

## Lógica como lenguaje formal

::: incremental

- Fórmulas bien formadas:
    - $\lnot p$
    - $(\lnot s \lor q)$
    - $(p \land \lnot r)$
    - $(p \land (q \lor r))$
    - $\lnot (p \lor q)$
- ¿Qué semántica podemos asignarle a este lenguaje?
- ¿Qué aparato deductivo podemos asignarle a este lenguaje?
:::

## Semántica

- Todas las __fórmulas__ representan __proposiciones__ o __afirmaciones__.
- $True$/$False$ representa la proposición que siempre es verdadera/falsa.
- $p$, $q$, $r$, ... son __variables proposicionales__ y pueden usarse para representar cualquier proposición.
$$p\equiv\textrm{hoy está lloviendo}$$
- $\lnot$, $\land$ y $\lor$ son __operaciones lógicas__.
- para entender el significado de las operaciones lógicas hacemos uso de __tablas de verdad__.

## El operador $\lnot$

- Si $p$ es una proposición cualquiera, $\lnot p$ representa la __negación de $p$__ o simplemente __no $p$__.

- Su tabla de verdad es:
\begin{center}
  \begin{tabular}{ | c | c | }
    \hline
    $p$ & $\lnot p$ \\ \hline
    $True$ & $False$ \\
    $False$ & $True$ \\
    \hline
  \end{tabular}
\end{center} 

- Ejemplo:
\begin{align*}
    p &\equiv \textrm{ahora está lloviendo} \\
    \lnot p &\equiv \textrm{ahora no está lloviendo} \\
\end{align*}

## El operador $\land$

- Si $p$ es una proposición cualquiera, $p \land q$ representa la __conjunción entre $p$ y $q$__ o simplemente __$p$ y $q$__.

- Su tabla de verdad es:
\begin{center}
  \begin{tabular}{ | c | c | c | }
    \hline
      $p$  & $q$ & $p \land q$ \\ \hline
      $True$  & $True$  & $True$  \\
      $True $ & $False$ & $False$  \\
      $False$ & $True$  & $False$  \\
      $False$ & $False$ & $False$  \\
    \hline
  \end{tabular}
\end{center}

- Ejemplo:
\begin{align*}
    p &\equiv \textrm{ahora está lloviendo} \\
    q &\equiv \textrm{tengo mi sombrilla} \\
    p \land q &\equiv \textrm{ahora está lloviendo y tengo mi sombrilla} \\
\end{align*}

## El operador $\lor$

- Si $p$ es una proposición cualquiera, $p \lor q$ representa la __disyunción entre $p$ y $q$__ o simplemente __$p$ o $q$__.

- Su tabla de verdad es:
\begin{center}
  \begin{tabular}{ | c | c | c | }
    \hline
      $p$  & $q$ & $p \land q$ \\ \hline
      $True$  & $True$  & $True$  \\
      $True $ & $False$ & $True$  \\
      $False$ & $True$  & $True$  \\
      $False$ & $False$ & $False$  \\
    \hline
  \end{tabular}
\end{center}

- Ejemplo:
\begin{align*}
    p &\equiv \textrm{ahora está lloviendo} \\
    q &\equiv \textrm{tengo mi sombrilla} \\
    p \land q &\equiv \textrm{ahora está lloviendo o tengo mi sombrilla} \\
\end{align*}
