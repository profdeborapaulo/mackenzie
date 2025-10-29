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

# Verifique o Status dos Arquivos:
Use este comando para ver quais arquivos foram alterados ou ainda não foram rastreados pelo Git.

git status

O resultado esperado: os arquivos aparecerão em vermelho (arquivos não rastreados).

# Adicione os Arquivos para Staging:

Use o comando add para incluir os arquivos alterados (rastreados ou não rastreados) na área de preparação (staging area), que é o que será incluído no próximo commit

No terminal:

git add .

Nota: O ponto (.) adiciona todos os arquivos novos e alterados no diretório atual. Se quiser adicionar um arquivo específico, use git add nome_do_arquivo.

# Verifique o Status Novamente:
Os arquivos agora devem aparecer em verde (prontos para o commit).
Bash
git status

# Crie o Primeiro Commit (Salvar Versão Local):
O commit salva o estado atual do seu projeto no histórico do Git. A flag -m é para adicionar uma mensagem que descreve a mudança.

git commit -m "Commit inicial do projeto de pipeline de dados"

# Vamos conectar ao GitHub
🚀 Passo 1 — Verifique se já há um repositório remoto configurado
Obs. Já tenho um repositório no GitHub que vou usar, então, vou digitar o commando:

git remote -v

Se não aparecer nada, significa que o repositório local ainda não está vinculado a nenhum remoto.

Se aparecer algo como origin https://github.com/seuusuario/algumrepo.git, e não for o “escola”, podemos trocar.

No nosso projeto, sabemos que ainda não foi conectado, então não vai aparecer nada.

⚙️ Passo 2 — Adicionar (ou atualizar) o repositório remoto

git remote add origin https://github.com/SEU_USUARIO/escola.git

👉 Substitua SEU_USUARIO pelo nome do seu perfil do GitHub.

git remote add origin https://github.com/profdeborapaulo/mackenzie.git

Caso já exista um remoto incorreto e queira substituí-lo:

git remote set-url origin https://github.com/SEU_USUARIO/escola.git

🧱 Passo 3 — (Opcional, mas recomendável) Criar um branch principal

Alguns repositórios mais novos no GitHub usam main como branch principal (não mais master).

git branch

Se aparecer * master, você pode renomear:

git branch -M main

☁️ Passo 4 — Enviar os arquivos para o GitHub

Agora sim, envie seu commit local para o repositório remoto:

git push -u origin main

O -u cria o link entre o branch local e remoto, para que no futuro você possa apenas digitar git push sem repetir tudo.

Se aparecer um erro do tipo: ! [rejected] main -> main (fetch first)

significa:

“O GitHub já tem commits que não existem no seu computador.
Antes de enviar seus arquivos (push), você precisa trazer o que está lá (pull) para sincronizar.”

✅ Existem duas maneiras de resolver 
🔹 Opção 1 — (Segura) Trazer o que está no GitHub antes de enviar

1️⃣ Puxe o conteúdo remoto (sem sobrescrever):
git pull origin main --allow-unrelated-histories

O --allow-unrelated-histories é necessário porque o seu repositório local e o remoto foram criados de forma independente (cada um com seu histórico de commits).

2️⃣ O Git pode abrir o editor de merge (geralmente o Vim) pedindo uma mensagem de merge commit.
Basta digitar :wq e Enter para salvar e sair, ou se estiver no VSCode ele fará isso automaticamente.

3️⃣ Depois, envie tudo normalmente:

git push -u origin main
Pronto ✅
Agora o GitHub vai receber seus arquivos e os históricos estarão unificados.

🔹 Opção 2 — (Mais rápida, mas apaga o que estava no GitHub)

⚠️ Use somente se o que estava no repositório remoto não importa (por exemplo, um README vazio criado pelo GitHub).

1️⃣ Force o envio do seu repositório local sobrescrevendo o remoto:

git push -u origin main --force

Isso vai substituir o conteúdo remoto pelo seu conteúdo local.
Tudo o que estava no GitHub será apagado.

Eu segui para a opção 1:

Agora sim, vamos conferir o estado do seu repositório e seguir para ativar o GitHub Actions passo a passo.

🧭 Etapa 1 — Conferir o status atual

Digite no terminal:

git status


Você pode ver algo como:

On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean


✅ Isso significa que:

Seu repositório local está sincronizado com o remoto;

Todos os commits foram enviados;

Está tudo pronto para criar e testar a pipeline CI/CD com GitHub Actions.

Se aparecer algo como “changes not staged for commit” ou “untracked files”, você pode simplesmente adicionar e commitar de novo:

git add .
git commit -m "Ajustes após sincronização"
git push

🧩 Etapa 2 — Garantir que a estrutura do GitHub Actions está correta

Verifique se a pasta .github/workflows está na raiz do repositório.
A estrutura deve estar assim:

📂 mackenzie/
 ┣ 📂 .github/
 ┃ ┗ 📂 workflows/
 ┃   ┗ 📄 main.yml
 ┣ 📄 README.md

👉 Se o .github estiver dentro de outra pasta (como githubActions/.github/workflows), o GitHub não reconhece o workflow.

No nosso caso está assim, então vamos precisar mover:
mv githubActions/.github ./
rm -rf githubActions
git add .
git commit -m "Movendo workflows para a raiz"
git push

⚙️ Etapa 3 — Criar (ou confirmar) o arquivo de workflow

Agora, dentro de .github/workflows, crie um arquivo chamado main.yml (ou outro nome, mas com .yml).

Cole este conteúdo de exemplo inicial:
name: Teste CI/CD

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Baixar o repositório
        uses: actions/checkout@v3

      - name: Verificar versão do Node
        run: node -v

      - name: Exibir mensagem de sucesso
        run: echo "🎉 Pipeline GitHub Actions funcionando com sucesso!"

🚀 Etapa 4 — Fazer commit e push do workflow

Salve o arquivo e no terminal:

git add .
git commit -m "Adiciona workflow de teste CI/CD"
git push

🧠 Etapa 5 — Verificar no GitHub se a pipeline rodou

1️⃣ Vá até seu repositório no GitHub (mackenzie).
2️⃣ Clique na aba “Actions” (na barra superior).
3️⃣ Você verá algo como:
“Workflow: Teste CI/CD — running...”
ou um ✅ verde indicando sucesso.
🧩 O que esse workflow faz

on.push.branches: [main] → dispara sempre que há um push na branch main.

runs-on: ubuntu-latest → executa em uma máquina Linux virtual.

actions/checkout@v3 → baixa seu código no ambiente do Actions.

run: node -v → roda um comando Node (só para teste).

echo "🎉 ..." → imprime uma mensagem no log.

🧰 Etapa 6 — (Opcional) Criar um teste real de build

Depois que esse teste simples funcionar, você pode expandir para algo como:

Rodar scripts de teste (npm test);

Fazer build de um projeto Node ou front-end;

Implantar (deploy) automaticamente.