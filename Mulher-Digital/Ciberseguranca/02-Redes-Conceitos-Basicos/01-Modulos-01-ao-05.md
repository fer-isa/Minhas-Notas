<div align="center">

  <img src="../../assets/introduction-to-cybersecurity.png" width="180" alt="Conceitos Básicos de Redes" />

  <h1>🌐 Conceitos Básicos de Redes — Módulos 1 ao 5</h1>
  <p><b>Formação Mulher Digital • Trilha de Cibersegurança & Infraestrutura</b></p>

  <p>
    <img src="https://img.shields.io/badge/Cisco_Networking_Academy-Redes_de_Computadores-005073?style=for-the-badge&logo=cisco&logoColor=white" alt="Redes" />
    <img src="https://img.shields.io/badge/Modelos-OSI_%7C_TCP%2FIP-0A84FF?style=for-the-badge" alt="OSI e TCP/IP" />
    <img src="https://img.shields.io/badge/Trilha-Mulher_Digital-8A2BE2?style=for-the-badge" alt="Mulher Digital" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>

</div>

<hr/>

<h2>📌 Visão Geral</h2>

<p>
Este documento consolida os conceitos essenciais de arquitetura e infraestrutura de redes de computadores dos <b>Módulos 1 ao 5</b>, abrangendo desde a taxonomia e escopo geográfico de redes até os modelos de comunicação em camadas (<b>Modelo OSI</b> e <b>Pilha TCP/IP</b>), dispositivos de interconexão e meios físicos de transmissão.
</p>

<hr/>

<details open>
  <summary><h2>🏗️ Módulo 1: Fundamentos, Escopo e Unidades de Medida</h2></summary>
  <br/>

  <ul>
    <li><b>Definição de Rede:</b> Conjunto de dispositivos autônomos interconectados por meios físicos ou sem fio que compartilham dados, recursos e serviços através de protocolos padronizados.</li>
    <li><b>Classificação por Escopo Organizacional:</b>
      <ul>
        <li><b>Rede Doméstica:</b> Conexão local simplificada de computadores e dispositivos móveis centralizados por um roteador Wi-Fi integrado.</li>
        <li><b>SOHO (Small Office / Home Office):</b> Estrutura compacta desenhada para pequenos escritórios, comércio local e ambientes de teletrabalho.</li>
        <li><b>Média e Grande Empresa:</b> Infraestruturas complexas e altamente segmentadas com switches gerenciáveis, roteadores dedicados, firewalls corporativos e alta redundância.</li>
      </ul>
    </li>
  </ul>

  <h3>📊 Unidades de Medida em Redes</h3>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left" width="20%">Unidade</th>
        <th align="center" width="15%">Símbolo</th>
        <th align="left" width="35%">Definição Conceitual</th>
        <th align="left" width="30%">Aplicação Principal</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>Bit</b></td>
        <td align="center"><code>b</code></td>
        <td>Menor unidade elementar de informação binária (0 ou 1).</td>
        <td>Taxas de transmissão e largura de banda (ex: Mbps, Gbps).</td>
      </tr>
      <tr>
        <td><b>Byte</b></td>
        <td align="center"><code>B</code></td>
        <td>Conjunto ordenado de 8 bits (representa 1 caractere).</td>
        <td>Capacidade de armazenamento e tamanho de arquivos (ex: MB, GB).</td>
      </tr>
    </tbody>
  </table>
</details>

<hr/>

<details open>
  <summary><h2>🖥️ Módulo 2: Arquitetura, Dispositivos e Classificação Geográfica</h2></summary>
  <br/>

  <h3>Modelos de Comunicação</h3>
  <ul>
    <li><b>Cliente-Servidor:</b> O dispositivo <i>Cliente</i> requisita serviços ou dados e o <i>Servidor</i> centralizado processa, autentica e entrega a resposta (ex: Servidores Web, DNS, E-mail, Banco de Dados).</li>
    <li><b>Ponto a Ponto (P2P / Peer-to-Peer):</b> Todos os nós da rede operam simultaneamente como clientes e servidores, compartilhando recursos sem dependência de um servidor centralizado.</li>
  </ul>

  <h3>Dispositivos de Rede</h3>
  <ul>
    <li><b>Dispositivos Finais (Hosts / End Devices):</b> Equipamentos que atuam como origem ou destino final do fluxo de dados (PCs, laptops, servidores, impressoras de rede, smartphones).</li>
    <li><b>Dispositivos Intermediários:</b> Equipamentos que gerenciam o fluxo, regeneram sinais, tomam decisões de encaminhamento e asseguram a conectividade (switches de Camada 2/3, roteadores de borda, firewalls, pontos de acesso wireless).</li>
  </ul>

  <h3>Classificação por Abrangência Geográfica</h3>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left" width="15%">Sigla</th>
        <th align="left" width="35%">Nome Completo</th>
        <th align="left" width="50%">Escopo / Raio de Cobertura</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>PAN</b></td>
        <td><i>Personal Area Network</i></td>
        <td>Rede de espaço pessoal de curtíssimo alcance (tecnologia Bluetooth, periféricos sem fio, smartwatches).</td>
      </tr>
      <tr>
        <td><b>LAN</b></td>
        <td><i>Local Area Network</i></td>
        <td>Rede local com limites geográficos restritos (residência, laboratório acadêmico, escritório, andar de edifício).</td>
      </tr>
      <tr>
        <td><b>MAN</b></td>
        <td><i>Metropolitan Area Network</i></td>
        <td>Rede metropolitana que interliga múltiplos prédios e campi dentro dos limites de uma cidade ou região.</td>
      </tr>
      <tr>
        <td><b>WAN</b></td>
        <td><i>Wide Area Network</i></td>
        <td>Rede de longa distância que conecta diferentes cidades, estados, países e continentes (ex: a Internet).</td>
      </tr>
    </tbody>
  </table>
</details>

<hr/>

<details open>
  <summary><h2>📡 Módulo 3: Meios Físicos de Transmissão & Redes Sem Fio</h2></summary>
  <br/>

  <ul>
    <li><b>Redes Sem Fio (Wireless / WLAN):</b> Propagação de sinais de dados através de ondas de radiofrequência (espectro 2.4 GHz e 5 GHz), oferecendo mobilidade aos clientes (padrões IEEE 802.11).</li>
    <li><b>Meios de Transmissão Cabeados:</b>
      <ul>
        <li><b>Par Trançado de Cobre (UTP / STP):</b> Utiliza pulsos elétricos para transmissão em distâncias de até 100 metros. O trançamento dos pares cancela interferências eletromagnéticas (EMI) e ruídos de <i>crosstalk</i>.</li>
        <li><b>Fibra Óptica (Monomodo e Multimodo):</b> Transmissão de dados na forma de pulsos de luz em núcleos de vidro, imune a interferências eletromagnéticas e ideal para enlaces de longa distância e altíssima largura de banda.</li>
      </ul>
    </li>
  </ul>
</details>

<hr/>

<details open>
  <summary><h2>📐 Módulos 4 & 5: Modelos Conceituais em Camadas e Protocolos</h2></summary>
  <br/>

  <p>
    Os <b>protocolos de rede</b> constituem o conjunto formal de regras, sintaxes e padrões que viabilizam a comunicação e interoperabilidade entre sistemas heterogêneos.
  </p>

  <h3>Comparativo Estruturado: Modelo OSI vs. Pilha TCP/IP</h3>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left" width="30%">Camada Modelo OSI (7 Camadas)</th>
        <th align="left" width="30%">Camada Pilha TCP/IP (4 Camadas)</th>
        <th align="left" width="40%">Exemplos de Protocolos & PDUs</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>7. Aplicação</b></td>
        <td rowspan="3" valign="middle"><b>Aplicação</b><br/><i>(Interface de usuário e serviços de rede)</i></td>
        <td><code>HTTP</code>, <code>HTTPS</code>, <code>DNS</code>, <code>DHCP</code>, <code>SSH</code>, <code>FTP</code></td>
      </tr>
      <tr>
        <td><b>6. Apresentação</b></td>
        <td><code>SSL/TLS</code>, <code>JPEG</code>, <code>ASCII</code>, <code>MIME</code></td>
      </tr>
      <tr>
        <td><b>5. Sessão</b></td>
        <td><code>NetBIOS</code>, <code>RPC</code>, <code>PPTP</code></td>
      </tr>
      <tr>
        <td><b>4. Transporte</b></td>
        <td valign="middle"><b>Transporte</b><br/><i>(Controle de fluxo e integridade de ponta a ponta)</i></td>
        <td><code>TCP</code> (Orientado à conexão), <code>UDP</code> (Sem conexão)<br/><b>PDU:</b> Segmento / Datagrama</td>
      </tr>
      <tr>
        <td><b>3. Rede</b></td>
        <td valign="middle"><b>Internet</b><br/><i>(Endereçamento lógico e roteamento de pacotes)</i></td>
        <td><code>IPv4</code>, <code>IPv6</code>, <code>ICMP</code>, <code>ARP</code>, <code>OSPF</code>, <code>BGP</code><br/><b>PDU:</b> Pacote</td>
      </tr>
      <tr>
        <td><b>2. Enlace de Dados</b></td>
        <td rowspan="2" valign="middle"><b>Acesso à Rede</b><br/><i>(Endereçamento físico e sinalização física)</i></td>
        <td><code>Ethernet (IEEE 802.3)</code>, <code>Wi-Fi (802.11)</code>, <code>MAC Address</code><br/><b>PDU:</b> Quadro (Frame)</td>
      </tr>
      <tr>
        <td><b>1. Física</b></td>
        <td>Cabos UTP/STP, Fibra Óptica, Conectores RJ-45, Sinais Elétricos e Ópticos<br/><b>PDU:</b> Bits</td>
      </tr>
    </tbody>
  </table>
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
