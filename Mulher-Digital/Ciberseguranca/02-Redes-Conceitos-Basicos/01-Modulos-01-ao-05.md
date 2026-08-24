<div align="center">
  <img src="../../assets/introduction-to-cybersecurity.png" width="180">
</div>

# 🌐 Conceitos Básicos de Redes — Módulos 1 ao 5
**Formação Mulher Digital • Trilha de Cibersegurança**

---

## 📌 Visão Geral
Este documento consolida os conceitos fundamentais de redes dos **Módulos 1 ao 5**, cobrindo desde a taxonomia de rede e dispositivos até os modelos conceituais de comunicação e meios físicos.

---

## 🏗️ Módulo 1: Fundamentos e Tipos de Rede

* **Definição de Rede:** Conjunto mundial de redes interconectadas que operam sob padrões comuns para troca de dados.
* **Classificação por Escopo:**
  * **Rede Doméstica:** Conexão simples de dispositivos locais centralizados por um roteador Wi-Fi integrado.
  * **SOHO (Small Office / Home Office):** Estrutura voltada a pequenos escritórios/trabalho remoto.
  * **Média / Grande Empresa:** Infraestrutura segmentada com switches dedicados, firewalls e roteamento avançado.

### 📊 Unidades de Medida

| Unidade | Símbolo | Definição | Aplicação Principal |
| :--- | :---: | :--- | :--- |
| **Bit** | `b` | Menor unidade de informação (0 ou 1). | Velocidade / Largura de Banda (ex: Mbps, Gbps). |
| **Byte** | `B` | Conjunto de 8 bits (representa 1 caractere). | Tamanho de Arquivos / Armazenamento (ex: MB, GB). |

---

## 🖥️ Módulo 2: Arquitetura e Classificação

### Modelos de Comunicação
* **Cliente-Servidor:** O *Cliente* solicita serviços/dados e o *Servidor* processa e responde (Web, Arquivos, Banco de Dados).
* **Ponto a Ponto (P2P):** Todos os dispositivos atuam simultaneamente como clientes e servidores, sem dependência de um nó central.

### Dispositivos da Rede
* **Dispositivos Finais (Hosts):** Pontos de origem ou destino da mensagem (computadores, servidores, smartphones, impressoras).
* **Dispositivos Intermediários:** Equipamentos que gerenciam o fluxo, direcionam dados e garantem a conectividade (roteadores, switches, firewalls).

### Classificação Geográfica

| Tipo | Nome Completo | Escopo / Alcance |
| :--- | :--- | :--- |
| **PAN** | *Personal Area Network* | Dispositivos pessoais de curto alcance (Bluetooth, smartwatch). |
| **LAN** | *Local Area Network* | Área local limitada (residência, laboratório, prédio). |
| **MAN** | *Metropolitan Area Network* | Cobertura em nível de cidade ou região metropolitana. |
| **WAN** | *Wide Area Network* | Longas distâncias geográficas, conectando países e continentes (Internet). |

---

## 📡 Módulo 3: Meios de Transmissão & Redes Sem Fio

* **Redes Sem Fio (Wireless):** Transmissão de dados via ondas de radiofrequência, garantindo mobilidade aos dispositivos clientes.
* **Meios Físicos Cabeados:**
  * **Par Trançado (UTP/STP):** Cabos de cobre amplamente usados em LANs corporativas.
  * **Fibra Óptica:** Transmissão via pulsos de luz para longas distâncias e altíssimas taxas de transferência.

---

## 📐 Módulo 4 & 5: Modelos em Camadas e Protocolos

Os **protocolos** estabelecem as regras para que dispositivos distintos consigam padronizar a transmissão e recepção de pacotes.

### Comparativo: Modelo OSI vs. Modelo TCP/IP

| Camada OSI (7 Camadas) | Camada TCP/IP (4 Camadas) | Exemplos de Protocolos / PDU |
| :--- | :--- | :--- |
| **7. Aplicação** | rowspan=3 **Aplicação** | HTTP, HTTPS, DNS, DHCP, SSH, FTP |
| **6. Apresentação** | | SSL/TLS, JPEG, ASCII |
| **5. Sessão** | | NetBIOS, RPC |
| **4. Transporte** | **Transporte** | TCP (Orientado à conexão), UDP (Sem conexão) |
| **3. Rede** | **Internet** | IPv4, IPv6, ICMP, ARP |
| **2. Enlace** | rowspan=2 **Acesso à Rede** | Ethernet, Wi-Fi (802.11), Switch L2 |
| **1. Física** | | Cabos UTP, Fibra Óptica, Sinais Elétricos |
