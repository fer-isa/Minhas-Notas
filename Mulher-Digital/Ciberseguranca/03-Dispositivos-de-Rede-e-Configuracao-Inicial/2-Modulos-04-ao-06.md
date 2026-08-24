<div align="center">

# 🌐 Comutação Ethernet & Camada de Rede — Módulos 4 ao 6
**Formação Mulher Digital • Trilha de Cibersegurança**

</div>

---

## 📌 Visão Geral
Este documento aborda o funcionamento da tecnologia Ethernet nas camadas 1 e 2 do modelo OSI, a estrutura dos quadros de dados, o comportamento da tabela CAM em switches e os princípios do protocolo IP na camada 3.

---

## 🔌 1. Tecnologia Ethernet e Subcamadas (IEEE)

A tecnologia Ethernet opera nas camadas **Física** e de **Enlace de Dados**, dividida em duas subcamadas padronizadas pelo IEEE:

* **Subcamada LLC (*Logical Link Control* - IEEE 802.2):** Interface de software que se comunica com os protocolos da Camada 3 (Rede) e identifica o protocolo encapsulado.
* **Subcamada MAC (*Media Access Control* - IEEE 802.3):** Responsável direta pelo controle de acesso ao meio físico, montagem do quadro e endereçamento físico.

---

## 📦 2. Estrutura do Quadro Ethernet (Ethernet Frame)

O quadro Ethernet possui tamanho total variando entre **64 bytes (mínimo)** e **1518 bytes (máximo)**. Quadros fora desses limites são classificados como *Runt* (<64B) ou *Giant* (>1518B) e são descartados por erro:

| Campo | Tamanho | Função |
| :--- | :---: | :--- |
| **Preâmbulo & SFD** | 8 bytes | Sincroniza o sinal e avisa a placa de rede da chegada do quadro. |
| **MAC Destino** | 6 bytes | Endereço físico do dispositivo que receberá o quadro. |
| **MAC Origem** | 6 bytes | Endereço físico da placa que enviou o quadro. |
| **Tipo / EtherType** | 2 bytes | Identifica o protocolo da camada superior (ex: IPv4 ou IPv6). |
| **Dados / Payload** | 46 a 1500 bytes | Carga útil encapsulada (pacote de rede). |
| **FCS (*Frame Check Sequence*)** | 4 bytes | Código matemático de verificação de integridade contra erros. |

---

## 🏷️ 3. Endereçamento MAC & Modos de Transmissão

O endereço MAC possui **48 bits** expressos em 12 dígitos hexadecimais (ex: `00:1A:2B:3C:4D:5E`):
* **Primeiros 24 bits (OUI):** Código identificador exclusivo do fabricante da placa.
* **Últimos 24 bits:** Número de série exclusivo da placa de rede.

### Modos de Comunicação
* **Unicast:** Destinado a um único nó final específico.
* **Broadcast:** Destinado a todos os dispositivos da LAN (`FF:FF:FF:FF:FF:FF`).
* **Multicast:** Destinado a um grupo selecionado de dispositivos assinantes.

---

## 🔄 4. Funcionamento do Switch & Tabela MAC (CAM)

1. **Aprendizado:** O switch examina o **MAC de Origem** de todo quadro que entra e associa o endereço à porta física na sua **Tabela CAM**.
2. **Encaminhamento Direto:** Ao consultar a tabela e encontrar o **MAC de Destino**, o switch envia o quadro exclusivamente para aquela porta correspondente.
3. **Inundação (*Flooding*):** Se o quadro for um *Unknown Unicast* (MAC de destino não registrado na tabela), o switch repassa o quadro para **todas as portas ativas**, exceto a de origem.

---

## 🌍 5. Camada 3: Protocolo IP (IPv4 vs. IPv6)

O protocolo IP fornece comunicação lógica de ponta a ponta entre diferentes redes através de três propriedades:

* **Sem Conexão (*Connectionless*):** Envia pacotes sem negociação de handshake prévio.
* **Melhor Esforço (*Best Effort*):** Não garante entrega de pacotes nem retransmissão de perdas no nível de rede.
* **Independente de Mídia:** Trafega de forma consistente por qualquer meio físico (cobre, fibra óptica ou sem fio).

### Comparativo: Cabeçalhos IPv4 vs. IPv6

| Característica | IPv4 | IPv6 |
| :--- | :--- | :--- |
| **Tamanho do Endereço** | 32 bits (`192.168.0.1`) | 128 bits (`2001:db8::1`) |
| **Espaço de Endereços** | ~4,3 bilhões | ~$3,4 \times 10^{38}$ |
| **Tamanho do Cabeçalho** | Variável (20 a 60 bytes) | Fixo (40 bytes) |
| **Fragmentação de Pacote** | Executada na origem e em roteadores | Executada exclusivamente no host de origem |
