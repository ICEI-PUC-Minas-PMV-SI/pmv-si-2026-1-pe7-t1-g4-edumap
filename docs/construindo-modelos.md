# Preparação dos dados

### K-Means
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

### XGBoost
- **Escolha das Features, do Target e Transformação de Dados (Encoding)**: Nesta etapa inicial, delimitamos quais variáveis serão utilizadas como preditoras (features) e qual será a variável de saída (target). As features selecionadas foram as notas (Linguagens, Ciências Humanas, Ciências da Natureza, Matemática, Redação), Grau, Tipo de Modalidade de Concorrência e Código do Curso. O target definido foi a coluna de aprovação (`APROVADO_T`).  Realizamos também a transformação da variável categórica `CODIGO_CURSO` em múltiplas colunas numéricas (variáveis dummy) utilizando a função pd.get_dummies. A separação entre features e target é a base do aprendizado supervisionado, ensinando ao modelo o que ele deve ler para tentar prever o resultado.  A transformação via dummies (One-Hot Encoding) foi necessária porque algoritmos de aprendizado de máquina exigem entradas numéricas, justificando a exclusão da primeira coluna (drop_first=True) para evitar multicolinearidade.  
  ```python
    features = df_dataset_tratado[[
        'NOTA_L',
        'NOTA_CH',
        'NOTA_CN',
        'NOTA_M',
        'NOTA_R',
        'GRAU_T',
        'TIPO_MOD_CONCORRENCIA_T',
        'CODIGO_CURSO'
    ]]
    
    features = pd.get_dummies(
        features,
        columns=['CODIGO_CURSO'],
        drop_first=True
    )
    
    target = df_dataset_tratado['APROVADO_T']
  ```
  Saída de Dados
  ```python
    Shape das features:
    (183541, 640)
  ```

- **Separação dos Dados (Treino e Teste):** O conjunto de dados total foi dividido em duas partes: 80% das amostras foram separadas para o treinamento do modelo e 20% foram reservadas para teste. Utilizamos a função `train_test_split` com o parâmetro `stratify=target`, a divisão impede o overfitting (quando o modelo apenas memoriza os dados), permitindo avaliar sua real capacidade de generalização em dados nunca vistos. O uso do parâmetro `stratify` foi fundamental devido ao alto desbalanceamento (90,2% de reprovados contra 9,8% de aprovados), pois ele garante que a proporção original entre as classes seja rigorosamente preservada tanto no conjunto de treino quanto no de teste
  ```python
    X_train, X_test, y_train, y_test = train_test_split(features, target.values.ravel(), test_size=0.2, random_state=42, stratify=target)
  ```
  Saída de Dados
  ```python
    Distribuição em y_train (percentual):
    0    0.902099
    1    0.097901
    
    Distribuição em y_test (percentual):
    0    0.902095
    1    0.097905
  ```

- **Tratamento de Dados Desbalanceados (Oversampling com SMOTE):** Aplicamos a técnica SMOTE (Synthetic Minority Over-sampling Technique) de forma exclusiva no conjunto de treinamento.  O SMOTE cria novas amostras sintéticas da classe minoritária (Aprovados) fazendo uma interpolação entre os vizinhos mais próximos, em vez de simplesmente duplicar linhas existentes. A distribuição inicial do target era altamente desbalanceada (apenas ~9,8% de aprovados). Isso faz com que o modelo tenda a favorecer a classe majoritária. O SMOTE foi testado para reduzir esse viés, ajudando o modelo a reconhecer os padrões da classe minoritária. (Nota: embora testado na preparação, análises posteriores do documento mostraram que o modelo base sem SMOTE teve acurácia mais estável no contexto do SISU, mas a técnica compõe a exploração da preparação )
  ```python
    sm = SMOTE(random_state=42)
    X_tr_sm, y_tr_sm = sm.fit_resample(X_train, y_train)
  ```

- **Validação Cruzada (K-Fold):** Aplicamos a Validação Cruzada K-Fold (StratifiedKFold) para dividir os dados em 5 partes (folds). Durante o processo, 4 partes são usadas para treinar o modelo e 1 parte para validação, repetindo-se o ciclo até que todas as partes tenham sido usadas como validação. Para garantir que o desempenho do modelo não fosse dependente de uma única separação "sortuda" ou "azarada" dos dados entre treino e teste.  Essa técnica fornece uma métrica média muito mais confiável e estável sobre a capacidade de generalização do algoritmo. 
Saída de Dados
  ```python
    F1-weighted por fold: [0.7622, 0.7671, 0.6479, 0.7619, 0.8664]
    F1-weighted médio: 0.7611
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







## Avaliação dos modelos criados

A avaliação dos modelos criados foi realizada considerando a finalidade de cada técnica aplicada no projeto. Como foram construídos modelos com naturezas diferentes, a análise dos resultados também precisou seguir critérios diferentes. O K-Means foi utilizado como modelo de aprendizado não supervisionado, com o objetivo de identificar agrupamentos naturais entre os candidatos a partir das características presentes no dataset. Já o XGBoost foi utilizado como modelo supervisionado, voltado à previsão da situação final do candidato, classificando os registros entre aprovados e não aprovados.

Essa diferença é importante porque os dois modelos não respondem exatamente à mesma pergunta. O K-Means contribui para compreender a estrutura interna dos dados, revelando perfis de candidatos e padrões de concorrência sem usar diretamente a variável de aprovação como alvo no treinamento. O XGBoost, por outro lado, aprende a partir de exemplos já rotulados, buscando identificar relações entre as variáveis explicativas e a classe final de aprovação.

No contexto do SISU, essa avaliação é especialmente relevante porque o dataset apresenta forte desbalanceamento entre as classes. A maior parte dos registros pertence a candidatos não aprovados, enquanto os aprovados representam uma parcela menor do conjunto. Esse comportamento é esperado em processos seletivos concorridos, mas exige cuidado na interpretação das métricas. Uma acurácia elevada, por exemplo, pode transmitir uma impressão exageradamente positiva se o modelo estiver apenas reconhecendo bem a classe majoritária e falhando na identificação da classe minoritária.

## Métricas utilizadas

### K-Means

Para avaliar a qualidade dos agrupamentos gerados pelo K-Means, foram utilizadas métricas de validação interna, já que modelos de clusterização não possuem uma variável alvo para comparação direta. O objetivo foi analisar se os clusters formados apresentavam coesão interna, separação entre si e coerência com os padrões presentes nos dados.

Antes da definição do modelo final, foram testados diferentes valores de K, variando de 2 a 6. Essa etapa foi necessária porque o número de clusters influencia diretamente a forma como os dados são segmentados. Para apoiar essa escolha, foram utilizadas duas abordagens principais: o Método do Cotovelo, baseado na inércia, e o Silhouette Score, voltado à avaliação da coesão interna e da separação entre os grupos.


<img width="688" height="389" alt="metodocotovelo" src="https://github.com/user-attachments/assets/9adfbe62-f549-4e76-bacd-7ac9bb82b0ac" />

O Método do Cotovelo mostrou que a inércia diminui conforme o número de clusters aumenta, comportamento esperado no K-Means. Essa redução ocorre porque, ao criar mais grupos, os pontos tendem a ficar mais próximos dos seus respectivos centroides. O problema é que essa melhora nem sempre significa que os clusters ficaram mais interpretáveis. A partir de certo ponto, o ganho passa a ser menor, criando grupos mais fragmentados sem necessariamente melhorar a leitura geral da segmentação.

Nos testes realizados, o valor de K = 2 apresentou inércia aproximada de 1.681.526,46. Para K = 3, a inércia caiu para aproximadamente 1.371.787,98, mas essa redução veio acompanhada de piora no Silhouette Score. Isso indica que, embora três clusters reduzissem as distâncias internas, eles não melhoravam a separação entre os grupos de forma consistente.


<img width="691" height="389" alt="silhouettascore" src="https://github.com/user-attachments/assets/4ee4a41a-947b-47cf-9e30-55f4e7598711" />

O Silhouette Score foi a principal métrica utilizada para apoiar a escolha do número de clusters. Essa métrica avalia se os pontos estão mais próximos dos elementos do próprio cluster do que dos elementos de outros clusters. Valores próximos de 1 indicam separação mais clara, valores próximos de 0 indicam sobreposição entre grupos e valores negativos sugerem que pontos podem ter sido alocados em clusters inadequados.

Entre os valores testados, K = 2 apresentou o melhor Silhouette Score, com valor aproximado de 0,3414. Os demais valores de K tiveram resultados inferiores, como 0,2184 para K = 3, 0,2281 para K = 4, 0,2423 para K = 5 e 0,2525 para K = 6. Com isso, K = 2 foi definido como a melhor escolha para o treinamento principal, por apresentar o melhor equilíbrio entre separação dos grupos e consistência interna dos clusters.


<img width="659" height="544" alt="silhuetaamostra" src="https://github.com/user-attachments/assets/c4165e22-7028-4580-9741-7b6463e075d0" />

A análise visual da silhueta por amostra mostrou que a separação obtida pelo K-Means pode ser considerada moderada. O score médio ficou próximo ao resultado calculado nas métricas, indicando que o modelo conseguiu encontrar alguma estrutura nos dados, mas não separou os grupos de forma totalmente nítida.

O gráfico também mostra diferença entre os clusters. Um dos grupos concentrou maior parte dos registros e apresentou uma região mais consistente, enquanto o outro apresentou menor coesão e algumas amostras com valores negativos ou próximos de zero. Isso sugere que existem pontos localizados em áreas de fronteira, próximos de mais de um cluster, o que reforça a ideia de sobreposição entre perfis.

Esse resultado faz sentido dentro do problema analisado. A aprovação no SISU não depende apenas da nota bruta do candidato, mas de uma combinação entre nota final, curso escolhido, instituição, modalidade de concorrência, quantidade de vagas, pesos das disciplinas, nota de corte e classificação. Por isso, é esperado que os candidatos não se organizem em grupos perfeitamente separados.

<img width="859" height="481" alt="distribuicaopontos" src="https://github.com/user-attachments/assets/351aca8a-4191-4299-b040-eafd8d2f5fac" />

A distribuição das distâncias dos pontos aos seus respectivos centroides foi utilizada para avaliar a compactação dos clusters e a possível presença de outliers. Esse gráfico mostra o quanto os candidatos estão próximos ou distantes do centro geométrico do grupo ao qual foram atribuídos.

A análise indicou que um dos clusters apresentou maior densidade e homogeneidade, enquanto o outro mostrou maior dispersão. Essa diferença sugere que o K-Means identificou um grupo mais compacto e outro mais heterogêneo. No contexto do SISU, essa heterogeneidade pode estar relacionada às diferentes regras de peso adotadas pelas instituições e cursos, já que algumas universidades utilizam pesos iguais para todas as áreas, enquanto outras valorizam determinadas disciplinas de acordo com o curso.

Também foi observado que existem pontos mais distantes dos centroides, formando uma cauda na distribuição. Esses casos podem representar candidatos com combinações atípicas de notas, pesos ou escolhas de curso. A presença desses pontos não invalida o modelo, mas mostra que o comportamento dos candidatos não é completamente uniforme.

Depois da análise inicial, foram calculadas as principais métricas de avaliação do K-Means. O modelo apresentou Silhouette Score = 0,3414, Davies-Bouldin Index = 1,6146 e Calinski-Harabasz Index = 56.863,5383.

O Silhouette Score de 0,3414 indica uma separação intermediária entre os clusters. Esse valor mostra que existem diferenças entre os grupos, mas que elas não são fortes o suficiente para afirmar que os candidatos foram divididos em perfis completamente distintos. O Davies-Bouldin Index de 1,6146 reforça essa leitura, pois valores menores indicam melhor separação e menor sobreposição entre clusters. Nesse caso, o resultado mostra que há alguma dispersão entre os grupos. Já o Calinski-Harabasz Index apresentou valor elevado, sugerindo que existe uma boa estrutura geral na divisão dos dados, mesmo que a separação não seja perfeita.

<img width="1161" height="428" alt="comparativodenotas" src="https://github.com/user-attachments/assets/f4dda304-6d5d-410e-bd5a-46d8f34109f6" />

A análise dos centroides permitiu interpretar melhor o significado dos agrupamentos. O gráfico comparativo de notas médias por cluster mostrou diferenças entre os grupos em disciplinas como Linguagens, Ciências Humanas, Ciências da Natureza, Matemática e Redação. Essa comparação ajuda a transformar os clusters em perfis mais compreensíveis, em vez de tratá-los apenas como divisões numéricas.

A diferença entre os clusters não indica uma separação pura entre aprovados e não aprovados. O modelo parece ter captado mais fortemente perfis de concorrência e padrões de composição da nota do que a aprovação propriamente dita. Isso mostra uma limitação importante do K-Means para esse problema: como ele não utiliza a variável APROVADO como alvo, ele não tenta aprender diretamente a fronteira entre aprovação e reprovação.

O gráfico dos pesos médios por cluster reforçou essa interpretação. A presença das variáveis de peso influenciou a formação dos agrupamentos, já que o K-Means utiliza distância euclidiana e é sensível à escala e à distribuição das variáveis. Mesmo com padronização, os pesos podem ter ajudado o modelo a separar candidatos mais pela regra de cálculo da nota do que pelo desempenho final em si.

Essa análise é importante porque mostra que os clusters não devem ser interpretados simplesmente como “grupo dos aprovados” e “grupo dos não aprovados”. A leitura mais adequada é que o modelo encontrou dois perfis de concorrência: um mais associado a cursos ou instituições com pesos diferenciados, e outro mais associado a regras de peso mais homogêneas.

<img width="1002" height="636" alt="clusterdimensionalidade" src="https://github.com/user-attachments/assets/23cc6ad2-6642-4426-b224-1757bac3d126" />

A visualização dos clusters após redução de dimensionalidade com PCA foi utilizada para representar os agrupamentos em duas dimensões. Como o conjunto original possui várias variáveis, o PCA ajuda a projetar os dados em um espaço visual mais simples, facilitando a observação da separação entre os grupos.

O gráfico mostrou que existe uma divisão entre os clusters, mas também regiões de proximidade e possível sobreposição. Essa visualização confirma o que as métricas já indicavam: o K-Means conseguiu encontrar estrutura nos dados, mas essa estrutura não é totalmente separada. O resultado é útil para análise exploratória, mas não deve ser tratado como uma solução definitiva para prever aprovação.

<img width="1154" height="860" alt="biplot" src="https://github.com/user-attachments/assets/18bb2c39-1ef3-4b2a-aa7e-e16dce98c6a8" />

O Biplot PCA com Clusters complementa a visualização anterior porque, além dos pontos agrupados, apresenta a direção e a influência das variáveis na projeção. Esse gráfico permite observar quais atributos ajudam a explicar a separação dos grupos no espaço formado pelas componentes principais.

A interpretação do biplot indica que a variabilidade dos dados está relacionada principalmente a dois fatores: o desempenho dos candidatos nas notas e o efeito dos pesos utilizados pelos cursos e instituições. As notas tendem a explicar parte da variação em uma direção, enquanto os pesos ajudam a explicar outra dimensão da separação. Isso reforça a conclusão de que o K-Means não isolou simplesmente aprovados e não aprovados, mas identificou perfis de concorrência influenciados tanto pelo desempenho acadêmico quanto pelas regras de composição da nota.

Depois do primeiro treinamento, foi realizada uma nova abordagem com refinamento de features e remoção das variáveis de peso. O objetivo foi testar se os pesos estavam influenciando artificialmente a formação dos clusters. Nesse segundo treinamento, a distribuição dos registros ficou mais equilibrada entre os grupos: o Cluster 0 passou a ter 94.763 registros e o Cluster 1 passou a ter 88.778 registros. As métricas, porém, indicaram uma leitura mista: o Silhouette Score caiu para 0,2730, enquanto o Davies-Bouldin Index melhorou para 1,3598 e o Calinski-Harabasz Index subiu para 84.373,8933.


### XGBoost

Para avaliar o desempenho do XGBoost, foram utilizadas métricas de classificação supervisionada. Como o objetivo do modelo era prever a situação final do candidato, a avaliação foi feita comparando as previsões do modelo com os valores reais da variável APROVADO.

O modelo foi treinado com hiperparâmetros ajustados, incluindo learning_rate = 0,30, max_depth = 10 e n_estimators = 671. Também foram utilizados parâmetros como gamma, subsample, colsample_bytree, reg_alpha e reg_lambda, buscando controlar a complexidade do modelo, reduzir overfitting e melhorar a capacidade de generalização.

As previsões foram feitas a partir das probabilidades geradas pelo modelo, com uso de threshold igual a 0,4 para a classe positiva. Essa escolha é relevante em um cenário desbalanceado, pois permite ajustar o ponto de decisão para tentar melhorar a identificação dos aprovados.

<Gráfico Relatório de Classificação do XGBoost>

  ```python

Relatório de Classificação:
               precision    recall  f1-score   support

           0       0.97      0.97      0.97     33115
           1       0.72      0.68      0.70      3594

    accuracy                           0.94     36709
   macro avg       0.84      0.82      0.83     36709
weighted avg       0.94      0.94      0.94     36709
  ```

A primeira métrica analisada foi a acurácia. O modelo apresentou aproximadamente 94% de acurácia, indicando alto desempenho geral. Mesmo assim, a acurácia precisa ser interpretada com cuidado, pois a classe de não aprovados é muito maior do que a classe de aprovados. Em uma base desbalanceada, um modelo pode parecer muito eficiente apenas por acertar a classe majoritária.

Por esse motivo, foram analisadas também as métricas precision, recall e F1-score para cada classe. Para a classe 0, referente aos não aprovados, o modelo apresentou precision de 0,97, recall de 0,97 e F1-score de 0,97. Esses valores mostram que o XGBoost reconheceu muito bem a classe majoritária.

Para a classe 1, referente aos aprovados, o modelo apresentou precision de 0,72, recall de 0,68 e F1-score de 0,70. Esse resultado é importante porque mostra que o modelo conseguiu identificar uma parte significativa dos aprovados, mesmo sendo a classe minoritária. O desempenho é inferior ao obtido para os não aprovados, mas pode ser considerado satisfatório diante do desbalanceamento dos dados.

A precision de 0,72 indica que, entre os candidatos classificados como aprovados pelo modelo, uma proporção relevante realmente pertencia a essa classe. O recall de 0,68 indica que o modelo conseguiu encontrar 68% dos aprovados reais. O F1-score de 0,70 mostra um equilíbrio razoável entre essas duas métricas, sendo uma medida mais adequada do que a acurácia para avaliar a classe minoritária.

<img width="690" height="590" alt="roccurve" src="https://github.com/user-attachments/assets/67be0059-7e5c-4a68-89fd-81a44e05348d" />

A Curva ROC também foi utilizada para avaliar o desempenho do modelo. O ROC AUC obtido foi de aproximadamente 0,9582, resultado bastante elevado. Essa métrica avalia a capacidade do modelo de separar as classes em diferentes limiares de decisão. Quanto mais próximo de 1, maior a capacidade de distinguir corretamente aprovados e não aprovados.

Esse resultado mostra que o XGBoost aprendeu padrões relevantes nos dados e conseguiu ordenar bem os candidatos em termos de probabilidade de aprovação. Mesmo que ainda existam erros na classificação final, o alto valor de ROC AUC indica boa capacidade discriminativa.

<img width="527" height="393" alt="matrizdeconfusao" src="https://github.com/user-attachments/assets/8246285a-e0e5-432e-bfbc-b06b2e7dcd85" />


A matriz de confusão permitiu observar os acertos e erros do modelo de forma mais concreta. A saída analisada apresentou 31.319 verdadeiros negativos, 2.202 verdadeiros positivos, 1.796 falsos positivos e 1.392 falsos negativos.

Esses valores mostram que o modelo teve ótimo desempenho ao identificar candidatos não aprovados, mas ainda apresentou erros relevantes na classe dos aprovados. Os falsos negativos merecem atenção, pois representam candidatos que foram aprovados na realidade, mas que o modelo classificou como não aprovados. Em um estudo sobre aprovação no SISU, esse tipo de erro é importante porque afeta justamente a classe de maior interesse analítico.

<img width="515" height="413" alt="matrizconfusaonormalizadaporclasse" src="https://github.com/user-attachments/assets/e21509a3-8237-435a-9663-8eff8c478b01" />

A matriz de confusão normalizada ajudou a interpretar esses resultados proporcionalmente. Essa visualização é útil porque evita que a classe majoritária domine a leitura dos erros. Com ela, fica mais claro que o modelo apresenta desempenho superior para a classe 0 e desempenho mais moderado para a classe 1.

A análise confirma que o XGBoost é forte para reconhecer o padrão dos não aprovados, mas ainda encontra maior dificuldade para capturar todos os aprovados. Essa dificuldade não significa que o modelo seja ruim. Ela reflete a própria estrutura do problema: há poucos aprovados em relação ao total de candidatos, e a aprovação depende de variáveis altamente competitivas e específicas.

<img width="877" height="394" alt="importanciadasfeatures" src="https://github.com/user-attachments/assets/deeced21-a356-4850-8a9a-457a9f695536" />

A importância das features foi analisada para compreender quais variáveis tiveram maior influência nas decisões do modelo. Embora o gráfico presente no notebook esteja identificado como “Importância das Features - Random Forest”, essa visualização foi utilizada na etapa supervisionada como apoio interpretativo para observar o peso relativo das variáveis na previsão da aprovação dos candidatos.

Essa análise ajuda a identificar quais atributos contribuíram mais para distinguir aprovados e não aprovados. Em um problema como o do SISU, essa leitura é relevante porque permite verificar se o modelo está se apoiando em variáveis coerentes com a lógica do processo seletivo, como nota do candidato, nota de corte, classificação, curso, quantidade de vagas e modalidade de concorrência.

A leitura desse gráfico também contribui para tornar a análise mais explicável. Em vez de observar apenas o resultado final da previsão, é possível discutir quais fatores tiveram maior participação no processo de decisão do modelo. Isso fortalece a interpretação dos resultados e permite relacionar o desempenho obtido ao contexto prático da competitividade dos cursos.

A Permutation Importance foi considerada como uma técnica complementar para avaliar a relevância das variáveis, mas no material analisado ela aparece mais como referência metodológica do que como um gráfico específico a ser inserido. Por esse motivo, não foi adicionada uma marcação própria para esse item. A análise visual de importância das features ficou concentrada no gráfico apresentado anteriormente.

Essa análise é útil porque permite verificar, por outro caminho, se o modelo está realmente utilizando variáveis relevantes para o problema. No contexto educacional, isso ajuda a evitar interpretações superficiais e torna a discussão mais alinhada ao fenômeno analisado, permitindo compreender melhor quais fatores estão mais associados à aprovação dos candidatos.

  ```python


              precision    recall  f1-score   support

           0      0.959     0.738     0.834     33115
           1      0.227     0.708     0.344      3594

    accuracy                          0.735     36709
   macro avg      0.593     0.723     0.589     36709
weighted avg      0.887     0.735     0.786     36709
  ```

Também foram realizados testes com SMOTE para lidar com o desbalanceamento das classes. O SMOTE cria amostras sintéticas da classe minoritária no conjunto de treino, buscando reduzir o viés do modelo em favor da classe majoritária.

A saída do relatório de classificação do modelo com SMOTE mostrou accuracy de 0,735. Para a classe 0, referente aos não aprovados, o modelo apresentou precision de 0,959, recall de 0,738 e F1-score de 0,834. Para a classe 1, referente aos aprovados, o modelo apresentou precision de 0,227, recall de 0,708 e F1-score de 0,344.

Esses resultados indicam que o SMOTE aumentou a capacidade do modelo de identificar aprovados, já que o recall da classe 1 chegou a 0,708. Isso significa que o modelo passou a encontrar uma proporção maior dos candidatos aprovados. Apesar disso, a precision caiu bastante, ficando em 0,227 para a classe positiva. Na prática, o modelo passou a classificar mais candidatos como aprovados, mas muitos desses casos eram falsos positivos.

Esse comportamento mostra que o balanceamento artificial melhorou a sensibilidade para a classe minoritária, mas prejudicou a confiabilidade das previsões positivas e reduziu o desempenho geral. Por isso, o SMOTE não se mostrou a melhor alternativa para o objetivo principal do projeto, já que aumentou o recall dos aprovados, mas gerou muitos erros ao prever aprovação.


```text
================================================================================
1) BRIER POR CLASSE (menor = melhor)
================================================================================

Modelo: Base
  Classe 0: Brier = 0.042078
  Classe 1: Brier = 0.042078

Modelo: Calibrado (sigmoid)
  Classe 0: Brier = 0.042403
  Classe 1: Brier = 0.042403

Modelo: Calibrado (isotonic)
  Classe 0: Brier = 0.040899
  Classe 1: Brier = 0.040899

Tabela Brier consolidada:
```

| Classe |   Base | Calibrado (isotonic) | Calibrado (sigmoid) |
| -----: | -----: | -------------------: | ------------------: |
|      0 | 0.0421 |               0.0409 |              0.0424 |
|      1 | 0.0421 |               0.0409 |              0.0424 |

O Brier Score foi utilizado para avaliar a qualidade das probabilidades previstas pelos modelos. Diferente da acurácia, que mede apenas se a classe final foi acertada ou não, o Brier avalia se as probabilidades atribuídas pelo modelo estão próximas dos resultados reais. Como essa métrica mede erro, valores menores indicam melhor calibração.

Na comparação realizada, o modelo base apresentou Brier Score de 0,0421 para as duas classes. O modelo calibrado com sigmoid apresentou resultado levemente pior, com Brier Score de 0,0424. Já o modelo calibrado com isotonic apresentou o melhor desempenho, com Brier Score de 0,0409.

Esse resultado indica que a calibração isotônica produziu probabilidades mais confiáveis em relação ao modelo base e ao modelo calibrado com sigmoid. Como o problema é binário, os valores aparecem iguais para as classes 0 e 1, pois a probabilidade de uma classe é complementar à probabilidade da outra. Assim, a análise do Brier reforça que o modelo calibrado com isotonic foi o mais adequado quando o objetivo é interpretar a probabilidade de aprovação de forma mais precisa.



<img width="790" height="390" alt="curvadecalibracao" src="https://github.com/user-attachments/assets/2458a246-3c40-4a71-9a0c-7ab5aecb67eb" />
<img width="790" height="390" alt="curvadecalibracao2" src="https://github.com/user-attachments/assets/01b60bed-1ae3-4887-8027-60d79b97cb11" />

A calibração do modelo também foi avaliada por meio das curvas de calibração para as classes 0 e 1. Esses gráficos comparam as probabilidades previstas pelo modelo com a frequência observada dos resultados reais. Em um modelo bem calibrado, os pontos tendem a se aproximar da linha de referência y = x, que representa a calibração perfeita.

Na curva da Classe 0, observa-se que as probabilidades previstas ficaram relativamente próximas da linha ideal, indicando boa correspondência entre confiança prevista e frequência observada. Isso sugere que, para essa classe, o modelo apresenta comportamento probabilístico consistente.

Na curva da Classe 1, a relação entre probabilidades previstas e frequência observada também acompanha de forma razoável a linha de calibração perfeita, embora com pequenas diferenças em alguns intervalos. Esse resultado mostra que o modelo consegue produzir probabilidades úteis para distinguir os candidatos dessa classe, ainda que a calibração não seja absolutamente perfeita.

A análise dessas curvas é importante porque complementa as métricas de classificação tradicionais. Enquanto medidas como accuracy, precision, recall e F1-score mostram o desempenho na decisão final, a curva de calibração revela se as probabilidades produzidas pelo modelo podem ser interpretadas com confiança. Em um problema como o do SISU, isso é relevante porque não interessa apenas saber se o candidato foi classificado corretamente, mas também se a probabilidade atribuída à previsão reflete adequadamente o comportamento real dos dados.

## Discussão dos resultados obtidos

Os resultados obtidos mostram que K-Means e XGBoost contribuíram de formas diferentes para a compreensão do problema. O K-Means foi mais útil na etapa exploratória, ajudando a identificar agrupamentos, perfis de concorrência e padrões relacionados às notas e aos pesos das disciplinas. O XGBoost apresentou melhor desempenho na tarefa preditiva, sendo mais adequado para estimar a aprovação dos candidatos a partir das variáveis disponíveis no dataset.

O K-Means mostrou que os dados possuem alguma estrutura interna, mas essa estrutura não é completamente separada. O melhor resultado ocorreu com dois clusters, com Silhouette Score em torno de 0,34, indicando separação moderada. Esse valor sugere que os candidatos compartilham características semelhantes em várias regiões do espaço de dados, especialmente quando estão próximos da nota de corte ou disputam cursos com regras parecidas de concorrência.

Essa sobreposição é coerente com o funcionamento do SISU. Dois candidatos podem ter desempenhos próximos no ENEM, mas resultados finais diferentes dependendo do curso escolhido, da instituição, da modalidade de concorrência, da quantidade de vagas, da nota de corte e da classificação final. Por isso, a aprovação não se organiza como uma fronteira simples. O K-Means consegue revelar perfis e estruturas internas, mas não deve ser usado isoladamente para prever a situação final do candidato.

A análise dos gráficos de centroides, distâncias e PCA reforçou essa leitura. O modelo não separou apenas aprovados e não aprovados. Ele identificou perfis de concorrência influenciados pelas notas, pelos pesos das disciplinas e pelas regras adotadas pelos cursos. Em especial, o Biplot PCA mostrou que a separação dos clusters foi influenciada tanto pelo desempenho acadêmico quanto pelas regras de ponderação das notas. Isso ajuda a explicar por que os agrupamentos encontrados fazem sentido do ponto de vista estrutural, mas não funcionam como uma classificação direta de aprovação.

O XGBoost apresentou resultados mais fortes para o objetivo de previsão. A acurácia de aproximadamente 94%, o ROC AUC de 0,9582 e o F1-score de 0,70 para a classe dos aprovados indicam que o modelo conseguiu aprender relações relevantes entre as variáveis e a aprovação. Mesmo com o desbalanceamento, o modelo não ficou restrito à classe majoritária, conseguindo identificar parte importante dos candidatos aprovados.

A principal dificuldade do XGBoost foi reconhecer todos os aprovados. O recall de 0,68 para a classe positiva mostra que ainda houve falsos negativos, ou seja, candidatos aprovados que foram classificados como não aprovados. Esse ponto precisa ser destacado porque a classe dos aprovados é justamente uma das mais importantes para a pesquisa. Ainda assim, o resultado é consistente para um problema real, desbalanceado e com múltiplos fatores envolvidos.

A análise da matriz de confusão reforça essa interpretação. O modelo apresentou alto desempenho na identificação dos não aprovados, mas ainda cometeu erros relevantes na classe dos aprovados. Em termos práticos, isso significa que o XGBoost conseguiu capturar bem o padrão dominante da base, mas encontrou maior dificuldade em identificar todos os casos positivos. Esse comportamento é esperado em um conjunto no qual a classe de aprovados representa uma parcela menor dos registros.

A análise de importância das features também contribuiu para interpretar o comportamento do modelo supervisionado. Embora o gráfico presente no notebook esteja identificado como “Importância das Features - Random Forest”, ele foi utilizado como apoio interpretativo na etapa supervisionada, permitindo observar quais variáveis tiveram maior peso relativo na separação entre aprovados e não aprovados. Esse tipo de análise torna o modelo mais explicável, pois permite relacionar o desempenho obtido com variáveis coerentes com a lógica do SISU, como notas, nota de corte, classificação, curso, instituição, quantidade de vagas e modalidade de concorrência.

A comparação com SMOTE mostrou que o balanceamento artificial nem sempre melhora o modelo de forma prática. A saída do relatório de classificação do modelo com SMOTE indicou aumento do recall da classe positiva, chegando a 0,708, mas também mostrou queda expressiva da precision, que ficou em 0,227 para os aprovados. Isso significa que o modelo passou a identificar uma proporção maior de candidatos aprovados, mas também passou a classificar muitos candidatos como aprovados quando, na realidade, não pertenciam a essa classe.

Esse resultado mostra que melhorar uma métrica isolada pode prejudicar a utilidade geral do modelo. Em aplicações ligadas à análise educacional, não basta aumentar a identificação dos aprovados se o modelo passa a gerar muitos falsos positivos. Para o objetivo do projeto, o SMOTE foi importante como experimento comparativo, mas não se mostrou a alternativa mais equilibrada, pois reduziu a precisão e piorou o desempenho global.

A calibração trouxe outra perspectiva para a avaliação do XGBoost. As curvas de calibração das classes 0 e 1 permitiram observar se as probabilidades previstas pelo modelo estavam próximas da frequência observada nos dados reais. Essa análise é importante porque vai além da decisão final de classe. Um modelo pode acertar muitas previsões, mas ainda assim produzir probabilidades pouco confiáveis. No contexto do SISU, probabilidades bem calibradas são relevantes porque ajudam a interpretar melhor o grau de confiança associado à previsão de aprovação.

A análise do Brier Score por classe reforçou essa leitura. O modelo base apresentou Brier Score de 0,0421, enquanto o modelo calibrado com sigmoid apresentou valor levemente maior, de 0,0424. O modelo calibrado com isotonic apresentou o melhor resultado, com Brier Score de 0,0409. Como o Brier mede erro probabilístico, valores menores indicam melhor calibração. Assim, a calibração isotônica se destacou por produzir probabilidades mais confiáveis.

A tabela final de comparação entre Base, SMOTE e Calibrado mostrou que cada abordagem teve vantagens e limitações. O modelo base apresentou bom equilíbrio geral de classificação, com Accuracy = 0,9425, Balanced Accuracy = 0,7907, Macro-F1 = 0,8203, LogLoss = 0,1446 e ECE = 0,0107. O modelo com SMOTE teve desempenho global inferior, com Accuracy = 0,7350, Balanced Accuracy = 0,7230, Macro-F1 = 0,5887, LogLoss = 0,5666 e ECE = 0,1132. Já o modelo calibrado com isotonic apresentou Accuracy = 0,9443, Balanced Accuracy = 0,7877, Macro-F1 = 0,8227, LogLoss = 0,1378 e ECE = 0,0056.

Esses resultados indicam que o modelo base foi uma boa escolha quando o objetivo principal é classificação geral. O SMOTE pode ser considerado quando a prioridade é aumentar a sensibilidade para a classe minoritária, mas seu custo em precisão e desempenho global foi alto. A calibração isotônica se mostrou mais adequada quando o foco é obter probabilidades mais confiáveis, já que apresentou melhor desempenho em métricas probabilísticas como Brier Score, LogLoss e ECE.

Comparando os dois modelos principais, o XGBoost foi superior para responder diretamente à questão de pesquisa relacionada à previsão da aprovação e à análise dos fatores associados ao resultado final. O K-Means, mesmo sem atingir separação forte entre os grupos, foi importante para revelar a estrutura dos dados e mostrar que existem perfis diferentes de concorrência. Dessa forma, os modelos se complementam: um ajuda a entender os padrões internos, enquanto o outro permite prever a classe de interesse.

Os resultados também reforçam que a aprovação no SISU é um fenômeno multifatorial. A nota do candidato é importante, mas não atua sozinha. A nota de corte, a classificação, o curso escolhido, a instituição, o turno, a quantidade de vagas, a modalidade de concorrência e os pesos das disciplinas influenciam diretamente o resultado final. Essa complexidade explica por que o K-Means encontrou separação apenas moderada e por que o XGBoost, mesmo com alto desempenho, ainda teve dificuldade em capturar todos os aprovados.

Com isso, os objetivos do projeto foram atendidos. O K-Means permitiu identificar perfis e compreender a estrutura interna dos dados. O XGBoost demonstrou boa capacidade de previsão, especialmente quando avaliado por métricas adequadas ao desbalanceamento. A análise conjunta dos modelos oferece uma visão mais completa da competitividade dos cursos no SISU 2023/1 em Minas Gerais, combinando exploração, interpretação, previsão e avaliação da confiabilidade probabilística.

# Revisão do pipeline de pesquisa e análise de dados

Nesta etapa, os alunos devem revisar o pipeline de pesquisa e análise de dados proposto na Etapa 03, avaliando criticamente cada uma de suas etapas, fluxos e decisões. O objetivo agora é identificar possíveis ajustes, melhorias ou generalizações que tornem o pipeline mais abrangente e adaptável, de forma que ele seja capaz de representar qualquer processo de construção de sistemas de aprendizado de máquina – independentemente da área de aplicação, tipo de dado ou técnica utilizada.

Lembre-se de que um pipeline bem estruturado deve contemplar, de forma flexível e modular, as principais fases da pesquisa e experimentação em ciência de dados e aprendizado de máquina, incluindo (mas não se limitando a): formulação do problema, coleta e preparação dos dados, análise exploratória, definição de métricas, seleção e validação de modelos, interpretação dos resultados e documentação.

O resultado desta etapa deverá ser um pipeline revisado e justificado, acompanhado de uma breve descrição das alterações realizadas e dos motivos que levaram a cada mudança.

## Observações importantes

Todas as tarefas realizadas nesta etapa deverão ser registradas em formato de texto junto com suas explicações de forma a apresentar os códigos desenvolvidos e também, o código deverá ser incluído, na íntegra, na pasta "src".
