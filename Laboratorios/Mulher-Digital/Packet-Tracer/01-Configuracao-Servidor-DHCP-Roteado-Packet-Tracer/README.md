<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=DHCP%20e%20Troubleshooting&fontSize=50&fontColor=FFFFFF&fontAlignY=35&desc=Laborat%C3%B3rio%20de%20Redes%20%7C%20Cisco%20Packet%20Tracer&descAlignY=55&descSize=20&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Cisco_Packet_Tracer-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Networking_CCST-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Troubleshooting-161B22?style=for-the-badge&logo=quicklook&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo
Neste laboratório, o foco foi configurar o roteador para entregar endereços IP automaticamente para os computadores da rede (servidor DHCP). Isso evita o trabalho manual e previne erros de digitação, algo essencial para manter a integridade e a organização em redes corporativas.

> **🛡️ Visão de Segurança (SOC):** 
> Entender como o DHCP distribui os IPs é fundamental para a triagem de incidentes. Em um cenário real de SOC, se um alerta de segurança apontar para o IP `192.168.1.11`, eu preciso saber analisar a tabela DHCP para descobrir exatamente **qual máquina** recebeu esse endereço naquele momento.

---

## 🗺️ A Topologia da Rede
<div align="center">
  <img src="https://github.com/user-attachments/assets/91be74b1-4821-4be7-876f-717c64647d2b" width="600px"/>
</div>

---

## 💡 O Que Aprendi na Prática (Conceitos Técnicos)
Este laboratório foi fundamental para consolidar a base de endereçamento e comunicação:

*   **Gateway:** Aprendi que ele atua como a "porta de saída" da nossa rede local. No laboratório, configurei a interface do roteador (IP `192.168.1.1`) para ser esse Gateway, permitindo que os computadores saibam por onde enviar informações para fora da rede.
*   **DHCP Pool:** Entendi que o "Pool" é um grupo (ou bolsão) de endereços IP. Precise criar esse Pool no roteador para que ele tivesse uma lista de IPs válidos para distribuir, garantindo que as máquinas pudessem se comunicar.
*   **Troubleshooting:** A prática da investigação. Apliquei o troubleshooting real quando me deparei com um erro no roteador, precisando analisar logs para descobrir a causa e aplicar a correção (detalhes na seção de conflitos abaixo).

---

## ⚙️ Comandos Utilizados e Configurações

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
  <summary><b>🔍 2. Verificando a Tabela DHCP (Bindings) (Clique para expandir)</b></summary>
  <br>
  <div align="center">
    <img src="https://github.com/user-attachments/assets/62c89a46-e87f-4eb1-85b1-1fbe8b25919d" width="700px"/>
    <p><i>Usei o comando <code>show ip dhcp binding</code> para visualizar a tabela de concessões e confirmar que os computadores pegaram os IPs finais .2 e .3 automaticamente.</i></p>
  </div>
</details>

---

## 🚨 Troubleshooting: Resolvendo o Conflito de IP

Durante a configuração, enfrentei um problema de rede que exigiu investigação analítica para ser solucionado:

1. **O Erro (Identificação):** O terminal do roteador retornou o log <code>%DHCPD-4-PING_CONFLICT</code>. Analisando essa mensagem, diagnostiquei que estava ocorrendo um conflito com o próprio IP reservado do nosso Gateway (<code>192.168.1.1</code>).
2. **A Ação (Correção):** Para resolver o conflito, precisei utilizar o comando <code>clear ip dhcp binding *</code> para limpar a tabela de IPs que estava gerando o erro.
3. **O Aprendizado (Escalonamento de Privilégios):** O comando falhou na primeira tentativa por falta de permissão. Isso me ensinou na prática que operações críticas exigem a elevação de privilégios (modo administrador/privilegiado) no terminal Cisco. Após elevar o acesso, a limpeza foi executada com sucesso.

---

## ✅ Teste Final de Conectividade (Ping)
<div align="center">
  <img src="https://github.com/user-attachments/assets/fe988890-46db-43f7-8fb0-0877256e50bc" width="700px"/>
  <p><i>Com o problema resolvido, validei a conectividade via Ping (ICMP). Houve sucesso tanto na comunicação com o Gateway (192.168.1.1) quanto na comunicação direta entre os dois computadores da topologia.</i></p>
</div>

<br>

<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Minhas_Notas-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2A4365,50:1A365D,100:0B1D3A&height=100&section=footer" width="100%" />
