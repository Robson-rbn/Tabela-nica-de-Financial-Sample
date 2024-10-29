## Instruções de Entrega do Desafio

Utilizaremos a tabela única de Financial Sample para criar as tabelas dimensão e fato do nosso modelo baseado em star schema.

O processo consiste na criação das tabelas com base na tabela original. A partir da cópia serão selecionadas as colunas que irão compor a visão da nova tabela. Sendo assim, a partir da tabela principal serão criadas as tabelas:

Financials_origem (modo oculto – backup)

D_Produtos (ID_produto, Produto, Média de Unidades Vendidas, Médias do valor de vendas, Mediana do valor de vendas, Valor máximo de Venda, Valor mínimo de Venda)

D_Produtos_Detalhes(ID_produtos, Discount Band, Sale Price, Units Sold, Manufactoring Price)

D_Descontos (ID_produto, Discount, Discount Band)

D_Detalhes (*)

D_Calendário – Criada por DAX com calendar()

F_Vendas (SK_ID , ID_Produto, Produto, Units Sold, Sales Price, Discount Band, Segment, Country, Salers, Profit, Date (campos))

*Verifique as informações que não foram contempladas nas demais tabelas dimensão que fornecem maiores detalhes sobre vendas.
______________________________________________________________________________________________________________________________________________

## Ações Realizadas:

_Foram criadas 5 tabelas dimensões e 1 tabela fato, derivadas da tabela "financials_origem":

- D_Produtos
- D_Detalhes
- D_Produtos_Detalhes
- D_Descontos
- F_Vendas
- D_Data

A tabela D_Data foi criada utilizando DAX:

- D_Date = CALENDARAUTO(12)

- Coluna Ano

  Ano = YEAR(D_Date[Date])

- Coluna Número Mês

    Número Mês = MONTH(D_Date[Date])

- Coluna Nome Mês

    Nome Mês = FORMAT(DATE(1, D_Date[Número Mês], 1), "MMM")

- Coluna Número Dia Semana

    Número Dia Semana = WEEKDAY(D_Date[Date])

- Coluna Nome Dia Semana

    Nome Dia Semana = FORMAT(D_Date[Date], "DDDD")
  

_Para adicionar a relação entre D_Detalhes e F_Vendas foi gerado um índice condicional com base nas colunas Produto, Segmento, País e Vendas.
_Para estabelecer a relação entre D_Date e F_Vendas, o Data de ambos foi deixado em formato short date e, no model view se arrastou o Data de F_Vendas até o Date de D_Date.
_Foram removidos as colunas com datas de F_Vendas e D_Detalhes.
