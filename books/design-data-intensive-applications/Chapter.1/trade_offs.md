# Trade Offs in Data Systems Architecture
> There are no solutions; there are only trade-offs. [...] But you try to get the best trade-offs you can, and that`s all you can hope for. - Thomas Sowell, interview with Fred Barnes (2005)

Antes de pensarmos em arquitetura, precisamos entender que para qualquer solução que iremos propor, estará essencialmente ligada aos dados. Hoje, tudo produz dados (o usuário que interage com a aplicação tanto acessa os dados armazenados quanto que ao mesmo tempo está gerando novos dados)

Pequenas quantidades de dados são fáceis de serem manipuladas e armazenadas, mas à medida que a quantidade de dados ou a taxa de queries aumenta, é necessário distribuir entre múltiplas máquinas, o que introduz complexidade.

Chamamos de [[data-intensive]] se o gerenciamento de dados é o desafio principal da aplicação.