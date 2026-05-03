# Preparação dos dados

Nesta etapa, deverão ser descritas todas as técnicas utilizadas para pré-processamento/tratamento dos dados.

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

Avalie quais etapas são importantes para o contexto dos dados que você está trabalhando, pois a qualidade dos dados e a eficácia do pré-processamento desempenham um papel fundamental no sucesso de modelo(s) de aprendizado de máquina. É importante entender o contexto do problema e ajustar as etapas de preparação de dados de acordo com as necessidades específicas de cada projeto.

# Descrição do modelo
## Escolha do Algoritmo
Para a resolução do problema da classificação da aprovação de candidados no SISU 2023, foi utilizado o algoritmo Random Forest, pertencente à família de métodos de aprendizado supervisionado baseados em ensemble. 

## Justificativa da Escolha
A escolha do Random Forest se deu por sua adequação às características do conjunto de dados ao tipo de problema abordado. O dataset apresenta
* grande volume de registros
* predominância de variáveis numéricas
* possíveis relações não lineares entre os atributos

Diante disso, o Random Forest se destaca por:
* capturar relações complexas sem necessidade de transformações avançadas
* apresenta alta robustez a ruídos e outliers
* reduz o risco de overfiting em comparação a árvores de decisão (quando usadas de maneira isolada)
* permite a análise da importância das variáveis

Além disso, o problema apresenta desbalanceamento entre as classes (aprovados e não aprovados), o que reforça a escolha de um modelo que permita ajustes específicos para lidar com essa característica.

**Nesta seção, conhecendo os dados e de posse dos dados preparados, é hora de descrever o algoritmo de aprendizado de máquina selecionado para a construção do modelo proposto. Inclua informações abrangentes sobre o algoritmo implementado, aborde conceitos fundamentais, princípios de funcionamento, vantagens/limitações e justifique a escolha do algoritmo utilizado.**

Explore aspectos específicos, como o ajuste dos parâmetros livres do algoritmo. Lembre-se de experimentar parâmetros diferentes e principalmente, de registrar os testes realizados com diferentes parâmetros que servirão para justificar as escolhas realizadas.

# Avaliação dos modelos criados

## Métricas utilizadas
  O modelo Random Forest foi configurado com 800 árvores (**_n_estimators=800_**), utilizando o critério **_entropy_** para avaliação das divisões. Não foi definida profundidade máxima para as árvores (**_max_depth=None_**), permitindo maior capacidade de aprendizado. 
  
  Os parâmetros **_min_samples_split=5_** e **_min_samples_leaf=2_** foram utilizados para reduzir divisões excessivas e melhorar a generalização do modelo. Além disso, foi aplicado **_class_weight='balanced_subsample'_** para auxiliar no tratamento do desbalanceamento entre as classes.
  
  O parâmetro **_ramdom_state=42_** foi definido para garantir reprodutibilidade dos resultados.

  Foi realizado ajuste do limiar de decisão (**_threshold_**) aplicado às probabilidades previstas pelo modelo. Foi adotado o limiar de **0.35**, buscando melhorar o equilíbrio entre o _precision_ e _recall_, especialmente na  identificação da classe minoritária (_candidatos aprovados_).

  O modelo apresentou **acurácia geral de 91%** na classificação dos candidatos. Para a classe de **não aprovados (0)**, foram obtidos **_precision_ de 96%, _recall_ de 95% e _F1-score_ de 95%. Já para a classe de **aprovados (1)**, o modelo alcançou _precision_ de 55%, _recall_ de 61% e _F1-score_ de 58%.

  Os resultados demonstram **bom desempenho geral e maior equilíbrio** na identificação da classe minoritária, indicando melhora na capacidade do modelo em reconhecer.


**_--Nesta seção, as métricas utilizadas para avaliar os modelos desenvolvidos deverão ser apresentadas (p. ex.: acurácia, precisão, recall, F1-Score, MSE etc.). A escolha de cada métrica deverá ser justificada, pois esta escolha é essencial para avaliar de forma mais assertiva a qualidade do modelo construído.--_**

## Discussão dos resultados obtidos

  Os resultados obtidos demonstram que o modelo Random Forest apresentou bom desempenho na tarefa de classificação da aprovação dos candidatos. A acurácia geral indica alta taxa de acertos nas previsões realizadas pelo modelo.

  Entretanto, considerando o desbalanceamento existente entre as classes, a análise não pode ser feita apenas com base na acurácia. Por este motivo, métricas como _precision_, _recall_ e _F1-score_ foram auxiliadoras para avaliar de forma mais adequada a qualidade do modelo.

  Para a classe de **não aprovados (0)**, o modelo apresentou desempenho elevado em todas as métricas, demonstrando grande capacidade de identificar candidatos não aprovados.

  Sobre a classe de **aprovados (1)**, os resultados medianos, com _precision_ de 55%, _recall_ de 61% e _F1-score_ de 58%. O valor do _recall_ indica que o modelo conseguiu identificar uma parcela significativa dos candidados, de fato, aprovados, reduzindo a quantidade de falsos negativos. Esse aspecto é importante no contexto do problema, pois demonstra a sensibilidade do modelo à classe minoritária. 

  O ajuste do limiar de decisão também contribuiu para melhorar o equilíbrio entre as métricas, permitindo aumentar a capacidade do modelo em reconhecer candidados aprovados, mesmo com um impacto moderado na precisão das previsões positivas.

  Na validação cruzada (**_k-fold_**), foram obtidos resultados de aproximadamente 76,22%, 76,71%, 64,79%, 76,19% e 86,64%, resultando em média de **76,11%**. Os resultados demonstram desempenho moderado entre os _folds_, embora ainda exista variação entre algumas divisões dos dados. A queda observada em determinados _folds_ pode estar relacionada ao desbalanceamento das classes e à dificuldade do modelo em igualar todos os subconjuntos avaliados. A utilização da métrica **_F1_weighted_** permitiu considerar o desempenho global do modelo levando em conta a proporção das classes no conjunto de dados, proporcionando uma avaliação mais equilibrada em relação ao desbalanceamento existente.

  Na análise de **Importância das Variáveis (_Feature Importance_)** foi utilizada para identificar quais variáveis exerceram maior influência nas decisões do modelo. Os resultados demonstraram qua a variável **CODIGO_CURSO** apresentou a maior importância no processo de classificação, indicando forte relação entre o curso escolhido e a probabilidade de aprovação dos candidatos. Em seguida, destacaram-se as variáveis relacionadas ao desempenho dos candidados (_notas_), principalmente:
  - **NOTA_M**
  - **NOTA_CH**
  - **NOTA_CN**
  - **NOTA_L**
  - **NOTA_R**
  - 
Logo, reforça que o desempenho nas provas é importante na previsão da aprovação.

Ainda falando sobre a Importância das Variáveis, **GRAU_T** e **TIPO_MOD_CONCORRENCIA_T** apresentam menor influência, contrubuindo de forma complementar para a classificação, mas não sendo o alvo principal no quesito **aprovação**. De forma geral, a análise evidencia que tanto fatores acadêmicos quando características relacionadas ao curso exercem impacto na previsão realizada pelo modelo.

- **Gráfico: Importância das Variáveis**
  <img width="867" height="384" alt="image" src="https://github.com/user-attachments/assets/4d1cd641-df7b-46aa-90d4-b3c4e8d15059" />


Ainda para melhorar a confiança das probabilidades previstas no modelo, foram aplicadas técnicas de calibração utilizando os métodos _sigmoid_ e _isotonic_. A avaliação foi realizada por meio de _Brier Score_, no qual valores menores indidcam melhor calibração das probabilidades. Os resultados mostraram que o método _isotonic_ apresentou melhor desempenho, com _Brier Score_ de aproximadamente **0,0550**, superior ao modelo base e ao método _sigmoid_. De forma geral, a calibração contribuiu para tornar as probabilidades mais consistentes com os resultados reais observados.

- **Curva de Calibração - Classe 0**
  <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/6182c9ed-fe29-4a69-8003-91d8a3fce773" />

- **Curva de Calibração - Classe 1**
  <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/c0c4e7fe-5c92-4f2b-8d32-beb6f01eb556" />







  _calibração_

**_Nesta seção, discuta os resultados obtidos pelo modelo construído, no contexto prático em que os dados se inserem, promovendo uma compreensão abrangente e aprofundada da qualidade dele. Lembre-se de relacionar os resultados obtidos por cada uma das métricas ao problema identificado, a questão de pesquisa levantada e estabelecer relação com os objetivos previamente propostos. 
É fundamental compreender o que cada uma das métricas "conta" sobre a qualidade do modelo desenvolvido._**

# Pipeline de pesquisa e análise de dados

Em pesquisa e experimentação em sistemas de informação, um pipeline de pesquisa e análise de dados refere-se a um conjunto organizado de processos e etapas que um profissional segue para realizar a coleta, preparação, análise e interpretação de dados durante a fase de pesquisa e desenvolvimento de modelos. Esse pipeline é essencial para extrair _insights_ significativos, entender a natureza dos dados e, construir modelos de aprendizado de máquina eficazes. 

## Observações importantes

Todas as tarefas realizadas nesta etapa deverão ser registradas em formato de texto junto com suas explicações de forma a apresentar os códigos desenvolvidos e também, o código deverá ser incluído, na íntegra, na pasta "src".
