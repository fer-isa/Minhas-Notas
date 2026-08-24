# 🧪 Laboratório: Configuração de Servidor DHCP no Roteador
**Formação Mulher Digital • Cisco Packet Tracer**

</div>

---

## 📌 1. Objetivo da Atividade
Configurar um roteador Cisco para atuar como **Servidor DHCP**, distribuindo de forma automatizada parâmetros de rede fundamentais (**Endereço IP**, **Máscara de Sub-rede**, **Gateway Padrão** e **Servidor DNS**) para os computadores da rede local (LAN).

---

## 🏗️ 2. Topologia & Montagem Física

### **Equipamentos Utilizados**
- **Roteador:** Cisco 2911  
- **Switch:** Cisco Catalyst 2960  
- **Hosts:** 2 PCs genéricos (`PC0` e `PC1`)  
- **Cabos:** Copper Straight-Through  

### **Mapeamento de Conexões**

| Origem | Interface | Destino | Interface |
|:---|:---|:---|:---|
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

```

### **B. Configuração do Pool DHCP**

```bash
Router(config)# ip dhcp excluded-address 192.168.1.1
Router(config)# ip dhcp pool REDE_LOCAL
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# exit
Router# write memory

```

---

## ✅ 4. Validação & Teste de Conectividade

1. Abra o **PC0** → **Desktop** → **IP Configuration**.
2. Altere de **Static** para **DHCP**.
3. O protocolo DORA será executado e o host receberá automaticamente os parâmetros:

```text
IP Address:      192.168.1.2
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.1.1
DNS Server:      8.8.8.8

```

4. Repita o processo no **PC1**, que deverá receber o IP `192.168.1.3`.

---

## ⚠️ 5. Troubleshooting (Caso Algo Não Funcione)

* **Lease não atualizado:** No PC → **Config** → altere Gateway/DNS para **DHCP / Automático**, volte em **Desktop** → **IP Configuration** e marque **DHCP** novamente.
* **Portas inativas:** Verifique se as luzes das portas estão verdes no Packet Tracer.
* **Interface desligada:** Confirme se aplicou o comando `no shutdown` na interface `GigabitEthernet0/0` do roteador.

---
## 📥 6. Arquivos do Laboratório

[![Download PKT](https://img.shields.io/badge/Download-Laborat%C3%B3rio_.PKT-007ACC?style=for-the-badge&logo=cisco&logoColor=white)](https://github.com/fer-isa/Minhas-Notas/blob/main/Laboratorios/Mulher-Digital/02-Configuracao-Servidor-DHCP-Roteador/lab-dhcp-router-cisco.pkt)

> 📄 **Link do arquivo:** [Acessar lab-dhcp-router-cisco.pkt](https://github.com/fer-isa/Minhas-Notas/blob/main/Laboratorios/Mulher-Digital/02-Configuracao-Servidor-DHCP-Roteador/lab-dhcp-router-cisco.pkt)
>
> > 💡 **Como baixar:**  
> 1. Clique no botão acima para abrir a página do arquivo.  
> 2. Na barra superior direita do GitHub, clique no **ícone de Download** (seta para baixo ⬇️) ao lado do botão *Raw*.
```

4. Clique no botão verde **Commit changes...** no canto superior direito para salvar.

```
