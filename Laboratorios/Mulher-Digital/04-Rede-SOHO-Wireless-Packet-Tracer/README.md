Aqui está o `README.md` completo para este novo laboratório, seguindo exatamente o mesmo padrão visual, badges e estrutura limpa:

**Nome sugerido para a nova pasta:** `04-Rede-SOHO-Wireless-Packet-Tracer`

---

```markdown
<div align="center">

# 🏢 Laboratório: Infraestrutura de Rede para Pequeno Escritório (SOHO)

![Cisco](https://img.shields.io/badge/Cisco-Packet_Tracer-1BA0D7?style=flat-square&logo=cisco&logoColor=white)
![Topologia](https://img.shields.io/badge/Topologia-SOHO_/_Wi--Fi-007ACC?style=flat-square)
![Formação](https://img.shields.io/badge/Mulher_Digital-Redes-8A2BE2?style=flat-square)
![Status](https://img.shields.io/badge/Status-Concluído-success?style=flat-square)

<p>Planejamento, montagem física, segurança de rede sem fio (WPA2-PSK) e distribuição dinâmica de IP (DHCP) em ambiente corporativo de pequeno porte.</p>

</div>

---

## 📌 1. Objetivo da Atividade

Montar uma topologia de rede completa para um pequeno escritório (**SOHO - Small Office / Home Office**), integrando dispositivos cabeados e sem fio através de um roteador wireless multifuncional (**WRT300N**)[cite: 1]. Configurar segurança de rede sem fio (**WPA2-Personal**), verificar a concessão automática de endereços IP via **DHCP** e validar a comunicação local por meio de testes de conectividade (**ICMP Ping**)[cite: 1].

---

## 🏗️ 2. Topologia & Montagem Física

### **Equipamentos Utilizados**

* **Roteador Multifuncional:** Linksys WRT300N (Switch, AP Wi-Fi e Servidor DHCP)[cite: 1]
* **Dispositivos Cabeados:** 2 PCs genéricos (`PC0` e `PC1`) e 1 Impressora de Rede (`Printer0`)[cite: 1]
* **Dispositivos Sem Fio:** 1 Notebook (`Laptop0` com módulo `WPC300N`) e 1 Smartphone (`Smartphone0`)[cite: 1]
* **Infraestrutura WAN:** Nuvem (`Cloud-PT`) e Modem Banda Larga (`Cable Modem`)[cite: 1]
* **Cabeamento:** Cabos Diretos (Copper Straight-Through) e Cabo Coaxial[cite: 1]

### **Mapeamento de Conexões**

| Origem | Interface | Destino | Interface | Tipo de Cabo |
| :--- | :--- | :--- | :--- | :--- |
| **Cloud-PT** | Coaxial 7 | Cable Modem | Port 0 | Cabo Coaxial[cite: 1] |
| **Cable Modem** | Port 1 | Roteador WRT300N | Internet | Cabo Direto[cite: 1] |
| **PC0** | FastEthernet0 | Roteador WRT300N | Ethernet 1 | Cabo Direto[cite: 1] |
| **PC1** | FastEthernet0 | Roteador WRT300N | Ethernet 2 | Cabo Direto[cite: 1] |
| **Printer0** | FastEthernet0 | Roteador WRT300N | Ethernet 3 | Cabo Direto[cite: 1] |
| **Laptop0** | Wireless (WPC300N) | Roteador WRT300N | Wi-Fi (SSID) | Sem Fio[cite: 1] |
| **Smartphone0** | Wireless0 | Roteador WRT300N | Wi-Fi (SSID) | Sem Fio[cite: 1] |

---

## 🔐 3. Configuração da Rede Sem Fio (Wi-Fi)

Acesse **WRT300N** → aba **GUI**:

### **A. Definição do SSID**
1. Acesse o menu **Wireless**[cite: 1].
2. No campo **Network Name (SSID)**, altere de `Default` para `Escritorio_Firma`[cite: 1].
3. Role até o final da página e clique em **Save Settings**[cite: 1].

### **B. Segurança e Criptografia**
1. Acesse o submenu **Wireless Security**[cite: 1].
2. Selecione **Security Mode:** `WPA2 Personal`[cite: 1].
3. Defina a **Passphrase:** `senha12345`[cite: 1].
4. Clique em **Save Settings**[cite: 1].

---

## 📱 4. Conexão e Adaptação dos Dispositivos Sem Fio

### **A. Smartphone**
1. Acesse **Smart Phone** → aba **Config** → **Wireless0**[cite: 1].
2. Defina o **SSID:** `Escritorio_Firma`[cite: 1].
3. Em **Authentication**, marque `WPA2-PSK` e insira a chave: `senha12345`[cite: 1].

### **B. Notebook (Laptop)**
1. Acesse **Laptop** → aba **Physical**, desligue o botão de energia e remova o módulo cabeado[cite: 1].
2. Insira a placa wireless **`WPC300N`** no compartimento e ligue o notebook novamente[cite: 1].
3. Vá em **Desktop** → aplicativo **PC Wireless** → aba **Connect** → clique em **Refresh**[cite: 1].
4. Selecione a rede `Escritorio_Firma`, clique em **Connect** e autentique com a chave `senha12345`[cite: 1].

---

## ⚙️ 5. Endereçamento Dinâmico (DHCP)

Todos os dispositivos foram configurados para receber endereçamento dinâmico distribuído pelo pool do WRT300N (faixa `192.168.0.X/24`)[cite: 1]:

* **PCs (`PC0` e `PC1`):** **Desktop** → **IP Configuration** → alterado para `DHCP`[cite: 1].
* **Impressora (`Printer0`):** **Config** → **FastEthernet0** → alterado para `DHCP`[cite: 1].
* **Dispositivos Wi-Fi:** Concessão automática obtida logo após a autenticação na rede[cite: 1].

---

## 🔍 6. Validação e Teste de Conectividade

No terminal de comandos do **PC0** (**Desktop** → **Command Prompt**):

### **Verificação dos Parâmetros Locais**
```bash
ipconfig /all

```

### **Teste de Conectividade com a Impressora**

```bash
ping 192.168.0.102

```

> *(Substitua o IP pelo endereço atribuído à sua impressora via DHCP)*.
> 
> 
> **Resultado:** 4 pacotes transmitidos e recebidos com sucesso (0% de perda).
> 
> 

---

## 📥 7. Arquivos do Laboratório

* 📄 **Link do arquivo:** [Acessar lab-rede-soho-wireless.pkt](https://www.google.com/search?q=lab-rede-soho-wireless.pkt)

> 💡 **Como baixar:**
> 1. Clique no botão azul **DOWNLOAD LABORATÓRIO .PKT** acima para abrir o arquivo no GitHub.
> 2. No canto superior direito, clique no **ícone de Download** (seta para baixo ⬇️) ao lado do botão *Raw*.
> 
> 

```

```
