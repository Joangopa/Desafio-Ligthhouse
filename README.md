# Desafio-Ligthhouse

## Instruções de Instalação

Para instalar os pacotes listados no `requirements.txt`, você precisa do Python 3.12.3 instalado em seu sistema.

1. **Instale Python 3.12.3** se ainda não o fez. Você pode baixá-lo em https://www.python.org/downloads/release/python-3123/.

2. **Certifique-se de que o `pip` está instalado e atualizado**:

   python -m ensurepip --upgrade

3. **Instale os pacotes usando o arquivo requirements.txt**:
    
    pip install -r requirements.txt


## Previsão da nota do imdb a partir dos dados.

A previsão da nota do IMDb pode ser tratada como um problema de regressão, uma vez que é um dado obtido pela média da valoração dada pelos usuários. Mas também poderia ser vista como um problema de classificação se considerarmos as classes como sendo intervalos onde a nota do IMDb pode ser alocada.

No nosso caso, iremos considerar a previsão da nota do IMDb como um problema de regressão e consideramos dois modelos de Machine Learning em particular: a Regressão Linear e o Random Forest Regressor.

Além destes dois modelos, consideramos dois grupos diferentes de variáveis a serem consideradas na implementação dos modelos. No primeiro grupo de variáveis, consideramos: o ano, a duração, o gênero, o Meta Score, o diretor, os atores principais, o número de votos e o faturamento do filme. Para o segundo grupo de variáveis, consideramos as variáveis do primeiro grupo, excetuando os atores principais.

A ideia de não considerar os atores principais dos filmes é que, ao considerar um novo filme para realizar uma predição, poderíamos ter atores que não façam parte de nossa base de dados. Situação que é menos provável de acontecer com os diretores de filme (ainda que possível).

Para o tratamento dos dados antes de considerar os modelos preditivos, consideramos os seguintes aspectos:

- Dados faltantes
- Variáveis categóricas


No caso dos dados faltantes, referimo-nos às colunas Meta_score e Gross. Para cada um dos filmes com estes dados faltantes, consideramos a média da respectiva variável (Meta_score ou Gross) dos filmes que obtiveram o mesmo rating IMDb, e preenchemos o dado faltante com esta média.

Para o tratamento das variáveis categóricas Director, Star1, Star2, Star3 e Star4, consideramos dicionários (um para os diretores e outro para os atores) nos quais a chave era dada pelo nome, e o valor por um índice único para cada nome. Assim, cada nome nestas variáveis foi substituído pelo respectivo valor obtido do dicionário correspondente.

Após considerar os modelos e transformações acima descritas, achamos que o modelo que melhor se aplicava aos dados foi a Regressão Linear, quando desconsideramos as variáveis dos atores principais do filme. Para isso, consideramos o erro quadrático médio e o parâmetro $R^2$. O primeiro mede o erro obtido ao comparar os valores reais e os valores preditos com os dados separados para teste. O segundo, o coeficiente de determinação, é uma medida estatística que indica quão bem os dados observados se ajustam a um modelo de regressão.