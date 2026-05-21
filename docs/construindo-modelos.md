# Preparação dos dados
Antes da aplicação do algoritmo K-Means, foi necessário realizar etapas de preparação e transformação dos dados, garantindo maior qualidade na formação dos clusters e evitando distorções nos cálculos de distância

- **Seleção de Features**: Definimos o conjunto de features que melhor representam os perfis dos candidatos:
  ```python
  features_cluster = df_dataset_tratado[['NOTA_L', 'NOTA_CH', 'NOTA_CN', 'NOTA_M', 'NOTA_R',
                                         'PESO_L', 'PESO_CH', 'PESO_CN', 'PESO_M', 'PESO_R',
                                         'GRAU_T', 'TIPO_MOD_CONCORRENCIA_T']].copy()
  ```
  Evitamos deliberadamente variáveis puramente identificadoras (como códigos de curso ou candidato) que não possuem significado ordinal, pois elas poderiam introduzir distorções na distância euclidiana

- **Transformação de Variáveis Categóricas**: O K-Means interpreta distância numérica, o que criaria viés artificial. Por isso, aplicamos one-hot encoding completo. Essa transformação expandiu as colunas categóricas em variáveis binárias (dummies), garantindo que cada categoria fosse tratada de forma equidistante e sem ordenação implícita.
  ```python
  features_cluster = pd.get_dummies(features_cluster, drop_first=False)
  ```
- **Normalização dos Dados**: Como o K-Means é um algoritmo baseado em distâncias (euclidiana), variáveis em escalas diferentes distorceriam os resultados (notas variam na casa das centenas; pesos geralmente entre 1 e 3). Aplicamos StandardScaler para centralizar todas as features com média 0 e desvio padrão 1:
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

- **Tratamento de Outliers e Análise de Estabilidade**: Embora o dataset já estivesse tratado, realizamos análise pós-clusterização para validar a robustez:
    - Calculamos a distância euclidiana de cada ponto ao centroide do seu cluster.
    - Plotamos histograma das distâncias (com KDE) por cluster.
    - Verificamos estatísticas descritivas das distâncias.

- **Definição do Número de Clusters**: Como o algoritmo K-Means requer a definição prévia do número de clusters (n_clusters), realizamos uma análise sistemática para identificar o valor mais adequado para nossos dados. Foram testados valores de K variando de 2 a 6, utilizando duas métricas principais de validação interna:
    - Método do Cotovelo (Elbow Method): baseado na inércia (soma das distâncias quadradas intra-cluster). Buscamos o ponto de inflexão onde o ganho de redução de inércia se torna marginal.
    - Silhouette Score: métrica que avalia simultaneamente a coesão interna dos clusters e a separação entre eles. Quanto mais próximo de 1, melhor a qualidade do agrupamento.
  ```python
  K = range(2, 7)
  inercias = []
  silhuetas = []
  
  for k in K:
      model_k = KMeans(n_clusters=k, random_state=42, n_init=10)
      labels_k = model_k.fit_predict(X_scaled)
      inercias.append(model_k.inertia_)
      silhuetas.append(silhouette_score(X_scaled, labels_k))
  ```
  
- **Redução de Dimensionalidade**: Foi utilizada a técnica PCA (Principal Component Analysis) para reduzir a dimensionalidade dos dados e permitir visualização gráfica dos clusters em duas dimensões. A redução manteve aproximadamente 55,92% da variância total dos dados originais.
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

### Modelo X

REMOVER POSTERIORMENTE ---->>>> Nesta seção, conhecendo os dados e de posse dos dados preparados, é hora de descrever os outros dois algoritmos de aprendizado de máquina selecionados para a construção dos modelos propostos. Inclua informações abrangentes sobre cada algoritmo implementado, aborde conceitos fundamentais, princípios de funcionamento, vantagens/limitações e justifique a escolha de cada um dos algoritmos. 

Explore aspectos específicos, como o ajuste dos parâmetros livres de cada algoritmo. Lembre-se de experimentar parâmetros diferentes e principalmente, de justificar as escolhas realizadas e registrar todos os experimentos realizados.

# Avaliação dos modelos criados

## Métricas utilizadas

### K-Means

Para avaliar a qualidade dos agrupamentos gerados pelo algoritmo, foram utilizadas diferentes métricas de validação interna, considerando que modelos de clusterização não possuem variável alvo para comparação direta.

A primeira métrica utilizada foi a **inércia**, responsável por medir a soma das distâncias entre os pontos e os centróides de seus respectivos clusters. Valores menores indicam grupos mais compactos e homogêneos. Para **k = 2**, o modelo apresentou inércia aproximada de **1.655.121,00**.

Também foi utilizado o **Silhouette Score**, métrica que avalia simultaneamente a coesão interna e a separação entre os clusters. O modelo obteve valot aproximado de **0,3389**, indicando separação moderada entre os grupos formados e sugerindo que os clusters apresentam características relativamente distintas.

Outra métrica aplicada foi o **Davies-Bouldin Index (DBI)**, utilizado para medir similaridade entre os clusters. Valores menores indicam melhor separação e menor sobreposição entre os grupos. O modelo apresentou **DBI = 1,6200**.

Além disso, foi utilizado o **Calinski-Harabasz Index (CHI)**, que avalia a razão entre clusters e dispersão interna dos grupos. Valores maiores indicam definição dos agrupamentos. O modelo obteve **CHI = 55.820,27** sugerindo boa capacidade de superação entre os clusters identificados.

A utilização conjunta dessas métricas permitiu avaliar a qualidade da clusterização de forma mais robusta, auxiliando na escolha do número ideal de clusters e na interpretação dos grupos formados pelo modelo.

### Modelo X

Nesta seção, as métricas utilizadas para avaliar os modelos desenvolvidos deverão ser apresentadas (p. ex.: acurácia, precisão, recall, F1-Score, MSE etc.). A escolha de cada métrica deverá ser justificada, pois esta escolha é essencial para avaliar de forma mais assertiva a qualidade do modelo construído. 

## Discussão dos resultados obtidos

Nesta seção, discuta os resultados obtidos por cada um dos modelos construídos na Etapa 03 e na Etapa 04, no contexto prático em que os dados se inserem, promovendo uma compreensão abrangente e aprofundada da qualidade de cada um deles. Lembre-se de relacionar os resultados obtidos ao problema identificado, a questão de pesquisa levantada e estabelecer relação com os objetivos previamente propostos. Não deixe de comparar os resultados obtidos por cada modelo com os demais.

# Revisão do pipeline de pesquisa e análise de dados

Nesta etapa, os alunos devem revisar o pipeline de pesquisa e análise de dados proposto na Etapa 03, avaliando criticamente cada uma de suas etapas, fluxos e decisões. O objetivo agora é identificar possíveis ajustes, melhorias ou generalizações que tornem o pipeline mais abrangente e adaptável, de forma que ele seja capaz de representar qualquer processo de construção de sistemas de aprendizado de máquina – independentemente da área de aplicação, tipo de dado ou técnica utilizada.

Lembre-se de que um pipeline bem estruturado deve contemplar, de forma flexível e modular, as principais fases da pesquisa e experimentação em ciência de dados e aprendizado de máquina, incluindo (mas não se limitando a): formulação do problema, coleta e preparação dos dados, análise exploratória, definição de métricas, seleção e validação de modelos, interpretação dos resultados e documentação.

O resultado desta etapa deverá ser um pipeline revisado e justificado, acompanhado de uma breve descrição das alterações realizadas e dos motivos que levaram a cada mudança.

## Observações importantes

Todas as tarefas realizadas nesta etapa deverão ser registradas em formato de texto junto com suas explicações de forma a apresentar os códigos desenvolvidos e também, o código deverá ser incluído, na íntegra, na pasta "src".
