# 🌐 Conceitos Básicos de Redes — Módulos 10 ao 15 (Roteamento e Endereçamento)
**Formação Mulher Digital | Trilha de Cibersegurança**

## 📌 Visão Geral
Este documento agrupa o resumo final do curso, cobrindo os **Módulos 10 a 15**. O foco recai sobre o endereçamento IP (IPv4 e IPv6), a mecânica de roteamento entre redes diferentes, e os protocolos essenciais que mantêm a internet funcionando (DHCP, DNS e ARP).

---

## 🔢 Endereçamento IP e Máscaras
* **O que é o IP:** É a identidade numérica exclusiva de um dispositivo, contendo o IP de Origem (emissor) e o IP de Destino (receptor) no pacote de dados[cite: 5]. Todo endereço possui uma parte que identifica a rede (Network ID) e outra que identifica o dispositivo dentro dessa rede (Host ID)[cite: 5].
* **IPv4 vs. IPv6:**
  * **IPv4:** Composto por 32 bits divididos em 4 octetos na notação decimal pontuada (ex: 192.168.1.50)[cite: 5]. Possui um limite de cerca de 4 bilhões de endereços[cite: 5].
  * **IPv6:** Composto por 128 bits divididos em 8 blocos de caracteres hexadecimais (ex: 2001:DB8::1)[cite: 5]. Oferece uma quantidade gigantesca de endereços, o que geralmente elimina a necessidade do uso de NAT[cite: 5].
* **Máscara de Sub-rede:** É um número de 32 bits que informa qual parte do IPv4 é a rede (bits 1) e qual parte é o host (bits 0)[cite: 5]. As redes são frequentemente representadas pela notação CIDR, como /24 para indicar que os primeiros 24 bits são a rede[cite: 5].

---

## 🌍 IPs Públicos, Privados e NAT
* **No IPv4:**
  * **Públicos:** São visíveis globalmente na internet, atribuídos pelo provedor e únicos no mundo[cite: 5].
  * **Privados:** Usados apenas na rede local (como 192.168.x.x ou 10.x.x.x), sendo invisíveis na internet[cite: 5].
  * **NAT:** É a técnica que traduz todos os IPs privados de uma casa/empresa em um único IP público na hora de acessar um site externo[cite: 6].
* **No IPv6:**
  * **GUA (Global Unicast Address):** O equivalente ao IP público, roteável diretamente na internet e que geralmente começa com 2 ou 3[cite: 6].
  * **ULA (Unique Local Address):** O equivalente ao IP privado, usado exclusivamente para comunicação interna e que começa com as letras "fd" ou "fc"[cite: 6].

---

## 🛠️ Protocolos de Descoberta e Configuração
* **DHCP (Dynamic Host Configuration Protocol):** Automatiza a entrega de configurações de rede (IP, máscara, gateway e DNS) aos dispositivos através do processo de 4 etapas "DORA" (Discover, Offer, Request, Pack/Ack)[cite: 5].
* **DNS (Domain Name System):** O serviço de tradução que converte nomes legíveis de sites (ex: google.com) em endereços numéricos IP, evitando que o usuário precise memorizar números[cite: 5].
* **ARP (Address Resolution Protocol):** Um mecanismo que descobre o endereço físico MAC a partir de um endereço IP conhecido, fazendo a ponte entre a Camada 3 (Rede) e a Camada 2 (Enlace)[cite: 6].

---

## 🛣️ Lógicas de Transmissão e Roteamento
* **Tipos de Transmissão:**
  * **Unicast:** Os dados vão de um emissor direto para um único receptor (1 para 1)[cite: 6].
  * **Broadcast:** Os dados são enviados uma única vez para todos os dispositivos na mesma rede local (1 para todos)[cite: 6].
  * **Multicast:** Os dados são enviados apenas para um grupo selecionado de dispositivos (1 para muitos)[cite: 6].
* **O Processo de Roteamento:** Opera na Camada 3 do modelo OSI e escolhe o melhor caminho para enviar pacotes de uma rede para outra utilizando uma "Tabela de Roteamento"[cite: 6].
* **Tipos de Rotas:** 
  * Diretamente Conectadas (redes vizinhas plugadas no roteador)[cite: 6].
  * Estáticas e Padrão (configuradas manualmente pelo administrador)[cite: 6].
  * Protocolos Dinâmicos: Como o RIP (escolhe a rota pelo menor número de roteadores) e o OSPF (escolhe o caminho mais rápido)[cite: 6].
* **Tipos de Gateway:** Existem Gateways Padrão (porta de saída local para a internet), de Protocolo, de Aplicativo, de Voz (VoIP) e de Armazenamento em nuvem[cite: 6].

---

## 💻 Comandos e Solução de Problemas (Windows)
* `ipconfig /all`: Mostra todas as informações detalhadas da rede, incluindo o MAC (Physical Address), IP, Subnet Mask e quem é o servidor DHCP[cite: 6].
* `arp -a`: Exibe a tabela de cache ARP, mostrando o vínculo entre os endereços IP e os endereços MAC dos aparelhos que conversaram com a sua máquina[cite: 6].
* `tracert <destino>`: Rastreia a rota e exibe cada salto (*hop*) que um pacote dá passando pelos roteadores até chegar ao seu destino final[cite: 6].
