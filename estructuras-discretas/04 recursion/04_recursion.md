---
title: 
- Recursión
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
- Otoño 2023
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

- En ocasiones es dificil definir una función u objeto de manera explícita
- Alternativa: Definición en función de sí mismo
- Siempre tiene dos partes: Base y parte recursiva
	- La base está compuesta por casos simples explícitamente definidos
	- La parte recursiva generaliza sobre nuevos casos definidos en función de otros anteriores


# Secuencias definidas recursivamente

- Es una lista inifinita de objetos enumerados en algún orden
- Denominemos al k-ésimo objeto como $S(k)$
$$S(1), S(2), \ldots S(k), \ldots$$

- Una secuencia definida recursivamente cuando $S(k)$ se define en función de alguno(s) de lo(s) $k-1$ previos objetos


## Ejemplo

Considere la siguiente secuencia definida recursivamente
$$
\begin{array}{lll}
   1.& S(1) =& 1 \\
   2.& S(n) =& 2\cdot S(n-1) \mbox{, para }n\geq 2
\end{array}
$$

* Podemos verificar que $S(2)=2$, $S(3)=4$ y luego $8, 16, 32 \ldots$

## Actividad


$$
\begin{array}{lll}
   1.& T(1) =& 1 \\
   2.& T(n) =& T(n-1) + 3 \mbox{, para }n\geq 2
\end{array}
$$

**Escriba los primeros 5 valores de la secuencia $T$**


## Actividad: Fibonacci

Sugerencia: Revise [el siguiente video](https://www.youtube.com/watch?v=8bCYiUIlF2k)

$$
\begin{array}{lll}
   1.& F(1) =& 1 \\
   1.& F(2) =& 1 \\
   2.& F(n) =& F(n-2) + F(n-1) \mbox{, para }n> 2
\end{array}
$$

- Escriba los primeros 8 valores de la secuencia $F$
- Calcule el cuociente entre varios valores sucesivos de $F$ y averigue acerca de la razón dorada


# Conjuntos definidos recursivamente

- Previamente, los objetos tenían un orden
- Los conjuntos **no** tienen este ordenamiento
- Se especifican algunos elementos iniciales
- Se provee de una regla para construir nuevos elementos a partir de los ya existentes

## Ejemplo

Considere el subconjunto $S$ de los enteros, que se define como
1. Paso base: $4\in S$
1. Paso recursivo: Si $x\in S$ e $y\in S$, entonces $x+y\in S$

- Así entonces el conjunto $S$ estará conformado por $4+4=8; 4+8=12; 8+8=16\ldots$ 
- Será el de los múltiplos de $4$

## Actividad

Considere el conjunto $\mathsf{A}^{*}$ de todas las palabras de largo finito sobre un alfabeto $\mathsf{A}$. Luego, se define recursivamente siguiendo las reglas:

1. La palabra sin símbolos (vacía) $\lambda$ pertenece a $\mathsf{A}^{*}$
1. Cualquier símbolo de $\mathsf{A}$ pertenece a $\mathsf{A}^{*}$
1. Si $x$ e $y$ son palabras en $\mathsf{A}^{*}$, entonces también lo será $xy$, es decir la concatenación de las palabras $x$ e $y$
 

* Sea $\mathsf{A}=\{0,1,\lambda\}$. Si $x=1101$ e $y=001$, **escriba** las palabras $xy$, $yx$ y $yx\lambda x$.

## Actividad

Entregue una definición recursiva para el conjunto de todas las palabras binarias que se leen de igual manera de derecha a izquierda, que de izquierda a derecha. Por ejemplo, $1001$ y $11011$.


---

### Solución.

Sea $\mathsf{A}=\{0,1,\lambda\}$.

1. $\lambda ,\ 0,\ 1\in \mathsf{A}^{*}$ 
1. Si $x\in \mathsf{A}^{*}$, entonces también $0x0$ y $1x1$


## Operaciones definidas recursivamente

- Ciertas operaciones sobre objetos pueden ser definidas recursivamente
- Por ejemplo, la exponenciación sobre un número real distinto de $0$

$$
\begin{array}{lll}
1. & p^0 =& 1 \\
2. & p^n =& (p^{n-1})\cdot p, \ \forall n\geq 1 
\end{array}
$$

---

- O la multiplicación de dos enteros $m$ y $n$

$$
\begin{array}{lll}
1. & m(1) &= m \\
2. & m(n) &= m(n-1)+m, \ \forall n\geq 1 
\end{array}
$$

- **Ejemplo**

Sea $x$ una palabra en un alfabeto (no es relevante qué alfabeto específico se use para este problema). Entregue una definición recursiva para la operación $x^n$ que representa la concatenación de $x$ con sí misma $n$ veces para $n\geq 1$.

---

### Ejemplo (solución)

Sea $x$ una palabra en un alfabeto (no es relevante qué alfabeto específico se use para este problema). Entregue una definición recursiva para la operación $x^n$ que representa la concatenación de $x$ con sí misma $n$ veces para $n\geq 1$.

$$
\begin{array}{lll}
1. & x^0 =& x \\
2. & x^{n} =& x^{n-1}x, \ \forall n\geq 1 
\end{array}
$$


## Algoritmos definidos recursivamente

- En palabras simples, es un programa que en su cuerpo tiene llamadas a sí mismo
- Recordemos la secuencia
$$
\begin{array}{lll}
   1.& S(1) =& 2 \\
   2.& S(n) =& 2\cdot S(n-1) \mbox{, para }n\geq 2
\end{array}
$$

- Calcule $S(2),S(3),S(4)$ y $S(5)$.

---

- Considere un programa que evalua $S(n)$

		Procedimiento S(n un nro entero)$
		  Si n = 1 entonces
		    retornar 2
		  Sino
		    i = 2
		    val = 2
		    mientras i <= n hacer
		      val = 2 * val
		      i = i + 1
		    fin de bloque mientras

		    retornar val
		  fin de bloque Si
		fin de procedimiento

---

- Otro enfoque consiste en una definición mucho más corta (**Observe**)

		Procedimiento S(n un nro entero)$
		  Si n = 1 entonces
		    retornar 2
		  Sino
		  	retornar 2 * S(n-1)
		  fin de bloque Si
		fin de procedimiento

- Analice como se calcula $S(3)$ con este código.

---

### Ventajas relativas en algoritmos recursivos e iterativos

- Recursividad ofrece (en ocasiones) una manera más natural para muchos problemas
- Recursividad genera procedimientos más cortos
- Operación de alg. recursivo es más compleja
- Ejecución de Alg. recursivo consume más memoria

---

### Actividad

Recuerde la secuencia antes vista y escriba una función recursiva para calcular $T(n)$

$$
\begin{array}{lll}
   1.& T(1) =& 1 \\
   2.& T(n) =& T(n-1) + 3 \mbox{, para }n\geq 2
\end{array}
$$ 

---

### Actividad

Recuerde la operación recursiva par multiplicar dos números y construya un pseudocódigo para ella.


## Conclusiones

- Muchos problemas pueden ser analizados más naturalmente bajo una perspectiva recursiva
- El "secreto" de una recursividad efectiva está en entregarle a cada llamada una versión más pequeña o simple del problema
- Nunca olvidar la definición del caso base... todo depende de ello!


## Relaciones de Recurrencia

Imagine que una persona deposita \$10.000 en una cuenta de ahorro de un banco con un \%11 de interés anual compuesto. ¿Cuanto se habrá reunido en la cuenta después de 30 años?

---

- Anteriormente, construímos procedimientos para calcular

$$
\begin{array}{lll}
   1.& S(1) =& 2 \\
   2.& S(n) =& 2\cdot S(n-1) \mbox{, para }n\geq 2
\end{array}
$$

---

- Luego, al calcular otros valores de la función
$$
\begin{array}{lll}
   1.& S(1) =& 2^1 \\
   2.& S(2) =& 2^2 \\
   3.& S(3) =& 2^3 \\
   4.& S(4) =& 2^4 \\
     & \ldots & \\
   n.& S(n) =& 2^n
\end{array}
$$

- Ahora vemos que basta con calcular $S(n)$ para cualquier número **sin** necesidad de tener que obtener los $n-1$ pasos previos.

---

**Soluciones cerradas**

- Soluciones como la del ejemplo  permiten obtener directamente cualquier valor  
- Se denominan **soluciones cerradas** de una relación de recurrencia
- Entonces, para nuestro ejemplo, **la solución** $S(n) = 2^n$ **resuelve** la **relación de recurrencia** $S(n) = 2\cdot S(n-1)$

---

### Relaciones lineales de 1er orden

Una relación $S(n)$ es lineal si sus valores tienen la forma
$$S(n)=f_1(n)S(n-1)+f_2(n)S(n-2)+\ldots + f_k(n)S(n-k) + g(n)$$

- Las $f$s y $g$ son expresiones que involucran solamente a $n$ más otras constantes

---

### Caracterizando las relaciones lineales de 1er orden

- Nos fijaremos ahora en qué condiciones considerar para
	- Las $f$s
	- La dependencia de $S(n)$ de sus valores anteriores (*orden*)
	- $g$
- Dependiendo de estas condiciones estudiaremos ciertos tipos de soluciones para cada tipo de relación 

---

#### Relaciones de 1er orden con coefs. constantes	

- La relación tendrá coeficientes constantes si todas las $f$s lo son
- Será de 1er orden si $S(n)$ solo depende de $S(n-1)$
- Entonces, podemos *continuar* caracterizando de manera general una relación lineal de 1er orden con coeficientes constantes como
$$S(n) = cS(n-1)+g(n)$$
- Por último, la relación será **homogenea** si $g(n) =0$ para cualquier valor de $n$.

---

- Primer orden $\Rightarrow$ Se requiere de un valor inicial para la base $S(1)$ u otro.
- Entonces, de manera general para este tipo de relaciones
$$
\begin{array}{lll}
   S(n) =& cS(n-1)+g(n) \\
     =& c[cS(n-2)+g(n-1)] + g(n) \\
     =& c^2S(n-2)+cg(n-1) + g(n) \\
     =& c^2[cS(n-3)+g(n-2)]+cg(n-1) + g(n) \\
     =& c^3S(n-3)+c^2g(n-2)+cg(n-1)+g(n)   \\
     & \vdots
\end{array}
$$

---

Luego de $k$ expansiones queda

$$S(n)=c^kS(n-k)+c^{k-1}g(n-(k-1))+\ldots + cg(n-1)+g(n)$$

- Si esta secuencia tiene un valor base en $1$, entonces la expansión terminará cuando $n-k=1$ o $k=n-1$

$$S(n)=c^{n-1}S(1)+c^{n-2}g(2)+\ldots + c^1g(n-1)+c^0g(n)$$
$$S(n)=c^{n-1}S(1)+\sum_{i=2}^{n}c^{n-i}g(i)$$

- Estamos muy cerca de una solución, pero deberemos **siempre** encontrar una expresión para la sumatoria

---

- Por ejemplo, cuando $g(n)=0$ queda solamente la primera parte de la solución (caso más simple denominado **homogeneo**)
- Ejemplo, volvamos a 
$$
\begin{array}{ll}
   S(1) =& 2 \\
   S(n) =& 2\cdot S(n-1) \mbox{, para }n\geq 2
\end{array}
$$

- Es lineal, de primer orden y con coefs. ctes.
- Entonces,
$$S(n)=2^{n-1}(2)+\sum_{i=2}^{n}0=2^n$$

---

**En síntesis**

1. Caracterizar la relación y  verificar calce con expresión general
1. Encontrar el  valor para $c$ usando el valor inicial $S(1)$
1. Encontrar (si fuera necesario) un valor sintetizado para la sumatoria y obtener la expresión final de la solución

---

**Ejercicio:**

Encuentre una solución para la relación
$$S(n)=2S(n-1)+3,\ \forall n\geq 2$$
sujeta al paso base $S(1)=4$.




## Relaciones lineales de 2do orden

- En una relación de 2do orden el término $n$-ésimo depende de los dos términos anteriores.
- Por lo tanto, este tipo de relaciones tiene la forma
$$S(n)=f_1(n)S(n-1)+f_2(n)S(n-2)+g(n)$$
- Consideraremos aquellas relaciones lineales homogeneas y con coeficientes constantes.
$$S(n)=c_1S(n-1)+c_2S(n-2)$$

---

### Soluciones

- Buscamos soluciones de la forma
$$S(n)=r^n\mbox{ , con $r$ constante}$$
- Por lo tanto $S(n)=r^n=c_1r^{n-1}+c_2r^{n-2}$
- Esta solución estará dada por $r^n-c_1r^{n-1}-c_2r^{n-2}=0$ y luego de dividir ambos lados por $r^{n-2}$ queda 
$$r^2-c_1r-c_2=0$$ 
- A esta expresión se le denomina **Ecuación característica** de la relación

---

- Esta ecuación tendrá 2 raices: $r_1$ y $r_2$
- A las raices de esta ecuación se le denominan raíces características

**Estrategia propuesta:**

- Lograremos caracterizar **La solución cerrada** de la relación mediante $r_1$ y $r_2$

---

¿Que sabemos hasta hora entonces?

1. $S(n)=c_1S(n-1)+c_2S(n-2)$
1. $S(n)=r^n$
1. Luego, $r^n=c_1r^{n-1}+c_2r^{n-2}$
1. Finalmente, hay que resolver $r^2-c_1r-c_2=0$
1. Podemos agregar que $r_1^2=(c_1r_1+c_2)$ **y** $r_2^2=(c_1r_2+c_2)$


**Luego, la solución tendrá la forma**
$$S(n)=\alpha_1 r_1^n + \alpha_2 r_2^n$$
 (probaremos informalmente esto a continuación...)


---

Acabamos de afirmar que $S(n)=\alpha_1 r_1^n + \alpha_2 r_2^n$

$$
\begin{array}{rcl}
   c_1S(n-1)+c_2S(n-2) &=& c_1(\alpha_1 r_1^{n-1}+\alpha_2 r_2^{n-1}) + c_2(\alpha_1 r_1^{n-2}+\alpha_2 r_2^{n-2}) \\
   \ldots              &=& c_1(\alpha_1 r_1^{n-2}r_1+\alpha_2 r_2^{n-2}r_2) + c_2(\alpha_1 r_1^{n-2}+\alpha_2 r_2^{n-2}) \\
   \ldots              &=& \alpha_1 r_1^{n-2}(c_1r_1+c_2) + \alpha_2 r_2^{n-2}(c_1r_2+c_2)\\
   \ldots              &=& \alpha_1 r_1^{n-2}r_1^2 + \alpha_2 r_2^{n-2}r_2^2 \\
   c_1S(n-1)+c_2S(n-2) &=& \alpha_1 r_1^{n} + \alpha_2 r_2^{n}
\end{array}
$$

Por lo tanto
 $$S(n)=c_1S(n-1)+c_2S(n-2) = \alpha_1 r_1^{n} + \alpha_2 r_2^{n}$$

**Ojo** Hemos supuesto hasta ahora que $r_1\neq r_2$

 ---

 Ahora solamente nos queda establecer un mecanismo para encontrar $\alpha_1$ y $\alpha_2$.

 1. Se identifican $c_1$ y $c_2$ a partir de la relación entregada.
 1. Se obtienen las soluciones para $r^2-c_1r-c_2=0$
 1. Se obtienen $\alpha_1$ y $\alpha_2$ usando las dos casos iniciales... $S(0)$ y $S(1)$

 ¿Como?

 ---

Reemplazando $n=0$ y $n=1$ en $S(n)=\alpha_1 r_1^n + \alpha_2 r_2^n$
$$
 \begin{array}{rcl}
 S(0) &=& \alpha_1 + \alpha_2 \\
 S(1) &=& \alpha_1 r_1 + \alpha_2 r_2
\end{array}
$$

Sustituyendo, se llega a que 
$$\alpha_1=\frac{S(1)-S(0)r_2}{r_1-r_2}$$ 
y 
$$\alpha_2=S(0)-\frac{S(1)-S(0) r_2}{r_1-r_2}$$

---

### Mutiplicidad de raíces

- Considere la ecuación característica
$$r^2-c_1 r - c_2=0$$
con raíces $r=r_1=r_2$ .
- La solución para $S(n)=c_1S(n-1)+c_2S(n-2)$ tendrá la forma
$$S(n)=\alpha_1 r^n + \alpha_2\cdot n\cdot r^n$$
- Los coeficientes se calculan siguiendo el esquema para el caso sin multiplicidad.

---

- Los coeficientes se calculan siguiendo el esquema para el caso sin multiplicidad. Es decir:
$$
 \begin{array}{rcl}
 S(0) &=& \alpha_1 r^0 + \alpha_2\cdot 0\cdot r^0 = \alpha_1 \\
 S(1) &=& \alpha_1 r^1 + \alpha_2\cdot 1\cdot r^1 = \alpha_1 r + \alpha_2 r\\
\end{array}
$$

Finalmente (verifique el desarrollo):
$$\alpha_1=S(0) \mbox{ ; } \alpha_2=\frac{S(1)-S(0)r}{r}$$