<div align="center">

  <h1>🌐 Laboratório Prático: Introdução às Redes Hierárquicas</h1>
  <p><b>Arquitetura de Rede Corporativa baseada no Modelo de Três Camadas (Acesso, Distribuição e Núcleo)</b></p>

  <p>
    <img src="https://img.shields.io/badge/Cisco-Packet_Tracer-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white" alt="Cisco Packet Tracer" />
    <img src="https://img.shields.io/badge/Arquitetura-Modelo_3_Camadas-0A84FF?style=for-the-badge" alt="Modelo Hierárquico" />
    <img src="https://img.shields.io/badge/Trilha-Mulher_Digital_Redes-8A2BE2?style=for-the-badge" alt="Mulher Digital" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>

</div>

<hr/>

<h2>📌 1. Visão Geral do Projeto</h2>

<p>
Este projeto documenta a implementação prática de uma arquitetura de rede corporativa baseada no <b>Modelo Hierárquico de Três Camadas da Cisco (Core, Distribution e Access)</b> desenvolvida no <b>Cisco Packet Tracer</b>.
</p>

<p>
O objetivo principal foi estruturar a segmentação física e lógica do ambiente, realizar o cabeamento estruturado com conexões específicas de <i>FastEthernet</i> e <i>GigabitEthernet</i>, parametrizar o endereçamento IPv4 estático nos computadores finais e ativar a interface de Gateway de saída no roteador de Núcleo (Core) via CLI do Cisco IOS.
</p>

<hr/>

<h2>🏗️ 2. Arquitetura da Topologia & Dispositivos</h2>

<p>A rede foi estruturada seguindo a divisão clássica do modelo hierárquico corporativo:</p>

<table width="100%">
  <thead>
    <tr bgcolor="#1f242c">
      <th align="left">Camada Hierárquica</th>
      <th align="left">Dispositivo / Modelo</th>
      <th align="left">Quantidade</th>
      <th align="left">Função na Arquitetura</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>Camada de Núcleo (Core)</b></td>
      <td>Roteador Cisco 4331</td>
      <td>1 unidade</td>
      <td>Encaminhamento de tráfego em alta velocidade e gateway da rede local</td>
    </tr>
    <tr>
      <td><b>Camada de Distribuição</b></td>
      <td>Switch Cisco Catalyst 3650-24PS</td>
      <td>1 unidade</td>
      <td>Agregação de tráfego dos switches de acesso e aplicação de políticas</td>
    </tr>
    <tr>
      <td><b>Camada de Acesso</b></td>
      <td>Switch Cisco Catalyst 2960-24TT</td>
      <td>2 unidades</td>
      <td>Conexão direta com os dispositivos dos usuários finais (estações de trabalho)</td>
    </tr>
    <tr>
      <td><b>Dispositivos Finais (End Devices)</b></td>
      <td>PCs genéricos (<code>PC-Lab01</code>, <code>PC-Lab02</code>, <code>PC-Sec01</code>, <code>PC-Sec02</code>)</td>
      <td>4 unidades</td>
      <td>Estações de trabalho divididas por setores (Laboratório e Secretaria)</td>
    </tr>
    <tr>
      <td><b>Meio Físico</b></td>
      <td>Cabo UTP Direto (<i>Copper Straight-Through</i>)</td>
      <td>Vários</td>
      <td>Interligação das portas FastEthernet e enlaces de uplink GigabitEthernet</td>
    </tr>
  </tbody>
</table>

<hr/>

<h2>🗺️ 3. Tabela de Endereçamento IP</h2>

<table width="100%">
  <thead>
    <tr bgcolor="#1f242c">
      <th align="left">Dispositivo</th>
      <th align="left">Interface</th>
      <th align="left">Endereço IPv4</th>
      <th align="left">Máscara de Sub-rede</th>
      <th align="left">Gateway Padrão</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>PC-Lab01</b></td>
      <td><code>FastEthernet0</code></td>
      <td><code>192.168.1.10</code></td>
      <td><code>255.255.255.0</code></td>
      <td><code>192.168.1.1</code></td>
    </tr>
    <tr>
      <td><b>PC-Lab02</b></td>
      <td><code>FastEthernet0</code></td>
      <td><code>192.168.1.11</code></td>
      <td><code>255.255.255.0</code></td>
      <td><code>192.168.1.1</code></td>
    </tr>
    <tr>
      <td><b>PC-Sec01</b></td>
      <td><code>FastEthernet0</code></td>
      <td><code>192.168.1.20</code></td>
      <td><code>255.255.255.0</code></td>
      <td><code>192.168.1.1</code></td>
    </tr>
    <tr>
      <td><b>PC-Sec02</b></td>
      <td><code>FastEthernet0</code></td>
      <td><code>192.168.1.21</code></td>
      <td><code>255.255.255.0</code></td>
      <td><code>192.168.1.1</code></td>
    </tr>
    <tr>
      <td><b>Roteador-Core</b></td>
      <td><code>GigabitEthernet0/0/0</code></td>
      <td><code>192.168.1.1</code></td>
      <td><code>255.255.255.0</code></td>
      <td><i>N/A (Interface Local)</i></td>
    </tr>
  </tbody>
</table>

<hr/>

<h2>💻 4. Configurações Realizadas</h2>

<details open>
  <summary><b>Etapa 1: Montagem Física e Gestão Energética</b></summary>
  <br/>
  <ul>
    <li>Disposição dos ativos na área de trabalho respeitando a hierarquia visual (Core no topo, Distribuição no meio e Acesso na base).</li>
    <li><b>Alimentação Energética:</b> Inserção física do módulo de fonte de alimentação <code>AC Power Supply</code> no slot traseiro do switch Catalyst 3650 (Distribuição) para permitir sua inicialização.</li>
  </ul>
</details>

<details open>
  <summary><b>Etapa 2: Mapeamento de Portas e Cabeamento</b></summary>
  <br/>
  <ul>
    <li>Conexão dos computadores finais às portas <b>FastEthernet</b> dos switches da Camada de Acesso.</li>
    <li>Conexão dos switches de Acesso para o switch de Distribuição utilizando portas de alta capacidade (<b>GigabitEthernet</b>).</li>
    <li>Conexão do enlace de Distribuição para a interface <code>GigabitEthernet0/0/0</code> do Roteador Core.</li>
  </ul>
</details>

<details open>
  <summary><b>Etapa 3: Configuração do Roteador Core via CLI (Cisco IOS)</b></summary>
  <br/>
  <pre>
Router> enable
Router# configure terminal
Router(config)# interface GigabitEthernet0/0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
  </pre>
</details>

<details>
  <summary><b>Etapa 4: Validação em Modo Simulação (PDU Flow)</b></summary>
  <br/>
  <p>
    Validação visual do encaminhamento de pacotes ICMP (PDUs) pelo modo de simulação, acompanhando a subida do tráfego das portas de acesso até a distribuição e a confirmação de rota de volta aos nós finais.
  </p>
</details>

<hr/>

<h2>🎥 5. Demonstração Visual do Laboratório</h2>

<p>Abaixo está o registro visual demonstrando a transmissão e o roteamento das PDUs ICMP trafegando pelas três camadas no Cisco Packet Tracer:</p>

<div align="center">
  <video src="https://github.com/user-attachments/assets/5fd4bf40-0b54-4418-bcfb-ce8ec6173cd6" controls="controls" width="85%" style="border-radius: 8px; box-shadow: 0px 4px 12px rgba(0,0,0,0.15);">
    Seu navegador não suporta a tag de vídeo.
  </video>
  <br/>
  <sub><i>Fluxo de pacotes ICMP percorrendo os switches de Acesso, Distribuição e Roteador Core</i></sub>
</div>

<hr/>

<h2>🧠 6. Desafios Encontrados & Reflexão Técnica</h2>

<blockquote>
  <p><b>1. Validação Criteriosa de Modelos de Hardware:</b><br/>
  Durante a montagem inicial, ocorreu a seleção de um modelo de switch de distribuição divergente por uma variação de numeração no catálogo. Essa situação evidenciou a importância de conferir minuciosamente a folha de especificações (<i>datasheet</i>) e capacidades modulares antes de iniciar o projeto.</p>

  <p><b>2. Precisão no Mapeamento de Portas e Uplinks:</b><br/>
  O cabeamento hierárquico exige atenção estrita entre portas FastEthernet (100 Mbps) e GigabitEthernet (1 Gbps). A conexão nas interfaces adequadas garante que os gargalos de tráfego sejam mitigados nos troncos de subida.</p>

  <p><b>3. Metodologia de Troubleshooting:</b><br/>
  Foi fundamental pausar a execução, auditar o esquema de ligações porta a porta e aplicar correções de forma analítica e estruturada.</p>
</blockquote>

<hr/>

<h2>🎯 7. Conclusão</h2>

<p>
A prática consolidou a compreensão dos princípios fundamentais do modelo corporativo em camadas da Cisco: alta disponibilidade, facilidade de expansão modular e simplificação na identificação de falhas na infraestrutura de rede.
</p>

<hr/>

<div align="center">
  <h3>👩‍💻 Desenvolvido por</h3>
  <p><b>Fernanda Isabelli Oliveira da Silva</b></p>
  <p>
    <a href="https://github.com/fer-isa">
      <img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white" alt="GitHub" />
    </a>
    <a href="https://www.linkedin.com/in/fernanda-isabelli/">
      <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" />
    </a>
  </p>
</div>
