# Mapa de seleção do Maestro

Detalhamento do "Procedimento de seleção" do `SKILL.md`. Para cada tipo de tarefa:

- **Obrigatória**: dona da etapa; sem ela a etapa fica sem método.
- **Recomendada**: entra por padrão nesse contexto, mas pode ser pulada com motivo (mudança pequena, já existe, usuário dispensou).
- **Condicional**: entra só se o gatilho entre parênteses aparecer.
- **Evitar**: disputa a mesma etapa com a dona, ou não agrega nesse caso.
- **Concluído quando**: o critério objetivo para encerrar.

A ordem das colunas "obrigatória → recomendada" é a ordem de execução, salvo indicação. Use só o que estiver instalado; se uma obrigatória faltar, aplique o método dela você mesmo e diga em uma linha que a skill não estava disponível.

## 1. Tarefa simples (uma edição, uma resposta, uma busca)

| Papel | Skills |
|---|---|
| Obrigatória | nenhuma |
| Recomendada | nenhuma |
| Condicional | a skill do formato, se o arquivo for Word/Excel/PowerPoint/PDF (`docx`, `xlsx`, `pptx`, `pdf`) |
| Evitar | qualquer roteiro: plano, spec, revisão em painel |
| Concluído quando | a edição foi conferida (arquivo aberto, comando rodado, valor checado na fonte) |

## 2. Correção de bug em projeto existente

| Papel | Skills |
|---|---|
| Obrigatória | `debugging-and-error-recovery` (reproduzir, localizar, corrigir, proteger) |
| Recomendada | `test-driven-development` (teste que falha antes da correção e passa depois) |
| Condicional | `code-review-and-quality` (correção em vários arquivos ou área sensível); `security-and-hardening` (o bug envolve autenticação, permissão, entrada externa ou dados pessoais); `performance-optimization` (o bug é lentidão medida); `browser-testing-with-devtools` (bug de interface e o MCP do Chrome DevTools está configurado; sem ele, conferir no navegador embutido); `run` (precisa ver a correção no app real) |
| Evitar | `spec-driven-development`, `planning-and-task-breakdown` e `incremental-implementation` para uma correção localizada; `do`/`make-plan` do Cowork Memory |
| Concluído quando | a causa raiz está identificada, o teste que reproduzia o bug passa, a suíte existente continua passando e o comportamento foi conferido em execução |

## 3. Funcionalidade nova em projeto existente

| Papel | Skills |
|---|---|
| Obrigatória | `incremental-implementation` |
| Recomendada | `using-agent-skills` (porta de entrada das skills de engenharia) → `spec-driven-development` (pular se a mudança for pequena e clara) → `planning-and-task-breakdown` (mais de um arquivo ou etapa) → `incremental-implementation` com `test-driven-development` → `code-review-and-quality` |
| Condicional | `api-and-interface-design` (cria ou muda endpoint, contrato ou módulo público); `frontend-ui-engineering` (componentes de interface); `security-and-hardening` (login, pagamento, upload, dados pessoais, integração externa); `context-engineering` (a sessão está perdendo contexto ou faltam regras do projeto); `deprecation-and-migration` (substitui algo existente) |
| Evitar | `frontend-design` e `design-taste-frontend` quando o projeto já tem design system: o visual segue o existente; `idea-refine` quando o requisito já está claro |
| Concluído quando | os critérios de aceite da spec (ou do pedido) estão atendidos, há teste cobrindo a mudança, build, lint e testes passam, e o fluxo foi conferido em execução |

## 4. Projeto do zero (planejar e implementar)

| Papel | Skills |
|---|---|
| Obrigatória | `spec-driven-development` → `planning-and-task-breakdown` → `incremental-implementation` |
| Recomendada | `constraint-driven-development` (fixar o padrão de qualidade antes do primeiro código) → `test-driven-development` → `code-review-and-quality` → `init` ou `context-engineering` (CLAUDE.md para as próximas sessões) |
| Condicional | `interview-me` (não se sabe para quem ou por quê); `idea-refine` (a ideia existe mas está crua); `deep-research` (falta dado de mercado ou técnico); `api-and-interface-design` (há API); `website-architect` (o projeto é um site); `ci-cd-and-automation` (vai ter pipeline); `shipping-and-launch` (vai para produção) |
| Evitar | começar pelo código; carregar todas as skills de revisão antes de existir código |
| Concluído quando | a spec existe com critérios de aceite, o plano tem tarefas verificáveis, a primeira fatia funciona de ponta a ponta com testes, e o projeto tem instruções (CLAUDE.md ou AGENTS.md) com os comandos reais de build e teste |

**Base Next.js do Vibe Coding Toolkit** (condicional: só se o usuário pedir essa stack ou o toolkit): o repositório `soumatheusgomes/vibe-coding-toolkit` tem uma receita de bootstrap (`docs/prompts/11-next-project-bootstrap.md`) e outra para adotar o toolkit num projeto existente (`docs/prompts/12-existing-project-setup.md`). Leia o arquivo do repositório como referência e siga o roteiro acima; não execute scripts nem instale ferramentas de terceiros citadas lá (Superpowers, RTK, Graphify, Caveman etc.) sem avaliar a origem e sem o pedido do usuário. As skills instaladas já cobrem o processo dessas ferramentas: brainstorming → `interview-me`/`idea-refine`; plano → `planning-and-task-breakdown`; TDD → `test-driven-development`; menor mudança completa → `incremental-implementation` e `code-simplification`.

## 5. Revisão de código e correção de problemas de qualidade

| Papel | Skills |
|---|---|
| Obrigatória | `code-review-and-quality` (ou o comando `code-review`, se o usuário pediu por ele ou quer só os achados de bugs de um diff/PR) |
| Recomendada | `code-simplification` para os achados de complexidade, depois de a revisão terminar |
| Condicional | `security-and-hardening` (toca autenticação, pagamento, entrada externa, segredos, dependências novas); `performance-optimization` (há métrica ruim ou a revisão aponta gargalo); `test-driven-development` (para corrigir um achado com teste); revisão em painel com lentes independentes (mudança grande ou crítica; ver `delegacao-e-ondas.md`) |
| Evitar | rodar a skill e o comando equivalente juntos (`code-review-and-quality` + `code-review`, `code-simplification` + `simplify`, `security-and-hardening` + `security-review`); achados sem cenário de falha concreto |
| Concluído quando | cada achado tem arquivo, severidade e cenário de falha; os achados corrigidos foram reverificados com os checks afetados; o que ficou aberto está listado |

## 6. Tarefa complexa com várias áreas em sequência

Exemplo: pesquisar concorrentes, definir a oferta, construir a landing page e conferir no celular.

| Papel | Skills |
|---|---|
| Obrigatória | Maestro (Parte 1 completa) e uma dona por etapa |
| Recomendada | a sequência do roteiro combinado correspondente, por exemplo `deep-research` → `oferta-5p` → `website-architect` → `design-taste-frontend` → navegador |
| Condicional | `logo-design` (não existe marca); `docs`/`docx` (o usuário pediu um documento com os achados); `schedule` (o usuário quer repetir a tarefa) |
| Evitar | duas skills de direção visual na mesma etapa; `deep-research` e a pesquisa interna de `oferta-5p` para a mesma pergunta |
| Concluído quando | cada etapa tem resultado verificado antes da próxima, e o resultado final foi comparado com o objetivo original |

## 7. Outros tipos frequentes

| Tipo | Obrigatória | Condicional | Evitar |
|---|---|---|---|
| Site ou landing page | `website-architect` | `design-taste-frontend` ou `frontend-design` para o visual; `logo-design`; `deep-research` sobre concorrentes | `frontend-ui-engineering` quando não há código existente |
| Oferta, preço, nicho | `oferta-5p` | `deep-research` (relatório completo pedido); `website-architect` (página de vendas pedida); `docs` (registrar o mapa da oferta para compartilhar) | `idea-refine` para a oferta em si |
| Documento | a skill do formato pedido (`docs`, `docx`, `google-workspace`, `pdf`, `pptx`, `xlsx`) | `deep-research` (precisa de fontes); `dataviz` (gráfico) | duas skills de formato para o mesmo arquivo |
| Pesquisa | `deep-research` (várias fontes, relatório) ou busca simples (pergunta factual) | skill de formato se pediram arquivo | `deep-research` para uma pergunta de uma linha |
| Memória | memória nativa no Claude Code | `consolidate-memory`; `cowork-mem` (só com banco confirmado); `structured-memory` (montar sistema em projeto); `import-memory` | duas famílias de memória gravando a mesma informação |
| Agir no computador ou na web | `built-in-browser`, `chrome-browser` ou `computer-use` | — | `computer-use` para sites |
| Configurar o Claude | `setup-claude`, `claude-automation-recommender`, `update-config` ou `init`, conforme o pedido | `find-skills` (procurar skill); `skill-creator` (criar ou melhorar skill) | instalar uma segunda skill para algo já coberto |

## Sinais de seleção errada

- Mais de uma skill carregada para a mesma etapa.
- Uma tarefa simples recebeu plano, spec ou revisão em painel.
- Uma skill foi carregada antes de a etapa dela começar e nunca foi usada.
- Uma skill da família Cowork Memory foi acionada sem que o banco exista.
- O resultado foi entregue sem a verificação que a skill dona da etapa exige.
