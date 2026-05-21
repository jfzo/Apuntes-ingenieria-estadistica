---
title: EST-1141
subtitle: Lenguajes de Programación
author: Juan Zamora O.
date: Programación funcional
fonttheme: "professionalfonts"
fontsize: 11pt
theme: default
innertheme: circles
urlcolor: blue
linkstyle: bold
aspectratio: 169
titlegraphic: logosAzul.png
logo: logoAzul.png
toc: true
toc-title: Estructura
section-titles: false
---


# Introducción
<!--
 pandoc -t beamer  02_programacion_funcional.md -o 02_programacion_funcional_new.pdf --katex --slide-level=2
 -->

<!--https://haskell.mooc.fi/part1-->
- Diseño de lenguajes imperativos se basa directamente en la arquitectura de von Neumann
	- Principal preocupación es la eficiencia
- El diseño de lenguajes funcionales se basa en funciones matemáticas
	- Base teórica sólida y cercana al usuario que no tiene mucha relación con la arquitectura de las máquinas sobre las cuales correran sus programas

# Funciones matemáticas

- Corresponde a una asociación de miembros desde un conjunto (dominio) a otro (range)
- Una expresión *lambda* especifica los parámetros y la asociación de una función en la forma:
$$\lambda(a)\ a\times a\times a$$

para la función $\mbox{cubo}(a)=a\times a \times a$

## Expresiones Lambda ($\lambda$)

- Expresiones lambda describen funciones sin nombre
- Se aplican sobre un parámetro colocando el parámetro al final de la expresión

$$(\lambda(a)\ a\times a\times a )\ (2)$$ 
- lo cual se evalua a 8

## Formas funcionales

- Una función de mayor nivel o *forma funcional* es aquella que toma funciones como parámetros, que genera una función como resultado o ambas

## Composición de funciones

- Forma funcional que toma 2 funciones como parámetros
- produce una función cuyo valor corresponde a la aplicación del primero sobre la aplicación del segundo
- Para $f(x)=x+2$ y $g(x)=3 *x$, $h=f\circ g$ produce $f(g(x))$ es decir $(3*x)+2$

## Aplicar a todo (apply-to-all)

- Forma funcional que toma una sola función como parámetro
- produce una lista de valores obtenidos luego de aplicar la función dada sobre cada elemento de una lista de parámetros
- Se simboliza con la letra $\alpha$
- Para $h(x)=x*x$, $\alpha(h, (2,3,4))$ produce $(4,9,16)$


# Fundamentos de lenguajes de programación funcional
- El objetivo es imitar el comportamiento de las funciones matemáticas

---

- Proceso de computo es fundamentalmente distinto al de un lenguaje imperativo
	- En un L.Imperativo las operaciones se realizan y sus resultados se almacenan en variables para su uso posterior
	- El manejo de variables es una preocupación constante y a la vez una fuente de complejidad

- En el paradigma funcional las variables no son necesarias (al igual que en matemáticas)

---

- En un lenguaje funcional la evaluación de una función siempre producirá el mismo resultado para los mismos parámetros (*transparencia referencial*)
- La iteración es llevada a cabo mediante llamadas recursivas a funciones (*recursión de cola*)