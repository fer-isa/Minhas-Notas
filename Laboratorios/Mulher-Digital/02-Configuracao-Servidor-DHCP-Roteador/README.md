<div align="center">

# 🧪 Laboratório: Configuração de Servidor DHCP no Roteador  
**Formação Mulher Digital • Cisco Packet Tracer**

</div>

---

## 📌 1. Objetivo da Atividade
Implementar um **Servidor DHCP** em um roteador Cisco, permitindo a distribuição automática dos parâmetros de rede para hosts da LAN:

- Endereço IP  
- Máscara de Sub-rede  
- Gateway Padrão  
- Servidor DNS  

---

## 🏗️ 2. Topologia & Montagem Física

### **Equipamentos Utilizados**
- **Roteador:** Cisco 2911  
- **Switch:** Cisco Catalyst 2960  
- **Hosts:** 2 PCs genéricos (`PC0` e `PC1`)  
- **Cabos:** Copper Straight-Through  

### **Mapeamento de Conexões**

| Origem | Interface | Destino | Interface |
|-------|-----------|---------|-----------|
| PC0 | FastEthernet0 | Switch 2960 | FastEthernet0/1 |
| PC1 | FastEthernet0 | Switch 2960 | FastEthernet0/2 |
| Switch 2960 | FastEthernet0/24 | Roteador 2911 | GigabitEthernet0/0 |

> ℹ️ **Nota:** PCs utilizam portas *FastEthernet (100 Mbps)*, enquanto o roteador Cisco 2911 opera com *GigabitEthernet (1 Gbps)*.

---

## 💻 3. Configuração no Roteador (CLI)

Acesse o CLI do roteador, recuse o assistente inicial (`no`) e aplique:

### **A. Configuração da Interface e Gateway**
```bash
Router> enable
Router# configure terminal
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
✅ 4. Validação & Teste de Conectividade
Abra o PC0 → Desktop → IP Configuration

Altere de Static para DHCP

O protocolo DORA será executado e o host receberá automaticamente:

Código
IP Address:      192.168.1.2
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.1.1
DNS Server:      8.8.8.8
Repita o processo no PC1, que deverá receber o IP 192.168.1.3.

⚠️ 5. Troubleshooting (Caso Algo Não Funcione)
Se o Packet Tracer não atualizar o leasing DHCP:

PC0 → Config → altere Gateway/DNS para DHCP / Automático

Volte em Desktop → IP Configuration → selecione novamente DHCP

Verifique se todos os links estão verdes (ativos)

Confirme que a interface do roteador está com no shutdown

## 📥 6. Arquivos do Laboratório

[![Download PKT](https://img.shields.io/badge/Download-Laboratório_.PKT-007ACC?style=for-the-badge&logo=cisco&logoColor=white)](./lab-dhcp-router-cisco.pkt?raw=true)

> 📄 **Link alternativo:** [Clique aqui para baixar lab-dhcp-router-cisco.pkt](./lab-dhcp-router-cisco.pkt?raw=true)
