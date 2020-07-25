---
layout: post
title:  "Análise Geoespacial com GIS (Geographic Information System) e Python: uma breve introdução - terceira parte"
date: 2020-07-25 00:00:00
description: Terceiro blogpost de uma sequência de 3
img: 2020-07-25-P3-PLOT3-SITUACAO_MAPA_MG_1.2.PNG # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Mining, Dataset, Geocoding, Visualization]
categories: [Mining, Dataset, Geocoding, Visualization]
---
Como mencionado na [primeira parte](https://pauloconceicao.github.io/como-postar-no-github-com-jekyll/) deste artigo ele é divido em três e, sendo esta a última, será abordada a manipulação de shapefiles e a utilização de Geopandas.

Se por acaso tu caiste de para-quedas nesse post, não esqueça de olhar a [parte dois](https://pauloconceicao.github.io/An%C3%A1lise-Geoespacial-com-GIS-e-python/).

## Lendo arquivos shapefile
Primeiramente, para quem vai usar Python é interessante ter as tais bibliotecas que falei. Dependendo do ambiente que for usado para rodar Python, muitas já serão instaladas. Mas se tu queres fazer um test drive e baixar o Python (o tamanho não passa de 40Mb) do site [www.python.org](www.python.org)  é recomendado instalar certos pacotes. São facilmente instalados usando o comando **pip** (Windows ou Linux), basta digitar na linha de comando:

* pip install numpy
* pip install matplotlib
* pip install pandas
* pip install geopandas

<div style="width: 600px;">
 <a href="/assets/img/2020-07-25-P3-FIG_04_IMPORT LIBRARIES.png"> <img src="/assets/img/2020-07-25-P3-FIG_04_IMPORT LIBRARIES.png" width="480px"></a>
</div>

Cada uma destas bibliotecas desempenha várias funções específicas que farão o trabalho bruto. Aqui, a mais importante e a biblioteca **Geopandas**, ela é capaz de ler diferentes formatos de arquivos chamados dados espaciais, pois além de Shapefile, existem outros como **KML**, **GeoJSON**, etc. Juntamente com a biblioteca Geopandas, outras bibliotecas serão utilizadas para que os dados possam ser mais bem visualizados e tratados, por isso elas serão importadas de acordo com a figura ao lado.

Após importar as bibliotecas necessárias, o arquivo já poderá ser lido.

<div style="width: 600px;">
 <a href="/assets/img/2020-07-25-P3-FIG_05_ARQUIVO.png"> <img src="/assets/img/2020-07-25-P3-FIG_05_ARQUIVO.png" width="480px"></a>
</div>

Aplicando a função **head()** no arquivo com os dados, pode-se observar mais detalhadamente como os dados são compostos. Os atributos do arquivo são o nome do empreendimento, situação da mina, município, supram, número do processo, DNPM, substância, risco ambiental, vulnerabilidade, latitude, longitude e geometria. O atributo **geometry**, refere-se ao dado espacial, que, neste caso, é o ponto de localização de cada empreendimento. O arquivo é composto por 400 empreendimentos (linhas) e 13 atributos (colunas).

<div style="width: 600px;">
 <a href="/assets/img/2020-07-25-P3-FIG_06_DATAFRAME.png"> <img src="/assets/img/2020-07-25-P3-FIG_06_DATAFRAME.png" width="480px"></a>
</div>

Como o foco é plotar os pontos de localização das minas abandonadas no mapa, não vamos nos estender muito na análise dos dados, numa primeira abordagem, assim, vamos nos fixar nos atributos 'Municipio', 'Substancia', ' Situacao', 'Risco__Amb' e 'geometry'.

O atributo 'Municipio' refere-se aos municípios onde cada mina abandonada está localizada. Tem-se as 400 minas distribuídas em 156 municípios. A figura abaixo mostra os 10 municípios com maior quantidade de minas abandonadas. Coromandel é o município que possui a maior quantidade de empreendimentos abandonados, 21 no total, sendo quase o dobro do segundo que é Jequitinhonha com 12.

<div style="width: 600px;">
 <a href="/assets/img/2020-07-25-P3-FIG_07_MUN_MG.png"> <img src="/assets/img/2020-07-25-P3-FIG_07_MUN_MG.png" width="480px"></a>
</div>

Com relação ao atributo 'Substancia', este refere-se a substância principal que cada mina abandonada produzia. Estas compunham-se de 29 substâncias, sendo granito, areia, argila e diamante as que representavam a maior quantidade. Granito, com 72 minas, equivalia a 18% do total de minas abandonadas. Enquanto, areia tinha 59 minas (14,75%), argila tinha 32 minas (8%) e diamante também tinha 32 minas (8%). O gráfico de barras abaixo mostra as substâncias e suas quantidades.

<div style="width: 600px;">
 <a href="/assets/img/2020-07-25-P3-PLOT1-Substâncias1_3.PNG"> <img src="/assets/img/2020-07-25-P3-PLOT1-Substâncias1_3.PNG" width="480px"></a>
</div>

A figura abaixo mostra o código que deu origem ao gráfico de barras.

<div style="width: 600px;">
 <a href="/assets/img/2020-07-25-P3-FIG_10_SUBSTS_MG_COD_PLOT.png"> <img src="/assets/img/2020-07-25-P3-FIG_10_SUBSTS_MG_COD_PLOT.png" width="480px"></a>
</div>

Para o atributo 'Situacao', foram vinculadas três situações da mina abandonada: Abandonada, Paralisada com controle ambiental e Paralisada sem controle ambiental. São consideradas Abandonadas, 166 minas (41,5%), 134 minas classificam-se como Paralisada com controle ambiental (33,5%) e 100 minas como Paralisada sem controle ambiental (25%). A figura abaixo mostra o fragmento de código para obter-se os dados e uma tabela com os valores.

<div style="width: 600px;">
 <a href="/assets/img/2020-07-25-P3-FIG_11_SITUACAO.PNG"> <img src="/assets/img/2020-07-25-P3-FIG_11_SITUACAO.PNG" width="480px"></a>
</div>

Para plotar os dados relacionados a localização das minas abandonadas pode-se utilizar um gráfico simples, do tipo par ordenado (x,y), onde o eixo **X** representa a longitude e **Y** representa a latitude. Esse par ordenado pode ser obtido a partir das variáveis **LAT**, **LONG** ou da variável **geometry**. **Geometry** contém os dados geoespaciais, que nesse caso representa o shapefile ponto. Com apenas uma linha de código é possível geral o gráfico determinando diversas características cor, tamanho, legenda, etc. A figura abaixo exemplifica a fração do código.

<div style="width: 600px;">
 <a href="/assets/img/2020-07-25-P3-FIG_14_COROMANDEL_CODE1.PNG"> <img src="/assets/img/2020-07-25-P3-FIG_14_COROMANDEL_CODE1.PNG" width="480px"></a>
</div>

O resultado do código é mostrado na próxima figura, onde vê-se os pontos discretizados que representam cada uma das 400 minas abandonadas e as cores rotulam a situação de cada mina.

<div style="width: 600px;">
 <a href="/assets/img/2020-07-25-P3-PLOT2-SITUACAO1_2.PNG"> <img src="/assets/img/2020-07-25-P3-PLOT2-SITUACAO1_2.PNG" width="480px"></a>
</div>

Com o gráfico de par ordenado é possível ter a noção de espaçamento entre as localizações. Mas para deixar o gráfico mais atrativo seria interessante visualizar os pontos diretamente no mapa de Minas Gerais. Para realizar esta tarefa basta ter-se o shapefile com polígonos que representem as fronteiras entre municípios e do estado de Minas Gerais. O download do arquivo **zip** está disponível em: [ftp://geoftp.ibge.gov.br/organizacao_do_territorio/malhas_territoriais/malhas_municipais/municipio_2019/UFs/MG/](ftp://geoftp.ibge.gov.br/organizacao_do_territorio/malhas_territoriais/malhas_municipais/municipio_2019/UFs/MG/)

O procedimento para descompactação e abertura do arquivo, segue os mesmos procedimentos que já foram descritos anteriormente. Após aberto, o arquivo mostrará o código e nome de cada município, bem como a variável **geometry** que armazena o polígono para cada município. Utilizando a função **plot** é possível, como mostrado na figura abaixo, e, automaticamente, carregar a variável **geometry** e ao mesmo tempo os dados da variável **‘Situacao’**, assim, plota-se o mapa de Minas Gerais e os pontos de localização das minas.

<div style="width: 600px;">
 <a href="/assets/img/2020-07-25-P3-FIG_13_COD_MAP_MG_Situacao.PNG"> <img src="/assets/img/2020-07-25-P3-FIG_13_COD_MAP_MG_Situacao.PNG" width="480px"></a>
</div>

A figura abaixo mostra o resultado do código, onde todos os municípios de Minas Gerais são plotados e os que possuem minas abandonadas mostram as respectivas localizações.

<div style="width: 600px;">
 <a href="/assets/img/2020-07-25-P3-PLOT3-SITUACAO_MAPA_MG_1.2.PNG"> <img src="/assets/img/2020-07-25-P3-PLOT3-SITUACAO_MAPA_MG_1.2.PNG" width="480px"></a>
</div>

Como visto anteriormente, Coromandel é o município de Minas Gerais com maior número de minas abandonadas. No arquivo contendo os dados dos municípios e no arquivo que contém os polígonos que descrevem cada município de Minas Gerais é possível isolar um ou mais municípios e plotar o respectivo mapa. A figura abaixo representa o fragmento de código que separa os dados de Coromandel.

<div style="width: 600px;">
 <a href="/assets/img/2020-07-25-P3-FIG_14_COROMANDEL_CODE1.PNG"> <img src="/assets/img/2020-07-25-P3-FIG_14_COROMANDEL_CODE1.PNG" width="480px"></a>
</div>

O procedimento para plotar o mapa de Coromandel e com as suas minas abandonadas é idêntico ao do mapa de Minas Gerais, o diferencial é que os arquivos para onde a função plot é apontada são mg_mun_COROMANDEL e data_COROMANDEL, ficando mg_mun_COROMANDEL.plot e data_COROMANDEL.plot. A figura abaixo mostra o resultado, sendo que dois pontos ficaram fora do mapa. A explicação pode estar relacionada a erro de digitação quando a base de dados foi formulada ou as minas foram registradas como pertencentes a Coromandel mas estão no município vizinho, não tem como sabermos.

<div style="width: 600px;">
 <a href="/assets/img/2020-07-25-P3-PLOT4-MAPA_MG_COMANDATEL_SITUACAI1_2.PNG"> <img src="/assets/img/2020-07-25-P3-PLOT4-MAPA_MG_COMANDATEL_SITUACAI1_2.PNG" width="480px"></a>
</div>

O atributo 'Risco__Amb', mostra a classificação das minas abandonadas quanto ao seu risco ambiental potencial de acordo com o Cadastro de Minas Abandonadas Paralisadas, da FEAM – Fundação Estadual do Meio Ambiente de Minas Gerais. A classificação é dividida em cinco categorias: BAIXA, MÉDIA, ALTA, MUITO BAIXA e MUITO ALTA. A classificação BAIXA está relacionada a 178 minas abandonadas, o que representa 44,5% do total, em segundo lugar, MÉDIA com 167 (41,75%) e em terceiro, ALTA com 30 (7,5%). As demais classificações completam o número restante (MUITO BAIXA E MUITO ALTA). A figura a abaixo mostra o código para obter-se os dados e os valores para cada classificação. Observa-se que uma entrada foi feita de forma errônea e foi atribuído a palavra “granito” no lugar de uma das classificações de risco. A figura abaixo mostra o código para obter-se o somatório para cada categoria.

<div style="width: 600px;">
 <a href="/assets/img/2020-07-25-P3-FIG_08_RISCO_MG.png"> <img src="/assets/img/2020-07-25-P3-FIG_08_RISCO_MG.png" width="480px"></a>
</div>

Seguindo o mapa anterior, um mapa contendo a Situação de Risco de cada mina abandonada também pode ser plotado. O seguinte mapa representa as mesmas minas de Coromandel, agora com a Situação de Risco de cada uma.

<div style="width: 600px;">
 <a href="/assets/img/2020-07-25-P3-PLOT5-MAPA_MG_COMANDATEL_RISCO_1_2.PNG"> <img src="/assets/img/2020-07-25-P3-PLOT5-MAPA_MG_COMANDATEL_RISCO_1_2.PNG" width="480px"></a>
</div>

Além dos atributos mencionadas nos mapas anteriores, o tipo de substância primária de cada mina também pode ser plotado. A figura abaixo ilustra as minas e suas substâncias. Observa-se para Coromandel, a maioria das minas abandonadas tinham Argila.

<div style="width: 600px;">
 <a href="/assets/img/2020-07-25-P3-PLOT6-MAPA_MG_COMANDATEL_SUBSTANCIA_1_2.PNG"> <img src="/assets/img/2020-07-25-P3-PLOT6-MAPA_MG_COMANDATEL_SUBSTANCIA_1_2.PNG" width="480px"></a>
</div>

## Finalização

Se houve interesse em aprender a utilizar Python existem excelentes referências básicas. Mesmo usuários Windows são capazes de desenvolver ótimos projetos com boa autonomia. Por falar em autonomia, independente da linguagem a ser escolhida, a escolha deve proporcionar agilidade, rapidez na curva de aprendizagem, vasto recurso em termos de bibliotecas e fóruns, multiplataforma e obviamente suprir as necessidades de quem usa.

A partir do mapeamento feito diversas análises espaciais podem ser utilizadas para avaliação, estimativa, predição, interpretação e muito mais, trazendo novas perspectivas e ampliando o número de cenários na tomada de decisões.

Bom, se tu chegaste aqui, agradeço pelo interesse e aproveito para deixar meu muito obrigado e espero que o texto possa ajudar de alguma forma. Até o próximo. Ahh, não esquece de dar uma curtida na postagem. Valeu tchê!