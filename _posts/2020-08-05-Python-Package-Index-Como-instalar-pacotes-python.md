---
layout: post
title:  "Python Package Index Como instalar pacotes python"
date: 2020-08-05 00:00:00
description: Como instalar pacotes em Python com Python Package Index (pypi)
img: 2020-08-05-capa-christina-wocintechchat.com-unsplash.jpg # Add image post (optional)
fig-caption: Photo by Christina @wocintechchat.com from Unsplash.com # Add figcaption (optional)
tags: [Mining, Dataset, Geocoding, Visualization]
categories: [Mining, Dataset, Geocoding, Visualization]
---

Python Package Index, popularmente conhecido como Pypi é onde os pacotes feitos por terceiros são armazenados, ou seja, é o repositório oficial de aplicações escritas em python. Pypi te ajuda a buscar, instalar e publicar pacotes codificados em Python tendo sidos desenvolvidos e compartilhados pela Python Community (galera que faz a felicidade dos programadores – tudo que tu pensares, lá tem, se não tem tu podes desenvolver e armazenar lá – simples assim).

<div style="width: 600px;">
 <a href="/assets/img/2020-08/2020-08-05-pypi.png"> <img src="/assets/img/2020-08/2020-08-05-pypi.png" width="480px"></a>
</div>
Photo by AllGo - An App For Plus Size People -on Unsplash.

##Aqui vai umas dicas para usar o Pypi
Primeiro: é sempre bom já ter o Python instalado e saber qual versão está rodando. Para isso, vá para a linha de comando é digite:
```python
python –version

O retorno será algo como:
```python
Python 3.x.y

`X` e `Y` serão a complementação da versão instalada, por exemplo, `python 3.8.0`.
Isso se tu instalaste a última versão. Se não tens python instalado, instale a última versão que estará disponível em [python.org] (https://python.org/).

Segundo: já com Python funcionando, tu precisaras do pip instalado (pip é a ferramenta mais pop para instalar os pacotes python, sem ela, não rola, literalmente). Na linha de comando digite:
```python
pip --version

Se não tem pip, digite:
```python
python -m ensurepip --default-pip

Se ainda não der digite:
```python
python get-pip.py

Às vezes é preciso instalar arquivos a partir da fonte, então para fazer um trabalho mais completo digite:
```python
python -m pip install --upgrade pip setuptools wheel

Bom, agora deve funcionar.

Outro procedimento que sempre é indicado seria Criar um Ambiente Virtual, mas isso fica para outro post.

Ok, voltando a instalação de pacotes via Pypi, o mais comum é usar o pip para instalar os pacotes armazenados no Pypi.
Para instalar a versão mais recente de algum pacote digite:
```python
pip install “NomedoPacote”

Para instalar uma versão específica, digite:
```python
pip install “NomedoPacote==1.2”

Para instalar uma versão maior ou igual a uma versão e menor que outra, digite:
```python
pip install “NomedoPacote>=1.5, <2”

Para instalar uma versão que é compatível com certa versão, digite:
```python
pip install “NomedoPacote~=1.5.2”

Para fazer upgrade de um pacote, digite:
```python
pip install --upgrade “NomedoPacote”

É isso, caso alguma dúvida persista consulte [https://packaging.python.org/tutorials/installing-packages/]( https://packaging.python.org/tutorials/installing-packages/)
