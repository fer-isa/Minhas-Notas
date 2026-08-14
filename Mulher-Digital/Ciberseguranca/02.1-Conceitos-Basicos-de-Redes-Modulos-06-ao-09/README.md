# 🌐 Conceitos Básicos de Redes — Módulos 6 ao 9 (Avançado)
**Formação Mulher Digital | Trilha de Cibersegurança**

## 📌 Visão Geral
Este documento contém as anotações e resumos dos **Módulos 6 ao 9** do curso de Redes. O conteúdo aprofunda o modelo OSI e TCP/IP, protocolos de endereçamento e os fundamentos de segurança de redes e topologias.

---

## 📦 Modelos de Rede e Encapsulamento
* **Encapsulamento e Quadro Ethernet:** O encapsulamento "empacota" os dados em uma caixa, enquanto o quadro Ethernet coloca uma etiqueta com o endereço do remetente e destinatário para que a rede saiba para onde enviar o pacote[cite: 4].
* **Camada de Acesso:** Funciona como a "porta de entrada" da rede, conectando os dispositivos dos usuários ao *backbone* (rede central) e fornecendo serviços como DHCP e NAT[cite: 4].
* **Ethernet vs. Internet:** A Ethernet é a tecnologia que define as regras de transmissão para conectar dispositivos em uma rede local (LAN), enquanto a Internet é a rede mundial que conecta milhões de redes entre si[cite: 4].

---

## 🆔 Identificação na Rede: MAC, IP e DNS
* **Endereço MAC:** É a identidade física e fixa da placa de rede, funcionando como o "RG" do dispositivo, garantindo que ele seja único no mundo (ex: `00:1A:2B:3C:4D:5E`)[cite: 4].
* **Endereço IP:** É a localização na rede (como o "endereço de uma casa") e pode mudar dependendo de onde o aparelho se conecta[cite: 4].
* **DNS (Domain Name System):** Funciona como a agenda de endereços da Internet[cite: 4]. Ele traduz nomes de sites que os humanos entendem (ex: `google.com`) em endereços IP numéricos que os computadores entendem (ex: `8.8.8.8`)[cite: 4].

---

## 🏢 Escopo Corporativo e NAT
* **Intranet e Extranet:**
  * **Intranet:** Internet particular de uma empresa, protegida por senhas e firewalls, para compartilhamento interno de arquivos e avisos exclusivos para funcionários[cite: 4].
  * **Extranet:** Extensão da rede com acesso controlado para pessoas de fora, como parceiros, clientes e fornecedores[cite: 4].
* **NAT (Network Address Translation):**
  * Mecanismo que traduz endereços IP privados em endereços IP públicos[cite: 4].
  * **Vantagens:** Economiza endereços IPv4, aumenta a segurança ocultando a rede interna e permite que vários dispositivos de uma mesma casa/empresa compartilhem um único IP público na Internet[cite: 4].

---

## 🗺️ Topologias e Endereçamento Avançado
* **Topologias de Rede:**
  * **Estrela:** Todos os dispositivos se conectam a um ponto central (switch/hub)[cite: 4]. É fácil de gerenciar e isola falhas por dispositivo[cite: 4].
  * **Barramento:** Todos os dispositivos compartilham um único cabo central[cite: 4]. É simples, mas tem maior risco de colisões de dados[cite: 4].
  * **Malha:** Múltiplos caminhos interconectados, oferecendo alta redundância e tolerância a falhas, embora seja mais complexa e cara[cite: 4].
* **IPv4 vs. IPv6:**
  * **IPv4:** Endereço de 32 bits (4 octetos) em formato decimal (ex: `192.168.1.10`)[cite: 4].
  * **IPv6:** Endereço de 128 bits em formato hexadecimal, criado para suprir a escassez de endereços do IPv4 e melhorar a eficiência[cite: 4].

---

## 🛡️ Segurança de Rede
* **Firewall:** Barreira de segurança (física ou lógica) que filtra o tráfego de entrada e saída com base em regras predefinidas, protegendo a rede contra acessos não autorizados e ataques como DoS e Port Scanning[cite: 4].
* **Boas Práticas:**
  1. Manter sistemas atualizados[cite: 4].
  2. Usar senhas fortes e autenticação multifator[cite: 4].
  3. Aplicar o princípio do menor privilégio[cite: 4].
  4. Utilizar criptografia sempre que possível (HTTPS, VPN)[cite: 4].
  5. Monitorar logs e eventos da rede[cite: 4].
