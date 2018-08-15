% Lógica proposicional
% Matemática estructural y lógica
% ISIS-1104

---
header-includes:
- \usepackage{examplep}
- \usepackage{bm}
- \usepackage{nicefrac}
---

# Lógica como sistema formal

## Lógica como lenguaje formal

. . .

::: incremental

- El alfabeto:
$$A = \{\lnot, \land, \lor, (, ), True, False, p, q, r, s, ...\}$$
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

. . .

::: incremental

- Todas las __fórmulas__ representan __proposiciones__ o __afirmaciones__.
- $True$/$False$ representa la proposición que siempre es verdadera/falsa.
- $p$, $q$, $r$, ... son __variables proposicionales__ y pueden usarse para representar cualquier proposición.
$$p\equiv\textrm{hoy está lloviendo}$$
- $\lnot$, $\land$ y $\lor$ son __operaciones lógicas__.
- para entender el significado de las operaciones lógicas hacemos uso de __tablas de verdad__.
:::

## El operador $\lnot$

. . .

::: incremental

- Si $p$ es una proposición cualquiera, $\lnot p$ representa la __negación de $p$__ o simplemente __no $p$__.
- Su tabla de verdad es:
\begin{center}
  \begin{tabular}{ | c | c | }
    \hline
    $p$     & $\lnot p$ \\ \hline
    $True$  & $False$   \\
    $False$ & $True$    \\
    \hline
  \end{tabular}
\end{center}
- Ejemplo:
\begin{align*}
    p &\equiv \textrm{ahora está lloviendo} \\
    \lnot p &\equiv \textrm{ahora no está lloviendo} \\
\end{align*}
:::

## El operador $\land$

. . .

::: incremental

- Si $p$ y $q$ son dos proposiciones, $(p \land q)$ representa la __conjunción entre $p$ y $q$__ o simplemente __$p$ y $q$__.
- Su tabla de verdad es: \vspace*{10px}
\begin{center}
  \begin{tabular}{ | c | c | c | }
    \hline
      $p$     & $q$     & $(p \land q)$ \\ \hline
      $True$  & $True$  & $True$  \\
      $True $ & $False$ & $False$ \\
      $False$ & $True$  & $False$ \\
      $False$ & $False$ & $False$ \\
    \hline
  \end{tabular}
\end{center}
- Ejemplo:
\begin{align*}
    p &\equiv \textrm{ahora está lloviendo} \\
    q &\equiv \textrm{tengo mi sombrilla} \\
    p \land q &\equiv \textrm{ahora está lloviendo y tengo mi sombrilla} \\
\end{align*}
:::

## El operador $\lor$

. . .

::: incremental

- Si $p$ y $q$ son dos proposiciones, $(p \lor q)$ representa la __disyunción entre $p$ y $q$__ o simplemente __$p$ o $q$__.
- Su tabla de verdad es: \vspace*{10px}
\begin{center}
  \begin{tabular}{ | c | c | c | }
    \hline
      $p$     & $q$     & $(p \land q)$ \\ \hline
      $True$  & $True$  & $True$  \\
      $True $ & $False$ & $True$  \\
      $False$ & $True$  & $True$  \\
      $False$ & $False$ & $False$ \\
    \hline
  \end{tabular}
\end{center}
- Ejemplo:
\begin{align*}
    p &\equiv \textrm{ahora está lloviendo} \\
    q &\equiv \textrm{tengo mi sombrilla} \\
    p \lor q &\equiv \textrm{ahora está lloviendo o tengo mi sombrilla} \\
\end{align*}
:::

## Combinando operadores

. . .

::: incremental

- Ahora podemos decidir el __valor de verdad__ de cualquier __fórmula__ de nuestro lenguaje.
- Por ejemplo, la tabla de verdad de $(\lnot p \land q)$: \vspace*{10px}
\begin{center}
  \begin{tabular}{ | c | c | c | c | }
    \hline
      $p$     & $q$     & $\lnot p$ & $(\lnot p \land q)$ \\ \hline
      $True$  & $True$  & $False$   & $False$       \\
      $True$  & $False$ & $False$   & $False$       \\
      $False$ & $True$  & $True$    & $True$        \\
      $False$ & $False$ & $True$    & $False$       \\
    \hline
  \end{tabular}
\end{center}
:::

## Combinando operadores

- Ahora ustedes calculen la tabla de verdad de $(\lnot p \lor q)$
\vspace*{165 pt}

## Extendiendo nuestro lenguaje

. . .

::: incremental
- Si $p$ y $q$ son dos proposiciones, $(p \Rightarrow q)$ representa el __condicional material entre $p$ y $q$__ o simplemente __si $p$ entonces $q$__.
- Su tabla de verdad es: \vspace*{10px}
\begin{center}
  \begin{tabular}{ | c | c | c | }
    \hline
      $p$     & $q$     & $(p \Rightarrow q)$ \\ \hline
      $True$  & $True$  & $True$  \\
      $True $ & $False$ & $False$  \\
      $False$ & $True$  & $True$  \\
      $False$ & $False$ & $True$ \\
    \hline
  \end{tabular}
\end{center} \vspace*{10px}
- Hay que tener cuidado con la interpretación:
    - Si Colombia gana el próximo mundial, entonces Bogotá queda en Sudamérica.
    - Si ahora está lloviendo, entonces yo tengo mi sombrilla.
:::

## Otra extensión: Equivalencias

. . .

::: incremental

- Como $(\lnot p \lor q)$ y $(p \Rightarrow q)$ siempre tienen el __mismo valor de verdad__, decimos que son __equivalentes__.
$$((\lnot p \lor q) \equiv (p \Rightarrow q))$$
- Sin embargo son __fórmulas__ distintas porque estan construidas con distintos __símbolos__.
- La tabla de verdad de $(p \equiv q)$ es: \vspace*{10 px}
\begin{center}
  \begin{tabular}{ | c | c | c | }
    \hline
      $p$     & $q$     & $(p \equiv q)$ \\ \hline
      $True$  & $True$  & $True$  \\
      $True $ & $False$ & $False$  \\
      $False$ & $True$  & $False$  \\
      $False$ & $False$ & $True$ \\
    \hline
  \end{tabular}
\end{center}
:::

## El resultado final

. . .

::: incremental

- El alfabeto:
$$A = \{\lnot, \land, \lor, \Rightarrow, \equiv, (, ), True, False, p, q, r, s, ...\}$$
- La sintaxis:
\begin{align*}
    \PVerb{sentence} &\rightarrow \PVerb{atomic_sentence} \mid \PVerb{complex_sentence} \\
    \PVerb{atomic_sentence} &\rightarrow \bm{True} \mid \bm{False} \mid \bm{p} \mid \bm{q} \mid \bm{r} \mid \bm{s} \mid ... \\
    \PVerb{complex_sentence} &\rightarrow  \PVerb{unary_op}\ \PVerb{sentence} \\
    \PVerb{complex_sentence} &\rightarrow  \bm{(} \PVerb{sentence}\ \PVerb{binary_op}\ \PVerb{sentence} \bm{)}\\
    \PVerb{unary_op} &\rightarrow \bm{\lnot} \\
    \PVerb{binary_op} &\rightarrow \bm{\land} \mid \bm{\lor} \mid \bm{\Rightarrow} \mid \bm{\equiv} \\
\end{align*}
:::

# De la lógica proposicional, los paréntesis y otros demonios

## El problema

. . .

::: incremental

- Tengamos en cuenta la siguiente fórmula bien formada
$$((((\lnot p \land q) \land r) \Rightarrow ((r \lor t) \lor u)) \land v)$$
- El uso de paréntesis hace difícil su lectura, entonces
$$\lnot p \land q \land r \Rightarrow r \lor t \lor u \land v$$
- Necesitamos una convención para evitar ambigüedad.
:::

## Precedencia de operadores

. . .

Tomaremos una convención prestada de la aritmética

. . .

::: incremental

- Las operaciones $*$ y $/$ tienen precedencia sobre $+$ y $-$:
$$ 2 * 3 + 5 = (2 * 3) + 5$$
$$ 6 - 8 / 2 = 6 - (8 / 2)$$
- Las operaciones con la misma precedencia son asociativas a izquierda:
$$ 2 - 3 + 5 = (2 - 3) + 5 $$
$$ 10 / 5 * 2 = (10 / 5) * 2 $$
:::

## Precedencia de operadores

. . .

::: incremental

- La precedencia de operadores lógicos que tomaremos es
$$\lnot \textrm{ precede a } \nicefrac{\land}{\lor} \textrm{ precede a } \Rightarrow \textrm{ precede a } \equiv$$
- Las operaciones son asociativas a izquierda.
- Ejemplo
$$p \Rightarrow \lnot q \land r \lor s \textrm{ es lo mismo que } (p \Rightarrow ((\lnot q \land r) \lor s))$$
- Dado que esto es una convención, no lo incluiremos dentro de la sintaxis de nuestro lenguaje.
:::
