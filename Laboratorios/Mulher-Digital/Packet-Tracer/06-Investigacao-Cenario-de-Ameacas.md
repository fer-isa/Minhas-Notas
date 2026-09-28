<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Investiga%C3%A7%C3%A3o%20de%20Amea%C3%A7as&fontSize=46&fontColor=FFFFFF&fontAlignY=35&desc=An%C3%A1lise%20de%20Vulnerabilidades%20e%20SOC%20%7C%20Cisco%20Packet%20Tracer&descAlignY=55&descSize=18&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Cisco_Packet_Tracer-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Ciberseguran%C3%A7a-161B22?style=for-the-badge&logo=shield&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Threat_Hunting-161B22?style=for-the-badge&logo=kalilinux&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Operações_SOC-161B22?style=for-the-badge&logo=target&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo
Neste laboratório, o foco foi investigar e mapear na prática três vetores críticos de ataque que agentes maliciosos utilizam para comprometer redes e dados: falhas de isolamento em redes Wi-Fi locais, engenharia social via e-mail de phishing com carga de ransomware, e interceptação de tráfego através de Rogue AP combinado com sequestro de DNS (DNS Hijacking).

> **🛡️ Visão de Segurança (SOC):**  
> Em operações de segurança (SOC), incidentes raramente acontecem de forma isolada. Este laboratório demonstra como vetores aparentemente simples como uma rede de convidados sem isolamento de clientes ou um ponto de acesso falso num café servem de porta de entrada para movimentação lateral e infecções massivas por ransomware. Compreender a correlação entre endereço IP, resolução de nomes (DNS) e comportamento do utilizador é indispensável para a triagem rápida de alertas e contenção de ameaças.

---

## 🗺️ Cenário Investigado
<div align="center">
  <img width="950" height="477" alt="Evidência 1 - Teste de Ping com Sucesso na Webcam" src="https://github.com/user-attachments/assets/f3685d66-c070-4366-9bc2-20ebb33b9e0e" />
  <p><i>Etapa inicial: Validação da falha de rede na residência, confirmando que o Smartphone 3 alcança diretamente a Webcam interna (192.168.100.101) via rede Guest aberta.</i></p>
</div>

---

## 💡 O Que Aprendi na Prática (Conceitos Técnicos)
Este laboratório ligou a teoria de redes e segurança à rotina operacional de investigação:

*   **Isolamento de Rede de Convidados (Client Isolation):** Uma rede Guest deve fornecer estritamente acesso à Internet pública. Quando a opção de isolamento de clientes ou regras de firewall interno não estão ativas, dispositivos desconhecidos ganham visibilidade total sobre os ativos locais da rede (LAN).
*   **Vetor Humano e Engenharia Social (Phishing):** A tecnologia mais avançada falha se o utilizador for induzido a clicar numa hiperligação fraudulenta. A carga maliciosa analisada ativou um ransomware com encriptação de disco e pedido de resgate financeiro.
*   **Rogue Access Point e Evil Twin:** A facilidade com que um atacante em local público pode replicar um SSID com nome atraente (`Cafe_WI-FI_FAST`) e sinal mais forte para enganar clientes em busca de conectividade.
*   **Envenenamento e Sequestro de DNS (DNS Spoofing / Hijacking):** A alteração do servidor DNS distribuído via DHCP permite manipular completamente o destino de domínios legítimos, direcionando pedidos de forma transparente para servidores maliciosos.

---

## ⚙️ Evidências e Fases da Investigação

<details open>
  <summary><b>🔍 1. Investigação da Falha no Roteador Doméstico (Clique para recolher)</b></summary>
  <br>
  <p>Para descobrir a origem da vulnerabilidade da webcam, acedi ao computador do escritório doméstico (Home Office PC) e identifiquei o Gateway padrão da rede:</p>
  <div align="center">
    <img width="956" height="537" alt="Evidência 2 - Descoberta do Default Gateway" src="https://github.com/user-attachments/assets/bbaf5bcf-6af3-4470-82d9-c24d5e32be85" />
    <p><i>Execução do comando <code>ipconfig</code> revelando o Default Gateway 192.168.100.1.</i></p>
  </div>
  <p>Acedendo à interface de gestão web do roteador doméstico com credenciais padrão (<code>admin/admin</code>), verifiquei as configurações de rádio e segurança sem fios:</p>
  <div align="center">
    <img width="931" height="812" alt="Evidência 3 - Verificação das Bandas Wireless" src="https://github.com/user-attachments/assets/fd33ea67-d452-460c-a3e0-4fa6accdaeef" />
    <p><i>Identificação das bandas ativas de 2.4 GHz e 5 GHz no roteador.</i></p>
  </div>
  <div align="center">
    <img width="775" height="507" alt="Evidência 4 - Falha de Segurança no Rádio Guest" src="https://github.com/user-attachments/assets/b052d54c-65d1-41c3-90c3-fb63de5ae689" />
    <p><i>Configuração crítica de segurança: enquanto as redes 2.4 GHz e 5 GHz-2 usam WPA2 Personal, a rede 5 GHz-1 (Guest) estava configurada como "Disabled" (sem autenticação).</i></p>
  </div>
</details>

<details open>
  <summary><b>🎣 2. Simulação de Phishing e Execução de Ransomware (Clique para recolher)</b></summary>
  <br>
  <p>Simulando o papel do atacante a partir do <b>Cafe Hacker Laptop</b>, disparei e-mails fraudulentos para os colaboradores da rede Filial contendo a ligação <code>pix.example.com</code>. Ao aceder à ligação no navegador da vítima (Laptop BR-2), o sistema foi comprometido por um ransomware:</p>
  <div align="center">
    <img width="1475" height="810" alt="Captura de tela 2026-09-28 135939" src="https://github.com/user-attachments/assets/4397e350-23f3-462c-ae3c-772f5a08f0b3" alt="Evidência 5 - Tela de Ransomware após Phishing" />
    <p><i>Ecrã de bloqueio e extorsão do ransomware (Decryptor 2.0) exigindo pagamento em criptomoeda para recuperação dos ficheiros encriptados.</i></p>
  </div>
</details>

<details open>
  <summary><b>📡 3. Sequestro de DNS via Ponto de Acesso Não Autorizado (Clique para recolher)</b></summary>
  <br>
  <p>No ambiente público (Café), abri a aplicação <b>PC Wireless</b> do utilizador e identifiquei os pontos de acesso disponíveis. A rede não autorizada <code>Cafe_WI-FI_FAST</code> apresentava maior intensidade de sinal (78%) em comparação com a rede legítima <code>Cafe_WiFi</code> (66%), induzindo a ligação:</p>
  <div align="center">
    <img width="587" height="437" alt="Captura de tela 2026-09-28 140531" src="https://github.com/user-attachments/assets/ed8eb542-c7cb-4b5a-8e55-c46d54c90701" alt="Evidência 6 - Lista de Redes Wi-Fi com o Rogue AP" />
    <p><i>Interface de ligação sem fios exibindo o Rogue AP "Cafe_WI-FI_FAST" com sinal superior para atrair as vítimas.</i></p>
  </div>
  <p>Após a ligação ao Rogue AP, ao navegar para um endereço legítimo (<code>friends.example.com</code>), a requisição foi desviada pelo atacante:</p>
  <div align="center">
    <img width="1486" height="767" alt="Captura de tela 2026-09-28 141234" src="https://github.com/user-attachments/assets/4368c1c9-bbe2-4598-9e8a-e9a225819db0"alt="Evidência 7 - Redirecionamento DNS para Ransomware" />
    <p><i>URL legítima apontando para o servidor de malware após o sequestro da resolução DNS.</i></p>
  </div>
</details>

---

## 🚨 Investigação Forense: Rastreando a Origem do Ataque

Para provar como o redirecionamento ocorreu, realizei a comparação forense entre a máquina comprometida e uma estação ligada com segurança via VPN no mesmo café:

1. **A Discrepância na Configuração de IP:**  
   Ao colocar as configurações lado a lado, identifiquei que a máquina vítima recebeu como servidor DNS o endereço `192.168.10.199`, enquanto a máquina na VPN utilizava o DNS corporativo legítimo `10.2.0.125`.

<div align="center">
  <img width="1646" height="675" alt="Evidência 8 - Comparativo de IP entre Cafe Customer e VPN Laptop" src="https://github.com/user-attachments/assets/dd10167c-0046-4638-a3a1-3ae5d3255383" />
  <p><i>Comparativo lado a lado: Cafe Customer (à esquerda) com DNS adulterado vs. VPN Laptop (à direita) com DNS legítimo.</i></p>
</div>

2. **A Prova Técnica (A "Arma do Crime"):**  
   Ao inspecionar a interface de rede do **Cafe Hacker Laptop**, confirmei que o seu IPv4 estático era exatamente `192.168.10.199`. O atacante executava um serviço DHCP que distribuía o próprio IP como servidor DNS e um serviço DNS que resolvia o domínio legítimo `friends.example.com` para o servidor de malware `10.6.0.250`.

<div align="center">
  <img width="726" height="655" alt="Evidência 9 - Configuração IP da Máquina do Atacante" src="https://github.com/user-attachments/assets/9720bd65-830f-4b60-9e07-6ce403fb2856" />
  <p><i>Configuração estática da máquina do atacante comprovando a identidade do servidor DNS fraudulento.</i></p>
</div>

---

## 🛡️ Recomendações de Mitigação (Defesa em Camadas)

*   **Segmentação e Isolamento Wi-Fi:** Desativar redes de convidados não monitorizadas ou aplicar autenticação WPA2/WPA3 forte, ocultação de broadcast do SSID e bloqueio total de tráfego destinado à sub-rede da LAN privada.
*   **Consciencialização dos Utilizadores (Security Awareness):** Treino contínuo contra técnicas de phishing, validação de remetentes e verificação de URLs antes de qualquer clique ou transferência.
*   **Controlos Perimétricos e Filtro de Conteúdo:** Utilização de firewalls de última geração (NGFW), sistemas de prevenção contra intrusão (IPS) e feeds de Threat Intelligence para bloqueio antecipado de domínios maliciosos conhecidos.
*   **Uso Obrigatório de VPN em Redes Públicas:** Garantir que todo o tráfego de dispositivos móveis seja encaminhado por túneis encriptados, neutralizando ataques de Man-in-the-Middle e rogue DNS.

<br>

<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Minhas_Notas-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2A4365,50:1A365D,100:0B1D3A&height=100&section=footer" width="100%" />
