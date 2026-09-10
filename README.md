# EV Challenge — GoodWe | Sprint 03 — Entrega

Projeto: **ChargeGrid Intelligence** | Disciplina: Prompt and Artificial Intelligence | FIAP (1CCPX) | Grupo 7

## Estrutura da entrega

```
.
├── codigo_fonte/
│   └── AI_assistant_sprint3.ipynb   ← notebook principal (código-fonte completo da aplicação)
├── casos_de_teste/                  ← gerado ao rodar a Seção 7 do notebook (ver abaixo)
├── relatorio_modelos.md             ← gerado ao rodar a Seção 7 do notebook
├── relatorio_evolucao.pdf           ← gerado ao rodar a Seção 10 do notebook (≤ 5 páginas)
├── comparativo_antes_depois.md      ← gerado ao rodar a Seção 8 do notebook
├── integrantes.txt                  ← nome, RM e turma dos integrantes
└── .gitignore                       ← garante que .env nunca é versionado
```

## Importante: todos os resultados vêm de execução real

Diferente de uma versão anterior desta entrega, **não há nenhum dado simulado ou de referência aqui**.
Todos os arquivos de resultado (`relatorio_modelos.md`, `comparativo_antes_depois.md`, `relatorio_evolucao.pdf`
e a pasta `casos_de_teste/`) são gerados **exclusivamente** ao executar o notebook
`codigo_fonte/AI_assistant_sprint3.ipynb` no Google Colab, chamando de verdade a API da OpenAI e do Google Gemini
com as chaves do grupo. Não existe nenhum script auxiliar de "dados de referência" nesta entrega — o que está
nos arquivos de resultado é exatamente o que os modelos responderam na última execução completa do notebook.

## Como gerar (ou regerar) os arquivos de resultado

1. Abra `codigo_fonte/AI_assistant_sprint3.ipynb` no Google Colab.
2. Configure os Secrets `OPENAI_API_KEY` e `GEMINI_API_KEY` (Seção 2 do notebook).
3. Execute todas as células, de cima para baixo (Runtime → Run all).
4. A Seção 7 chama a OpenAI e o Gemini de verdade e roda a suíte de testes (funcionais — incluindo os 5 casos
   idênticos às Sprints 1/2 —, memória e segurança/Prompt Injection/invenção de especificações).
5. A Seção 7.4 exporta `relatorio_modelos.md`; a Seção 7.5 aplica automaticamente o modelo/temperatura vencedor
   ao chat da Seção 4; a Seção 7.6 exporta a pasta `casos_de_teste/`; a Seção 8 exporta
   `comparativo_antes_depois.md`; e a Seção 10 exporta `relatorio_evolucao.pdf` — todos com os resultados
   **reais** dessa execução.
6. Baixe os arquivos gerados pelo painel de arquivos do Colab (`relatorio_modelos.md`, `relatorio_evolucao.pdf`,
   `comparativo_antes_depois.md` e a pasta `casos_de_teste/`) e substitua os desta pasta antes do commit final.

Como os modelos de linguagem têm componente probabilístico, pequenas variações entre execuções são esperadas —
isso é normal e não indica erro.

