# Implantação da solução

A implantação da solução EduMap foi realizada em ambiente de computação em nuvem, utilizando **Google Cloud Platform** como provedor principal. A escolha do GCP se deu pela integração entre serviços gerenciados, facilidade de publicação de aplicações baseadas em containers e disponibilidade do Cloud Run, capaz de executar aplicações web sob demanda, com escalabilidade automatica.

A solução foi organizada em duas camadas principais: **frontend e backend**. O frontend foi desenvolvido com HTML, CSS e JavaScript, permitindo que o usuário informe seus dados de entrada, como objetivo, área de interesse, grau, modalidade e notas do ENEM. O backend foi desenvolvido com FastAPI, responsável por receber os dados enviados pelo usuário, processar a requisição e realizar a inferência utilizando os modelos treinados.

Os modelos de Machine Learning foram treinados previamente em ambiente de desenvolvimento e exportados em arquivos **.pkl**. Na implantação em nuvem, esses arquivos foram agrupados junto ao backend, permitindo que a aplicação em produção realize previsões em tempo de execução, sem necessidade reprocessamento da base original. Dessa forma, a cada nova requisição enviada pelo frontend, a API carrega as entradas do usuário, aplica o pipeline de predição e retorna em tempo real as recomendações de cursos e probabilidades associadas.

O backend foi publicado no Cloud Run por meio do comando de deploy com origem no código-fonte. A aplicação FastAPI foi configurada para executar com Uvicorn, escutando a porta definida pela variável do ambiente **PORT**, como exigência do Cloud Run. O frontend também foi implantado no Cloud Run, utilizando um Dockerfile baseado em Nginx. Para isso, or arquivos estáticos das interface foram copiados para o diretório padrão do Nginx, e a configuração do servidor foi ajustada para escutar na porta 8080, compatível com o ambiente do Cloud Run.

A comunicação entre o frontend e o backend foi realizada por meio de requisições HTTP para a rota **/predict** da API. No arquivo de configuração do frontend, foi definida a URL pública do backend, permitindo que a interface hospedada em nuvem envie os dados do usuário diretamente para a API.

A escolha do Google Cloud Run foi motivada pela facilidade de publicação, escalabilidade automática e a cobrança sob demanda. Como a aplicação possui uso acadêmico e baixo volume inicial de acessos, o modelo severless é adequado, pois permite que a aplicação escale conforme a quantidade de requisições, sem a necessidade de manter os servidores ativos continuamente.

Para o planejamento de capacidade operacional, considerou-se um cenário incial de baixa a média utilização, com requisições ocasionais feitas por usuários acessando a interface web. Como cada inferência consiste apenas no carregamento dos dados enviados, aplicação do modelo já treinado e retorno da resposta, o tempo de processamento esperado é baixo (menos de 1 segundo) Assim, o sistema foi dimensionado para operar inicialmente com uma instância mínima sob demanda, permitindo escalabilidade automática caso o volume de acessos aumente.

Após a implantação, foram realizados testes para validar o funcionamento da solução. Inicialmente, foi testada a rota raiz da API, que retornou o status **online**. Em seguida, foi realizado o teste na rota /predict, enviando dados simulados de um candidato. A API retornoi corretamente o perfil indicado e uma lista de cursos recomendados com percentuais de chance, comprovando que o modelo estava sendo utilizado em produção para inferência em tempo real.

Também foi realizado o teste da interface web hospedada na nuvem. O frontend carregou corretamente os arquivos de estilo, scripts e imagens, e passou a se comunicar com a API publicada no Cloud Run. Com isso, foi possível validar o fluxo completo da solução: o usuário acessa a interface, informa seus dados, o fronted envia a requisição para o backend, a API executa a inferência com o modelo treinado e retorna as recomendações.

Dessa forma, a implantação atende ao requisito de disponibilizar a aplicação em ambiente de computação em nuvem, preparada para realizar previsões em tempo real com modelos treinados, sem a necessidade de reprocessamento durante o uso em produção.

Link da Aplicação: https://edumap-front-34527319953.us-central1.run.app/


## Testes

| Teste Realizado | Resultado Esperado | Resultado Obtido |
|----------------|-------------------|------------------|
| Verificação da rota raiz da API (`/`) | Retorno do status da aplicação | Sucesso |
| Teste da rota `/predict` | Retorno das recomendações geradas pelo modelo | Sucesso |
| Comunicação entre frontend e backend | Troca correta de dados entre os componentes | Sucesso |
| Exibição das recomendações na interface | Apresentação dos resultados ao usuário | Sucesso |
| Tempo médio de resposta | Inferior a 1 segundo | Inferior a 1 segundo |
| Disponibilidade da aplicação em nuvem | Aplicação acessível pela internet | Sucesso |



# Apresentação da solução

Nesta seção, deve ser produzido um vídeo de até 15 minutos apresentando o escopo geral do projeto, um resumo das etapas desenvolvidas, a demonstração da solução publicada e as conclusões finais, destacando aprendizados, impacto e possibilidades de melhorias.

<a href="../docs/img/EduMap - 7° periodo.pdf">Acesse a apresentação final do projeto EduMap.



