---
title: 
- Lógica Proposicional y de Predicados
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


# Cálculo Proposicional

- Hemos revisado la notación formal para representar proposiciones correctamente formadas
- Operadores y el cálculo de proposiciones (simples y compuestas) usando tablas de verdad
- Queremos ahora poder razonar (alcanzar conclusiones lógicas) basandonos en afirmaciones entregadas

## Argumentos

Podemos representar un *argumento* de la siguiente manera:
$$P_1\land P_2 \land P_3\land  \ldots P_m \Rightarrow Q$$

- Donde $P_1\land P_2 \land \ldots$ son declaraciones o afirmaciones dadas inicialmente, englobadas como **la hipótesis** del argumento.
- $Q$ es **la conclusión** del argumento.

---

### Argumentos válidos

- Un argumento es válido cuando la conclusión se deduce lógicamente de las premisas
- Esto significa que si todas las premisas son verdaderas entonces la  conclusión también debe serlo.
- Por lo tanto, el argumento siempre debe ser verdadero (es una *tautología*)

Por ejemplo: 
$$P\land Q \Rightarrow Q$$

---

### Ejercicio

Represente formalmente el argumento:

>"La manzana es una fruta y el tomate también. Por lo tanto, Valparaíso está en cuarentena."

Demuestre que este argumento **no** es válido.    

---

### Ejercicio

Represente formalmente el argumento:

>Si mi padre tiene un hijo, entonces yo existo. Mi padre sí tiene un hijo. Por lo tanto, existo.

- Demuestre que este argumento **sí** es válido.
- Averigue acerca del *Modus Ponens*

# Reglas de derivación

- Existen dos categorías de reglas:
    1. **Equivalencia**: Establecen sustituciones válidas entre sentencias.
    2. **Inferencia**: Indican patrones de derivación que pueden ser usados para simplificar una expresión.

## Reglas de Equivalencia

| Expresión | Equivalente a | Nombre |
|---|---|---|
|$P\lor Q$| $Q\lor P$ | Conmutativa |
|$P\land Q$| $Q\land P$ |  ... |
|$(P\lor Q)\lor R$|$P\lor (Q \lor R)$| Asociativa|
|$(P\land Q)\land R$|$P\land (Q \land R)$| ...|
|$P\lor (Q\land R)$|$(P\lor Q)\land (P \lor R)$| Distributiva|
|$P\land (Q\lor R)$|$(P\land Q)\lor (P \land R)$| ...|

---

| Expresión | Equivalente a | Nombre |
|---|---|---|
|$\neg(P\lor Q)$|$\neg P\land \neg Q$| De Morgan|
|$\neg(P\land Q)$|$\neg P\lor \neg Q$| ...|
|$P\Rightarrow Q$|$\neg P \lor Q$|Implicancia|
|$P$|$\neg(\neg P)$|Doble negación|
|$P\Leftrightarrow Q$|$(P\Rightarrow Q)\land(Q\Rightarrow P)$|Def. de equiv.|


## Reglas de Inferencia

| Dadas | Se deriva | Nombre |
|---|---|---|
|$P,P\Rightarrow Q$|$Q$|Modus ponens|
|$P\Rightarrow Q, \neg Q$|$\neg P$|Modus tollens|
|$P,Q$|$P\land Q$|Conjunción|
|$P\land Q$|$P,Q$|Simplificación|
|$P$|$P\lor Q$|Adición|

- *Hint*: equivalencia entre columnas 1 y 2 es en **una dirección**.

---

### Ejemplo

Considere el siguiente argumento: $$[(A\land \neg B)\Rightarrow C]\land \neg C \Rightarrow (\neg A\lor B)$$

- Identifique y enumere las premisas
- Demuestre la validez del argumento

---

**(Solución)**

- Se aplican reglas señalandolas en cada paso:
1. $(A\land \neg B)\Rightarrow C$ (hip.)
2. $\neg C$ (hip.)
3. $\neg(A\land \neg B)\lor C \land \neg C$ (impl.)
4. $\neg(A\land \neg B)\lor$ **F** (impl.)
4. $\neg(A\land \neg B)$
4. $\neg A\lor B$ (D.Mor, D.Neg.)


---

### Ejercicio

En una escena de un crimen, los investigadores establecen el siguiente argumento:

>El robo no fue el objeto del asesinato, puesto que nada desapareció.

- **¿Es válido?**


---

**(Solución mediante propiedades)**

- Primero hay que formalizar esta proposición de manera simbólica    
   - Si fue un robo, entonces algo habría desaparecido
   - Nada desapareció
   
$$
\begin{array}{l}
   P\Rightarrow Q  \\
   \neg Q \\ \hline 
   \neg P
\end{array}
$$

- ¿Cómo se llama la propiedad aplicada?
- Demuestre ahora usando la tabla de verdad.



---

### Ejercicio

Demuestre la validez del argumento

$$[(A\lor \neg B)\Rightarrow C]\land (C\Rightarrow D)\land A\Rightarrow D$$

- Para realizar esta actividad, averigue primero acerca de la regla del Silogismo Hipotético.

---

$$
\begin{array}{lll}
1. & (A\lor \neg B)\Rightarrow C & \mbox{hip}\\
2. & C\Rightarrow D & \mbox{hip} \\ 
3. & A & \mbox{hip} \\ 
4. & (A\lor \neg B)\Rightarrow D & 1,2,\mbox{Silogismo Hipot.}\\
5. & A\lor \neg B & 3, Adición.\\\hline
   & D & 4,5,\mbox{M.Ponens}
\end{array}
$$




---

Demuestre la validez del argumento

$$A\land (B\Rightarrow C)\land [(A\land B)\Rightarrow(D\lor \neg C)]\land B\Rightarrow D$$

## Método de deducción

Método útil para probar argumentos de la forma
$$P_1\land P_2\land \ldots \land P_m \Rightarrow (R\Rightarrow S)$$

1. Agregue $R$ como otra hipótesis
2. Derive S

**Ejemplo** Pruebe que $[A\Rightarrow (A\Rightarrow B)]\Rightarrow (A\Rightarrow  B)$ es una tautología (En otras palabras, derive $(A\Rightarrow B)$ partir de las premisas)

---

$$[A\Rightarrow (A\Rightarrow B)]\Rightarrow (A\Rightarrow  B)$$



$$
\begin{array}{lll}
1. & A\Rightarrow (A\Rightarrow B) & \mbox{hip}\\
2. & A & \mbox{hip*} \\ 
3. & A\Rightarrow B & 1,2,\mbox{Mod.P}\\ \hline
   & B & 2,3,\mbox{Mod.P}
\end{array}
$$

* Cualquier argumento que podamos probar con este método será una tautología.


---

**Demuestre** usando el método de deducción que 
$$(P\Rightarrow Q)\land (Q\Rightarrow R)\Rightarrow (P\Rightarrow R)$$

**Demuestre** el siguiente argumento:

>Si la seguridad es un problema, entonces aumentaran las regulaciones. Si la seguridad no es un problema, entonces creceran las transacciones en la WEB. Por lo tanto, si la regulación no aumenta, entonces creceran las transacciones en la WEB.



---

**(Pequeña ayuda)**
Utilice las siguientes sentencias para formalizar el argumento:

- $P:\mbox{la seguridad es un problema}$
- $Q:\mbox{aumentaran la regulaciones}$
- $R:\mbox{creceran las transacciones en la WEB}$

[comment]: <> ($$(P\Rightarrow Q)\land (\neg P\Rightarrow R)\Rightarrow (\neg Q\Rightarrow R)$$)


# Ejercicios

### Ejercicios

Siendo $A$ verdadero, $B$ falso, y $C$ verdadero, ¿Cuál es el valor de verdad de cada una de las formas?

1. $A\land (B\lor C)$
2. $(A\land B)\lor C$
3. $\neg (A\land B)\lor C$
4. $\neg A\lor\neg(\neg B\land C)$

---

Escriba la negación de cada proposición:

1. Si la comida es buena, entonces el servicio es excelente.
1. La comida es buena o el servicio es excelente
1. O bien la comida es buena y el servicio excelente, o sino el precio es alto
1. La comida no es buena y el servicio tampoco es excelente
1. Si el precio es alto, entonces la comida es buena y el servicio es excelente 

---

Use las letras indicadas para cada proposición simple y represente simbólicamente cada proposición compuesta:

1. $A:\mbox{los precios suben}$;$B:\mbox{la vivienda será abundante}$;$C:\mbox{la vivienda será costosa}$. 

	*Si los precios suben, entonces la vivienda será abundante y cara; pero si la vivienda no es cara, entonces todavía será abundante*.

2. $A:\mbox{irse a dormir}$;$B:\mbox{ir a nadar}$;$C:\mbox{cambiarse ropa}$. 

	*Ya sea irse a dormir o a nadar es una condición suficiente para cambiarse ropa; de cualquier manera, cambiarse ropa no implica ir a nadar*.

---

1. $A:\mbox{va a llover}$;$B:\mbox{va a nevar}$. 

	*Va a llover o a nevar, pero no ambas*.
	
1. $A:\mbox{Javiera gana}$;$B:\mbox{Javiera pierde}$; $C:\mbox{Javiera estará cansada}$. 

	*Si Javiera gana or pierde, estará cansada*.
	
1. $A:\mbox{Javiera gana}$;$B:\mbox{Javiera pierde}$; $C:\mbox{Javiera estará cansada}$. 

	*Javiera va a ganar, o bien, si ella pierde, estará cansada*.

---

Represente formalmente cada argumento e indique qué regla de inferencia es ilustrada por cada argumento: 

1. Si María es la autora, entonces el libro es de ficción. Sin embargo, el libro no es de ficción. Por lo tanto, María no es la autora.
2. El perro tiene un abrigo brillante y adora ladrar. En consecuencia, el perro adora ladrar.
3. Si Pablito es un buen nadador, entonces es un buen corredor. Si Pablito es un buen corredor, entonces es un buen ciclista. Por lo tanto, si Pablito es un buen nadador, entonces es un buen ciclista.

---

Justifique cada paso de la prueba con la regla correcta:

1. $$A\land (B \Rightarrow C)\Rightarrow (B\Rightarrow (A\land C))$$

$$
\begin{array}{lll}
1. & A & \mbox{?}\\
2. & B\Rightarrow C & \mbox{?} \\ 
3. & B & \mbox{?}\\
4. & C & \mbox{?}\\ 
5. & A\land C & \mbox{?}
\end{array}
$$

---

2. $$\neg A\land B\land [B\Rightarrow (A\lor C)]\Rightarrow C$$

$$
\begin{array}{lll}
1. & \neg A & \mbox{?}\\
2. & B  & \mbox{?} \\ 
3. & B\Rightarrow (A\lor C) & \mbox{?}\\
4. & A\lor C & \mbox{?}\\ 
5. & \neg(\neg A)\lor C & \mbox{?} \\
6. & \neg A\Rightarrow C & \mbox{?} \\
7. &  C & \mbox{?} \\
\end{array}
$$

---

Utilice lógica proposicional para demostrar que cada argumento es válido:

1. $\neg(A\lor \neg B)\land (B\Rightarrow C)\Rightarrow (\neg A\land C)$
1. $\neg A\land (B\Rightarrow A)\Rightarrow \neg B$
1. $(A\Rightarrow B)\land[A\Rightarrow (B\Rightarrow C)]\Rightarrow(A\Rightarrow C)$
1. $[(C\Rightarrow D)\Rightarrow C]\Rightarrow [(C\Rightarrow D)\Rightarrow D]$
1. $(A\Rightarrow C)\land (C\Rightarrow \neg B)\land B\Rightarrow \neg A$
1. $[A\Rightarrow (B\lor C)]\land \neg C\Rightarrow(A\Rightarrow B)$


# Cuantificadores y Predicados

* Considere la proposición, "*Todas las personas que tienen la misma madre, son hermanos.*"
* Quisieramos poder inferir que a partir de "Todos los gatos tienen cola" y "Tom es un gato", "Tom tiene cola".
    * Díficil de representar usando letras, paréntesis y conectores lógicos
* Poder expresivo de proposiciones actuales es limitada

---

**Por lo tanto ...**

- Dado que poder expresivo de proposiciones es limitada
- Necesitamos un mecanismo para 
    - representar propiedades de objetos/individuos de un cierto dominio, 
    - construir nuevas proposiciones y 
    - calcular su valor de verdad 

## Cuantificadores

* Son frases que permiten especificar cuantos objetos tienen o cumplen con cierta propiedad
    * "Para cada", "Para todo", "Para cualquier" o "Para algún"
* El más usado es el **cuantificador universal**, representado por $\forall$, y se lee como "Para cada", "Para todo", "Para cualquier"
* Existen otros como el **existencial**, simbolizado por $\exists$, y se lee como "Existe uno", "Para al menos uno" o "Para agún"

**Por ejemplo** $(\forall x)(x>0)$

## Predicados
- Un cuantificador y el objeto sobre el que actúa o hace referencia generalmente se colocan entre paréntesis
- El segundo conjunto de paréntesis describe una propiedad satisfecha por el individuo o variable referenciada
- A esta manera de describir una propiedad se le denomina **Predicado**

**De manera más general, una proposición con predicados sería** $(\forall x)P(x)$

Para el ejemplo anterior $P(x)$ simboliza $x>0$

## Valor de verdad

* El valor de verdad de la expresión $(\forall x)P(x)$ depende del dominio al que pertencen los objetos $x$
* Por ejemplo
    * $Dom(x)$: animales de 4 patas y $P(x)$ tiene cola
    * $(\forall x)P(x)$ indica que todos los animales de 4 patas tienen cola.
    * $(\exists x)P(x)$ indica que existe al menos un animal de 4 patas tiene 
	
	
---

### Ejemplos adicionales

1. Sea $P(x)$ el predicado que indica "$x > 3$". ¿Cuales son los valores de verdad de $P(4)$ y $P(2)$?
1. Sea $Q(w)$ el predicado "$w$ es una carrera del IES-PUCV". Suponga que solo Ingeniería Estadística (IE) y Estadistica (E) son impartidas por el IES, y que Teología (T) es otra carrea PUCV ¿Qué valores de verdad tienen los predicados $Q(E)$, $Q(T)$ y $Q(IE)$?


---

### Ejercicios

1. Construir una interpretación de $(\forall x)P(x)$ que tenga valor verdadero
2. Construir una interpretación de $(\forall x)P(x)$ que tenga valor falso

Hasta ahora solo hemos revisado predicados que representan la propiedad de un solo objeto o variable. Los predicados pueden ser binarios, ternarios o n-arios.

## Predicados n-arios

- En ocasiones nos interesará describir propiedades o relaciones entre varios individuos
    - "María es madre de Teresa"
    - "Los números 2, 3 y 4 son sucesores entre sí"

---

-  Podemos ahora integrar el uso de estos predicados con los cuantificadores anteriores
    - "Para todo número entero $x$, existe otro $y$ tal que este $y$ es mayor que $x$"
    - La expresión $(\forall x)(\exists y)Q(x, y)$ simboliza esta última proposición.
    - ¿Qué indicaría $(\exists y)(\forall x)Q(x, y)$?

	
---

### Ejemplos

<!-- pag. 31, rosen -->
1. Sea $Q(x,y)$ la sentencia que indica "x=y+3". ¿Qué valores de verdad tienen las proposiciones $Q(10, 7)$ y $Q(7, 10)$?
1. Sea $F(a, b)$ la sentencia $a$ es *follower* de $b$. Se sabe que María (M) sigue a Tomas (T) y Pepa (P), y esta última solo sigue a María de vuelta. Entonces, ¿qué valores tienen las proposiciones $F(M, T)$, $F(P, M)$ y $F(P, T)$?

---

### Acerca de la notación

- Hasta ahora hemos usado variables ($x, y \ldots$) y constantes (*Tom*, *María* $\ldots$) sin hacer mayor distinción
- Es importante notar que en expresiones como $(\forall x)P(x)$, $x$ es una variable que representa a cualquier elemento del dominio **(comienzan con minúscula)**

---

- El valor de verdad de esta proposición es independiente de qué individuo del dominio sea referenciado
- Podría haberse escrito $(\forall z)P(z)$ o $(\forall w)P(w)$ y tendría la misma interpretación
- Las constantes sirven para hacer referencia a objetos específicos en el dominio **(comienzan con mayúscula)**

---

### En síntesis

Para interpretar una expresión que contenga predicados se necesita:

* Colección no vacía de objetos, es decir el Dominio 
* La asignación de una propiedad de los objetos del dominio para cada predicado
* La asociación de un objeto específico del dominio a cada constante usada en la expresión

Ahora podemos usar toda la simbología revisada hasta ahora para construir proposiciones con predicados simples y compuestas

---

Como interpretaría la siguiente sentencia
$$(\forall x)(\exists y)[S(x,y)\land L(y, a)]$$
Si el dominio consiste en todas las ciudades de Chile, $S(x,y)$ denota la relación "$x$ e $y$ están en la misma región" y $L(y, a)$ denota "$y$ comienza con la misma letra que $a$".

Establezca en lenguaje natural la afirmación planteada por la proposición.

## Traduciendo del lenguaje natural

Si se dice "Todo auto tiene una falla", lo que realmente se está indicando es que 

1. Para cualquier cosa, 
2. si es un auto ($P(x)$), entonces 
3. tiene una falla ($Q(x)$)

Entonces, 

$$(\forall x)[P(x)\Rightarrow Q(x)]$$

---

### Más ejemplos

Considere la frase "Hay alguien que conoce a todo el mundo".

- Formalización inicial: $\exists x(x\mbox{ conoce a todo el mundo})$
- $x$ conoce a todo el mundo aún no tiene el suficiente nivel de representación simbólica, ya que se está expresando una propiedad usando lenguaje natural

¿Como podría corregirse la representación? Por ejemplo, introduzca una relación $Q(x,y)$ que indica "$x$ conoce a $y$".

---

- Exprese ahora como un predicado la frase "Todo el mundo tiene a alguien que sea su madre".
    - Utilice la relación $M(x,y)$ que indica "$x$ es la madre de $y$".
    - Considere que el predicado $\exists x M(x,y)$ indica "alguien es la madre de $y$".

---

### Ejercicio

Siendo las sentencias $D(x)$ "$x$ es un perro", $R(x)$ "$x$ es un conejo" y $C(x,y)$ "$x$ persigue a $y$".

Traduzca las siguientes sentencias:

1. Todos los perros persiguen a todos los conejos.
2. Algunos perros persiguen a todos los conejos.
3. Solo los perros persiguen a los conejos. 

---

### Negando expresiones con cuantificadores

* A menudo usamos cuantificadores como "nadie" o "ninguno"
* Esto equivale en el cálculo de predicados a que ningún individuo posea una cierta propiedad
* Por ejemplo, "Nadie es perfecta".
    * Suponiendo que $P(x)$ indica "$x$ es perfecta"
	
<!--    * Podría expresarse de dos maneras: $\neg\exists x P(x)$ o $\forall x\neg P(x)$
* Estas dos expresiones son equivalentes, es decir 
$$\neg\exists x P(x) \equiv\forall x\neg P(x)$$-->

---

Para un universo finito de $n$ individuos $A_1,A_2,\ldots A_n$ 
$$\forall x P(x) \equiv P(A_1)\land P(A_2)\land \ldots P(A_n)$$
donde $P(x)$ es $V$ o $F$ para c/individuo del **dominio** (siempre debe haber uno definido).

Para el cuantificador existencial también existe una expresión similar
$$\exists x P(x) \equiv P(A_1)\lor P(A_2)\lor \ldots P(A_n)$$

---

Usando las definiciones anteriores **demuestre** que 

1. $$\neg [\forall x P(x)] \equiv \exists x \neg P(x)$$
2. $$\neg [\exists x P(x)] \equiv \forall x \neg P(x)$$

---

Considerando a los seres vivos del planeta tierra como dominio ¿Como fomalizaría las siguientes expresiones?

1. "Todos los seres humanos son mamíferos"
    - $\forall x (humano(x) \Rightarrow mamifero(x))$
1. "Algunos seres humanos son mujeres"
    - $\exists x (humano(x) \land mujer(x))$
1. "Solo piensan los seres humanos"
    - $\forall x (piensa(x) \Rightarrow humano(x))$

*Observe* asociaciones $\forall$ con $\Rightarrow$, y $\exists$ con $\land$ usadas para **restringir** el dominio

---

Cual sería la expresión resultante de 
$$\neg [ \forall x (piensa(x) \Rightarrow humano(x))]$$

Intente tomar el predicado resultante y expresarlo en lenguaje natural ¿Tiene sentido?
<!-- SOLUC.: Algun ser vivo piensa y no es humano-->

## Validez de predicados

- Existen infinitas interpretaciones para una expresión con predicados
- Un predicado es válido si es verdadero en todas sus posibles **interpretaciones**
- Validez quiere decir intrinsecamente cierto
- para proposiciones usabamos tablas de verdad... No es posible para predicados
- Basta un caso o interpretación en que el predicado sea falso para decidir su no validez 

---

Una **interpretación** de una expresión con predicados consiste de:

1. Colección de objetos, denominada dominio de interpretación
1. La asignación de una propiedad de los objs. del dominio para cada predicado
1. La asignación de un obj. particular del dominio para cada simbolo constante en la expresión

---

### Una posible interpretación para $\exists x \forall y Q(x,y)$

**Considere** un universo de discurso o dominio constituido por  3 personas: **J**uan, **M**aría y **X**imena. Además, definamos $Q(x,y)$ cómo el predicado "*$x$ admira a $y$*", cuyas asignaciones son las siguientes:


| $x \| y$  | J | M | X |
|---|---|---|---|
| **J** | F | V | V |
| **M** | V | F | F |
| **X** | F | V | V |


Examinemos si es cierta o no la frase: "Hay alguien que admira a todo el mundo".

---

* Primero debemos expresar esta frase en términos de un predicado. 
* $\forall y Q(x,y)$ equivale a decir "$x$ admira a todo el mundo".
* "Hay alguien que admira a todo el mundo" **entonces** puede expresarse como $\exists x \forall y Q(x,y)$

* Analicemos primero el valor de verdad de $\forall y Q(x,y)$. 
* Si encontramos al menos una interpretación en que sea cierta será suficiente ¿Existe alguna?

<!-- SOLUC. No existe ningun caso, entonces la frase es falsa.-->

---

### Acerca de determinar la validez
+ No es posible examinar todas las interpretaciones
+ Deberemos razonar usando las reglas que ya conocemos 
+ A veces resultará mejor encontrar una interpretación que sea falsa para demostrar la "no validez"

---

### Algunas expresiones (genéricas) válidas


$$\forall x P(x) \Rightarrow \exists x P(x)\mbox{(hint: la prop. inversa no es válida)}$$

$$\forall x P(x) \Rightarrow P(A)$$

$$\forall x [P(x)\land Q(x)]\iff \forall x P(x) \land \forall x Q(x)$$

$$P(x)\Rightarrow [Q(x)\Rightarrow P(x)] \mbox{(hint: revise tabla de implicancia)}$$


## Lógica de Predicados

* Al examinar proposiciones, revisamos expresiones  de la forma $P_1\land \ldots \land P_n\Rightarrow Q$ denominadas argumentos.
* Su validez consiste en poder deducir lógicamente $Q$ a partir únicamente de la estructura interna de las premisas y **no** de los valores particulares de las premisas.
* Ahora estudiaremos el mismo proceso, pero considerando predicados, cuantificadores y conectores lógicos.

---

* Por lo tanto, buscaremos demostrar que la expresión bien formada
$$P_1\land \ldots \land P_n\Rightarrow Q$$
es verdadera in todas las posibles interpretaciones.

* El sistema formal que nos permite razonar en este sentido se denomina **Lógica de Predicados**
* Para esto, usaremos reglas de derivación para poder transitar desde las hipotesis hasta la conclusión
* Todas las reglas ya vistas también son parte de este sistema

---

### Nuevas reglas de inferencia 

* Idea general para la demostración de validez:
    * Quitar los cuantificadores, manipular usando reglas proposicionales y re-incorporar los cuantificadores
* Proveen de un mecanismo para quitar y luego insertar los cuantificadores
* Son 4: **Instanciación** (Universal | Existencial); **Generalización** (Universal | Existencial);

---

### Instanciación Universal

* Es una manera de descomponer el cuantificador en múltiples variables o también constantes del dominio
* Esta regla permite que a partir de $\forall P(x)$ se derive $P(A), P(x), P(y), P(z), \ldots$
* La variable sustituída no puede aparecer dentro del ámbito de otro cuantificador
    **Ejemplo (incorrecto)** $(\forall x)(\exists y)P(x,y)$, se sustituye $x$ por $y$ y lleva a $(\exists y)P(y,y)$

---

#### Ejemplo
Considere el argumento 

	"Todos los humanos son mortales. Socrates es humano. 
	        Por lo tanto, Socrates es mortal."


Esto puede formalizado como

- $H(x)$ es "x es humano".
- $S$ es una constante que simboliza a Socrates.
- $M(x)$ es "x es mortal"

---

El argumento queda expresado como
$$(\forall x)[H(x)\Rightarrow M(x)]\land H(S)\Rightarrow M(S)$$

---

El argumento queda expresado como
$$(\forall x)[H(x)\Rightarrow M(x)]\land H(S)\Rightarrow M(S)$$

La demostración es
$$
\begin{array}{llr}
   1.& (\forall x)[H(x)\Rightarrow M(x)]& \mbox{hip.}\\
   2.& H(S)                             & \mbox{hip.}\\
   3.& H(S)\Rightarrow M(S)             & \mbox{1, I.U.}\\ 
   4.& M(S)                             & \mbox{2,3, M.P.}
\end{array}
$$

---

### Ejercicio

Demostrar el argumento expresado como
$$(\forall x)[P(x)\Rightarrow R(x)]\land \neg R(y)\Rightarrow \neg P(y)$$

---

Demostrar el argumento expresado como
$$(\forall x)[P(x)\Rightarrow R(x)]\land \neg R(y)\Rightarrow \neg P(y)$$


$$
\begin{array}{llr}
   1.& (\forall x)[P(x)\Rightarrow R(x)]& \mbox{hip.}\\
   2.& \neg R(y)                        & \mbox{hip.}\\
   3.& P(y)\Rightarrow R(y)             & \mbox{1, I.U.}\\ 
   4.& \neg P(y)                        & \mbox{2,3, M.T.}
\end{array}
$$

---

### Instanciación Existencial

* Permite quitar el cuantificador existencial $\exists$
* Indica que a partir de $\exists x P(x)$ podemos derivar $P(A)$ o $P(B)$ o cualquier otra constante
* La constante usada en la derivación debe haber sido introducida justo antes de usar la regla

---

#### Ejemplo

Demostrar el argumento expresado como
$$\forall x[P(x)\Rightarrow Q(x)]\land \exists y P(y)\Rightarrow Q(A)$$

---

Demostrando $\forall x[P(x)\Rightarrow Q(x)]\land \exists y P(y)\Rightarrow Q(A)$

$$
\begin{array}{llr}
   1.& (\forall x)[P(x)\Rightarrow Q(x)]& \mbox{hip.}\\
   2.& \exists y P(y)                   & \mbox{hip.}\\
   3.& P(A)                             & \mbox{2, I.E.}\\ 
   4.& P(A)\Rightarrow Q(A)             & \mbox{1, I.U.}\\
   5.& Q(A)                             & \mbox{3,4, M.P.}\\
\end{array}
$$

La I.E. **debe** ser la primera regla usada. Si se invierte el orden de los pasos 3 y 4, **no** se podría suponer que ese $A$ específico es el que cumple con $P(A)$.

---

### Generalización Universal

<!--Ahora revisaremos las dos reglas que permiten insertar los cuantificadores-->
* Permite insertar un cuantificador universal
* Si sabemos que se cumple $P(x)$ para cualquier objeto del dominio, entonces podemos concluir que $\forall xP(x)$.
* Deberemos tener cuidado de que $x$ no represente a un individuo en particular.


---

### Ejemplo

Demostrar el argumento expresado como
$$\forall x[P(x)\Rightarrow Q(x)]\land \forall x P(x)\Rightarrow \forall x Q(x)$$

---

Demostrando $\forall x[P(x)\Rightarrow Q(x)]\land \forall x P(x) \Rightarrow \forall x Q(x)$

$$
\begin{array}{llr}
   1.& \forall x[P(x)\Rightarrow Q(x)]  & \mbox{hip.}\\
   2.& \forall x P(x)                   & \mbox{hip.}\\
   3.& P(x)\Rightarrow Q(x)             & \mbox{1, I.U.}\\ 
   4.& P(x)                             & \mbox{2, I.U.}\\
   5.& Q(x)                             & \mbox{3,4, M.P.}\\
   6.& \forall x Q(x)                   & \mbox{5, G.U.}\\
\end{array}
$$

---

- No existe restricción de re-usar la variable $x$ sobre I.U. en el paso 4.
- La variable $x$ es arbitraria, ya que en los pasos 3 y 4 representa a cualquier elemento en el dominio.
- La variable sobre la que se generaliza no puede aparecer **libre**  en ninguna hipotesis 
- Tampoco puede haber sido deducida en una I.E. a partir de una formula en que aparece **libre**

**Ejemplo** Siendo $P(x)$ una de las hipotesis, *no* podría derivarse $\forall  x P(x)$, debido a que $x$ aparece **libre**.

---

#### Ejemplo

Dada la hipotesis $(\forall x)(\exists y)Q(x,y)$, ¿sería válida la secuencia?

$$
\begin{array}{llr}
   1.& (\forall x)(\exists y)Q(x,y)     & \mbox{hip.}\\
   2.& (\exists y)Q(x,y)                & \mbox{1, I.U.}\\
   3.& Q(x,A)                           & \mbox{2, I.E.}\\ 
   4.& (\forall x)Q(x,A)                & \mbox{3, G.U.}\\ 
\end{array}
$$

---

### Generalización Existencial

- Permite la inserción de un cuantificador existencial a partir de $P(x)$ o $P(A)$
- Si algún individuo $x$ cumple la $P$, entonces se deriva $\exists x P(x)$


**Ejemplo** Probar que $(\forall x)P(x)\Rightarrow (\exists x)P(x)$

$$
\begin{array}{llr}
   1.& (\forall x)P(x)                  & \mbox{hip.}\\
   2.& P(x)                             & \mbox{1, I.U.}\\
   3.& (\exists x)P(x)                  & \mbox{2, G.E.}\\ 
\end{array}
$$

---

- Para ir de $P(A)$ a $\exists xP(x)$, $x$ no puede aparecer en $P(A)$. 
- Por **ejemplo**: A partir de $P(A,y)$ derivar $(\exists y)P(y,y)$
    - No es válido porque la variable que sustituyó a la const. $A$ aparece en el predicado sobre el cual se aplicó la G.E.

---

### Estrategia General

* Quitar los cuantificadores
* Operar con las expresiones resultantes
* Insertar cuantificadores tanto como sea necesario

---

### El Método de la deducción con cuantificadores

- **Esquema general:** $P_1\land P_2\land\ldots \land P_m \Rightarrow (B\Rightarrow C)$
- Estrategia general: Se supone $B$, se demuestra $C$ usando $B$ como premisa y se concluye $B\Rightarrow C$. Finalmente, se prescinde de $B$.
- Recordar que para G.U. la variable sobre la que se generaliza no puede aparecer libre en ninguna hipotesis
    - Si sólo $B$ contiene a $x$ como variable libre, aún podría aplicarse la G.U.
    - La aplicación de esta propiedad  puede realizarse luego de prescindir de $B$.

---

#### Ejemplo

Determine la validez de 
$$\forall x[S(x)\Rightarrow P(x)]\Rightarrow \forall x[\neg P(x)\Rightarrow  \neg S(x)]$$

$$
\begin{array}{llr}
   1.& \forall x[S(x)\Rightarrow P(x)]  & \mbox{hip.}\\
   2.& S(x)\Rightarrow P(x)             & \mbox{1, I.U.}\\
   3.& \neg P(x)                        & \mbox{*hip}\\
   4.& \neg S(x)                        & \mbox{2, 3, M.T.}\\ 
   5.& \neg P(x)\Rightarrow \neg S(x)   & \mbox{3, 4, M.Ded.}\\
   6.& \forall x [\neg P(x)\Rightarrow \neg S(x)]   & \mbox{5, G.U.}\\
\end{array}
$$


