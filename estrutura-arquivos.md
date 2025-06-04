# Estrutura de Arquivos para Documentação Azure VM Lab

Este documento explica a estrutura de pastas e arquivos recomendada para o repositório Azure VM Lab, além de sugestões de conteúdo para os arquivos de documentação complementares.

## Estrutura do Repositório

```
azure-vm-lab/
├── README.md                # Documentação principal
├── images/                  # Pasta para capturas de tela
│   ├── vm-creation-step1.png
│   ├── vm-creation-step2.png
│   ├── vm-creation-step3.png
│   ├── vm-dashboard.png
│   └── vm-iis-welcome.png
├── docs/                    # Documentação adicional
│   ├── configuracao-inicial.md
│   └── troubleshooting.md
└── scripts/                 # Scripts úteis
    └── install-iis.ps1
```

## Sugestões de Conteúdo para Arquivos Complementares

### 📄 docs/configuracao-inicial.md

```markdown
# Configuração Inicial da VM Azure

Este documento detalha os passos necessários para configurar sua VM Windows após a criação.

## Atualizações do Sistema

1. Abra o Windows Update
2. Verifique e instale todas as atualizações disponíveis
3. Reinicie a VM se necessário

## Instalação do IIS

Execute o seguinte comando no PowerShell com privilégios de administrador:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## Configuração de Firewall

Abra as portas necessárias no firewall do Windows:

```powershell
New-NetFirewallRule -DisplayName "Allow HTTP" -Direction Inbound -Protocol TCP -LocalPort 80 -Action Allow
```

## Verificação do Servidor Web

1. Abra o navegador na VM
2. Acesse `http://localhost`
3. Confirme que a página padrão do IIS é exibida

## Configuração de Auto-Shutdown

1. No portal Azure, acesse sua VM
2. Clique em "Auto-shutdown"
3. Configure um horário para desligar automaticamente
4. Salve as configurações

*Documentação elaborada por Tabata Gonzales*
```

### 📄 docs/troubleshooting.md

```markdown
# Guia de Solução de Problemas - Azure VM

Este documento lista problemas comuns e suas soluções para VMs Windows no Azure.

## Problemas de Conexão RDP

### Problema: Não consigo conectar via RDP

**Possíveis causas e soluções:**

1. **Firewall bloqueando porta 3389**
   - Verifique o NSG (Network Security Group) no Azure
   - Confirme regra de entrada permitindo RDP (TCP 3389)

2. **VM não está em execução**
   - Verifique status da VM no portal Azure
   - Inicie a VM se estiver parada

3. **Credenciais incorretas**
   - Confirme nome de usuário e senha
   - Redefina senha se necessário pelo portal Azure

## Problemas com IIS

### Problema: Site não está acessível externamente

**Possíveis causas e soluções:**

1. **Porta 80 bloqueada**
   - Verifique NSG para regra de entrada HTTP (porta 80)
   - Execute o comando para abrir a porta no firewall do Windows:
   ```powershell
   New-NetFirewallRule -DisplayName "Allow HTTP" -Direction Inbound -Protocol TCP -LocalPort 80 -Action Allow
   ```

2. **IIS não está executando**
   - Verifique status do serviço IIS:
   ```powershell
   Get-Service W3SVC
   ```
   - Inicie o serviço se estiver parado:
   ```powershell
   Start-Service W3SVC
   ```

## Problemas de Performance

### Problema: VM lenta ou com alta utilização de CPU

**Possíveis causas e soluções:**

1. **VM subdimensionada**
   - Verifique o tamanho atual da VM no portal
   - Considere redimensionar para um tamanho maior

2. **Muitos processos em execução**
   - Use o Gerenciador de Tarefas para identificar processos consumindo recursos
   - Encerre processos desnecessários

## Contato para Suporte

Se os problemas persistirem, entre em contato com Tabata Gonzales para suporte adicional.

*Documentação elaborada por Tabata Gonzales*
```

## Script de Instalação do IIS

### 📄 scripts/install-iis.ps1

```powershell
# Script de instalação e configuração do IIS
# Autor: Tabata Gonzales

# Instala o IIS com ferramentas de gerenciamento
Install-WindowsFeature -name Web-Server -IncludeManagementTools

# Configura o firewall para permitir HTTP
New-NetFirewallRule -DisplayName "Allow HTTP" -Direction Inbound -Protocol TCP -LocalPort 80 -Action Allow

# Cria uma página personalizada
$htmlContent = @"
<!DOCTYPE html>
<html>
<head>
    <title>VM Azure - Laboratório</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 40px;
            text-align: center;
        }
        h1 {
            color: #0078D4;
        }
    </style>
</head>
<body>
    <h1>Servidor Web Azure</h1>
    <p>Implementado por Tabata Gonzales</p>
    <p>Data de configuração: $(Get-Date -Format 'dd/MM/yyyy')</p>
</body>
</html>
"@

# Salva o conteúdo HTML na página padrão
Set-Content -Path "C:\inetpub\wwwroot\index.html" -Value $htmlContent

# Reinicia o serviço IIS
Restart-Service W3SVC

Write-Host "IIS instalado e configurado com sucesso!" -ForegroundColor Green
```