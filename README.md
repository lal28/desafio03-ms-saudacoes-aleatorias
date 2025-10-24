# Pipeline CI/CD - Microserviço Saudações Aleatórias

## 📚 Sobre o Projeto

Este projeto faz parte da solução de um desafio de um curso de DevOps e implementa uma pipeline CI/CD completa para um microserviço Go.

**Template base:** https://gitlab.com/avanti-dvp/ms-saudacoes-aleatorias

## 🔧 Principais Mudanças Implementadas

### 1. **Renomeação dos Jobs**
Os jobs foram renomeados para seguir as especificações do curso:
- `lint` → `build-lint`
- `build-and-push` → `release`
- `destroy` → `cleanup`

### 2. **Fluxo de Execução**
A pipeline foi ajustada para três cenários:

**Push em branches não-main:**
```
build-lint → test
```

**Push na branch main:**
```
build-lint → test → release → deploy
```

**Execução manual (workflow_dispatch):**
```
build-lint → test → release → deploy → cleanup
```

### 3. **Condicionais dos Jobs**
- Jobs `release` e `deploy`: executam em push na main **OU** em workflow_dispatch
- Job `cleanup`: executa **APENAS** em workflow_dispatch manual


### 4. **Ajustes nas versões Utilizadas**
- **Go**: 1.24 (build-lint) e 1.22 (test)
- **golangci-lint**: v1.64.2 (compatível com Go 1.24)

## 🚀 Como Usar

### Deploy Automático
Faça push na branch `main` e a pipeline executará automaticamente até o deploy.

### Cleanup Manual
1. Vá em **Actions** no GitHub
2. Selecione o workflow **"CI/CD Pipeline"**
3. Clique em **"Run workflow"**
4. Selecione a branch
5. Clique em **"Run workflow"** novamente

Isso executará todo o fluxo incluindo a destruição da infraestrutura ao final.

## 📋 Requisitos

### Secrets do GitHub
- `DOCKER_PASS`: Token de acesso ao Docker Hub
- `KOYEB_TOKEN`: Token de acesso à plataforma Koyeb


