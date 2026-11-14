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

A publicação, os novos checks e as proteções da `main` serão registrados após a criação da organização e dos repositórios. Até a confirmação via GitHub, as referências de destino representam a estrutura preparada.
