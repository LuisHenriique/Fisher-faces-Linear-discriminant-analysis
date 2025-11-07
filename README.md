# Projeto Final - Álgebra Linear: Reconhecimento de Imagens com LDA (Fisherfaces)

## Descrição

Este projeto é um trabalho final para a disciplina de Álgebra Linear que implementa o algoritmo de **Análise Discriminante Linear (LDA)**, também conhecido como método Fisherfaces, para reconhecimento facial.

O objetivo é demonstrar "manualmente" (usando NumPy) como reduzir a dimensionalidade de um conjunto de dados de imagens (o Olivetti Faces Dataset) de 4096 dimensões (pixels) para apenas 39, mantendo a informação que *maximiza a separabilidade* entre as diferentes classes (pessoas).

## O que este projeto faz?

O notebook `main.ipynb` executa os seguintes passos:

1.  **Carregamento e Preparação:**
    * Carrega o dataset Olivetti Faces (400 imagens, 40 pessoas).
    * Divide os dados em conjuntos de treino (300 imagens) e teste (100 imagens).

2.  **Cálculo das Matrizes de Dispersão (Manual):**
    * Calcula a **matriz de dispersão interna** (within-class), $S_W$, que mede a variância *dentro* de cada classe.
    * Calcula a **matriz de dispersão entre classes** (between-class), $S_B$, que mede a variância *entre* as diferentes classes.

3.  **Problema do Autovalor:**
    * Resolve o problema de autovalor generalizado ($S_W^{-1} S_B$) para encontrar os autovetores (os "discriminantes lineares") que melhor separam as classes.

4.  **Redução de Dimensionalidade:**
    * Seleciona os $k=39$ melhores autovetores para criar a matriz de projeção $W$ (de 4096x39).
    * Projeta os dados de treino e teste do espaço original de 4096 dimensões para o novo espaço de 39 dimensões.

5.  **Validação:**
    * Treina um classificador K-Nearest Neighbors (KNN) usando os dados de treino reduzidos (`x_train_lda`).
    * Testa o classificador nos dados de teste reduzidos (`x_test_lda`) para avaliar a eficácia da redução.

6.  **Visualização:**
    * Plota os dois primeiros componentes LDA (LDA1 vs. LDA2) para inspecionar visualmente a separação das classes.

## Resultados

A redução de dimensionalidade foi altamente eficaz:

* **Acurácia do Classificador:** O modelo KNN, treinado apenas nas 39 features criadas pelo LDA, alcançou **99.00%** de acurácia no conjunto de teste.
* **Visualização:** Os gráficos de dispersão mostram uma nítida separação entre os grupos (pessoas) no espaço LDA, confirmando que o algoritmo cumpriu seu objetivo de maximizar a separabilidade.
