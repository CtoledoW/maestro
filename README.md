# maestro

Skill de orquestração para o Claude, escrita em português. Ela transforma um objetivo em execução controlada: entender, planejar, decompor, executar, validar, corrigir e entregar. Em cada etapa, escolhe a skill certa entre as que estão instaladas.

> Princípio central: **uma ação executada não é uma tarefa concluída.** Concluído é o que foi verificado contra o objetivo original.

## O que a skill faz

- **Ajusta o processo ao tamanho da tarefa.** Tarefas simples são feitas direto. As complexas seguem um protocolo de 8 etapas.
- **Define critérios de sucesso verificáveis** antes de começar e faz uma auditoria antes de entregar.
- **Escolhe uma skill "dona" para cada etapa.** Isso evita que skills parecidas disputem o mesmo pedido.
- **Separa** fato confirmado, hipótese, decisão e resultado validado nos relatórios.
- Para projetos de código, **encaminha para a [`using-agent-skills`](https://github.com/CtoledoW/using-agent-skills)**.

## Estrutura

| Arquivo | Conteúdo |
|---|---|
| `SKILL.md` | Protocolo de execução, mapa de escolha das skills e regras de desempate |
| `references/mapa-de-selecao.md` | Detalhamento por tipo de tarefa: skills obrigatórias, recomendadas e condicionais |
| `references/delegacao-e-ondas.md` | Como delegar a agentes e executar tarefas em paralelo sem conflitos |

## Como instalar

### Instalação manual a partir deste repositório

No **Claude Code**, clone o repositório na pasta de skills pessoais (vale para todos os projetos):

```bash
git clone https://github.com/CtoledoW/maestro.git ~/.claude/skills/maestro
```

Para usar em um único projeto, clone em `.claude/skills/maestro/`, dentro da pasta do projeto.

No **app Claude**, compacte a pasta da skill (com o `SKILL.md`) em um arquivo `.zip`. Depois, envie esse arquivo na área de skills das configurações.

## Como usar

Chame pelo nome (`/maestro`) ou peça uma tarefa de várias etapas:

```text
/maestro Quero criar um sistema de agendamento para um salão de beleza.
Antes de executar, me mostre: objetivo, critérios de sucesso, plano em etapas
e quais skills você vai usar em cada uma.
```

## Requisitos e limitações

- O mapa cita skills que podem não estar instaladas no seu ambiente. Nesse caso, a própria skill diz qual falta e segue sem ela.
- Para os roteiros de engenharia, instale também as skills do pacote [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills).

## Créditos

- **Autoria:** Brismarp Tecnologia.
- O arquivo `references/delegacao-e-ondas.md` é **adaptado** de documentos do projeto [Vibe Coding Toolkit](https://github.com/soumatheusgomes/vibe-coding-toolkit), de **Matheus Gomes** (licença MIT). A licença original está em [`LICENSE-vibe-coding-toolkit`](LICENSE-vibe-coding-toolkit).
- O mapa de seleção referencia skills de vários autores. Os créditos de cada uma estão nos repositórios delas.

## Série *Do Planejamento ao Código*

Este repositório faz parte do material educacional gratuito *Do Planejamento ao Código — 5 Skills para Desenvolver Projetos com Inteligência Artificial*, da Brismarp Tecnologia.

| Capítulo | Repositório |
|---|---|
| 1. Planejamento e orquestração | **maestro** (este) |
| 2. Arquitetura e organização do ambiente | [claude-code-setup](https://github.com/CtoledoW/claude-code-setup) |
| 3. Desenvolvimento e implementação | [using-agent-skills](https://github.com/CtoledoW/using-agent-skills) |
| 4. Automação e produtividade | [convert-documents-to-markdown](https://github.com/CtoledoW/convert-documents-to-markdown) |
| 5. Qualidade e curadoria de ferramentas | [find-skills](https://github.com/CtoledoW/find-skills) |

## Licença

[MIT](LICENSE) © 2026 Brismarp Tecnologia.

---

**Brismarp Tecnologia** — Inovação que conecta ideias ao futuro

Material gratuito e educacional. Se este repositório ajudou você, dê os créditos aos autores originais citados acima.
