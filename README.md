# Auditoria V2 — versão final baseada no Excel real

Esta versão usa a aba **Resultados** da planilha real como referência. Foram encontrados 27 campos e 663 lotes únicos em 2.551 registros históricos com lote.

## O que fazer no Supabase

1. Como as tabelas antigas ainda devem estar vazias, abra SQL Editor.
2. Execute `sql/01_recriar_estrutura_real.sql`.
3. No Table Editor, abra `base_dados` e importe `dados/base_dados.csv`.
4. Abra `auditorias` e importe `dados/auditorias_historico.csv`.
5. Confira se os dados apareceram.

> Se você já tiver colocado dados novos nas tabelas antigas, NÃO execute o script de recriação sem falar comigo, pois ele apaga essas duas tabelas para corrigir a estrutura.

## GitHub

Substitua o `index.html` do seu repositório pelo `index.html` deste pacote e faça commit/push.

O arquivo já está configurado com a Project URL e a Publishable Key que você forneceu. A Publishable Key é própria para uso no frontend; ainda assim, a segurança real deve ser feita pelas RLS/Auth antes de uso amplo.

## Regra

- Acuracidade = lotes validados / lotes auditados × 100.
- QTD SISTEMA > 0 e sem auditoria na data = pendente.
- QTD SISTEMA = 0 não é pendente.
- Um lote com QTD SISTEMA = 0 pode ser conferido quando QTD FÍSICA > 0.
- QTD FÍSICA diferente da QTD SISTEMA = DIVERGÊNCIA.
- CAT/etiqueta podem gerar divergência.
