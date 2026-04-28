# Fidelidade — Clusterização de Clientes

## 0.0 Orientações

**Objetivo:** [INSERIR — uma frase descrevendo o problema que o projeto resolve]

| Recurso | Link |
| --- | --- |
| Base de dados | [INSERIR LINK DA BASE DE DADOS] |
| Notebook principal | [INSERIR LINK DO NOTEBOOK] |
| Aplicação / API / Dashboard | [INSERIR LINK, se existir] |
| Artigo ou post | [INSERIR LINK, se existir] |

> Status do projeto: [Em desenvolvimento]

---

## 1.0 Problema de Negócio

### Contexto

[INSERIR — quem é a empresa, área ou pessoa interessada na solução]

### Dor

[INSERIR — qual situação gerou a necessidade do projeto e o que acontece se o problema não for resolvido]

### Objetivo

[INSERIR — o que precisa ser entregue e quem vai usar a solução]

---

## 2.0 Premissas de Negócio

[INSERIR — lista numerada das regras, hipóteses e limites adotados no projeto]

### 2.1 Perguntas de Negócio

1. [INSERIR pergunta 1]
2. [INSERIR pergunta 2]
3. [INSERIR pergunta 3]

### 2.2 Descrição dos Dados

| Atributo | Tradução | Descrição |
| --- | --- | --- |
| [INSERIR coluna] | [INSERIR nome amigável] | [INSERIR o que representa] |

### 2.3 Acesso aos Dados

[INSERIR — origem dos dados: Kaggle, banco de dados, API, CSV, web scraping etc.]

---

## 3.0 Estratégia da Solução

### 3.1 Metodologia

O projeto seguiu as etapas do CRISP-DM:

1. Entendimento do negócio
2. Coleta de dados
3. Limpeza dos dados
4. Feature engineering
5. Análise exploratória
6. Preparação dos dados
7. Modelagem
8. Avaliação
9. [INSERIR — deploy ou entrega final]

### 3.2 Produto Final

[INSERIR — o que foi entregue: notebook analítico, modelo treinado, API, dashboard, planilha etc.]

### 3.3 Ferramentas Utilizadas

| Categoria | Ferramenta |
| --- | --- |
| Linguagem | Python 3.11.9 |
| Análise de dados | pandas, numpy |
| Modelagem | scikit-learn |
| Visualização | matplotlib [INSERIR outras, se houver] |
| Ambiente | Docker, Jupyter Notebook |
| Versionamento | Git |

### 3.4 Estrutura do Projeto

```text
├── LICENSE                  <- Licença de uso do projeto
├── Makefile                 <- Comandos de automação (ex.: make data, make train)
├── README.md                <- Documentação principal do projeto
├── requirements.txt         <- Dependências Python para reproduzir o ambiente
├── .env                     <- Variáveis de ambiente (não versionar credenciais)
├── .gitignore               <- Arquivos e pastas ignorados pelo Git
├── Dockerfile               <- Define como construir a imagem Docker
├── docker-compose.yml       <- Orquestra o container (portas, volumes, nome do serviço)
│
├── data/
│   ├── raw/                 <- Dados originais e imutáveis (nunca alterar)
│   ├── external/            <- Dados provenientes de fontes externas ou terceiros
│   ├── interim/             <- Dados intermediários após transformações parciais
│   └── processed/           <- Dados finais prontos para modelagem
│
├── docs/                    <- Documentação técnica do projeto
│
├── models/                  <- Modelos treinados, serializados e resumos de performance
│
├── notebooks/               <- Notebooks Jupyter
│                               Convenção de nome: número (ordenação) + iniciais do autor
│                               + descrição curta separada por hífen.
│                               Ex.: 1.0-gnl-exploracao-inicial.ipynb
│
├── references/              <- Dicionários de dados, manuais e materiais de referência
│   └── git_references.md   <- Padrão de commits (Conventional Commits) e Git Flow do projeto
│
├── reports/                 <- Análises geradas em HTML, PDF, LaTeX etc.
│   └── figures/             <- Gráficos e imagens para uso nos relatórios e no README
│
└── src/                     <- Código-fonte reutilizável do projeto
    ├── __init__.py          <- Torna src um módulo Python importável
    ├── data/
    │   └── make_dataset.py  <- Scripts para baixar, extrair ou gerar os dados
    ├── features/
    │   └── build_features.py <- Scripts para transformar dados brutos em features de modelagem
    ├── models/
    │   ├── train_model.py   <- Scripts para treinar e serializar modelos
    │   └── predict_model.py <- Scripts para aplicar modelos treinados e gerar predições
    └── visualization/
        └── visualize.py     <- Scripts para criar visualizações exploratórias e de resultado
```

> Os commits seguem o padrão **[Conventional Commits](https://www.conventionalcommits.org)** com extensões documentadas em [references/git_references.md](references/git_references.md).

---

## 4.0 Análise dos Dados

- **Dimensão da base:** [INSERIR — número de linhas e colunas]
- **Período coberto:** [INSERIR, se aplicável]
- **Dados nulos:** [INSERIR — quais colunas e proporção]
- **Dados duplicados:** [INSERIR]

### 4.1 Insights de Negócio

| Hipótese | Resultado | Relevância | Comentário |
| --- | --- | --- | --- |
| [INSERIR hipótese] | Verdadeira / Falsa / Inconclusiva | Alta / Média / Baixa | [INSERIR interpretação] |

[INSERIR IMAGEM — gráfico ou visualização principal da EDA]

---

## 5.0 Modelos de Machine Learning Utilizados

**Tipo de problema:** Clusterização

**Baseline:** [INSERIR — ex.: K-Means com k=2, segmentação manual existente etc.]

**Algoritmos testados:**

- [INSERIR modelo 1]
- [INSERIR modelo 2]
- [INSERIR modelo 3]

**Métrica de avaliação:** [INSERIR — ex.: Silhouette Score, Davies-Bouldin, Within-Cluster SSE]

[INSERIR — justificativa de por que esses algoritmos fazem sentido para o problema]

---

## 6.0 Seleção do Modelo de Machine Learning

### 6.1 Seleção de Atributos

[INSERIR — quais variáveis entraram no modelo e por quê]

### 6.2 Métricas dos Algoritmos

| Modelo | [Métrica 1] | [Métrica 2] | [Métrica 3] |
| --- | --- | --- | --- |
| Baseline | [INSERIR] | [INSERIR] | [INSERIR] |
| [Modelo A] | [INSERIR] | [INSERIR] | [INSERIR] |
| [Modelo B] | [INSERIR] | [INSERIR] | [INSERIR] |

### 6.3 Fine Tuning

[INSERIR — parâmetros testados e melhores resultados, ou indicar que não foi realizado]

### 6.4 Modelo Final

[INSERIR — modelo escolhido e justificativa técnica e de negócio]

---

## 7.0 Resultado de Negócio

### 7.1 Performance do Modelo Final

[INSERIR — métricas finais em linguagem objetiva]

### 7.2 Performance Visual ou Estratificada

[INSERIR IMAGEM — gráfico de clusters, distribuição por grupo, silhouette plot etc.]

### 7.3 Cenário Principal

[INSERIR — resposta à pergunta principal do negócio com números]

### 7.4 Tradução Financeira

[INSERIR — valor monetário, redução de custo, aumento de conversão ou marcar como N/A]

### 7.5 Cenários Operacionais

[INSERIR — simulações alternativas, se houver]

### 7.6 Threshold ou Regra de Decisão

[INSERIR — como o time de negócio deve usar os clusters na prática]

---

## 8.0 Aplicação em Produção

[INSERIR — link de produção, ou explicar como rodar localmente]

**Como executar localmente:**

```bash
# 1. Subir o container Docker
docker compose up -d

# 2. Entrar no container
docker compose exec clusterizacao bash

# 3. Iniciar o Jupyter Notebook
jupyter notebook --ip=0.0.0.0 --port=8888 --no-browser --allow-root
```

Abra o link `http://127.0.0.1:8888/tree?token=...` que aparecer no terminal.

**Exemplo de uso da solução** *(se houver API ou script de predição)*:

```python
# [INSERIR — exemplo de requisição ou chamada ao modelo]
```

---

## 9.0 Conclusão

[INSERIR — o objetivo do projeto foi atingido? Qual foi o principal resultado? Como a solução ajuda o negócio?]

**Estado atual:** [INSERIR — protótipo / análise concluída / em produção]

**Limitações:** [INSERIR, se houver]

---

## 10.0 Próximos Passos de Melhoria

- [ ] [INSERIR melhoria de dados]
- [ ] [INSERIR melhoria de modelagem]
- [ ] [INSERIR melhoria de produto ou deploy]
- [ ] [INSERIR monitoramento ou automação]

---

## 11.0 Aprendizados do Projeto

- **Negócio:** [INSERIR]
- **Dados:** [INSERIR]
- **Modelagem:** [INSERIR]
- **Deploy:** [INSERIR]

[INSERIR LINK — artigo ou post, se houver]

---

## 12.0 Contatos

<ul class="actions">
    <table>
        <tr>
            <th><a href="[INSERIR LINK DO PORTFÓLIO]"> Portfólio de Projetos</a></th>
            <th><a href="[INSERIR LINKEDIN]"> Linkedin</a></th>
            <th><a href="[INSERIR MEDIUM OU BLOG]"> Medium</a></th>
            <th><a href="[INSERIR GITHUB]"> GitHub</a></th>
            <th><a href="mailto:gabrielnobregalvao@gmail.com"> E-mail</a></th>
        </tr>
    </table>
</ul>
