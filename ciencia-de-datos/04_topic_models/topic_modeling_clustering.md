---
title: EST-297
subtitle: Modelos de Clustering para Texto
author: Juan Zamora O.
date: Ciencia de Datos
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
classoption: t 
toc-title: Estructura de la Presentación
graphics: true
imagepath: ./imgs
linespread: 1.2
---

# Aproximaciones Low-Rank para Clustering

Una matriz $X$ de rango $r$ admite una factorización de la forma 
$$X=BC^T, \ B\in\mathbf{R}^{m\times r}, \ C\in\mathbf{R}^{n\times r}$$


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
- Encuentra matrices no-negativas $W\in \mathbf{R}^{m\times k}$ y $H\in \mathbf{R}^{k\times n}$  tales que minimizan $$\lVert X-WH \rVert^{2}_{F}=\sum_i\sum_j(X_{ij}-[WH]_{ij})^2$$

* $W$: base para un espacio $k$-dimensional, la $i$-ésima columna de H: corresponde a representación k-dim de $i$-ésima columna de $X$


## Método de Lee y Seung (2001)
    
Lee y Seung propusieron reglas de actualización multiplicativas para minimizar:
$$
    \min_{W,H \geq 0} \| V - WH \|_F^2
$$

Las reglas de actualización son:
\begin{align*}
    H &\leftarrow H \circ \frac{W^\top V}{W^\top WH} \\
    W &\leftarrow W \circ \frac{V H^\top}{WHH^\top}
\end{align*}
donde $\circ$ denota el producto elemento a elemento (Hadamard).

---

### Ejemplo numérico: datos iniciales

#### Matriz original y objetivo

Matriz original $V$:

$$
V = \begin{bmatrix}
5 & 3 \\
3 & 2 \\
4 & 1
\end{bmatrix}
$$

Factorizar $V \approx W H$, con $W \in \mathbb{R}^{3 \times 2}_{\geq 0}$, $H \in \mathbb{R}^{2 \times 2}_{\geq 0}$.

---

### Inicialización

Matrices iniciales:

$$
W^{(0)} = \begin{bmatrix}
1 & 0.5 \\
0.5 & 1 \\
1 & 1
\end{bmatrix}
\quad , \quad
H^{(0)} = \begin{bmatrix}
1 & 2 \\
1 & 1
\end{bmatrix}
$$

---

### Iteración 1: Actualización de $H$
$$
H_{ij} \leftarrow H_{ij} \times \frac{(W^T V)_{ij}}{(W^T W H)_{ij}}
$$

$$
W^T V = \begin{bmatrix}
9.5 & 4.0 \\
9.5 & 4.5
\end{bmatrix}
\quad , \quad
W^T W H^{(0)} = \begin{bmatrix}
4.25 & 6.5 \\
4.25 & 6.25
\end{bmatrix}
$$

$$
H^{(1)} = \begin{bmatrix}
2.235 & 1.231 \\
2.235 & 0.72
\end{bmatrix}
$$

---

### Iteración 1: Actualización de $W$
$$
W_{ij} \leftarrow W_{ij} \times \frac{(V H^T)_{ij}}{(W H H^T)_{ij}}
$$

$$
V H^{(1)T} = \begin{bmatrix}
14.88 & 13.365 \\
9.21 & 8.085 \\
10.171 & 9.16
\end{bmatrix}
\quad , \quad
W^{(0)} H^{(1)} H^{(1)T} = \begin{bmatrix}
9.54 & 8.49 \\
8.06 & 8.4 \\
12.6 & 11.26
\end{bmatrix}
$$

$$
W^{(1)} = \begin{bmatrix}
1.56 & 0.79 \\
0.57 & 0.96 \\
0.81 & 0.81
\end{bmatrix}
$$

---

### Iteración 2: Actualización de $H$

$$
W^{(1)T} V = \begin{bmatrix}
13.89 & 6.75 \\
11.37 & 5.04
\end{bmatrix}
\quad , \quad
W^{(1)T} W^{(1)} H^{(1)} = \begin{bmatrix}
12.98 & 5.76 \\
9.94 & 4.21
\end{bmatrix}
$$

$$
H^{(2)} = \begin{bmatrix}
2.39 & 1.44 \\
2.56 & 0.86
\end{bmatrix}
$$

---

### Iteración 2: Actualización de $W$

$$
V H^{(2)T} = \begin{bmatrix}
20.35 & 17.45 \\
12.87 & 11.12 \\
11.98 & 10.17
\end{bmatrix}
\quad , \quad
W^{(1)} H^{(2)} H^{(2)T} = \begin{bmatrix}
18.1 & 15.7 \\
14.9 & 13.2 \\
15.9 & 14.2
\end{bmatrix}
$$

$$
W^{(2)} = \begin{bmatrix}
1.75 & 0.88 \\
0.49 & 0.81 \\
0.61 & 0.58
\end{bmatrix}
$$

---

### Iteración 3: Actualización de $H$

$$
W^{(2)T} V = \begin{bmatrix}
14.6 & 7.1 \\
11.4 & 5.2
\end{bmatrix}
\quad , \quad
W^{(2)T} W^{(2)} H^{(2)} = \begin{bmatrix}
13.9 & 6.1 \\
10.7 & 4.7
\end{bmatrix}
$$

$$
H^{(3)} = \begin{bmatrix}
2.51 & 1.68 \\
2.73 & 0.95
\end{bmatrix}
$$

---

### Iteración 3: Actualización de $W$

$$
V H^{(3)T} = \begin{bmatrix}
21.2 & 18.1 \\
13.2 & 11.5 \\
12.1 & 10.5
\end{bmatrix}
\quad , \quad
W^{(2)} H^{(3)} H^{(3)T} = \begin{bmatrix}
19.3 & 16.8 \\
15.8 & 14.0 \\
16.8 & 15.0
\end{bmatrix}
$$

$$
W^{(3)} = \begin{bmatrix}
1.92 & 0.95 \\
0.41 & 0.67 \\
0.44 & 0.41
\end{bmatrix}
$$

---

### Iteración 4: Actualización de $H$ y resultado final

$$
W^{(3)T} V = \begin{bmatrix}
15.1 & 7.3 \\
11.2 & 5.0
\end{bmatrix}
\quad , \quad
W^{(3)T} W^{(3)} H^{(3)} = \begin{bmatrix}
14.6 & 6.4 \\
10.9 & 4.7
\end{bmatrix}
$$

$$
H^{(4)} = \begin{bmatrix}
2.60 & 1.92 \\
2.80 & 1.01
\end{bmatrix}
$$

---

Resultado final aproximado:

$$
W^{(4)} \approx \begin{bmatrix}
1.92 & 0.95 \\
0.41 & 0.67 \\
0.44 & 0.41
\end{bmatrix}
\quad , \quad
H^{(4)} \approx \begin{bmatrix}
2.60 & 1.92 \\
2.80 & 1.01
\end{bmatrix}
$$

y

$$
W^{(4)} H^{(4)} \approx V
$$


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

---

### Distribuciones de probabilidad en LDA

- $\theta_d \sim \text{Dirichlet}(\alpha)$: distribución de temas en un documento.
- $\phi_k  \sim \text{Dirichlet}(\beta)$: distribución de palabras en un tema.
- $z_{d,n} \sim \text{Multinomial}(\theta_d)$: elección de tema para palabra$n$en documento$d$.
- $w_{d,n} \sim \text{Multinomial}(\phi_{z_{d,n}})$: elección de palabra según el tema.

---

### Estimación de parámetros

- El modelo observa solo las palabras. Los temas son variables latentes.
- Se busca inferir:
  - $\theta_d$: proporción de temas en cada documento.
  - $\phi_k$: distribución de palabras por tema.
  - $z_{d,n}$: asignación de temas a palabras.
 
- Métodos comunes:
  -  Muestreo de Gibbs (Gibbs Sampling)
  - Inferencia variacional (Variational Bayes)

---

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
\node[yshift=4.4cm, xshift=0cm] at (current page.south)
{
    \includegraphics[width=1.05\textwidth]{topics_top10palabras.jpeg}
};
\end{tikzpicture}

---

\begin{tikzpicture}[remember picture, overlay]
\node[yshift=5cm, xshift=0cm] at (current page.south)
{
    \includegraphics[width=0.9\textwidth]{heat_topics.png}
};
\end{tikzpicture}



## ¿De qué sirve esta perspectiva generadora de documentos?

* Existen técnicas estadísticas y computacionales para invertir este procedimiento a partir de documentos existentes (...nuestros documentos), pudiendo así inferir la composición *más probable* de los tópicos que permitieron generar esta colección de documentos.

* Los tópicos estimados tienen un significado identificado por el/la analista


## Evaluación de modelos LDA
 
- Evaluar la calidad de los tópicos descubiertos no es trivial
    - **No existe** una "respuesta correcta" contra la cual comparar.
 
\vspace{0.3cm}

Existen dos enfoques complementarios:
 
- **Perplexity**: métrica estadística que mide qué tan bien el modelo predice datos no vistos (ajuste probabilístico).
    - Blei, Ng & Jordan (2003) 
- **Coherence**: métrica semántica que mide si las palabras de un tópico tienen sentido conjunto para un humano.
    - Newman et al. (2010) y Röder et al. (2015) posteriormente mostraron que perplexity no siempre se correlaciona con interpretabilidad humana.
 
---
 
### Perplexity
 
Mide la capacidad del modelo de predecir un conjunto de documentos no usados en el entrenamiento (*held-out*). Se basa en la *log-verosimilitud* del modelo.
 
**(Blei, Ng & Jordan, 2003):**
 
$$
\text{Perplexity}(D_{test}) = \exp\left(-\frac{\sum_{d=1}^{M} \log p(w_d)}{\sum_{d=1}^{M} N_d}\right)
$$
 
donde:

- $D_{test}$ = conjunto de documentos de prueba (*held-out*), de tamaño $M$
- $M$ = número total de documentos en $D_{test}$
- $w_d$ = vector de palabras (todos los tokens) del documento $d$
- $N_d$ = número de palabras (tokens) en el documento $d$
- $p(w_d)$ = probabilidad del documento $d$, marginalizando sobre tópicos: $p(w_d) = \prod_{i=1}^{N_d} \sum_{k=1}^{K} p(w_{d,i} \mid z_{d,i}=k) \, p(z_{d,i}=k \mid d)$


---

**Acerca de la notación**: $M$ aparece en ambas sumatorias (numerador y denominador) 

— El numerador es la log-verosimilitud total del corpus de prueba; el denominador es el número total de tokens en ese mismo corpus.
 
**Interpretación:**

- Rango: $(0, \infty)$
- **Menor perplexity = mejor modelo** (el modelo está menos "sorprendido" por datos nuevos)
- Perplexity decreciente indica mejor ajuste estadístico del modelo a los datos
    - No garantiza tópicos interpretables
 
---
 
### Coherence 
 
Mide si las palabras top de un tópico co-ocurren de manera consistente en los documentos, capturando la interpretabilidad semántica.
 
**UMass Coherence, Mimno et al. 2011:**
 
$$
C_{UMass}(t) = \sum_{i=2}^{N} \sum_{j=1}^{i-1} \log \frac{D(w_i, w_j) + 1}{D(w_j)}
$$
 
donde:

- $w_1, ..., w_N$ = las $N$ palabras más probables del tópico $t$ (ordenadas por relevancia)
- $D(w_j)$ = número de documentos donde aparece la palabra $w_j$
- $D(w_i, w_j)$ = número de documentos donde co-ocurren $w_i$ y $w_j$
- El $+1$ es un suavizado (Laplace) para evitar $\log(0)$

---

**Variante más usada en la práctica — Coherence $C_v$ (Röder et al., 2015):**

- Combina similitud coseno de vectores *Normalized Pointwise Mutual Information* con una ventana deslizante de co-ocurrencia
- Muestra mejor correlación con juicio humano que UMass.
 
**Interpretación:**

- **Mayor coherence = tópicos más interpretables** (palabras que tienden a aparecer juntas)
- Valores de $C_v$ suelen ubicarse entre 0.3 y 0.7 en corpus reales
- Valores >0.5 son considerados aceptables

---

Los rangos varían según la métrica:
 
| Métrica | Rango | Interpretación |
|---------|-------|----------------|
| **$C_v$ (histórica)** | $[0, 1]$ | Mayor = mejor; típicamente 0.4–0.7; **NO recomendada** |
| **$C_{UMass}$** | $(-\infty, 0]$ | Mayor (menos negativo) = mejor; $-2$ a $-10$ típico |
| **$C_{UCI}$ (PMI)** | $(-\infty, +\infty)$ | Mayor = mejor; típicamente $-1$ a $+2$ |
| **$C_{NPMI}$ (normalizado)** | $[-1, +1]$ | Mayor = mejor; $0.0$ a $0.2$ común en LDA |
 


---
 
### Validación y selección de modelos
 
**Flujo de trabajo recomendado:**
 
1. **Entrenar múltiples modelos LDA** variando el número de tópicos $k$
2. **Calcular perplexity** sobre un conjunto *held-out* para cada $k$, se grafica curva y busca el "codo" donde deja de mejorar sustancialmente
3. **Calcular coherence** ($C_v$ o UMass) para cada $k$, buscar el máximo o un punto estable alto
4. **Triangular ambas métricas**: rara vez coinciden exactamente en el mismo $k$, priorizae *coherence* para interpretabilidad
5. **Validación humana final**: inspeccionar manualmente las top-X palabras de los tópicos del modelo  candidato antes de decidir

---


### Advertencia respecto a la cantidad de tópicos

- Más tópicos $=$ mejor ajuste estadístico **pero** tópicos redundantes o fragmentados

- *Chang et al. (2009)* demostraron que perplexity puede mejorar mientras la interpretabilidad humana empeora
    - Coherence se considera el estándar en la práctica

---

**Ejemplo en R (paquete `topicmodels` + `ldatuning`):**
 
```r
library(ldatuning)
 
# CaoJuan2009 y Griffiths2004 son métricas similares a Coherence
resultado <- FindTopicsNumber(
  dtm,
  topics = seq(2, 15, by = 1),
  metrics = c("Griffiths2004", "CaoJuan2009", "Deveaud2014"),
  method = "Gibbs",
  control = list(seed = 42, iter = 500),
  mc.cores = 2L
)

FindTopicsNumber_plot(resultado)
```

 
## Referencias
 
- **Blei, D. M., Ng, A. Y., & Jordan, M. I. (2003).** "Latent Dirichlet Allocation." *Journal of Machine Learning Research*, 3, 993–1022.
- **Chang, J., Gerrish, S., Wang, C., Boyd-Graber, J., & Blei, D. (2009).** "Reading tea leaves: How humans interpret topic models." *Advances in Neural Information Processing Systems*, 22.
- **Mimno, D., Wallach, H., Talley, E., Leenders, M., & McCallum, A. (2011).** "Optimizing semantic coherence in topic models." *Proceedings of EMNLP*, 262–272.
- **Röder, M., Both, A., & Hinneburg, A. (2015).** "Exploring the space of topic coherence measures." *Proceedings of WSDM*, 399–408.
- **Newman, D., Lau, J. H., Grieser, K., & Baldwin, T. (2010).** "Automatic evaluation of topic coherence." *Proceedings of NAACL*, 100–108.


