<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=ACL%20Traffic%20Filtering&fontSize=44&fontColor=FFFFFF&fontAlignY=35&desc=Diagn%C3%B3stico%20e%20Resolu%C3%A7%C3%A3o%20de%20ACL%20Padr%C3%A3o%20%7C%20Cisco%20Packet%20Tracer&descAlignY=55&descSize=18&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Cisco_Packet_Tracer-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Standard_ACL-161B22?style=for-the-badge&logo=shield&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/ICMP_Troubleshooting-161B22?style=for-the-badge&logo=wireshark&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Cisco_NetAcad-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo
Investigar e restaurar a conectividade remota interrompida por uma **Lista de Controle de Acesso (ACL Padrão IPv4)** no roteador de borda `R1`. O cenário exigiu análise detalhada de tráfego ICMP, inspeção visual de pacotes via Simulation Panel, remoção dos filtros aplicados às interfaces seriais e correção de inconsistências de endereçamento IP estático nos hosts de destino.

> **🛡️ Visão de Segurança (SOC):**  
> Listas de Controle de Acesso (ACLs) representam a primeira linha de contenção em roteadores e firewalls de borda. Regras mal dimensionadas ou aplicadas na direção incorreta geram indisponibilidade de serviços legítimos (falso-positivo operacional) ou abrem brechas no perímetro. Compreender o fluxo de descarte e ler a ordem sequencial das regras é mandatório para análise de incidentes de rede.

<h2>🔍 A Metodologia de Troubleshooting Aplicada</h2>

<p>Para identificar se o bloqueio ocorria por regra de segurança ou falha de conectividade básica, o problema foi investigado em 4 etapas estruturadas:</p>

<pre><code>[1. Delimitar Escopo]      --> O PC1 não alcança a rede local (LAN) ou apenas redes remotas (WAN)?
[2. Inspeção de Políticas] --> Existem ACLs ativas bloqueando a rede de origem no gateway padrão?
[3. Modo de Simulação]     --> O pacote é descartado no roteador de borda ou no host de destino?
[4. Auditoria de Hosts]    --> IP, Máscara de Sub-rede e Gateway Padrão dos nós finais estão íntegros?</code></pre>

<hr>

## 🧯 O Problema: Bloqueio de Tráfego Inter-Redes

<details open>
  <summary><b>❌ 1. Ponto de partida e comportamento anômalo (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Comportamento na LAN:</b> O <code>PC1</code> comunicava-se normalmente com <code>PC2</code> e <code>PC3</code>, atestando comutação correta de Camada 2 no switch local <code>S1</code>.</li>
    <li><b>Falha de saída WAN:</b> Qualquer tentativa de ping originada no <code>PC1</code> com destino ao <code>PC4</code> ou ao <code>DNS Server</code> falhava com perda total de pacotes.</li>
    <li><b>Hipótese diagnóstica:</b> Bloqueio intencional por filtro de pacotes ou descarte ativo no gateway da rede local (<code>R1</code>).</li>
  </ul>
</details>

---

## 🛠️ A Solução: Investigação e Correção Passo a Passo

<details open>
  <summary><b>🔎 2. Auditoria da ACL no Roteador R1 (Clique para recolher)</b></summary>
  <br>
  <p>No terminal do roteador <code>R1</code>, o comando <code>show access-lists</code> revelou a regra responsável pelo descarte silencioso do tráfego:</p>
  <pre><code>R1# show access-lists
Standard IP access list 11
    10 deny 192.168.10.0 0.0.0.255
    20 permit any</code></pre>
  <ul>
    <li><b>Análise da regra:</b> A instrução <code>10</code> descarta todo tráfego originado no segmento <code>192.168.10.0/24</code> (rede do PC1).</li>
    <li><b>Vínculo de interface:</b> Através do <code>show running-config</code>, confirmou-se que a ACL 11 estava atrelada como filtro de saída (<code>out</code>) na interface <code>Serial0/0/0</code>.</li>
  </ul>
</details>

<details open>
  <summary><b>🗑️ 3. Remoção do Filtro e Exclusão da ACL (Clique para recolher)</b></summary>
  <br>
  <p>Para desvincular o filtro da porta WAN e excluir a regra da memória do equipamento, executou-se:</p>
  <pre><code>R1# configure terminal
R1(config)# interface Serial0/0/0
R1(config-if)# no ip access-group 11 out
R1(config-if)# exit
R1(config)# no access-list 11
R1(config)# end
R1# copy running-config startup-config</code></pre>
  <ul>
    <li>A interface serial voltou a encaminhar os pacotes de saída sem restrições de filtragem por IP de origem.</li>
  </ul>
</details>

<details open>
  <summary><b>🎯 4. Rastreio via Modo Simulação e Correção de Endereçamento (Clique para recolher)</b></summary>
  <br>
  <p>Mesmo após remover a ACL, os pings continuavam apresentando <i>Request timed out</i>. Ao ativar o <b>Simulation Panel</b>, o pacote ICMP viajou com sucesso por toda a malha de roteadores (<code>R1 &rarr; R2 &rarr; R3</code>), mas recebeu descarte visual (X vermelho) diretamente nos destinos finais:</p>
  <ul>
    <li><b>Erro no PC4:</b> Estava com o IP <code>192.168.30.12</code> configurado em vez de <code>192.168.30.10</code>. Corrigido para <code>192.168.30.10</code> e gateway <code>192.168.30.1</code>.</li>
    <li><b>Erro no DNS Server:</b> Estava configurado com o IP <code>192.168.31.12</code> em vez de <code>192.168.31.10</code>. Corrigido para <code>192.168.31.10</code> e gateway <code>192.168.31.1</code>.</li>
  </ul>
</details>

---

## 💡 O Que Aprendi na Prática (Conceitos de Troubleshooting)
* **ACL Padrão vs. Estendida:** As ACLs padrão avaliam unicamente o endereço IP de origem (`source IP`), devendo ser posicionadas estrategicamente o mais próximo possível do destino para evitar bloqueios colaterais em outras rotas válidas.
* **Ordem de Processamento das Regras:** As ACLs processam as linhas em ordem sequencial (top-down). Ao encontrar a primeira correspondência (`match`), a ação (`permit` ou `deny`) é executada imediatamente, sem avaliar as regras seguintes.
* **O "Implicit Deny" Invisível:** Toda ACL Cisco possui uma regra oculta implícita no final (`deny ip any any`). Se um pacote não casar com nenhuma instrução explícita de permissão, ele será descartado por padrão.
* **Isolamento de Falhas com Modo Simulação:** Um `Request timed out` nem sempre é sinal de bloqueio ativo no firewall/roteador; pacotes descartados no nó de destino por erro de IP ou gateway ausente produzem exatamente o mesmo sintoma na estação de origem.

---

## 🗺️ Evidências: Validação de Conectividade Fim a Fim

<details open>
  <summary><b>✅ 5. Testes de conectividade remota restabelecida (Clique para recolher)</b></summary>
  <br>
  <p>Com a ACL 11 excluída do roteador <code>R1</code> e as configurações IP corrigidas no <code>PC4</code> e no <code>DNS Server</code>, os testes de ICMP executados no <b>PC1</b> confirmaram convergência total:</p>
  <pre><code>C:\&gt;ping 192.168.30.10
Pinging 192.168.30.10 with 32 bytes of data:
Reply from 192.168.30.10: bytes=32 time=2ms TTL=125
Reply from 192.168.30.10: bytes=32 time=2ms TTL=125
Reply from 192.168.30.10: bytes=32 time=2ms TTL=125

Ping statistics for 192.168.30.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)</code></pre>
  <pre><code>C:\&gt;ping 192.168.31.10
Pinging 192.168.31.10 with 32 bytes of data:
Reply from 192.168.31.10: bytes=32 time=2ms TTL=125
Reply from 192.168.31.10: bytes=32 time=2ms TTL=125
Reply from 192.168.31.10: bytes=32 time=10ms TTL=125

Ping statistics for 192.168.31.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)</code></pre>
  <div align="center">
    <p><i>Conexão bidirecional validada com sucesso através de roteamento OSPF após eliminação do filtro de borda e correção de host.</i></p>
  </div>
</details>

<hr>

<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas/tree/main/Mulher-Digital/Ciberseguranca">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Índice_de_Cibersegurança-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=120&section=footer&animation=fadeIn" width="100%" />

</div>
