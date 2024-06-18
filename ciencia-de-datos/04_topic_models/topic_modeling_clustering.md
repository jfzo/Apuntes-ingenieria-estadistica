---
title: EST-297
subtitle: Fundamentos de Ciencia de Datos
author: Juan Zamora O.
date: Junio, 2024.
fonttheme: "professionalfonts"
fontsize: 11pt
theme: default
innertheme: circles
urlcolor: blue
linkstyle: bold
aspectratio: 169
titlegraphic: logosAzul.png
logo: logoAzul.png
section-titles: false
toc: true
toc-title: Estructura de la Presentación
section-titles: false
---

# Aproximaciones Low-Rank para Clustering

Una matriz $X$ de rango $r$ admite una factorización de la forma $$X=BC^T, \ B\in\mathbf{R}^{m\times r}, \ C\in\mathbf{R}^{n\times r}$$


$X$ es aproximada con bajo rango (low-rank) cuando $rango(X) << \min(m,n)$

\begin{tikzpicture}[remember picture, overlay]
\node[yshift=2.7cm, xshift=0cm] at (current page.south) 
{
    \includegraphics[width=0.4\textwidth]{nmf_view.png}
};
\end{tikzpicture}    

# (NMF) Factorización de matrices no-negativas

- Grupo de algoritmos de de análisis multivariado y algebra lineal donde una matriz $X$ es factorizada en dos matrices $W$ y $H$
- Cada columna de $X$ es aproximada por una combinación lineal no-negativa de las columnas de $W$, donde los coeficientes de mezcla corresponden a las columnas de $H$ 
- Las tres matrices tienen elementos no-negativos
- Usado en sistemas recomendadores, procesamiento de audio, agrupamiento de texto.

# NMF

- Dada  una matriz no-negativa $X\in \mathbf{R}^{m\times n}$ y un $k\in\mathbf{Z}<< \min(m,n)$
- Encuentra matrices no-negativas $W\in \mathbf{R}^{m\times k}$ y $H\in \mathbf{R}^{k\times n}$ tales que minimizan $$\lVert X-WH \rVert^{2}_{F}=\sum_i\sum_j(X_{ij}-[WH]_{ij})^2$$

* $W$: base para un espacio $k$-dimensional, la $i$-ésima columna de H: corresponde a representación k-dim de $i$-ésima columna de $X$

# Aplicación de NMF para extracción de tópicos en texto

- Se construye matriz de terminos vs documentos
- Se aplica NMF para obtener $W$ y $H$


\begin{tikzpicture}[remember picture, overlay]
\node[yshift=3.5cm, xshift=0cm] at (current page.south) 
{
    \includegraphics[width=0.8\textwidth]{nmf_ex_topics.png}
};
\end{tikzpicture}    

## Clustering y Modelos estadísticos de Texto

- Abundante en diversos dominios (redes sociales, medios digitales, registros en salud ...)
- Resulta útil poder explorar estas coleciones de alguna manera asistida
- Clustering permite caracterizar de manera *automática* una colección de documentos
- A finales de los 90, aparecieron varios modelos estadístico de texto usando un modelo de mezcla sobre variables aleatorias multinomiales
    - LSI
    - pLSI

---

- LDA aparece a principio del 2000
- Incluye un modelo generativo para los documentos, además de los tópicos
- La idea es que documentos son representados como mezclas aleatorias de tópicos latentes
- Cada tópico se caracteriza como una una distribución sobre las palabras
- Distribución apriori de tópicos es una Dirichlet

Referencias: [Blei et al. 2003](http://www.jmlr.org/papers/volume3/blei03a/blei03a.pdf)

## Idea fundamental

* Consideremos un conjunto de $D$ documentos $\{W_1,W_2\ldots W_D\}$ 
* Cada documento $W_d$ contiene $N_d$ palabras, es decir $W_d=\{w_{d1},w_{d2}\ldots w_{dN_d}\}$
* El objetivo es agrupar los documentos y sus palabras en $G$ grupos, denominados *tópicos*


## El Modelo *generativo* LDA

- Para cada documento $W_d$ de los $D$ documentos, $\theta_d$ representa su proporción de tópicos y $\theta_d\sim Dir(\alpha)$
    - $\alpha=(\alpha_1,\alpha_2\ldots \alpha_G)$ es un apriori común sobre los tópicos para todos los documentos
- La distribución $\psi_g$, para el tópico $g\in\{1\ldots G\}$ también cumple con que $\psi_g\sim Dir(\beta)$
    - $\beta=(\beta_1,\beta_2\ldots \beta_V)$ y $V$ es el tamaño del vocabulario
- Luego, el tópico $z_{id}$ de la $i$-ésima palabra en el documento $d$ sigue una distribución multinomial, es decir $z_{id}\sim M(1,\theta_d)$

## El Modelo *generativo* LDA

- Dado este tópico $z_{id}$, la $i$-ésima palabra en el documento $d$ es también tomada a partir de una distribución multinomial, es decir $w_{id}\sim M(1,\psi_{z_{id}})$
- Notar que la distribución de palabras sobre los tópicos es una mezcla de multinomiales 
$$w_{id}|\theta\sim \sum_{g=1}^{G}\theta_{dg}M(1, \psi_g)$$

---

### Resumen gráfico de LDA

- La inferencia puede ser realizada usando el algoritmo *EM Bayesiano Variacional*, MCMC o Expectation-Propagation

\begin{tikzpicture}[remember picture, overlay]
\node[yshift=3.0cm, xshift=0cm] at (current page.south)
{
    \includegraphics[width=0.6\textwidth]{tm_model.png}
};
\end{tikzpicture}

---

### *Ejemplo* de las palabras más representativas en $11$ tópicos 

\begin{tikzpicture}[remember picture, overlay]
\node[yshift=3.4cm, xshift=0cm] at (current page.south)
{
    \includegraphics[width=1.05\textwidth]{topics_top10palabras.jpeg}
};
\end{tikzpicture}

---

\begin{tikzpicture}[remember picture, overlay]
\node[yshift=4cm, xshift=0cm] at (current page.south)
{
    \includegraphics[width=0.9\textwidth]{heat_topics.png}
};
\end{tikzpicture}



## ¿De qué sirve esta perspectiva generadora de documentos?

* Existen técnicas estadísticas y computacionales para invertir este procedimiento a partir de documentos existentes (...nuestros documentos), pudiendo así inferir la composición *más probable* de los tópicos que permitieron generar esta colección de documentos.

* Los tópicos estimados tienen un significado identificado por el/la analista

* Para encontrar la cantidad de tópicos se utiliza una medida denominada *Perplexity*
    - Se calcula tomando la log-verosimilitud de los documentos con los tópicos resultantes
    - Que tanto es posible reproducir la composición de los documentos dados los tópicos
    - El bjetivo es escoger el número de tópicos que minimiza la Perplexity 
