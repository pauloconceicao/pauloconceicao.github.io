---
layout: post
title:  "Análise Geoespacial com GIS (Geographic Information System) e Python: uma breve introdução"
date: 2020-07-18 00:00:00
description: Primeiro blogpost de uma sequência de 3
img: Abandoned-Mine1.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Mining, Dataset, Geocoding, Visualization]
categories: [Mining, Dataset, Geocoding, Visualization]
---

Análise Geoespacial com GIS (Geographic Information System) e Python: uma breve introdução

Este tutorial é dividido em três partes e mostrará como fazer e personalizar um mapa das minas abandonadas do estado de Minas Gerais usando geoespacial análise com GIS (Geographic Information System) e a biblioteca Geopandas da linguagem Python. O foco será a plotagem de mapas do estado e de municípios de Minas Gerais onde se possa observar a localização das minas abandonadas e atributos relativos as minas. Aprofundamentos no tema Geographic Information System e Python podem ser encontrados em GIS e Python.


![capa]({{site.baseurl}}/assets/img/capa.png)

Qual profissional de Engenharia de Minas que quando estava fazendo uma apresentação, relatório, palestra ou aula e deparou-se com a necessidade de colocar um mapa de localização de pontos, linhas ou polígonos para representar algo ou materializar uma ideia? Muitas são as maneiras para fazer isso que vão desde fazer download de imagem ou gerar um mapa. Mas que tal fazer teu próprio mapa, que represente tuas ideias e que se possa colocar cores, legendas etc., como tu queres e de maneira, relativamente, fácil e rápida? Se tu gostaste da ideia, continue lendo e no final veja se o resultado poderá ser de alguma utilidade.

### O que tu verás nesse pequeno artigo:

* Motivando a usar Data Science, GIS e Python
* Conceito de dados vetoriais voltados a criação de mapas.
* Definição de dados geoespaciais (shapefiles).
* Como dados geoespaciais são lidos.
* Onde encontrar dados geoespaciais sobre Minas Gerais.
* Rudimentos da Linguagem Python.
* Plotagem de mapas através de shapefiles.
* Visualização em mapa das minas abandonadas do estado de Minas Gerais com atributos como risco ambiental, situação da mina e substância mineral.

>Bottleneck: Se tu já sabes o que quer, nesse caso, fazer um mapa com pontos de localização, mas e o como fazer?

<p>Bom, nada vem sem estudo e esforço. É essencial saber o que se quer, mas principalmente, como fazer. Existem softwares comerciais que desempenham muito bem a função de criar mapas, mas envolve custo computacional, de aprendizado e tempo. E talvez seja usado só uma vez. Mas que tal aprender algo que possa ser usado nas mais diversas oportunidades e que traga um upgrade profissional?</p>

**Motivação**: Para mim, o momento **Eureka** de problemas como este ou a resposta, está em aprender uma linguagem de programação ou de script. Ela proverá independência e total fluidez para tuas ideias. Minha recomendação é a queridinha da Data Science: Python.

<p>Antecipadamente, comento que está fora da intenção deste pequeno artigo ensinar alguém a ser fluente em Python, mas sim, derrubar o muro de resistência em aprender uma linguagem e mostrar que com poucos comandos é possível realizar tarefas que antes pareciam ser impossíveis, como plotar teu próprio mapa.</p>

### Por que usar Python? ###
A linguagem Python tem ganho cada vez mais destaque no cenário tecnológico mundial como a linguagem dos cientistas de dados. Aí tu vais dizer, mas eu não sou cientista de dados. Calma, baixa a guarda e segue com a leitura, pois se tu és engenheiro ou trabalha com pesquisa, faz apresentações, palestras, etc, será bom entender algo sobre o assunto. O fato do crescimento do uso de Python é tão marcante que empresas como Google, Youtube, Dysney, Mozilla, Drop Box, Bit Torrent, Intel, Cisco, Hewlett-Packard, Seagate, Qualcomm, IBM, NASA entre outras usam Python em diversas tarefas.

Para muitos, Python é uma linguagem de programação, mas na verdade é uma scripting linguage, deixo o termo original para manter a terminologia correta, sem os erros grotescos que muitas vezes as traduções proporcionam. Python não usa compilador e pode rodar em qualquer lugar que rode o shell do Python (mas o que é um Shell? Nada a ver com gasolina. Shell é uma interface de usuário para acessar os serviços de um sistema operacional). É limpa, fácil de ler, com isso não se perde tempo fazendo debugging de código para achar erros. Assim, segundo JetBrains.com, 84% dos usuários de Python, usam Python como primeira linguagem. Outro dado interessante é que 60% dos usuários, usam Python tanto para trabalhar, como para uso pessoal. Ainda, 58% dos usuários usa análise de dados. Quando se fala em Python, tem que ser falado em conta o sistema operacional: 69% dos usuários rodam Python em Linux. Esse número é totalmente justificado, e falo por experiência própria, pois muitas bibliotecas, pacotes, módulos e frameworks não rodam de forma apropriada em Windows. Aqui temos outro bottleneck: ou não. Pense que esta é uma ótima oportunidade para aprenderes Linux. Para os mais reticentes: sim, podes usar Python no Windows, mas sempre tem **“o Mas”**... como eu já disse, prepare-se para instabilidades e incompatibilidades. O Python cru roda no Windows, o problema são as bibliotecas extras e são, exatamente, elas a beleza do Python.



**Caso queira continuar lendo** [Link para o artigo completo](https://www.linkedin.com/pulse/geoespacial-an%25C3%25A1lise-com-gis-geographic-information-e-nunes-concei%25C3%25A7%25C3%25A3o/)



