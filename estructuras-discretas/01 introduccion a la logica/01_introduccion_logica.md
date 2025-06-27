---
title: 
- Introducción a la Lógica
subtitle:
- EST-1132 / Estructuras Discretas
author:
- Juan Zamora O.
classoption: t
#output: 
#  beamer_presentation:
#    citation_package: natbib
#theme:
#- Copenhagen
#date:
#- Otoño 2023
header-includes: |
    \usepackage{tikz}
    \usepackage[T1]{fontenc}
    \usepackage[utf8]{inputenc}
    \usepackage{url}
    \usepackage{colortbl}

    \setbeamertemplate{footline}{%
    \raisebox{5pt}{\makebox[0.5\paperwidth]{\hfill\makebox[20pt]{\color{black}\scriptsize\insertframenumber}}}\hspace*{5pt}}
    \newcommand{\bigCI}{\mathrel{\text{\scalebox{1.07}{$\perp\mkern-1 0mu\perp$}}}}

    \definecolor{LightRed}{RGB}{252,160,140}
    \definecolor{LightBlue}{RGB}{140,186,252}   
    
    \newcolumntype{a}{>{\columncolor{LightRed}}c}
    \newcolumntype{b}{>{\columncolor{LightBlue}}c}

    \newcommand{\empt}[2]{#1^{( #2 )}}
    \thispagestyle{empty}

    \titlegraphic { 
    \begin{tikzpicture}[overlay,remember picture]
    \node[below=-2.6cm] at (current page.south){
        \includegraphics[width=6cm]{logosAzul.png}
    };
    \end{tikzpicture}
    }
    \logo{
	\begin{tikzpicture}[overlay,remember picture]
		\node[opacity=0.4,right=-0.6cm, above=0.07cm] at ([xshift=-0.6cm]current page.south east){
    			\includegraphics[height=1cm]{logoAzul.png}
        };
	\end{tikzpicture}
    }
---


## Introducción

<!--
  pandoc -t beamer .\slides.md -o .\slides.pdf  --citeproc  --katex --slide-level=2 --from markdown+pipe_tables
 -->

* La lógica formal nos permite razonar acerca de frases declarativas o proposiciones
* Corresponde a la base del razonamiento matemático: Teoremas y pruebas.
* Tiene aplicaciones en el diseño de circuitos electrónicos, verificación de la correctitud de programas computacionales, programación de computadores, inteligencia artificial y  muchos otros.



## Declaraciones

- Una declaración o proposición es una frase cuyo resultado puede ser **V**erdadero o **F**also
- A este resultado de la proposición lo denominamos *Valor de verdad*
- Por ejemplo:
	- 10 es menor que 7
	- Valparaíso está en cuarentena
	- Juan es muy buen profesor



## Conectores y valores de verdad

- Los conectores son palabras que permiten unir proposiciones
	- Ejemplos: "y" (tambien conocido como *and*)
- Lo qué resulta de esa unión se denomina proposición compuesta

¿Cómo determinamos el valor de verdad de una proposición compuesta?

* Depende del valor de verdad de cada proposición simple y del conector usado ... existen algunas reglas para determinar esto

## Ejemplos

Por ejemplo, analicemos las siguientes proposiciones:

1. El día de hoy es jueves
2. Esta clase corresponde al curso de estructuras discretas

¿Que les parece cada declaración?

### Ejemplos

Por ejemplo, analicemos las siguientes proposiciones:

1. El día de hoy es jueves --> V
2. Esta clase corresponde al curso de estructuras discretas --> V

~~¿Que les parece cada declaración?~~ Por lo tanto, ¿Que valor de verdad tendría esta proposición compuesta?

- "El día de hoy es jueves y esta clase corresponde al curso de estructuras discretas"


## Representaciones simbólicas

Necesitamos una manera de poder tratar proposiciones y conectores que:

1. Sirva para todas las proposiciones (Generalidad)
2. Facilite la explicación de reglas (Economía en la escritura)

* Letras mayúsculas del principio del alfabeto representaran proposiciones (simples y también compuestas)


## Conjunciones y Disyunciones

* Los símbolos $\lor$ y $\land$ representan conectores (iremos agregando otros cuando se haga necesario)

* Decimos entonces que la proposición compuesta $A\land B$ dependerá de los valores de ambas proposiciones $A$ y $B$.

## Siga su intuición

1. Si $A$ es **V** y $B$ es **F**, ¿Que valor tiene la proposición $A\land B$?
1. Si $A$ es **F** y $B$ es **V**, ¿Que valor tiene la proposición $A\land B$?
1. Si $A$ es **F** y $B$ es **V**, ¿Que valor tiene la proposición $B\land A$?
1. Si $A$ es **F** y $B$ es **F**, ¿Que valor tiene la proposición $A\land B$?


## Ahora considere la Tabla

\begin{table}[]
\begin{tabular}{l|l|l}
A & B & $A\wedge B$ \\ \hline
V & V & V                \\
V & F & F                \\
F & V & F                \\
F & F & F               
\end{tabular}
\end{table}

---

Analice nuevamente y compare con su respuesta anterior...


1. Si $A$ es **V** y $B$ es **F**, ¿Que valor tiene la proposición $A\land B$?
1. Si $A$ es **F** y $B$ es **V**, ¿Que valor tiene la proposición $A\land B$?
1. Si $A$ es **F** y $B$ es **F**, ¿Que valor tiene la proposición $A\land B$?

## Conjunciones y Disyunciones

- A la expresión $A\land B$ se le denomina **conjunción**.
- Otro conector muy usado es el de la **disyunción** ($\vee$), cuya Tabla de verdad es:

\begin{table}[]
\begin{tabular}{l|l|l}
A & B & $A\vee B$ \\ \hline
V & V & V                \\
V & F & V                \\
F & V & V                \\
F & F & F               
\end{tabular}
\end{table}


- **Ejercicio** Siguiendo los ejemplos anteriores de conjunciones, construya una proposición compuesta para cada fila de la tabla de este conector.

## Implicancias

- Las proposiciones también pueden ser combinadas de la forma 
	"Si $A$, entonces $B$" (antecedente y consecuente)
- Esta proposición compuesta se representa como $A\Rightarrow B$ y se lee como $A$ implica $B$ 
- Indica que el valor de verdad de $A$ implica o conduce al valor de verdad de $B$
- Recuerda que lo que nos interesa es obtener el valor de verdad de la proposición compuesta a partir de los valores de sus componentes $A$ y $B$.

---


\begin{table}[]
\begin{tabular}{l|l|l}
A & B & $A\Rightarrow B$ \\ \hline
V & V & V                \\
V & F & F                \\
F & V & V                \\
F & F & V               
\end{tabular}
\end{table}

## Consideremos la siguiente proposición:

<center>"Si llueve, entonces me mojo"</center>

Examinemos varios casos. Entonces, cuando sabemos que	

- llovió y que además me encuentro mojado, la declaración es **V**
- llovió y que no me encuentro mojado, la declaración es **F**
- **no** llovió, entonces independientemente de si me encuentro o no mojado, no podemos decir que la declaración es **F**. Por convención, en este caso la declaración es **V**

## Equivalencias

- Conector simbolizado por $\Leftrightarrow$
- Es en realidad un "atajo" para la expresión 
$$(A\Rightarrow B)\land(B\Rightarrow A)$$
- *Ejercicio*: Construya la tabla de verdad para la Equivalencia.
- *Ejercicio*: Estructure como implicancia la frase: "*El fuego es una condición necesaria para el humo*".


## La Negación

- Es un conector **unario**, ya que actua sobre una declaración
- Es simbolizado por $\neg$
- Invierte el valor de verdad de la proposición
- Por ejemplo, $\neg A$ tiene valor **V** cuando $A$ es **F**
- Ejercicio: Usando los conectores $\lnot$, $\land$ y $\lor$, construya una expresión equivalente a $A\Rightarrow B$ para todos los valores posibles de $A$ y $B$

## Ejercicios

- Aplique la negación a cada una de las proposiciones y determine la proposición resultante:
1. Saldrá el sol mañana.
2. Mi perro es blanco y grande.
3. El cielo es oscuro o está contaminado.
4. A María le gusta el chocolate pero odia las almendras

## Orden de precedencia de operadores

- ¿Cómo resolvería la siguiente proposición $A\land B\Rightarrow C$ ?
* Es posible indicar qué operaciones se calculan primero usando paréntesis
	* $(A\land B)\Rightarrow C$
* Sin embargo, el exceso de paréntesis puede resultar abrumador

---

El orden en el cual los conectores son aplicados se denomina orden de precedencia:

1. Operaciones entre paréntesis, desde la más interna hacia afuera
1. Negación
1. $\land$, $\lor$
1. $\Rightarrow$
1. $\Leftrightarrow$

## Ejemplo

- $\neg A\lor  B$ es distinto de $\neg (A\lor B)$
- $A\land \neg(B\Rightarrow C)$ lo último que se calcula es $\land$
	- Primero se calcula $(B\Rightarrow C)$,
	- luego la negación de esta proposición
	- finalmente, la disyunción

- ¿Cómo resolvería la siguiente proposición?

$$((A\lor B)\land C)\Rightarrow(B\lor \neg C)$$

## Acerca de la notación

- También usaremos letras del final del alfabeto ($P,Q,R$) para representar proposiciones arbitrariamente simples y compuestas
- Por ejemplo, la expresión $((A\lor B)\land C)\Rightarrow(B\lor \neg C)$ puede ser también representada por $P \Rightarrow Q$

## Ejercicio

Construya la tabla de verdad para la siguiente proposición

$$(A\Rightarrow B)\Leftrightarrow (B\Rightarrow A)$$

## Tautologías

- Es una expresión cuyos valores de verdad son siempre verdaderos.
- Por ejemplo la proposición $A\lor \neg A$ (¡Asociela con una frase del mundo real!)
- Analicemos por ejemplo $(A\Rightarrow B)\Leftrightarrow(\neg B \Rightarrow \neg A)$

- Busque porqué una expresión como $A\land \neg A$ se denomina **contradicción**.
- ¡Asociela con una frase del mundo real!


## Algunas equivalencias tautológicas

**Disyunciones**

1. $A\lor B \Leftrightarrow B\lor A$ (conmutatividad)
1. $(A\lor B)\lor C \Leftrightarrow A\lor (B\lor C)$ (asociatividad)
1. $A\lor (B\land C) \Leftrightarrow (A\lor B)\land (A\lor C)$ (distributividad)
1. $A\lor$**F**$\Leftrightarrow A$ (identidad)
1. $A\lor \neg A\Leftrightarrow$**V** (complemento)


---

**Conjunciones**

1. $A\land B \Leftrightarrow B\land A$ (conmutatividad)
1. $(A\land B)\land C \Leftrightarrow A\land (B\land C)$ (asociatividad)
1. $A\land (B\lor C) \Leftrightarrow (A\land B)\lor (A\land C)$ (distributividad)
1. $A\land$**V**$\Leftrightarrow A$ (identidad)
1. $A\land \neg A\Leftrightarrow$**F** (complemento)

- Escoja dos de las tautologías y demuestre construyendo su tabla de verdad.

## Leyes de De Morgan

$$\neg(A\lor B) \Leftrightarrow \neg A\land \neg B$$

$$\neg(A\land B)\Leftrightarrow \neg A \lor \neg B$$

- Hint: Estas leyes ayudan a expresar la negación de una proposición compuesta.

