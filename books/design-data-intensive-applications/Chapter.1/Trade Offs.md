
> There are no solutions; there are only trade-offs. [...] But you try to get the best trade-offs you can, and that`s all you can hope for. - Thomas Sowell, interview with Fred Barnes (2005)

Antes de pensarmos em arquitetura, precisamos entender que para qualquer solução que iremos propor, estará essencialmente ligada aos dados. Hoje, tudo produz dados (o usuário que interage com a aplicação tanto acessa os dados armazenados quanto que ao mesmo tempo está gerando novos dados)

Pequenas quantidades de dados são fáceis de serem manipuladas e armazenadas, mas à medida que a quantidade de dados ou a taxa de queries aumenta, é necessário distribuir entre múltiplas máquinas, o que introduz complexidade.

Chamamos de [[data-intensive]] se o gerenciamento de dados é o desafio principal da aplicação. Diferente de aplicações que são [[compute-intensive]], onde o desafio principal é a quantidade de cálculos que precisam ser feitos, em aplicações data-intensive o desafio é como armazenar, acessar e processar grandes quantidades de dados.

Os blocos de construção são sempre os mesmos e incluem:

- Guardar dados para serem acessados pela própria aplicação ou por outras aplicações.([[Bancos da dados]])
- Lembrar do resultado de operações muito custosas para acelerar a leitura ([[caches]])
- Permitir usuários buscarem dados por uma palavra chave ou filtrar de várias formas ([[indexação]])
- Lidar com eventos e alterações de dados em tempo real ([[streaming]])
- Periódicamente processar grandes quantidades de dados acumulados ([[processamento em lote]])

Construir uma aplicação é pegar vários serviços (como bancos de dados ou APIs) e conectá-los com um código que implementa a lógica de negócio. A arquitetura de uma aplicação é o desenho de como esses serviços se conectam e interagem.

Entretanto, conforme a aplicação cresce, desafios aparecem. Não é só colocar qualquer banco de dados por exemplo pois cada um deles tem suas características e são mais adequados para determinados tipos de aplicações. Por exemplo, um banco de dados relacional é ótimo para aplicações que precisam de consistência e integridade dos dados, enquanto um banco de dados NoSQL pode ser mais adequado para aplicações que precisam de alta escalabilidade e flexibilidade.

Alguns tópicos que serão abordados neste capítulo incluem justamente para ajudar a entender essas escolhas:

- [[Operational Versus Analytical Systems]] (Diferença entre um sistema operacional e um sistema analítico)
- [[Cloud Versus Self-Hosting]] (Prós e contras de hospedar a aplicação na nuvem ou em servidores próprios)
- [[Distributed Versus Single-Node Systems]] (Quando mover de um sistema de nó único para um sistema distribuído)
- [[Data Systems, Law, and Society]] (Balanciando as necessidades de negócio e os direitos dos usuários)