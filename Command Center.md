---
cssclasses:
  - command-center
---

# ⏤\/⏤ AGENTIC OS · Marketing

`= "● LIVE · " + dateformat(date(now), "cccc, dd 'de' LLLL yyyy")`

## Ações rápidas

```meta-bind-button
label: Radar de mercado
style: primary
actions:
  - type: command
    command: obsidian-shellcommands:shell-command-radar-mercado
```
```meta-bind-button
label: Gerar pautas
style: default
actions:
  - type: command
    command: obsidian-shellcommands:shell-command-gerar-pautas
```
```meta-bind-button
label: Analisar concorrente
style: default
actions:
  - type: command
    command: obsidian-shellcommands:shell-command-analise-concorrente
```
```meta-bind-button
label: Relatório semanal
style: default
actions:
  - type: command
    command: obsidian-shellcommands:shell-command-relatorio-semanal
```
```meta-bind-button
label: Abrir navegador
style: default
actions:
  - type: command
    command: obsidian-shellcommands:shell-command-open-browser
```

> Botões chamam comandos prontos do Shell commands. Se algum não achar, abra o seletor do Meta Bind e escolha pela lista.

## Resultados dos agentes (output)

```dataview
TABLE tipo AS "Tipo", file.mtime AS "Quando"
FROM "output"
WHERE file.name != "_sobre"
SORT file.mtime DESC
LIMIT 8
```

## Meus agentes

```dataview
TABLE description AS "O que faz", model AS "Modelo"
FROM ".claude/agents"
SORT file.name ASC
```

## Base de conhecimento (wiki)

```dataview
LIST
FROM "wiki"
WHERE file.name != "index" AND file.name != "log"
SORT file.mtime DESC
LIMIT 8
```
