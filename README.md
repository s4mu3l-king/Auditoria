# Auditoria de Conferência — V2 Online

## Objetivo

Versão simples para publicar como site estático no GitHub Pages e gravar as auditorias online em Supabase.

### Por que mudou?
O Excel não é uma boa camada de gravação simultânea para vários usuários diretamente de um site estático. Nesta V2, o Excel é usado para carga/relatório e o banco online guarda as alterações em tempo real. Isso evita que dois usuários sobrescrevam a mesma planilha.

GitHub Pages hospeda HTML/CSS/JS estático; Supabase fornece banco e API para leitura/gravação pelo navegador.

## Arquivos

- `index.html` — aplicativo inteiro.
- `sql/01_criar_banco.sql` — cria as tabelas e políticas.
- `README.md` — instruções.

## Passo a passo

1. Crie uma conta/projeto no Supabase.
2. Abra o SQL Editor.
3. Cole o conteúdo de `sql/01_criar_banco.sql`.
4. Execute.
5. No projeto Supabase, copie a Project URL e a Publishable Key.
6. Abra `index.html` e substitua:
   `COLE_SUA_URL`
   `COLE_SUA_PUBLISHABLE_KEY`
7. Crie um repositório no GitHub.
8. Envie `index.html` e a pasta `sql`.
9. Ative GitHub Pages.
10. Acesse o link publicado.

## Importação do Excel

A V2 inicial deixa a gravação online pronta. A importação automática do Excel/OneDrive deve ser feita como etapa administrativa, para não permitir que um usuário substitua a base por engano.

## Segurança

As policies SQL desta primeira versão são deliberadamente simples para facilitar o primeiro teste. Antes de produção, configure Supabase Auth e restrinja as policies por usuário/empresa.

## Regras de negócio

- Acuracidade = lotes validados / lotes auditados * 100.
- QTD SISTEMA > 0 e sem QTD FÍSICA = pendente.
- QTD SISTEMA = 0 não entra como pendente.
- Um lote com QTD SISTEMA = 0 pode ser auditado quando QTD FÍSICA > 0.
- Igualdade QTD FÍSICA x QTD SISTEMA = VALIDADO.
- Diferença = DIVERGÊNCIA.
- QTD FÍSICA > 0 sem QTD SISTEMA = VERIFICAR QUANTIDADE SISTÊMICA NÃO CONSTA.
