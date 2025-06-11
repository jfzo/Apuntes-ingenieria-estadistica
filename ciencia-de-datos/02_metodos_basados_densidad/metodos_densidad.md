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


# OPTICS: Ordering Points To Identify the Clustering Structure

- Dificil caracterizar estructura intrinseca de grupos mediante parámetros globales de densidad
- Pueden existir grupos de diversa densidad en distintas regiones del espacio
- *Idea base*: Grupos de mayor densidad están contenidos en grupos con menor densidad
- Se construyen *simultaneamente* grupos con diferentes densidades para un valor fijo de *MinPts*

## Conceptos y ventajas


* **Concepto:** OPTICS es una generalización de **DBSCAN** que aborda la dificultad de elegir el parámetro $\epsilon$ (radio). Genera un orden de los puntos basado en su **densidad** y su **distancia de alcanzabilidad** (reachability distance).
* **Salida:** Produce un "**diagrama de alcanzabilidad**" (reachability plot) que visualiza la estructura jerárquica de clústeres. Los valles en el diagrama corresponden a clústeres.
* **Ventajas:**
    * No requiere un valor global de $\epsilon$.
    * Puede descubrir clústeres de **diferentes densidades**.
    * Identifica **ruido** de manera efectiva.

---

Además usa un gráfico (*reachability  plot*) que muestra la densidad y conectividad de los puntos. **Útil** para distinguir clusters

\begin{tikzpicture}[remember picture, overlay]
\node[yshift=1.9cm, xshift=3cm] at (current page.south) 
{
    \includegraphics[width=0.6\textwidth]{reachability_plot.jpeg}
};
\end{tikzpicture}   



---

### Parámetros y Ajuste

* **`min_samples` (Mínimo de muestras):**
    * **Definición:** El número mínimo de puntos requeridos para formar un núcleo denso.
    * **Ajuste:** Un valor más alto requiere clústeres más densos. Típicamente se elige entre 2 y el doble de la dimensionalidad de los datos. Se puede empezar con un valor bajo (ej. 5) y aumentarlo.
* **`max_eps` (Máximo épsilon):**
    * **Definición:** El radio máximo para considerar vecinos. Limita la distancia máxima para buscar vecinos. No es el $\epsilon$ global de DBSCAN.
    * **Ajuste:** Un valor demasiado pequeño puede resultar en clústeres no detectados. Un valor demasiado grande puede hacer que el cálculo sea lento y unir clústeres distintos. A menudo se establece en `inf` (infinito) para permitir a OPTICS explorar todas las posibles densidades, o un valor grande basado en la escala de tus datos.
* **`metric` (Métrica de distancia):**
    * **Definición:** La función de distancia utilizada (ej., euclidiana, manhattan, etc.).
    * **Ajuste:** Depende de la naturaleza de tus datos. La euclidiana es común para datos numéricos.


# HDBSCAN Clustering


## HDBSCAN: Hierarchical Density-Based Spatial Clustering of Applications with Noise

### Concepto y Ventajas

* **Concepto:** Basado en DBSCAN, pero construye una **jerarquía de clústeres** a partir de un árbol de conectividad mínima (MST) de los datos, usando la "distancia de conectividad mutua inversa".
* **Aislamiento de clústeres:** Identifica la **estabilidad de los clústeres** a través de diferentes umbrales de densidad, seleccionando los clústeres más "estables".
* **Ventajas:**
    * **No requiere el parámetro $\epsilon$**.
    * Puede encontrar clústeres de diferentes densidades.
    * Maneja el **ruido** de manera robusta.
    * Generalmente más eficiente que OPTICS para extraer clústeres.


---

### Parámetros y Ajuste

* **`min_cluster_size` (Tamaño mínimo del clúster):**
    * **Definición:** El número mínimo de puntos para que se considere un clúster válido.
    * **Ajuste:** Un valor más pequeño detectará clústeres más pequeños y posiblemente más ruidosos. Un valor más grande solo identificará clústeres substanciales. Depende del dominio del problema; empezar con 2-10 es razonable.
* **`min_samples` (Mínimo de muestras / `min_points`):**
    * **Definición:** El número mínimo de puntos para considerar un punto como un "núcleo" de un clúster. También influye en el suavizado del árbol de conectividad.
    * **Ajuste:** Similar a `min_samples` en OPTICS. Un valor más alto hace que los clústeres sean más "densos" y ruidosos. A menudo se elige igual o ligeramente menor que `min_cluster_size`.

---

* **`cluster_selection_epsilon`:**
    * **Definición:** Un umbral de distancia que permite que puntos adyacentes se unan a clústeres existentes, incluso si no son parte de un núcleo denso. Rara vez se usa y no se recomienda modificarlo al principio.
    * **Ajuste:** Generalmente se deja en su valor por defecto (0.0). Solo se ajusta en casos muy específicos donde se necesita una relajación en la definición de densidad.
* **`metric` (Métrica de distancia):**
    * **Definición:** La función de distancia utilizada.
    * **Ajuste:** Similar a OPTICS. La euclidiana es la más común.

---

\begin{tikzpicture}[remember picture, overlay]
\node[yshift=0.5cm, xshift=0cm] at (current page.center) 
{
    \includegraphics[width=0.6\textwidth]{hdbscan_data.png}
};
\end{tikzpicture}   

---


\begin{tikzpicture}[remember picture, overlay]
\node[yshift=1.5cm, xshift=-4cm] at (current page.center) 
{
    \includegraphics[width=0.4\textwidth]{hdbscan_data_cd1.png}
};
\end{tikzpicture}   

\begin{tikzpicture}[remember picture, overlay]
\node[yshift=1.5cm, xshift=4cm] at (current page.center) 
{
    \includegraphics[width=0.4\textwidth]{hdbscan_data_cd2.png}
};
\end{tikzpicture}   


\begin{tikzpicture}[remember picture, overlay]
\node[yshift=-2.5cm, xshift=-4cm] at (current page.center) 
{
    \includegraphics[width=0.4\textwidth]{hdbscan_data_cd3.png}
};
\end{tikzpicture}   

\begin{tikzpicture}[remember picture, overlay]
\node[yshift=-2.5cm, xshift=4cm] at (current page.center) 
{
    \includegraphics[width=0.4\textwidth]{hdbscan_data_cd4.png}
};
\end{tikzpicture}   


---


\begin{tikzpicture}[remember picture, overlay]
\node[yshift=-0.01cm, xshift=0cm] at (current page.center) 
{
    \includegraphics[width=0.7\textwidth]{hdbscan_dendrogram.png}
};
\end{tikzpicture}   






## Comparación: OPTICS vs. HDBSCAN


\begin{tikzpicture}[remember picture, overlay]
\node[yshift=0cm, xshift=0cm] at (current page.center) 
{
    \includegraphics[width=0.6\textwidth]{hbscan_optics.png}
};
\end{tikzpicture}

---

### Consideraciones Finales

* **Ajuste de Parámetros Global:** Ambos métodos se benefician de un buen conocimiento del dominio de los datos. La validación interna (ej. coeficientes de silueta adaptados a ruido) o el análisis visual pueden guiar el ajuste.
* **Recomendación:** Si bien OPTICS proporciona una visión más granular, HDBSCAN es a menudo el preferido para la mayoría de las aplicaciones debido a su capacidad para extraer clústeres de forma automática y robusta sin la necesidad de definir un $\epsilon$ global.



# Identificación de tendencias

- Un método de clustering intentará encontrar grupos **aún cuando no existan**

¿Existe o no una tendencia de agrupamiento en los datos?

- Una manera que no realiza muchos supuestos es la es la evaluación visual de tendencia (**VAT** e **improved VAT**)
  


## Método VAT

Este método consiste en:

    1. Calcular la matriz de distancia entre los objetos del conjunto de datos
    2. Re-ordenar las filas/columnas de la matriz de manera que los objetos similares queden próximos. Este proceso genera una matriz de distancias ordenada (MDO).
    3. Mostrar la MDO.

VAT permite detectar tendencia de manera visual contando los bloques cuadrados a lo largo de la diagonal

---

\begin{tikzpicture}[remember picture, overlay]
\node[yshift=0cm, xshift=-3cm] at (current page.center) 
{
    \includegraphics[width=0.5\textwidth]{multishapes_data.png}
};
\end{tikzpicture}  

\begin{tikzpicture}[remember picture, overlay]
\node[yshift=0cm, xshift=4cm] at (current page.center) 
{
    \includegraphics[width=0.45\textwidth]{vat_dist_multishapes.png}
};
\end{tikzpicture}  

--- 

### VAT e iVAT

```
- Bezdek, J. C., & Hathaway, R. J. (2002, May). VAT: A tool for visual assessment of (cluster) tendency. In Proceedings of the 2002 International Joint Conference on Neural Networks. IJCNN'02 (Cat. No. 02CH37290) (Vol. 3, pp. 2225-2230). IEEE.
- Wang, L., Nguyen, U. T., Bezdek, J. C., Leckie, C. A., & Ramamohanarao, K. (2010, June). iVAT and aVAT: enhanced visual analysis for cluster tendency assessment. In Pacific-Asia Conference on Knowledge Discovery and Data Mining (pp. 16-27). Berlin, Heidelberg: Springer Berlin Heidelberg.
```

# Validación de resultados de Clustering

- El objetivo es poder medir la calidad de solución entregada por un método
- Estas medidas se categorizan en 3 grupos:
  1. Medidas internas: No usa referencia externa, solo propiedades intrinsecas de la solución
  2. Medidas externas: Compara solución con un patrón externo, por ejemplo etiquetas de clase. Permite medir en qué medida el agrupamiento coincide con lo esperado.


## Medidas internas

- A menudo reflejan cohesión/compactitud, conectividad y separación entre particiones
- **Cohesión**: Que tan cercanos están los objetos dentro de cada grupo.
  - Los distintos indices se basan en medidas de distancia
  - **Variación intra cluster** es un ejemplo de indicador de cohesión
- **Separación**: Que tan bien separado se encuentra un cluster de los otros.
  - Distancias entre centroides o representantes de cada grupo
  - Distancias mínimas entre pares de objetos en ambos clusters   
- **Conectividad**: Grado de conectividad de los clusters basado en k-vecinos más cercanos. 
  - Principio: Items en el vecindario debieran compartir el mismo cluster.

\begin{tikzpicture}[remember picture, overlay]
\node[yshift=1.5cm, xshift=0cm] at (current page.south) 
{
    \includegraphics[width=0.55\textwidth]{tres_criterios_clustering.png}
};
\end{tikzpicture}  

---

### Coeficiente de Silhouette

- Compara las distancias internas entre los objetos en un cluster con las distancias al cluster más cercano
- Para el objeto $i$, la distancia promedio mas corta a objetos del cluster más cercano $b_i$

$$S_i=\frac{b_i-a_i}{\max(a_i,b_i)}$$

- Valores de $S_i$ cercanos a $1$ indican una asignación correcta. Valores cercanos a $0$ indica que la observación se encuentra entre 2 grupos. Valores negativos indican una asignación incorrecta.

---

### Indice Dunn

- Contrasta la separación entre los grupos con la dispersión interna de cada uno.
- Calcula 
    - Distancia más pequeña entre objetos de clusters distintos ($\alpha$)
    - Distancia mayor entre objetos del mismo cluster ($\beta$)

$$D=\frac{\alpha}{\beta}$$

- A mayor valor, mayor separación entre los grupos relativa a sus diametros

## Medidas externas

- En general operan sobre la matriz de contingencia entre clusters y clases indicadas en el conjunto de datos
- Purity (P): Cada cluster se etiqueta según la clase más frecuente. Se suma la cantidad de objetos correctamente etiquetados y se divide por el total de objetos.
    - Ojo: Aumenta a medida que aumenta la cantidad de clusters
    $$P=\frac{1}{n}\sum_{k}\max_{j}|W_k\cap C_j|$$
- Rand Index (RI): Considera los pares de objetos que son asignados dentro del mismo o en distinto cluster.
    - $Vp$: Objetos similares que son asignados al mismo cluster
    - $Vn$: Objetos disimiles asignados en clusters distintos
    - $Fp$: Objetos disimiles asignados  al mismo cluster
    - $Fn$: Objetos similares que son asignados en clusters distintos
    $$RI=\frac{Vp+Vn}{Vp+Vn+Fp+Fn}$$