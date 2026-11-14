# Roteiro de demonstração

Abra a [demonstração publicada](https://smartmall-ai-demo.vercel.app) e entre com **`marina` / `marina123`**, conta fictícia de administração. Não há código de acesso adicional. Aguarde **Conectado à API**; a API gratuita pode levar cerca de um minuto para despertar. Use somente dados fictícios.

O fluxo está publicado e foi verificado em desktop e celular; veja [deploy e evidências](deploy.md). A IA da demonstração está sempre em simulação e a indicação permanece visível. O ensaio da apresentação e a validação com usuários ainda precisam ocorrer.

## Problema e proposta

Explicar como registros dispersos dificultam o entendimento, o encaminhamento e o acompanhamento de ocorrências operacionais de um shopping. Apresentar o SmartMall AI como um fluxo único, com IA para apoiar a triagem e revisão humana para confirmar as decisões.

## Demonstração do fluxo

1. Em **Nova ocorrência**, registrar um relato fictício de ar-condicionado sem refrigeração, com descrição e local. Enviar e abrir o detalhe pela lista.
2. Recarregar a página e mostrar que o registro continua salvo na API.
3. Selecionar **Solicitar análise** e explicar categoria, prioridade e equipe sugeridas. Mostrar **Resultado de simulação**.
4. Selecionar **Usar sugestões no formulário**, revisar os valores e **Confirmar revisão**. Explicar que a sugestão não substitui a decisão humana.
5. Em **Atribuir nova tarefa**, informar atividade, responsável fictício e prazo. Criar a tarefa vinculada.
6. Iniciar e concluir a tarefa. Resolver a ocorrência explicitamente; tarefas pendentes impedem esse encerramento.
7. Mostrar o histórico e o dashboard com os dados persistidos.

A demonstração não chama o provedor real. Os testes técnicos também cobrem falha controlada da IA, com registro preservado e classificação manual disponível; a banca pode consultar essas evidências sem provocar uma falha no ambiente publicado.

## Evidências a preparar

- Execução do fluxo com persistência após recarregar a página.
- Estado de falha da IA sem perda do registro.
- Exemplo de revisão humana das sugestões.
- Observação real de uma sessão de teste e melhoria aplicada, se realizadas.
- Links definitivos dos três repositórios e dos ambientes publicados.

## Limitações

Mencionar os módulos incompletos e decisões pendentes. Não afirmar redução percentual de tempo, uso por shopping real ou aprovação de usuários sem evidências correspondentes.
