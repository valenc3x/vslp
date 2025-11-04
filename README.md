Very Simple Language Parser
====

Descripción del Lenguaje
---
Define en una sola sintaxis elementos de HTML y CSS utilizando objetos que describen carateristicas de tags de HTML y reglas de CSS

Detecta errores de token inválidos, errores de sintaxis y uso invalido de objetos no definidos

Descripción del compilador/intérprete
---

  Python 2.7 con los modulos de expresiones regulares
  
  No se utilizan librerías externas.

Descripción de análisis léxico
------------
Patrones de construcción

```
    INISET   =  \#set
    NAMETAG  =  \:
    SET      =  set
    STYLE    =  style
    EQUALS   =  \=
    ENDSET   =  \#endset
    LPAR     =  \(
    RPAR     =  \)
    COMMA    =  \,
    APOS     =  \'
    DOTCOMMA =  \;
    INITEMP  =  \#template
    ENDTEMP  =  \#endtemplate
    ININEST  =  \{\%
    ENDNEST  =  \%\}
    FOR      =  for
    SELE     =  \#|\.\w+
    NUM      =  [1-9][0-9]*
    ID       =  (-|\w)+
    LKEY     =  \{
    RKEY     =  \}
```

Descripción de análisis sintáctico
---
Gramática Formal

```mermaid
graph TD
    A["A"] --> S["S"]
    A --> C["C"]
    S --> C
    S --> D["#set : id D"]
    D --> E["set id = E D"]
    D --> Y["style = id Y D"]
    D --> ENDSET["#endset"]
    E --> J1["set ( id J"]
    Y --> J2["style ( 'selector' J"]
    J1 --> J3["J"]
    J2 --> J3
    J3 --> J4[", id : id J"]
    J3 --> SEMI[") ;"]
    J4 --> J3
    C --> T["#template : id T"]
    T --> B1["B #endtemplate"]
    T --> ENDTEMPLATE["#endtemplate"]
    B1 --> B["B"]
    B --> I1["{% id I"]
    B --> FOR["for ( num , num ) { B }"]
    I1 --> I2["B %}"]
    I1 --> CLOSE["%}"]
    I2 --> B
```

Se utilizó un parser LL de implementación propia. Se realiza análisis de First y Follow, se crea la tabla de parseo y se realiza el análisis semántico, al tiempo que se genera la entrada para análisis semantico.

Descripción de análisis semántico y generación de código intermedio
---
Luego del análisis sintáctico, pasamos la entrada a código intermedio con representación de cuadruplos, en donde se lleva un control de las variables declaradas y se detecta error en caso de usar variables no declaradas previamente.

Se diseñaron cuadruplos para la representación intermedia del código de entrada y se muestran al final del análisis


Descripción del ejecutor
---
*Coming soon*

