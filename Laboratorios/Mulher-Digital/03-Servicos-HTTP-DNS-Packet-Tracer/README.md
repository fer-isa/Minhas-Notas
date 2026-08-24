<div align="center">

# 🌐 Laboratório 2: Serviços HTTP & DNS

![Cisco](https://img.shields.io/badge/Cisco-Packet_Tracer-1BA0D7?style=flat-square&logo=cisco&logoColor=white)
![Status](https://img.shields.io/badge/Status-Concluído-success?style=flat-square)
![Trilha](https://img.shields.io/badge/Mulher_Digital-Redes-8A2BE2?style=flat-square)

<p>Configuração de serviços de aplicação e análise de protocolos nas camadas 4 e 7 do Modelo OSI.</p>

</div>

---
---

## 📌 1. Objetivo da Atividade

Configurar uma rede local com serviços da camada de aplicação (**HTTP** e **DNS**) em um servidor dedicado e validar a comunicação e encapsulamento de pacotes (**Camadas 4 e 7 do Modelo OSI**) utilizando utilitários de rede e o modo de simulação.

---

## 🏗️ 2. Topologia & Montagem Física

### **Equipamentos Utilizados**

* **Switch:** Cisco Catalyst 2960 (1 unidade)
* **Host:** PC genérico (`PC-Cliente`)
* **Servidor:** Servidor genérico (`Servidor-Central`)
* **Cabos:** Copper Straight-Through (Cabo Direto)

### **Mapeamento de Conexões**

| Origem | Interface | Destino | Interface |
| --- | --- | --- | --- |
| **PC-Cliente** | FastEthernet0 | Switch 2960 | FastEthernet0/1 |
| **Servidor-Central** | FastEthernet0 | Switch 2960 | FastEthernet0/2 |

---

## ⚙️ 3. Endereçamento IP

Configurações estáticas aplicadas na aba **Desktop** → **IP Configuration**:

| Dispositivo | Endereço IP | Máscara de Sub-rede | Gateway Padrão | Servidor DNS |
| --- | --- | --- | --- | --- |
| **Servidor-Central** | `192.168.1.10` | `255.255.255.0` | — | — |
| **PC-Cliente** | `192.168.1.5` | `255.255.255.0` | — | `192.168.1.10` |

---

## 🛠️ 4. Configuração dos Serviços (Servidor-Central)

Acesse **Servidor-Central** → aba **Services**:

### **A. Servidor Web (HTTP / HTTPS)**

1. Acesse o menu **HTTP** e certifique-se de que os serviços **HTTP** e **HTTPS** estão em `On`.
2. No arquivo `index.html`, clique em **Edit** e personalize a página:
* Altere o título para: `Bem-vinda à aula de Redes!`
* Altere o texto após `<hr>` para: `Esta é a nossa primeira página web configurada e testada no laboratório!`


3. Clique em **Save**.

### **B. Servidor de Nomes (DNS)**

1. Acesse o menu **DNS** e ligue o serviço (`On`).
2. Cadastre o registro preenchendo os campos:
* **Name:** `[www.aula.com](https://www.aula.com)`
* **Type:** `A Record`
* **Address:** `192.168.1.10`


3. Clique em **Add**.

---

## 🔍 5. Validação com Utilitários de Rede

No **PC-Cliente** → aba **Desktop** → **Command Prompt**:

### **Teste 1: Conectividade Básica (Ping)**

```bash
ping 192.168.1.10

```

### **Teste 2: Resolução de DNS (nslookup)**

```bash
nslookup www.aula.com

```

---

## 🔬 6. Análise de Protocolos (Modo Simulação)

1. No canto inferior direito, alterne de **Realtime** para **Simulation**.
2. Clique em **Show All/None** e depois em **Edit Filters**.
3. Marque apenas as caixas: **DNS**, **TCP**, **HTTP** e **ICMP**.
4. No **PC-Cliente**, abra o **Web Browser**, digite `[www.aula.com](https://www.aula.com)` e clique em **Go**.
5. Clique no botão **Play** ou avance com **Capture/Forward** para acompanhar o fluxo das PDUs.

---

## 📥 7. Arquivos do Laboratório

* 📄 **Link do arquivo:** [Acessar lab-servicos-http-dns.pkt](https://www.google.com/search?q=lab-servicos-http-dns.pkt)

> 💡 **Como baixar:**
> 1. Clique no botão azul **DOWNLOAD LABORATÓRIO .PKT** acima para abrir a página do arquivo.
> 2. Na barra superior direita do GitHub, clique no **ícone de Download** (seta para baixo ⬇️) ao lado do botão *Raw*.
> 
>
