# High Value Customer Identification

## 0.0 Planejamento da Solução

### Input - Entrada

1. Problema de negócio.
   1. Selecionar os clientes mais valiosos para integras um programa de fidelização.
2. Conjunto de dados
   1. Venda de um e-commerce online, durante o período de um ano.

### Output - Saída

1. A indicação das pessoas que farão parte do programa de Insiders. Lista de clientes.

| cliente_id | is_insider |
| ---------- | ---------- |
| a3d4fg5    | 1 |
| 3djgh9m    | 0 |

2. Relatório com as respostas das perguntas de negócio.
   1. Quem são as pessoas elegíveis para participar do programa de Insiders?
   2. Quantos clientes farão parte do grupo?
   3. Quais as principais características desses clientes?
   4. Qual a porcentagem de contribuição do faturamento, vinda do Insiders?
   5. Qual a expectativa de faturamento desse grupo para os próximos meses?
   6. Quais as condições para uma pessoa ser elegível ao Insiders?
   7. Quais as condições para uma pessoa ser removida do Insiders?
   8. Qual a garantia que o programa Insiders é melhor que o restante da base?
   9. Quais ações o time de marketing pode realizar para aumentar o faturamento?

### Tasks - Tarefas

1. Quem são as pessoas elegíveis para participar do programa de Insiders?
   1. O que é ser elegível?
   2. O que são clientes de maior "valor"?
      1. Faturamento:
         1. Alto ticket médio.
         2. Alto LTV.
         3. Baixa Recência.
         4. Alto basket size.
         5. Baixa probabilidade de Churn. (Modelo Classificação)
         6. Alta Previsão de LTV (Modelo Classificação)
         7. Alta propensão de compra (Modelo Classificação)
      2. Custo:
         1. Baixa taxa de devolução.
      3. Experiência de compra:
         1. Média alta das avaliações.
2. Quantos clientes farão parte do grupo?
   1. Número total de clientes.
   2. % do grupo Insiders
3. Quais as principais características desses clientes?
   1. Características gerais:
      1. Idade
      2. Localização
   2. Características consumo:
      1. Atributos de clusterização.
4. Qual a porcentagem de contribuição do faturamento, vinda do Insiders?
   1. Faturamento total do ano.
   2. Faturamento do grupo Insiders.
5. Qual a expectativa de faturamento desse grupo para os próximos meses?
   1. LTV do grupo insiders (Pode ser feito simulação ARIMA)
   2. Análise de Cohort.
6. Quais as condições para uma pessoa ser elegível ao Insiders?
   1. Definir a periodicidade (15 dias, 1 mês, 3 meses)
   2. A pessoa precisa ser similar ou parecido com o grupo.
7. Quais as condições para uma pessoa ser removida do Insiders?
   1. Definir a periodicidade (15 dias, 1 mês, 3 meses)
   2. A pessoa precisa ser não similar ou não parecido com o grupo.
8. Qual a garantia que o programa Insiders é melhor que o restante da base?
   1. Teste A/B.
   2. Teste A/B Bayesiano.
   3. Teste de Hipótese.
9. Quais ações o time de marketing pode realizar para aumentar o faturamento?
   1. Desconto.
   2. Preferência de Compra.
   3. Frete.

## 1.0 Beanckmark de Soluções

### 1.0 Desk Research
Iniciar com Modelo RFM: Recência, Frequência e Monetário.