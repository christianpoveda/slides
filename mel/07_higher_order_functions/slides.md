% Funciones de alto orden
% Matemática estructural y lógica
% ISIS-1104

---
header-includes:
- \usepackage{examplep}
- \usepackage{bm}
- \newcommand{\then}{\Rightarrow}
---

Esta clase solo compila en Java 8 o superior

## Ingeniería de software 101

Supongan que tenemos el siguiente método

```java
public static List<Integer> sum2(List<Integer> lista) {
    ArrayList<Integer> nLista = new ArrayList<Integer>();
    for (Integer i: lista) {
        nLista.add(i + 2);
    }
    return nLista;
}
```

## Ingeniería de software 101

Y este otro método

```java
public static List<Integer> mul2(List<Integer> lista) {
    ArrayList<Integer> nLista = new ArrayList<Integer>();
    for (Integer i: lista) {
        nLista.add(i * 2);
    }
    return nLista;
}
```

## Ingenieria de software 101

- Estos métodos son iguales salvo la función que estoy __aplicando__ sobre los elementos de la lista.
- ¿Es posible volver ésta función __argumento__ de mi método?
- Justamente este es el problema que resuelven las funciones de __alto orden__.

## Funciones como variables

En Java 8, `Function<U, V>` es una función que recibe una variable de tipo `U` y retorna una variable de tipo `V`
```java
Function<Integer, Integer> doblar = i -> 2 * i;
Function<Integer, Boolean> esPositivo = b -> b > 0;
Function<String, Boolean> esVacio = s -> s.length() == 0;
```

## Funciones de alto orden: `map`

Tengamos en cuenta el siguiente método

```java

public static List<Integer> map(List<Integer> lista,
    Function<Integer, Integer> op) {
    ArrayList<Integer> nLista = new ArrayList<Integer>();
    for (Integer i: lista) {
        nLista.add( op.apply(i) );
    }
    return nLista;
}
```

## Funciones de alto orden: `map`

Ahora podemos rescribir `sum2` y `mul2`:
```java
public static List<Integer> sum2(List<Integer> lista) {
    return map(lista, x -> 2 + x);
}

public static List<Integer> mul2(List<Integer> lista) {
    return map(lista, x -> 2 * x);
}
```

## Funciones de alto orden: `map`

Podemos mejorar `map` aun mas

```java
public static List<Integer> map(List<Integer> lista,
    Function<Integer, Integer> fun) {
    ArrayList<Integer> nLista = new ArrayList<Integer>();
    for (Integer i: lista) {
        nLista.add( fun.apply(i) );
    }
    return nLista;
}
```

## Funciones de alto orden: `map`

Usando _generics_ podemos hacer que funcione para cualquier tipo

```java
public static <T> List<T> map(List<T> lista,
    Function<T, T> fun) {
    ArrayList<T> nLista = new ArrayList<T>();
    for (T i: lista) {
        nLista.add( fun.apply(i) );
    }
    return nLista;
}
```

## Funciones de alto orden: `map`

Ahora las siguientes funciones pueden implementarse usando `map`

```java
public static List<Boolean> negar(List<Boolean> lista) {
    return map(lista, x -> !(x));
}

public static List<String> admirar(List<String> lista) {
    return map(lista, x -> "¡" + x + "!");
}
```

## Funciones de alto orden: `filter`

Supongan que tenemos el siguiente método

```java
public static List<Integer> pos(List<Integer> lista) {
    ArrayList<Integer> nLista = new ArrayList<Integer>();
    for (Integer i: lista) {
        if (i >= 0) {
            nLista.add(i);
        }
    }
    return nLista;
}
```

## Funciones de alto orden: `filter`

Y también tenemos este otro método

```java
public static List<Integer> neg(List<Integer> lista) {
    ArrayList<Integer> nLista = new ArrayList<Integer>();
    for (Integer i: lista) {
        if (i < 0) {
            nLista.add(i);
        }
    }
    return nLista;
}
```

## Funciones de alto orden: `filter`

Necesitamos una función similar a `map`, pero que sea capaz de filtrar en vez de aplicar

```java
public static <T> List<T> filter(List<T> lista,
    Function<T, Boolean> pred) {
    ArrayList<T> nLista = new ArrayList<T>();
    for (T i: lista) {
        if( pred.apply(i) ) {
            nLista.add(i);
        }
    }
    return nLista;
}
```

## Funciones de alto orden: `filter`

Ahora podemos rescribir `pos` y `neg`:
```java
public static List<Integer> pos(List<Integer> lista) {
    return filter(lista, x -> x >= 0);
}

public static List<Integer> neg(List<Integer> lista) {
    return filter(lista, x -> x < 0);
}
```

## Funciones de alto orden: `fold`

Supongan que tenemos el siguiente método

```java
public static Integer superSuma(List<Integer> lista) {
    Integer acum = 0;
    for (Integer i: lista) {
        acum = acum + i;
    }
    return acum;
}
```

## Funciones de alto orden: `fold`

Y también tenemos este otro método

```java
public static Boolean superO(List<Boolean> lista) {
    Boolean acum = false;
    for (Boolean b: lista) {
        acum = acum || b;
    }
    return acum;
}
```

## Funciones de alto orden: `fold`

Para reescribir ambos métodos introducimos una función capaz de `reducir` una lista a un único valor
```java
  public static <T> T fold(List<T> list,
    BiFunction<T, T, T> op,
    T init) {
	T acum = init;
    for (T elem: list) {
    	acum = op.apply(acum, elem);
    }
    return acc;
  }
```

## Funciones de alto orden: `fold`

Ahora podemos rescribir `superSuma` y `superO`:
```java
public static Integer superSuma(List<Integer> lista) {
    return fold(lista, (x, y) -> x + y, 0);
}

public static List<Integer> superO(List<Integer> lista) {
    return filter(lista, (x, y) -> x || y, false);
}
```

## En resumen

Si tengo una `lista`:

- `map` me permite __aplicar__ una __función__ a todos sus elementos.
- `filter` me permite __filtrar__ sus elementos usando un __predicado__.
- `fold` me permite __acumular__ sus elementos usando una __operación__.
