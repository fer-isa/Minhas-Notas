<div align="center">
  <h2>🌐 Laboratório de Redes: DHCP e Troubleshooting</h2>
  <p><i>Meus estudos práticos de endereçamento IP e resolução de conflitos via Cisco IOS</i></p>
  
  <img src="https://img.shields.io/badge/Cisco_Packet_Tracer-049CE4?style=for-the-badge&logo=cisco&logoColor=white" />
  <img src="https://img.shields.io/badge/Networking-CCST-success?style=for-the-badge" />
</div>

<br>

### 🎯 O Objetivo
Neste laboratório, o foco foi configurar o roteador para entregar endereços IP automaticamente para os computadores da rede (servidor DHCP). Isso evita o trabalho manual e previne erros de digitação, algo essencial para o dia a dia em redes corporativas.

### 🗺️ A Topologia da Rede
<div align="center">
  <img src="https://github.com/user-attachments/assets/91be74b1-4821-4be7-876f-717c64647d2b" width="600px"/>
</div>

<br>

### 💡 O Que Eu Aprendi na Prática (Conceitos Técnicos)
Este laboratório foi fundamental para eu entender, consolidar e aplicar os seguintes termos:
*   **Gateway:** Aprendi que ele atua como a "porta de saída" da nossa rede local. No laboratório, configurei a interface do roteador (IP `192.168.1.1`) para ser esse Gateway, permitindo que os computadores saibam por onde enviar informações.
*   **DHCP Pool:** Entendi que o "Pool" é um grupo (ou bolsão) de endereços IP. Eu precisei criar esse Pool no roteador para que ele tivesse uma lista de IPs válidos para distribuir, garantindo que as máquinas pudessem se comunicar na rede.
*   **Troubleshooting:** Aprendi que esse termo é usado para descrever a investigação e a resolução de um problema técnico. Eu apliquei o troubleshooting na prática quando me deparei com um erro no roteador e precisei analisar os logs para descobrir a causa e aplicar a correção.

### ⚙️ Comandos Utilizados

<details>
  <summary><b>🛠️ 1. Configurando o Pool e o Gateway (Clique para expandir)</b></summary>
  <br>
  <p>Os comandos que utilizei no terminal (CLI) para criar o bolsão de IPs (Pool) e definir quem era o Gateway padrão da rede:</p>
  <pre><code>
Router(config)# ip dhcp pool REDE_LAN
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# dns-server 8.8.8.8
  </code></pre>
</details>

<details>
  <summary><b>🔍 2. Verificando a Tabela (Bindings) (Clique para expandir)</b></summary>
  <br>
  <div align="center">
    <img src="https://github.com/user-attachments/assets/62c89a46-e87f-4eb1-85b1-1fbe8b25919d" width="700px"/>
    <p><i>Usei o comando <code>show ip dhcp binding</code> para visualizar a tabela de concessões e confirmar que os computadores pegaram os IPs finais .2 e .3 automaticamente.</i></p>
  </div>
</details>

<br>

### 🚨 Troubleshooting: Resolvendo o Conflito de IP
Durante a configuração, enfrentei um problema real de rede que me exigiu investigar (troubleshooting) o que estava acontecendo:
<ul>
  <li><b>O Erro:</b> O terminal do roteador me mostrou o aviso <code>%DHCPD-4-PING_CONFLICT</code>. Analisando a mensagem, descobri que estava acontecendo um conflito com o IP do nosso Gateway (<code>192.168.1.1</code>).</li>
  <li><b>A Investigação e a Permissão:</b> Para resolver o conflito, aprendi que precisava usar o comando <code>clear ip dhcp binding *</code> para limpar a tabela de IPs que estava gerando o erro. </li>
  <li><b>O Aprendizado:</b> O comando falhou na primeira tentativa por falta de permissão. Isso me ensinou que, no sistema da Cisco, operações críticas exigem que o usuário eleve seu acesso para um nível superior (modo privilegiado/administrador) no terminal. Ao ajustar a permissão para um nível acima, consegui executar a limpeza com sucesso.</li>
</ul>

<br>

### ✅ Teste Final (Ping)
<div align="center">
  <img src="https://github.com/user-attachments/assets/fe988890-46db-43f7-8fb0-0877256e50bc" width="700px"/>
  <p><i>Com o problema resolvido, utilizei o comando Ping para testar a conectividade. Houve sucesso tanto na comunicação com o Gateway (192.168.1.1) quanto na comunicação direta entre os dois computadores (192.168.1.11).</i></p>
</div>
