Segundo a documentação oficial, Singer é uma especificação open-source para construção de pipelines de movimentação de dados, baseada em dois componentes principais: _Taps_, responsáveis pela extração dos dados, e _Targets_, responsáveis pelo carregamento nos destinos.

[Documentação Singer](https://www.singer.io/)

Diferentemente do [[Airbyte]] e [[Fivetran]], não é propriamente uma plataforma, mas um padrão para desenvolvimento de conectores. Possui uma abordagem mais code-oriented, permitindo desenvolver e customizar os conectores conforme a necessidade. Existem conectores prontos mantidos pela comunidade, mas a configuração, execução e orquestração ficam sob responsabilidade do usuário.

Possui uma filosofia semelhante à do [[Kedro]] no sentido de trabalhar com componentes modulares e pipelines definidos por código, permitindo maior controle sobre a implementação e execução dos fluxos. Entretanto, enquanto o Singer é voltado especificamente à movimentação e integração de dados, o [[Kedro]] oferece uma estrutura mais abrangente para organização, desenvolvimento e execução de pipelines de processamento de dados.

Não possui interface gráfica nativa para construção de pipelines e não é uma solução propriamente no-code.