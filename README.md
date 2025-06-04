# 🚀 Laboratório Azure: Criação de Máquinas Virtuais

<div align="center">
  
![Azure](https://img.shields.io/badge/Microsoft%20Azure-0078D4?style=for-the-badge&logo=microsoft-azure&logoColor=white)
![Windows Server](https://img.shields.io/badge/Windows%20Server-0078D6?style=for-the-badge&logo=windows&logoColor=white)
![Status](https://img.shields.io/badge/Status-Conclu%C3%ADdo-brightgreen?style=for-the-badge)

**Documentação prática para implementação e configuração de VMs na Microsoft Azure**

*Autor: Tabata Gonzales*

</div>

---

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Pré-requisitos](#pré-requisitos)
- [Passo a Passo](#passo-a-passo)
- [Configurações Importantes](#configurações-importantes)
- [Capturas de Tela](#capturas-de-tela)
- [Lições Aprendidas](#lições-aprendidas)
- [Referências](#referências)

## 📖 Sobre o Projeto

Este repositório documenta minha experiência prática com a criação de máquinas virtuais na Microsoft Azure, explorando conceitos de computação em nuvem, escalabilidade e eficiência. O projeto abrange desde a criação básica até configurações avançadas, incluindo instalação do IIS e conectividade RDP.

### 🛠️ Tecnologias Utilizadas

- **Microsoft Azure** - Plataforma de nuvem
- **Windows Server 2022** - Sistema operacional da VM
- **IIS (Internet Information Services)** - Servidor web
- **RDP (Remote Desktop Protocol)** - Protocolo de acesso remoto
- **PowerShell** - Scripts de automação

## ✅ Pré-requisitos

Para reproduzir este laboratório, você precisa:

- ✅ Conta ativa no Microsoft Azure
- ✅ Conhecimentos básicos de Windows Server
- ✅ Acesso ao Portal do Azure
- ✅ Conhecimento básico em redes (firewall, portas)
- ✅ Cliente RDP instalado (Windows Remote Desktop)

## 🚀 Passo a Passo

### 1. Acessando o Portal do Azure
1. Acesse [portal.azure.com](https://portal.azure.com)
2. Faça login com sua conta Microsoft/Azure
3. No menu principal, clique em **"Máquinas Virtuais"**
4. Selecione **"+ Criar"** → **"Máquina virtual do Azure"**

### 2. Configurações Básicas da VM
1. **Assinatura**: Selecione sua assinatura ativa
2. **Grupo de recursos**: Crie um novo ou use existente
3. **Nome da VM**: Digite um nome descritivo (ex: `vm-lab-tabata`)
4. **Região**: Escolha a região mais próxima
5. **Imagem**: Selecione **Windows Server 2022 Datacenter**
6. **Tamanho**: Escolha `Standard_B1s` (básico para laboratório)

### 3. Configuração de Conta Administrador
1. **Nome de usuário**: Digite um nome de administrador
2. **Senha**: Crie uma senha forte (min. 12 caracteres)
3. **Confirmar senha**: Digite novamente a senha

### 4. Configuração de Rede
1. **Portas de entrada**: Marque **"Permitir portas selecionadas"**
2. **Selecionar portas**: Escolha **RDP (3389)** e **HTTP (80)**
3. Mantenha as demais configurações padrão

### 5. Finalização e Criação
1. Clique em **"Examinar + criar"**
2. Aguarde a validação
3. Clique em **"Criar"** para iniciar a implantação
4. Aguarde aproximadamente 5-10 minutos

### 6. Conexão via RDP
1. Na VM criada, clique em **"Conectar"** → **"RDP"**
2. Baixe o arquivo `.rdp`
3. Execute o arquivo e insira as credenciais
4. Conecte-se à máquina virtual

## ⚙️ Configurações Importantes

### Instalação do IIS
Execute no PowerShell da VM:
```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

### Configuração do Firewall
Para permitir tráfego HTTP:
```powershell
New-NetFirewallRule -DisplayName "Allow HTTP" -Direction Inbound -Protocol TCP -LocalPort 80 -Action Allow
```

### Teste de Conectividade
1. Abra o navegador na VM
2. Acesse `http://localhost`
3. Verifique se a página padrão do IIS aparece

## 📸 Capturas de Tela

![Criação da VM](./images/vm-creation-step1.png)
*Tela inicial de criação da máquina virtual*

![Configurações Básicas](./images/vm-creation-step2.png)
*Formulário de configurações básicas da VM*

![Configuração de Rede](./images/vm-creation-step3.png)
*Configuração de portas e acesso à rede*

![Dashboard da VM](./images/vm-dashboard.png)
*Dashboard de monitoramento da VM no portal Azure*

![IIS Funcionando](./images/vm-iis-welcome.png)
*Página de boas-vindas do IIS após instalação*

## 💡 Lições Aprendidas

### ✅ Principais Aprendizados
- **Planejamento de custos**: VMs consomem recursos constantemente, importante desligar quando não usar
- **Segurança de rede**: Configurar apenas as portas necessárias nos Network Security Groups
- **Backup automático**: Configurar backups desde o início evita perda de dados
- **Monitoramento**: Azure Monitor fornece métricas importantes de performance

### ⚠️ Dificuldades Encontradas
- **Conectividade RDP**: Inicial dificuldade com firewall, resolvido liberando porta 3389
- **Custos inesperados**: VM ficou ligada por 3 dias, gerando custo maior que esperado
- **Performance lenta**: VM básica (B1s) mostrou limitações, upgrade para B2s resolveu
- **Configuração IIS**: Necessário instalar role manualmente, não vem pré-instalado

### 💰 Dicas de Economia
- Sempre **desligar a VM** quando não estiver usando
- Usar **discos Standard** para laboratórios (não Premium)
- Configurar **auto-shutdown** para evitar custos desnecessários
- Monitorar gastos pelo **Azure Cost Management**

## 📚 Referências

- [Documentação oficial da Microsoft](https://learn.microsoft.com/pt-br/azure/)
- [Criar VM Windows no Portal Azure](https://learn.microsoft.com/pt-br/azure/virtual-machines/windows/quick-create-portal)
- [Configuração de IIS no Windows Server](https://learn.microsoft.com/pt-br/iis/)
- [Melhores práticas de segurança Azure](https://learn.microsoft.com/pt-br/azure/security/)
- Material do curso DIO - Digital Innovation One

---

<div align="center">

**Desenvolvido por Tabata Gonzales** 👩‍💻

[⬆ Voltar ao topo](#-laboratório-azure-criação-de-máquinas-virtuais)

</div>
