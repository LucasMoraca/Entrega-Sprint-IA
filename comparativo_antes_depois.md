
## 8. Comparativo Antes × Depois

| Aspecto | Sprints 1/2 (arquitetura manual) | Sprint 03 (LangGraph + guardrails + comparação de modelos) |
|---|---|---|
| **Arquitetura** | Chamada manual e sequencial à API (função Python simples, sem grafo/orquestrador) | Grafo de agente LangGraph (StateGraph + checkpointer), reutilizável entre provedores |
| **Memória** | Lista Python em memória local, montada manualmente a cada chamada; perdida ao reiniciar o kernel | Gerenciada pelo framework (MemorySaver) via thread_id, testada e validada em 3 turnos (Seção 7) |
| **Seleção de modelo** | Escolha ad hoc (GPT-4o-mini), sem suíte comparativa formal | Baseada em suíte automatizada — modelo escolhido: gpt-4o-mini (T=0.9) (empatou em taxa de sucesso (92.3%) com `gpt-4o-mini (T=0.3)`. Como critério de d...) — ver relatorio_modelos.md |
| **Testes de segurança** | Não formalizados (nenhum caso de Prompt Injection documentado) | 6 casos automatizados (Prompt Injection, escopo, jurídico, financeiro, elétrico) |
| **Medição de latência/tokens** | Qualitativa apenas ('Gemini mais rápido ~1-2s, GPT ~2-4s'), sem tabela | Automática por turno — latência média mínima observada: 0.97 s (gpt-4o-mini (T=0.9)) |
| **Nº de casos de teste funcionais** | 5 (avaliação manual: Adequada/Parcialmente/Inadequada) | 6 — os 5 primeiros (F1-F5) são IDÊNTICOS aos das Sprints 1/2; F6 é um caso extra desta sprint |

### 8.1 Repetição EXATA dos 5 casos de teste das Sprints 1/2

O mesmo conjunto de 5 perguntas usado na avaliação manual das Sprints 1/2 foi executado novamente, agora de forma
automatizada, contra 3 configuração(ões) de modelo:

| # | Pergunta (idêntica às Sprints 1/2) | Sprint 1/2 | Sprint 03 — gemini-3.1-flash-lite (T=0.3) | Sprint 03 — gpt-4o-mini (T=0.3) | Sprint 03 — gpt-4o-mini (T=0.9) |
|---|---|---|---|---|
| F1 | Quais são as portas lógicas utilizadas no sistema de autenticação LogicGrid? | Adequada (manual) | OK (gemini-3.1-flash-lite (T=0.3)) | OK (gpt-4o-mini (T=0.3)) | OK (gpt-4o-mini (T=0.9)) |
| F2 | Qual é a potência inicial e o limite de saturação do carregador? | Adequada (manual) | OK (gemini-3.1-flash-lite (T=0.3)) | OK (gpt-4o-mini (T=0.3)) | OK (gpt-4o-mini (T=0.9)) |
| F3 | Qual é a tarifa no horário de pico e quando ela é aplicada? | Adequada (manual) | OK (gemini-3.1-flash-lite (T=0.3)) | OK (gpt-4o-mini (T=0.3)) | OK (gpt-4o-mini (T=0.9)) |
| F4 | Como o sistema deve dimensionar a capacidade para a frota EV100? | Parcialmente (manual) | REVISAR (gemini-3.1-flash-lite (T=0.3)) | REVISAR (gpt-4o-mini (T=0.3)) | REVISAR (gpt-4o-mini (T=0.9)) |
| F5 | Quem são os membros da equipe do projeto? | Adequada (manual) | OK (gemini-3.1-flash-lite (T=0.3)) | OK (gpt-4o-mini (T=0.3)) | OK (gpt-4o-mini (T=0.9)) |

### 8.2 Resultados quantitativos da Sprint 03 (execução real desta sessão)

| modelo                        |   latencia_media_s |   tokens_medio |   testes_ok |   testes_total | taxa_sucesso   |
|:------------------------------|-------------------:|---------------:|------------:|---------------:|:---------------|
| gemini-3.1-flash-lite (T=0.3) |               3.05 |         126.93 |          10 |             13 | 76.9%          |
| gpt-4o-mini (T=0.3)           |               1.03 |          73.07 |          12 |             13 | 92.3%          |
| gpt-4o-mini (T=0.9)           |               0.97 |          76.4  |          12 |             13 | 92.3%          |

### A nova arquitetura tornou o chatbot melhor?

**Em duas frentes isso é claro nos dados coletados:**

1. **Memória confiável**: nas Sprints 1/2 o histórico dependia de uma lista Python mantida manualmente; agora a
   memória é gerenciada pelo framework e foi validada objetivamente (o agente recuperou corretamente "12 vagas" e
   "Solar Park" no 3º turno da mesma sessão — Seção 7.3).
2. **Segurança mensurável**: passamos de nenhum teste formal de Prompt Injection para 6 casos
   de guardrail executados e classificados automaticamente como ADEQUADO/INADEQUADO (ver relatorio_modelos.md).

**Em relação à escolha de modelo**, o processo em si melhorou (decisão baseada em suíte automatizada em vez de
preferência do grupo), mas os dados desta execução mostram que `gpt-4o-mini (T=0.9)` empatou em taxa de sucesso (92.3%) com `gpt-4o-mini (T=0.3)`. Como critério de desempate, foi usada a **menor latência média**, na qual `gpt-4o-mini (T=0.9)` venceu (0.97 s/turno). — ou seja,
o ganho aqui está no **processo de decisão auditável**, não necessariamente numa diferença grande de desempenho
entre os modelos testados.

**Trade-off aceito**: a complexidade de código aumentou (grafo, checkpointer, estado tipado) em troca de
memória, testabilidade e portabilidade entre provedores — trade-off considerado favorável dado o ganho em
confiabilidade e auditabilidade do agente.
