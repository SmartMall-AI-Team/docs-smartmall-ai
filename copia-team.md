# Cópia independente — SmartMall-AI-Team

Preparada em 14/11/2026 a pedido de João Geraldo, com administração pelo perfil [Setezin7](https://github.com/Setezin7).

## Estrutura

Os três repositórios permanecem separados e públicos: [backend](https://github.com/SmartMall-AI-Team/be-smartmall-ai), [frontend](https://github.com/SmartMall-AI-Team/fe-smartmall-ai) e [documentação](https://github.com/SmartMall-AI-Team/docs-smartmall-ai). Não há um monorepo agregador publicado.

A cópia parte das branches `main` disponíveis no workspace original. O histórico Git e as autorias foram preservados; mudanças de identificação, links atuais e CI são commits novos. CODEOWNERS e revisão passam a apontar para `@Setezin7`. O workflow do frontend consulta o backend da nova organização e mantém o SHA fixado já usado na origem.

| Repositório | Commit da origem preservado |
| --- | --- |
| Backend | `50aa769` |
| Frontend | `104fe4c` |
| Documentação | `0b36ce7` |

## O que não é transferido com Git

- Pull requests, issues, aprovações, números de execuções e logs antigos do GitHub Actions. Links específicos para esses registros continuam apontando à origem; os novos repositórios terão registros próprios.
- Membros e convites de colaboradores. As pessoas não recebem acesso automaticamente; a liderança precisa confirmar quem participará da nova organização.
- Recursos e configurações de Vercel, Render e Supabase. As URLs presentes nos documentos continuam sendo o ambiente anterior e não comprovam publicação da cópia. Não foram criados recursos pagos nem alterado o ambiente existente.
- Trello e Miro. Os links referem-se aos quadros anteriores e seu acesso continua independente do GitHub.
- `.env`, chaves de IA, credenciais de banco, dados locais, ambientes virtuais e dependências instaladas.

Os arquivos de execução e deploy são mantidos para reprodução. Para um ambiente novo, usar `.env.example`, banco exclusivo e novas configurações dos serviços. Não reutilizar credenciais do ambiente anterior automaticamente.

## Evidências anteriores e verificação atual

Os documentos de entrega conservam resultados obtidos na origem, com suas datas e links originais. Esses números não representam uma execução nova na organização Team7. O código funcional não foi reimplementado ou apresentado com autoria diferente.

## Publicação e verificações desta cópia

Os três repositórios foram criados **públicos**, com branch padrão `main`, na organização [SmartMall-AI-Team](https://github.com/SmartMall-AI-Team). Setezin7 foi verificado como membro administrador ativo e único proprietário. A permissão base é leitura; somente proprietários podem criar repositórios.

| Repositório | Entrega e verificação na nova organização |
| --- | --- |
| Backend | [PR #1](https://github.com/SmartMall-AI-Team/be-smartmall-ai/pull/1) integrado; [55 testes aprovados no CI](https://github.com/SmartMall-AI-Team/be-smartmall-ai/actions/runs/43630462244) |
| Frontend | [PR #1](https://github.com/SmartMall-AI-Team/fe-smartmall-ai/pull/1) integrado; build e [12 cenários Playwright aprovados](https://github.com/SmartMall-AI-Team/fe-smartmall-ai/actions/runs/43630474360) |
| Documentação | [PR #1](https://github.com/SmartMall-AI-Team/docs-smartmall-ai/pull/1); links Markdown locais e arquivos revisados |

Proteções configuradas nos três repositórios: uma aprovação e revisão de CODEOWNERS, descarte de aprovações após novos commits, conversas resolvidas, proteção incluindo administradores, bloqueio de force push e exclusão da main. A integração é restrita a `Setezin7`. A exceção nominal permite ao líder integrar PRs próprios, preservando checks obrigatórios; não houve revisão independente desta cópia.

No backend, `check` do GitHub Actions é obrigatório e a branch precisa estar atualizada. O frontend executa CI com API e banco descartáveis; seu check foi verificado para esta integração, mas não é obrigatório na proteção, seguindo a política da origem. Documentação não possui CI funcional.

Os commits novos da preparação foram reconhecidos pelo GitHub como autoria de `Setezin7`. O conteúdo funcional de aplicação, testes, migrações e lockfiles foi comparado com a origem e preservado. Nenhum `.env` foi publicado; os três diretórios originais mantiveram seus remotes e conteúdo.
