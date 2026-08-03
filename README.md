# Dashboard — Metas e Resultados (Processual)

Dashboard do setor Processual do escritório Borges Macedo Advocacia, alimentado
em tempo real pela planilha do Google Sheets **"Metas e Resultados - Processual"**.

## Como funciona

- O dashboard lê a aba `Resultados Gerais - <Mês>/<Ano>` da planilha.
- Os dados são buscados no navegador a cada carregamento, com atualização
  automática a cada **5 minutos** (e também ao voltar para a aba do navegador).
- O seletor no topo permite alternar entre os meses disponíveis.
- Não há build nem servidor: é um único arquivo `index.html`.

## O que é exibido

| Seção | Conteúdo |
|---|---|
| Resumo | Métricas financeiras (alvarás, acordos, honorários) com velocímetro da meta |
| Metas do Mês | Um card por métrica com responsável, resultado, meta e meta proporcional |
| Visão Geral das Métricas | Tabela completa: métrica, responsável, resultado, % da meta, meta proporcional, meta do mês e média/dia |
| Desempenho vs. Meta Proporcional | Barras com o % atingido de cada métrica |
| Evolução dos Alvarás | Alvarás creditados mês a mês comparados à meta mensal |

As cores dos percentuais vêm da **formatação condicional da própria planilha**
(verde / amarelo / vermelho), lidas via API do Google Sheets. Sem a API, o
dashboard usa como critério 100% (verde), 70% (amarelo) e abaixo disso vermelho.

## Formatos de aba suportados

A planilha mudou de layout ao longo do tempo e o dashboard detecta os dois
automaticamente pelo cabeçalho:

- **Julho/2026 em diante:** `Métrica | Responsável | Resultado | % | Meta do Mês | Meta Proporcional | Média/dia`
- **Até Junho/2026:** `Métrica | Meta do Mês | Meta Proporcional | Resultado | % | Média/dia` (sem responsável)

## Configuração

Os parâmetros ficam no bloco `CONFIG`, no início do `<script>` do `index.html`:

| Campo | Descrição |
|---|---|
| `SHEET_ID` | ID da planilha do Google Sheets |
| `GOOGLE_API_KEY` | Chave da API do Google (usada para ler as cores das células) |
| `ABA_PREFIXO` | Prefixo do nome das abas mensais (`Resultados Gerais - `) |
| `PRIMEIRO_MES` | Primeiro mês disponível no seletor (`{ mes: 2, ano: 2026 }` = Março/2026) |
| `AUTO_REFRESH_MIN` | Intervalo da atualização automática, em minutos |

> A planilha precisa estar compartilhada como **"qualquer pessoa com o link pode ver"**
> para que o dashboard consiga lê-la.

## Publicação

O site é servido pelo GitHub Pages a partir da branch `main`, pasta raiz.
Qualquer alteração enviada para a `main` entra no ar em cerca de 1 minuto.
