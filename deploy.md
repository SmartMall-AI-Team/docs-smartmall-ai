# Deploy da demonstração

## Estado verificável

Demonstração publicada em 14/11/2026: [frontend Vercel](https://smartmall-ai-demo.vercel.app) e [API Render](https://smartmall-ai-demo-api-8mez.onrender.com/health/ready), com PostgreSQL Supabase e IA explicitamente simulada. Por solicitação posterior da liderança, o código de acesso foi dispensado; o login dos perfis fictícios permanece. As evidências iniciais abaixo foram obtidas antes dessa alteração.

A remoção foi integrada no [backend #8](https://github.com/SmartMall-AI/be-smartmall-ai/pull/8), com 55 testes aprovados e check obrigatório aprovado. O deploy Render `dep-dbs7dlbbc2fs73apjom0` ficou `live` no commit `50aa769d5f3382c05d490506119a8e3a6e47a737`; o rebuild Vercel `dpl_37WSXub1dr8xfFpTv59uh2vtvvAj` ficou `READY` com `VITE_DEMO_ACCESS_REQUIRED=false`. A verificação publicada aprovou ausência do campo, login e recarga em desktop e celular, além de consulta operacional sem Authorization retornando 200 com `Cache-Control: no-store` e `/api/v1/access` indicando `false`.

Backend e frontend foram integrados nos PRs [backend #5](https://github.com/SmartMall-AI/be-smartmall-ai/pull/5) e [frontend #4](https://github.com/SmartMall-AI/fe-smartmall-ai/pull/4), com checks aprovados. O [Actions do frontend](https://github.com/SmartMall-AI/fe-smartmall-ai/actions/runs/43603088430) repete os 12 cenários com o comando real de início do deploy.

O projeto exclusivo [smartmall-ai-demo no Supabase](https://supabase.com/dashboard/project/umvvwwbhoqkfhviwtqel) está saudável, em `us-west-1`, PostgreSQL 17.11. Uma conexão privada com papel exclusivo `smartmall_demo_api` aplicou as migrações até `3c4e52d8a901` e o seed fictício inicial, com uma ocorrência. As cinco tabelas operacionais têm RLS habilitada. Os testes posteriores criam registros fictícios adicionais. O endereço do Session pooler foi conferido no painel: `aws-1-us-west-1.pooler.supabase.com:5432`. O projeto UniVerso existente foi preservado.

O papel da API não é superuser, não cria bancos/roles e recebeu somente uso/criação no schema público para possuir as tabelas da aplicação. A senha foi gerada no banco, transferida de forma privada para a sessão de preparação e o armazenamento temporário foi removido; não foi inserida em Git ou no texto das migrações.

O [plano Render](https://dashboard.render.com/blueprint/exs-dbs6n0u1egvs73d0448g/sync/exe-dbs6n361egvs73d04ap0) foi aprovado pela liderança e aplicado: criou somente o serviço web gratuito `smartmall-ai-demo-api-8mez`, sem adotar nem alterar serviços existentes. O [serviço da API](https://dashboard.render.com/web/srv-dbs6r4c9v7es73bs0d5g) teve o deploy verificado `dep-dbs6rnrbc2fs73ao1kv0`, commit `7c9ec22811e56649a01074575e823300542bcf5f`, concluído em `live`. A infraestrutura do Blueprint fica em aprovação manual.

**Decisão posterior da liderança em 14/11/2026:** manter o backend com deploy manual por enquanto. A inspeção identificou que o aplicativo Render estava instalado na CHSRC, mas não na SmartMall-AI; a instalação nessa organização foi adiada pelo usuário. `autoDeployTrigger` foi alterado para `off` no serviço e no Blueprint. Isso não muda o deploy automático do frontend Vercel, que foi verificado após o merge do README na main.

O [projeto Vercel](https://vercel.com/contasjoaoneto-6902/smartmall-ai-demo) está conectado ao repositório `SmartMall-AI/fe-smartmall-ai`, com Node.js 24 e as variáveis públicas corretas. O primeiro deploy verificado `dpl_FiCuLPFfESZzz1wXzkNDsjtdyhpv` terminou em `READY`, publicado a partir do commit `4a72f9a12c9529458f1ee220745db0ca0f976b07`. A dificuldade inicial de vínculo GitHub foi resolvida; a publicação usa o repositório, não um upload manual de arquivos. A origem de produção está autorizada no CORS; previews não foram configurados como ambientes integrados independentes.

Verificação HTTP externa: frontend 200, prontidão da API/banco 200, consulta operacional sem código 401 e validação do código 200 com CORS restrito à origem de produção e `Cache-Control: no-store`. O código privado foi entregue fora dos repositórios e não aparece neste documento.

Os 12 cenários Playwright também passaram contra os endereços publicados, em 1,5 minuto: seis fluxos em desktop e celular. Cobrem persistência após recarga, revisão, tarefa/prazo/status, encerramento bloqueado, equipamentos, indicadores, recuperação de rede e validação/remoção do código. A falha de IA e a interrupção de rede são induzidas no navegador; a análise bem-sucedida continua simulada. Esses testes não representam sessões VAL-01 com usuários.

## Arquitetura

Frontend Vercel → API FastAPI no Render → PostgreSQL Supabase. Somente o backend conhece `DATABASE_URL`. A demonstração dispensa código de acesso.

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
| DEMO_ACCESS_TOKEN | Vazio; demonstração sem código de acesso |
| DATABASE_URL | URI privada do banco exclusivo, com TLS |
| CORS_ORIGINS | Origem HTTPS exata do frontend, sem caminho |

`app.deploy` serializa migrações e seed com bloqueio PostgreSQL e só depois inicia Uvicorn na porta `PORT`. O seed é fictício e idempotente; reiniciar preserva alterações já feitas. Falha de migração impede iniciar o servidor. Antes de um deploy manual, conferir o commit da main e o check obrigatório `check`; depois acionar **Manual Deploy → Deploy latest commit** no serviço e aguardar `live` e prontidão 200. Não usar deploy de commit específico para substituir a main sem alinhamento.

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
| VITE_DEMO_ACCESS_REQUIRED | `false` |

Essas duas variáveis são públicas. Não criar `VITE_DEMO_ACCESS_TOKEN`, `VITE_DATABASE_URL` nem `VITE_OPENAI_API_KEY`. Alterar uma variável Vite exige novo build. Adicionar no CORS do backend somente as origens de produção/preview realmente usadas; não usar wildcard para todos os previews da Vercel.

## Acesso e limites

Em `APP_ENV=demo`, a simulação de IA continua obrigatória, mas `DEMO_ACCESS_TOKEN` pode ficar vazio. Nesse caso, as rotas dispensam código e `GET /api/v1/access` retorna `{"access_required":false}`. As respostas da demonstração mantêm `Cache-Control: no-store`.

Com `VITE_DEMO_ACCESS_REQUIRED=false`, a interface mostra somente o login dos perfis fictícios, sem campo de código. Não há identidade individual, papéis autorizados, auditoria por pessoa nem isolamento entre lojistas. Se o código opcional for reativado, configurar também o frontend e publicar novamente.

O assessor de segurança do Supabase retornou somente cinco avisos informativos de RLS sem políticas. Isso é intencional: o acesso ao banco passa pela conexão privada da API, e os papéis públicos não devem obter políticas de leitura/escrita.

## Verificação após publicar

1. Conferir health e prontidão; consulta operacional sem código deve retornar 200 e `/api/v1/access` deve indicar `false`.
2. Conferir ausência do campo de código e entrar com um perfil fictício.
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
