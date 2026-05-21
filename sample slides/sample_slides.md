---
title: EST-XXX
subtitle: NOMBRE DEL CURSO
author: Juan Zamora O.
date: FECHA.
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
classoption: t 
---

# Aproximaciones Low-Rank para Clustering

Una matriz $X$ de rango $r$ admite una factorización de la forma

$$X=BC^T, \ B\in\mathbf{R}^{m\times r}, \ C\in\mathbf{R}^{n\times r}$$


$X$ es aproximada con bajo rango (low-rank) cuando $rango(X) << \min(m,n)$

\begin{tikzpicture}[remember picture, overlay]
\node[yshift=2.7cm, xshift=0cm] at (current page.south) 
{
    \includegraphics[width=0.4\textwidth]{tm_model.png}
};
\end{tikzpicture}    


# Ejemplo numérico: datos iniciales

$$
V = \begin{bmatrix}
5 & 3 \\
3 & 2 \\
4 & 1
\end{bmatrix}
$$


# Ejemplo con 2 columnas de igual ancho

::: columns

:::: column

Left column text.

Another text line.

::::

:::: column

- Item 1.
- Item 2.
- Item 3.

::::

:::


# Pseudocódigo {.fragile}

\begin{lstlisting}[frame=single,framerule=0pt]
for i:=maxint to 0 do
begin
    j:=square(root(i));
end;
\end{lstlisting}

# Codigo en R {.fragile}

\begin{lstlisting}[language=R]
library(topicmodels)

# Entrenamiento del modelo
lda_model <- LDA(dtm_train, k = 2, control = list(seed = 1234))

# Cálculo de perplejidad en datos de prueba
log_likelihood <- mean(sapply(seq_len(nrow(dtm_test)), function(i) {
  logLikelihood(lda_model, dtm_test[i, ]) # Puede requerir función auxiliar
}))

num_words <- sum(colSums(dtm_test))
perplexity <- exp(-log_likelihood / num_words)

cat("Perplexity:", perplexity, "\n")
\end{lstlisting}


# Codigo en Python {.fragile}

\begin{lstlisting}[language=Python]

for i in range(2, num):
    if (num % i) == 0:
        # if factor is found, set flag to True
        flag = True
        # break out of loop
        break
\end{lstlisting}


# {.fragile}

### Codigo en Python

\begin{lstlisting}[language=Python]

for i in range(2, num):
    if (num % i) == 0:
        # if factor is found, set flag to True
        flag = True
        # break out of loop
        break
\end{lstlisting}
