---
title: 
- Conteo y Combinatoria
subtitle:
- EST-1132 / Estructuras Discretas
author:
- Juan Zamora O.
#output: 
#  beamer_presentation:
#    citation_package: natbib
#theme:
#- Copenhagen
date:
- Otoño 2024
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


# Introducción

- La idea de *colección* es transversal también en en el análisis de algoritmos (ej. Ordenamiento)
- En esta unidad revisarem
	- Notación usada para conjuntos
	- Operaciones entre conjuntos
	- Algunas identidades

# Conjuntos

- Colección de objetos que comparten alguna propiedad
- Ejemplos: Números naturales, estudiantes de Ingeniería Estadística, niños menores de 11 años ...
- Para referenciar conjuntos usaremos letras mayúsculas. 
	- Por ejemplo $A,B,C\ldots$
- Para referenciar objetos o miembros de un conjunto usaremos letras minúsculas.
	- Por ejemplo $a,b,c,e,d\ldots$

---

Siguiendo con la notación

- La pertenencia de un objeto $a$ a un conjunto $D$ se simboliza $a\in D$
- La **no pertenencia** de un objeto $a$ a un conjunto $D$ se simboliza $a\notin D$
- Dos conjuntos son iguales si contienen los mismos elementos

## Definición de un conjunto

- Se deben identificar sus elementos
- Para un conjunto finito es posible listar todos sus elementos
- Para uno infinito es más dificil...podría indicarse el patrón $\{2,4,6,\ldots\}$
	- O una definición recursiva 
- De todas formas, la manera más clara es describir la propiedad característica del conjunto de elementos

---

- De todas formas, la manera más clara es describir la propiedad característica del conjunto de elementos
	- $S=\{x|x \mbox{ es un entero positivo par}\}$
- De manera más general, un conjunto $S$ se define como
$$S=\{x|P(x)\}$$

Esto significa que $(\forall x)[(x\in S\Rightarrow P(x))\wedge(P(x)\Rightarrow x\in S)]$

## Actividad

1. Listar los elementos de los siguientes conjuntos:
	i. $\{x|x\mbox{ es un entero y } 3 < x \leq 7 \}$
	ii. $\{x|x\mbox{ es un mes con 30 dias}\}$
	iii. $\{x|x\mbox{ es la capital de Chile}\}$
2. Describir los siguientes conjuntos mediante su propiedad
	i. $\{2,3,7,11,13,17,\ldots\}$
	ii. $\{2,4,6,8,10,12,\ldots\}$

# Algunos conjuntos importantes

- $\mathbb{N}$: Enteros no negativos ($0\in\mathbb{N}$)
- $\mathbb{Z}$: Enteros
- $\mathbb{Q}$: Racionales
- $\mathbb{R}$: Reales
- $\mathbb{C}$: Complejos
- $\emptyset$: Vacío. Ej.$\{x|x\in\mathbb{N}\mbox{ y }x<0\}$ 

## Actividad

1. Listar los elementos de cada conjunto
	i. $A=\{x|x\in\mathbb{N}\wedge (\forall y)(y\in\{2,3,4,5\}\Rightarrow x\geq y)\}$
	ii. $B=\{x|(\exists y)(\exists z)(y\in\{1,2\}\wedge z\in\{2,3\}\wedge x=y+z)\}$

# Subconjunto de un conjunto

- Considere los conjuntos $A=\{2,3,5,12\}$ y $B=\{2,3,4,5,9,12\}$
- Se puede ver que cada miembro de $A$ es también un miembro de $B$, pero existen elementos de $B$ que no están en $A$	
	- Cuando ocurre esto, se dice que $A$ es un **subconjunto** de $B$
$$A\subseteq B$$ o bien $$A\subset B$$ 
- Para indicar que todos los elementos de $A$ están en $B$, pero $A\neq B$ se indica $A$ como subconjunto propio de $B$ y se representa como $A\subset B$

---

Si se tienen los conjuntos:
$$A=\{1,7,9,15\}$$
$$B=\{7,9\}$$
$$C=\{7,9,15,20\}$$

Entonces

- $B\subset C$
- $B\subset A$

## Actividad

Considere los conjuntos:
$$A=\{x|x\in\mathbb{N}\wedge x\geq 5\}$$
$$B=\{10,12,16,20\}$$
$$C=\{x|(\exists y)(y\in\mathbb{N}\wedge x=2y)\}$$

Indique cuales afirmaciones son verdaderas:

**i.** $B\subseteq C$ **ii.** $B\subset A$ **iii.** $A\subseteq C$ **iv.** $\{10,12,16,20\}\subset B$
**v.** $26\in C$ **vi.** $\{11,12,13\}\subseteq A$ **vii.** $\{11,12,13\}\subset C$

# El Conjunto Potencia

- Conjunto de conjuntos.
- Dado un conjunto $S$, podemos conformar uno nuevo cuyos elementos son todos los posibles subconjuntos de $S$.
- Se simboliza $\wp(S)$

Ej. Dado $S=\{0,1\}$, $\wp(S)=\{\emptyset, \{0\}, \{1\},\{0,1\}\}$

**Notar que todos los miembros de $\wp$ son conjuntos**

## Actividad

1. Para $A=\{1,2,3\}$, ¿Cual es $\wp(A)$?
2. ¿Cuantos elementos tiene este conjunto potencia?
3. Si $S$ tiene $n$ elementos, ¿Cuantos elementos tiene $\wp(S)$?



# Operaciones sobre conjuntos

Dados dos conjuntos $A$ y $B$.

- Unión: $A\cup B=\{x|x\in A\lor x\in B\}$
- Intersección: $A\cap B=\{x|x\in A\wedge x\in B\}$

*Ejemplo*: Para $A=\{1,3,5,7,9\}$ y $B=\{3,5,6,10,11\}$
- $A\cup B=\{1,3,5,6,7,9,10,11\}$
- $A\cap B=\{3,5\}$

---

Sea $S$ un conjunto universo (ej. $\mathbb{N}$)
- Complemento de un conjunto $A\in\wp(S)$: $A'=\{x|x\in S\wedge x\notin A\}$

*Ejemplo*: Si $S=\{1,2,3\}$ y $A\in\wp(S)=\{1,3\}$, entonces $A'=\{2\}$.

- Diferencia entre dos conjuntos $A$ y $B$, $A-B=\{x|x\in A\wedge x\notin B\}$ 

*Ejemplo*: Si $A=\{4,7,8\}$ y $B=\{3,4,6,7\}$, entonces $A-B=\{8\}$. ¿Que se obtendría para $B-A$?


---

- El producto cartesiano entre dos conjuntos $A$ y $B$ se define como $A\times B=\{(x,y)|x\in A\wedge y\in B\}$
- Es decir, es el conjunto de todos los pares ordenados cuya primera componente proviene de $A$ y el segundo de $B$.

*Ejemplo*: Si $A=\{2,3\}$ y $B=\{4\}$, entonces $A\times B=\{(2,4),(3,4)\}$

*Ejemplo*: Si $A=\{2,3\}$, entonces $A\times A=A^2=\{(2,2),(2,3),(3,2),(3,3)\}$


# Identidades básicas de conjuntos

\begin{tikzpicture}[remember picture, overlay]
    \node[above left, yshift=-1cm, xshift=4cm] at (current page.center) 
    {
        \includegraphics[width=0.8\textwidth]{conjuntos_identidades.png}
    };
\end{tikzpicture}

# Conteo

* Este problema consiste esencialmente en encontrar la cantidad de elementos de un conjunto determinado
* Permite por ejemplo abordar preguntas como ¿cuantas operaciones realiza un algoritmo?¿cuanto almacenamiento necesita una base de datos?
* Hasta ahora hemos abordado preguntas similares en varios momentos del Curso
    * ¿Cuantas filas tiene una tabla de verdad con $n$ proposiciones?
    * ¿Cuantos subconjuntos tiene un conjunto con $n$ miembros?

## Principios generales

Revisaremos 4 principios de conteo que nos permitiran resolver varios problemas

1. Multiplicación
2. Adición
3. Inclusión y Exclusión
4. Palomera

## Principio de Multiplicación

Si hay $n_1$ resultados posibles para un primer evento y $n_2$ posibles resultados para un segundo evento, entonces hay $n_1\times n_2$ posibles resultados para la secuencia de los dos eventos.

---

### Principio de Multiplicación

**Ejemplo**
    
Un niño puede escoger sólo una gomita de dos opciones disponibles, una roja y otra verde, y un caramelo de tres opciones disponibles, naranjo, amarillo y azul. ¿Cual es la cantidad de elecciones posibles que tiene el niño?


\begin{tikzpicture}[remember picture, overlay]
    \node[above left, yshift=1cm, xshift=4cm] at (current page.south) 
    {
        \includegraphics[width=0.5\textwidth]{dulces.png}
    };
	\end{tikzpicture}

---

### Extensión del principio

- Este principio puede ser extendido y aplicado para cualquier secuencia finita de eventos
- Útil para contar resultados posibles de una tarea que puede ser dividida en una secuencia de subtareas sucesivas

## Principio de Adición

Si se tienen dos eventos disjuntos  $A$ y $B$ con $n_1$ y $n_2$ resultados posibles, respectivamente, entonces el número total de resultados posibles para el evento "$A$ o $B$" es $n_1+n_2$ .

---

### Principio de Adición

**Ejemplo**

Una persona desea comprar un vehículo en una tienda. El vendedor tiene 23 automoviles y 14 camionetas disponibles en stock. ¿Cuantas selecciones posibles tiene el comprador?

¿Que ocurre si los eventos no son disjuntos? ¿Que ocurre con el resultado anterior si el vendedor tiene 23 automoviles, 14 camionetas y 17 vehículos rojos? *En este caso no podemos concluir que hay $23+14+17$ opciones*.

## Uso combinado de ambos principios

¿Cuantos números de 4 dígitos comienzan con 4 o con 5?

Ejemplos: 4102 , 4499, 5300, 5120 ...

---

Primero, se podría dividir la tarea de conformar números de 4 dígitos $4x_1x_2x_3$ en 3 subtareas:

1. Existen 10 resultados posibles para $x_1$
1. Existen 10 resultados posibles para $x_2$
1. Existen 10 resultados posibles para $x_3$

Por el principio de multiplicación, se tienen $10\times 10\times 10 = 1000$ posibles resultados. Debido a que la segunda tarea cumple con el mismo principio, la cantidad total de números se calcula usando el principio de adición $1000+1000=2000$.



## Principio de Inclusión y Exclusión

- Una buena manera de resumirlo es con la identidad: $|A\cup B|=|A|+|B|-|A\cap B|$
- Al contar el número de elementos en la unión entre $A$ y $B$ se debe 
    - incluir el número de elementos en cada conjunto
    - también se debe excluir aquellos elementos en la intersección


## Principio de Inclusión y Exclusión

**Ejemplo**

Una encuestadora entrevista 35 votantes, todos/todas los/las cuales apoyan el referendo 1, el referendo 2 o ambos. Se determina que 14 votantes apoyan el referendo 1 y 26 el 2. ¿Cuant@s votantes apoyan ambos referendos?


---

**Solución** 

* Sea $A$ el conjunto de votantes que apoyan el referendo 1 y $B$ los que apoyan al 2.
* Se sabe entonces que $|A\cup B|=35$, $|A|=14$ y $|B|=26$.
* Entonces, al reemplazar en $|A\cup B|=|A|+|B|-|A\cap B|$ se obtiene $|A\cap B|=5$.

## Principio de la Palomera

- Origen del nombre: Si **más de $k$ palomas** vuelan dentro de $k$ casilleros, entonces al menos una casilla tendrá más de una paloma.

¿Cuantas personas deben estar dentro de una habitación de manera que 2 de ellas tengan apellidos que comiencen con la misma letra inicial?

Tenemos 27 letras en el alfabeto (*casillas*). Si consideramos el apellido de 28 personas (*palomas*), entonces habrá 28 iniciales sobre 27 alternativas posibles. Al menos dos de los apellidos tendran la misma letra inicial.



## Permutaciones y Combinaciones

- Un arreglo *ordenado* de objetos se denomina permutación
- Considere el ejercicio entregado en la actividad anterior
	- ¿Cuántos números de 4 dígitos existen si el mismo dígito no puede usarse dos  veces?
- Para este problema, el número 4983 es distinto al 3894 y también al 4893.
- Para resolverlo, consideramos que hay 10 dígitos, y por el principio de la multiplicación:
$$10\cdot 9\cdot 8\cdot 7\mbox{ numeros}$$

---

- El número de permutaciones de 10 dígitos distintos escogidos de a 4 se representa como $P(10,4)$
- En general, $P(n,r)$ es la cantidad de permutaciones de $r$ objetos distintos escogidos a partir de un conjunto de $n$ objetos.
- Formalmente, para $r< n$
$$P(n,r)=\frac{n!}{(n-r)!}$$
- **Calcule nuevamente** $P(10,4)$ usando la expresión anterior.

---

- ¿Cuantas permutaciones de 3 objetos pueden construirse con los objetos *a*, *b* y *c*?
- ¿Cuantas palabras de 3 letras sin repetir pueden formarse a partir de la palabra *discreta*?
- Idem, pero a partir de la palabra *discretas*.

## Combinaciones

- Anteriormente, contamos arreglos de objetos donde el orden en que aparecian importaba.
- Cuando solo interesa qué objetos aparecen y **no** su orden, se denominan **combinaciones**
- Intentaremos derivar la cantidad de arreglos posibles de $r$ objetos a partir de un conjunto de $n$...

---

- Para cada configuración de $r$ objetos, existen $P(r,r)$ maneras de permutarlos
- Si existen $C(n,r)$ maneras de combinar $r$ objetos a partir de un conjunto de $n$
	- entonces, $P(n,r)=C(n,r)\cdot P(r,r)=C(n,r)\cdot r!$
	- luego 
	$$C(n,r)=\frac{P(n,r)}{P(r,r)}=\frac{n!}{r!(n-r)!}$$
- Otra notación usada es $\binom{n}{r}$

---

- En un juego de 52 cartas. ¿Cuantas manos de 5 cartas pueden conformarse?
- ¿Cuantos comites de 3 personas se pueden formar a partir de un grupo de 12?
- Hay 15 estudiantes. ¿Cuantos grupos de 3 estudiantes pueden formarse?

---

### Ejercicio

En una clase conformada por 19 estudiantes de primer año y 34 de segundo, se necesita formar un grupo de 8. 

1. ¿Cuantos grupos de 3 de 1ro y 5 de 2do pueden formarse?
1. ¿Cuantos con exactamente 1 de 1ro?
1. ¿Cuantos con uno de 1ro como máximo?
1. ¿Cuantos con al menos uno de 1ro?

---

### Permutaciones con duplicados

- ¿Cuantas permutaciones pueden generarse a partir de los caracteres de la palabra PUCV?
- ¿Cuantas a partir de la palabra estadistica? (tilde omitido a propósito)

---

En general, si se tienen $n$ objetos de los cuales un conjunto de $n_1$ son indistinguibles entre sí, lo mismo para $n_2$, $n_3$...$n_k$. 

El número de permutaciones distintas de $n$ objetos es
$$\frac{n!}{(n_1!)(n_2!)\ldots (n_k!)}$$


## El Teorema Binomial como resultado del conteo

- El cuadrado de binomio $(a+b)^2$ es un caso particular 
- Este teorema entrega un mecanismo para calcular $(a+b)^n$
- Revisaremos como puede establecerse este teorema como un problema de conteo

---

Consideremos el triangulo de pascal:

\begin{tikzpicture}[remember picture, overlay]
    \node[above left, yshift=-0.5cm, xshift=3cm] at (current page.center) 
    {
        \includegraphics[width=0.45\textwidth]{triangulo_pascal.png}
    };
\end{tikzpicture}

\vspace{70pt}
- Podemos tomar la fila $n=2$ y veremos los coeficientes de $(a+b)^2=1a^2+2ab+1b^2$

---

Luego, 

\begin{tikzpicture}[remember picture, overlay]
    \node[above left, yshift=-5cm, xshift=5cm] at (current page.north) 
    {
        \includegraphics[width=0.75\textwidth]{triangulo_pascal_generico.png}
    };
\end{tikzpicture}


\vspace{80pt}

- Ahora podemos establecer de manera general para cualquier entero no negativo $n$
$$(a+b)^n=\sum_{k=0}^{n}C(n,k)a^{n-k}b^k$$

---

### Ejercicios

Usando el teorema binomial recién planteado obtenga 
- $(a+b)^0$
- $(x-3)^4$
- $(x+1)^5$
- El 5to término en la expansión de $(x+y)^7$
