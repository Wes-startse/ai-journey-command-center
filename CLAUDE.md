# CLAUDE.md — Command Center de Marketing

> Lido pelo agente no início de toda sessão. Define o que este vault é, como se organiza e como os agentes trabalham nele.

## 1. O que é este vault

Um Second Brain de **marketing e negócio**: a memória viva da operação (clientes, campanhas, conteúdo, mercado) que a IA organiza, alimenta e consulta em linguagem natural. A `Command Center.md` na raiz é a porta de entrada. Os agentes ficam em `.claude/agents/` e trabalham sobre este conhecimento.

Não é um repositório de arquivos parados: é base consultável. Tudo que um agente produz vira nota datada e rastreável.

## 2. Arquitetura (3 camadas)

```
/
├── CLAUDE.md            ← este arquivo (schema)
├── Command Center.md    ← painel de entrada (Dataview + botões)
├── raw/                 ← fontes imutáveis (read-only para o agente)
│   ├── clippings/       ← artigos web (Web Clipper), referências
│   ├── briefings/       ← briefings de cliente e de campanha
│   └── transcricoes/    ← reuniões, calls, áudios transcritos
├── wiki/                ← conhecimento curado (read-write)
│   ├── index.md         ← catálogo
│   ├── log.md           ← histórico append-only
│   ├── clientes/        ← uma nota por cliente/conta
│   ├── campanhas/       ← briefings e resultados de campanha
│   ├── conteudo/        ← pautas e calendário editorial
│   ├── mercado/         ← concorrentes e tendências
│   ├── conceitos/       ← playbooks e definições (ICP, funnel, CAC)
│   └── sinteses/        ← análises consolidadas a partir do output
└── output/              ← resultados crus dos agentes (datados)
```

Fluxo: **raw/ entra → o agente processa → output/ sai → você promove o que vale pra wiki/.**

**Regra dura:** o agente nunca modifica `raw/`. Lê e cita. O resultado de cada run cai em `output/`; o conhecimento que você decide manter é curado em `wiki/`.

## 3. Convenções

- **Nomes de arquivo:** kebab-case, sem acento, sem espaço (`exemplo-cliente.md`). Datas no formato `AAAA-MM-DD` no título quando a nota é de um dia.
- **Frontmatter por tipo:** `tipo: cliente | campanha | pauta | mercado | conceito | sintese`; pautas usam também `status: ideia | produzindo | publicado`. É o que faz os painéis Dataview funcionarem.
- **Toda saída cita a fonte.** Sem link/origem, não entra como verdade. Conhecimento sem rastreabilidade é boato.

## 4. Os agentes

Cada agente é um arquivo markdown em `.claude/agents/` no formato de subagent do Claude Code: frontmatter (`name`, `description` com gatilhos, `tools`, `model`, `mcpServers`, `skills`) e corpo com as instruções. Para criar: "crie um agente em .claude/agents/ que [tarefa], gatilho [frase]".

Já vêm prontos: `radar-mercado`, `gerador-de-pautas`, `analise-concorrente`, `qualificador-leads`, `revisor-de-copy`, `relatorio-semanal`.

## 5. Operações

- **Ingest:** ao receber uma fonte (artigo em `raw/clippings`, briefing em `raw/briefings`, transcrição), o agente resume, cria a nota na pasta certa do `wiki/` com frontmatter, linka e atualiza `wiki/index.md` e `wiki/log.md`. Nunca toca `raw/`.
- **Query:** perguntas sobre a operação são respondidas a partir do `wiki/`, citando a fonte.
- **Run de agente:** acionado pelos botões da Command Center ou em linguagem natural pela frase de gatilho; o resultado é salvo em `output/` com data e frontmatter.
- **Lint (opcional):** revisar duplicatas, notas órfãs e links quebrados; só relatório, sem corrigir sem aprovação.

## 6. Governança

- O que entra: conhecimento de marketing e negócio. O que não entra sem critério: dado pessoal sensível e informação sob sigilo (LGPD).
- Custo do Claude é visível e controlável: rode o que dá retorno.
- Os comandos dos botões rodam no seu sistema. Use só comandos que você confia.

## 7. Tom do conteúdo gerado

PT-BR direto, sem consultorês ("alavancar", "robusto", "endereçar" fora). Termos técnicos de marketing em inglês preservados (CTR, funnel, awareness, lead, CAC). Conclusão primeiro. Sem encher de bullet.
