###  Pré-requisitos Globais

Antes de começar, garanta que você tem os seguintes softwares instalados e configurados no seu sistema:

-   **[Git](https://git-scm.com/downloads)**: Para clonar o repositório.
-   **[Node.js](https://nodejs.org/en/)**: Versão `18.x` ou superior.
-   **[Python](https://www.python.org/downloads/)**: Versão `3.9` ou superior.

### ⚙️ Instalação das Dependências do OCR (Obrigatório)

O microsserviço de OCR depende de duas ferramentas externas. A instalação correta delas é **crucial** para o funcionamento do sistema.

---
#### **Instrução para Windows**

1.  **Instalar Tesseract-OCR:**
    * Baixe o instalador `tesseract-ocr-w64-setup-*.exe` a partir de [**Tesseract at UB Mannheim**](https://github.com/UB-Mannheim/tesseract/wiki).
    * Execute o instalador. Durante a instalação, na tela "Additional language data", marque a opção **"Portuguese"** para adicionar o suporte ao idioma português.
    * **IMPORTANTE:** Na tela de instalação, certifique-se de marcar a opção **"Add Tesseract to the system PATH"**. Isso configura a variável de ambiente automaticamente.

2.  **Instalar Poppler:**
    * Baixe a versão mais recente do [**Poppler for Windows**](https://github.com/oschwartz10612/poppler-windows/releases/). Procure pelo arquivo `Release-*.zip`.
    * Extraia o conteúdo do arquivo `.zip` para uma pasta permanente no seu computador (ex: `C:\Program Files\poppler`).
    * Copie o caminho da pasta `bin` que está dentro do diretório que você extraiu (ex: `C:\Program Files\poppler\bin`).
    * Adicione este caminho ao **PATH do sistema**:
        * Pesquise por "Editar as variáveis de ambiente do sistema" no menu Iniciar.
        * Clique em "Variáveis de Ambiente...".
        * Na seção "Variáveis do sistema", encontre e selecione a variável `Path` e clique em "Editar".
        * Clique em "Novo", cole o caminho da pasta `bin` do Poppler e clique em "OK" em todas as janelas.

3.  **Verificação:**
    * Abra um **novo** terminal (importante para carregar o novo PATH) e execute os comandos `tesseract --version` e `pdftoppm -v`. Se ambos os comandos exibirem as versões das ferramentas, a instalação foi bem-sucedida.

---
#### **Instrução para Linux (Debian/Ubuntu)**

1.  **Instalar Tesseract-OCR e Poppler:**
    * Abra o terminal e execute os comandos abaixo para instalar as ferramentas e o pacote de idioma português:
    ```bash
    sudo apt update
    sudo apt install -y tesseract-ocr tesseract-ocr-por poppler-utils
    ```
2.  **Verificação:**
    * Execute os comandos `tesseract --version` e `pdftoppm -v`. Se ambos exibirem as versões, a instalação está correta.

---
#### **Instrução para macOS (usando Homebrew)**

1.  **Instalar Tesseract-OCR e Poppler:**
    * Se você não tiver o [Homebrew](https://brew.sh/index_pt-br) instalado, instale-o primeiro.
    * Abra o terminal e execute os comandos para instalar as ferramentas e o pacote de idioma português:
    ```bash
    brew install tesseract tesseract-lang poppler
    ```
2.  **Verificação:**
    * Execute os comandos `tesseract --version` e `pdftoppm -v`. Se ambos exibirem as versões, a instalação está correta.

---


### Instruções Passo a Passo

#### 1. Clone o Repositório

```bash
git https://github.com/filipetocchio/Qota-OCR-Service
cd  Qota-OCR-Service
```

#### 2. Configuração do Microsserviço de OCR (Python)

Este serviço precisa estar rodando para que a validação de documentos funcione.

```bash
# Navegue até a pasta do serviço
cd  Qota-OCR-Service

# Crie e ative um ambiente virtual
python -m venv venv

# No Windows:
.\venv\Scripts\activate

# No Linux/macOS:
source venv/bin/activate


python -m pip install --upgrade pip

# Instale as dependências
pip install -r requirements.txt

# Inicie o servidor Python (deixe este terminal aberto)
python app.py
```

> **Nota:** O servidor do OCR irá rodar na porta `8000`.