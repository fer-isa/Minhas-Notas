# 🌐 Conceitos Básicos de Redes — Módulos 10 ao 15
**Formação Mulher Digital • Trilha de Cibersegurança**

---

## 📌 Visão Geral
Este documento consolida o fechamento da trilha de redes, abrangendo a arquitetura de endereçamento IP (IPv4 e IPv6), mecanismos de roteamento entre redes distintas e os protocolos essenciais de infraestrutura (**DHCP**, **DNS** e **ARP**).

---

## 🔢 Endereçamento IP e Máscaras de Sub-rede

* **Estrutura do Endereço IP:** Composto pela identificação de rede (*Network ID*) e identificação do nó final (*Host ID*).
* **Máscara de Sub-rede:** Sequência de 32 bits que delimita a fronteira entre rede e host. Representada também pela notação **CIDR** (ex: `/24` = `255.255.255.0`).

### Comparativo: IPv4 vs. IPv6

| Característica | IPv4 | IPv6 |
| :--- | :--- | :--- |
| **Tamanho** | 32 bits (4 octetos) | 128 bits (8 hextetos) |
| **Notação** | Decimal pontuado (ex: `192.168.1.50`) | Hexadecimal (ex: `2001:0db8::1`) |
| **Capacidade** | ~4,3 bilhões de endereços | 340 undecilhões de endereços |
| **Dependência de NAT** | Alta (para contornar escassez) | Desnecessário (conectividade fim a fim) |

---

## 🌍 IPs Públicos, Privados e Escopo IPv6

### No IPv4
* **IPs Públicos:** Endereços globais únicos e roteáveis na Internet, atribuídos por provedores (ISPs).
* **IPs Privados:** Endereços reservados para tráfego em rede local (RFC 1918: `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`).
* **NAT (*Network Address Translation*):** Traduz múltiplos endereços privados em um único IP público de saída.

### No IPv6
* **GUA (*Global Unicast Address*):** Equivalente ao IP público, roteável na Internet (inicia geralmente com `2000::/3`).
* **ULA (*Unique Local Address*):** Equivalente ao IP privado local, não roteável na Internet (inicia com `fc00::/7` ou `fd00::/8`).

---

## 🛠️ Protocolos de Infraestrutura e Descoberta

| Protocolo | Camada OSI | Função Operacional | Mecânica de Funcionamento |
| :--- | :---: | :--- | :--- |
| **DHCP** | Aplicação (L7) | Atribuição dinâmica de configurações de rede | Processo **DORA** (*Discover, Offer, Request, Acknowledge*). |
| **DNS** | Aplicação (L7) | Resolução de nomes para endereços IP | Consulta hierárquica distribuída (ex: `site.com` $\to$ IP). |
| **ARP** | Enlace / Rede (L2/L3) | Descoberta de endereço MAC a partir do IP | Envio de broadcast local e resposta unicast com o MAC destino. |

---

## 🛣️ Modos de Transmissão & Roteamento

### Tipos de Transmissão
* **Unicast:** Envio ponto a ponto de um transmissor exclusivo para um receptor específico (1:1).
* **Broadcast:** Envio simultâneo para todos os hosts pertencentes ao mesmo domínio de difusão (1:Todos).
* **Multicast:** Envio direcionado para um grupo específico de dispositivos assinantes do canal (1:Muitos).

### Mecânica de Roteamento (Camada 3)
* **Rotas Diretamente Conectadas:** Redes plugadas diretamente às interfaces ativas do roteador.
* **Rotas Estáticas:** Caminhos inseridos manualmente pelo administrador de rede.
* **Rotas Dinâmicas:** Aprendizado automático de rotas via protocolos de roteamento:
  * **RIP:** Baseado em contagem de saltos (*Hop Count*).
  * **OSPF:** Baseado no menor custo/largura de banda (*Link-State*).

---

## 💻 Diagnóstico e Solução de Problemas (CLI)

```powershell
# Exibe detalhes completos de adaptadores, MAC, IP, Máscara, Gateway e DHCP
ipconfig /all

# Exibe a tabela de cache ARP (vínculo IP x MAC conhecidos)
arp -a

# Rastreia cada salto (hop) de roteadores até o destino especificado
tracert 8.8.8.8
