---
tipo: sintese
data: 2026-06-18
---

# Síntese — Arquitetura do Command Center

Decisão fechada na reunião: agentes ficam como markdown em `.claude/agents`, e a operação segue três camadas — `raw/` (fonte que entra), `output/` (resultado do agente) e `wiki/` (conhecimento curado). Execução começa sob demanda (botão), com medição de custo, antes de pensar em agendamento. A VPS com modelo local fica como horizonte de próxima aula; o vault permanece a fonte de verdade.

[origem: raw/transcricoes/2026-06-18-weslley-renato-arquitetura.md]
