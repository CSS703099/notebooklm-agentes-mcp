# Agentes de IA com MCP — Guia de Estudo

Projeto do desafio **Explore o Poder do NotebookLM**, da DIO, na trilha CI&T — Do Prompt ao Agente.

**Objetivo** — Entender como um agente descobre e usa ferramentas via MCP e aplicar o conceito a um assistente financeiro com dados fictícios, identificando onde entram validação, autorização e supervisão humana.

O caso prático é o **Banco na Viagem**, um protótipo de portfólio em que regras determinísticas reconhecem a intenção do usuário e acionam ferramentas MCP. A aplicação usa dados fictícios em USD. O cenário com um LLM é um exercício de arquitetura.

[Abrir o caderno no Gemini Notebook](https://notebook.google.com/notebook/09be77ef-8138-4849-b740-fcf2a45c0c9c)

## Fontes e curadoria

| ID | Fonte | Por que entrou |
| --- | --- | --- |
| F1 | [Architecture overview](https://modelcontextprotocol.io/docs/2025-11-25/learn/architecture) | Documentação oficial de arquitetura, papéis, primitivas e transportes. |
| F2 | [Tools — especificação 2025-11-25](https://modelcontextprotocol.io/specification/2025-11-25/server/tools) | Referência normativa para descoberta, chamada, mudanças de catálogo e validação de ferramentas. |
| F3 | [Security Best Practices](https://modelcontextprotocol.io/docs/2025-11-25/tutorials/security/security_best_practices) | Guia oficial de segurança com cenários sobre tokens, sessões e fronteiras de confiança. |
| F4 | [The Model Context Protocol — Anthropic](https://www.youtube.com/watch?v=CQywdSdi5iA) | Vídeo introdutório dos criadores do protocolo, importado pela transcrição. |
| F5 | [Banco na Viagem](https://github.com/CSS703099/banco-na-viagem-mcp) | Documentação e código públicos do caso prático com dados de demonstração. |
| F6 | [Lifecycle — especificação 2025-11-25](https://modelcontextprotocol.io/specification/2025-11-25/basic/lifecycle) | Fonte primária sobre inicialização e negociação de capacidades. |
| F7 | [MCP for Beginners — Microsoft](https://github.com/microsoft/mcp-for-beginners) | Material didático mantido pela Microsoft, com exemplos em diferentes linguagens. |

O Deep Research buscou fontes primárias sobre arquitetura, descoberta e chamada de ferramentas, transportes e execução segura. Das **23 sugestões**, foram importadas F6 e F7 após conferir autoria, escopo e relevância. O relatório gerado serviu como instrumento de descoberta. As conclusões normativas deste projeto se referem à revisão **2025-11-25**.

## Diretriz salva no chat

> Você é meu tutor de Model Context Protocol (MCP). Quero explicar host, cliente e servidor, rastrear a descoberta e a chamada de ferramentas e propor controles para um assistente financeiro de demonstração. Responda em português do Brasil, em nível iniciante a intermediário, com um exemplo curto e uma pergunta de recuperação ativa. Fundamente afirmações técnicas nas fontes selecionadas, cite os trechos junto da afirmação e identifique a versão da especificação quando relevante. Separe requisitos normativos, recomendações e inferências. Se as fontes não sustentarem algo, diga que não há evidência suficiente. No caso Banco na Viagem, trate os dados como fictícios, separe o comportamento documentado do protótipo de extensões hipotéticas e não proponha executar operações financeiras reais.

## Perguntas e respostas conferidas

| Teste | Síntese da resposta | Como foi conferida |
| --- | --- | --- |
| Qual a diferença entre host, cliente e servidor? Como funcionam `tools/list` e `tools/call` em uma consulta de saldo fictício? | O host coordena os clientes. Cada cliente mantém uma conexão com um servidor, que fornece as capacidades. `tools/list` consulta o catálogo e `tools/call` invoca uma ferramenta. O protótipo aciona a consulta via regras locais. | F1, papéis dos participantes. F2, listagem e chamada. F5, arquitetura da demonstração. |
| Quando o servidor anuncia `listChanged`? Qual a força da notificação de mudança? | A capacidade é informada na inicialização. Na revisão estudada, quando o catálogo muda, servidores que declararam a capacidade têm a recomendação `SHOULD` de enviar `notifications/tools/list_changed`. Uma nova chamada `tools/list` permite atualizar o catálogo. | F2, seção [List Changed Notification](https://modelcontextprotocol.io/specification/2025-11-25/server/tools#list-changed-notification). |
| Quais controles usar se um LLM for integrado ao protótipo? O protótipo já usa LLM? | O chat separou validação de argumentos no servidor, confirmação humana e restrição de escopo. Na extensão hipotética, uma lista de ferramentas de leitura e a verificação de permissões no servidor limitam chamadas induzidas por conteúdo externo. F5 descreve seleção por regras determinísticas. | F2, seções de interação e segurança. F3, boas práticas de autorização. F5, funcionamento da demonstração. |
| Qual era o saldo real do cliente ontem? | O tutor explicou que o caderno contém uma amostra fictícia e que não há consulta em tempo real para informar um saldo real. | F5, descrição dos dados da demonstração. |

A primeira resposta usou linguagem de obrigação ao tratar da notificação de mudança. A segunda consulta pediu a revisão explícita. A regra correta, conferida na fonte F2, é **SHOULD**, condicionada à declaração da capacidade e à mudança no catálogo. A nota **Segurança MCP** guarda essa segunda resposta no caderno.

## Materiais

- [Mapa mental em PNG](mapa-mental-mcp.png) — artefato original do Estúdio sobre papéis, primitivas, fluxo, transportes, segurança e Banco na Viagem.
- [Apresentação em PDF](apresentacao-mcp.pdf) — seis slides gerados a partir das sete fontes do caderno.
- [Evidência do chat com citação](chat-citacao-mcp.jpg) — resposta revisada com a referência oficial visível.
- **Guia de estudo** — disponível no Estúdio do caderno, com glossário, exercícios e gabarito.

Os materiais do Estúdio foram gerados com IA. A especificação e as notas de verificação acima são as referências para o sentido normativo dos termos.
