---
title: Configuração do Husky - Hooks de Qualidade
type: note
permalink: configuracoes/configuracao-do-husky-hooks-de-qualidade
---

# Configuração do Husky com Hooks de Qualidade de Código

## Data: 05/01/2025

## Contexto
Instalação e configuração do Husky para automatizar verificações de qualidade de código através de Git hooks no projeto user-contact (Laravel 12).

## Implementação Realizada

### 1. Instalação
- **Husky 9.1.7** instalado como dependência de desenvolvimento
- Script `prepare: "husky"` adicionado ao package.json para inicialização automática

### 2. Hooks Configurados

#### Pre-commit Hook
- **Arquivo**: `.husky/pre-commit`
- **Comando**: `vendor/bin/pint --dirty`
- **Função**: Formatar automaticamente apenas arquivos modificados antes do commit
- **Benefício**: Garante formatação consistente em todo commit

#### Pre-push Hook  
- **Arquivo**: `.husky/pre-push`
- **Comando**: `composer quality-check`
- **Função**: Executar validação completa antes do push
- **Inclui**:
  - Formatação com Pint
  - Análise estática com PHPStan
  - Execução de todos os testes PHPUnit

### 3. Testes de Validação
- ✅ Pint executou corretamente (26 arquivos processados)
- ✅ Quality check passou completamente
- ✅ Todos os testes passaram (2/2)
- ✅ PHPStan não encontrou erros
- ✅ Hooks executaram automaticamente durante commit e push

### 4. Commit Realizado
**Hash**: 3ffbcf0
**Mensagem**: "feat: configurar Husky com hooks de qualidade de código"
**Arquivos alterados**: 4 files (package.json, package-lock.json, .husky/pre-commit, .husky/pre-push)

## Fluxo de Trabalho Estabelecido

### No Commit:
1. Desenvolvedor executa `git commit`
2. Hook pre-commit executa automaticamente
3. Pint formata código modificado (`--dirty`)
4. Commit procede se formatação bem-sucedida

### No Push:
1. Desenvolvedor executa `git push`  
2. Hook pre-push executa automaticamente
3. Quality check completo (format + analyse + test)
4. Push procede apenas se todos os checks passarem

## Benefícios Alcançados

### Qualidade de Código
- **Formatação consistente**: Todo código commitado segue padrões Pint
- **Análise estática**: PHPStan previne bugs antes do push
- **Cobertura de testes**: Garante que mudanças não quebram testes existentes

### Eficiência do Time
- **Automação**: Sem necessidade de lembrar de rodar comandos manualmente
- **Feedback rápido**: Erros detectados localmente antes do push
- **Padronização**: Todos os desenvolvedores seguem mesmo fluxo

### Integração com Projeto
- **Laravel 12**: Compatible com estrutura streamlined
- **Composer scripts**: Utiliza scripts já configurados (quality-check)
- **Fluxo dev**: Integra com workflow existente (dev, test, analyse)

## Arquivos Relacionados
- `package.json` - Dependência e script prepare
- `package-lock.json` - Lock file atualizado
- `.husky/pre-commit` - Hook de formatação
- `.husky/pre-push` - Hook de validação completa
- `composer.json` - Scripts quality-check, format, analyse, test

## Comandos Úteis
```bash
# Bypass hooks (use com cautela)
git commit --no-verify
git push --no-verify

# Executar manualmente
npx husky
vendor/bin/pint --dirty
composer quality-check

# Testar hooks
.husky/pre-commit
.husky/pre-push
```

## Status
✅ **IMPLEMENTADO E FUNCIONAL**
- Instalação completa
- Hooks configurados e testados
- Commit e push realizados com sucesso
- Validação automática operacional