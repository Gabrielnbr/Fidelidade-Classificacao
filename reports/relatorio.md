# Relatório do Projeto — Histórico de Decisões por Notebook

> Cada tabela abaixo registra as ações realizadas em um notebook ao longo dos ciclos do projeto.
>
> **Colunas:**
> - `id` — sequencial dentro do notebook (1, 2, 3...)
> - `ciclo` — número do ciclo CRISP-DM em que a ação foi tomada
> - `ação` — o que foi feito (verbo no infinitivo)
> - `decisão` — justificativa / racional da ação
> - `resultado` — efeito observado
> - `ativo` — `Sim` ou `Não`
> - `ciclo_fim` — número do ciclo em que a ação foi **inativada**. Preencher apenas quando `ativo = Não`.
> - `motivo` — explica o **porquê** da inativação. Preencher apenas quando `ativo = Não`.

---

## `1.0.descricao_dados`

No ciclo 1, na primeira iteração do projeto, optei por iniciar fazendo o modelo RFM, afim de entregar valor coma mais agilidade.

| id   | ciclo | ação | decisão | resultado | ativo | ciclo_fim | motivo |
| ---- | ----- | ---- | ------- | --------- | ----- | --------- | ------ |
| 1    | 1     | Renomear colunas para snake_case | Mais bonitinho de trabalhar | Colunas em snake_case | sim |  |  |
| 2    | 1     | Remover NAs em description e customer_id | 1º ciclo, só montar o pipe | Retirado 135000 linhas | sim |  |  |
| 3    | 1     | Converter invoice_date para datetime | Tratamento padrão | datetime64[ns] aaaa/mm/dd | sim |  |  |
| 4    | 1     | Converter customer_id para int | Tratamento padrão | int | sim |  |  |
| 5    | 1     | Exportar df para data/interim/1.descricao.pkl | para ser utilizado pelos próximos notebooks | novo arquivo de dados em pkl | sim |  |  |
| 6    | 2     | Separar variáveis numéricas e categóricas | gerar análise inicial | 2 novos df | sim |  |  |
| 7    | 2     | Gerar estatística descritiva das variáveis numéricas | análise inicial | Tabela estatística descritiva | sim |  |  |
| 8    | 2     | Plotar histogramas das variáveis numéricas | verificar distribuição | Conjunto de histogramas | sim |  |  |
| 9    | 3     | Identificar invoice_no com caracteres não-numéricos (potenciais cancelamentos) | Identificações de contexto de sucesso ou insucesso da compra | Confirmação da variabilidade do contexto de compra, especificado no próprio notebook na seção 1.4 . Necessidade de diversos tipos de tratamento a serem realizados no notebook 2.0 ainda neste ciclo | sim |  |  |
| 10   | 3     | Identificar stock_code com caracteres não-numéricos (códigos não-produto) | Identificar contexto na variabilidade de tipos de categorização do estoque | Confirmação da variabilidade na classificação dos itens em estoque, especificado no próprio notebook na seção 1.4 . Necessidade de diversos tipos de tratamento a serem realizados no notebook 2.0 ainda neste ciclo| sim |  |  |
| 11   | 4     | Estudar a coluna `description` | Coluna ainda não estudada | São as descrições dos produtos, a princípio não tem muito o que ser feito com ela. Outras observações no notebook 1.0 | sim |  |  |
| 12   | 4     | Estudar a coluna `country` | Coluna ainda não estudada | São 37 países com quase 90% concentrado em 1 único país. Bem desbalanceado. Talvez mudar com lat-lon central. | sim |  |  |
|    |      |  |  |  |  |  |  |


---

## `2.0.filtragem_var`

| id | ciclo | ação | decisão | resultado | ativo | ciclo_fim | motivo |
| -- | ----- | ---- | ------- | --------- | ----- | --------- | ------ |
| 1  | 3     | Filtrar unit_price >= 0.04 | Retirar todos os valores de produtos zerados, pode ser sujeira, ainda tenho que analizar mais em ciclo próximo | retirado as linhas | sim |  |  |
| 2  | 3     | Excluir stock_codes especiais (POST, D, C2, M, BANK CHARGES, PADS, DOT, CRUK) | Retirados, pois não irei trabalha-los agora. Quero testar o comportamento do modelo. | retirado as linhas | sim |  |  |
| 3  | 3     | Separar quantity em df_compras (>0) e df_returns (<0) | Valores negativos em quantity foi identificado o insucesso da compara podendo ser retorno, mudança, cancelamento ou outros. Para o RFM muitas devoluções ou cancelamentos, talvez não seja um bom cliente. Explicações complementare notebook 1.0 seção 1.4. | Gerado mais 2 DF | sim |  |  |
| 4  | 3     | Exportar df, df_compras e df_returns para data/interim/2.*.pkl | deixei 3 DF, poi 1 contém todo o histórico e os outros 2 possuem a separação do sucesso da compra  | 3 DF ao total | sim |  |  |
| 5  | 4    | Retirar coluna `description` | Não há necessidade dela no momento | Retirado a coluna | sim |  |  |
| 6  | 4    | Remover colunas 'European Community' e 'Unspecified' | Não são países ou são sujeiras. | Retirado linhas | sim |  |  |
|    |      |  |  |  |  |  |  |

---

## `3.0.feature_engineering`

| id | ciclo | ação | decisão | resultado | ativo | ciclo_fim | motivo |
| -- | ----- | ---- | ------- | --------- | ----- | --------- | ------ |
| 1  | 1     | Criar feature `faturamento` = quantity × unit_price | Base para Fórmula RFM | Nova Feature | sim |  |  |
| 2  | 1     | Calcular feature `monetário` (soma de faturamento por cliente) | Monetary do RFM | Nova Feature | sim |  |  |
| 3  | 1     | Calcular feature `recencia_days` (dias desde a última compra) | Recencia do RFM | Nova Feature | sim |  |  |
| 4  | 1     | Calcular feature `frequencia` (contagem de invoice_no únicos por cliente) | Frequencia do RFM | Nova Feature | sim |  |  |
| 5  | 1     | Exportar df para data/interim3.0.fe.pkl | para ser utilizar pelos próximos notebooks | novo arquivo de dados em pkl | sim |  |  |
| 6  | 2     | Calcular feature `avg_faturamento` (média de faturamento por cliente) | Média do Faturamento | Nova Feature | sim |  |  |
| 7  | 3     | Calcular feature `retornos` (contagem de invoice_no únicos em df_returns) | calculo da quantidade de insucesso na venda | Nova Feature | sim |  |  |
| 8   | 3      | Calcular a partir dos dados separados dos df de compras ou devoluções  | Os dados são os mesmo a qualidade é que está mudando, estou tratando de forma separada os dados de sucesso ou insucesso das compras. Até agora estavam todos juntos. | (`RFM` e `AVG_F` -> `df_compras`) & (`retornos` -> `df_returns`) | sim |  |  |

---

## `4.0.eda`

| id | ciclo | ação | decisão | resultado | ativo | ciclo_fim | motivo |
| -- | ----- | ---- | ------- | --------- | ----- | --------- | ------ |
|    |       |      |  |  |  |  |  |

---

## `5.0.data_preparation`

| id | ciclo | ação | decisão | resultado | ativo | ciclo_fim | motivo |
| -- | ----- | ---- | ------- | --------- | ----- | --------- | ------ |
| 1  | 3     | Aplicar MinMaxScaler em todas as colunas exceto customer_id | diminuir tamanho da escala para reduzir ruído | mms aplicado | sim |  |  |
| 2  | 3     | Exportar df para data/interim/5.data_prep.pkl | para ser utilizar pelos próximos notebooks | novo arquivo de dados em pkl | sim |  |  |
| 3  | 4     | Aplicar `np.log1p` em todas as colunas exceto customer_id | foi tentado com `np.log`, mas gerou muitos NaN devido a valores 0, tentativa de diminuir o pico e organizar a curva | Melhorou só um pouco a curva, vamos ver o impacto mais a frente | sim |  |  |

---

## `6.0.feature_selection`

| id | ciclo | ação | decisão | resultado | ativo | ciclo_fim | motivo |
| -- | ----- | ---- | ------- | --------- | ----- | --------- | ------ |
|    |       |      |  |  |  |  |  |

---

## `7.0.Hyperparametros_fine-tunning`

| id | ciclo | ação | decisão | resultado | ativo | ciclo_fim | motivo |
| -- | ----- | ---- | ------- | --------- | ----- | --------- | ------ |
| 2  | 1     | Montar pipeline para testes KMeans para k ∈ {2..10} via Elbow (WSS) com KElbowVisualizer | Métricas de avaliação, com pipe pronto, posso fazer múltiplas iterações para testes | Pipe organizado. | sim |  |  |
| 3  | 2     | Montar pipeline para testes KMeans para k ∈ {2..10} via Silhouette Score com KElbowVisualizer | Métricas de avaliação, com pipe pronto, posso fazer múltiplas iterações para testes | Pipe organizado. | sim |  |  |
| 4  | 1     | Exportar X para data/interim/7.data-k-definition.pkl | Garantir continuidade dos dados | novo arquivo de dados em pkl | sim |  |  |
| 5  | 3     | Plotar SilhouetteVisualizer em painel 5×2 para cada k | Verificar a variabilidades dos múltiplos cluster afim de encontrar bons padrões e chancelar as métricas anteriores | Visualização dos clusters mais claras e divididas além das métricas simples | sim |  |  |

---

## `8.0.model_training`

| id | ciclo | ação | decisão | resultado | ativo | ciclo_fim | motivo |
| -- | ----- | ---- | ------- | --------- | ----- | --------- | ------ |
| 1  | 1     | Treinar KMeans com o K definido no notebook 7.0 | Treinamento padrão.  | Modelo treinado | sim |  |  |
| 2  | 1     | Calcular WSS (inertia_) do modelo final | Métrica avaliatória |  | sim |  |  |
| 3  | 1     | Calcular Silhouette Score (métrica euclidiana) do modelo final | métrica avaliatória |  | sim |  |  |
| 4  | 1     | Adicionar coluna `clusters` ao dataframe de features (df_cluster) | Serve para montar as análises dos clusters no notebook 9.0 | df pronto para exportar e realizar análise | sim |  |  |
| 5  | 1     | Exportar df_cluster para data/processed/8.data_model_training.pkl | Gerar df para análise dos cluster notebook 9.0 | novo df em pkl | sim |  |  |
| 6  | 1     | Exportar modelo KMeans para models/8.model_training.pkl | Garantir a utilização do mesmo modelo caso seja necessário e garantir modelo para período de produção, caso seja necessário | modelo pronto | sim |  |  |

---

## `9.0.cluter_analysis`

| id | ciclo | ação | decisão | resultado | ativo | ciclo_fim | motivo |
| -- | ----- | ---- | ------- | --------- | ----- | --------- | ------ |
| 1  | 1     | Plotar SilhouetteVisualizer do modelo final | Avaliação da qualidade dos clusters | RFM ainda não está legal, precisa de mais features. |  |  |  |
| 2  | 1     | Preparar scatter 3D (recencia × invoice_no × faturamento) — comentado | Verificar separação de cluster RFM | Cluster ainda muito compacto, precisa de mais features de separação. | sim |  |  |
| 3  | 1     | Calcular simples cluster profile | Verificar a cada ciclo como esse profile se comporta | DF simples com os valores de cada cluster | sim |  |  |
| 4  | 2     | Plotar pairplot 2D das features colorido por cluster | Observar as relação 2 a 2 das variáveis | Ainda estão com clusters muito agrupados, continuar testando nas próximas iterações | sim |  |  |
| 5  | 2     | Aplicar UMAP e plotar embedding 2D colorido por cluster | Verificar a distribuição topológica em 2d | péssima visualização, trabalhar melhor as features e talvez implantar o 3d | sim |  |  |
| 6  | 3     | Aplicar UMAP e plotar embedding 3D colorido por cluster | Muita perca de informaçãono gráfico 2d | Clusters muito compactos, tem que ser trabalhado melhor as features | sim |  |  |

---

## `10.0.negocio`

| id | ciclo | ação | decisão | resultado | ativo | ciclo_fim | motivo |
| -- | ----- | ---- | ------- | --------- | ----- | --------- | ------ |
|    |       |      |         |           |       |        |        |

---

## `11.0.deploy`

| id | ciclo | ação | decisão | resultado | ativo | ciclo_fim | motivo |
| -- | ----- | ---- | ------- | --------- | ----- | --------- | ------ |
|    |       |      |         |           |       |        |        |
