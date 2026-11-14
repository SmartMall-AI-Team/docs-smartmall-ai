# SmartMall AI — guia para a banca

Este guia facilita a avaliação da entrega; não representa critérios oficiais do evento.

**[Abrir demonstração](https://smartmall-ai-demo.vercel.app)** · **[Documentação](README.md)** · **[Swagger público](https://smartmall-ai-demo-api-8mez.onrender.com/docs)**

## 1. Entrar e conhecer a proposta

Use **`marina` / `marina123`**, conta fictícia de administração. Não há código de acesso adicional nem cadastro prévio. Se a API estiver despertando, aguarde cerca de um minuto até aparecer **Conectado à API**.

O SmartMall AI centraliza relatos operacionais de um shopping e acompanha triagem, revisão humana e atendimento. A proposta é diminuir a dispersão de informações; não há medição de redução de tempo nem validação com usuários reais.

## 2. Testar o fluxo

| Passo | Ação | Resultado a observar |
| --- | --- | --- |
| Registrar | Em **Nova ocorrência**, cadastre um relato fictício com título, descrição e local | O registro continua disponível após recarregar |
| Analisar | Selecione **Solicitar análise** | Sugestões com indicação **Resultado de simulação** |
| Revisar | Use **Usar sugestões no formulário**, ajuste e **Confirmar revisão** | A decisão humana é salva sem aplicar sugestões automaticamente |
| Encaminhar | Em **Atribuir nova tarefa**, informe atividade, responsável fictício e prazo | Tarefa vinculada à ocorrência |
| Acompanhar | Inicie e conclua a tarefa; depois resolva a ocorrência | Histórico e dashboard atualizados; tarefas pendentes impedem encerrar |

Veja os passos completos no [roteiro de demonstração](demonstracao.md). Use apenas dados fictícios: todos compartilham o mesmo ambiente.

Outros perfis disponíveis na tela: `operacao` / `operacao123`, `joao` / `joao123`, `ana` / `ana123` e `carlos` / `carlos123`. São perfis de navegação demonstrativos, sem autorização real por pessoa.

## 3. Conferir implementação e evidências

| Frente | Entrega verificável | Onde conferir |
| --- | --- | --- |
| Backend | Ocorrências, tarefas, responsáveis, equipamentos, filtros, histórico e dashboard | [Código](https://github.com/SmartMall-AI/be-smartmall-ai) · [Contrato](contrato-api.md) |
| Frontend | Formulários, triagem manual e assistida, tarefas, equipamentos e indicadores | [Código](https://github.com/SmartMall-AI/fe-smartmall-ai) · [Revisão técnica](entrega-frontend.md) |
| Testes | 55 testes backend; 12 cenários desktop/celular na entrega protegida; login e recarga sem código verificados depois nos dois formatos | [Evidências datadas](deploy.md) · [Actions backend](https://github.com/SmartMall-AI/be-smartmall-ai/actions) · [Actions frontend](https://github.com/SmartMall-AI/fe-smartmall-ai/actions) |
| Hospedagem | Vercel → API Render → PostgreSQL Supabase | [Arquitetura](arquitetura.md) · [Prontidão da API/banco](https://smartmall-ai-demo-api-8mez.onrender.com/health/ready) |
| Evolução | Alterações integradas por PR, com autoria e checks preservados | [PRs backend](https://github.com/SmartMall-AI/be-smartmall-ai/pulls?q=is%3Apr+is%3Amerged) · [PRs frontend](https://github.com/SmartMall-AI/fe-smartmall-ai/pulls?q=is%3Apr+is%3Amerged) |

Os testes usam PostgreSQL real e falhas de IA/rede controladas. Não representam sessões com usuários. O [PR backend #8](https://github.com/SmartMall-AI/be-smartmall-ai/pull/8) registra a remoção do código compartilhado e o teste de acesso sem código.

## 4. Distinguir entrega e próximos passos

- **Funcionando:** fluxo operacional persistido, revisão humana, triagem manual, IA simulada e demonstração pública.
- **Integração preparada:** OpenAI com saída estruturada e testes controlados. A tentativa real retornou saldo esgotado; nenhuma análise real foi validada.
- **Pendente:** autenticação e permissões reais, filtros completos, edição de responsável/prazo, validação com usuários e mensuração de resultados.
- **Rádio:** anotação digitada local; sem captura de áudio ou transcrição automática.

Consulte [escopo](escopo.md), [backlog](backlog.md) e [plano de validação](validacao-usuarios.md) para critérios e trabalho futuro.

## 5. Equipe e organização

[João Geraldo — @geraldojoao](https://github.com/geraldojoao) lidera o projeto e responde pelo backend. [Equipe e frentes](equipe.md) · [Governança](governanca.md) · [Contribuição](CONTRIBUTING.md).

O [Trello](https://trello.com/b/TMJ0EfTl) é privado; o acesso não é necessário para consultar a demonstração e as evidências públicas deste guia.
