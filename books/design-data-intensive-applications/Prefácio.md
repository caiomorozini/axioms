O autor inicia o livro fazendo a seguinte reflexão: "There are hundreds of databases to choose from. Which one shoud you use for your application?" E como toda bom pragmático, ele apenas responde que depende e que a resposta está no próprio livro.

Uma palavra que irá se repetir ao longo do livro é o termo [[Trade Offs]], que significa "compromissos" ou "trocas". Uma abordagem que encaixa perfeitamente em um cenário pode não ser a melhor escolha em outro. O autor enfatiza que não existe uma solução única para todos os problemas, e que cada decisão de design envolve considerar os prós e contras de diferentes abordagens. Cabe ao desenvolvedor avaliar cuidadosamente as necessidades específicas de sua aplicação e escolher a solução que melhor se adapta a essas necessidades, mesmo que isso signifique abrir mão de certas vantagens em favor de outras.

Apesar das diferentes e diversas tecnologias surgirem, os **fundamentos** permanecem os mesmos. Se você entender os princípios fundamentais, estará em uma ótima posição para avaliar novas tecnologias e tomar decisões.

> The computing industry tends to be attracted to things that are new and shiny and to look down on ideas that are considered old or academic. That is a mistake; many powerful, foundational ideas in computing arose from research, some recent, some decades ago. On the other hand, academia sometimes lacks a clear idea of what issues are important in pratice.

## O que mudou na segunda edição

A primeira versão foi publicada em 2017 e muita coisa mudou desde então. consequentemente, o livro precisou ser revisado para refletir as mudanças no cenário de desenvolvimento de software. A maior mudança tecnológica como todos sabemos é a explosão no interesse por [[artificial inteligence]] e a ascenção de [[cloud native data systems architectures]].

> While this book is not about AI per se, we have added coverage of data systems that support AI and machine learning, including vector indexes (used for semantic search), DataFrames (used for training datasets), and batch processing systems for preparing large amounts of training data

Também foi adicionado algumas discussões a respeito de algumas tecnologias ([[sync engines and local-first software]], [[workflow engines and durable execution]], [[formal methos and randomized testing]], [[GraphQL]])

O que eu achei curioso foi que ele removeu o MapReduce pois agora está obsoleto e não é mais utilizado.