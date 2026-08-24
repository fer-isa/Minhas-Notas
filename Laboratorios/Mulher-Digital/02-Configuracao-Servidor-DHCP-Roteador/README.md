Entendi perfeitamente. O bloco de código (`bash`) não estava sendo fechado antes dos tópicos seguintes, fazendo com que todo o texto até o final ficasse preso dentro da caixa escura de terminal.

Aqui está o trecho da seção 3 até a 6 com os blocos devidamente fechados para que as seções 4, 5 e 6 (o download) fiquem 100% normais e fora de blocos de código:

```markdown
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

> 📄 **Link direto:** [Clique aqui para baixar lab-dhcp-router-cisco.pkt](https://www.google.com/search?q=./lab-dhcp-router-cisco.pkt%3Fraw%3Dtrue)

```

```
