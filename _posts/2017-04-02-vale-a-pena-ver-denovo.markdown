---
layout: post
title:  "Vale a pena ver denovo"
date:   2017-04-02 22:46:55 -0300
categories: BDD
---

Este post descreverá a experiencia obtida com a implementação do exercício da disciplina de Laboratorio de Engenharia de Software.

A utilização do BDD(Behavior Driven Development) melhora a comunicação entre Stakeholders e Desenvolvedores. Ele utiliza a metodologia de desenvolvimento orientado a testes onde os testes devem ser implementados antes do desenvolvimento de cada funcionalidade.

Inicialmente, realizei a leitura do livro "The Cucumber for Java Book", onde aprendi sobre a configuração da framework e sobre como que funciona a estrutura para a criação dos cenários e steps.

A criação dos cenários possibilitou um melhor entendimento de cada funcionalidade implementada. Além disso, assegurou que as mesma estão funcionando de acordo com o seu propósito.

O desenvolvimento foi feito de forma incremental, onde as primeiras implementações dos steps são feitas de forma bem simples apenas para que seja validado o comportamento daquele cenário. Posteriormente, a solução foi refatorada para que esta funcione utilizando padrões de projeto.

Acredito que como é uma mudança de paradigma desenvolver os testes antes da implementação, muitas pessoas tem dificuldade em enxergar que este tipo de solução trás muitos benefícios. Por exemplo, é possível identificar facilmente se uma nova funcionalidade irá afetar o funcionamento de outra já implementada. A rastreabilidade de erros no seu código aumenta consideravelmente visto que a framework mostra aonde exatamente está ocorrendo o erro.

A utilização da técnica para a implementação dos exercícios foi bem interessante. No segundo exercício, utilizei o BDD desde o início. Ou seja, criei os cenários e em seguida implementei as funcionalidades. Deu para verificar a evolução da solução e ver que ela está funcionando como deveria. O primeiro exercício foi feito da mesma maneira porém não foi finalizado. O terceiro e o quarto exercício foram feitos com a implementação já pronta. Ou seja, os cenários foram feitos depois da implementação. 

Acredito que vale a pena aprender a desenvolver software desta maneira. Continuarei a estudar mais sobre a framework e aprender a utilizar os seus recursos da maneira correta para que minhas próximas soluções sejam cada vez melhores.

Todos os códigos podem ser encontrados no [link](https://github.com/asleao/vale-a-pena-ver-denovo)