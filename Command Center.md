---
cssclasses:
  - command-center
---

<div class="cc-console">
  <div class="cc-chrome">
    <span class="cc-dots"><i></i><i></i><i></i></span>
    <span class="cc-path">agentic-os://marketing</span>
    <span class="cc-live"><i></i>LIVE</span>
  </div>
  <div class="cc-brand">
    <div class="cc-prompt"><span class="cc-dir">~/marketing</span> <span class="cc-arrow">❯</span> <span class="cc-cmd">launch command-center</span></div>
    <h1>AGENTIC&nbsp;OS<span class="cc-cursor">▮</span></h1>
    <p class="cc-sub">Central de comando · clientes, campanhas, conteúdo e mercado num só lugar.</p>
  </div>
  <div class="cc-pipeline">
    <span class="cc-stage">raw</span><span class="cc-flow">→</span><span class="cc-stage">output</span><span class="cc-flow">→</span><span class="cc-stage cc-stage-on">wiki</span>
    <span class="cc-tag">6 agentes online</span>
  </div>
</div>

`= "● SYNC · " + dateformat(date(now), "cccc, dd 'de' LLLL yyyy · HH:mm")`

## Deploy de agentes

```meta-bind-button
label: Radar de mercado
icon: radar
style: primary
class: cc-cmd-btn
actions:
  - type: command
    command: obsidian-shellcommands:shell-command-radar-mercado
```

```meta-bind-button
label: Gerar pautas
icon: lightbulb
style: default
class: cc-cmd-btn
actions:
  - type: command
    command: obsidian-shellcommands:shell-command-gerar-pautas
```

```meta-bind-button
label: Analisar concorrente
icon: telescope
style: default
class: cc-cmd-btn
actions:
  - type: command
    command: obsidian-shellcommands:shell-command-analise-concorrente
```

```meta-bind-button
label: Qualificar lead
icon: user-check
style: default
class: cc-cmd-btn
actions:
  - type: command
    command: obsidian-shellcommands:shell-command-qualificador-leads
```

```meta-bind-button
label: Revisar copy
icon: pen-tool
style: default
class: cc-cmd-btn
actions:
  - type: command
    command: obsidian-shellcommands:shell-command-revisor-de-copy
```

```meta-bind-button
label: Relatório semanal
icon: file-text
style: default
class: cc-cmd-btn
actions:
  - type: command
    command: obsidian-shellcommands:shell-command-relatorio-semanal
```

```meta-bind-button
label: Abrir navegador
icon: globe
style: default
class: cc-cmd-btn cc-btn-util
actions:
  - type: command
    command: obsidian-shellcommands:shell-command-open-browser
```

> Cada botão dispara um comando do Shell commands que roda o agente e salva a saída em `output/`. Não achou algum? Abra o seletor do Meta Bind e escolha pela lista.

## Últimos outputs

```dataview
TABLE WITHOUT ID ("▸ " + file.link) AS "Resultado", tipo AS "Tipo", dateformat(file.mtime, "dd/MM HH:mm") AS "Gerado"
FROM "output"
WHERE file.name != "_sobre"
SORT file.mtime DESC
LIMIT 8
```

## Agentes instalados

```dataviewjs
// .claude é uma dotfolder: o índice do Dataview não a vê.
// Lemos direto pelo adapter e renderizamos cards (mais legível que tabela).
const dir = ".claude/agents";
const grid = dv.container.createEl("div", { cls: "cc-agents" });
try {
  const listing = await app.vault.adapter.list(dir);
  const files = (listing.files || []).filter(p => p.endsWith(".md")).sort();
  for (const path of files) {
    const raw = await app.vault.adapter.read(path);
    const fm = raw.match(/^---\r?\n([\s\S]*?)\r?\n---/);
    let name = path.split("/").pop().replace(/\.md$/, "");
    let desc = "", model = "";
    if (fm) {
      const get = (k) => {
        const m = fm[1].match(new RegExp("^" + k + ":\\s*(.+)$", "m"));
        return m ? m[1].trim().replace(/^["']|["']$/g, "") : "";
      };
      name = get("name") || name;
      desc = get("description");
      model = get("model");
    }
    const triggers = [...desc.matchAll(/["“”']([^"“”']+)["“”']/g)].map(m => m[1]);
    const func = (desc.split(/\bUse quando\b/i)[0] || desc).trim();
    const card = grid.createEl("div", { cls: "cc-agent-card" });
    const head = card.createEl("div", { cls: "cc-agent-head" });
    head.createEl("span", { cls: "cc-agent-name", text: name });
    if (model) head.createEl("span", { cls: "cc-agent-model", text: model });
    card.createEl("div", { cls: "cc-agent-desc", text: func || desc });
    if (triggers.length) {
      const tags = card.createEl("div", { cls: "cc-agent-tags" });
      for (const t of triggers) tags.createEl("span", { cls: "cc-agent-tag", text: t });
    }
  }
} catch (e) {
  dv.paragraph("⚠️ Não consegui ler `.claude/agents`: " + e.message);
}
```

## Base de conhecimento

```dataview
LIST
FROM "wiki"
WHERE file.name != "index" AND file.name != "log"
SORT file.mtime DESC
LIMIT 8
```
