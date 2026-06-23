---
tipo: transcricao
participantes: [Weslley, Renato]
data: 2026-06-18
fonte: reuniao
---

# Transcrição — Weslley × Renato · Arquitetura do Command Center (18/06/2026)

> Dados fictícios, para uso didático.

**Weslley:** Renato, fechei o desenho do command center da turma. A ideia é cada agente ser um markdown em `.claude/agents`, e o resultado cair numa pasta `output`.

**Renato:** Faz sentido manter o agente como arquivo. Versiona fácil e qualquer um abre. Só cuida pra não misturar o que é fonte com o que é resultado.

**Weslley:** Por isso separei: `raw` pra fonte que entra, `output` pro que o agente gera, e `wiki` pro que a gente decide manter.

**Renato:** Bom. Pro custo, segura o impulso de deixar tudo rodando direto. Começa sob demanda, botão, e mede. Quando virar rotina, a gente pensa em agendar.

**Weslley:** E o passo da VPS? Queria mostrar pra turma como horizonte.

**Renato:** Deixa como horizonte mesmo. Primeiro a galera sente o valor rodando local. Depois a gente sobe os agentes pra rodar sozinhos, com modelo local pra não pesar no token. O vault continua sendo a fonte de verdade, isso não muda.

**Weslley:** Perfeito. Então a aula fecha em: montar o command center funcional com plugins, criar um agente, rodar, ver o resultado no output. VPS na próxima.

**Renato:** Fechado. Manda o starter que eu reviso os prompts dos agentes.
