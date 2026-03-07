# Introdução

O projeto EduMap investiga a aplicação de técnicas de Ciência de Dados e _Machine Learning_ na análise de dados do Sistema de Seleção Unificada (SISU), sistema utilizado por instituições públicas brasileiras para selecionar candidatos ao ensino superior com base nas notas obtidas no Exame Nacional do Ensino Médio (ENEM). Entre as informações mais relevantes desse processo está a **nota de corte**, que representa a menor pontuação necessária para que um candidato permaneça entre os classificados dentro do número de vagas de determinado curso e instituição.

O objetivo do projeto é desenvolver e avaliar modelos de aprendizado de máquina capazes de analisar dados históricos do SISU — especificamente da edição 2023/1 — para estimar a nota de corte associada a diferentes cursos e instituições. A investigação envolve etapas de preparação e análise do conjunto de dados, identificação de padrões relevantes e treinamento de modelos capazes de produzir estimativas com base nas características presentes no dataset.

Como resultado, o EduMap busca demonstrar o potencial das técnicas de aprendizado de máquina na análise de dados educacionais e na identificação de padrões em processos seletivos complexos. Além disso, pretende-se disponibilizar uma aplicação que permita aos usuários inserir informações sobre cursos e instituições para obter uma estimativa da nota de corte prevista pelos modelos desenvolvidos, tendo como público-alvo estudantes interessados em compreender melhor a dinâmica de concorrência do SISU e pessoas interessadas em aplicações práticas de análise de dados.


<!-- Texto descritivo introdutório apresentando a visão geral do projeto a ser desenvolvido considerando o contexto em que ele se insere, os objetivos gerais, a justificativa e o público-alvo do projeto.

Nos últimos anos, o processo de ingresso no ensino superior brasileiro tem sido amplamente influenciado pelos resultados do Exame Nacional do Ensino Médio (ENEM), utilizado como principal mecanismo de seleção para diversas instituições públicas por meio do Sistema de Seleção Unificada (SISU). Esse sistema centraliza a oferta de vagas em cursos de graduação em instituições públicas de todo o país e utiliza as notas obtidas pelos candidatos no ENEM para realizar a classificação e seleção dos estudantes.

O SISU reúne um grande volume de informações sobre candidatos, cursos, instituições e desempenho nas provas do ENEM, formando bases de dados ricas e complexas que possibilitam diferentes tipos de análises educacionais. Entre os dados disponíveis estão informações sobre cursos ofertados, quantidade de vagas, modalidade de concorrência, notas obtidas nas áreas avaliadas pelo ENEM, classificação dos candidatos, notas de corte e resultados de aprovação e matrícula.

A análise desses dados permite compreender melhor o comportamento do processo seletivo, bem como identificar padrões relacionados ao desempenho dos candidatos e à competitividade dos cursos. Nesse contexto, técnicas de ciência de dados e aprendizado de máquina podem ser aplicadas para explorar o conjunto de dados e desenvolver modelos capazes de identificar padrões e realizar previsões relacionadas ao processo de seleção.

Diante disso, este projeto propõe a análise de um dataset contendo informações sobre candidatos participantes do processo seletivo de cursos de graduação, com o objetivo de explorar os dados e experimentar modelos de aprendizado de máquina capazes de auxiliar na compreensão de padrões presentes no processo de seleção e classificação dos candidatos. -->

## Problema

O projeto EduMap investiga a possibilidade de prever a nota de corte de cursos ofertados no processo seletivo do Sistema de Seleção Unificada (SISU) a partir da análise de dados históricos do programa. A nota de corte corresponde à menor pontuação necessária para que um candidato permaneça entre os classificados dentro do número de vagas disponíveis em determinado curso, universidade e modalidade de concorrência. Como essa nota é resultado da interação entre diversos fatores — como número de vagas, instituição, curso, turno e comportamento dos candidatos durante o processo seletivo — ela apresenta variações que não podem ser determinadas apenas por regras simples, tornando-se um problema adequado para investigação com técnicas de Ciência de Dados e _Machine Learning_.

No contexto do acesso ao ensino superior público brasileiro, a nota de corte é amplamente utilizada pelos candidatos como referência para avaliar suas chances de aprovação em cursos e instituições durante o período de inscrições do SISU. No entanto, essas notas são atualizadas ao longo do processo seletivo e refletem o comportamento coletivo dos candidatos, o que torna sua estimativa antecipada uma tarefa complexa.

A partir do conjunto de dados do SISU referente à Chamada Regular da edição de 2023/1, este projeto busca analisar padrões presentes nas ofertas de cursos e nas notas registradas, investigando como esses dados podem ser utilizados para construir modelos capazes de estimar a nota de corte associada a diferentes combinações de cursos e instituições. Dessa forma, o trabalho explora o uso de métodos de análise de dados aplicados a um contexto educacional real, contribuindo para a compreensão dos fatores relacionados à competitividade no acesso ao ensino superior gratuito no Brasil.

<!-- Nesta seção, você deve apresentar o problema que a sua investigação/experimentação busca resolver. Por exemplo, caso o _dataset_ selecionado, seja um _dataset_ que contenha uma série temporal com o preço de diversas ações da bolsa de valores, o problema pode estar relacionado a dificuldade em saber a melhor hora (hora certa??) de comprar ou então, de executar a venda de uma determinada ação.

Descreva ainda o contexto em que essa aplicação será usada, se houver: empresa parceira, tecnologias etc. Novamente, descreva apenas o que de fato existir, pois ainda não é a hora de apresentar requisitos  detalhados ou projetos.

**Atenção:** Nesta etapa, apresente apenas informações reais e já confirmadas. Não antecipe requisitos técnicos detalhados, funcionalidades específicas ou desenhos de projeto — essa parte será desenvolvida posteriormente.

O ingresso em instituições públicas de ensino superior no Brasil é altamente competitivo e depende diretamente do desempenho dos candidatos no ENEM e da concorrência existente em cada curso. Um dos principais indicadores desse processo é a nota de corte, que representa a menor pontuação necessária para que um candidato seja classificado dentro do número de vagas disponíveis.

Entretanto, a nota de corte não é um valor fixo e pode variar significativamente de acordo com diversos fatores, como o número de candidatos concorrendo a uma vaga, a distribuição das notas obtidas no ENEM, a quantidade de vagas disponíveis e a modalidade de concorrência adotada no processo seletivo.

Para candidatos, gestores educacionais e pesquisadores, pode ser difícil compreender ou prever o comportamento dessas notas ao longo do processo seletivo, especialmente em cursos com grande número de concorrentes. Dessa forma, surge a necessidade de utilizar métodos analíticos capazes de identificar padrões nos dados históricos e auxiliar na compreensão do comportamento das notas e da classificação dos candidatos.

Neste contexto, a aplicação de técnicas de ciência de dados e aprendizado de máquina pode contribuir para a análise desse fenômeno, permitindo explorar relações entre variáveis como notas nas diferentes áreas do ENEM, pesos atribuídos pelos cursos, quantidade de vagas e desempenho dos candidatos no processo seletivo.

> **Links Úteis**:
> - [Objetivos, Problema de pesquisa e Justificativa](https://medium.com/@versioparole/objetivos-problema-de-pesquisa-e-justificativa-c98c8233b9c3)
> - [Matriz Certezas, Suposições e Dúvidas](https://medium.com/educa%C3%A7%C3%A3o-fora-da-caixa/matriz-certezas-suposi%C3%A7%C3%B5es-e-d%C3%BAvidas-fa2263633655)
> - [Brainstorming](https://www.euax.com.br/2018/09/brainstorming/) -->

## Questão de pesquisa

A partir do problema apresentado, a seguinte questão de pesquisa orienta o desenvolvimento deste trabalho:

É possível utilizar técnicas de Ciência de Dados e _Machine Learning_ para estimar a nota de corte de cursos ofertados no Sistema de Seleção Unificada (SISU) a partir de características relacionadas ao curso, à instituição, modalidade, turno, região do campus e à oferta de vagas presentes em dados históricos do processo seletivo?

<!-- A questão de pesquisa é o ponto de partida e a base orientadora de todo o trabalho a ser desenvolvido. Ela deve estar diretamente alinhada ao problema identificado e expressar, de forma clara, o que se deseja investigar ou comprovar.

O papel da questão de pesquisa é guiar todas as etapas do projeto — desde a definição da metodologia até a análise e interpretação dos resultados. Ao término da investigação ou experimentação, o objetivo é que seja possível responder a essa questão de forma fundamentada, utilizando evidências obtidas ao longo do processo.

**Dica:** Formule a questão de pesquisa de forma específica e objetiva, evitando perguntas muito amplas ou genéricas. Pergunte-se: "Ao final do trabalho, minha pesquisa terá condições de responder claramente a essa pergunta?"

A partir do problema apresentado, a seguinte questão de pesquisa orienta o desenvolvimento deste trabalho:
É possível utilizar técnicas de aprendizado de máquina para identificar padrões nos dados do processo seletivo do ensino superior e auxiliar na previsão ou análise do comportamento da nota de corte e da classificação dos candidatos?
Essa questão busca investigar se modelos de aprendizado de máquina podem extrair conhecimento relevante a partir do conjunto de dados disponível e contribuir para uma melhor compreensão do processo de seleção universitária.

> **Links Úteis**:
> - [Questão de pesquisa](https://www.enago.com.br/academy/how-to-develop-good-research-question-types-examples/)
> - [Problema de pesquisa](https://blog.even3.com.br/problema-de-pesquisa/) -->


## Objetivos preliminares

### Objetivo Geral

Desenvolver, experimentar e avaliar modelos adequados de aprendizado de máquina aplicados ao conjunto de dados do Sistema de Seleção Unificada (SISU) 2023/1, com o objetivo de investigar a capacidade desses modelos em prever a nota de corte de cursos ofertados no processo seletivo a partir de características relacionadas aos cursos, às instituições e à oferta de vagas. O projeto busca analisar padrões presentes nos dados históricos do sistema e verificar em que medida técnicas de _Machine Learning_ podem contribuir para estimar a nota de corte em diferentes combinações de cursos e instituições no contexto do processo seletivo.

### Objetivos Específicos

- Realizar a coleta e preparação do conjunto de dados do Sistema de Seleção Unificada (SISU), incluindo etapas de limpeza, organização e tratamento das informações disponíveis.
 
- Explorar e analisar os dados por meio de técnicas de Ciência de Dados, buscando identificar padrões e relações relevantes entre as variáveis presentes no dataset.
 
- Selecionar e treinar três diferentes modelos de aprendizado de máquina adequados ao problema de previsão da nota de corte.
  
- Avaliar e comparar o desempenho dos três modelos treinados, analisando sua capacidade de estimar a nota de corte com base nos dados utilizados.
 
- Implantar e disponibilizar uma solução baseada no modelo desenvolvido, permitindo que usuários informem dados relevantes — como curso e instituição — para obter uma estimativa da nota de corte prevista, demonstrando a aplicação prática de um dos modelos desenvolvidos no projeto.


<!-- Nesta seção, você deve apresentar os objetivos preliminares do trabalho, deixando claro que o objetivo geral é experimentar modelos de aprendizado de máquina adequados para solucionar o problema descrito anteriormente.

Além do objetivo geral, é importante definir pelo menos dois objetivos específicos, que direcionem a investigação de acordo com o foco que o grupo pretende adotar. Esses objetivos específicos podem envolver: 
* Explorar um determinado tipo de modelagem ou técnica de aprendizado de máquina;
* Comparar diferentes abordagens para resolver o mesmo problema;
* Aplicar o modelo em um cenário real ou simulado;
* Otimizar parâmetros para melhorar métricas específicas de desempenho.

Exemplo:
Objetivo específico 1: Predizer a tendência de alta, estabilidade ou queda de uma determinada ação em uma janela de tempo definida.
Objetivo específico 2: Estimar o valor exato da ação ao final do período analisado.

Objetivo Geral

Explorar e experimentar modelos de aprendizado de máquina aplicados ao dataset do processo seletivo do ensino superior brasileiro, com o objetivo de identificar padrões e analisar fatores relacionados ao desempenho e classificação dos candidatos.

Objetivos Específicos
- Analisar e explorar o conjunto de dados, identificando as principais variáveis e relações existentes entre elas.
- Aplicar técnicas de pré-processamento e preparação de dados para possibilitar o uso em modelos de aprendizado de máquina.
- Experimentar diferentes algoritmos de aprendizado de máquina para analisar padrões relacionados à classificação e às notas dos candidatos.
- Avaliar o desempenho dos modelos utilizando métricas adequadas de avaliação.

**Importante:** À medida que a pesquisa/experimentação avança, os objetivos podem ser ajustados ou refinados. Mantenha essa seção atualizada no repositório para refletir o andamento e as novas decisões do projeto.
 
> **Links Úteis**:
> - [Objetivo geral e objetivo específico: como fazer e quais verbos utilizar](https://blog.mettzer.com/diferenca-entre-objetivo-geral-e-objetivo-especifico/) -->

## Justificativa

O acesso ao ensino superior é um tema de grande relevância social e educacional no Brasil. Segundo dados do Instituto Nacional de Estudos e Pesquisas Educacionais Anísio Teixeira (INEP), milhões de estudantes realizam o ENEM todos os anos com o objetivo de ingressar em instituições de ensino superior públicas ou privadas.

O Sistema de Seleção Unificada (SISU) representa um dos principais mecanismos de acesso ao ensino superior público no país, reunindo informações sobre milhares de cursos e candidatos em cada edição do processo seletivo. Esse grande volume de dados constitui uma importante fonte para análises acadêmicas e para o desenvolvimento de soluções baseadas em ciência de dados.

A utilização de técnicas de análise de dados e aprendizado de máquina nesse contexto pode contribuir para a compreensão do comportamento do processo seletivo, permitindo identificar padrões relacionados ao desempenho dos candidatos, à concorrência entre cursos e às variações das notas de corte.

Além disso, o estudo desse tipo de base de dados também possui relevância acadêmica, pois permite aplicar conceitos de mineração de dados, aprendizado de máquina e análise estatística em um contexto real e de grande impacto social. Dessa forma, o projeto contribui tanto para o desenvolvimento de competências técnicas na área de ciência de dados quanto para a análise de um fenômeno relevante no sistema educacional brasileiro.

Nesta seção, apresente a importância e a motivação para trabalhar com o conjunto de dados escolhido. Explique por que esse dataset é relevante e como ele se conecta ao problema identificado anteriormente.

Indique:
* Razões para a escolha dos objetivos específicos – Justifique por que decidiu aprofundar sua investigação nessas metas, relacionando-as ao potencial de solução ou melhoria para o problema.
* Relevância do estudo do problema – Mostre a importância de compreender e tratar a questão apresentada, tanto no contexto acadêmico quanto no profissional.
* Impacto social, econômico ou ambiental – Descreva como o problema afeta a sociedade ou um setor específico, buscando sempre quantificar o impacto por meio de dados reais.

**Importante:**
* Apresente números, estatísticas e informações concretas, citando as fontes (relatórios, artigos científicos, portais oficiais etc.).
* Mantenha a objetividade e a clareza, evitando argumentos genéricos.
* Construa um texto coeso que conecte o problema, os objetivos e a relevância do trabalho.

> **Links Úteis**:
> - [Como montar a justificativa](https://guiadamonografia.com.br/como-montar-justificativa-do-tcc/)

## Público-Alvo
Os resultados deste projeto podem beneficiar diferentes grupos interessados na análise de dados educacionais e no processo de seleção para o ensino superior.
Entre os principais públicos interessados estão:
- Pesquisadores e estudantes da área de ciência de dados, que podem utilizar o estudo como referência para aplicações de técnicas de aprendizado de máquina em bases de dados educacionais.
- Estudantes que participam do ENEM e do SISU, que podem se beneficiar de análises que auxiliem na compreensão da competitividade de determinados cursos.
- Gestores educacionais e instituições de ensino, que podem utilizar análises baseadas em dados para compreender melhor o comportamento do processo seletivo e apoiar decisões relacionadas à oferta de cursos e vagas.
- Professores e pesquisadores da área de educação, interessados em compreender padrões de desempenho e seleção no ensino superior.


Nesta seção, descreva quem poderá se beneficiar com a sua investigação, apresentando os diferentes perfis de pessoas ou grupos impactados.

O objetivo aqui não é definir clientes específicos ou papéis exatos dentro da aplicação, mas sim compreender o perfil dos usuários e partes interessadas. Para isso, considere:
* Conhecimentos prévios relacionados ao domínio do problema e ao uso de tecnologia;
* Nível de familiaridade com recursos digitais e possíveis barreiras de uso;
* Contexto profissional e hierárquico, quando aplicável (ex.: nível de decisão, responsabilidades, área de atuação);
* Necessidades e expectativas que podem ser atendidas pelo projeto.

**Dica:** Seja objetivo e baseie suas descrições em informações reais ou plausíveis para o contexto escolhido. Isso ajudará a manter o foco no desenvolvimento de soluções relevantes e aplicáveis.

> **Links Úteis**:
> - [Público-alvo](https://blog.hotmart.com/pt-br/publico-alvo/)
> - [Como definir o público alvo](https://exame.com/pme/5-dicas-essenciais-para-definir-o-publico-alvo-do-seu-negocio/)
> - [Público-alvo: o que é, tipos, como definir seu público e exemplos](https://klickpages.com.br/blog/publico-alvo-o-que-e/)
> - [Qual a diferença entre público-alvo e persona?](https://rockcontent.com/blog/diferenca-publico-alvo-e-persona/)

## Estado da arte

Estado da Arte
A aplicação de técnicas de ciência de dados e aprendizado de máquina em dados educacionais tem crescido significativamente nos últimos anos. Pesquisas nessa área buscam identificar padrões em dados de desempenho acadêmico, prever resultados educacionais e apoiar processos de tomada de decisão em instituições de ensino. No contexto do ensino superior, diversos estudos utilizam dados de exames padronizados e históricos acadêmicos para prever desempenho, evasão, classificação ou probabilidade de aprovação em processos seletivos.

A seguir são apresentados estudos relevantes da literatura que abordam problemas semelhantes ao investigado neste projeto.

Estudo 1
Predicting Student Performance Using Machine Learning Techniques
Problema e contexto
O estudo investigou a aplicação de algoritmos de aprendizado de máquina para prever o desempenho de estudantes a partir de dados educacionais. O objetivo foi identificar fatores que influenciam o sucesso acadêmico e construir modelos capazes de prever resultados educacionais.
Dados (dataset)
Foi utilizado um dataset educacional contendo informações acadêmicas de estudantes, incluindo notas, características demográficas e dados institucionais. O conjunto de dados passou por etapas de pré-processamento, incluindo limpeza de dados, tratamento de valores ausentes e normalização de variáveis.
Abordagem/algoritmos
Foram testados diversos algoritmos de aprendizado de máquina, incluindo:
- Decision Tree
- Random Forest
- Support Vector Machine (SVM)
- Naive Bayes
- Métricas de avaliação

Os modelos foram avaliados utilizando:
- Acurácia
- Precisão
- Recall
- F1-score

Essas métricas foram escolhidas para avaliar a capacidade dos modelos em classificar corretamente o desempenho dos estudantes.

Resultados
O algoritmo Random Forest apresentou melhor desempenho entre os modelos testados, alcançando níveis de acurácia superiores a 80%. O estudo concluiu que técnicas de aprendizado de máquina podem ser eficazes para identificar padrões em dados educacionais e auxiliar na previsão de desempenho acadêmico.

Estudo 2
Educational Data Mining: A Review of Applications and Techniques
Problema e contexto
Este estudo apresenta uma revisão das principais aplicações de mineração de dados educacionais, com foco na análise de desempenho de estudantes e na previsão de resultados acadêmicos.
Dados (dataset)
A revisão analisa diversos conjuntos de dados educacionais provenientes de sistemas acadêmicos, plataformas de ensino e exames educacionais.
Abordagem/algoritmos
Os principais algoritmos identificados na literatura incluem:
Random Forest
Logistic Regression
Neural Networks
K-means Clustering
Métricas de avaliação

As métricas mais utilizadas nos estudos analisados foram:
- Accuracy
- AUC (Area Under the Curve)
- RMSE
- MAE

Resultados
A revisão mostra que técnicas de aprendizado de máquina têm sido amplamente utilizadas para prever desempenho acadêmico, evasão e sucesso educacional, destacando o potencial dessas abordagens para apoiar decisões educacionais.

Estudo 3
Predicting Academic Performance with Machine Learning
Problema e contexto
Este estudo buscou prever o desempenho acadêmico de estudantes utilizando modelos de aprendizado de máquina baseados em dados históricos de desempenho educacional.
Dados (dataset)
O dataset utilizado continha informações sobre:
- notas dos estudantes
- características demográficas
- histórico acadêmico
Foram aplicadas técnicas de pré-processamento, como normalização e remoção de valores inconsistentes.
Abordagem/algoritmos
Os algoritmos utilizados foram:
Logistic Regression
Random Forest
Gradient Boosting
Métricas de avaliação

Os modelos foram avaliados utilizando:
- Accuracy
- Precision
- Recall
- ROC-AUC

Resultados
Os modelos baseados em árvores de decisão, especialmente Random Forest e Gradient Boosting, apresentaram melhor desempenho na previsão do desempenho acadêmico.

Estudo 4
Machine Learning Approaches for Predicting University Admission
Problema e contexto
Este estudo investigou a aplicação de modelos de aprendizado de máquina para prever a admissão de candidatos em universidades com base em dados de desempenho acadêmico e exames padronizados.
Dados (dataset)
O dataset incluiu informações sobre:
- notas em exames padronizados
- histórico acadêmico
- características demográficas
- Os dados foram submetidos a etapas de limpeza e normalização.

Abordagem/algoritmos
Os algoritmos utilizados foram:
- Linear Regression
- Random Forest
- Artificial Neural Networks
- Métricas de avaliação

As métricas utilizadas incluíram:
- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)

Resultados
Os resultados indicaram que modelos baseados em aprendizado de máquina podem prever com razoável precisão as chances de admissão de candidatos em processos seletivos universitários.

Estudo 5
Learning Analytics in Higher Education: A Review
Problema e contexto
O estudo analisa aplicações de Learning Analytics no ensino superior, com foco na utilização de dados educacionais para melhorar processos de ensino, aprendizagem e tomada de decisão.
Dados (dataset)
Os datasets analisados incluem registros acadêmicos, dados de desempenho de estudantes e informações institucionais.
Abordagem/algoritmos
As técnicas mais utilizadas incluem:
- Data Mining
- Machine Learning
- Statistical Modeling
- Métricas de avaliação

As métricas variam conforme o objetivo do estudo, incluindo:
- Accuracy
- F1-score
- RMSE

Resultados
O estudo conclui que o uso de análise de dados educacionais tem grande potencial para apoiar instituições de ensino na melhoria do desempenho acadêmico e na identificação de padrões educacionais.

Síntese Crítica da Literatura

A análise dos estudos apresentados revela um consenso na literatura sobre o potencial das técnicas de aprendizado de máquina para analisar e prever fenômenos relacionados ao desempenho acadêmico e aos processos educacionais. Diversos trabalhos demonstram que algoritmos como Random Forest, Gradient Boosting e redes neurais apresentam bons resultados na identificação de padrões em dados educacionais, especialmente quando utilizados em conjuntos de dados históricos que contêm informações sobre desempenho acadêmico e características dos estudantes.

Apesar desse consenso, existem divergências em relação às técnicas mais adequadas para cada tipo de problema. Alguns estudos destacam o bom desempenho de modelos baseados em árvores de decisão, enquanto outros enfatizam a eficácia de redes neurais ou modelos estatísticos tradicionais. Essas diferenças geralmente estão relacionadas às características dos datasets utilizados, como tamanho da base de dados, quantidade de variáveis disponíveis e qualidade dos dados.

Além disso, a literatura ainda apresenta algumas lacunas importantes. Muitos estudos utilizam datasets limitados ou restritos a instituições específicas, o que dificulta a generalização dos resultados. Também há desafios relacionados à qualidade dos dados, presença de valores ausentes e possíveis vieses nos modelos. Outra lacuna relevante está na análise de processos seletivos nacionais em larga escala, como o caso do ENEM e do SISU, que envolvem grande volume de dados e múltiplos fatores que influenciam o processo de seleção.

Nesse contexto, o presente projeto se alinha às pesquisas existentes ao aplicar técnicas de aprendizado de máquina em um dataset relacionado ao processo de ingresso no ensino superior brasileiro. Ao explorar dados de candidatos, cursos e notas obtidas no ENEM, o trabalho busca identificar padrões e analisar fatores relacionados à classificação e às notas de corte, contribuindo para o avanço das análises de dados educacionais no contexto brasileiro.



Nesta seção, descreva abordagens da literatura que tratam problemas semelhantes ao seu. Seu objetivo é documentar métodos, dados, métricas e resultados.

### O que levantar (mínimo 5 trabalhos)
Para **cada estudo encontrado** aderente à temática do grupo, registre de forma objetiva:
* Problema e contexto: que problema o trabalho buscou resolver e em qual domínio/cenário foi aplicado.
* Dados (dataset): origem, tamanho, período, variáveis/atributos, pré-processamentos relevantes (faltantes, balanceamento, normalização).
* Abordagem/algoritmos: algoritmos utilizados e parâmetros principais (quando informados).
* Métricas de avaliação: quais e por quê (ex.: Acurácia, F1, AUC, RMSE, MAE, etc.).
* Resultados: principais números, comparações internas, limitações citadas e conclusões.

* Texto-síntese crítico (2–4 parágrafos) respondendo:
- O que os estudos concordam? Onde divergem?
- Quais lacunas permanecem (dados, métricas, cenários, limitações técnicas/éticas)?
- Como seu projeto se alinha aos estudos identificados?

**Dica:** Prefira artigos dos últimos 5 anos ou referências clássicas indispensáveis.

### Ferramentas inteligentes permitidas
Você pode utilizar: Perplexity, SciSpace, Elicit, Research Rabbit, Litmaps.
Use-as para descoberta, organização e triagem de literatura. 

**Atenção:** 
* Sempre acesse a fonte original (PDF/artigo) antes de citar; verifique números e conclusões.
* Registre DOI/URL oficial e dados bibliográficos completos.
* Evite “alucinações” das ferramentas: desconfie de referências sem DOI ou que você não consiga localizar oficialmente.
* Use as ferramentas inteligentes para mapear redes de citação (Research Rabbit), mapas de tópicos (Litmaps), filtrar por período e gerar resumos iniciais (Perplexity/SciSpace/Elicit).
* Leia os trabalhos mais promissores e descarte estudos fora de escopo.

> **Links Úteis**:
> - [Google Scholar](https://scholar.google.com/)
> - [IEEE Xplore](https://ieeexplore.ieee.org/Xplore/home.jsp)
> - [Science Direct](https://www.sciencedirect.com/)
> - [ACM Digital Library](https://dl.acm.org/)

# Descrição do _dataset_ selecionado

## Identificação e origem

- Nome: 2023 - Relatório SISU - Chamada Regular 1/2023
- Link de acesso: https://dadosabertos.mec.gov.br/sisu/item/258-2023-relatorio-sisu-chamada-regular-1-2023
- Fonte: Portal de Dados Abertos do Ministério da Educação
- Licença de uso: Open Data Commons Open Database License (ODbL)

## Visão geral

O dataset reúne informações sobre o processo seletivo do **Sistema de Seleção Unificada (SISU)** referente à **primeira edição do ano de 2023**.
Ele reúne dados sobre:
- Candidatos participantes do processo seletivo
- Instituições de ensino superior
- Cursos ofertados
- Notas do ENEM
- Pesos das áreas de conhecimento
- Classificação dos candidatos
- Aprovação e matrícula

Esse dataset possibilita diversas análises relacionadas ao processo de acesso ao ensino superior no Brasil.

O SISU é atualmente um dos principais mecanismos de acesso ao ensino superior público brasileiro, é um sistema informatizado do Ministério da Educação que utiliza as notas do **ENEM (Exame Nacional do Ensino Médio)** para selecionar estudantes para vagas em instituições públicas de ensino superior.


### Estrutura geral do dataset

O conjunto de dados contém registros relacionados ao processo seletivo do SISU, incluindo:
- Registros de **inscrições em cursos ofertados pelo SISU**
- Informações sobre **instituições de ensino superior**
- Dados sobre **cursos, vagas e modalidades de concorrência**
- Informações sobre **candidatos e suas notas no ENEM**
- Dados sobre **classificação e resultado da seleção**

### Estrutura dos dados

Cada linha do dataset representa uma inscrição de um candidato em um curso específico dentro do processo do SISU. 
Como cada candidato pode escolher **duas opções de curso**, é possível que um mesmo candidato apareça mais de uma vez no dataset.

### Conteúdo principal

A partir desse conjunto de dados, é possivel realizar diversas análises relacionadas ao processo seletivo do ensino superior, tais como:
- Prever nota de corte de um curso
- Prever o nível de concorrência de um curso
- Prever quais fatores mais influenciam a nota de corte
- Prever a modalidade de concorrência escolhido
- Distribuição desigual de oportuniades
- Relação entre oferta e competição
- Prever a nota de corte do curso 
- Impacto das cotas no acesso ao ensino superior
- Diferenças de nota entre cursos e regiões

## Atributos 

|       Atributo        |                   Descrição                    |  Tipo   | Unidade |               Exemplos               |
| :-------------------: | :--------------------------------------------: | :-----: | :-----: | :----------------------------------: |
|          ANO          |            Ano do processo seletivo            | Inteiro |   Ano   |                 2023                 |
|        EDICAO         |        Número da edição do SISU no ano         | Inteiro | Número  |                  1                   |
|         ETAPA         |       Identificador da etapa do processo       | Inteiro | Número  |                  4                   |
|       DS_ETAPA        |    Descrição da etapa do processo seletivo     | String  |    -    |           CHAMADA REGULAR            |
|      CODIGO_IES       | Código identificador da instituição de ensino  | Inteiro | Código  |                 1234                 |
|       NOME_IES        |     Nome da instituição de ensino superior     | String  |    -    | Universidade Federal de Minas Gerais |
|       SIGLA_IES       |              Sigla da instituição              | String  |    -    |                 UFMG                 |
|        UF_IES         |             Estado da instituição              | String  |   UF    |              MG, SP, RJ              |
|     CODIGO_CAMPUS     |         Código identificador do campus         | Inteiro | Código  |                 567                  |
|      NOME_CAMPUS      |         Nome do campus da instituição          | String  |    -    |           Campus Pampulha            |
|   MUNICIPIO_CAMPUS    |    Município onde o campus está localizado     | String  |    -    |            Belo Horizonte            |
|      NOME_CURSO       |             Nome do curso ofertado             | String  |    -    |      Medicina, Engenharia Civil      |
|         GRAU          |           Tipo de formação do curso            | String  |    -    |      Bacharelado, Licenciatura       |
|         TURNO         |                 Turno do curso                 | String  |    -    |          Matutino, Noturno           |
|   MOD_CONCORRENCIA    |           Modalidade de concorrência           | String  |    -    |      Ampla concorrência, Cotas       |
| QT_VAGAS_CONCORRENCIA | Número de vagas disponíveis para a modalidade  | Inteiro |  Vagas  |                  20                  |
|        NOTA_L         |           Nota em Linguagens no ENEM           |  Float  | Pontos  |                640.5                 |
|        NOTA_CH        |            Nota em Ciências Humanas            |  Float  | Pontos  |                610.2                 |
|        NOTA_CN        |          Nota em Ciências da Natureza          |  Float  | Pontos  |                590.8                 |
|        NOTA_M         |               Nota em Matemática               |  Float  | Pontos  |                720.3                 |
|        NOTA_R         |                Nota na Redação                 |  Float  | Pontos  |                 800                  |
|    NOTA_CANDIDATO     |   Nota final do candidato considerando pesos   |  Float  | Pontos  |                705.4                 |
|      NOTA_CORTE       |  Nota mínima necessária para entrar no curso   |  Float  | Pontos  |                785.6                 |
|     CLASSIFICACAO     | Posição do candidato na lista de classificação | Inteiro | Posição |                  12                  |
|       APROVADO        |       Indica se o candidato foi aprovado       | String  |    -    |                S / N                 |

## Qualidade dos dados 
Durante a análise preliminar do dataset, alguns aspectos relacionados à qualidade dos dados devem ser considerados.

**Valores faltantes:** Alguns atributos podem apresentar valores ausentes, principalmente em campos relacionados a pesos das provas ou notas mínimas, pois nem todos os cursos utilizam esses critérios.

**Inconsistências:** Podem ocorrer pequenas variações em campos categóricos, como nomes de cursos, municípios ou modalidades de concorrência, além de diferenças de capitalização ou abreviações.

**Duplicatas:** Não foram identificadas duplicatas diretas. Um mesmo candidato pode aparecer mais de uma vez no dataset devido às duas opções de curso permitidas no SISU.

**Outliers:** Podem existir notas muito altas ou muito baixas em comparação com a média, principalmente em cursos altamente concorridos, sendo necessário avaliar esses casos durante a análise exploratória.

# Canvas analítico


<img width="1220" height="864" alt="Captura de tela 2026-03-07 172718" src="https://github.com/user-attachments/assets/f9b65cb7-b195-449e-938c-71557cbafaa8" />


<!--
> **Links Úteis**:
> - [Modelo do Canvas Analítico](https://github.com/ICEI-PUC-Minas-PMV-SI/PesquisaExperimentacao-Template/blob/main/help/Software-Analtics-Canvas-v1.0.pdf) -->

# Vídeo de apresentação da Etapa 01

Nesta etapa, o grupo deverá produzir um vídeo de 5 a 8 minutos apresentando o trabalho realizado, no qual cada integrante deve dizer seu nome e apresentar uma parte do conteúdo desenvolvido, garantindo que todos participem ativamente da gravação. A ausência de participação de qualquer membro resultará em penalização na nota final desta etapa. Recomenda-se que o grupo elabore previamente um roteiro para organizar a ordem das falas, distribuir o tempo de forma equilibrada e assegurar que todos os tópicos relevantes sejam apresentados de maneira clara e objetiva.

# Referências

- BRASIL. Ministério da Educação. **2023 – Relatório SISU – Chamada Regular 1/2023**. Portal Dados Abertos do MEC, 2023. Disponível em: https://dadosabertos.mec.gov.br/sisu/item/258-2023-relatorio-sisu-chamada-regular-1-2023. Acesso em: 7 mar. 2026.
  
- ENAGO ACADEMY. **Como desenvolver uma pergunta de pesquisa relevante: tipos e exemplos**. Enago Academy, 2022. Disponível em: https://www.enago.com/academy/how-to-develop-good-research-question-types-examples/. Acesso em: 7 mar. 2026.
  
- TUMELERO, Naína. **Aprenda como fazer o objetivo geral e os objetivos específicos do seu trabalho**. Blog Mettzer, 2017. Atualizado em: 7 mar. 2025. Disponível em: https://blog.mettzer.com/diferenca-entre-objetivo-geral-e-objetivo-especifico/. Acesso em: 7 mar. 2026.
  
- PONTIFÍCIA UNIVERSIDADE CATÓLICA DE MINAS GERAIS. Sistema Integrado de Bibliotecas. **Orientações para elaboração de citações e referências**: conforme as NBRs 10520:2023 e 6023:2025, da Associação Brasileira de Normas Técnicas (ABNT). 6. ed. Belo Horizonte: PUC Minas, 2025. Disponível em: https://www.pucminas.br/biblioteca. Acesso em: 7 mar. 2026.
 
<!-- Inclua todas as referências (livros, artigos, sites, etc) utilizados no desenvolvimento do trabalho utilizando o padrão ABNT.

> **Links Úteis**:
> - [Padrão ABNT PUC Minas](https://portal.pucminas.br/biblioteca/index_padrao.php?pagina=5886) -->
