# Workflows
Um workflow é um conjunto de instruções que diz ao GitHub Actions o que fazer e quando fazer. São fluxos de trabalho automatizados.

Ele é descrito em um arquivo YAML, que fica guardado dentro da pasta:

.github/workflows/

Um workflow é gatilhado (ativado) por eventos como:

-- push → quando você envia código para o repositório

-- pull_request → quando alguém faz um pedido de revisão de código

-- schedule → em horários programados (tipo cron jobs)

-- workflow_dispatch → quando é iniciado manualmente


# Criando workflows:

Para criar nosso primeiro workflow, vamos seguir este passo a passo:

# Passo 1: Ambiente de desenvolvimento do projeto:

Abra o ambiente de desenvolvimento, no caso, o vscode na pasta do projeto onde você já criou a estrutura do .github/workflows


# Passo 2: Criar um arquivo yaml dentro da pasta workflows.
Este arquivo é típico de workflow (ci.yml, por exemplo) e possui a seguinte estrutura:

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

## Explicando cada parte do projeto:

-- name: Nome visível do workflow. Aparecerá na aba “Actions”.

-- on: push Gatilho — quando você fizer um git push, o workflow será executado.

-- jobs: Agrupa um ou mais “trabalhos” (jobs) dentro do workflow.

-- runs-on: Define o sistema operacional (máquina virtual) usado.

-- steps: Lista as etapas (passos) que serão executadas.

-- run:	Executa um comando direto no terminal.

# Acessando e configurando o Git
Passo 1:  Certifique-se de que o Git está instalado no seu sistema:
git --version

Passo 2: Configurar o Nome de Usuário Global
Neste caso, o nome que será anexado sempre que o commit for realizado.
git config --global user.name "Seu Nome Completo"

Passo 3: Configurar o E-mail Global
Este e-mail será anexado a todos os seus commits. Use o mesmo e-mail associado à sua conta do GitHub para que seus commits sejam vinculados corretamente ao seu perfil online.

git config --global user.email "seu.email@exemplo.com"
 
Passo 4: Configurações Opcionais (e Altamente Recomendadas)

A. Historicamente, o nome padrão era master. A comunidade padronizou para main. Isso garante consistência com o GitHub (que usa main por padrão).

git config --global init.defaultBranch main 

B. Ativar o Colorir no Terminal (Opcional, para melhor leitura)

git config --global color.ui auto

Passo 5: Verificar as Configurações
Para garantir que tudo foi configurado corretamente, você pode visualizar o arquivo de configuração global.
git config --list --global

# Conectar o Git ao GitHub:

Após a configuração inicial, você estará pronto para usar o Git para interagir com o GitHub. O próximo passo é Clonar um Repositório ou Inicializar um Repositório Local.

Como já criamos e configuramos nosso repositório local, então vamos seguir para inicializar o git:
git init

# Adicione o Conteúdo do Projeto:
Já criamos nossa estrutura e temos arquivos dentro da pasta, então vamos enviar.
No terminal:

