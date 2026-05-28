# Preparação dos dados

### K-Means
Antes da aplicação do algoritmo K-Means, foi necessário realizar etapas de preparação e transformação dos dados, garantindo maior qualidade na formação dos clusters e evitando distorções nos cálculos de distância

- **Seleção de Features**: Definimos o conjunto de features que melhor representam os perfis dos candidatos:
  ```python
  features_cluster = df_dataset_tratado[['NOTA_L', 'NOTA_CH', 'NOTA_CN', 'NOTA_M', 'NOTA_R',
                                         'PESO_L', 'PESO_CH', 'PESO_CN', 'PESO_M', 'PESO_R',
                                         'GRAU_T', 'TIPO_MOD_CONCORRENCIA_T']].copy()
  ```
  Evitamos deliberadamente variáveis puramente identificadoras (como códigos de curso ou candidato) que não possuem significado ordinal, pois elas poderiam introduzir distorções na distância euclidiana

- **Transformação de Variáveis Categóricas**: O K-Means interpreta distância numérica, o que criaria viés artificial. Por isso, aplicamos one-hot encoding completo nas variáveis categóricas. Essa transformação expandiu as colunas categóricas em variáveis binárias (dummies), garantindo que cada categoria fosse tratada de forma equidistante e sem ordenação implícita.
  ```python
  features_cluster = pd.get_dummies(features_cluster, drop_first=False)
  ```
- **Normalização dos Dados**: Como o K-Means é um algoritmo baseado em distâncias (euclidiana), variáveis em escalas diferentes distorceriam os resultados (notas variam na casa das centenas; pesos geralmente entre 1 e 3). Aplicamos `StandardScaler` para centralizar todas as features com média 0 e desvio padrão 1:
  ```python
  from sklearn.preprocessing import StandardScaler
  
  scaler = StandardScaler()
  X_scaled = scaler.fit_transform(features_cluster)
  
  print("=== NORMALIZAÇÃO ===")
  print("Shape de X_scaled:", X_scaled.shape)
  
  print("\nMédia aproximada após scaling:")
  print(round(X_scaled.mean(), 4))
  
  print("\nDesvio padrão aproximado após scaling:")
  print(round(X_scaled.std(), 4))
  ```
  A aplicação do `StandardScaler` apresentou os resultados esperados para a padronização. A matriz `X_scaled` manteve a estrutura original do dataset com 183.541 registros e 12 variáveis, enquanto a média de 0.0 e o desvio padrão de 1.0 confirmam que todas as features passarão a contribuir de forma equilibrada no cálculo das distâncias.
  ```python
  === NORMALIZAÇÃO ===
  Shape de X_scaled: (183541, 12)
  
  Média aproximada após scaling:
  0.0
  
  Desvio padrão aproximado após scaling:
  1.0
  ```

- **Definição do Número de Clusters**: O algoritmo K-Means requer a definição prévia do número de clusters (`n_clusters`). Foram testados valores de K variando de 2 a 6, utilizando o Método do Cotovelo (inércia) e o Silhouette Score
    - **Método do Cotovelo** (Elbow Method): baseado na inércia (soma das distâncias quadradas intra-cluster). Buscamos o ponto de inflexão onde o ganho de redução de inércia se torna marginal.
    - **Silhouette Score:** métrica que avalia simultaneamente a coesão interna dos clusters e a separação entre eles. Quanto mais próximo de 1, melhor a qualidade do agrupamento.

   ```python
    === TESTE DE DIFERENTES VALORES DE K ===
    k=2 | Inércia=1681526.46 | Silhouette=0.3414
    k=3 | Inércia=1371787.98 | Silhouette=0.2184
    k=4 | Inércia=1246144.86 | Silhouette=0.2281
    k=5 | Inércia=1132939.60 | Silhouette=0.2423
    k=6 | Inércia=1042607.96 | Silhouette=0.2525
  ```
  
  - **Justificativa da Escolha do K=2:** A escolha por formar 2 agrupamentos (K=2) deu-se porque este foi o melhor resultado matemático alcançável com este modelo para a estrutura dos nossos dados. O valor obteve o maior Silhouette Score (aproximadamente 0,3414), já os demais, a inércia diminui progressivamente conforme o número de clusters aumentava. Dessa forma, o valor K = 2 foi escolhido para o treinamento final do modelo por apresentar o melhor equilíbrio entre separação dos grupos e consistência interna dos clusters, resultando na segmentação mais adequada para a estrutura dos dados analisados

- **Tratamento de Outliers e Análise de Estabilidade**: Calculamos a distância euclidiana de cada ponto ao centroide do seu respectivo cluster e plotamos um histograma para validar a robustez dos grupos gerados. Ambas as curvas do histograma seguem uma distribuição bem comportada, concentrando a grande maioria dos candidatos a distâncias predominantemente entre 1.0 e 3.0 dos seus centros. Não há a presença de caudas excessivamente longas, o que demonstra que candidatos com notas anômalas não distorceram a estrutura geométrica encontrada.
  
- **Redução de Dimensionalidade**: Utilizamos a técnica PCA (Principal Component Analysis) para reduzir a dimensionalidade dos dados (de 12 colunas originais para 2) e permitir visualização gráfica. A redução manteve aproximadamente 55,94% da variância total dos dados originais (Sendo o Componente Principal 1 = 28,63% e Componente Principal 2 = 27,31%)..
  ```python
  from sklearn.decomposition import PCA
  pca = PCA(n_components=2, random_state=42)
  X_pca = pca.fit_transform(X_scaled)
  ```
<!-- Nesta etapa, deverão ser descritas todas as técnicas utilizadas para pré-processamento/tratamento dos dados.

Algumas das etapas podem estar relacionadas à:

* Limpeza de Dados: trate valores ausentes: decida como lidar com dados faltantes, seja removendo linhas, preenchendo com médias, medianas ou usando métodos mais avançados; remova _outliers_: identifique e trate valores que se desviam significativamente da maioria dos dados.

* Transformação de Dados: normalize/padronize: torne os dados comparáveis, normalizando ou padronizando os valores para uma escala específica; codifique variáveis categóricas: converta variáveis categóricas em uma forma numérica, usando técnicas como _one-hot encoding_.

* _Feature Engineering_: crie novos atributos que possam ser mais informativos para o modelo; selecione características relevantes e descarte as menos importantes.

* Tratamento de dados desbalanceados: se as classes de interesse forem desbalanceadas, considere técnicas como _oversampling_, _undersampling_ ou o uso de algoritmos que lidam naturalmente com desbalanceamento.

* Separação de dados: divida os dados em conjuntos de treinamento, validação e teste para avaliar o desempenho do modelo de maneira adequada.
  
* Manuseio de Dados Temporais: se lidar com dados temporais, considere a ordenação adequada e técnicas específicas para esse tipo de dado.
  
* Redução de Dimensionalidade: aplique técnicas como PCA (Análise de Componentes Principais) se a dimensionalidade dos dados for muito alta.

* Validação Cruzada: utilize validação cruzada para avaliar o desempenho do modelo de forma mais robusta.

* Monitoramento Contínuo: atualize e adapte o pré-processamento conforme necessário ao longo do tempo, especialmente se os dados ou as condições do problema mudarem.

* Entre outras....

Avalie quais etapas são importantes para o contexto dos dados que você está trabalhando, pois a qualidade dos dados e a eficácia do pré-processamento desempenham um papel fundamental no sucesso de modelo(s) de aprendizado de máquina. É importante entender o contexto do problema e ajustar as etapas de preparação de dados de acordo com as necessidades específicas de cada projeto. -->

# Descrição dos modelos
### K-Means

O algoritmo K-Means foi utilizado como técnica de aprendizado não supervisionado como o objetivo de identificar padrões e classificar os candidatos em grupos com características semelhantes. Diferente dos modelos supervisionados, o K-Means **não utiliza variável alvo** durante o treinamento, realizando os agrupamentos com base na similaridade entre os dados de entrada.

Ofuncionamento do algoritmo baseia-se na criação de centróides, que representam o centro de cada cluster. A partir disso, os registros são associados ao grupo cujo centróide apresenta menor distância em relação aos seus atributos. Esse processo é repetido iterativamente até que os clusters se estabilizem.

O K-Means foi escolhido devido à sua simplicidade e capacidade de identificar padrões em grandes volumes de dados. Além disso, o algoritmo permite compreender diferentes perfis de candidatos, constibuindo para análises exploratórias complementares ao modelo supervisionado.

Entre as vantagens do K-Means, destacam-se a facilidade de implementação, boa escalabilidade e interpretabilidade dos grupos formados. Como limitação, o modelo é sensível à escolha do número de clusters, à escala de variáveis e à presença de sobreposição entre os grupos.

### XGBoost

O algoritmo XGBoost (_Extreme Gradient Boosting_) foi utilizado como técnica de aprendizado supervisionado para classificar os candidatos entre aprovados e não aprovados. O modelo baseia-se em árvores de decisão construídas sequencialmente, onde cada nova árvore busca corrigir os erros das anteriores por meio de técnicas de otimização baseadas em gradiente.

O funcionamento do XGBoost ocorre através do método _boosting_, combinando múltiplas árvores para melhorar gradualmente o desempenho do modelo. Além disso, o algoritmo utiliza regularização para reduzir overfitting e melhorar a capacidade de generalização.

O XGBoost foi escolhido por conta do seu desempenho em problemas de classificação, capacidade de lidar com um maior volume de dados e eficiência na identificação de relações não lineares entre as variáveis.

Entre as vantagens do modelo, destacam-se a alta precisão, robustez e capacidade de capturar padrões complexos. Como limitação, o algoritmo apresenta maior custo computacional e maior sensibilidade ao ajuste de hiperparâmetros.


# Avaliação dos modelos criados

## Métricas utilizadas

### K-Means

Para avaliar a qualidade dos agrupamentos gerados pelo algoritmo, foram utilizadas diferentes métricas de validação interna, considerando que modelos de clusterização não possuem variável alvo para comparação direta.

A primeira métrica utilizada foi a **inércia**, responsável por medir a soma das distâncias entre os pontos e os centróides de seus respectivos clusters. Valores menores indicam grupos mais compactos e homogêneos. Para **k = 2**, o modelo apresentou inércia aproximada de **1.655.121,00**.

Também foi utilizado o **Silhouette Score**, métrica que avalia simultaneamente a coesão interna e a separação entre os clusters. O modelo obteve valot aproximado de **0,3389**, indicando separação moderada entre os grupos formados e sugerindo que os clusters apresentam características relativamente distintas.

Outra métrica aplicada foi o **Davies-Bouldin Index (DBI)**, utilizado para medir similaridade entre os clusters. Valores menores indicam melhor separação e menor sobreposição entre os grupos. O modelo apresentou **DBI = 1,6200**.

Além disso, foi utilizado o **Calinski-Harabasz Index (CHI)**, que avalia a razão entre clusters e dispersão interna dos grupos. Valores maiores indicam definição dos agrupamentos. O modelo obteve **CHI = 55.820,27** sugerindo boa capacidade de superação entre os clusters identificados.

A utilização conjunta dessas métricas permitiu avaliar a qualidade da clusterização de forma mais robusta, auxiliando na escolha do número ideal de clusters e na interpretação dos grupos formados pelo modelo.

### XGBoost

Para avaliar o desempenho do modelo XGBoost, foram utilizadas métricas de classificação supervisionada, considerando o desbalanceamento entre as classes.

A **accuracy** foi utilizada para medir a proporção geral de acertos do modelo que apresentou aproximadamente **94,47%** de acurácia.

Também foram utilizadas as métricas de **precision, recall** e **F1-score**. A _precision_ mede a quantidade de previsões positivas corretas, o _recall_ avalia a capacidade do modelo em identificar candidados aprovados, e o _F1-score_ representa o equilíbrio entre essas duas métricas.

Para a classe de aprovados, o modelo apresentou aproximadamente **72,70% de precision**, **70,20% de recall** e **71,40% de F1-score**, indicando desempenho satisfatório na identificação da classe minoritária (aprovados).

Além disso, foram analisadas métricas da matriz de confusão, como **specificity**, **false positive rate** e **false negative rate**, permitindo avaliar os erros cometidos pelo modelo.

Durante os experimentos, foram realizados ajustes de hiperparâmetros como **_learning_rate=0.30_**, **_max_depth=10_** e **_n_estimators=671_**, buscando melhorar o desempenho do modelo. Também foram utilizados parâmetros de regularização, como **gamma, subsample, colsample_bytree, reg_alpha** e **reg_lambda**, com o objetivo de reduzir overfitting e melhorar a capacidade de generalização.


## Discussão dos resultados obtidos

Nesta seção, discuta os resultados obtidos por cada um dos modelos construídos na Etapa 03 e na Etapa 04, no contexto prático em que os dados se inserem, promovendo uma compreensão abrangente e aprofundada da qualidade de cada um deles. Lembre-se de relacionar os resultados obtidos ao problema identificado, a questão de pesquisa levantada e estabelecer relação com os objetivos previamente propostos. Não deixe de comparar os resultados obtidos por cada modelo com os demais.

# Revisão do pipeline de pesquisa e análise de dados

Nesta etapa, os alunos devem revisar o pipeline de pesquisa e análise de dados proposto na Etapa 03, avaliando criticamente cada uma de suas etapas, fluxos e decisões. O objetivo agora é identificar possíveis ajustes, melhorias ou generalizações que tornem o pipeline mais abrangente e adaptável, de forma que ele seja capaz de representar qualquer processo de construção de sistemas de aprendizado de máquina – independentemente da área de aplicação, tipo de dado ou técnica utilizada.

Lembre-se de que um pipeline bem estruturado deve contemplar, de forma flexível e modular, as principais fases da pesquisa e experimentação em ciência de dados e aprendizado de máquina, incluindo (mas não se limitando a): formulação do problema, coleta e preparação dos dados, análise exploratória, definição de métricas, seleção e validação de modelos, interpretação dos resultados e documentação.

O resultado desta etapa deverá ser um pipeline revisado e justificado, acompanhado de uma breve descrição das alterações realizadas e dos motivos que levaram a cada mudança.

## Observações importantes

Todas as tarefas realizadas nesta etapa deverão ser registradas em formato de texto junto com suas explicações de forma a apresentar os códigos desenvolvidos e também, o código deverá ser incluído, na íntegra, na pasta "src".
