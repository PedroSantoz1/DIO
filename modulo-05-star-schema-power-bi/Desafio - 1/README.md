# Star Schema Financeiro no Power BI

Modelo dimensional criado no Power BI a partir da planilha **Financial Sample.xlsx** da formação Power BI Analyst da DIO.

## Arquivos

- [`star-schema-financial-sample.pbix`](star-schema-financial-sample.pbix): modelo editável no Power BI Desktop.
- [`Financial Sample.xlsx`](Financial%20Sample.xlsx): planilha usada como fonte.
- [`modelo-star-schema.png`](modelo-star-schema.png): captura da exibição Modelo.

## Estrutura do modelo

A tabela fato `F_Vendas` mantém os 700 registros da planilha e os valores para análise, como unidades vendidas, vendas, descontos, custo e lucro. `ID_Registro` identifica cada linha da fato. A consulta `Financials_Origem` foi mantida como fonte de transformação, com a carga desabilitada.

| Dimensão | Chave de relacionamento | Valores distintos na origem |
| --- | --- | ---: |
| `D_Produto` | `Product` | 6 |
| `D_Pais` | `Country` | 5 |
| `D_Segmento` | `Segment` | 5 |
| `D_Desconto` | `Discount Band` | 4 |
| `D_Data` | `Date` | Calendário diário |

Todas as dimensões se relacionam diretamente com `F_Vendas` em cardinalidade **1 para muitos**. `D_Data` foi criada com `CALENDARAUTO()`, marcada como tabela de datas e inclui `Ano`, `Mes` e `MesNumero`.

## Transformações realizadas

1. Importação da planilha no Power Query como `Financials_Origem`.
2. Correção do cabeçalho ` Sales` para `Sales`.
3. Criação de `F_Vendas` e das dimensões como referências da consulta de origem.
4. Remoção de duplicatas nas dimensões de produto, país, segmento e desconto.
5. Remoção de `Month Number`, `Month Name` e `Year` da fato, mantendo `Date` para o relacionamento com o calendário.
6. Criação dos relacionamentos entre as dimensões e a fato na exibição Modelo.

## Fonte dos dados

Planilha e exemplo de referência disponíveis no [repositório Power BI Analyst de Juliana Zanelatto](https://github.com/julianazanelatto/power_bi_analyst/tree/main/M%C3%B3dulo%204/Desafios%20de%20Projeto).

As datas da planilha representam meses e estão registradas no primeiro dia de cada mês. Assim, os resultados por `Date` refletem a granularidade mensal dos dados de origem.

Ao abrir o `.pbix` em outro computador, os dados já salvos no arquivo podem ser vistos. Para **atualizar** a consulta, ajuste o caminho do arquivo Excel na etapa `Fonte` de `Financials_Origem` para a planilha `Financial Sample.xlsx` no local onde o repositório foi baixado.
