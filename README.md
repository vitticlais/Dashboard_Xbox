# dashboard-xbox-game-pass

Dashboard interativo em **Excel** sobre as vendas de assinaturas do **Xbox Game Pass** em 2024: faturamento total, faturamento por auto renovação e vendas dos adicionais **EA Play Season Pass** e **Minecraft Season Pass**, com filtro por tipo de assinatura (mensal, trimestral ou anual).

**Arquivo:** [`dashboard-xbox-game-pass.xlsx`](dashboard-xbox-game-pass.xlsx)

![Dashboard](images/dashboard.png)

## Perguntas de negócio

| # | Pergunta | Onde aparece |
|---|---|---|
| 1 | Qual o faturamento total de vendas de planos (todas as assinaturas agregadas)? | Gráfico "Total Subscriptions Xbox Game Pass" |
| 2 | Qual o faturamento, separado por auto renovação e sem auto renovação? | Mesmo gráfico (barras Yes/No) |
| 3 | Qual o total de vendas de assinaturas do EA Play Season Pass? | Cartão "Total Subscriptions EA Play Season Pass" |
| 4 | Qual o total de vendas de assinaturas do Minecraft Season Pass? | Cartão "Total Subscriptions Minecraft Season Pass" |

Todos respondem ao filtro **Subscription Type** (segmentação de dados no dashboard).

## Dados utilizados

Aba `Bases` (oculta), tabela `Tabela1`, com **295 assinantes** e **13 colunas**, de 01/01/2024 a 16/12/2024. Os nomes são fictícios.

| Coluna | Descrição |
|---|---|
| Subscriber ID | Identificador único do assinante |
| Name | Nome do assinante |
| Plan | Core, Standard ou Ultimate |
| Start Date | Data de início da assinatura |
| Auto Renewal | Yes/No |
| Subscription Price | Preço do plano (Core R$ 5, Standard R$ 10, Ultimate R$ 15) |
| Subscription Type | Monthly, Quarterly ou Annual |
| EA Play Season Pass / Price | Contratou (Yes/No) e valor (`-` quando não contratou) |
| Minecraft Season Pass / Price | Contratou (Yes/No) e valor |
| Coupon Value | Desconto aplicado |
| Total Value | Plano + EA Play + Minecraft − cupom (conferido: bate em todas as 295 linhas) |

Distribuição: Core 101, Ultimate 98 e Standard 96 assinantes; Monthly 139, Quarterly 85 e Annual 71; auto renovação Yes 148 e No 147.

## Resultados por tipo de assinatura

Valores conferidos recalculando direto da base:

| Tipo | Faturamento total | Sem auto renovação | Com auto renovação | EA Play | Minecraft |
|---|---|---|---|---|---|
| Monthly | R$ 3.571 | R$ 2.824 | R$ 747 | R$ 1.350 | R$ 1.800 |
| Quarterly | R$ 2.308 | R$ 806 | R$ 1.502 | R$ 990 | R$ 1.140 |
| Annual | R$ 1.754 | R$ 217 | R$ 1.537 | R$ 600 | R$ 940 |
| **Todos** | **R$ 7.633** | R$ 3.847 | R$ 3.786 | R$ 2.940 | R$ 3.880 |

O EA Play é vendido só para o plano Ultimate; o Minecraft, para Standard e Ultimate.

## Estrutura da planilha

| Aba | Conteúdo |
|---|---|
| `Dashboard` (visível) | Painel final: título, cartões, gráfico e segmentação |
| `Cálculos` (oculta) | 3 tabelas dinâmicas que respondem às perguntas |
| `Bases` (oculta) | Dados de origem (`Tabela1`) |
| `Assets` (oculta) | Paleta de cores, logos e ícones usados no layout |

## Como reproduzir

1. **Base:** coloque os dados em uma aba e transforme em Tabela (`Ctrl+T`), chamada `Tabela1`.
2. **Tabelas dinâmicas** (Inserir → Tabela Dinâmica, a partir de `Tabela1`, na aba `Cálculos`):
   - `tbl_annual_total`: Linhas = `Auto Renewal`; Valores = Soma de `Total Value`; Filtro = `Subscription Type`.
   - `tbl_easeasonpass_total`: Linhas = `Plan`; Valores = Soma de `EA Play Season Pass Price`; Filtro = `Subscription Type`.
   - tabela do Minecraft: Linhas = `Plan`; Valores = Soma de `Minecraft Season Pass Price`; Filtro = `Subscription Type`.
3. **Valores dos cartões:** nas células `E25` e `E36` de `Cálculos`, `GETPIVOTDATA` busca o total de cada tabela (clique na célula do total ao digitar `=` para o Excel montar a fórmula).
4. **Gráfico:** com a primeira tabela dinâmica selecionada, insira um gráfico de colunas (Yes/No).
5. **Segmentação:** selecione uma tabela dinâmica → Análise de Tabela Dinâmica → Inserir Segmentação de Dados → `Subscription Type`. Em Relatório de Conexões, ligue a segmentação às **três** tabelas.
6. **Dashboard:** insira formas (retângulos arredondados) para os cartões. Para ligar uma forma a uma célula, selecione a forma, clique na barra de fórmulas e digite `=Cálculos!E25` (e `=Cálculos!E36` para o outro cartão). Acrescente logos, ícones e a paleta da aba `Assets`.
7. **Acabamento:** oculte linhas de grade e cabeçalhos de linha/coluna do dashboard, oculte as abas de apoio e deixe só o `Dashboard` visível.

## Como usar

Abra a aba `Dashboard` e clique em Monthly, Quarterly ou Annual na segmentação. Cartões e gráfico se atualizam. Para atualizar com dados novos, acrescente linhas à `Tabela1` e use Dados → Atualizar Tudo.

## O que aprendi

*(Escreva com suas palavras: tabelas dinâmicas, segmentação conectada a várias tabelas, formas ligadas a células, GETPIVOTDATA...)*
