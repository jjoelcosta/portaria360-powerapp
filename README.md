# portaria360-powerapp
Sistema de controle de acesso com Power Apps
# 🚪 Portaria360 - Sistema de Controle de Acesso

Sistema desenvolvido em **Power Apps** para controle de entrada/saída de pessoas e veículos em arena esportiva.

## 🎯 Funcionalidades

- ✅ Busca por CPF, Placa ou Nome (normalização automática)
- ✅ Validação de acessos liberados por data
- ✅ Registro de entrada/saída com catraca/cabide
- ✅ Controle de permissões (portaria vs administração)
- ✅ Preenchimento automático de cor/setor por local

## 🏗️ Arquitetura

### Tecnologias
- **Power Apps** (Canvas App)
- **Dataverse** (banco de dados)
- **Power Automate** (automações)

### Tabelas Principais
1. **Pessoas Autorizadas** - cadastro de autorizados
2. **Solicitações Portaria360** - pedidos de acesso
3. **Controle_Acesso** - registro de entradas/saídas
4. **Locais Arena** - cadastro de locais

## 📱 Telas

### TelaBusca
Busca inteligente com normalização: 
- Remove `.`, `-`, espaços
- Case-insensitive
- Filtra por status e datas

```powerapps
// Exemplo de fórmula (simplificada)
Filter(
    'Pessoas Autorizadas';
    'Status Acesso' = LIBERADO &&
    StartsWith(CPF; TextoNormalizado)
)
```

### TelaDetalhes
- Exibição de dados da pessoa
- Registro de entrada/saída
- Controle de cabide/catraca

## 🔐 Segurança

Controle de acesso por email:
- **Portaria**: acesso somente a busca e registro
- **Administração**: acesso completo

```powerapps
// Bloqueio de telas
If(
    Lower(User().Email) = "portarias. arena@arenabsb.com. br";
    Navigate(TelaBusca);
    Notify("Acesso restrito")
)
```

## 🤖 Automações

### Flow: Preencher Cor e Setor
Quando `Local Autorizado` é escolhido:
1. Busca dados em `Locais Arena`
2. Preenche `Cor` e `Setor` automaticamente

## 📊 Modelo de Dados

Ver:  [docs/modelo-dados.md](docs/modelo-dados.md)

## 🚀 Como Implementar

1. Importar tabelas no Dataverse
2. Importar fluxos no Power Automate
3. Criar app no Power Apps
4. Aplicar fórmulas das telas
5. Configurar permissões

## 📸 Screenshots

![Tela de Busca](docs/screenshots/tela-busca.png)
![Tela de Detalhes](docs/screenshots/tela-detalhes.png)

## 📄 Licença

MIT License - veja [LICENSE](LICENSE)

## 👤 Autor

Joel Costa (@jjoelcosta)

## 🤝 Contribuições

Contribuições são bem-vindas! Abra uma issue ou PR. 

---

**Nota**:  Este é um projeto educacional/demonstrativo. 
Dados sensíveis foram removidos. 
