# Command Center · Marketing — Starter

Vault inicial de **Second Brain de marketing/negócio** para a aula Agentic OS. O aluno baixa, abre no Obsidian, ativa os plugins e faz a configuração inicial com os prompts, ao vivo. A central já vem montada e os agentes de marketing já vêm prontos. Desktop-only.

---

## O que já vem pronto

- `CLAUDE.md` — a base da estrutura do vault (o que é, camadas, agentes, governança).
- `Command Center.md` — o painel (Dataview + botões), abre sozinho no boot, **já com visual escuro estilo Agentic OS** (via CSS snippet pré-ligado).
- `raw/` — fontes imutáveis: `clippings/` (Web Clipper), `briefings/`, `transcricoes/`. O agente lê e cita, nunca edita.
- `output/` — onde caem os resultados dos agentes (datados). É o que os botões geram.
- `wiki/` — conhecimento curado: `index.md`, `log.md`, `clientes/`, `campanhas/`, `conteudo/`, `mercado/`, `conceitos/`, `sinteses/`.
- `.claude/agents/` — seis agentes de marketing prontos: `radar-mercado`, `gerador-de-pautas`, `analise-concorrente`, `qualificador-leads`, `revisor-de-copy`, `relatorio-semanal`. Todos salvam em `output/` e leem de `raw/`+`wiki/`.
- `.obsidian/` — lista de plugins, Homepage, **Shell commands já configurados** e o snippet visual já ativado.

**Dados de exemplo já incluídos** (pra não começar vazio): uma transcrição fictícia em `raw/transcricoes/`, a síntese dela em `wiki/sinteses/` (exemplo de ingest com fonte citada) e um resultado de radar em `output/`. Apague quando tiver os seus.

> Arquitetura de camadas do vault-mãe: `raw/` (entra) → `output/` (o agente gera) → `wiki/` (você cura) → `CLAUDE.md` (schema). O que muda é o contexto: aqui é marketing/negócio.

---

## Quick start do aluno (3 passos)

1. **Baixe e abra.** Baixe o repositório (Code → Download ZIP), descompacte e, no Obsidian, "Abrir pasta como cofre" apontando para esta pasta.
2. **Ative os plugins.** Settings → Community plugins. Se os plugins já vieram no pacote (ver nota abaixo), é só **ativar**. Se não, instale os sete: Dataview, Meta Bind, Shell commands, Terminal, Surfing, Homepage, Hidden Folders Access.
3. **Recarregue** (`Ctrl+R`). A central abre, as listas se preenchem e os botões já apontam pros comandos.

Depois, a configuração inicial em sala é só ajustar os prompts dos agentes ao contexto de cada um (ver "Personalizar").

---

## Pré-requisito do computador

O Claude Code CLI instalado e no PATH (os botões chamam `claude`). Teste: `claude --version`.

---

## Se um comando do Shell não carregar (plano B)

Se a versão do plugin Shell commands diferir, recrie os comandos (Settings → Shell commands → New command) com estes textos. Defina o "Working directory" como a raiz do vault.

| Nome | Comando |
|---|---|
| Radar de mercado | `claude -p "Roda o agente radar-mercado e salve em Mercado/."` |
| Gerar pautas | `claude -p "Roda o agente gerador-de-pautas e salve em Conteudo/."` |
| Analisar concorrente | `claude -p "Roda o agente analise-concorrente para o concorrente indicado e salve em Mercado/."` |
| Relatório semanal | `claude -p "Roda o agente relatorio-semanal e salve em Campanhas/."` |
| Abrir navegador | `cmd /c start "" https://www.google.com` |

Mac/Linux: troque a última por `open URL` / `xdg-open URL`.

---

## Personalizar

- **Ajustar um agente:** edite o arquivo em `.claude/agents/`. O texto abaixo do frontmatter é o cérebro dele. Adapte ao setor do aluno.
- **Criar um agente novo:** no terminal embutido, rode `claude` e peça: "crie um agente em .claude/agents/ que [tarefa], gatilho [frase]".
- **Mudar um botão:** edite o comando em Settings → Shell commands (só o texto entre aspas).

---

## Detalhe: a pasta `.claude`

O Obsidian esconde pastas que começam com ponto. O painel "Meus agentes" só enxerga `.claude/agents/` com o plugin **Hidden Folders Access** ativo (já está na lista). Alternativa: renomear para `Agents/` e trocar `FROM ".claude/agents"` por `FROM "Agents"` no `Command Center.md` (mas aí o Claude Code não descobre os agentes automaticamente).
