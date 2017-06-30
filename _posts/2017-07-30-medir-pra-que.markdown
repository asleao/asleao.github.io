---
layout: post
title:  "Medir? Pra que?"
date:   2017-06-30
categories: Testes
---

Este post descreverá a experiência obtida com a medição de software feita no trabalho da disciplina de Laboratorio de Engenharia de Software.

A fim de medir a qualidade do desenvolvimento, foi necessário definir no início do projeto quais eram as métricas de qualidade a serem medidas, ou seja, o que medir? Foram escolhidas as seguintes métricas:

* CodeSmells
* Confiabilidade
* Segurança
* Manutenibilidade
* Duplicações
* Tamanho do código
* Nível de complexidade
* Commits que falharam

Com excessão da última métrica escolhida, todas as métricas escolhidas podem ser medidas através do software **SonarQube**. Ele foi configurado no ambiente de integração contínua para que cada nova modificação no software a equipe pudesse acompanhar se as métricas escolhidas estavam de acordo com os padrões definidos. A informação sobre os commits que falharam foi fornecida pela API do TravisCI. Os padrões definidos para as métricas foram:

* Confiabilidade: Nota >= B
* Segurança >= D
* Manutenibilidade >=B
* Duplicações no máximo 5%
* Complexidade 30 pontos por arquivo
* 5 commits com falha por Sprint

Para verificar se os valores que definimos nas métricas de qualidade estavam sendo atingidos, além de conferir os valores no Sonar, utilizamos o gráfico da Monalessa XMmR, que realiza o cálculo da mediana para montar o gráfico das métricas. Utilizamos este gráfico pois o cálculo da mediana permite variações menos bruscas no gráfico. Os dados a serem avaliados podem conter valores muito altos ou muito baixos que poderiam elevar os limites do gráfico. Como por exemplo, o código cair de uma nota A para a nota D.

A experiência de realizar tais medições ajudou a equipe a identificar se o que estava sendo produzido estava de acordo com os padrões definidos no início do projeto e ajudou também na escrita de código com mais qualidade evitando possíveis problemas futuros como, por exemplo, a produção de códigos muito complexos. Além disso, como o sonar além de medir os atributos, mostra possíveis soluções para os problemas identificados. Por exemplo, no caso dos code smells ele fala qual linha do código que foi escrito algo errado e mostra o padrão a ser seguido.

Acredito que vale a pena realizar as medições de qualidade ao longo do desenvolvimento de um software. Além de produzir produtos com mais qualidade, com certeza evitará problemas mais complexos no final do ciclo de vida de desenvolvimento, onde o impacto para a realização de mudanças é muito alto.
