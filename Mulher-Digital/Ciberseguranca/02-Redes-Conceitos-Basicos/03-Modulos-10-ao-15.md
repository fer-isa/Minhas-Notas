<div align="center">

  <img src="../../assets/introduction-to-cybersecurity.png" width="180" alt="Conceitos Básicos de Redes - Módulos 10 ao 15" />

  <h1>🌐 Conceitos Básicos de Redes — Módulos 10 ao 15</h1>
  <p><b>Formação Mulher Digital • Trilha de Cibersegurança & Infraestrutura</b></p>

  <p>
    <img src="https://img.shields.io/badge/Cisco_Networking_Academy-Roteamento_%26_IP-005073?style=for-the-badge&logo=cisco&logoColor=white" alt="Roteamento" />
    <img src="https://img.shields.io/badge/Protocolos-DHCP_%7C_DNS_%7C_ARP-0A84FF?style=for-the-badge" alt="Protocolos" />
    <img src="https://img.shields.io/badge/Trilha-Mulher_Digital-8A2BE2?style=for-the-badge" alt="Mulher Digital" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>

</div>

<hr/>

<h2>📌 Visão Geral</h2>

<p>
Este documento consolida o fechamento da trilha de redes de computadores dos <b>Módulos 10 ao 15</b>, abrangendo o esquema estrutural de endereçamento IP (<b>IPv4 e IPv6</b>), segmentação de escopos públicos e privados, protocolos essenciais de infraestrutura e resolução (<b>DHCP, DNS e ARP</b>), mecânica de roteamento de Camada 3 e ferramentas de diagnóstico via linha de comando (CLI).
</p>

<hr/>

<details open>
  <summary><h2>🔢 1. Endereçamento IP e Máscaras de Sub-rede</h2></summary>
  <br/>

  <ul>
    <li><b>Estrutura do Endereço IP:</b> Cada endereço lógico é hierarquicamente dividido em duas partes fundamentais: a identificação da rede (<b>Network ID</b>) e a identificação exclusiva da estação na rede (<b>Host ID</b>).</li>
    <li><b>Máscara de Sub-rede:</b> Sequência de 32 bits formada por bits contíguos em <code>1</code> seguidos de bits em <code>0</code>, utilizada pelo dispositivo para delimitar a fronteira exata entre a porção de rede e a porção de host. É comumente expressa na notação decimal (<code>255.255.255.0</code>) ou <b>CIDR</b> (<code>/24</code>).</li>
  </ul>

  <h3>Tabela Comparativa: IPv4 vs. IPv6</h3>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left" width="22%">Característica</th>
        <th align="left" width="38%">IPv4</th>
        <th align="left" width="40%">IPv6</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>Comprimento do Endereço</b></td>
        <td>32 bits (4 octetos)</td>
        <td>128 bits (8 hextetos)</td>
      </tr>
      <tr>
        <td><b>Formato de Notação</b></td>
        <td>Decimal pontuado (ex: <code>192.168.1.50</code>)</td>
        <td>Hexadecimal com dois-pontos (ex: <code>2001:0db8:85a3::1</code>)</td>
      </tr>
      <tr>
        <td><b>Espaço de Endereçamento</b></td>
        <td>~4,29 bilhões ($2^{32}$) de endereços</td>
        <td>~340 undecilhões ($2^{128}$) de endereços</td>
      </tr>
      <tr>
        <td><b>Dependência de NAT</b></td>
        <td>Alta dependência para contornar o esgotamento</td>
        <td>Desnecessário (restaura o modelo de conectividade ponta a ponta)</td>
      </tr>
    </tbody>
  </table>
</details>

<hr/>

<details open>
  <summary><h2>🌍 2. Escopos de Endereçamento: IPs Públicos, Privados e Escopo IPv6</h2></summary>
  <br/>

  <h3>Arquitetura no IPv4</h3>
  <ul>
    <li><b>IPs Públicos:</b> Endereços globais exclusivos e roteáveis na Internet, alocados pela IANA/ISPs para permitir comunicação externa.</li>
    <li><b>IPs Privados (RFC 1918):</b> Faixas reservadas exclusivamente para comunicação em redes locais (LANs), bloqueadas para tráfego direto na Internet:
      <ul>
        <li>Classe A: <code>10.0.0.0/8</code> (de <code>10.0.0.0</code> a <code>10.255.255.255</code>)</li>
        <li>Classe B: <code>172.16.0.0/12</code> (de <code>172.16.0.0</code> a <code>172.31.255.255</code>)</li>
        <li>Classe C: <code>192.168.0.0/16</code> (de <code>192.168.0.0</code> a <code>192.168.255.255</code>)</li>
      </ul>
    </li>
    <li><b>NAT (<i>Network Address Translation</i>):</b> Mecanismo implementado no roteador de borda para traduzir múltiplos IPs privados da LAN para um único IP público válido durante o envio de pacotes à WAN.</li>
  </ul>

  <h3>Arquitetura no IPv6</h3>
  <ul>
    <li><b>GUA (<i>Global Unicast Address</i>):</b> Equivalente funcional ao IP público no IPv4; globalmente exclusivo e diretamente roteável na Internet (inicia tipicamente no bloco <code>2000::/3</code>).</li>
    <li><b>ULA (<i>Unique Local Address</i>):</b> Equivalente ao IP privado; utilizado para comunicação estritamente local em intranets sem rota na Internet pública (prefixos <code>fc00::/7</code> e <code>fd00::/8</code>).</li>
  </ul>
</details>

<hr/>

<details open>
  <summary><h2>🛠️ 3. Protocolos Fundamentais de Infraestrutura e Descoberta</h2></summary>
  <br/>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left" width="18%">Protocolo</th>
        <th align="center" width="18%">Camada OSI</th>
        <th align="left" width="30%">Função Operacional</th>
        <th align="left" width="34%">Mecânica de Funcionamento</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>DHCP</b></td>
        <td align="center">Aplicação (Camada 7)</td>
        <td>Atribuição automática e dinâmica de parâmetros de rede (IP, Máscara, Gateway, DNS).</td>
        <td>Processo <b>DORA</b> em 4 etapas:<br/><b>D</b>iscover $\to$ <b>O</b>ffer $\to$ <b>R</b>equest $\to$ <b>A</b>cknowledge.</td>
      </tr>
      <tr>
        <td><b>DNS</b></td>
        <td align="center">Aplicação (Camada 7)</td>
        <td>Resolução de nomes de domínio amigáveis em endereços IP roteáveis.</td>
        <td>Estrutura hierárquica e distribuída de servidores (Root, TLD, Autoritativo).</td>
      </tr>
      <tr>
        <td><b>ARP</b></td>
        <td align="center">Enlace / Rede (Camadas 2/3)</td>
        <td>Mapeamento do endereço físico MAC de destino a partir de um IP conhecido.</td>
        <td>Disparo de requisição em <i>Broadcast</i> local (<code>ARP Request</code>) e resposta em <i>Unicast</i> (<code>ARP Reply</code>).</td>
      </tr>
    </tbody>
  </table>
</details>

<hr/>

<details open>
  <summary><h2>🛣️ 4. Modos de Transmissão & Mecânica de Roteamento</h2></summary>
  <br/>

  <h3>Modos de Transmissão de Dados</h3>
  <ul>
    <li><b>Unicast:</b> Comunicação ponto a ponto entre um transmissor exclusivo e um único receptor específico (relação 1:1).</li>
    <li><b>Broadcast:</b> Envio simultâneo de pacotes de um nó para todos os dispositivos pertencentes ao mesmo domínio de difusão (relação 1:Todos).</li>
    <li><b>Multicast:</b> Envio de pacotes de uma origem para um conjunto específico e previamente inscrito de hosts clientes (relação 1:Muitos).</li>
  </ul>

  <h3>Tipos de Rotas na Tabela de Roteamento (Camada 3)</h3>
  <ul>
    <li><b>Rotas Diretamente Conectadas:</b> Redes vinculadas diretamente às interfaces físicas ativas e configuradas no roteador.</li>
    <li><b>Rotas Estáticas:</b> Caminhos de rede configurados e mantidos manualmente pelo administrador, com baixa sobrecarga de processamento.</li>
    <li><b>Rotas Dinâmicas:</b> Aprendizado e convergência automática de tabelas de rotas através de protocolos de roteamento:
      <ul>
        <li><b>RIP (<i>Routing Information Protocol</i>):</b> Protocolo vetor de distância baseado em contagem de saltos (máximo de 15 saltos).</li>
        <li><b>OSPF (<i>Open Shortest Path First</i>):</b> Protocolo estado de enlace (*Link-State*) que calcula o caminho mais curto com base em custo e largura de banda.</li>
      </ul>
    </li>
  </ul>
</details>

<hr/>

<details open>
  <summary><h2>💻 5. Diagnóstico e Solução de Problemas via CLI</h2></summary>
  <br/>

  <p>Comandos essenciais utilizados no Prompt de Comando / Terminal para verificação e troubleshooting de rede:</p>

  <pre>
# 1. Exibir detalhes completos de adaptadores de rede, MAC, IP, Gateway e DHCP
ipconfig /all

# 2. Exibir a tabela de cache ARP (mapeamento de endereços IP vinculados a MACs na rede local)
arp -a

# 3. Rastrear cada salto (hop) de roteadores intermediários até o endereço de destino
tracert 8.8.8.8

# 4. Testar a conectividade ICMP e medir o tempo de ida e volta (RTT) dos pacotes
ping 192.168.1.1
  </pre>
</details>

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
