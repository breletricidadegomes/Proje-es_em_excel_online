![Excel Online](https://img.shields.io/badge/Excel%20Online-217346?style=flat&logo=microsoftexcel&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)
# Automação de Projeção de Séries Temporais (Office Script)

Script em **TypeScript para Office Scripts (Excel Online / Power Automate)** que gera projeções futuras de indicadores mensais a partir de um histórico armazenado em tabela do Excel, usando regressão linear (`FORECAST.LINEAR`).

## O que o script faz

1. **Limpa projeções anteriores**: remove linhas marcadas com uma cor de destaque (indicando que foram geradas automaticamente), preservando o histórico real.
2. **Gera novos períodos**: a partir de um parâmetro configurável em uma célula (quantidade de meses a projetar), cria novas linhas na tabela com competência (ano/mês) sequencial.
3. **Calcula a projeção**: aplica `FORECAST.LINEAR` sobre o histórico de duas métricas (ex.: volume e uma taxa/indicador), usando a competência como variável independente.
4. **Atualiza gráficos dinamicamente**: ajusta o intervalo de dados e o eixo de categorias de dois gráficos do Excel para refletir automaticamente o novo tamanho da série (histórico + projeção).

## Como funciona o controle

Uma pequena tabela auxiliar na planilha funciona como "painel de controle":

| Campo | Descrição |
|---|---|
| Ação | `"Sim"` para gerar novas projeções, `"Apagar"` para apenas limpar as existentes |
| Períodos a mais | Quantidade de meses futuros a projetar |

Um botão vinculado ao script (via Power Automate ou botão de macro no Excel) dispara a execução.

## Estrutura esperada da tabela de dados

A tabela principal deve conter, nesta ordem, colunas equivalentes a:

`competência | ano | mês | métrica_1 | métrica_2 | projeção_métrica_1 | projeção_métrica_2`

## Requisitos

- Excel com suporte a **Office Scripts** (Microsoft 365 / Excel Online).
- Duas tabelas nomeadas: uma com o histórico/projeções e outra com os parâmetros de controle.
- Dois gráficos nomeados na planilha, com séries identificadas por nome (ex.: "Volume", "Projeção", etc.).

## Limitações conhecidas

- Os nomes das tabelas, gráficos e endereços de célula são fixos no código; para reaproveitar em outra planilha, ajuste esses identificadores.
- A projeção usa regressão linear simples — adequada para tendências aproximadamente lineares, não para sazonalidade complexa.

## Licença

MIT — sinta-se livre para usar, adaptar e distribuir.
