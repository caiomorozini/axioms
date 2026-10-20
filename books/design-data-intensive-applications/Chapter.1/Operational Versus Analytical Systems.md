Eu particulamente achei muito interessante esse assunto pois converge bastante com minha experiência profissional. Toda a infraestutura montada para suportar o ambiente de bigdata seguiu muitos dos princípios que são discutidos nesse capítulo. Outra coisa importante ressaltar é que essa etapa não se trata de complexidade de implementação, mas sim de complexidade de decisão. A escolha de uma arquitetura adequada para o problema que se deseja resolver é crucial para o sucesso do projeto.

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

