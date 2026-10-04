# React Inversify

A React library that integrates the Inversify dependency injection container, enabling modern, scalable, and maintainable application architecture through inversion of control patterns.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Node.js & NPM Setup](#nodejs--npm-setup)
- [Visual Studio Configuration](#visual-studio-configuration)
- [Terraform Setup](#terraform-setup)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Development](#development)
- [Contributing](#contributing)

## Prerequisites

Before you begin, ensure you have the following installed on your system:

- **Node.js** (v16.0.0 or higher)
- **npm** (v7.0.0 or higher) - comes with Node.js
- **Visual Studio Code** (recommended) or **Visual Studio 2022**
- **Git** (for version control)
- **Terraform** (v1.0.0 or higher) - if using infrastructure as code features

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/akashy1992/react-inversify.git
cd react-inversify
```

### 2. Install Dependencies

```bash
npm install
```

This command will install all required dependencies as specified in `package.json`.

## Node.js & NPM Setup

### Node.js Installation

#### Windows
1. Download the LTS version from [nodejs.org](https://nodejs.org/)
2. Run the installer and follow the prompts
3. Verify installation:
   ```bash
   node --version
   npm --version
   ```

#### macOS
Using Homebrew:
```bash
brew install node
```

#### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install nodejs npm
```

### NPM Package Management

#### Installing Packages
```bash
# Install all dependencies from package.json
npm install

# Install a specific package
npm install <package-name>

# Install as a dev dependency
npm install --save-dev <package-name>
```

#### Updating Packages
```bash
# Check for outdated packages
npm outdated

# Update all packages
npm update

# Update a specific package
npm update <package-name>
```

#### Running Scripts
```bash
# View available scripts in package.json
npm run

# Build the project
npm run build

# Start development server
npm start

# Run tests
npm test

# Run linting
npm run lint
```

#### Managing Cache
```bash
# Clear npm cache
npm cache clean --force

# Verify cache integrity
npm cache verify
```

## Visual Studio Configuration

### Visual Studio Code Setup

#### 1. Install Extensions
Recommended extensions for this project:

- **ES7+ React/Redux/React-Native snippets** - by dsznajder.es7-react-js-snippets
- **Prettier - Code formatter** - by Prettier
- **ESLint** - by Microsoft
- **TypeScript Vue Plugin** (if using TypeScript)
- **Inversify Inspector** - for debugging dependency injection

To install extensions:
1. Open VS Code
2. Go to Extensions (Ctrl+Shift+X / Cmd+Shift+X)
3. Search for the extension name
4. Click Install

#### 2. Configure Workspace Settings

Create `.vscode/settings.json` in the project root:

```json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[react]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```

#### 3. Configure Launch Configuration

Create `.vscode/launch.json` for debugging:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "React DevServer",
      "type": "chrome",
      "request": "launch",
      "url": "http://localhost:3000",
      "webRoot": "${workspaceFolder}/src",
      "sourceMapPathOverride": {
        "webpack:///src/*": "${webspaceRoot}/*"
      }
    }
  ]
}
```

### Visual Studio 2022 Setup

#### 1. Install Tools
- Open Visual Studio Installer
- Select "Node.js development" workload
- Install "Node.js development tools"

#### 2. Open Project
1. File → Open → Folder
2. Select the react-inversify project folder
3. Visual Studio will auto-detect Node.js and npm

#### 3. Configure Launch Settings

Create `launch.json` in your project debug configuration:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "npm start",
      "type": "node",
      "request": "launch",
      "program": "${workspaceFolder}/node_modules/react-scripts/bin/react-scripts.js",
      "args": ["start"],
      "cwd": "${workspaceFolder}"
    }
  ]
}
```

## Terraform Setup

### Purpose

Terraform configuration is used for infrastructure as code, managing cloud resources for deployment and environment setup.

### Installation

#### Windows
```bash
# Using Chocolatey
choco install terraform

# Or download from terraform.io and add to PATH
```

#### macOS
```bash
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
```

#### Linux
```bash
wget https://releases.hashicorp.com/terraform/1.x.x/terraform_1.x.x_linux_amd64.zip
unzip terraform_1.x.x_linux_amd64.zip
sudo mv terraform /usr/local/bin/
```

### Verify Installation
```bash
terraform --version
```

### Terraform Project Structure

```
terraform/
├── main.tf           # Primary resource definitions
├── variables.tf      # Input variable definitions
├── outputs.tf        # Output values
├── terraform.tfvars  # Variable values (do not commit)
└── .gitignore        # Exclude sensitive files
```

### Basic Terraform Commands

#### Initialize Terraform
```bash
cd terraform
terraform init
```

#### Validate Configuration
```bash
terraform validate
```

#### Plan Deployment
```bash
terraform plan -out=tfplan
```

#### Apply Configuration
```bash
terraform apply tfplan
```

#### Destroy Resources
```bash
terraform destroy
```

### Example: AWS Deployment

Create `terraform/main.tf`:

```hcl
provider "aws" {
  region = var.aws_region
}

resource "aws_s3_bucket" "app_bucket" {
  bucket = var.app_name
}

resource "aws_s3_bucket_website_configuration" "app_website" {
  bucket = aws_s3_bucket.app_bucket.id

  index_document {
    suffix = "index.html"
  }
}
```

### Environment Variables

```bash
export AWS_ACCESS_KEY_ID="your-access-key"
export AWS_SECRET_ACCESS_KEY="your-secret-key"
export AWS_REGION="us-east-1"
```

Or create `terraform.tfvars`:

```hcl
aws_region = "us-east-1"
app_name   = "react-inversify-app"
```

## Getting Started

### 1. Setup Development Environment

```bash
# Clone repository
git clone https://github.com/akashy1992/react-inversify.git
cd react-inversify

# Install dependencies
npm install

# Verify setup
npm run build
```

### 2. Start Development Server

```bash
npm start
```

The application will open in your browser at `http://localhost:3000`

### 3. Development Workflow

```bash
# Run tests in watch mode
npm test

# Lint code
npm run lint

# Format code with Prettier
npm run format

# Build for production
npm run build
```

## Project Structure

```
react-inversify/
├── src/
│   ├── components/      # React components
│   ├── containers/      # Container setup and DI configuration
│   ├── services/        # Business logic and services
│   ├── types/           # TypeScript type definitions
│   ├── App.tsx          # Main app component
│   └── index.tsx        # Application entry point
├── public/              # Static assets
├── tests/               # Test files
├── terraform/           # Infrastructure as code
├── .vscode/             # VS Code configuration
├── package.json         # Project dependencies and scripts
├── tsconfig.json        # TypeScript configuration
├── .eslintrc.json       # ESLint configuration
├── .prettierrc           # Prettier configuration
└── README.md            # This file
```

## Development

### Scripts Available

```bash
npm start              # Start development server
npm run build          # Create production build
npm test               # Run test suite
npm run lint           # Check code quality
npm run format         # Format code with Prettier
npm run eject          # Eject from create-react-app (one-way operation)
```

### Git Workflow

```bash
# Create feature branch
git checkout -b feature/your-feature-name

# Make changes and commit
git add .
git commit -m "feat: description of changes"

# Push branch
git push origin feature/your-feature-name

# Create Pull Request on GitHub
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For issues, questions, or contributions, please visit the [GitHub repository](https://github.com/akashy1992/react-inversify/issues).

---

**Last Updated:** October 2026
