
## Matemática estructural y lógica

ISIS-1104

---

## Sistemas formales

+++

### ¿Para qué?

Para razonar sobre la correctitud de las cosas
```java
int public signo(int x) {
    if (x > 0) {
        return 1
    } else {
        return 0;
    }
}
```

+++

### ¿Qué es?
Un sistema formal está constituido por dos partes:
@ul
- Un lenguaje formal
- Un aparato deductivo
@ulend

+++

### Lenguaje formal
A su vez un lenguaje formal esta constituido por:
@ul
- Una colección de simbolos, el __alfabeto__ (usualmente denotado por `\(A\)`).
- Una serie de reglas que nos indican como combinar simbolos, la __sintaxis__.
@ulend

+++

@ul
- Una sucesión de símbolos del alfabeto es una __fórmula__.
- Una fórmula que sigue la __sintaxis__ es una __fórmula bien formada (fbf)__.
@ulend

+++

### Ejemplo

Los números decimales:
@ul
- El alfabeto: `\(A = \{0, 1, 2, 3, 4, 5, 6, 7, 8, 9, .\}\)`
- La sintaxis: Una fbf es toda aquella que esté compuesta de dos sucesiones de números separadas por un punto.
@ulend

+++

### Ejemplo

@ul
- Fórmulas bien formadas:
    - `\(1.4142\)`
    - `\(32.04\)`
    - `\(1234.0\)`
- Fórmulas inválidas:
    - `\(12341\)`
    - `\(132.432.23\)`
    - `\(.123\)`
@ulend

+++

