# Conhecendo os dados

Este trabalho tem como objetivo realizar uma 1ª análise exploratória de dados (EDA), a Engenharia de Dados e, em seguida, uma 2ª análise exploratória de dados a partir de um dataset do SISU 2023/1, com foco no estado de Minas Gerais. A análise busca compreender a estrutura dos dados, identificar padrões, detectar possíveis outliers e analisar relações entre variáveis que influenciam a competitividade dos cursos.

O projeto está inserido no contexto do sistema EduMap, que visa analisar notas de corte e o nível de concorrência em cursos superiores, utilizando técnicas de ciência de dados e aprendizado de máquina.

## 2. Conhecendo os Dados
### 2.1 Descrição da Base de Dados

O dataset utilizado foi obtido a partir do portal de dados abertos do MEC:

- Base: SISU 2023 – Chamada Regular;
- Fonte: dadosabertos.mec.gov.br;
- Registros totais: 1.048.575;
- Recorte utilizado: Minas Gerais (~196.095 registros).

Cada linha representa um candidato participante do processo seletivo, contendo informações como:

- Ano e edição do SISU
- Código e nome da instituição
- Curso e turno
- Nota do candidato
- Classificação
- Situação (aprovado, lista de espera, etc.)
- 
### 2.2 Análise Descritiva
#### 2.2.1 Medidas de Tendência Central
Foram utilizadas funções do Pandas para análise estatística descritiva:

`df_dataset.describe()`

A partir disso, foi possível observar:

- A média das notas indica o nível geral de desempenho dos candidatos
- A mediana ajuda a entender a distribuição central sem influência de outliers
- Diferenças entre média e mediana sugerem assimetria nos dados
  
#### 2.2.2 Medidas de Dispersão
A análise também considerou:
- Desvio padrão → variabilidade das notas
- Intervalo entre valores mínimos e máximos
- Possíveis dispersões elevadas indicando heterogeneidade dos dados

Essas medidas mostram que há grande variação nas notas e classificações, o que é esperado em processos seletivos amplos como o SISU.

### 2.3 Análise Visual dos Dados

Foram utilizados gráficos com Matplotlib e Seaborn, incluindo:
- Histogramas → distribuição das notas
- Boxplots → identificação de outliers
- Gráficos de dispersão → relação entre variáveis

Exemplo de código utilizado:

`sns.histplot(df_dataset['NOTA'], kde=True)
plt.show()`

Essas visualizações ajudaram a:
- Identificar distribuição assimétrica das notas
- Detectar valores extremos (outliers)
- Compreender padrões de concentração de dados
  
### 2.4 Detecção de Outliers

A identificação de outliers foi realizada principalmente com:
- Boxplots
- Análise de dispersão

Observações:
- Foram identificados valores extremos em notas e classificações
- Esses valores podem representar candidatos com desempenho muito acima ou abaixo da média
- A presença de outliers pode impactar modelos de machine learning

### 2.5 Análise de Relações entre Variáveis

Foram analisadas relações entre variáveis utilizando:
- Correlação
- Gráficos de dispersão
- Técnicas estatísticas

Exemplo de código:
`df_dataset.corr()`

Também foram utilizadas técnicas mais avançadas como:
- VIF (Variance Inflation Factor) para multicolinearidade
- Análise com bibliotecas como statsmodels

Principais observações:
- Algumas variáveis apresentam correlação com a nota de corte
- Relações entre classificação e aprovação são evidentes
- Existem dependências entre variáveis relacionadas ao desempenho do candidato

### 2.6 Trechos de Código Relevantes
Leitura dos dados:
`df_dataset = pd.read_csv(path, encoding='latin1', sep=';')`

Inspeção inicial:
`df_dataset.head()
df_dataset.info()`

Bibliotecas utilizadas:
`import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt`

Modelagem inicial (contexto do projeto):
`from sklearn.ensemble import RandomForestClassifier`

## 3. Descrição dos Achados

A partir da análise exploratória, foram identificados os seguintes pontos relevantes:
- Centralidade dos dados: As notas apresentam concentração em uma faixa intermediária, com leve assimetria.
- Dispersão: Existe alta variabilidade nas notas e classificações, indicando diversidade no desempenho dos candidatos.
- Outliers: Foram identificados valores extremos que podem influenciar análises estatísticas e modelos preditivos.
- Correlação entre variáveis:
  - Relação entre nota e classificação (quanto maior a nota, melhor a posição)
  - Variáveis relacionadas ao curso e instituição influenciam a competitividade
  - Algumas correlações são moderadas, indicando influência parcial entre variáveis
- Balanceamento de dados: Observou-se possível desbalanceamento nas classes (ex: aprovados vs não aprovados), o que motivou o uso de técnicas como SMOTE posteriormente.

<!-- Nesta seção, deverá ser registrada uma detalhada análise descritiva e exploratória sobre a base de dados selecionada na Etapa 1 com o objetivo de compreender a estrutura dos dados, detectar eventuais _outliers_ e também, avaliar/detectar as relações existentes entre as variáveis analisadas.

Para isso, sugere-se que sejam utilizados cálculos de medidas de tendência central, como média, mediana e moda, para entender a centralidade dos dados; sejam exploradas medidas de dispersão como desvio padrão e intervalos interquartil para avaliar a variabilidade dos dados; sejam utilizados gráficos descritivos como histogramas e box plots, para representar visualmente as características essenciais dos dados, pois essas visualizações podem facilitar a identificação de padrões e anomalias; sejam analisadas as relações entre as variáveis por meio de análise de correlação, gráficos de dispersões, mapas de calor, entre outras técnicas. 

Inclua nesta seção, gráficos, tabelas, trechos de código e demais artefatos que você considere relevantes para entender os dados com os quais você irá trabalhar.  Além disso, inclua e comente os trechos de código mais relevantes desenvolvidos para realizar suas análises. Na pasta "src", inclua o código fonte completo.

## Descrição dos achados

A partir da análise descrita e exploratória realizada, descreva todos os achados considerados relevantes para o contexto em que o trabalho se insere. Por exemplo: com relação à centralidade dos dados algo chamou a atenção? Foi possível identificar correlação entre os atributos? Que tipo de correlação (forte, fraca, moderada)? -->

## 4. Ferramentas utilizadas

As seguintes ferramentas foram utilizadas na análise:

| Ferramenta | Tipo | Finalidade | Principais Aplicações |
|------------|------|------------|----------------------|
| Matplotlib | Biblioteca base | Criação de gráficos estáticos | Gráficos de linha, barras, histogramas, dispersão |
| Seaborn    | Biblioteca estatística | Visualização avançada e estética | Heatmaps, pairplot, regressão, distribuição |
| Pandas     | Manipulação de dados | Estruturação e análise de dados | DataFrames, leitura de CSV, gráficos rápidos |
| Plotly     | Biblioteca interativa | Gráficos interativos e dashboards | Dashboards, zoom, gráficos dinâmicos |
| Google Colab | Ambiente de execução | Desenvolvimento e execução de código | Análise de dados, visualização e compartilhamento |


## 5. Considerações Finais

A análise exploratória foi essencial para compreender a estrutura do dataset e identificar padrões importantes. Foi possível detectar:
- Variabilidade significativa nos dados
- Presença de outliers
- Relações entre variáveis relevantes para modelagem
Essas descobertas são fundamentais para as próximas etapas do projeto, especialmente na construção de modelos preditivos mais precisos.

<!-- 🐍 Linguagem
Python
📚 Bibliotecas
Pandas: manipulação e análise de dados
NumPy: cálculos numéricos
Matplotlib / Seaborn: visualização de dados
Statsmodels: análise estatística
Scikit-learn: modelagem e machine learning
Imbalanced-learn (SMOTE): balanceamento de classes
SHAP: interpretação de modelos
💻 Ambiente
Google Colab -->

<!-- Nesta seção, deverá ser registrada uma detalhada análise descritiva e exploratória sobre a base de dados selecionada na Etapa 1 com o objetivo de compreender a estrutura dos dados, detectar eventuais _outliers_ e também, avaliar/detectar as relações existentes entre as variáveis analisadas.

Para isso, sugere-se que sejam utilizados cálculos de medidas de tendência central, como média, mediana e moda, para entender a centralidade dos dados; sejam exploradas medidas de dispersão como desvio padrão e intervalos interquartil para avaliar a variabilidade dos dados; sejam utilizados gráficos descritivos como histogramas e box plots, para representar visualmente as características essenciais dos dados, pois essas visualizações podem facilitar a identificação de padrões e anomalias; sejam analisadas as relações entre as variáveis por meio de análise de correlação, gráficos de dispersões, mapas de calor, entre outras técnicas. 

Inclua nesta seção, gráficos, tabelas, trechos de código e demais artefatos que você considere relevantes para entender os dados com os quais você irá trabalhar.  Além disso, inclua e comente os trechos de código mais relevantes desenvolvidos para realizar suas análises. Na pasta "src", inclua o código fonte completo.

## Descrição dos achados

A partir da análise descrita e exploratória realizada, descreva todos os achados considerados relevantes para o contexto em que o trabalho se insere. Por exemplo: com relação à centralidade dos dados algo chamou a atenção? Foi possível identificar correlação entre os atributos? Que tipo de correlação (forte, fraca, moderada)?  -->

## Ferramentas utilizadas

As principais ferramentas utilizadas nesta etapa do projeto estão apresentadas a seguir, acompanhadas de suas características iniciais. Embora existam diversas opções para análise de dados, optou-se pelo uso do ambiente Google Colab, no qual foram empregadas bibliotecas específicas conforme descrito.

Toda a programação foi desenvolvida utilizando a linguagem Python, escolhida por sua versatilidade, simplicidade e alta eficiência. O Python se destaca no contexto de ciência de dados por possuir um amplo ecossistema de bibliotecas científicas, estatísticas e matemáticas desenvolvidas por terceiros, o que amplia significativamente suas capacidades.

A utilização dessas bibliotecas permite a execução de análises mais avançadas, manipulação eficiente de grandes volumes de dados e a construção de visualizações robustas, tornando o Python uma das principais linguagens utilizadas em projetos acadêmicos e profissionais na área de análise de dados.

| Ferramenta | Tipo | Finalidade | Principais Aplicações |
|------------|------|------------|----------------------|
| Matplotlib | Biblioteca base | Criação de gráficos estáticos | Gráficos de linha, barras, histogramas, dispersão |
| Seaborn    | Biblioteca estatística | Visualização avançada e estética | Heatmaps, pairplot, regressão, distribuição |
| Pandas     | Manipulação de dados | Estruturação e análise de dados | DataFrames, leitura de CSV, gráficos rápidos |
| Plotly     | Biblioteca interativa | Gráficos interativos e dashboards | Dashboards, zoom, gráficos dinâmicos |
| Google Colab | Ambiente de execução | Desenvolvimento e execução de código | Análise de dados, visualização e compartilhamento |
