# 👻 Módulo de Segurança Ghost
**Ferramenta de Reforço de Segurança Windows e Azure Baseada em PowerShell**

> **Reforço de segurança proativo para endpoints Windows e ambientes Azure.** Ghost fornece funções de reforço baseadas em PowerShell que podem ajudar a reduzir vetores de ataque comuns ao desativar serviços e protocolos desnecessários.

## ⚠️ Avisos Importantes

**TESTE OBRIGATÓRIO**: Sempre teste o Ghost em ambientes não-produtivos primeiro. Desativar serviços pode afetar funções comerciais legítimas.

**NENHUMA GARANTIA**: Embora o Ghost mire em vetores de ataque comuns, nenhuma ferramenta de segurança pode prevenir todos os ataques. Este é um componente numa estratégia de segurança abrangente.

**IMPACTO OPERACIONAL**: Algumas funções podem afetar a funcionalidade do sistema. Revise cuidadosamente cada configuração antes da implementação.

**AVALIAÇÃO PROFISSIONAL**: Para ambientes de produção, consulte especialistas em segurança para garantir que as configurações estejam alinhadas com as necessidades da sua organização.

## 📊 Panorama de Segurança

Danos por ransomware alcançaram **$57 bilhões em 2025**, com pesquisas mostrando que muitos ataques bem-sucedidos exploram serviços básicos do Windows e configurações incorretas. Vetores de ataque comuns incluem:

- **90% dos incidentes de ransomware** envolvem exploração de RDP
- **Vulnerabilidades SMBv1** permitiram ataques como WannaCry e NotPetya
- **Macros de documentos** permanecem como método principal de entrega de malware
- **Ataques baseados em USB** continuam a visar redes air-gapped
- **Abuso do PowerShell** aumentou significativamente nos últimos anos

## 🛡️ Funções de Segurança do Ghost

Ghost fornece **16 funções de reforço do Windows** mais **integração de segurança Azure**:

### Reforço de Endpoint Windows

| Função | Propósito | Considerações |
|----------|---------|----------------|
| `Set-RDP` | Gerencia acesso ao Remote Desktop | Pode afetar administração remota |
| `Set-SMBv1` | Controla protocolo SMB legado | Necessário para sistemas muito antigos |
| `Set-AutoRun` | Controla AutoPlay/AutoRun | Pode afetar conveniência do usuário |
| `Set-USBStorage` | Limita dispositivos de armazenamento USB | Pode afetar uso legítimo de USB |
| `Set-Macros` | Controla execução de macros do Office | Pode afetar documentos com macros habilitadas |
| `Set-PSRemoting` | Gerencia PowerShell remoto | Pode afetar gerenciamento remoto |
| `Set-WinRM` | Controla Windows Remote Management | Pode afetar administração remota |
| `Set-LLMNR` | Gerencia protocolo de resolução de nomes | Geralmente seguro para desativar |
| `Set-NetBIOS` | Controla NetBIOS sobre TCP/IP | Pode afetar aplicações legadas |
| `Set-AdminShares` | Gerencia compartilhamentos administrativos | Pode afetar acesso remoto a arquivos |
| `Set-Telemetry` | Controla coleta de dados | Pode afetar capacidades diagnósticas |
| `Set-GuestAccount` | Gerencia conta de Convidado | Geralmente seguro para desativar |
| `Set-ICMP` | Controla respostas ping | Pode afetar diagnósticos de rede |
| `Set-RemoteAssistance` | Gerencia Remote Assistance | Pode afetar operações de help desk |
| `Set-NetworkDiscovery` | Controla descoberta de rede | Pode afetar navegação de rede |
| `Set-Firewall` | Gerencia Windows Firewall | Crítico para segurança de rede |

### Segurança da Nuvem Azure

| Função | Propósito | Requisitos |
|----------|---------|--------------|
| `Set-AzureSecurityDefaults` | Habilita segurança básica do Azure AD | Permissões do Microsoft Graph |
| `Set-AzureConditionalAccess` | Configura políticas de acesso | Licenciamento Azure AD P1/P2 |
| `Set-AzurePrivilegedUsers` | Audita contas privilegiadas | Permissões de Global Admin |

### Opções de Implementação Empresarial

| Método | Caso de Uso | Requisitos |
|--------|----------|--------------|
| **Execução Direta** | Teste, ambientes pequenos | Direitos de admin local |
| **Group Policy** | Ambientes de domínio | Admin de domínio, gerenciamento GP |
| **Microsoft Intune** | Dispositivos gerenciados na nuvem | Licenciamento Intune, Graph API |

## 🚀 Início Rápido

### Avaliação de Segurança
```powershell
# Carregue o módulo Ghost
Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1' -OutFile .\Ghost.ps1
Get-Content .\Ghost.ps1
. .\Ghost.ps1

# Verifique a postura de segurança atual
Get-Ghost
```

### Reforço Básico (Teste Primeiro)
```powershell
# Reforço essencial - teste primeiro em ambiente de laboratório
Set-Ghost -SMBv1 -AutoRun -Macros

# Revise as mudanças
Get-Ghost
```

### Implementação Empresarial
```powershell
# Implementação Group Policy (ambientes de domínio)
Set-Ghost -SMBv1 -AutoRun -GroupPolicy

# Implementação Intune (dispositivos gerenciados na nuvem)
Set-Ghost -SMBv1 -RDP -USBStorage -Intune
```

## 📋 Métodos de Instalação

### Opção 1: Download Direto (Teste)
```powershell
Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1' -OutFile .\Ghost.ps1
Get-Content .\Ghost.ps1
. .\Ghost.ps1
```

### Opção 2: Instalação de Módulo
```powershell
# Instale da PowerShell Gallery (quando disponível)
Install-Module Ghost -Scope CurrentUser
Import-Module Ghost
```

### Opção 3: Implementação Empresarial
```powershell
# Copie para localização de rede para implementação Group Policy
# Configure scripts PowerShell do Intune para implementação na nuvem
```

## 💼 Exemplos de Casos de Uso

### Pequenos Negócios
```powershell
# Proteção básica com impacto mínimo
Set-Ghost -SMBv1 -AutoRun -Macros -ICMP
```

### Ambiente de Saúde
```powershell
# Reforço focado em HIPAA
Set-Ghost -SMBv1 -RDP -USBStorage -AdminShares -Telemetry
```

### Serviços Financeiros
```powershell
# Configuração de alta segurança
Set-Ghost -RDP -SMBv1 -AutoRun -USBStorage -Macros -PSRemoting -AdminShares
```

### Organização Cloud-First
```powershell
# Implementação gerenciada pelo Intune
Connect-IntuneGhost -Interactive
Set-Ghost -SMBv1 -RDP -AutoRun -Macros -Intune
```

## 🔍 Detalhes das Funções

### Funções Principais de Reforço

#### Serviços de Rede
- **RDP**: Bloqueia acesso ao desktop remoto ou randomiza porta
- **SMBv1**: Desativa protocolo legado de compartilhamento de arquivos
- **ICMP**: Previne respostas ping para reconhecimento
- **LLMNR/NetBIOS**: Bloqueia protocolos legados de resolução de nomes

#### Segurança de Aplicações
- **Macros**: Desativa execução de macros em aplicações Office
- **AutoRun**: Previne execução automática de mídias removíveis

#### Gerenciamento Remoto
- **PSRemoting**: Desativa sessões remotas do PowerShell
- **WinRM**: Para o Windows Remote Management
- **Remote Assistance**: Bloqueia conexões de assistência remota

#### Controle de Acesso
- **Admin Shares**: Desativa compartilhamentos C$, ADMIN$
- **Guest Account**: Desativa acesso da conta de convidado
- **USB Storage**: Restringe uso de dispositivos USB

### Integração Azure
```powershell
# Conecte ao tenant Azure
Connect-AzureGhost -Interactive

# Habilite padrões de segurança
Set-AzureSecurityDefaults -Enable

# Configure acesso condicional
Set-AzureConditionalAccess -BlockLegacyAuth -RequireMFA

# Audite usuários privilegiados
Set-AzurePrivilegedUsers -AuditOnly
```

### Integração Intune (Novo no v2)
```powershell
# Conecte ao Intune
Connect-IntuneGhost -Interactive

# Implemente via políticas Intune
Set-IntuneGhost -Settings @{
    RDP = $true
    SMBv1 = $true
    USBStorage = $true
    Macros = $true
}
```

## ⚠️ Considerações Importantes

### Requisitos de Teste
- **Ambiente de Laboratório**: Teste primeiro todas as configurações em ambiente isolado
- **Implementação Gradual**: Implemente gradualmente para identificar problemas
- **Plano de Rollback**: Certifique-se de que pode reverter mudanças se necessário
- **Documentação**: Registre quais configurações funcionam para seu ambiente

### Impacto Potencial
- **Produtividade do Usuário**: Algumas configurações podem afetar fluxos de trabalho diários
- **Aplicações Legadas**: Sistemas mais antigos podem exigir protocolos específicos
- **Acesso Remoto**: Considere o impacto na administração remota legítima
- **Processos de Negócio**: Verifique se as configurações não quebram funções críticas

### Limitações de Segurança
- **Defesa em Profundidade**: Ghost é uma camada de segurança, não uma solução completa
- **Gerenciamento Contínuo**: Segurança requer monitoramento e atualizações contínuas
- **Treinamento de Usuário**: Controle técnico deve ser pareado com consciência de segurança
- **Evolução de Ameaças**: Novos métodos de ataque podem contornar proteções atuais

## 🎯 Exemplos de Cenários de Ataque

Embora o Ghost mire em vetores de ataque comuns, a prevenção específica depende de implementação e teste adequados:

### Ataques Estilo WannaCry
- **Mitigação**: `Set-Ghost -SMBv1` desativa o protocolo vulnerável
- **Considerações**: Certifique-se de que nenhum sistema legado requer SMBv1

### Ransomware Baseado em RDP
- **Mitigação**: `Set-Ghost -RDP` bloqueia acesso ao desktop remoto
- **Considerações**: Pode requerer métodos alternativos de acesso remoto

### Malware Baseado em Documentos
- **Mitigação**: `Set-Ghost -Macros` desativa execução de macros
- **Considerações**: Pode afetar documentos legítimos com macros habilitadas

### Ameaças Entregues via USB
- **Mitigação**: `Set-Ghost -USBStorage -AutoRun` restringe funcionalidade USB
- **Considerações**: Pode afetar uso legítimo de dispositivos USB

## 🏢 Recursos Empresariais

### Suporte Group Policy
```powershell
# Aplique configurações via registro Group Policy
Set-Ghost -SMBv1 -RDP -AutoRun -GroupPolicy

# Configurações se aplicam em todo o domínio após atualização GP
gpupdate /force
```

### Integração Microsoft Intune
```powershell
# Crie políticas Intune para configurações Ghost
Set-IntuneGhost -Settings $GhostSettings -Interactive

# Políticas são implementadas automaticamente em dispositivos gerenciados
```

### Relatórios de Conformidade
```powershell
# Gere relatório de avaliação de segurança
Get-Ghost | Export-Csv -Path "SecurityAudit-$(Get-Date -Format 'yyyy-MM-dd').csv"

# Relatório de postura de segurança Azure
Get-AzureGhost | Out-File "AzureSecurityReport.txt"
```

## 📚 Melhores Práticas

### Antes da Implementação
1. **Documente o Estado Atual**: Execute `Get-Ghost` antes das mudanças
2. **Teste Cuidadosamente**: Valide em ambiente não-produtivo
3. **Planeje Rollback**: Saiba como reverter cada configuração
4. **Revisão das Partes Interessadas**: Certifique-se de que unidades de negócio aprovem mudanças

### Durante a Implementação
1. **Abordagem Gradual**: Implemente primeiro em grupos piloto
2. **Monitore Impacto**: Observe reclamações de usuários ou problemas de sistema
3. **Documente Problemas**: Registre quaisquer problemas para referência futura
4. **Comunique Mudanças**: Informe usuários sobre melhorias de segurança

### Após Implementação
1. **Avaliação Regular**: Execute periodicamente `Get-Ghost` para verificar configurações
2. **Atualize Documentação**: Mantenha configurações de segurança atuais
3. **Revise Efetividade**: Monitore incidentes de segurança
4. **Melhoria Contínua**: Ajuste configurações baseado no panorama de ameaças

## 🔧 Solução de Problemas

### Problemas Comuns
- **Erros de Permissão**: Certifique-se de sessão PowerShell elevada
- **Dependências de Serviço**: Alguns serviços podem ter dependências
- **Compatibilidade de Aplicação**: Teste com aplicações de negócio
- **Conectividade de Rede**: Verifique se acesso remoto ainda funciona

### Opções de Recuperação
```powershell
# Reabilite serviços específicos se necessário
Set-RDP -Enable
Set-SMBv1 -Enable
Set-AutoRun -Enable
Set-Macros -Enable
```

## 👨‍💻 Sobre o Autor

**Jim Tyler** - Microsoft MVP para PowerShell
- **YouTube**: [@PowerShellEngineer](https://youtube.com/@PowerShellEngineer) (10,000+ inscritos)
- **Newsletter**: [PowerShell.News](https://powershell.news) - Inteligência de segurança semanal
- **Autor**: "PowerShell for Systems Engineers"
- **Experiência**: Décadas de automação PowerShell e segurança Windows

## 📄 Licença e Isenção de Responsabilidade

### Licença MIT
Ghost é fornecido sob a Licença MIT para uso, modificação e distribuição gratuitos.

### Isenção de Responsabilidade de Segurança
- **Nenhuma Garantia**: Ghost é fornecido "como está" sem garantia de qualquer tipo
- **Teste Obrigatório**: Sempre teste em ambientes não-produtivos primeiro
- **Orientação Profissional**: Consulte profissionais de segurança para implementações de produção
- **Impacto Operacional**: Os autores não são responsáveis por qualquer interrupção operacional
- **Segurança Abrangente**: Ghost é um componente numa estratégia de segurança completa

### Suporte
- **GitHub Issues**: [Reporte bugs ou solicite recursos](https://github.com/jimrtyler/Ghost/issues)
- **Documentação**: Use `Get-Help <function> -Full` para ajuda detalhada
- **Comunidade**: Fóruns da comunidade PowerShell e segurança

---

**🔒 Fortaleça sua postura de segurança com Ghost - mas sempre teste primeiro.**

```powershell
# Comece com avaliação, não suposições
Get-Ghost
```

**⭐ Dê uma estrela a este repositório se Ghost ajuda a melhorar sua postura de segurança!**