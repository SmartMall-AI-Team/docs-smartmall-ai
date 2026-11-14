# Revisão e integração do frontend

**Estado atual:** [demonstração publicada](https://smartmall-ai-demo.vercel.app), sem código de acesso adicional, com IA simulada. Entre com `marina` / `marina123`. O [guia de deploy](deploy.md) registra as verificações posteriores; o relato abaixo preserva as evidências da revisão inicial.

Revisão técnica de 14/11/2026, conduzida por João Geraldo (`geraldojoao`). Foram consultados os PRs abertos dos três repositórios: somente o [frontend #3](https://github.com/SmartMall-AI/fe-smartmall-ai/pull/3) estava aberto. Backend e documentação não tinham PRs pendentes. O trabalho original de Felipe (`FelipeAaugusto`) foi preservado; as correções foram acrescentadas em [df9095b](https://github.com/SmartMall-AI/fe-smartmall-ai/commit/df9095bc5ebbff84834fbe8d28e6909957380516), sem force push.

O PR foi [aprovado pela liderança](https://github.com/SmartMall-AI/fe-smartmall-ai/pull/3#pullrequestreview-5904558614) após as correções e os checks aprovados, e [integrado à main por merge commit](https://github.com/SmartMall-AI/fe-smartmall-ai/commit/40816bd2e83b7a25f1456649c5d26b86907cc07c), mantendo a proteção e a autoria dos commits.

## Problemas encontrados e corrigidos

| Problema antes da revisão | Comportamento corrigido |
| --- | --- |
| Categoria, equipe e recomendação só podiam ser revistas após obter análise da IA | Classificação manual disponível sem IA e após falha 503 |
| Reabrir o detalhe preenchia os campos com sugestões originais, mesmo após decisão humana salva | Campos mostram os valores persistidos; copiar sugestões exige ação explícita |
| Prazo buscado em `occurrence.tasks`, ausente na rota de listagem | Lista usa o primeiro prazo de tarefa não concluída obtido de `/tasks` |
| Recarregar perfil técnico ou lojista abria dashboard sem conteúdo para esse perfil | Recarga abre a área correspondente ao perfil |
| Alterar prioridade não recarregava histórico e resposta de análise tinha tipo incorreto | Histórico atualizado e resposta tipada como análise, conforme contrato |

## Evidências verificadas

- `npm ci` e `npm run build` aprovados, com dependências diretas fixadas. O build mantém aviso de bundle acima de 500 kB.
- 10 testes Playwright aprovados: cinco fluxos repetidos em Chromium desktop e celular, consumindo FastAPI e PostgreSQL reais em banco descartável.
- Cadastro e consulta após recarga; falha controlada de IA com registro preservado e triagem manual; simulação identificada; revisão humana persistida sem reaplicar sugestões.
- Criação de tarefa com responsável e prazo; início e conclusão; bloqueio de encerramento prematuro; resolução explícita; histórico e contagens do dashboard.
- Cadastro de equipamento pela interface e persistência do vínculo; recarga do perfil técnico; erro de conexão sem dados fictícios substitutos e recuperação da API.
- Os 46 testes do backend foram executados novamente e passaram.
- [GitHub Actions do frontend](https://github.com/SmartMall-AI/fe-smartmall-ai/actions/runs/43600532632) repete build e testes contra o backend fixado em `a335e02a63a201c5381417c9a83d2d1de89d6f55`. O banco do CI é exclusivo dessa execução.

Os testes de navegador induzem o 503 da IA e a queda de rede; os demais fluxos usam a API real local. A análise bem-sucedida usa `AI_SIMULATION=true`, nunca uma resposta real da OpenAI. Esses testes são evidências técnicas, não sessões de validação com usuários.

## Cobertura dos requisitos e limites

FE-01 a FE-05 têm interface executável e fluxo técnico integrado verificado. HIST-01 exibe eventos persistidos. FE-06 é parcial: busca/filtros rápidos de ocorrências e cadastro/consulta de equipamentos; faltam filtros completos de categoria, equipamento e local. INT-01 tem os cenários técnicos descritos acima; o aceite da equipe e a apresentação continuam pendentes.

Responsável e prazo são definidos ao criar a tarefa; a interface atual atualiza status, mas ainda não edita responsável/prazo de uma tarefa existente. Login e perfis são demonstrativos e não concedem autorização. O rádio permite anotações digitadas, sem captura de áudio nem transcrição automática; o texto fica neste navegador.

Na revisão inicial, VAL-01, DEMO-01, hospedagem pública, autenticação real e chamada real à IA estavam pendentes. A hospedagem foi concluída depois, conforme o [guia de deploy](deploy.md); as sessões com usuários, o ensaio final, a autenticação real e a validação da chamada real à IA continuam pendentes. Não há comprovação de redução do tempo de atendimento.

Veja o [README do frontend](https://github.com/SmartMall-AI/fe-smartmall-ai/blob/main/README.md) para reproduzir os testes. Use somente dados fictícios e banco de testes exclusivo: os cenários criam registros e não os removem.
