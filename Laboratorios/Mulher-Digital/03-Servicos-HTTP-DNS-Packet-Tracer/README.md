<div align="center">

# 🌐 Laboratório: Serviços de Aplicação (HTTP & DNS) e Camada de Transporte
**Formação Mulher Digital • Cisco Packet Tracer**

</div>

---

## 📌 1. Objetivo da Atividade
Construir uma topologia de rede local (LAN), configurar serviços da camada de aplicação (**HTTP** e **DNS**) em um servidor dedicado e validar o fluxo de comunicação e encapsulamento de pacotes (**Camadas 4 e 7 do Modelo OSI**) utilizando o modo de simulação.

---

## 🏗️ 2. Topologia & Montagem Física

### **Equipamentos Utilizados**
- **Switch:** Cisco Catalyst 2960 (1 unidade)
- **Host:** PC genérico (`PC-Cliente`)
- **Servidor:** Servidor genérico (`Servidor-Central`)
- **Cabos:** Copper Straight-Through (Cabo Direto)

### **Mapeamento de Conexões**

| Origem | Interface | Destino | Interface |
|:---|:---|:---|:---|
| PC-Cliente | FastEthernet0 | Switch 2960 | FastEthernet0/1 |
| Servidor-Central | FastEthernet0 | Switch 2960 | FastEthernet0/2 |

---

## ⚙️ 3. Endereçamento IP

Configuração estática dos parâmetros de rede aplicada na aba **Desktop** → **IP Configuration**:

| Dispositivo | Endereço IP | Máscara de Sub-rede | Gateway Padrão | Servidor DNS |
|:---|:---|:---|:---|:---|
| **Servidor-Central** | `192.168.1.10` | `255.255.255.0` | — | — |
| **PC-Cliente** | `192.168.1.5` | `255.255.255.0` | — | `192.168.1.10` |

---

## 🛠️ 4. Configuração dos Serviços (Servidor-Central)

Acesse **Servidor-Central** → aba **Services**:

### **A. Servidor Web (HTTP / HTTPS)**
1. Acesse o menu **HTTP** e certifique-se de que as opções **HTTP** e **HTTPS** estejam em `On`.
2. No arquivo `index.html`, clique em **Edit** e personalize a página inicial:
   - Título: `Bem-vinda à aula de Redes!`
   - Mensagem: `Esta é a nossa primeira página web configurada e testada no laboratório!`
3. Clique em **Save**.

### **B. Servidor de Resolução de Nomes (DNS)**
1. Acesse o menu **DNS** e mude o status para `On`.
2. Preencha os campos para adicionar o registro:
   - **Name:** `www.aula.com`
   - **Type:** `A Record`
   - **Address:** `192.168.1.10`
3. Clique em **Add**.

---

## 🔍 5. Validação com Utilitários de Rede

No **PC-Cliente** → **Desktop** → **Command Prompt**:

### **Teste 1: Conectividade Básica (ICMP)**
```bash
ping 192.168.1.10
