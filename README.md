# 🛡️ Laboratório Prático: Automação de Backup em Nuvem com BASH

Bem-vindos ao laboratório de **Gerenciamento de Arquivos e Nuvem**! ☁️📂

Nesta prática, vamos sair da teoria e criar uma solução real de **backup automatizado e versionado**. Vocês vão provar na prática que sincronização (como o Google Drive para Desktop) não é a mesma coisa que backup seguro, e aprenderão a usar o terminal (CLI) para proteger seus dados contra perdas acidentais ou malwares.

---

## 🎯 Objetivo da Aula
Criar um script em Shell Script (`.sh`) que:
1. Navegue por diretórios do Windows usando o Git Bash.
2. Compacte uma pasta inteira no formato `.zip`.
3. Adicione a data do dia no nome do arquivo (versionamento).
4. Salve o arquivo final na pasta de sincronização da nuvem.

---

## ⚙️ Pré-requisitos
* Sistema Operacional Windows.
* **Git Bash** instalado.
* Terminal aberto.

---

## 🚀 Passo a Passo

### 1. Preparando o Ambiente de Teste
Abra o seu terminal (Git Bash) e execute os comandos abaixo. Vamos criar nossas pastas diretamente na raiz do disco `C:` para facilitar a visualização no Windows Explorer.

```bash
# Criando a pasta de trabalho (origem) e a pasta da "nuvem" (destino)
mkdir -p ~/Projetos_Aula
mkdir -p ~/Nuvem_Drive

# Criando arquivos simulados de teste
echo "<h1>Meu site incrivel</h1>" > /c/Projetos_Aula/index.html
echo "body { background: blue; }" > /c/Projetos_Aula/style.css

```

> **Dica:** Abra o "Meu Computador > Disco Local (C:)" e verifique se as pastas foram criadas corretamente!

### 2. O Script de Backup (`rotina_backup.sh`)

Utilize um editor de código (como o VS Code) ou o editor nativo do terminal (como o `nano`) para criar o arquivo do nosso script. Salve-o na raiz do seu usuário ou dentro de uma pasta de scripts.

**Código do Script:**

```bash
#!/bin/bash
# Sistema de Backup em Nuvem (Gerando .zip)

echo "=========================================="
echo "   INICIANDO BACKUP PARA A NUVEM"
echo "=========================================="
echo ""

# 1. Capturando a data atual (Formato AAAA-MM-DD)
DATA=$(date +%Y-%m-%d)
NOME_ARQUIVO="backup_$DATA.zip" 

# 2. Definindo os caminhos (PATHs absolutos apontando para o disco C)
ORIGEM="/c/Projetos_Aula"
DESTINO="/c/Nuvem_Drive/$NOME_ARQUIVO"

# 3. Executando a compactação em ZIP
echo "Compactando arquivos da pasta $ORIGEM..."

# Entrando na pasta de origem para evitar a criação de árvores de pastas vazias no .zip
cd "$ORIGEM" || exit

# Comando zip: -r (recursivo), arquivo de destino, e "." para todos os arquivos da pasta atual
zip -r "$DESTINO" .

echo ""
echo "=========================================="
echo "BACKUP CONCLUÍDO COM SUCESSO!"
echo "Arquivo gerado: $NOME_ARQUIVO"
echo "=========================================="

```

### 3. Permissão e Execução

No ecossistema Linux/Bash, os scripts precisam de permissão explícita para rodar. No seu terminal, navegue até a pasta onde salvou o arquivo `rotina_backup.sh` e execute:

```bash
# Dando permissão de execução
chmod +x rotina_backup.sh

# Rodando o script
./rotina_backup.sh

```

Verifique o resultado listando os arquivos na pasta de destino:

```bash
ls -lh /c/Nuvem_Drive

```

*🎉 Sucesso! Você deve ver um arquivo `.zip` perfeitamente formatado com a data de hoje.*

---

## 🤖 Desafio Extra: Automação Total (Agendador de Tarefas)

No mundo corporativo, backups não são feitos manualmente. Para que esse script rode sozinho no Windows toda semana:

1. Aperte `Win + R`, digite `taskschd.msc` e dê `Enter`.
2. Vá em **Criar Tarefa Básica...**
3. Configure para rodar **Semanalmente** (ex: Sexta-feira às 23h00).
4. Na aba **Ação**, escolha **Iniciar um programa**.
5. No campo "Programa/script", coloque o caminho do executável do Git Bash (ex: `C:\Program Files\Git\bin\bash.exe`).
6. No campo "Adicione argumentos", digite: `-c "/c/caminho/para/seu/rotina_backup.sh"`.

Salvem suas alterações, subam os scripts pro repositório individual de vocês e até a próxima aula! 👨‍💻👩‍💻

