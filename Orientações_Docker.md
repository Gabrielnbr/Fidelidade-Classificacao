# Guia Docker — Projeto Fidelidade Clusterização

## O que é Docker?

Docker permite criar um ambiente isolado (chamado **container**) com tudo que o projeto precisa: Python, bibliotecas, configurações. É como uma "caixinha" que roda igual em qualquer máquina, sem precisar instalar nada diretamente no seu computador.

**Conceitos essenciais:**
- **Imagem**: receita de bolo (o `Dockerfile` define como construí-la)
- **Container**: o bolo pronto e rodando (instância da imagem)
- **Volume**: ponte entre sua pasta local e o container — edite arquivos no VS Code e as mudanças aparecem dentro do container em tempo real

---

## Pré-requisitos

Instale o [Docker Desktop](https://www.docker.com/products/docker-desktop/) e abra-o antes de usar qualquer comando abaixo.

---

## Fluxo de trabalho diário

### 1. Primeira vez (ou após mudar o Dockerfile/requirements.txt)

```bash
docker compose up --build -d
```

| Parte | O que faz |
| --- | --- |
| `docker compose up` | Cria e inicia o container definido no `docker-compose.yml` |
| `--build` | Reconstrói a imagem antes de subir (necessário quando o `Dockerfile` ou `requirements.txt` muda) |
| `-d` | Modo *detached* — sobe o container em segundo plano, liberando o terminal |

---

### 2. Dias seguintes (imagem já construída)

```bash
docker compose up -d
```

| Parte | O que faz |
| --- | --- |
| `docker compose up` | Inicia o container |
| `-d` | Modo *detached* — roda em segundo plano, sem prender o terminal |

---

### 3. Entrar no terminal do container

```bash
docker compose exec clusterizacao bash
```

| Parte | O que faz |
| --- | --- |
| `docker compose exec` | Executa um comando dentro de um container que já está rodando |
| `clusterizacao` | Nome do serviço definido no `docker-compose.yml` |
| `bash` | Abre um terminal Bash interativo dentro do container |

Você estará dentro do container, na pasta `/app`, com Python 3.11.9 disponível.

---

### 4. Parar o container

```bash
docker compose down
```

| Parte | O que faz |
| --- | --- |
| `docker compose down` | Para e remove o container (a imagem continua salva; os arquivos da pasta local não são apagados) |

---

## Instalar novas bibliotecas

### Forma correta (permanente)

1. Adicione a biblioteca no arquivo `requirements.txt`:
   ```
   plotly
   ```
2. Reconstrua a imagem:
   ```bash
   docker compose up --build -d
   ```
   *(mesma lógica do passo 1 do fluxo diário — ver tabela acima)*

### Forma rápida (temporária — some quando o container reiniciar)

Entre no container e instale com pip:

```bash
docker compose exec clusterizacao bash
pip install plotly
```

| Comando | O que faz |
| --- | --- |
| `docker compose exec clusterizacao bash` | Abre o terminal do container (ver tabela acima) |
| `pip install plotly` | Instala a biblioteca `plotly` apenas dentro do container em execução, sem alterar a imagem |

> Use a forma temporária para testar. Quando confirmar que precisa da biblioteca, adicione ao `requirements.txt`.

---

## Rodar scripts Python

Dentro do container (após `docker compose exec clusterizacao bash`):

```bash
python meu_script.py
```

| Parte | O que faz |
| --- | --- |
| `python` | Chama o interpretador Python 3.11.9 instalado no container |
| `meu_script.py` | Nome do script a executar (deve estar na pasta `/app`, espelhada da sua pasta local) |

Ou diretamente, sem entrar no container:

```bash
docker compose exec clusterizacao python meu_script.py
```

| Parte | O que faz |
| --- | --- |
| `docker compose exec clusterizacao` | Executa um comando no serviço `clusterizacao` em execução |
| `python meu_script.py` | Roda o script diretamente, sem abrir um terminal interativo |

---

## Rodar Jupyter Notebook

Dentro do container:

```bash
jupyter notebook --ip=0.0.0.0 --port=8888 --no-browser --allow-root
```

| Parte | O que faz |
| --- | --- |
| `jupyter notebook` | Inicia o servidor Jupyter Notebook |
| `--ip=0.0.0.0` | Aceita conexões de qualquer endereço de rede (necessário para acessar de fora do container) |
| `--port=8888` | Define a porta em que o servidor vai escutar (mapeada para o host no `docker-compose.yml`) |
| `--no-browser` | Não tenta abrir o navegador automaticamente (o container não tem interface gráfica) |
| `--allow-root` | Permite rodar como usuário root dentro do container (comportamento padrão em containers Docker) |

Copie o link `http://127.0.0.1:8888/tree?token=...` que aparecer no terminal e abra no navegador.

O volume está configurado, então os notebooks salvos aparecem na sua pasta local.

---

## Verificar bibliotecas instaladas

Dentro do container:

```bash
pip list
```

| Parte | O que faz |
| --- | --- |
| `pip list` | Exibe todas as bibliotecas Python instaladas no ambiente atual do container e suas versões |

---

## Comandos úteis de diagnóstico

| Comando | O que faz |
| --- | --- |
| `docker ps` | Lista apenas os containers que estão rodando no momento |
| `docker ps -a` | Lista todos os containers (incluindo os que estão parados) |
| `docker images` | Lista todas as imagens Docker disponíveis na máquina |
| `docker compose logs` | Exibe os logs de saída do container (útil para depurar erros de inicialização) |
| `docker system prune` | Remove imagens, containers parados e caches não utilizados para liberar espaço em disco |

---

## Resolução de problemas comuns

### "No such service" ou "container not running" ao usar `exec`

O `exec` só funciona com o container **já rodando**. A ordem correta é:

```bash
# 1. Primeiro, sobe o container
docker compose up -d

# 2. Só depois entra nele
docker compose exec clusterizacao bash
```

Para confirmar que o container está rodando antes de executar o `exec`:

```bash
docker ps
```

Se o container `fidelidade_clusterizacao` aparecer na lista, está rodando. Se não aparecer, rode `docker compose up -d` primeiro.

---

### "jupyter-notebook: command not found"

Significa que o `jupyter` não está instalado na imagem. Solução:

1. Certifique-se que `requirements.txt` contém a linha `jupyter`
2. Reconstrua a imagem (obrigatório após mudar `requirements.txt`):

   ```bash
   docker compose up --build -d
   ```

3. Entre no container e verifique:

   ```bash
   docker compose exec clusterizacao bash
   jupyter --version
   ```

---

### Notebook `.ipynb` aberto no VS Code não roda

O VS Code abre o arquivo, mas o **kernel** (o Python que executa as células) precisa estar conectado. Existem duas formas:

**Forma A — Rodar via navegador (recomendada para iniciantes):**

1. Suba o container: `docker compose up -d`
2. Entre no container: `docker compose exec clusterizacao bash`
3. Inicie o Jupyter: `jupyter notebook --ip=0.0.0.0 --port=8888 --no-browser --allow-root`
4. Copie o link `http://127.0.0.1:8888/tree?token=...` que aparece no terminal
5. Abra esse link no navegador — lá você navega e executa os notebooks normalmente

**Forma B — Conectar o VS Code ao Jupyter do container:**

1. Suba o container e inicie o Jupyter (passos 1–3 acima)
2. No VS Code, abra o `.ipynb`
3. No canto superior direito clique em **"Select Kernel"** → **"Existing Jupyter Server"**
4. Cole a URL com o token: `http://127.0.0.1:8888/?token=SEU_TOKEN`
5. Selecione o kernel Python — agora as células rodam dentro do container

---

## Estrutura dos arquivos Docker neste projeto

```
projeto/
├── Dockerfile           # Define como construir a imagem (Python 3.11.9 + dependências do sistema)
├── docker-compose.yml   # Orquestra o container (portas, volumes, nome)
├── requirements.txt     # Bibliotecas Python a instalar
└── .dockerignore        # Arquivos ignorados ao copiar para a imagem
```

---

## Fluxo resumido

```
Edite código no VS Code  →  mudanças aparecem no container via volume
Precisa de nova lib      →  adicione no requirements.txt e rode --build
Terminou o dia           →  docker compose down
Voltou no dia seguinte   →  docker compose up -d
```
