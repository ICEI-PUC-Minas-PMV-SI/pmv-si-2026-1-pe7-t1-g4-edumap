# Introdução

O projeto EduMap está inserido no contexto da crescente utilização de dados educacionais para apoiar a tomada de decisão e ampliar a compreensão sobre o acesso ao ensino superior no Brasil. O Sistema de Seleção Unificada (SISU), como principal mecanismo de ingresso em instituições públicas, gera um volume significativo de dados que refletem a dinâmica da concorrência entre cursos, instituições e modalidades de acesso. Nesse cenário, o avanço das técnicas de Ciência de Dados e de aprendizado de máquina possibilita a análise mais aprofundada dessas informações, contribuindo para a identificação de padrões e relações que não são facilmente perceptíveis por métodos tradicionais.

Diante desse contexto, o objetivo geral consiste em investigar os fatores que influenciam a competitividade dos cursos no SISU 2023/1, analisando como variáveis como instituição, curso, turno, modalidade de concorrência, localização e número de vagas se relacionam com a nota de corte, a classificação e a aprovação dos candidatos. Para isso, o projeto envolve etapas de tratamento de dados, análise estatística e aplicação de modelos interpretáveis de aprendizado de máquina.

A relevância do estudo está na ampliação do entendimento sobre os determinantes da competitividade no SISU, contribuindo para análises mais embasadas e transparentes. O público-alvo inclui estudantes, pesquisadores e gestores educacionais interessados em compreender melhor a dinâmica de acesso ao ensino superior público.


<!-- Texto descritivo introdutório apresentando a visão geral do projeto a ser desenvolvido considerando o contexto em que ele se insere, os objetivos gerais, a justificativa e o público-alvo do projeto.

Nos últimos anos, o processo de ingresso no ensino superior brasileiro tem sido amplamente influenciado pelos resultados do Exame Nacional do Ensino Médio (ENEM), utilizado como principal mecanismo de seleção para diversas instituições públicas por meio do Sistema de Seleção Unificada (SISU). Esse sistema centraliza a oferta de vagas em cursos de graduação em instituições públicas de todo o país e utiliza as notas obtidas pelos candidatos no ENEM para realizar a classificação e seleção dos estudantes.

O SISU reúne um grande volume de informações sobre candidatos, cursos, instituições e desempenho nas provas do ENEM, formando bases de dados ricas e complexas que possibilitam diferentes tipos de análises educacionais. Entre os dados disponíveis estão informações sobre cursos ofertados, quantidade de vagas, modalidade de concorrência, notas obtidas nas áreas avaliadas pelo ENEM, classificação dos candidatos, notas de corte e resultados de aprovação e matrícula.

A análise desses dados permite compreender melhor o comportamento do processo seletivo, bem como identificar padrões relacionados ao desempenho dos candidatos e à competitividade dos cursos. Nesse contexto, técnicas de ciência de dados e aprendizado de máquina podem ser aplicadas para explorar o conjunto de dados e desenvolver modelos capazes de identificar padrões e realizar previsões relacionadas ao processo de seleção.

Diante disso, este projeto propõe a análise de um dataset contendo informações sobre candidatos participantes do processo seletivo de cursos de graduação, com o objetivo de explorar os dados e experimentar modelos de aprendizado de máquina capazes de auxiliar na compreensão de padrões presentes no processo de seleção e classificação dos candidatos. -->

## Problema

A elevada competitividade observada nos processos seletivos do Sistema de Seleção Unificada (SISU) evidencia a complexidade dos fatores que influenciam o ingresso no ensino superior público. Elementos como instituição, curso, turno, modalidade de concorrência, localização e número de vagas interagem de forma não trivial, impactando diretamente indicadores como nota de corte, classificação e aprovação dos candidatos. No entanto, essas relações nem sempre são explícitas ou facilmente interpretáveis, o que dificulta uma compreensão aprofundada dos determinantes da competitividade entre os diferentes cursos ofertados.

Além disso, embora exista grande volume de dados disponibilizados pelo SISU, sua utilização ainda é, em muitos casos, limitada a análises descritivas superficiais, sem o devido aproveitamento de técnicas mais robustas de Ciência de Dados e aprendizado de máquina. A ausência de abordagens analíticas mais avançadas compromete a identificação de padrões relevantes e a extração de conhecimento útil, tanto para candidatos quanto para gestores educacionais. Isso gera uma lacuna no entendimento sobre como diferentes variáveis contribuem, individual e conjuntamente, para os resultados do processo seletivo.

Diante desse cenário, torna-se necessário desenvolver uma abordagem sistemática que permita não apenas analisar, mas também interpretar os fatores que influenciam as notas de a competitividade dos cursos no SISU 2023/1. A aplicação de modelos interpretáveis de aprendizado de máquina, aliada a técnicas de análise exploratória e segmentação de dados, surge como uma alternativa promissora para suprir essa lacuna. Assim, o problema central deste estudo consiste em compreender, de forma estruturada e baseada em dados, quais variáveis são mais determinantes e como elas se relacionam com os resultados do processo seletivo, considerando também as potencialidades e limitações do uso de Inteligência Artificial nesse contexto.

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

Quais são os principais fatores que influenciam a competitividade dos cursos ofertados no SISU 2023/1 e de que forma variáveis institucionais, acadêmicas e estruturais impactam a nota de corte, a classificação e a aprovação dos candidatos, segundo a análise por técnicas de Ciência de Dados e aprendizado de máquina?

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

Investigar, por meio da aplicação de técnicas de Ciência de Dados e de aprendizado de máquina, os principais fatores que impactam a competitividade dos cursos ofertados no SISU 2023/1, examinando de que forma variáveis relacionadas à instituição, ao curso, ao turno, à modalidade de concorrência, à localização e à quantidade de vagas se correlacionam com a nota de corte, a classificação e a aprovação dos candidatos.

### Objetivos Específicos

- Realizar o pré-processamento e a estruturação do conjunto de dados referente ao SISU 2023/1, visando sua adequação para as etapas analíticas.
- Conduzir uma análise estatística exploratória das distribuições de notas de corte, aprovações e classificações entre cursos, instituições e modalidades de concorrência.
- Determinar os atributos mais significativos na explicação da competitividade dos cursos ofertados.
- Empregar modelos de aprendizado de máquina com foco em interpretabilidade para avaliar a influência das variáveis sobre a nota de corte e a aprovação dos candidatos.
- Executar a segmentação de cursos com características semelhantes em termos de competitividade e acesso.
- Analisar criticamente o potencial e as limitações da utilização de técnicas de Inteligência Artificial na interpretação de dados educacionais do SISU.


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

O acesso ao ensino superior constitui um dos principais fatores associados ao desenvolvimento social e econômico de um país. No Brasil, o Exame Nacional do Ensino Médio (ENEM) tornou-se o principal mecanismo de avaliação utilizado para o ingresso em instituições de ensino superior, sendo aplicado anualmente a milhões de estudantes. De acordo com os dados do Instituto Nacional de Estudos e Pesquisas Educacionais Anísio Teixeira (INEP), o ENEM contou com mais de 3,9 milhões de inscritos na edição de 2023 (INEP, 2023), demonstrando a grande relevância desse exame no contexto educacional brasileiro.

O Sistema de Seleção Unificada (SISU) foi criado com o objetivo de centralizar o processo de seleção de candidatos para instituições públicas de ensino superior, utilizando as notas obtidas no ENEM como critério de classificação. A cada edição do sistema, milhares de cursos e instituições participam do processo seletivo, gerando um grande volume de dados relacionados às características dos cursos, número de vagas ofertadas, modalidades de concorrência e desempenho dos candidatos.

Esse conjunto de dados representa uma fonte relevante para estudos acadêmicos e aplicações práticas de análise de dados. A utilização de técnicas de Ciência de Dados e aprendizado de máquina permite explorar esses dados de forma sistemática, possibilitando identificar padrões associados à competitividade dos cursos e às variações nas notas de corte observadas durante o processo seletivo.

Nesse contexto, a escolha de investigar a previsão da nota de corte por meio de técnicas de aprendizado de máquina justifica-se pelo potencial dessas abordagens em identificar relações complexas entre variáveis presentes no dataset, como curso, instituição, modalidade de concorrência, turno e número de vagas. A análise desses fatores pode contribuir para compreender melhor a dinâmica do processo seletivo e auxiliar na construção de modelos capazes de estimar a nota de corte a partir de dados históricos.

Além da relevância acadêmica, este estudo também apresenta potencial impacto social, uma vez que a compreensão do comportamento das notas de corte pode auxiliar estudantes interessados em ingressar no ensino superior a avaliar de forma mais informada suas possibilidades de aprovação em determinados cursos e instituições. Dessa forma, o projeto contribui tanto para o desenvolvimento de competências técnicas na área de Ciência de Dados quanto para a análise de um fenômeno relevante no sistema educacional brasileiro.

<!-- Nesta seção, apresente a importância e a motivação para trabalhar com o conjunto de dados escolhido. Explique por que esse dataset é relevante e como ele se conecta ao problema identificado anteriormente.

Indique:
* Razões para a escolha dos objetivos específicos – Justifique por que decidiu aprofundar sua investigação nessas metas, relacionando-as ao potencial de solução ou melhoria para o problema.
* Relevância do estudo do problema – Mostre a importância de compreender e tratar a questão apresentada, tanto no contexto acadêmico quanto no profissional.
* Impacto social, econômico ou ambiental – Descreva como o problema afeta a sociedade ou um setor específico, buscando sempre quantificar o impacto por meio de dados reais.

**Importante:**
* Apresente números, estatísticas e informações concretas, citando as fontes (relatórios, artigos científicos, portais oficiais etc.).
* Mantenha a objetividade e a clareza, evitando argumentos genéricos.
* Construa um texto coeso que conecte o problema, os objetivos e a relevância do trabalho.

> **Links Úteis**:
> - [Como montar a justificativa](https://guiadamonografia.com.br/como-montar-justificativa-do-tcc/) -->

## Público-Alvo
Os resultados deste projeto EduMap podem beneficiar diferentes grupos interessados na análise de dados educacionais e no funcionamento do processo de seleção para o ensino superior no Brasil.

Entre os principais públicos interessados estão:
- **Candidatos ao Ensino Superior:** Estudantes com domínio sobre as regras do SISU, mas com níveis variados de letramento digital. Buscam uma ferramenta simplificada que converta dados complexos em estimativas compreensíveis para auxiliar na tomada de decisão durante o processo seletivo, sem a necessidade de conhecimentos em Ciência de Dados.
- **Comunidade Acadêmica e Técnica:** Pesquisadores e estudantes de áreas como Ciência de Dados e Educação. Possuem alta familiaridade com recursos tecnológicos e buscam no projeto uma referência metodológica sobre o uso de Machine Learning aplicado a bases de dados governamentais abertas.
- **Gestores e Analistas Educacionais:** Profissionais de instituições de ensino ou órgãos públicos que atuam no planejamento de vagas e políticas de acesso. Possuem interesse técnico na identificação de padrões de competitividade e comportamento regional das notas de corte para subsidiar decisões estratégicas.

<!-- Nesta seção, descreva quem poderá se beneficiar com a sua investigação, apresentando os diferentes perfis de pessoas ou grupos impactados.

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
> - [Qual a diferença entre público-alvo e persona?](https://rockcontent.com/blog/diferenca-publico-alvo-e-persona/) -->

## Estado da Arte

Nesta seção, são apresentadas abordagens da literatura que tratam problemas semelhantes ao do projeto EduMap, focando na previsão de notas ou probabilidades de admissão em contextos educacionais, utilizando técnicas de Ciência de Dados e Machine Learning. Os trabalhos selecionados envolvem a previsão de admissões universitárias, notas de exames ou acesso ao ensino superior, com base em dados históricos e variáveis acadêmicas. Foram priorizados artigos dos últimos 5 anos, com ênfase em métodos preditivos aplicados a processos seletivos.

### Trabalho 1
<details>
<summary>Prediction for University Admission using Machine Learning (CHITHRA APOORVA et al., 2020)</summary>

- **Problema e contexto:** O estudo aborda o desafio enfrentado por estudantes indianos que buscam admissão em programas de mestrado em Ciência da Computação em universidades dos EUA. Os alunos frequentemente carecem de informações precisas sobre suas chances de admissão, levando a processos ineficientes, altos custos e dependência de fontes não confiáveis. O objetivo é desenvolver o modelo UAP (University Admission Predictor) para prever as chances de admissão com base em fatores cruciais, auxiliando na tomada de decisões informadas.
- **Dados (dataset):**
  - Origem: dados coletados de fontes como Yocket, focando em perfis de estudantes indianos.
  - Tamanho: não explicitado, mas sem valores ausentes ou outliers após análise.
  - Período: não especificado.
  - Variáveis/atributos: pontuação GRE, TOEFL/IELTS, qualidade do SOP (Statement of Purpose), força do LOR (Letter of Recommendation), CGPA de graduação, experiência em pesquisa e chance de admissão (rótulo).
  - Pré-processamentos: inspeção de valores, remoção de ruído, divisão em conjuntos de treino e teste; sem imputação necessária.
- **Abordagem/algoritmos:**
  - Algoritmos utilizados: K-Nearest Neighbors (KNN), Linear Regression, Ridge Regression e Random Forest.
  - Parâmetros principais: não customizados além dos padrões; foco em regressão para prever probabilidades.
- **Métricas de avaliação:** Acurácia (accuracy), escolhida para avaliar o desempenho geral dos modelos.
- **Resultados:**
  - Acurácia média de 79%; Linear Regression superou os outros.
  - Limitações: dados limitados a estudantes indianos e poucas universidades; não considera mudanças em critérios de admissão.
  - Conclusões: O modelo auxilia estudantes a economizarem tempo e recursos, com potencial para expansão.
</details>

### Trabalho 2
<details>
<summary>Optimizing University Admissions: A Machine Learning Perspective (MAULANA et al., 2023)</summary>

 - **Problema e contexto:** O artigo aborda limitações nos processos tradicionais de admissão universitária, que falham em capturar capacidades holísticas e podem introduzir viés. Propõe o uso de Machine Learning para prever chances de admissão em programas de mestrado na UCLA, analisando padrões complexos em dados de candidatos para melhorar decisões de estudantes e instituições.
- **Dados (dataset):**
  - Origem: dataset de admissões na UCLA do Kaggle.
  - Tamanho: não explicitado, mas com estatísticas descritivas.
  - Período: não especificado.
  - Variáveis/atributos: pontuações GRE (0–340), TOEFL (0–120), classificação da universidade (1–5), SOP (1–5), LOR (1–5), GPA de graduação (0–10), experiência em pesquisa (binária) e chance de admissão (alvo, 0–1).
  - Pré-processamentos: análise exploratória com matriz de correlação e gráficos; sem detalhes específicos de limpeza.
- **Abordagem/algoritmos:**
  - Algoritmos utilizados: K-Nearest Neighbors (KNN), Random Forest, Support Vector Regression (SVR) e XGBoost.
  - Parâmetros principais: padrões das bibliotecas scikit-learn e XGBoost; sem afinação customizada.
- **Métricas de avaliação:** R-squared (R²), Root Mean Squared Error (RMSE) e Mean Absolute Error (MAE), para medir variância explicada e erros de previsão.
- **Resultados:**
  - Random Forest: R² = 0.816, RMSE = 0.005, MAE = 0.050 (melhor desempenho).
  - Importância de features: CGPA (0.80) como mais influente.
  - Limitações: dataset específico da UCLA; falta de validação em outros contextos.
  - Conclusões: Random Forest é eficaz; ênfase no desempenho acadêmico; adaptável a outras universidades.
</details>

### Trabalho 3
<details>
<summary>A Machine-Learning-Based Approach to Informing Student Admission Decisions (LIU et al., 2025)</summary>

- **Problema e contexto:** O estudo aborda desafios em decisões de admissão em programas com alto volume de candidaturas e vagas limitadas, como mestrado em Psicologia em uma universidade alemã. Abordagens tradicionais usam yields fixos, ignorando incertezas, levando a sub ou superlotação. Propõe uma abordagem baseada em Machine Learning para prever matrículas condicionais, incorporar incerteza e ajustar admissões de forma data-driven.
- **Dados (dataset):**
  - Origem: dados de um mestrado em Psicologia em universidade alemã.
  - Tamanho: ~1500 candidaturas/ano, 996 admitidos totais.
  - Período: 2017–2020.
  - Variáveis/atributos: idade, gênero, local de bacharelado, status da instituição, origem biográfica, major de bacharelado, distância de deslocamento e total de candidaturas.
  - Pré-processamentos: imputação com missForest (<5% faltantes), codificação dummy para categóricos; foco em dados da primeira rodada.
- **Abordagem/algoritmos:**
  - Algoritmos utilizados: Logistic Regression, Elastic Net, Classification Tree e Random Forest (selecionado).
  - Parâmetros principais: para Random Forest, n_estimators=100, max_depth=15/10, min_samples_split=5, min_samples_leaf=2; tuning via grid search e cross-validation.
  - Abordagem: previsão de probabilidades individuais, agregação via Poisson binomial, bootstrapping para incerteza.
- **Métricas de avaliação:** AUC, Brier Score, Mean Absolute Difference, cobertura de IC 95%, correlação rolling; para risco: P(E > SP | A), etc.
- **Resultados:**
  - Random Forest: AUC=0.84, Brier=0.15; MAE=9.05 para matrículas.
  - Reduz risco de superlotação vs. tradicional (94% para 5–20%).
  - Limitações: dados de um programa; requer total de candidaturas conhecido.
  - Conclusões: Supera métodos tradicionais; melhora eficiência.
</details>

### Trabalho 4
<details>
<summary>Machine Learning para Previsão de Acessos ao Ensino Superior (EPALANGA, 2025)</summary>

- **Problema e contexto:** A dissertação aborda a falta de ferramentas analíticas avançadas para gerenciar o acesso ao ensino superior em Portugal via Concurso Nacional de Acesso. Foca na previsão do número de candidaturas e nota de admissão do último colocado para cursos no ano seguinte, usando Machine Learning para otimizar decisões sobre vagas e estratégias.
- **Dados (dataset):**
  - Origem: site oficial da DGES.
  - Tamanho: 890.192 vagas disponíveis, 746.415 preenchidas (77.7% ocupação média).
  - Período: 2004–2024.
  - Variáveis/atributos: código de instituição, nome do curso, vagas iniciais, colocados, nota do último colocado, taxa de ocupação, ano; features derivadas como médias cumulativas e taxas de crescimento.
  - Pré-processamentos: remoção de linhas introdutórias, renomeação, conversão de tipos, imputação de faltantes com médias anuais, remoção de valores inválidos; engenharia de features temporais.
- **Abordagem/algoritmos:**
  - Algoritmos utilizados: Random Forest Regressor (principal), baselines Linear Regression e ARIMA.
  - Parâmetros principais: n_estimators=100, max_depth=15/10, min_samples_split=5, min_samples_leaf=2; tuning via grid search.
  - Abordagem: CRISP-DM; seleção de features via importância de permutação.
- **Métricas de avaliação:** MAE, R², RMSE; distribuição de erros (% <1, <2, <5), IC 99%.
- **Resultados:**
  - Random Forest (nota de admissão): MAE=1.35, R²=0.984; (colocados): MAE=2.35, R²=0.989.
  - Supera baselines.
  - Limitações: falta de dados individuais; generalização limitada.
  - Conclusões: Automatiza previsões com alta acurácia; dashboard interativo para suporte.
</details>

### Trabalho 5
<details>
<summary>Prevendo as notas do ENEM com Machine Learning (WATANABE, s.d.)</summary>

- **Problema e contexto:** O artigo aborda um desafio da Codenation para prever a nota da prova de matemática (NU_NOTA_MT) dos participantes do ENEM 2016 usando Machine Learning. O foco é criar um modelo preditivo baseado apenas no dataset train.csv, destacando análise exploratória e construção de modelo para alta acurácia.
- **Dados (dataset):**
  - Origem: desafio Codenation, microdados ENEM 2016.
  - Tamanho: não explicitado.
  - Período: 2016.
  - Variáveis/atributos: NU_NOTA_MT (alvo), NU_NOTA_CN, NU_NOTA_CH, NU_NOTA_LC, NU_NOTA_REDACAO, componentes de redação (NU_NOTA_COMP1–5), TP_PRESENCA_LC.
  - Pré-processamentos: filtro de nulos/zeros em notas chave (assumindo ausência), preenchimento de componentes com 0; padronização com StandardScaler; análise de distribuição e correlação.
- **Abordagem/algoritmos:**
  - Algoritmo utilizado: RandomForestRegressor.
  - Parâmetros principais: criterion='mae', max_depth=8, n_estimators=500, n_jobs=-1, random_state=0.
- **Métricas de avaliação:** MAE, MSE, RMSE; calculadas no conjunto de treino.
- **Resultados:**
  - Ranking 6º no desafio (score 93.86%).
  - Limitações: suposições sobre nulos podem viésar; sem conjunto de validação explícito.
  - Conclusões: Importância da análise exploratória; sugestões para engenharia de features e AutoML.
</details>

### Texto-síntese crítico

Os estudos concordam na utilidade de técnicas de Machine Learning, como Random Forest e regressão linear, para prever resultados em processos seletivos educacionais, destacando variáveis acadêmicas (ex.: CGPA, GRE, notas de provas) como preditores principais. Há convergência na ênfase em pré-processamento de dados para lidar com ausentes e na superioridade de ensembles como Random Forest sobre baselines, alcançando acurácias ou R² acima de 0.8 em cenários de admissão ou previsão de notas. Divergências aparecem nos contextos: enquanto alguns focam em admissões pós-graduadas nos EUA (Trabalhos 1 e 2), outros tratam de acesso ao ensino superior europeu (Trabalhos 3 e 4) ou exames brasileiros como ENEM (Trabalho 5), variando métricas de classificação (AUC, acurácia) para regressão (MAE, R²).

Lacunas incluem generalização limitada (datasets específicos de uma universidade ou país), falta de dados individuais socioeconômicos, validação externa insuficiente e considerações éticas sobre viés. Limitações técnicas envolvem tamanhos de amostras pequenos e ausência de atualizações em tempo real; éticas, o risco de perpetuar desigualdades em seleções. O projeto EduMap alinha-se aos estudos ao usar ML para prever notas de corte no SISU com base em dados históricos, preenchendo uma lacuna no contexto brasileiro ao focar em dados abertos do MEC e disponibilizar uma aplicação prática. Diferencia-se ao priorizar regressão para estimativa contínua (nota de corte) em um sistema unificado como SISU, incorporando variáveis como curso, instituição e vagas, e avaliando múltiplos modelos para robustez.


<!-- Nesta seção, descreva abordagens da literatura que tratam problemas semelhantes ao seu. Seu objetivo é documentar métodos, dados, métricas e resultados.

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
> - [ACM Digital Library](https://dl.acm.org/) -->

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

[Acesso ao vídeo de apresentação da Etapa 01.](https://drive.google.com/file/d/1sdocJuI29CSaYA1Kzk9g1O1U3O4esCgR/view?usp=sharing)


<!-- Nesta etapa, o grupo deverá produzir um vídeo de 5 a 8 minutos apresentando o trabalho realizado, no qual cada integrante deve dizer seu nome e apresentar uma parte do conteúdo desenvolvido, garantindo que todos participem ativamente da gravação. A ausência de participação de qualquer membro resultará em penalização na nota final desta etapa. Recomenda-se que o grupo elabore previamente um roteiro para organizar a ordem das falas, distribuir o tempo de forma equilibrada e assegurar que todos os tópicos relevantes sejam apresentados de maneira clara e objetiva. -->

# Referências

- BRASIL. Ministério da Educação. **2023 – Relatório SISU – Chamada Regular 1/2023**. Portal Dados Abertos do MEC, 2023. Disponível em: https://dadosabertos.mec.gov.br/sisu/item/258-2023-relatorio-sisu-chamada-regular-1-2023. Acesso em: 7 mar. 2026.
  
- ENAGO ACADEMY. **Como desenvolver uma pergunta de pesquisa relevante: tipos e exemplos**. Enago Academy, 2022. Disponível em: https://www.enago.com/academy/how-to-develop-good-research-question-types-examples/. Acesso em: 7 mar. 2026.
  
- TUMELERO, Naína. **Aprenda como fazer o objetivo geral e os objetivos específicos do seu trabalho**. Blog Mettzer, 2017. Atualizado em: 7 mar. 2025. Disponível em: https://blog.mettzer.com/diferenca-entre-objetivo-geral-e-objetivo-especifico/. Acesso em: 7 mar. 2026.
  
- PONTIFÍCIA UNIVERSIDADE CATÓLICA DE MINAS GERAIS. Sistema Integrado de Bibliotecas. **Orientações para elaboração de citações e referências**: conforme as NBRs 10520:2023 e 6023:2025, da Associação Brasileira de Normas Técnicas (ABNT). 6. ed. Belo Horizonte: PUC Minas, 2025. Disponível em: https://www.pucminas.br/biblioteca. Acesso em: 7 mar. 2026.

- INEP. 3,9 milhões estão inscritos no Enem 2023. Instituto Nacional de Estudos e Pesquisas Educacionais Anísio Teixeira, 2023. Disponível em: https://www.gov.br/inep/pt-br/centrais-de-conteudo/noticias/enem/3-9-milhoes-estao-inscritos-no-enem-2023. Acesso em: 7 mar. 2026.

- CHITHRA APOORVA, D. A. et al. Prediction for University Admission using Machine Learning. International Journal of Recent Technology and Engineering (IJRTE), v. 8, n. 6, p. 4922–4926, 2020. DOI: 10.35940/ijrte.F9043.038620. Disponível em: https://www.researchgate.net/publication/363859360_Prediction_for_University_Admission_using_Machine_Learning. Acesso em: 7 mar. 2026.

- MAULANA, A. et al. Optimizing University Admissions: A Machine Learning Perspective. Journal of Educational Management and Learning, v. 1, n. 1, p. 1–7, 2023. DOI: 10.60084/jeml.v1i1.46. Disponível em: https://pdfs.semanticscholar.org/e550/b3552f887bf7463905ddc4372f63e608af0a.pdf. Acesso em: 7 mar. 2026.

- LIU, T. et al. A Machine-Learning-Based Approach to Informing Student Admission Decisions. Behavioral Sciences, v. 15, n. 3, p. 330, 2025. DOI: 10.3390/bs15030330. Disponível em: https://www.mdpi.com/2076-328X/15/3/330. Acesso em: 7 mar. 2026.

- EPALANGA, A. E. Machine Learning para Previsão de Acessos ao Ensino Superior. Mestrado em Engenharia Informática e Computação, Faculdade de Engenharia da Universidade do Porto, 2025. Disponível em: https://repositorio-aberto.up.pt/bitstream/10216/168200/2/733106.pdf. Acesso em: 7 mar. 2026.

- WATANABE, W. Prevendo as notas do ENEM com Machine Learning — Data Science. Medium, s.d. Disponível em: https://medium.com/@wesleywatanabe/data-science-machine-learning-enem-regressao-linear-5cd140459dc3. Acesso em: 7 mar. 2026.
 
<!-- Inclua todas as referências (livros, artigos, sites, etc) utilizados no desenvolvimento do trabalho utilizando o padrão ABNT.

> **Links Úteis**:
> - [Padrão ABNT PUC Minas](https://portal.pucminas.br/biblioteca/index_padrao.php?pagina=5886) -->
