# 🌐 Conceitos Básicos de Redes — Módulos 6 ao 9 (Avançado)
**Formação Mulher Digital • Trilha de Cibersegurança**

---

## 📌 Visão Geral
Este documento consolida o aprofundamento técnico em comunicação de redes, cobrindo o encapsulamento de dados, esquemas de endereçamento e identificação, segmentação corporativa, topologias e fundamentos de segurança defensiva.

---

## 📦 Modelos de Rede & Encapsulamento

* **Encapsulamento:** Processo sequencial de adicionar cabeçalhos e trailers de controle a cada camada do modelo OSI/TCP/IP à medida que a informação desce na pilha até se transformar em bits.
* **Quadro Ethernet (Layer 2):** Estrutura de dados que envelopa o pacote IP, adicionando os endereços MAC de origem e destino para entrega local.
* **Camada de Acesso:** Ponto de entrada que conecta os nós finais à infraestrutura de agregação/núcleo, provendo serviços de rede locais.
* **Ethernet vs. Internet:**
  * **Ethernet:** Padrão físico e de enlace (IEEE 802.3) para transmissão em redes locais (LAN).
  * **Internet:** Malha global de redes interconectadas através de protocolos de roteamento IP e ASN.

---

## 🆔 Identificação na Rede: MAC, IP e DNS

| Mecanismo | Camada OSI | Formato / Exemplo | Função Principal |
| :--- | :---: | :--- | :--- |
| **Endereço MAC** | Enlace (L2) | Hexadecimal (`00:1A:2B:3C:4D:5E`) | Identificador físico e exclusivo gravado na placa de rede (NIC). |
| **Endereço IP** | Rede (L3) | Decimal pontuado / Hexadecimal | Identificador lógico e roteável de localização na rede. |
| **DNS** | Aplicação (L7) | Nomes de Domínio (`cisco.com`) | Resolução e tradução de nomes legíveis para endereços IP numéricos. |

---

## 🏢 Escopo Corporativo e NAT

### Segmentação de Acesso
* **Intranet:** Rede interna de acesso restrito exclusiva a colaboradores autorizados da organização.
* **Extranet:** Extensão controlada e autenticada da intranet para terceiros, clientes e fornecedores.

### NAT (*Network Address Translation*)
* **Objetivo:** Mapeamento e tradução de múltiplos endereços IP privados internos para um único endereço IP público válido na Internet.
* **Benefícios:** Conservação do pool de endereços IPv4 públicos e segurança por ofuscação da topologia interna.

---

## 🗺️ Topologias & Protocolos IP

### Comparativo de Topologias Físicas

| Topologia | Estrutura | Vantagens | Desvantagens |
| :--- | :--- | :--- | :--- |
| **Estrela** | Conexão de todos os nós a um concentrador central (Switch). | Isolamento simples de falhas e expansão rápida. | Ponto único de falha no dispositivo central. |
| **Barramento** | Meio de transmissão compartilhado linear único (*backbone*). | Baixo consumo de cabo e custo reduzido. | Alto risco de colisão e difícil isolamento de erros. |
| **Malha (Mesh)** | Conexões diretas ponto a ponto redundantes entre nós. | Alta tolerância a falhas e caminhos alternativos. | Elevado custo e complexidade de cabeamento/portas. |

### Endereçamento IPv4 vs. IPv6

* **IPv4:** Endereço de 32 bits (4 octetos em formato decimal, ex: `192.168.1.10`), com espaço total de ~$4.3 \times 10^9$ endereços.
* **IPv6:** Endereço de 128 bits (8 grupos de 4 dígitos hexadecimais), projetado para substituir o IPv4 com segurança nativa e espaço quase ilimitado.

---

## 🛡️ Fundamentos de Segurança de Rede

* **Firewall (Borda / Host):** Sistema de filtragem e inspeção de pacotes (Stateful / Stateless / NGFW) baseado em regras rígidas de portas, protocolos e fluxos.
* **Hardening & Boas Práticas Operacionais:**
  1. **Patch Management:** Manutenção e atualização contínua de firmwares e SOs.
  2. **Autenticação Robusta:** Políticas de senhas fortes associadas a MFA (Multi-Factor Authentication).
  3. **Least Privilege:** Concessão restrita do menor nível de privilégio exigido por função.
  4. **Criptografia de Tráfego:** Uso mandatório de túneis e protocolos seguros (TLS/HTTPS, SSH, IPsec).
  5. **Auditoria Contínua:** Coleta e correlação de logs de eventos e tráfego anômalo.
