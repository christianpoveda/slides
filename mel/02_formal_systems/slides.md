% Sistemas formales
% Matemática estructural y lógica 
% ISIS-1104

---
header-includes:
- \usepackage{examplep}
- \usepackage{bm}
---

## ¿Para qué?

. . .

Para razonar sobre la correctitud de las cosas

. . . 

```java
int public signo(int x) {
    if (x #= 0) {
        return 1
    } else {
        return -1;
    }
}
```

. . .

¿Qué está mal con este código?


# Lenguajes formales

## Ejemplo: El lenguaje de los decimales

. . .

- Cosas que son decimales
    - $1.46$
    - $32.04$
    - $1234.0$

. . .

- Cosas que __no__ son decimales:
    - $12341$
    - $132.432.23$
    - $.123$

## Ejemplo: El lenguaje de los decimales

. . . 

::: incremental
- Un decimal es un número, seguido por un punto, seguido por otro número.
$$\PVerb{decimal} \rightarrow \PVerb{numero}\ \bm{.}\ \PVerb{numero}$$
- A su vez, un número puede ser, o un dígito
$$\PVerb{numero} \rightarrow \PVerb{digito}$$
- O un dígito seguido de otro número
$$\PVerb{numero} \rightarrow \PVerb{digito}\  \PVerb{numero}$$
- Finalmente, un dígito es un caracter entre 0 y 9
$$\PVerb{digito} \rightarrow \bm{0} \mid \bm{1} \mid \bm{2} \mid \bm{3} \mid \bm{4} \mid \bm{5} \mid \bm{6} \mid \bm{7} \mid \bm{8} \mid \bm{9}$$
:::

## Ejemplo: El lenguaje de los decimales

. . . 

¿Es $1.46$ un decimal?

. . . 

\begin{tikzpicture}[sibling distance=10em,
  every node/.style = {shape=rectangle, rounded corners,
    draw, align=center,
    top color=white, bottom color=blue!20}]
  \node {decimal \\ $1.46$}
    child { 
        node { numero \\ $1$ }
        child { node { digito \\ $\bm{1}$ } }
        }
    child { node {$\bm{.}$} }
    child { 
        node { numero \\ $46$ } 
        child { node { digito \\ $\bm{4}$ } }
        child { 
            node { numero \\ $6$ }
            child { node { digito \\ $\bm{6}$ } }
            }
        };
\end{tikzpicture}

## Ejemplo: El lenguaje de los decimales

. . .

Ahora ustedes ¿Es $32.5.1$ un decimal?
\vspace*{165 pt}

## Ejemplo: El lenguaje de los decimales

. . .

::: incremental

- $\{0, 1, 2, 3, 4, 5, 6, 7, 8, 9, .\}$ son los __símbolos terminales__.
- $\{\PVerb{decimal}, \PVerb{numero}, \PVerb{digito}\}$ son los __símbolos auxiliares__.
- `decimal` es el __símbolo inicial__. 
- Y estas son __producciones__:
\begin{align*}
    \PVerb{decimal} &\rightarrow \PVerb{numero}\ \bm{.}\ \PVerb{numero} \\
    \PVerb{numero} &\rightarrow \PVerb{digito} \\
    \PVerb{numero} &\rightarrow \PVerb{digito}\  \PVerb{numero} \\
    \PVerb{digito} &\rightarrow \bm{0} \mid \bm{1} \mid \bm{2} \mid \bm{3} \mid \bm{4} \mid \bm{5} \mid \bm{6} \mid \bm{7} \mid \bm{8} \mid \bm{9} \\
\end{align*}
- Este conjunto de conceptos conforman una __forma normal__.
:::

## Definiciones

. . .

::: incremental
- Un lenguaje formal esta constituido por:
    - Una colección de _simbolos_, el __alfabeto__ (usualmente denotado por $A$).
    - Una serie de reglas que nos indican como combinar simbolos (usualmente una _forma normal_), la __sintaxis__.
- Una sucesión de símbolos del alfabeto es una __fórmula__.
- Una fórmula que sigue la __sintaxis__ es una __fórmula bien formada__.
:::

# Semántica

## Ejemplo: Los números naturales

. . .

::: incremental

- El alfabeto: 
$$A = \{zero, succ, (, )\}$$
- La sintaxis: 
$$\PVerb{natural} \rightarrow \bm{zero} \mid \bm{succ} \bm{(} \PVerb{natural} \bm{)}$$
- Algunas fbf: 
    - $zero$
    - $succ(zero)$
    - $succ(succ(zero))$
    - ...
:::

## Ejemplo: Los números naturales

. . . 

::: incremental

- Sabemos que $zero$ representa al número $0$.
$$I(zero) = 0$$
- Sabemos que $succ(zero)$ representa al siguiente número, $1$.
$$I(succ(zero)) = 1$$
- Sabemos que $succ\ \PVerb{natural}$ representa al sucesor de \PVerb{natural}.
$$I(succ(\PVerb{natural})) = 1 + I(\PVerb{natural})$$
- Esto es una __semántica__ para este lenguaje, le dá un significado.
:::

## Ejercicio: Los números binarios

. . .

Escriba una semántica para el siguiente lenguaje

. . .

- El alfabeto: 
$$A = \{0, 1\}$$
- La sintaxis: 
\begin{align*}
    \PVerb{binario} &\rightarrow \PVerb{digito} \\
    \PVerb{binario} &\rightarrow \PVerb{digito}\ \PVerb{binario} \\
    \PVerb{digito} &\rightarrow \bm{0} \mid \bm{1} \\
\end{align*}

. . .

Para que se pueda interpretar como números, es decir:
$$I(110) = 6$$

# Aparato deductivo

## Ejemplo: Los naturales con la suma

. . . 

::: incremental

- El alfabeto: 
$$A = \{zero, succ, (, ), plus\}$$
- La sintaxis: 
\begin{align*}
    \PVerb{nat_sum} &\rightarrow \PVerb{natural} \\
    \PVerb{nat_sum} &\rightarrow \PVerb{natural}\ \bm{plus}\ \PVerb{nat_sum} \\
    \PVerb{natural} &\rightarrow \bm{zero} \mid \bm{succ} \bm{(} \PVerb{natural} \bm{)} \\
\end{align*}
- Algunas fórmulas bien formadas:
    - $succ(succ(zero))$
    - $succ(zero)\ plus\ zero$
    - $zero\ plus\ succ(zero)\ plus\ succ(succ(zero))$
:::

## Ejemplo: Los naturales con la suma

. . .

¿Cómo transformar cualquier suma de naturales a un natural puro?

. . .

$$succ(succ(zero))\ plus\ succ(zero) \leadsto succ(succ(succ(zero)))$$

. . .

Con dos __reglas de inferencia__:

. . .

- Sumar cero no cambia nada
$$\frac{zero\ plus\ x}{x}$$

. . .

- Mover uno a la derecha
$$\frac{succ(x)\ plus\ y}{x\ plus\ succ(y)}$$

## Ejemplo: Los naturales con la suma

. . .

::: incremental

- Partiendo de
$$succ(succ(zero))\ plus\ succ(zero)$$
- Podemos mover uno a la derecha
$$succ(zero)\ plus\ succ(succ(zero))$$
- _Rinse and repeat_
$$zero\ plus\ succ(succ(succ(zero)))$$
- Sumar cero no cambia nada
$$succ(succ(succ(zero)))$$
:::

## Ejemplo: Los naturales con la suma

. . .

Ahora ustedes transformen
$$succ(zero)\ plus\ succ(succ(zero))$$
\vspace*{165 pt}

## En conclusión...

. . .

::: incremental

- Un __lenguaje formal__ es un conjunto de _simbolos_ con una _sintaxis_.
- Un __aparato deductivo__ permite transformar las _fórmulas_ de un __lenguaje__ usando _reglas de inferencia_, este proceso se conoce como __derivación__.
- Cuando un __lenguaje formal__ cuenta con un __aparato deductivo__, este pasa a ser un __sistema formal__. 
:::



