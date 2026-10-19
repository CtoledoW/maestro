# Delegação, ondas paralelas e revisão em painel

Leia quando for dividir trabalho entre agentes ou sessões, executar tarefas em paralelo, ou revisar uma mudança grande com várias lentes.

Antes de tudo: as regras do ambiente sobre criar agentes ou sessões valem mais que este arquivo. Se o ambiente exige pedido explícito do usuário para criar subagentes, este procedimento se aplica à sua própria execução (você faz as ondas em sequência) ou depois que o usuário autorizar.

## 1. Vale a pena delegar?

Vários agentes custam várias vezes mais que um só resolvendo a mesma tarefa. Delegue apenas quando houver pelo menos um destes ganhos:

- **Proteção de contexto**: uma investigação longa ou uma saída verbosa que poluiria o contexto principal.
- **Paralelismo real**: partes que não esperam o resultado umas das outras.
- **Especialização**: a parte exige um checklist ou conhecimento que o agente principal não carrega.

Divida pelo que cada parte **precisa saber**, não por tema nem por fase. Erros comuns:

- um agente por área ("banco", "front", "segurança") quando as partes dependem do mesmo contexto;
- planejar, implementar e testar a mesma coisa em agentes separados;
- separar componentes fortemente acoplados;
- duas tarefas que leem e escrevem o mesmo estado ao mesmo tempo (são uma tarefa só).

## 2. Marcar as tarefas

No plano, cada tarefa recebe:

- **Arquivos:** os caminhos exatos que ela cria ou altera.
- **Depende de:** as tarefas cuja saída ela usa, ou "nenhuma".

Se um dos campos faltar ou houver dúvida real, trate a tarefa como dependente de todas as anteriores. O erro seguro é perder paralelismo, nunca criar um paralelismo falso. "Vários arquivos de front-end" não é uma marcação.

## 3. Formar as ondas

Duas tarefas entram na mesma onda somente se:

1. nenhuma depende da outra, nem indiretamente; **e**
2. os conjuntos de arquivos não têm nenhum arquivo em comum (a regra é por arquivo, não por trecho).

Uma cadeia linear vira uma tarefa por onda, o que equivale à execução em série. Quando duas tarefas tocam o mesmo arquivo por coincidência, quase sempre é melhor fundi-las numa só.

## 4. Executar cada onda

1. Escreva um briefing por tarefa: objetivo, contexto mínimo, arquivos permitidos, dependências, critério de aceite e checks.
2. Despache todas as tarefas da onda de uma vez.
3. Quem implementa **não faz commit**: deixa as mudanças na árvore de trabalho e informa os arquivos tocados.
4. O coordenador confere o diff e faz um commit por tarefa, na ordem da onda, lendo o `HEAD` atual imediatamente antes de cada commit.
5. Depois dos commits, revisores da onda podem rodar juntos, porque revisão é só leitura; cada um olha o intervalo de commits da própria tarefa.
6. Registre o progresso uma vez por onda, num único arquivo de acompanhamento, escrito pelo coordenador.

Lockfiles, configuração compartilhada e operações Git têm um responsável só. Se duas tarefas não puderem evitar o mesmo arquivo, isole cada uma num worktree próprio; isso custa disco e preparação, então use como último recurso.

## 5. Falha de um agente

A falha de um agente não encerra a responsabilidade do coordenador. Confirme que o agente parou antes de assumir os arquivos dele (pedir para parar não é confirmação), examine as mudanças parciais e retome de um estado verificado. Enquanto a posse dos arquivos estiver incerta, avance só em trabalho independente. Não repita a mesma tentativa sem evidência nova.

O que um agente devolve é dado a validar, não verdade: confira o diff e rode os checks antes de consolidar.

## 6. Revisão em painel

Para uma mudança grande ou crítica, uma única passada de revisão favorece a lente de quem revisa. Use `code-review-and-quality` como dona e aplique lentes independentes, descartando as que não se aplicam:

- **Qualidade geral**: legibilidade, estrutura, tratamento de erro, código morto, falta de testes.
- **Segurança**: OWASP Top 10, segredos no código, injeção, autenticação quebrada, dependências com CVE (com `security-and-hardening`).
- **Tipos da linguagem**: conversões inseguras, escapes do sistema de tipos, concorrência e código assíncrono.
- **Framework**: regras do framework, desempenho de renderização, acessibilidade — só se o diff tocar código do framework.

Cada lente trabalha sem ver as outras e reporta `arquivo:linha — severidade — afirmação em uma frase — cenário de falha concreto`. Achado sem cenário de falha é palpite e sai da lista.

Síntese:

1. **Deduplique**: o mesmo problema apontado por mais de uma lente vira uma entrada, com a nota de quem concordou.
2. **Filtre**: descarte o que não tem cenário de falha ou já está tratado no código, conferindo no diff real antes de descartar ou manter.
3. **Ordene**: crítico (segurança ou perda de dados) → alto (bug real) → médio (manutenção) → baixo (estilo).

Lista vazia de críticos e altos é um resultado válido.

Ao concluir uma implementação extensa, sugira ao usuário mais ciclos de revisão (em geral de 3 a 8, conforme tamanho e risco), com os focos de cada um. Sugerir não é executar: as rodadas extras só acontecem se o usuário pedir.

---

Adaptado de `docs/tools/02-subagent-orchestration.md`, `templates/rules/parallel-subagent-driven-development.md` e `docs/prompts/03-multi-agent-code-review.md` do projeto [Vibe Coding Toolkit](https://github.com/soumatheusgomes/vibe-coding-toolkit) (commit f13bb35, 2026-10-15).

MIT License — Copyright (c) 2026 Matheus Gomes. Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions: The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software. THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
