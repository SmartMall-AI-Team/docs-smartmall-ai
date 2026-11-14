# SmartMall AI — links para avaliação

Ponto de entrada para conhecer a proposta, experimentar a demonstração e conferir código, planejamento e evidências.

## Demonstração e API

| Material | Link | Como acessar |
| --- | --- | --- |
| Site na Vercel | [Abrir SmartMall AI](https://smartmall-ai-demo.vercel.app) | Use o perfil fictício `marina` / `marina123`; não há código adicional |
| Roteiro da banca | [Guia de avaliação](avaliacao.md) | Passos para testar o fluxo e limites da entrega |
| Demonstração passo a passo | [Roteiro de demonstração](demonstracao.md) | Registro → análise → revisão → tarefa → acompanhamento |
| API no Render | [Documentação interativa — Swagger](https://smartmall-ai-demo-api-8mez.onrender.com/docs) | Rotas e schemas públicos; use somente dados fictícios |
| Disponibilidade da API e banco | [Prontidão do serviço](https://smartmall-ai-demo-api-8mez.onrender.com/health/ready) | Retorno esperado: `status=ok` e `database=ok` |

O serviço gratuito da API pode precisar despertar após inatividade. Aguarde a indicação **Conectado à API** na interface. O ambiente compartilha dados fictícios e usa **IA simulada**, indicada na tela. Os perfis demonstrativos não representam autenticação ou permissões reais.

## Planejamento e organização do grupo

| Material | Link | Acesso e finalidade |
| --- | --- | --- |
| Trello | [Quadro de desenvolvimento do hackathon](https://trello.com/b/TMJ0EfTl/smartmall-ai-desenvolvimento-do-hackathon) | Quadro privado; solicitar acesso à liderança. Etapas, responsáveis, checklists e evidências |
| Miro | [Fluxograma base do projeto](https://miro.com/app/board/uXjVEOPHRG4=/?share_link_id=465697087214) | Link compartilhado; abertura do quadro depende das permissões do Miro |
| Escopo | [MVP e critérios de aceite](escopo.md) | Proposta, entrega essencial e limites |
| Backlog público | [Entregas por frente](backlog.md) | Alternativa pública para consultar o planejamento sem acesso ao Trello |
| Equipe | [Responsabilidades](equipe.md) | Liderança e divisão das frentes |
| Governança | [Revisão e permissões](governanca.md) | Branches, pull requests, CODEOWNERS e integração |

**Liderança:** [João Geraldo — Setezin7](https://github.com/Setezin7). O acesso privado ao Trello é concedido separadamente pela liderança; os demais materiais públicos permitem avaliar a entrega sem depender desse acesso.

## Organização e código-fonte

| Recurso | Link |
| --- | --- |
| Organização de referência | [SmartMall-AI-Team](https://github.com/SmartMall-AI-Team) |
| Backend | [be-smartmall-ai](https://github.com/SmartMall-AI-Team/be-smartmall-ai) |
| Frontend | [fe-smartmall-ai](https://github.com/SmartMall-AI-Team/fe-smartmall-ai) |
| Documentação central | [docs-smartmall-ai](https://github.com/SmartMall-AI-Team/docs-smartmall-ai) |
| Contrato da API | [Rotas, campos, regras e erros](contrato-api.md) |
| Arquitetura | [Componentes e responsabilidades](arquitetura.md) |

## Evidências e situação da entrega

| Evidência | Link |
| --- | --- |
| Verificação do backend nesta organização | [GitHub Actions — 55 testes aprovados](https://github.com/SmartMall-AI-Team/be-smartmall-ai/actions/runs/43630462244) |
| Verificação do frontend nesta organização | [GitHub Actions — build e 12 cenários aprovados](https://github.com/SmartMall-AI-Team/fe-smartmall-ai/actions/runs/43630474360) |
| Publicação da demonstração | [Deploy e verificações datadas](deploy.md) |
| Histórico da cópia e autoria | [Origem e publicação na SmartMall-AI-Team](copia-team.md) |
| Validação com usuários | [Plano e registros](validacao-usuarios.md) — sessões ainda pendentes |

Os serviços Vercel/Render e o banco são o ambiente de demonstração já existente; a publicação dos repositórios nesta organização preservou código e histórico, sem transferir esses recursos. Os testes automatizados não substituem validação com usuários. A integração OpenAI real continua pendente de saldo e validação; não há medição comprovada de redução de tempo.

## Conferência dos endereços

Em **14/11/2026**, o site Vercel, o Swagger e a prontidão da API retornaram HTTP 200; a prontidão informou API e banco disponíveis. O link compartilhado do Miro retornou HTTP 200, o que não comprova acesso anônimo ao conteúdo do quadro. Os três repositórios GitHub foram publicados como públicos. Esta é uma conferência datada, não um monitoramento contínuo.
