---
layout: post
title:  "Contribuições do trabalho de LES"
date:   2017-06-05
categories: BDD
---

Neste post, falarei um pouco sobre o trabalho que desenvolvi com o meu grupo na disciplina de LES, quais foram as minhas contribuições e o quanto elas impactaram no projeto.

Nosso trabalho teve como objetivo desenvolver um sistema que auxiliasse na gestão e alocação de membros nas ferramentas utilizadas no laboratório LEDS. A ideia do projeto, é ter um micro serviço principal, onde serão cadastrados os projetos, credenciais, ferramentas e participantes de um projeto e micro serviços separados para cada uma das ferramentas. Ao cadastrar um novo projeto, o sistema principal se comunica com os micro serviços de cada ferramenta e realiza a criação deste projeto e alocação dos membros nestas. Como são muitas, o escopo do projeto se limitou a integrar com apenas 2 ferramentas.

Ao longo da disciplina, minhas maiores contribuições na documentação do projeto foram na escrita da introdução, especificação dos requisitos, projeto arquitetural, projeto detalhado, projeto interface com o usuário, projeto persistencia de dados, padrões de projeto, gestão de configuração, gestão de projetos e gerência da qualidade. Escrevi alguns subtópicos e auxiliei na escrita de outros. Já na implementação, pude contribuir na configuração do ambiente de integração contínua do projeto e na configuração dos micro serviços. Além disso, auxiliei no desenvolvimento de cada micro serviço bem como a criação dos BDD's. Como essa parte de comunicação entre API's terceiras era algo que nenhum dos integrantes da equipe já tinha feito, fizemos grande parte das funcionalidade juntos. Tivemos alguns problemas com a questão de autenticação o que fez com que nós conseguissemos implementar apenas o micro serviço do Github. 

Neste trabalho tive a oportunidade de conhecer técnologias novas e aprender sobre como realizar as comunicações entre API's terceiras. Tivemos bastante dificuldade, mas acredito que conseguimos adquirir bastante conhecimento.
