<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=NAT%20Est%C3%A1tico%20no%20Roteador&fontSize=48&fontColor=FFFFFF&fontAlignY=35&desc=Tradu%C3%A7%C3%A3o%20de%20Endere%C3%A7os%20e%20Conectividade%20%7C%20Cisco%20Packet%20Tracer&descAlignY=55&descSize=18&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Cisco_Packet_Tracer-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Networking_CCST-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Configuração_NAT-161B22?style=for-the-badge&logo=quicklook&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Segurança_Defensiva-161B22?style=for-the-badge&logo=shield&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo
Neste laboratório, o foco foi implementar o **NAT Estático (Network Address Translation)** no roteador Cisco 1941, configurando a tradução biunívoca entre um endereço IPv4 privado da rede interna (LAN) e um endereço IPv4 público/externo para comunicação com a rede externa e servidores.

> **🛡️ Visão de Segurança (SOC):**  
> O NAT não serve apenas para economizar blocos de IPv4: ele é uma barreira de segurança defensiva perimetral fundamental. Dispositivos com endereços privados (`192.168.0.0/16`, `10.0.0.0/8`, `172.16.0.0/12`) não são roteáveis na Internet pública, o que impede varreduras e acessos externos diretos aos hosts da nossa rede interna. Em análise de tráfego de SOC e leitura de logs de firewall, saber interpretar o par *Inside Local* (IP real do host interno) e *Inside Global* (IP público visível na borda) é essencial para correlacionar qual máquina interna iniciou uma conexão externa suspeita.

---

## 🗺️ A Topologia da Rede
A estrutura do laboratório foi composta por um host local conectado a um switch, que se comunica com a interface interna do roteador. O roteador, por sua vez, liga a rede local ao servidor externo:

<div align="center">
  <!-- FOTO 1 AQUI: Topologia no Packet Tracer (computador 1 -> Switch0 -> Router0 -> Server0) -->
  <img width="767" height="610" alt="Captura de tela 2026-09-29 161341" src="https://github.com/user-attachments/assets/0fe7aa8c-1e3b-43fa-8c13-bca8f580a54b" alt="Evidência 1 - Topologia do Laboratório de NAT Estático no Packet Tracer />
  <p><i>Topologia: PC0 (192.168.1.10) conectado à interface Gi0/0 (LAN) e o Servidor externo (200.0.0.10) conectado à interface Gi0/1 (WAN).</i></p>
</div>

---

## 💡 O Que Aprendi na Prática (Conceitos Técnicos)
*   **Inside Local vs. Inside Global:** O endereço *Inside Local* é o IP privado configurado diretamente na placa de rede da máquina interna (`192.168.1.10`). O *Inside Global* é o endereço IP válido e roteável (`200.0.0.2`) que o roteador assume e apresenta para a rede externa em nome desse host.
*   **Papel das Zonas NAT (`ip nat inside` e `ip nat outside`):** O roteador precisa saber explicitamente de onde o pacote está vindo e para onde ele vai. Sem definir a interface de entrada como *inside* e a de saída como *outside*, o motor de NAT não sabe quando disparar a tradução.
*   **NAT Estático (1:1):** Mapeamento fixo e manual entre um único IP privado e um único IP público. É amplamente utilizado quando servidores internos (como servidores web ou de aplicação) precisam ser acessíveis de fora por um IP fixo conhecido.

---

## ⚙️️ Comandos Utilizados e Configurações

<details open>
  <summary><b>🛠️ 1. Configuração do Roteador no Terminal CLI (Clique para recolher)</b></summary>
  <br>
  <p>No terminal do Cisco Router 1941, configurei o endereçamento das interfaces, o direcionamento das zonas NAT e a regra estática de tradução:</p>
  <div align="center">
    <!-- FOTO 2 AQUI: CLI do Roteador com os comandos de IP, nat inside, nat outside e a regra de NAT -->
    <img width="705" height="437" alt="Captura de tela 2026-09-29 161230" src="https://github.com/user-attachments/assets/e06b14a6-1dc3-40ab-836c-f44423a63a26"alt="Evidência 2 - Comandos CLI executados no Roteador" />
    <p><i>Histórico de comandos aplicados na interface Gi0/0 (inside), Gi0/1 (outside) e a criação da regra com <code>ip nat inside source static</code>.</i></p>
  </div>
  <pre><code>
Router>enable
Router#configure terminal

! Interface Interna (LAN)
Router(config)#interface gigabitEthernet 0/0
Router(config-if)#ip address 192.168.1.1 255.255.255.0
Router(config-if)#ip nat inside
Router(config-if)#no shutdown
Router(config-if)#exit

! Interface Externa (WAN)
Router(config)#interface gigabitEthernet 0/1
Router(config-if)#ip address 200.0.0.1 255.255.255.0
Router(config-if)#ip nat outside
Router(config-if)#no shutdown
Router(config-if)#exit

! Regra de Tradução Estática
Router(config)#ip nat inside source static 192.168.1.10 200.0.0.2
Router(config)#end
  </code></pre>
</details>

<details open>
  <summary><b>🔍 2. Verificando a Tabela de Traduções NAT (Clique para recolher)</b></summary>
  <br>
  <p>Para auditar se o roteador realmente vinculou os endereços de acordo com o planejado, utilizei o comando de inspeção <code>show ip nat translations</code>:</p>
  <div align="center">
    <!-- FOTO 3 AQUI: Saída do comando show ip nat translations mostrando a tabela -->
    <img width="703" height="107" alt="Captura de tela 2026-09-29 161310" src="https://github.com/user-attachments/assets/4929f4e8-7960-4edf-9692-cef249047650" alt="Evidência 3 - Saída do comando show ip nat translations"/>
    <p><i>Tabela NAT comprovando a associação permanente entre o endereço Inside local (192.168.1.10) e o Inside global (200.0.0.2).</i></p>
  </div>
</details>

---

## ✅ Teste Final de Conectividade e Validação (Ping)
Com as interfaces ativas e a regra carregada na tabela do roteador, acessei o Prompt de Comando do **PC0** e efetuei o teste de conectividade ICMP contra o endereço do servidor externo (`200.0.0.10`):

<div align="center">
  <!-- FOTO 4 AQUI: Terminal do PC0 com o ping para 200.0.0.10 e 1 pacote perdido por ARP -->
  <img width="550" height="297" alt="Captura de tela 2026-09-29 161203" src="https://github.com/user-attachments/assets/fb469a19-f185-4f27-98a3-5fb802f3a1ac" alt="Evidência 4 - Teste de Ping com Sucesso no Prompt de Comando do PC0"/>
  <p><i>Validação do tráfego: o primeiro pacote sofreu Request timed out devido ao tempo de convergência e resolução de ARP entre os saltos, seguido por 3 respostas completas (Reply) com TTL=127, validando a travessia e a tradução do NAT com sucesso.</i></p>
</div>

<br>

<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Minhas_Notas-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2A4365,50:1A365D,100:0B1D3A&height=100&section=footer" width="100%" />
