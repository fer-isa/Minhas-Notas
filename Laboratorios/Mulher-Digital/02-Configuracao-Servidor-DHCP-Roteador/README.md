<div align="center">

# 🧪 Laboratório: Configuração de Servidor DHCP no Roteador
**Formação Mulher Digital • Cisco Packet Tracer**

</div>

---

## 📌 1. Objetivo da Atividade
Configurar um roteador Cisco para atuar como **Servidor DHCP**, distribuindo de forma automatizada parâmetros de rede fundamentais (**Endereço IP**, **Máscara de Sub-rede**, **Gateway Padrão** e **Servidor DNS**) para os computadores da rede local (LAN).

---

## 🏗️ 2. Topologia & Montagem Física

### Equipamentos Utilizados
* **1x Roteador:** Cisco 2911 (*Network Devices > Routers*)
* **1x Switch:** Cisco Catalyst 2960 (*Network Devices > Switches*)
* **2x Hosts Finais:** PCs Genéricos (`PC0` e `PC1`) (*End Devices > End Devices*)
* **Meio Físico:** Cabos de Cobre Direto (*Copper Straight-Through*)

### Mapeamento de Conexões e Portas

| Dispositivo Origem | Interface de Saída | Dispositivo Destino | Interface de Entrada |
| :--- | :--- | :--- | :--- |
| **PC0** | FastEthernet0 | **Switch 2960** | FastEthernet0/1 |
| **PC1** | FastEthernet0 | **Switch 2960** | FastEthernet0/2 |
| **Switch 2960** | FastEthernet0/24 | **Roteador 2911** | GigabitEthernet0/0 |

> ℹ️ **Nota sobre Interfaces:** Dispositivos finais utilizam portas *FastEthernet* (100 Mbps), enquanto o roteador Cisco 2911 opera nativamente com interfaces de alta velocidade *GigabitEthernet* (1 Gbps).

---

## 💻 3. Configuração no Roteador (CLI)

Ao iniciar a interface CLI do roteador e recusar o assistente inicial (`no`), aplique os seguintes comandos:

### A. Ativação da Interface e Gateway Padrão
```bash
Router> enable
Router# configure terminal
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
. Criação e Configuração do Pool DHCPBashRouter(config)# ip dhcp pool MULHER_DIGITAL2026
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# exit
Router(config)# exit
Router# write

---

✅ 4. Validação & Teste de ConectividadeClique no PC0 e navegue até a aba Desktop $\to$ IP Configuration.Alterne de Static para DHCP.Em poucos segundos, o protocolo DORA é concluído e o host recebe automaticamente:IP Address: 192.168.1.2Subnet Mask: 255.255.255.0Default Gateway: 192.168.1.1DNS Server: 8.8.8.8Repita o teste no PC1 para validar a entrega sequencial do IP 192.168.1.3.⚠️ 5. Troubleshooting (Resolução de Problemas no Simulador)Caso o Packet Tracer não atualize o leasing DHCP na interface gráfica:Acesse o PC0 $\to$ aba Config.Altere o campo Gateway/DNS para a opção DHCP / Automático.Retorne à aba Desktop $\to$ IP Configuration e repita a alternância para DHCP.Valide se todas as portas e links estão sinalizados com triângulos verdes ativos.📥 Arquivos do Laboratório💾 [📥 **Download do laboratório:**  
[lab-dhcp-router-cisco.pkt](./lab-dhcp-router-cisco.pkt)

---

**Passo 3: Salvar**

1. Clique no botão verde **Commit changes...** no topo.
2. Confirme clicando em **Commit changes**.

Assim que salvar este README, já podemos subir o arquivo `.pkt` para essa mesma pasta!
