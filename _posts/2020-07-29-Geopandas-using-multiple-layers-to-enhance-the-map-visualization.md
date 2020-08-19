---
layout: post
title:  "Geopandas using multiple layers to enhance the map visualization"
date: 2020-07-29 00:00:00
description: Usando múltiplas camadas para melhorar a visualização de mapas através de geopandas
img: 2020-07-29-capa-geopandas.jpg # Add image post (optional)
fig-caption: Photo from Unsplash.com # Add figcaption (optional)
tags: [Mining, Dataset, Geocoding, Visualization]
categories: [Mining, Dataset, Geocoding, Visualization]
---

Mesmo usando os comandos e procedimentos certos, nem sempre se consegue obter os melhores mapas com a riqueza de detalhes que o projeto exige. Por isso é importante usar certos truques e/ou recursos adicionais para obter o máximo de uma aplicação.

##Dataset:
Quanto mais variadas forem as bases de dados que temos para trabalhar, maior serão nossos desafios e, consequentemente, mais aprenderemos. Sendo assim, trago uma base bem interessante que é a `Massa d'Água da Região Atlântico Sul` localizada no [PORTAL BRASILEIRO DE DADOS ABERTOS]( http://dados.gov.br/dataset/massa-dagua-da-regiao-atlantico-sul). Nele constam todas (ou quase) as massas de água do Rio Grande do Sul, com arquivos nos formatos KML, GeoJSON, CSV, shapefile e outros. Os arquivos possuem diversos atributos como `ID`, `shape_Leng`, `shape_Area`, `Geometry` e muito mais.

##Projeto:
Digamos que queremos visualizar estruturas com dimensões onde a maior seja milhares vezes maior que a menor num simples gráfico 2D sem nenhum recurso de zoom. Imediatamente, vê-se que algumas dessas estruturas vão ficar invisíveis. Sem usar zoom, a solução seria plotar o mapa por partes para visualizar o máximo ou tentar intensificar cada estrutura.

Para exemplificar melhor, a Figura 1 mostra o mapa das massas de água Atlântico Sul, do Rio Grande do Sul. Vê-se que há diferença considerável entre os tamanhos das massas de água e, que as menores são quase imperceptíveis. 

<div style="width: 600px;">
 <a href="/assets/img/2020-08/2020-07-29-FIG1.png"> <img src="/assets/img/2020-08/2020-07-29-FIG1.png" width="480px"></a>
</div>
**Figura1**

Uma alternativa para tentar melhor a visualização seria traçar as bordas de cada estrutura. Para isso deixaríamos a cor da massa de água transparente, para o contorno se sobressair. Aplicando o comando para realizar a tarefa, ficaria `arquivo.plot(facecolor=”none”, edgecolor=”blue”)`. Contudo, isso causaria uma certa confusão, pois os argumentos `“none”` e `None` são diferentes quando se usa `“facecolor”`, eles têm funções opostas. O melhor procedimento é usar `arquivo.boundary.plot()`. Este contexto é mais explícito e claro para o módulo de plotagem. A Figura 2 exemplifica o resultado da operação. Ainda assim, não parece um resultado muito bom, pois massas de água pequenas ou sinuosas parecem estar preenchidas e não é possível fazer distinção entre estruturas muito próximas.

<div style="width: 600px;">
 <a href="/assets/img/2020-08/2020-07-29-FIG2.png"> <img src="/assets/img/2020-08/2020-07-29-FIG2.png" width="480px"></a>
</div>
**Figura2**

## Melhorando o resultado
Bom, o meu truque para intensificar a visualização é usar múltiplas camadas. Usaremos uma camada para o contorno e outra para o preenchimento. Quando se usa múltiplas camadas, usa-se `zorder` para controlar a ordem em que as camadas aparecem e, aí vem a segunda parte do truque que é ordenar de forma correta as camadas, pois se ordenar errado o preenchimento fica por baixo e não aparecerá. A terceira parte, que é opcional, é adicionar cor variável as massas de água, a variação pode estar relacionada ao ID da estrutura ou ao tamanho. A Figura 3 mostra o resultado. Melhor, né?

<div style="width: 600px;">
 <a href="/assets/img/2020-08/2020-07-29-FIG3.png"> <img src="/assets/img/2020-08/2020-07-29-FIG3.png" width="480px"></a>
</div>
**Figura3**

## Código completo
```python
import pandas as pd
import geopandas as gpd
import matplotlib.pyplot as plt

gdf = gpd.read_file('DATA_SETS\MASSAS_DAGUA\Atlantico_Sul.shp')
gdf = gdf.dropna()
gdf.shape
gdf.head()
# Figura 1
gdf.plot(figsize=(14, 8));

# Figura 2
gdf.boundary.plot(figsize=(14, 8));

# Figura 3
ax = gdf.plot(figsize=(14, 8), column='objectid', cmap='brg', zorder=2)
gdf.boundary.plot(ax=ax, zorder=1);
```

## Conclusão
Para quem está iniciando com Geopandas e mapeamento é importante ter em mente que sempre tem mais de uma maneira de fazer as coisas. Deixe que a imaginação seja a válvula propulsora e Python, o fio condutor, proporcionando uma infinidade de ferramentas para materializar o que a mente idealizar.
