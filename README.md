# Server Getting Start

## Python
- Python 3.12
## PostgreSQL

### macOS

```bash
brew install postgresql@14
brew install pgvector
```

```bash
brew services start postgresql@14
```

```bash
createdb morphik
createuser -s postgres
```

### Ubuntu/Debian
Install PostgreSQL from the official repositories.We recommend version 14 . Other versions may work, but haven’t been extensively tested!
```bash
sudo apt update
sudo apt install postgresql postgresql-contrib
```

```bash
sudo apt install postgresql-14-pgvector
```

```bash
sudo systemctl start postgresql
sudo systemctl enable postgresql
```

```bash
sudo -u postgres createdb morphik
sudo -u postgres createuser -s postgres
```

### Windows
1. Download and install PostgreSQL from the official website.
2. During installation, make note of the password you set for the postgres user.
3. Install pgvector:
- Open pgAdmin (installed with PostgreSQL)
- Connect to your PostgreSQL server
- Right-click on “Extensions” and select “Create > Extension”
- Select “pgvector” from the dropdown and click “Save”
4. Create a database for Morphik:
- Right-click on “Databases” and select “Create > Database”
- Name it “morphik” and click “Save”

## Addition Dependencies
Some system-level dependencies might be required for processing various document types:

### macOS

```bash
# Install via Homebrew
brew install poppler tesseract libmagic
```
### Ubuntu/Debian
```bash
# Install via apt
sudo apt-get update
sudo apt-get install -y poppler-utils tesseract-ocr libmagic-dev
```
### Windows
For Windows, you may need to install these dependencies manually:

- Poppler: Download from poppler for Windows
- Tesseract: Download the installer from UB Mannheim
- libmagic: This is included in the python-magic-bin package which will be installed with pip

If you encounter database initialization issues within Docker, you may need to manually initialize the schema:

```bash
psql -U postgres -d morphik -a -f init.sql
```


# Setting Up the Environment

## Active Python

```bash
python3.12 -m venv .venv
```

### Linux/macOS
```bash
source .venv/bin/activate
```

### Windows(Command Prompt)
```bash
.venv\Scripts\activate.bat
```

### Windows(PowerShell)
```bash
.venv\Scripts\Activate.ps1
```
If you encounter execution policy errors in PowerShell, you may need to run:

```bash
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

## Installing Python Dependencies

```bash
pip install -r requirements.txt
```

## Python Dependencies for Document Processing
```bash
# If using Python 3.12+, you might need a specific version of unstructured
pip install unstructured==0.16.10

# Download required NLTK resources
python -m nltk.downloader averaged_perceptron_tagger punkt
```

## Setting up the Server Parameters

```bash
cp .env.example .env
```

```bash
python quick_setup.py
```

## Launching the Server
```bash
python start_server.py
```


# Morphik UI Getting Start

## Node and NPM
### macOS
```bash
# Install Homebrew if you don't have it
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Node.js
brew install node
```

### Linux
```bash
# Install NVM
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.2/install.sh | bash

# Set up NVM environment (add these to your .bashrc or .zshrc)
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

# Restart your terminal or source your profile
source ~/.bashrc  # or ~/.zshrc

# Update npm to the latest version
npm install -g npm

# Install the latest LTS version of Node.js
nvm install --lts

# Use the installed version
nvm use --lts
```

### Windows
1. Using the official installer:
- Visit nodejs.org
- Download the Windows installer (.msi)
- Run the installer and follow the prompts
2. Using Chocolatey:
```bash
# Install Chocolatey if you don't have it (run in PowerShell as Admin)
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

# Install Node.js
choco install nodejs
```


## Running the UI

```bash
cd ee/ui-component
```

```bash
npm i
```


```bash
npm run dev
```