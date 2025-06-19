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


## ¿Qué es LDA?

- LDA aparece a principio del 2000
- Incluye un modelo generativo para los documentos, además de los tópicos
- Cada documento es una mezcla de temas
- Cada tema es una distribución de palabras
- Distribución apriori de tópicos es una Dirichlet

Referencias: [Blei et al. 2003](http://www.jmlr.org/papers/volume3/blei03a/blei03a.pdf)

——-

### Distribuciones de probabilidad en LDA

- \( \theta_d \sim \text{Dirichlet}(\alpha) \): distribución de temas en un documento.
- \( \phi_k \sim \text{Dirichlet}(\beta) \): distribución de palabras en un tema.
- \( z_{d,n} \sim \text{Multinomial}(\theta_d) \): elección de tema para palabra \( n \) en documento \( d \).
    \item \( w_{d,n} \sim \text{Multinomial}(\phi_{z_{d,n}}) \): elección de palabra según el tema.


### Estimación de parámetros

- El modelo observa solo las palabras. Los temas son variables latentes.
- Se busca inferir:
  - \( \theta_d \): proporción de temas en cada documento.
  - \( \phi_k \): distribución de palabras por tema.
  - \( z_{d,n} \): asignación de temas a palabras.
 
- Métodos comunes:
  -  Muestreo de Gibbs (Gibbs Sampling)
  - Inferencia variacional (Variational Bayes)

### ¿Qué es Gibbs Sampling?

- Método de Monte Carlo para estimar distribuciones condicionales.
- En LDA:
  - Se fija el tema de todas las palabras excepto una.
  - Se estima la probabilidad condicional de cada posible tema para esa palabra.
  - Se repite este proceso para todas las palabras, muchas veces.
- El resultado converge a una estimación de la distribución posterior conjunta.



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
