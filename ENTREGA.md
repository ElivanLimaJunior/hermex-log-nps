# Índice da entrega — Checkpoint Nível 1 (Hermex Log)

Este arquivo liga cada missão do enunciado ao arquivo que a atende.

- O **[RELATORIO_DO_PROJETO.md](RELATORIO_DO_PROJETO.md)** explica o projeto completo: os dados, cada etapa, cada visualização do dashboard com seus números, os insights e as recomendações.
- O **[README.md](README.md)** traz a visão geral.

Para as etapas executadas em plataformas externas (ChatGPT, Miro, Google Sheets e Forms, n8n, Looker Studio, Notion), a entrega traz **todo o conteúdo necessário para reproduzi-las**: textos para colar, arquivos para importar, configurações passo a passo e os resultados esperados.

---

## Instruções iniciais

| Item | Onde |
|---|---|
| Datasets do projeto | `dados/pesquisa_satisfacao.csv`, `dados/handoff_vendas_posvenda.csv` |
| Dicionário de dados e verificação de qualidade | `RELATORIO_DO_PROJETO.md`, seção 3 |

## 1ª Etapa — Assistente GPT para comunicação de prazos

| Missão | Onde |
|---|---|
| Planejamento: (a) problema, (b) critérios (estado, tipo de frete, dias úteis), (c) formato de saída | `etapa-1-assistente-gpt/1_planejamento_assistente.txt` |
| Matriz CSD e como cada categoria é tratada nas instruções | `etapa-1-assistente-gpt/1_planejamento_assistente.txt` (seção Matriz CSD) |
| Briefing: personalidade, cadeia de pensamento (5 etapas numeradas), formato de saída, cuidados | `etapa-1-assistente-gpt/2_briefing_hermex_prazos.txt` |
| Criação do GPT "Hermex Prazos": descrição, instruções, recursos desabilitados, quebra-gelos | `etapa-1-assistente-gpt/3_configuracao_gpt.txt` |
| Testes SP, BA e AM, com respostas esperadas e critérios de avaliação | `etapa-1-assistente-gpt/4_testes_assistente.txt` |

## 2ª Etapa — Mapeamento do pós-vendas e responsabilidades

| Missão | Onde |
|---|---|
| Fluxograma com simbologia (ovais, atividades, losangos) e looping | `etapa-2-processo-raci/1_fluxograma_posvendas.txt` (especificação) e `etapa-2-processo-raci/fluxograma_posvendas.md` (diagrama Mermaid) |
| Atividades candidatas à automação (borda vermelha) com os 5 critérios | mesmos arquivos (seção "Anotações de automação") |
| Matriz RACI: 13 atividades × 5 papéis | `etapa-2-processo-raci/matriz_raci.csv` e `etapa-2-processo-raci/2_matriz_raci.txt` |
| Importação do handoff e verificação da estrutura para gatilho no n8n | `etapa-2-processo-raci/3_verificacao_planilha_handoff.txt` |
| Justificativa do handoff como ponto mais crítico (≥ 3 critérios) | `etapa-2-processo-raci/4_justificativa_handoff.txt` (5 de 5 critérios) |

## 3ª Etapa — Automação do NPS com n8n e IA

| Missão | Onde |
|---|---|
| Dataset no Sheets e Google Forms (ID, Nota NPS, Comentário) gravando na planilha | `etapa-3-automacao-n8n/1_google_forms_e_planilha.txt` |
| Workflow "Hermex — NPS Automação" com gatilho do Google Sheets e Pin Data | **`etapa-3-automacao-n8n/hermex_nps_automacao.json`** (importável) e `etapa-3-automacao-n8n/4_importar_e_configurar_n8n.txt` |
| Nó IF (nota < 6) e Gemini classificando em uma única palavra | o JSON acima e `etapa-3-automacao-n8n/2_prompt_gemini.txt` |
| Gmail para o pós-vendas (cliente, nota, categoria, comentário) com `{{$json['campo']}}` | `etapa-3-automacao-n8n/3_emails.txt` e o JSON |
| Gmail de agradecimento ao cliente (nota ≥ 6) | `etapa-3-automacao-n8n/3_emails.txt` e o JSON |
| Testes: detrator e promotor (e cenários extras) | `etapa-3-automacao-n8n/5_testes_workflow.txt` e `etapa-3-automacao-n8n/gabarito_classificacao.csv` |

## 4ª Etapa — Dashboard no Looker Studio e base no Notion

| Missão | Onde |
|---|---|
| Conexão da fonte e tipos de campo (geográfico, datas, número) | `etapa-4-dashboard-notion/1_looker_studio_passo_a_passo.txt` |
| Campos calculados: Promotores, Detratores, NPS, Dias até envio, Dias até entrega | mesmo arquivo (passo 3) e `dados/pesquisa_satisfacao_enriquecida.csv` |
| 4 visualizações (scorecards, mapa, barras, tabela) e **os dados de cada uma** | `RELATORIO_DO_PROJETO.md` seção 7.3, `dados/indicadores_por_estado.csv`, `dados/indicadores_por_regiao.csv` e `etapa-4-dashboard-notion/2_valores_esperados.txt` |
| Database "Processos Hermex Log": Devolução, Reembolso, SLA por Região | `etapa-4-dashboard-notion/3_notion_base_conhecimento.md` |
| Governança de dados: (a) responsáveis, (b) frequência, (c) riscos, (d) dados semânticos × brutos | `etapa-4-dashboard-notion/4_governanca_dados.txt` |

## Conclusão — compartilhamento

| Item | Onde |
|---|---|
| README detalhado (cenário, perguntas, ferramentas, desafios, insights, recomendações) | `README.md` |
| Relatório completo do projeto | `RELATORIO_DO_PROJETO.md` |

---

## Decisões registradas

1. **Detrator no n8n = nota < 6**, como pede o enunciado. O Looker usa < 7 (padrão NPS). O impacto está no `RELATORIO_DO_PROJETO.md`, seção 10.1.
2. **Uma tabela de prazos única** para o GPT e o Notion: SP 2–4; Sudeste 2–5; Sul 3–6; Centro-Oeste 4–7; Nordeste 6–12; Norte 8–16 dias úteis.
3. **Frete expresso tratado como Dúvida** na Matriz CSD: o GPT não promete prazo expresso.
4. **Busca do nome e do e-mail do cliente pelo `id_pedido`** no workflow, porque o Forms coleta só ID, nota e comentário.
