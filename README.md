# Predição de Balneabilidade com Machine Learning

TCC do MBA em Ciências de Dados (turma T9) — previsão se uma praia está própria ou imprópria para banho a partir de dados climáticos, sem esperar pelo resultado do exame de coliformes (que pode levar até 7 dias).

O modelo combina 11.026 laudos de análise da água da SEMACE (2014–2022) com dados climáticos do INMET (estação A305, Fortaleza). O melhor resultado foi um XGBoost, na configuração baseline (sem ajuste de hiperparâmetros), com **96,71% de acurácia** (validação cruzada, 5 dobras, ± 0,38 ponto percentual) — estatisticamente empatado com as duas melhores alternativas testadas, mas escolhido por ser a mais simples entre elas.

O texto completo do trabalho, com toda a metodologia, análise e discussão dos resultados, está em [`TCC_Wagner_Oliveira_T9.pdf`](TCC_Wagner_Oliveira_T9.pdf).

## Sobre os dados

A pasta `dados/` tem uma **amostra anonimizada de 200 linhas** dos dados usados no trabalho — não o dataset completo (que tem mais de 11 mil laudos e pertence à SEMACE). A amostra serve pra dar uma ideia real da estrutura dos dados e permitir conferir os passos de tratamento do notebook, mas não é suficiente pra reproduzir os resultados do TCC (pra isso precisaria do dataset completo).

Antes de publicar, removi da amostra qualquer coluna que identificasse pessoas: o nome do responsável técnico pelo laudo (`responsavel`) e os IDs internos de usuário/cliente do sistema da SEMACE (`usuario_id`, `cliente_id`). Nenhuma dessas colunas era usada como variável no modelo.

- `dados/dadosbalneabilidade_amostra.csv` — amostra dos laudos SEMACE, já anonimizada.
- `dados/inmet_filtrado_amostra.csv` — amostra dos dados climáticos do INMET.

## Sobre o notebook

`notebooks/analise_balneabilidade_corrigida.ipynb` é o notebook completo de análise: limpeza dos dados, extração de variáveis por fuzzy matching (RapidFuzz) a partir do texto livre dos laudos, e treinamento dos modelos em 3 fases incrementais de variáveis.

Os outputs (gráficos, tabelas, prints) foram removidos antes de publicar — o notebook aqui é só código, pra leitura e conferência da metodologia. Como ele foi escrito pra rodar sobre o dataset completo (não a amostra publicada), não dá pra executar ele do início ao fim só com o que está neste repositório.

## Licença

Código sob licença MIT (ver [`LICENSE`](LICENSE)). Os dados de amostra são derivados de laudos públicos da SEMACE (órgão ambiental do Governo do Ceará) e dados públicos do INMET, disponibilizados aqui já anonimizados.
