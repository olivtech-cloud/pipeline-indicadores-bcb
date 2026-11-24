# pipeline-indicadores-bcb

Pipeline diário com Databricks, Delta Lake e API do Banco Central (Selic e dólar).

## O problema
Coletar todo dia a Selic e o dólar e manter um histórico confiável numa tabela Delta, sem duplicar dados.

## Como funciona
1. Busca as séries da Selic e do dólar na API do Banco Central (últimos 20 dias úteis)
2. Converte os tipos (data e número) e junta as duas séries pela data
3. Faz checagens de qualidade: tabela não vazia, sem nulos, sem datas duplicadas e dólar maior que zero
4. Atualiza a tabela Delta com MERGE, sem duplicar linhas
5. Roda todo dia em um job agendado do Databricks, com alerta por email em caso de falha
6. Avisa quando o dólar varia 4% ou mais de um dia pro outro

## Tecnologias
Python, SQL, PySpark, Databricks, Delta Lake

## Status
Em desenvolvimento.
