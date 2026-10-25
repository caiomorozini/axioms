# Sistemas operacionais e sistemas analíticos

Achei esse assunto muito interessante, pois ele converge bastante com a minha experiência profissional. Ao longo da minha trajetória, tive dificuldade para compreender essa divisão: atuei com ciência de dados durante a iniciação científica na faculdade, depois trabalhei com backend e, mais tarde, com sistemas analíticos. Quando entrei no mundo analítico, passei a enxergar os dados de outra forma, mas nunca consegui me adaptar completamente a esse distanciamento em relação ao backend. Toda a infraestrutura que construímos para dar suporte ao ambiente de big data seguia muitos dos princípios discutidos neste capítulo. Outro ponto importante é que essa etapa não envolve apenas complexidade de implementação, mas também — e sobretudo — complexidade de decisão. Escolher uma arquitetura adequada ao problema que se deseja resolver é crucial para o sucesso do projeto.

Os conceitos se misturam, o que muda aqui é a forma com os dados são utilizados e quem são os usuários finais. Em sistemas operacionais, o foco é em transações rápidas e consistentes, enquanto em sistemas analíticos, o foco é em consultas complexas e análise de grandes volumes de dados.
Quem está por trás de cada tipo de sistema também é diferente. Sistemas operacionais são desenvolvidos pelos engenheiros de softwares (backend é o caso mais comum), enquanto sistemas analíticos pertencem a dois tipos de profissionais (que requer acesso aos dados da organização): analistas de dados que geram relatórios e dashboards para ajudar na tomada de decisão, e cientistas de dados que utilizam técnicas de aprendizado de máquina para gerar modelos preditivos (e.g. previsão de demanda, detecção de fraude, recomendação de produtos, etc.).

Quero falar um pouco mais sobre os profissionais que trabalham com sistemas analíticos pois apesar de muita das vezes utilizarem ferramentas diferentes, eles tem algumas características em comum.

- "Perform analytics": olham para os dados que os usuários e os serviços backend geraram.
- Não modificam os dados (exceto talvez para corrigir erros ou inconsistências). **Aqui pode entrar o caso dos ETLs, pois geram datasets derivados que foram transformados de alguma forma.**

---
Em resumo:

- Sistemas do tipo operacionais consistem em serviços backend e infraestrutura de dados onde o dado é criado.
- Sistemas do tipo analíticos servem para atender a necessidade de análise de dados, onde o dado é consumido. Contém apenas uma cópia "read-only" dos dados, que é atualizada periodicamente a partir do sistema operacional e são otimizadas para os tipos de processamentos usuais de análise de dados (e.g. agregações, joins, filtros, etc.).


> Há um motivo desses sistemas serem separados!

Conforme esses sistemas se tornaram maduros, surgiram também dois novos profissionais:

- Engenheiros de dados: são responsáveis por criar pipelines de dados que extraem, transformam e carregam os dados do sistema operacional para o sistema analítico. Eles também são responsáveis por garantir a qualidade dos dados e a eficiência das operações de ETL.
- Engenheiros analíticos: modelam e transformam dados para tornar os dados mais úteis para análise. Eles trabalham em estreita colaboração com analistas de dados e cientistas de dados para garantir que os dados estejam estruturados de forma a facilitar a análise e a geração de insights.

Esse livro cobre todas essas áreas pois ambos tem papéis importantes no ciclo de vida do dado e é importante ter essa visão macro para trabalhar melhor com colegas que atuam do outro lado dessa divisão.

## Caracterizando [[processamento transacional]] e analítico

Nos primeiros anos dos processos envolvendo processamento de dados, escrever em um banco de dados tipicamente estava relacionado à uma transação comercial: fazer uma venda, fazer um pedido para um fornecedor, pagar o salário de um funcionário, etc. Hoje as bases de dados não necessáriamente envolvem transações financeiras porém o nome acabou ficando mas o seu significado sim: **[[processamento transacional]] refere-se à um grupo de leitura e escrita que forma uma unidade lógica**

> No capítulo 8 esse mesmo termos será utilizado para se referir a leituras e escritas de baixa latência.

Esses termos podem parecer bem confusos, ainda mais nos dias atuais onde bancos de dados são utilizados para posts em redes sociais, movimento em jogos e vários outros casos, o padrão básico para acessa-los é similar ao processamento transacional:

Um sistema operacional olha para um pequeno número de registros selecionados por uma chave ([[point query]]) e registros são inseridos, atualizados ou deletados com base no input do usuário. As aplicações por essencia serem interativas, esse padrão de acesso ficou conhecido como transação online ([[OLTP]] - [[Online Transaction processing]]).

O lado analítico também começou a crescer bastante porém a visão e o acesso mudam um pouco nesse caso. Normalmente, uma query analítica irá ler um grande número de registros e calcular estatíticas de agregação (como soma, contagem ou média) ao invés de retornar um registro individual para o usuário (como um sistema operacional faz).
Por exemplo, um analista em uma cadeia de supermercados quer responder perguntas como:

- Qual foi o total de vendas de cada uma das lojas em janeiro?
- Quantas bananas além do usual vendemos desde a última promoção?
- Qual marca de comida de bebês é mais comum de ser vendida junto com a marca X de fraldas?

O report gerado por esses resultados são tipos de queries muito relevantes para um BI, ajudando a gestão/executivos na tomada de decisão. Para diferenciar o uso dos bancos de dados é chamado de processamento analítico online ([[OLAP]] - [[Online Analytical Processing]])

Propriedade | OLTP | OLAP
---|---|---
Padrão de leitura | Point queries (acessar registros individuais por chaves) | Agregamento de um número grande de registros
Padrão de escrita | Insere, atualiza e deleta registros individuais | [[bulk loading]] (ETL) ou event stream
Uso de exemplo humano | Usuário final de uma aplicação web ou mobile | Analistas para apoio de tomada de decisão
Caso de uso para máquinas | Checar se a ação está autorizada | Detectar fraude/abuso
Volume | Muitas queries pequenas | Poucas queries mas com muita complexidade
Representatividade do dado | Último estado do dado (atual na linha do tempo) | Dado histórico
Tamanho do dataset | Giga a Terabytes | Tera até pentabytes

> O significado do **online** em OLAP não é claro, provavelmente indica que a query não é apenas para reports pré-definidos e que analistas usam o sistema interativamente com queries de exploração.


A partir dessa classificação, podemos discutir como corporações reais se comportam pensando até mesmo em governança. Os acessos às bases de dados para as equipes de dados costumam ser bem mais flexiveis dado a natureza e a necessidade, mas deixar usuários interagirem com bases de dados com liberdade é um risco muito grande dado que queries podem potencialmente ler e alterar os registros. Além disso, podem executar queries com custo de processamento elevado impactando o desempenho do banco de dados para outros usuários. Por essa razão, as queries construídas para sistemas OLTP são fixas e sem muitas costumizações e são utilizadas ocasionalmente para manutenção e troubleshooting. Por ouitro lado, é comum que bancos de dados analíticos deem acesso aos usuários a liberdade de escrever queries arbitrárias ou gerar queries automaticamente usando ferramentas de visualização de dados ou dashboards como Tableau, Looker ou Power BI.


## Data Warehousing

[[Data warehouse]] como o nome já diz, são bancos de dados onde a finalidade são consultas analíticas. Antes da existencia dessa divisão, os bancos OLTP eram utilizados para ambos os propósitos.
Pela natureza da forma como os ambientes analíticos são utilizados pelos analistas e cientistas, há razões para essa separação:

- Os dados de interesse podem estar espalhados por multiplos sistemas, tornando difícil combinar os datasets em uma única query.
> Casa diretamente com uma situação que esbarrei recentemente. Para sistemas operacionais, os serviços estão distribuídos em [[microserviços]] e há uma separação de domínio de aplicativos tanto para as APIs quanto para os bancos de dados (pensando até mesmo em [[Kubernetes]], onde há uma separação de rede entre esses domínios). Se você precisa de alguma informação que pertence a outro domínio, o ideal nesse caso é os mantenedores do domínio fornecerem uma interface que irá prover essa informação. Nem sempre isso será atendido e muito menos você terá acesso a essas tabelas, pois são as mesmas que os sistemas utilizam para as atividades transacionais.
- Os schemas e os layouts que são bons para OLTP não são ideais para sistemas analíticos (ver [[Stars and Snowflakes: Schemas for Analytics]])
- Queries analíticas podem ser muito caras e rodar em cima de tabelas OLTP podem causar impacto na performance para outros usuários.
- Sistemas OLTP podem estar localizadas em redes separadas que os usuários não tem permissão para acesso direto (por seguraça ou motivos de compliance).

Como contraste, um data warehouse permite realizar diferentes operações sem precisar se preocupar com essas questões. Mais para frente, será mostrado também que muitas vezes os dados são armazenados de formas diferentes por questões de otimização, por conta dos tipos de queries que são executadas ([[Chapter 04]]).
Dessa forma faz sentido pensar que os data warehouses são cópias com acesso apenas de leitura de dados de vários sistemas OLTP. Dados são extraídos de tabelas OLTP, transformados em schemas mais amigáveis para análises, limpos e então carregados nos data warehouses. Esse processo de extrair, transformar e carregar é chamado de [[ETL]]. 
> Nem sempre essa é a ordem, por exemplo: podemos carregar antes de transformar [[ELT]]

![[etl.png]]
Aqui o livro vai citar algumas ferramentas como [FiveTran](https://www.fivetran.com/), [Singer](https://www.singer.io/) e [Airbyte](https://airbyte.com/) que são serviços utilizados para conectar sistemas com warehouses. Confesso que nunca tinha ouvido falar (talvez o Airbyte, e diferente do livro eu quero me aprofundar nessas tecnologias. Por isso vou separar uma seção de pesquisa e teste para algumas das ferramentas que o livro for citando).
## Em poucas palavras

OLTP atende às operações da aplicação com leituras e escritas pontuais sobre o estado atual dos dados. OLAP atende à exploração e análise de grandes volumes, normalmente históricos. Separar os ambientes ajuda a evitar que consultas analíticas pesadas prejudiquem a operação e permite organizar os dados para os padrões de acesso de cada finalidade.

## Perguntas para revisão

- Como diferem os padrões de leitura e escrita de OLTP e OLAP?
- Por que consultas analíticas costumam ser executadas em um data warehouse, em vez de diretamente nos bancos OLTP?
- Que necessidades de governança, segurança e desempenho essa separação ajuda a atender?