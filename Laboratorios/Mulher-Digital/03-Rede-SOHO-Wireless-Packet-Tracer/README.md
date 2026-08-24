<div align="center">

  <h1>🌐 Laboratório Prático: Infraestrutura de Rede SOHO</h1>
  <p><b>Simulação de Rede Local Híbrida (Cabeada & Wi-Fi) com Servidor DHCP e Segurança WPA2-Personal</b></p>

  <p>
    <img src="https://img.shields.io/badge/Cisco%20Packet%20Tracer-005073?style=for-the-badge&logo=cisco&logoColor=white" alt="Cisco Packet Tracer" />
    <img src="https://img.shields.io/badge/Topologia-SOHO-0A84FF?style=for-the-badge" alt="SOHO" />
    <img src="https://img.shields.io/badge/Serviço-DHCP-30D158?style=for-the-badge" alt="DHCP" />
    <img src="https://img.shields.io/badge/Segurança-WPA2--PSK-FF9F0A?style=for-the-badge" alt="WPA2" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>

</div>

<hr/>

<h2>📌 1. Visão Geral do Projeto</h2>

<p>
Este projeto documenta o planejamento, arquitetura, configuração e homologação de uma rede de pequeno escritório (<b>SOHO — Small Office / Home Office</b>) desenvolvida no <b>Cisco Packet Tracer</b>.
</p>

<p>
O cenário integra conexões de alta velocidade cabeadas (<i>Copper Straight-Through</i>) e estações sem fio (<i>Wi-Fi 802.11</i>), centralizadas por um roteador multifuncional <b>Linksys WRT300N</b> responsável pelo roteamento de borda, switch de Camada 2, ponto de acesso wireless e distribuição dinâmica de endereços via <b>DHCP</b>.
</p>

<hr/>

<h2>🏗️ 2. Arquitetura da Topologia & Especificação de Hardware</h2>

<table width="100%">
  <thead>
    <tr bgcolor="#1f242c">
      <th align="left">Dispositivo</th>
      <th align="left">Modelo / Tipo</th>
      <th align="left">Interface</th>
      <th align="left">Meio Físico / Mídia</th>
      <th align="left">Função no Ecossistema</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>Cloud-PT</b></td>
      <td>Nuvem WAN</td>
      <td><code>Coaxial 7</code></td>
      <td>Cabo Coaxial</td>
      <td>Emulação do Provedor de Internet (ISP)</td>
    </tr>
    <tr>
      <td><b>Cable Modem</b></td>
      <td>Modem Banda Larga</td>
      <td><code>Port 0 / Port 1</code></td>
      <td>Coaxial / UTP Direto</td>
      <td>Modulação de sinal e conexão com a borda</td>
    </tr>
    <tr>
      <td><b>WRT300N</b></td>
      <td>Roteador Wireless</td>
      <td><code>Internet / Eth 1-3 / Wi-Fi</code></td>
      <td>Par Trançado / Rádio 2.4 GHz</td>
      <td>Gateway, Switch L2, Access Point e Servidor DHCP</td>
    </tr>
    <tr>
      <td><b>PC0</b></td>
      <td>Estação de Trabalho</td>
      <td><code>FastEthernet0</code></td>
      <td>Cabo Direto (Cat5e/Cat6)</td>
      <td>Host corporativo cabeado</td>
    </tr>
    <tr>
      <td><b>PC1</b></td>
      <td>Estação de Trabalho</td>
      <td><code>FastEthernet0</code></td>
      <td>Cabo Direto (Cat5e/Cat6)</td>
      <td>Host corporativo cabeado</td>
    </tr>
    <tr>
      <td><b>Printer</b></td>
      <td>Impressora de Rede</td>
      <td><code>FastEthernet0</code></td>
      <td>Cabo Direto (Cat5e/Cat6)</td>
      <td>Serviço de impressão compartilhado na LAN</td>
    </tr>
    <tr>
      <td><b>Laptop</b></td>
      <td>Computador Portátil</td>
      <td><code>WPC300N (Módulo Wi-Fi)</code></td>
      <td>Conexão Sem Fio (WLAN)</td>
      <td>Estação móvel corporativa</td>
    </tr>
    <tr>
      <td><b>Smart Phone</b></td>
      <td>Dispositivo Móvel</td>
      <td><code>Wireless0</code></td>
      <td>Conexão Sem Fio (WLAN)</td>
      <td>Dispositivo móvel corporativo</td>
    </tr>
  </tbody>
</table>

<hr/>

<h2>⚙️ 3. Parâmetros de Configuração & Endereçamento</h2>

<table width="100%">
  <thead>
    <tr bgcolor="#1f242c">
      <th align="left" width="50%">📶 Rede Sem Fio (WLAN)</th>
      <th align="left" width="50%">🏷️ Endereçamento Lógico (IPv4 / DHCP)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <ul>
          <li><b>SSID:</b> <code>Escritorio_Firma</code></li>
          <li><b>Modo de Segurança:</b> <code>WPA2-Personal</code></li>
          <li><b>Criptografia:</b> <code>AES</code></li>
          <li><b>Chave de Acesso:</b> <code>senha12345</code></li>
        </ul>
      </td>
      <td>
        <ul>
          <li><b>Sub-rede:</b> <code>192.168.0.0/24</code></li>
          <li><b>Gateway Padrão:</b> <code>192.168.0.1</code></li>
          <li><b>Máscara de Sub-rede:</b> <code>255.255.255.0</code></li>
          <li><b>Atribuição:</b> Dinâmica via DHCP Pool</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

<hr/>

<h2>📋 4. Passo a Passo da Implementação</h2>

<details open>
  <summary><b>Etapa 1: Cabeamento Estruturado e Conexões Físicas</b></summary>
  <br/>
  <ul>
    <li>Conexão WAN: <b>Cloud-PT</b> (Porta Coaxial 7) conectada à porta <b>Port 0</b> do Cable Modem via cabo coaxial.</li>
    <li>Conexão Modem-Roteador: <b>Cable Modem</b> (Port 1) conectado à porta <b>Internet</b> do WRT300N via cabo direto.</li>
    <li>Conexão LAN Cabeada: <b>PC0</b> (Ethernet 1), <b>PC1</b> (Ethernet 2) e <b>Printer</b> (Ethernet 3) interligados com cabo par trançado direto.</li>
  </ul>
</details>

<details>
  <summary><b>Etapa 2: Hardening e Configuração do Roteador WRT300N</b></summary>
  <br/>
  <ul>
    <li>Acesso à interface gráfica (<i>GUI</i>) do roteador.</li>
    <li>Definição do SSID da rede wireless para <code>Escritorio_Firma</code>.</li>
    <li>Aplicação de criptografia WPA2-Personal com chave pré-compartilhada para evitar acessos não autorizados.</li>
  </ul>
</details>

<details>
  <summary><b>Etapa 3: Customização de Hardware no Laptop e Conexão Wi-Fi</b></summary>
  <br/>
  <ul>
    <li>Desligamento físico do Laptop no módulo de energia.</li>
    <li>Remoção da placa cabeada padrão RJ-45 e inserção do módulo de rádio wireless <code>WPC300N</code>.</li>
    <li>Inicialização do sistema operacional e associação à rede <code>Escritorio_Firma</code> via utilitário <i>PC Wireless</i>.</li>
  </ul>
</details>

<details>
  <summary><b>Etapa 4: Habilitação de DHCP em Todos os Dispositivos Finais</b></summary>
  <br/>
  <ul>
    <li>Configuração das interfaces de rede dos PCs, Laptop, Smartphone e Impressora para o modo <b>DHCP</b>.</li>
    <li>Lease automático de endereçamento IP, máscara e gateway padrão concedido pelo WRT300N.</li>
  </ul>
</details>

<hr/>

<h2>🧪 5. Validação e Homologação de Conectividade</h2>

<p><b>A. Verificação de Endereço IP (PC0 via Prompt de Comando):</b></p>

<pre>
PC> ipconfig

FastEthernet0 Connection:
   IP Address......................: 192.168.0.100
   Subnet Mask.....................: 255.255.255.0
   Default Gateway.................: 192.168.0.1
   DHCP Server.....................: 192.168.0.1
</pre>

<p><b>B. Teste de Conectividade ICMP (PC0 $\to$ Impressora de Rede <code>192.168.0.102</code>):</b></p>

<pre>
PC> ping 192.168.0.102

Pinging 192.168.0.102 with 32 bytes of data:

Reply from 192.168.0.102: bytes=32 time=1ms TTL=128
Reply from 192.168.0.102: bytes=32 time=1ms TTL=128
Reply from 192.168.0.102: bytes=32 time=1ms TTL=128
Reply from 192.168.0.102: bytes=32 time=1ms TTL=128

Ping statistics for 192.168.0.102:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 1ms, Maximum = 1ms, Average = 1ms
</pre>

<blockquote>
  <b>✅ Conclusão dos Testes:</b> Comunicação bidirecional estabelecida com 0% de perda de pacotes, confirmando a interoperabilidade da rede local.
</blockquote>

<hr/>

<h2>💡 6. Competências Técnicas Desenvolvidas</h2>

<ul>
  <li><b>Design de Redes SOHO:</b> Compreensão e montagem de topologias integradas combinando cabeamento estruturado e redes sem fio.</li>
  <li><b>Segurança em Redes Wi-Fi:</b> Implementação de controle de autenticação e criptografia robusta (WPA2-PSK/AES).</li>
  <li><b>Serviços Essenciais de Infraestrutura:</b> Configuração e validação prática do protocolo DHCP para automação de endereçamento.</li>
  <li><b>Diagnóstico e Troubleshooting:</b> Validação e testes de fluxo de pacotes através de ferramentas de linha de comando (CLI/ICMP).</li>
</ul>

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
