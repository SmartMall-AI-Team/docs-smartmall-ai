# Deploy da demonstração

## Estado verificável

Preparação implementada em 14/11/2026: backend com barreira de acesso, RLS, inicialização com migrações/seed e Blueprint do Render; frontend com configuração Vercel e entrada do código privado. Foram aprovados 54 testes do backend e 12 cenários de navegador com FastAPI/PostgreSQL reais em banco descartável, desktop e celular. Esses resultados são locais; não representam um ambiente público já publicado.

Backend e frontend foram integrados nos PRs [backend #5](https://github.com/SmartMall-AI/be-smartmall-ai/pull/5) e [frontend #4](https://github.com/SmartMall-AI/fe-smartmall-ai/pull/4), com checks aprovados. O [Actions do frontend](https://github.com/SmartMall-AI/fe-smartmall-ai/actions/runs/43603088430) repete os 12 cenários com o comando real de início do deploy.

O projeto exclusivo [smartmall-ai-demo no Supabase](https://supabase.com/dashboard/project/umvvwwbhoqkfhviwtqel) foi criado e está saudável, em `us-west-1`, PostgreSQL 17.11. Uma conexão privada com papel exclusivo `smartmall_demo_api` aplicou as migrações até `3c4e52d8a901` e o seed fictício. As cinco tabelas operacionais têm RLS habilitada e o seed contém uma ocorrência fictícia. O endereço do Session pooler foi conferido no painel: `aws-1-us-west-1.pooler.supabase.com:5432`. O projeto UniVerso existente foi preservado.

O papel da API não é superuser, não cria bancos/roles e recebeu somente uso/criação no schema público para possuir as tabelas da aplicação. A senha foi gerada no banco, transferida de forma privada para a sessão de preparação e o armazenamento temporário foi removido; não foi inserida em Git ou no texto das migrações.

O [plano Render](https://dashboard.render.com/blueprint/exs-dbs6n0u1egvs73d0448g/sync/exe-dbs6n361egvs73d04ap0) está preparado e ainda não foi aplicado: cria somente um serviço web gratuito no workspace confirmado pela liderança, sem adotar nem alterar serviços existentes. Vercel e a API ainda dependem da conclusão da configuração e da validação após publicação. Os endereços de exemplo abaixo não representam URLs publicadas.

## Arquitetura

Frontend Vercel → API FastAPI no Render → PostgreSQL Supabase. Somente o backend conhece `DATABASE_URL`. O código privado do ambiente fica no Render e é digitado pelos participantes na interface, nunca incorporado ao JavaScript publicado.

## Banco Supabase

1. Criar um projeto exclusivo para dados fictícios, na organização indicada pela liderança, verificando plano/custo antes de confirmar qualquer recurso pago.
2. No painel **Connect**, obter a URI do **Session pooler** se o ambiente da API usar IPv4. Copiar o host exato fornecido pelo painel. A URI deve usar TLS (`sslmode=require`) e senha codificada quando contiver caracteres reservados.
3. Guardar a URI em `DATABASE_URL` do Render. Não a colocar no frontend, Git, Trello ou logs.
4. As migrações Alembic são a fonte do schema. O comando de início da API aplica essas migrações antes de aceitar tráfego e habilita RLS sem políticas públicas nas cinco tabelas operacionais. A conexão privada da API deve ser o papel proprietário que executa as migrações; papéis públicos não conseguem ler/escrever os dados mesmo com grants de tabela. Isso bloqueia o acesso alternativo pela Data API do Supabase. Não adicionar políticas públicas para contornar essa proteção.

O backend atual usa SQLAlchemy/psycopg com conexão persistente; este guia usa pooling em modo sessão. Não substituir por pooling transacional sem validar prepared statements e bloqueios de sessão.

## API Render

Usar o `render.yaml` de `SmartMall-AI/be-smartmall-ai`, branch `main`, com plano gratuito. O serviço é novo e não deve adotar nem alterar aplicações existentes.

| Configuração | Valor |
| --- | --- |
| Python | 3.12, selecionado por `.python-version` |
| Build | `pip install uv==0.13.8 && uv sync --frozen --no-dev` |
| Start | `uv run --no-sync python -m app.deploy` |
| Health | `/health/ready` |
| APP_ENV | `demo` |
| AI_SIMULATION | `true` |
| DEMO_SEED | `true` |
| DEMO_ACCESS_TOKEN | Gerado no Render; ao menos 32 caracteres ASCII sem espaços |
| DATABASE_URL | URI privada do banco exclusivo, com TLS |
| CORS_ORIGINS | Origem HTTPS exata do frontend, sem caminho |

`app.deploy` serializa migrações e seed com bloqueio PostgreSQL e só depois inicia Uvicorn na porta `PORT`. O seed é fictício e idempotente; reiniciar preserva alterações já feitas. Falha de migração impede iniciar o servidor. O Blueprint solicita deploy automático apenas após os checks da branch passarem.

O Render gratuito pode suspender após 15 minutos sem tráfego e levar cerca de um minuto para retomar. Verificar o sistema antes da apresentação. O recurso de pre-deploy pago não é necessário para o comando acima.

## Frontend Vercel

Conectar somente `SmartMall-AI/fe-smartmall-ai`, usando a raiz desse repositório. HACKRUN é apenas a pasta agregadora local.

| Configuração | Valor |
| --- | --- |
| Framework | Vite |
| Node.js | 24 |
| Instalação | `npm ci` |
| Build | `npm run build` |
| Saída | `dist` |
| VITE_API_BASE_URL | `https://<endereço-real-da-api>/api/v1` |
| VITE_DEMO_ACCESS_REQUIRED | `true` |

Essas duas variáveis são públicas. Não criar `VITE_DEMO_ACCESS_TOKEN`, `VITE_DATABASE_URL` nem `VITE_OPENAI_API_KEY`. Alterar uma variável Vite exige novo build. Adicionar no CORS do backend somente as origens de produção/preview realmente usadas; não usar wildcard para todos os previews da Vercel.

## Acesso e limites

Em `APP_ENV=demo`, faltar código forte ou desabilitar a simulação impede a API de iniciar. Todas as rotas, inclusive Swagger e OpenAPI, exigem `Authorization: Bearer <código>`, exceto `/health`, `/health/ready` e preflights CORS. `GET /api/v1/access` permite validar o código sem consultar o banco. Código ausente/inválido retorna 401, com `WWW-Authenticate: Bearer`.

A interface valida o código antes de entrar, guarda-o somente na sessão da aba e o remove ao sair. A barreira é compartilhada e permite acesso completo aos registros fictícios; não implementa identidade individual, papéis autorizados, auditoria por pessoa nem isolamento entre lojistas. Use HTTPS e distribua o código somente aos participantes. Para revogar acessos, trocar o valor no Render e reiniciar o serviço.

O assessor de segurança do Supabase retornou somente cinco avisos informativos de RLS sem políticas. Isso é intencional: o acesso aos dados passa pela API privada, e os papéis públicos não devem obter políticas de leitura/escrita.

## Verificação após publicar

1. Conferir health e prontidão; consulta sem código deve retornar 401, sem conteúdo operacional.
2. Entrar com o código privado e um perfil fictício. Conferir erro com código inválido e remoção ao sair.
3. Criar uma ocorrência e encontrá-la após recarregar; solicitar análise e manter a indicação de simulação visível.
4. Revisar, criar tarefa com responsável/prazo, iniciar/concluir e resolver explicitamente. Conferir histórico e dashboard.
5. Repetir em celular e após um novo deploy, verificando que o banco preservou os registros.
6. Registrar URLs reais e evidências neste guia. Só então iniciar VAL-01 com participantes; testes automatizados não substituem sessões com usuários.

## Referências oficiais

- [Vite na Vercel](https://vercel.com/docs/frameworks/frontend/vite)
- [Blueprint e deploy após checks no Render](https://render.com/docs/blueprint-spec)
- [Versão Python no Render](https://render.com/docs/python-version)
- [Limites do Render gratuito](https://render.com/docs/free)
- [Conexões PostgreSQL do Supabase](https://supabase.com/docs/guides/database/connecting-to-postgres)
