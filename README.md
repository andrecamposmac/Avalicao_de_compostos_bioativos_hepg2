# Descoberta de Fármacos com Machine Learning - Bioatividade HepG2

Este projeto visa desenvolver um modelo de Machine Learning capaz de prever a bioatividade de compostos químicos frente à linhagem celular **HepG2** (células de carcinoma hepatocelular humano). O objetivo é identificar potenciais candidatos a fármacos citotóxicos através da análise de suas estruturas moleculares.

O projeto está estruturado em uma série de notebooks Jupyter que cobrem desde a coleta de dados até o ajuste fino do modelo final.

## 📋 Estrutura do Projeto

O fluxo de trabalho foi dividido em 6 etapas principais:

1.  **Obtenção de Dados (`01_obtencao_de_dados.ipynb`):**
    *   Coleta de dados da base **ChEMBL** (biblioteca de moléculas bioativas).
    *   Filtragem por alvo biológico: Linhagem celular HepG2.
    *   Resultado: Obtenção de 25.862 compostos com atividade registrada.

2.  **Manipulação de Dados (`02_manipulacao_de_dados.ipynb`):**
    *   Limpeza inicial do dataset (remoção de valores nulos, duplicatas, etc.).
    *   Classificação dos compostos em:
        *   **Ativos:** IC50 <= 1000 nM
        *   **Inativos:** IC50 >= 10000 nM
        *   **Intermediários:** 1000 nM < IC50 < 10000 nM
    *   Conversão da métrica IC50 para **pIC50** (escala logarítmica negativa) para facilitar a modelagem.

3.  **Análise Exploratória de Dados (`03_analise_de_dados_exploratoria.ipynb`):**
    *   Análise das propriedades físico-químicas baseadas na **Regra de Lipinski** (Peso Molecular, LogP, Doadores/Aceitadores de Hidrogênio).
    *   Testes estatísticos (Mann-Whitney) para verificar diferenças significativas entre compostos ativos e inativos.
    *   Visualização da distribuição química do espaço amostral.

4.  **Preparação de Dados para ML (`04_preparacao_de_dados_ML.ipynb`):**
    *   Cálculo de descritores moleculares (fingerprints) usando a biblioteca **PaDEL-Descriptor**.
    *   Geração de vetores numéricos (ex: PubChem Fingerprints) que representam a estrutura química das moléculas, tornando-as legíveis para os algoritmos.

5.  **Comparação de Modelos (`05_ml_comparacao.ipynb`):**
    *   Uso da biblioteca **LazyPredict** para testar dezenas de algoritmos de regressão simultaneamente.
    *   Avaliação de métricas como R-Squared e RMSE.
    *   **Resultado:** O modelo **RandomForestRegressor** destacou-se com um R-Squared de aproximadamente 0.62 no conjunto de teste.

6.  **Fine Tuning (`06_ml_fine_tuning.ipynb`):**
    *   Otimização dos hiperparâmetros do RandomForest (n_estimators, max_depth) via **GridSearchCV**.
    *   Seleção de features baseada em variância (VarianceThreshold) para reduzir a dimensionalidade.
    *   O modelo final alcançou um R-Squared próximo de 0.60 após a validação cruzada, confirmando sua capacidade preditiva.

## 🛠 Tecnologias Utilizadas

*   **Python 3**
*   **Bioinformática:** `chembl_webresource_client`, `padelpy`.
*   **Data Science:** `pandas`, `numpy`, `scikit-learn`, `scipy`.
*   **Machine Learning:** `lazypredict`, `xgboost`, `lightgbm`.
*   **Visualização:** `matplotlib`, `seaborn`.

## 🚀 Como Executar

Para reproduzir este estudo:
1.  Clone o repositório e instale as dependências (recomenda-se criar um ambiente virtual).
2.  Execute os notebooks na ordem numérica (01 a 06).
    *   *Nota:* A etapa 04 requer o software PaDEL instalado ou configurado corretamente via biblioteca python.
3.  Os arquivos CSV intermediários (datasets processados) serão gerados a cada etapa para uso na seguinte.

## 📊 Resultados Chave

*   O projeto demonstrou que descritores químicos simplificados (fingerprints) conseguem capturar padrões estruturais correlacionados com a citotoxicidade em células HepG2.
*   Modelos baseados em árvores (Random Forest, XGBoost) superaram modelos lineares tradicionais para este tipo de dado farmacológico.

---
**Autor:** André Campos Machado
