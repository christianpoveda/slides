definicion de tipos -> what?, why? un slide que sea "ustedes se han enfrentado a un sistema de tipos, entidades que restringen blah blah" (1 slide)
Mostrar un sistema de tipos :P

contexto:
    rust -> que es rust?
            tipos en rust?
problema:  Ejemplo de algo que no se pueda hacer sin bounded const generics.

definición del problema: ponerle BCG a Rust arregla todo. what's BCG? (2 slides)
           mostrar como el ejemplo de arriba se arregla (como se vería al final)

related work: 
           Conectar BCG con dependent types: CG < BCG < BGC + Runtime = Dependent Types (1 slide)
           Lit review: Dependent Types: (1 slide)
            Lenguaje 
            Haskell [referencias]
            Idris [referencias]
            Agda [referencias]
            Coq [referencias]
            Nuevos lenguajes
            En los ultimos 3 años estos son los papers que hay en [PLDI, POPL, IQ, OOPSLA]
           Explicar Idris (1+ slide): How it works, what it can do

           Const generics en Rust: Progreso actual (1 slide)
           
Road ahead: (2+ slides)
            - Deconstruir ejemplo para mostrar que hace falta hacer
            - Unficacion de expresiones (Que opciones hay)
Validacion:
            - verificación formal en teoría de tipos o algo que haga la prueba por mi
            - aplicaciones y ejemplos: Listas, ejemplos de los otros langs
            - PR a Rust

Cronograma

maximo 15 slides
