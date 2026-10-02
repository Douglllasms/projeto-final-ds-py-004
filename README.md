## Fonte dos dados

Os dados utilizados neste projeto têm origem no
Sistema de Operações do Crédito Rural e do Proagro (SICOR),
mantido pelo Banco Central do Brasil (BCB).

O SICOR reúne informações sobre as operações de crédito rural
registradas pelas instituições financeiras no Brasil.

Fonte oficial:
Banco Central do Brasil — Crédito Rural / SICOR

https://www.bcb.gov.br/estabilidadefinanceira/micrrural

Para acesso e extração dos microdados, foi utilizada a plataforma
Base dos Dados, por meio do Google BigQuery.

Conjunto de dados:
Microdados do Sistema de Operações do Crédito Rural e do Proagro (SICOR)

https://basedosdados.org/dataset/544c9d22-97b7-479a-8eca-94762840b465

## Recorte da análise

Para reduzir o volume de dados e tornar a análise compatível com
o escopo do projeto, foi definido o seguinte recorte:

- Ano de emissão: 2025
- Cobertura geográfica: Brasil
- Unidades da Federação: 27
- Fonte: SICOR / Banco Central do Brasil
- Forma de acesso: Base dos Dados / Google BigQuery

## Tabelas utilizadas

Foram utilizadas duas tabelas do conjunto
`basedosdados.br_bcb_sicor`.

### 1. operacao

Tabela:
`basedosdados.br_bcb_sicor.operacao`

Contém os registros das operações de crédito rural.

Foi aplicado o filtro:

`ano_emissao = 2025`

O resultado utilizado no projeto possui:

- 2.442.343 registros
- 15 colunas

Arquivo gerado:

`operacao_2025.csv`

### 2. empreendimento

Tabela:
`basedosdados.br_bcb_sicor.empreendimento`

A tabela funciona como um catálogo das características dos
empreendimentos financiados.

Foram selecionados apenas os empreendimentos relacionados às
operações emitidas em 2025.

O resultado possui:

- 1.050 registros
- 10 colunas

Arquivo gerado:

`empreendimento_2025.csv`

## Relacionamento entre as tabelas

As tabelas `operacao` e `empreendimento` serão relacionadas pelo campo:

`id_empreendimento`

Antes da união, foi verificada a integridade da chave na tabela
de empreendimentos utilizada no projeto:

- total de registros: 1.050
- IDs de empreendimento distintos: 1.050

Portanto, cada `id_empreendimento` utilizado no recorte possui
um único registro na tabela de empreendimentos.

## Estratégia de preparação

As duas tabelas foram extraídas separadamente.

A união dos dados não foi realizada no BigQuery, pois o projeto
exige a utilização de `merge` com Pandas.

Dessa forma, o relacionamento entre as bases será realizado
durante a etapa de análise e transformação no notebook Python,
permitindo também verificar a quantidade de registros antes e
depois da união.
