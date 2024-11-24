# Python Flask - Demo Web Application

This is a simple Python Flask web application. The app provides system information and a realtime monitoring screen with dials showing CPU, memory, IO and process information.

The app has been designed with cloud native demos & containers in mind, in order to provide a real working application for deployment, something more than "hello-world" but with the minimum of pre-reqs. It is not intended as a complete example of a fully functioning architecture or complex software design.

Typical uses would be deployment to Kubernetes, demos of Docker, CI/CD (build pipelines are provided), deployment to cloud (Azure) monitoring, auto-scaling

## Screenshot

![screen](https://user-images.githubusercontent.com/14982936/30533171-db17fccc-9c4f-11e7-8862-eb8c148fedea.png)

# Status

![](https://img.shields.io/github/last-commit/benc-uk/python-demoapp) ![](https://img.shields.io/github/release-date/benc-uk/python-demoapp) ![](https://img.shields.io/github/v/release/benc-uk/python-demoapp) ![](https://img.shields.io/github/commit-activity/y/benc-uk/python-demoapp)

Live instances:

[![](https://img.shields.io/website?label=Hosted%3A%20Azure%20App%20Service&up_message=online&url=https%3A%2F%2Fpython-demoapp.azurewebsites.net%2F)](https://python-demoapp.azurewebsites.net/)  
[![](https://img.shields.io/website?label=Hosted%3A%20Kubernetes&up_message=online&url=https%3A%2F%2Fpython-demoapp.kube.benco.io%2F)](https://python-demoapp.kube.benco.io/)

## Building & Running Locally

### Pre-reqs

- Be using Linux, WSL or MacOS, with bash, make etc
- [Python 3.8+](https://www.python.org/downloads/) - for running locally, linting, running tests etc
- [Docker](https://docs.docker.com/get-docker/) - for running as a container, or image build and push
- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux) - for deployment to Azure

Clone the project to any directory where you do development work

```
git clone https://github.com/benc-uk/python-demoapp.git
```

### Makefile

A standard GNU Make file is provided to help with running and building locally.

```text
help                 💬 This help message
lint                 🔎 Lint & format, will not fix but sets exit code on error
lint-fix             📜 Lint & format, will try to fix errors and modify code
image                🔨 Build container image from Dockerfile
push                 📤 Push container image to registry
run                  🏃 Run the server locally using Python & Flask
deploy               🚀 Deploy to Azure Web App
undeploy             💀 Remove from Azure
test                 🎯 Unit tests for Flask app
test-report          🎯 Unit tests for Flask app (with report output)
test-api             🚦 Run integration API tests, server must be running
clean                🧹 Clean up project
```

Make file variables and default values, pass these in when calling `make`, e.g. `make image IMAGE_REPO=blah/foo`

| Makefile Variable | Default                |
| ----------------- | ---------------------- |
| IMAGE_REG         | ghcr<span>.</span>io   |
| IMAGE_REPO        | benc-uk/python-demoapp |
| IMAGE_TAG         | latest                 |
| AZURE_RES_GROUP   | temp-demoapps          |
| AZURE_REGION      | uksouth                |
| AZURE_SITE_NAME   | pythonapp-{git-sha}    |

The app runs under Flask and listens on port 5000 by default, this can be changed with the `PORT` environmental variable.

# Containers

Public container image is [available on GitHub Container Registry](https://github.com/users/benc-uk/packages/container/package/python-demoapp)

Run in a container with:

```bash
docker run --rm -it -p 5000:5000 ghcr.io/benc-uk/python-demoapp:latest
```

Should you want to build your own container, use `make image` and the above variables to customise the name & tag.

## Kubernetes

The app can easily be deployed to Kubernetes using Helm, see [deploy/kubernetes/readme.md](deploy/kubernetes/readme.md) for details

# GitHub Actions CI/CD

A working set of CI and CD release GitHub Actions workflows are provided `.github/workflows/`, automated builds are run in GitHub hosted runners

### [GitHub Actions](https://github.com/benc-uk/python-demoapp/actions)

[![](https://img.shields.io/github/workflow/status/benc-uk/python-demoapp/CI%20Build%20App)](https://github.com/benc-uk/python-demoapp/actions?query=workflow%3A%22CI+Build+App%22)

[![](https://img.shields.io/github/workflow/status/benc-uk/python-demoapp/CD%20Release%20-%20AKS?label=release-kubernetes)](https://github.com/benc-uk/python-demoapp/actions?query=workflow%3A%22CD+Release+-+AKS%22)

[![](https://img.shields.io/github/workflow/status/benc-uk/python-demoapp/CD%20Release%20-%20Webapp?label=release-azure)](https://github.com/benc-uk/python-demoapp/actions?query=workflow%3A%22CD+Release+-+Webapp%22)

[![](https://img.shields.io/github/last-commit/benc-uk/python-demoapp)](https://github.com/benc-uk/python-demoapp/commits/master)

## Running in Azure App Service (Linux)

If you want to deploy to an Azure Web App as a container (aka Linux Web App), a Bicep template is provided in the [deploy](deploy/) directory

For a super quick deployment, use `make deploy` which will deploy to a resource group, temp-demoapps and use the git ref to create a unique site name

```bash
make deploy
```

## Running in Azure App Service (Windows)

Just don't, it's awful
---------------

Objetivo da Tarefa:

Acredito que o seu objetivo seja resolver o problema de senha no seu pipeline Jenkins, implementando uma das soluções propostas.

Passo a Passo Detalhado (Considerando a Solução Ansible):

Como a solução com Ansible é considerada mais segura e automatizada, vamos detalhar os passos para implementá-la:

- Instalação do Ansible:
        No servidor Jenkins (ou em um servidor de controle): Instale o Ansible seguindo as instruções oficiais para a sua distribuição Linux.
        Nos nós (máquinas onde o pipeline será executado): Instale o agente Ansible.
```
    Criação do Playbook:
        Um playbook é um arquivo YAML que descreve as tarefas a serem executadas.
        Exemplo:
        YAML

        - name: Atualizar pacotes
          hosts: all
          become: yes
          tasks:
            - name: Atualizar lista de pacotes
              apt:
                update_cache: yes

        Use o código com cuidado.
```
-  Explicação:
        hosts: all: Indica que a tarefa será executada em todos os hosts.
        become: yes: Executa as tarefas com privilégios de root.
        apt: update_cache: yes: Atualiza a lista de pacotes disponíveis.

-  Integração com o Jenkins:

    Instale o plugin Ansible: No seu Jenkins, instale o plugin Ansible para executar playbooks a partir do pipeline.
    Configure o plugin: Configure o plugin com as informações do seu inventário Ansible e credenciais de autenticação.
    Escreva a etapa no seu pipeline:
    Groovy
   ```
    pipeline {
        agent any
        stages {
            stage('Atualizar pacotes') {
                steps {
                    ansiblePlaybook playbook: 'meu_playbook.yml'
                }
            }
        }
    }

    Use o código com cuidado.
  ``
- Execução do Pipeline:
        Ao executar o pipeline, a etapa Ansible será acionada, executando o playbook e atualizando os pacotes nos nós.

- Outras Soluções:

    Configurar o sudoers: Essa opção deve ser usada com cautela, pois pode comprometer a segurança do sistema.
    Usar o plugin de credenciais do Jenkins: Essa opção é útil para armazenar senhas de forma segura, mas ainda requer a configuração do sudo para permitir a autenticação.
    Usar o sudo com senha: Essa é a opção menos recomendada, pois exige que a senha seja digitada manualmente a cada execução.

- Considerações Adicionais:

    Segurança: Ao utilizar o Ansible, é importante seguir as melhores práticas de segurança, como limitar os privilégios do usuário Ansible e utilizar variáveis para armazenar senhas de forma segura.
    Complexidade: A escolha da solução ideal dependerá da complexidade do seu ambiente e das suas necessidades específicas.
    Documentação: Consulte a documentação oficial do Ansible e do plugin Ansible para Jenkins para obter mais informações e exemplos.
