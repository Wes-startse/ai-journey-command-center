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

## Setup via Claude Code (cola um prompt)

Em vez de configurar na mão, abra o Claude Code na pasta do vault e cole um dos prompts. Ele faz a parte mecânica: baixa os plugins, cria/valida os arquivos e adapta os comandos a esta máquina.

> **Único passo manual que sobra** (nenhum prompt evita — é segurança do Obsidian): abrir a pasta como cofre e, quando perguntado, clicar **"Confiar e ativar plugins da comunidade"**, depois `Ctrl+R`.

### Prompt A — dentro do starter (recomendado)

Use quando você baixou/clonou este starter e abriu o Claude Code dentro dele.

````text
Você está na pasta do meu Command Center (vault Obsidian) — o starter já vem com os
arquivos prontos. Falta o que não dá pra versionar: baixar os binários dos plugins e
adaptar os comandos a ESTA máquina. Faça, validando no fim:

1) PLUGINS — para cada id em .obsidian/community-plugins.json, baixe da ÚLTIMA release
   no GitHub os arquivos main.js, manifest.json e styles.css (quando existir) para
   .obsidian/plugins/<id>/. Repositórios:
   - dataview = blacksmithgu/obsidian-dataview
   - obsidian-meta-bind-plugin = mProjectsCode/obsidian-meta-bind-plugin
   - obsidian-shellcommands = Taitava/obsidian-shellcommands
   - terminal = polyipseity/obsidian-terminal
   - surfing = PKM-er/Obsidian-Surfing
   - homepage = mirnovov/obsidian-homepage
   - hidden-folders-access = dsebastien/obsidian-hidden-folders-access
   Depois confirme que o "id" de cada manifest.json bate com o nome da pasta (senão o
   Obsidian não carrega). Se um asset não existir na release, me avise e siga.

2) COMANDOS — apps GUI no Obsidian NÃO herdam o PATH do shell, então "claude" puro não
   é encontrado. Descubra o caminho ABSOLUTO do binário (ex.: readlink -f "$(which
   claude)") e reescreva os 6 comandos dos agentes em
   .obsidian/plugins/obsidian-shellcommands/data.json para o formato:
     <caminho-absoluto> --permission-mode acceptEdits -p "Roda o agente <nome> e salve em output/."
   O --permission-mode acceptEdits é obrigatório: rodando headless, sem ele o agente não
   grava o arquivo em output/. Mantenha o comando "Abrir navegador" como está.

3) VERIFIQUE e corrija se preciso (seguindo o CLAUDE.md):
   - Command Center.md: cssclass command-center; os 7 botões (6 agentes + abrir
     navegador) em blocos meta-bind-button SEPARADOS POR LINHA EM BRANCO entre si
     (colados, o Obsidian renderiza como texto cru).
   - A lista de agentes no painel usa um bloco dataviewjs que lê .claude/agents via
     app.vault.adapter e renderiza CARDS (createEl), não uma tabela: cada card com
     nome, badge do modelo, a função e os gatilhos como chips. NÃO use
     FROM ".claude/agents" (o Dataview não indexa pastas que começam com ponto e a
     query volta vazia).
   - .obsidian/plugins/homepage/data.json abre Command Center.md em "Reading view".
   - .obsidian/snippets/command-center.css ativado em appearance.json.

4) No fim, diga em até 3 linhas o que ainda preciso fazer na mão no Obsidian.
````

### Prompt B — do zero (sem o starter)

Use numa pasta vazia, quando você quer montar tudo sem baixar o repositório.

````text
Quero transformar esta pasta num "Command Center" de marketing (vault Obsidian +
agentes). Monte tudo, me mostrando o plano antes de escrever.

ESTRUTURA: CLAUDE.md (schema de 3 camadas: raw/ fontes imutáveis → output/ resultados
dos agentes → wiki/ conhecimento curado), Command Center.md (painel), e as pastas
raw/{clippings,briefings,transcricoes}, output/, wiki/{clientes,campanhas,conteudo,
mercado,conceitos,sinteses} com index.md e log.md.

AGENTES: em .claude/agents/, seis subagents (radar-mercado, gerador-de-pautas,
analise-concorrente, qualificador-leads, revisor-de-copy, relatorio-semanal), cada um
com frontmatter (name, description com gatilhos, tools, model, mcpServers, skills) e
instruções no corpo. Todos salvam em output/.

PAINEL (Command Center.md): cssclass "command-center"; header em HTML estilo terminal
escuro (chrome de janela com pontos, caminho, indicador LIVE e um wordmark estilo
prompt). Uma grade de 7 botões do Meta Bind (os 6 agentes + abrir navegador), cada bloco
meta-bind-button SEPARADO POR LINHA EM BRANCO (se colarem, o Obsidian renderiza como
texto), com label, icon (lucide), style e class. Blocos Dataview listando output/ e o
wiki. Para a lista de AGENTES use um bloco dataviewjs que lê .claude/agents via
app.vault.adapter e renderiza CARDS (createEl, não tabela): cada card com nome, badge
do modelo, a função e os gatilhos (frases entre aspas da description) como chips. NÃO
use FROM ".claude/agents", porque o Obsidian não indexa pastas que começam com ponto e
a query volta vazia.

VISUAL: .obsidian/snippets/command-center.css, tema escuro + accent laranja (#FE840C),
estilo console: header com chrome de terminal, botões em GRADE (torne inline-block o
wrapper de code-block que o Obsidian gera, cobrindo as variações de DOM, pra fluírem
lado a lado em vez de empilhar), os agentes como GRADE DE CARDS (nome, badge do modelo,
função e chips de gatilho), cards com hover, tabelas do Dataview estilizadas,
respeitando prefers-reduced-motion e foco de teclado. Ative em .obsidian/appearance.json.

PLUGINS: .obsidian/community-plugins.json com dataview, obsidian-meta-bind-plugin,
obsidian-shellcommands, terminal, surfing, homepage, hidden-folders-access. Baixe da
última release no GitHub (main.js + manifest.json + styles.css quando houver) para
.obsidian/plugins/<id>/, usando: blacksmithgu/obsidian-dataview,
mProjectsCode/obsidian-meta-bind-plugin, Taitava/obsidian-shellcommands,
polyipseity/obsidian-terminal, PKM-er/Obsidian-Surfing, mirnovov/obsidian-homepage,
dsebastien/obsidian-hidden-folders-access. Confirme que o "id" de cada manifest bate
com a pasta.

COMANDOS (.obsidian/plugins/obsidian-shellcommands/data.json): um comando por agente +
um pra abrir o navegador. IMPORTANTE: apps GUI no Obsidian não herdam o PATH do shell —
descubra o caminho ABSOLUTO do binário claude (which/readlink) e use-o; inclua
--permission-mode acceptEdits (sem ele, headless, o agente não grava em output/).
Formato: <claude-abs> --permission-mode acceptEdits -p "Roda o agente <nome> e salve em
output/.". Configure o Homepage pra abrir a Command Center.md em "Reading view".

Por fim, liste o que sobra pra eu fazer manualmente no Obsidian (confiar/ativar plugins
da comunidade + Ctrl+R).
````

### Por que ainda sobra um passo manual

O Obsidian, por segurança, não deixa um processo externo ativar plugins da comunidade sozinho: na primeira abertura do vault ele pede confirmação. O prompt deixa tudo pronto; quem dá o "ok" de confiar e ativar é você, uma vez, com um clique.

---

## Pré-requisito do computador

O Claude Code CLI instalado. Teste: `claude --version`. Atenção: o Obsidian aberto pela interface gráfica pode **não enxergar** `~/.local/bin` (não herda o PATH do seu shell), por isso o prompt de setup reescreve os comandos com o **caminho absoluto** do `claude` em vez de chamar `claude` puro.

---

## Se um comando do Shell não carregar (plano B)

Se a versão do plugin Shell commands diferir, recrie os comandos (Settings → Shell commands → New command) com estes textos. Defina o "Working directory" como a raiz do vault.

Troque `<claude>` pelo **caminho absoluto** do binário (descubra com `readlink -f "$(which claude)"`) — o Obsidian pela GUI pode não achar `claude` puro. O `--permission-mode acceptEdits` autoriza o agente a gravar em `output/` rodando headless.

| Nome | Comando |
|---|---|
| Radar de mercado | `<claude> --permission-mode acceptEdits -p "Roda o agente radar-mercado e salve em output/."` |
| Gerar pautas | `<claude> --permission-mode acceptEdits -p "Roda o agente gerador-de-pautas e salve em output/."` |
| Analisar concorrente | `<claude> --permission-mode acceptEdits -p "Roda o agente analise-concorrente para o concorrente indicado e salve em output/."` |
| Qualificar lead | `<claude> --permission-mode acceptEdits -p "Roda o agente qualificador-leads para o nome + empresa indicados e salve em output/."` |
| Revisar copy | `<claude> --permission-mode acceptEdits -p "Roda o agente revisor-de-copy sobre o texto indicado e salve em output/."` |
| Relatório semanal | `<claude> --permission-mode acceptEdits -p "Roda o agente relatorio-semanal e salve em output/."` |
| Abrir navegador | `cmd /c start "" https://www.google.com` |

Mac/Linux: troque a última por `open URL` / `xdg-open URL`.

---

## Personalizar

- **Ajustar um agente:** edite o arquivo em `.claude/agents/`. O texto abaixo do frontmatter é o cérebro dele. Adapte ao setor do aluno.
- **Criar um agente novo:** no terminal embutido, rode `claude` e peça: "crie um agente em .claude/agents/ que [tarefa], gatilho [frase]".
- **Mudar um botão:** edite o comando em Settings → Shell commands (só o texto entre aspas).

---

## Detalhe: a pasta `.claude`

O Obsidian esconde pastas que começam com ponto e **o Dataview nem indexa elas** — por isso uma query `FROM ".claude/agents"` volta vazia. O painel "Agentes instalados" contorna isso com um bloco `dataviewjs` que lê `.claude/agents` direto pelo `app.vault.adapter` e renderiza os agentes como **cards** (nome, badge do modelo, função e chips de gatilho); funciona sem renomear nada e sem depender de indexação. O plugin **Hidden Folders Access** (já na lista) serve só pra você *ver* a pasta no explorador, se quiser. Não renomeie a pasta para `Agents/`: o Claude Code descobre os agentes a partir de `.claude/agents/`.
