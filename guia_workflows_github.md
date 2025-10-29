# Workflows

Um **workflow** é um conjunto de instruções que diz ao **GitHub Actions** o que fazer e quando fazer. São fluxos de trabalho automatizados.

Ele é descrito em um arquivo **YAML**, que fica guardado dentro da pasta:

```
.github/workflows/
```

Um workflow é **gatilhado (ativado)** por eventos como:

- **push** → quando você envia código para o repositório  
- **pull_request** → quando alguém faz um pedido de revisão de código  
- **schedule** → em horários programados (tipo cron jobs)  
- **workflow_dispatch** → quando é iniciado manualmente  

---

## Criando Workflows

Para criar nosso primeiro workflow, vamos seguir este passo a passo:

### Passo 1: Ambiente de desenvolvimento do projeto

Abra o ambiente de desenvolvimento, no caso, o **VS Code**, na pasta do projeto onde você já criou a estrutura do `.github/workflows`.

### Passo 2: Criar um arquivo YAML dentro da pasta workflows

Este arquivo é típico de workflow (por exemplo, `ci.yml`) e possui a seguinte estrutura:

```yaml
name: Testar e construir o projeto

on: 
  push:        # Quando alguém fizer um push no repositório
    branches:
      - main   # Apenas quando for na branch 'main'

jobs:
  build:       # Nome do trabalho (job)
    runs-on: ubuntu-latest  # Sistema operacional onde será executado

    steps:     # Etapas do job
      - name: Clonar o repositório
        uses: actions/checkout@v4

      - name: Configurar Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Instalar dependências
        run: npm install

      - name: Executar testes
        run: npm test
```

### Explicando cada parte do projeto

- **name:** Nome visível do workflow (aparecerá na aba “Actions”).  
- **on: push:** Gatilho — quando você fizer um git push, o workflow será executado.  
- **jobs:** Agrupa um ou mais “trabalhos” (jobs) dentro do workflow.  
- **runs-on:** Define o sistema operacional (máquina virtual) usado.  
- **steps:** Lista as etapas (passos) que serão executadas.  
- **run:** Executa um comando direto no terminal.  

---

## Acessando e Configurando o Git

### Passo 1: Verificar instalação do Git

```bash
git --version
```

### Passo 2: Configurar o Nome de Usuário Global

O nome que será anexado sempre que um commit for realizado:

```bash
git config --global user.name "Seu Nome Completo"
```

### Passo 3: Configurar o E-mail Global

Use o mesmo e-mail associado à sua conta do GitHub para que seus commits sejam vinculados corretamente:

```bash
git config --global user.email "seu.email@exemplo.com"
```

### Passo 4: Configurações opcionais (e altamente recomendadas)

#### A. Definir o nome padrão da branch principal

Por padrão, use `main` (em vez de `master`):

```bash
git config --global init.defaultBranch main
```

#### B. Ativar cores no terminal (para melhor leitura)

```bash
git config --global color.ui auto
```

### Passo 5: Verificar as Configurações

Para garantir que tudo foi configurado corretamente:

```bash
git config --list --global
```

---

## Conectar o Git ao GitHub

Após a configuração inicial, você estará pronto para usar o Git para interagir com o GitHub.

### Inicializar um repositório local

```bash
git init
```

### Adicionar o conteúdo do projeto

Como já criamos a estrutura e temos arquivos dentro da pasta, vamos enviar tudo:

```bash
git add .
git commit -m "Primeiro commit"
git branch -M main
git remote add origin https://github.com/usuario/repositorio.git
git push -u origin main
```
