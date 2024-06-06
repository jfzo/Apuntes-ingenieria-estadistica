---
title: EST-297
subtitle: Métodos de Clustering basados en Densidad
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


# Revisitando técnicas basadas en representantes

**Supuesto** bastante usado

- Grupos/Clusters generados a partir de una distribución o mezcla de distribuciones simétricas (e.g. Normal)
- Expectation Maximization, K-Means y extensiones por mencionar algunos


Enfoque basado en densidad no supone forma específica.

- Útil por ejemplo en datos geo-espaciales.

---

\begin{tikzpicture}[remember picture, overlay]
\node[yshift=0cm, xshift=-4cm] at (current page.center) 
{
    \includegraphics[width=0.4\textwidth]{kmeans_fails_rolls.png}
};
\end{tikzpicture}


\begin{tikzpicture}[remember picture, overlay]
\node[yshift=0cm, xshift=4cm] at (current page.center) 
{
    \includegraphics[width=0.4\textwidth]{kmeans_voronoi.jpeg}
};
\end{tikzpicture}

--- 

- Minimización de la distancia al cuadrado entre los puntos y sus respectivos centroides produce a un particionamiento tipo polígono de Voronoi.
 Esto no solo ocurren en 2D
- **Urge** contar con mecanismos de descubrimiento de grupos 
    - con forma arbitraria.
    - identificando ruido
    - que no requieran de $k$
    
    
## Clustering basado en densidad    

- *Grupos basados en densidad* se definen como areas densas y conectadas, *separadas* entre sí por áreas de  menor densidad.
- El ruído se define como áreas con densidad menor que la de los clusters
- Noción de *Localidad* asociada a la definición de cluster
    - Posibilita encontrar regiones densas con forma arbitraria
    
\begin{tikzpicture}[remember picture, overlay]
\node[yshift=2.0cm, xshift=5cm] at (current page.south) 
{
    \includegraphics[width=0.25\textwidth]{density_clusters_example.png}
};
\end{tikzpicture}    

---

- Puede ser considerado como un método no paramétrico
    - No hace supuestos respecto del número de grupos o su distribución

**Un algoritmo de clustering basado en densidad debe responder algunas preguntas:**

- ¿Como se estima la densidad?
- ¿Como se define la conectividad?


# DBSCAN Clustering

- Diseñado para descubrir clusters y ruído en los datos. 
- Agrupa las observaciones mediante basándose en un umbral para el radio de búsqueda de vecinos y el número minimo de vecinos requeridos para identificar puntos clave.
    - Puntos clave $\sim$ *core-points*
- Cada cluster debe tener al menos un *core-point*
- *core-points* son aquellos con vecindarios ($\epsilon$-vec.) densos
- Un *core-point* es aquel cuyo vecindario contiene *al menos* *MinPts* puntos
    - Es decir, punto cuya densidad excede un determinado umbral.
- Ruído: Aquellos puntos que no pertenecen a ningún cluster

---

- Cuenta la cantidad de puntos en vecindarios de radio fijo ($\epsilon$) $$N_{\epsilon}(p)=\{q\in \mathbf{D} | dist(p,q)\leq \epsilon\}$$
- Considera dos puntos conectados cuando son vecinos recíprocos    
- Un punto $q$ es alcanzable de manera directa (*directly-density-reachable*) por un *core-point* $p$ si se encuentra en su vecindario, $$|N_{\epsilon}(p)|\geq MinPts \ y \ q\in N_{\epsilon}(p)$$


---

- Alcance (*density-reachable*($\mathsf{R}$)) queda dado por la clausura transitiva de la relación *directly-density-reachable*($\mathsf{DR}$) $$q\mathsf{R}p\exists p_1,\ldots,p_m\ \mbox{con}\ p_1=p\ y \ p_m=q \ \ t.q.\ \  p_{i+1}\mathsf{DR}p_i$$
- Dos puntos $p$ y $q$ están conectados por densidad (*density-connected*) si existe otro $r$ a partir del cual ambos son *density-reachable*
- Un **cluster** es entonces un conjunto de puntos conectados por densidad (*density-connected*($\mathsf{C}$))
    - maximal respecto de *density-reachability* $$q\mathsf{C}p, \exists r\ \  t.q.\ \ r\mathsf{R}p\ \land r\mathsf{R}q$$
- Ruido se define como aquel conjunto de puntos que no pertenecen a ningún cluster 

\begin{tikzpicture}[remember picture, overlay]
\node[yshift=3.5cm, xshift=6cm] at (current page.south) 
{
    \includegraphics[width=0.3\textwidth]{transitive_closure_relation.png}
};
\end{tikzpicture}    

## Parámetros del método

- Número mínimo de puntos ($MinPts$): Menor número requerido para formar un cluster
    - Fijado a un valor mayor que el número de dimensiones de los datos
- $\epsilon$ ($eps$): Distancia máxima a la que pueden estar dos puntos para seguir formando parte del mismo cluster.
    - Estimado mediante un gráfico de distancia a los $k$-vecinos
        - Se calcula la distancia de cada punto a su $k$-ésimo vecino más cercano
        - Se ordenan estos valores (menor a mayor) y grafican 
    - Buscar la "rodilla" en la curva (valor sobre el que las distancias empiezan a desviarse hacia los valores atípicos)

---

\begin{tikzpicture}[remember picture, overlay]
\node[yshift=0cm, xshift=0cm] at (current page.center) 
{
    \includegraphics[width=0.5\textwidth]{knn_dist_plot.png}
};
\end{tikzpicture}    


## Conclusiones

- Complejidad O(nlog n)
- Incorpora ídentificación de ruído
- Densidad puede variar entre clusters ... problema!
- Problemas en alta dimensionalidad
- Algunas extensiones son OPTICS y HDBSCAN


# OPTICS Clustering

- Dificil caracterizar estructura intrinseca de grupos mediante parámetros globales de densidad
- Pueden existir grupos de diversa densidad en distintas regiones del espacio
- *Idea base*: Grupos de mayor densidad están contenidos en grupos con menor densidad
- Se construyen *simultaneamente* grupos con diferentes densidades para un valor fijo de *MinPts*

## Conceptos relevantes

OPTICS introduce dos conceptos:

1. *Core-distance*: Valor $\epsilon$ más pequeño para un punto $p$ que lo convierte en *core-point*.
2. *reachability-distance*: Distancia más pequeña entre un par de puntos $p$ y $q$ que los hace directamente alcanzables

Además usa un gráfico (*reachability  plot*) que muestra la densidad y conectividad de los puntos. **Útil** para distinguir clusters

\begin{tikzpicture}[remember picture, overlay]
\node[yshift=1.5cm, xshift=4cm] at (current page.south) 
{
    \includegraphics[width=0.4\textwidth]{reachability_plot.jpeg}
};
\end{tikzpicture}   


# HDBSCAN Clustering

- Objetivo: Convertir DBSCAN en un método jerárquico
- Explora todas las posibles escalas de densidad
- Puede ser visto como DBSCAN clustering a lo largo de todos los valores de $\epsilon$
    - Equivale a encontrar los componentes conectados del grafo de "mutual reachability" para todos los valores de $\epsilon$
- Parametros: min_cluster_size, min_samples
