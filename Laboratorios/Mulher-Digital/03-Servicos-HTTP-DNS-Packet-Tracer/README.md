<div align="center">

  <h1>🌐 Laboratório 2: Serviços HTTP & DNS</h1>
  <p><b>Configuração de serviços de aplicação e análise de protocolos nas camadas 4 e 7 do Modelo OSI</b></p>

  <p>
    <img src="https://img.shields.io/badge/Cisco-Packet_Tracer-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white" alt="Cisco Packet Tracer" />
    <img src="https://img.shields.io/badge/Protocolos-HTTP%20%7C%20DNS-blue?style=for-the-badge" alt="HTTP e DNS" />
    <img src="https://img.shields.io/badge/Trilha-Mulher_Digital_Redes-8A2BE2?style=for-the-badge" alt="Mulher Digital" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>

</div>

<hr/>

<h2>📌 1. Objetivo da Atividade</h2>

<p>
Configurar uma rede local com serviços da camada de aplicação (<b>HTTP</b> e <b>DNS</b>) em um servidor dedicado, validando a comunicação, a resolução de nomes de domínio e o encapsulamento de pacotes (<b>Camadas 4 e 7 do Modelo OSI</b>) através de utilitários de rede (<code>ping</code> e <code>nslookup</code>) e do modo de simulação do Cisco Packet Tracer.
</p>

<hr/>

<h2>🏗️ 2. Topologia & Montagem Física</h2>

<h3>📦 Equipamentos Utilizados</h3>
<ul>
  <li><b>Switch de Acesso:</b> Cisco Catalyst 2960 (1 unidade)</li>
  <li><b>Dispositivo Final (Cliente):</b> PC genérico (<code>PC-Cliente</code>)</li>
  <li><b>Servidor Dedicado:</b> Servidor genérico (<code>Servidor-Central</code>)</li>
  <li><b>Meio de Transmissão:</b> Cabo de par trançado direto (<i>Copper Straight-Through</i>)</li>
</ul>

<h3>🔌 Mapeamento de Conexões</h3>

<table width="100%">
  <thead>
    <tr bgcolor="#1f242c">
      <th align="left">Dispositivo de Origem</th>
      <th align="left">Interface de Origem</th>
      <th align="left">Dispositivo de Destino</th>
      <th align="left">Interface de Destino</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>PC-Cliente</b></td>
      <td><code>FastEthernet0</code></td>
      <td><b>Switch 2960</b></td>
      <td><code>FastEthernet0/1</code></td>
    </tr>
    <tr>
      <td><b>Servidor-Central</b></td>
      <td><code>FastEthernet0</code></td>
      <td><b>Switch 2960</b></td>
      <td><code>FastEthernet0/2</code></td>
    </tr>
  </tbody>
</table>

<hr/>

<h2>⚙️ 3. Endereçamento IP</h2>

<p>Configurações estáticas aplicadas em <b>Desktop</b> → <b>IP Configuration</b>:</p>

<table width="100%">
  <thead>
    <tr bgcolor="#1f242c">
      <th align="left">Dispositivo</th>
      <th align="left">Endereço IPv4</th>
      <th align="left">Máscara de Sub-rede</th>
      <th align="left">Gateway Padrão</th>
      <th align="left">Servidor DNS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>Servidor-Central</b></td>
      <td><code>192.168.1.10</code></td>
      <td><code>255.255.255.0</code></td>
      <td><i>Não configurado</i></td>
      <td><i>Não configurado</i></td>
    </tr>
    <tr>
      <td><b>PC-Cliente</b></td>
      <td><code>192.168.1.5</code></td>
      <td><code>255.255.255.0</code></td>
      <td><i>Não configurado</i></td>
      <td><code>192.168.1.10</code></td>
    </tr>
  </tbody>
</table>

<hr/>

<h2>🛠️ 4. Configuração dos Serviços (Servidor-Central)</h2>

<details open>
  <summary><b>A. Servidor Web (HTTP / HTTPS)</b></summary>
  <br/>
  <ol>
    <li>Acesse a aba <b>Services</b> → menu <b>HTTP</b> e garanta que os serviços <b>HTTP</b> e <b>HTTPS</b> estejam marcados como <code>On</code>.</li>
    <li>Na lista de arquivos do servidor, localize o arquivo <code>index.html</code> e clique em <b>Edit</b>.</li>
    <li>Personalize o conteúdo da página web:
      <ul>
        <li>Altere a tag de título para: <code>&lt;h1&gt;Bem-vinda à aula de Redes!&lt;/h1&gt;</code></li>
        <li>Altere o corpo do texto para: <code>&lt;p&gt;Esta é a nossa primeira página web configurada e testada no laboratório!&lt;/p&gt;</code></li>
      </ul>
    </li>
    <li>Clique em <b>Save</b> e confirme a substituição do arquivo.</li>
  </ol>
</details>

<details open>
  <summary><b>B. Servidor de Nomes de Domínio (DNS)</b></summary>
  <br/>
  <ol>
    <li>Acesse o menu <b>DNS</b> na aba <b>Services</b> e ative o serviço (<code>On</code>).</li>
    <li>Crie uma nova entrada de registro preenchendo os seguintes parâmetros:
      <ul>
        <li><b>Name:</b> <code>www.aula.com</code></li>
        <li><b>Type:</b> <code>A Record</code> (Mapeamento de Host para IPv4)</li>
        <li><b>Address:</b> <code>192.168.1.10</code></li>
      </ul>
    </li>
    <li>Clique no botão <b>Add</b> para registrar a resolução de nomes.</li>
  </ol>
</details>

<hr/>

<h2>🔍 5. Validação com Utilitários de Rede</h2>

<p>No <b>PC-Cliente</b> → aba <b>Desktop</b> → <b>Command Prompt</b>:</p>

<h3>Teste 1: Conectividade Básica (ICMP / Ping)</h3>
<pre>
PC> ping 192.168.1.10

Pinging 192.168.1.10 with 32 bytes of data:

Reply from 192.168.1.10: bytes=32 time&lt;1ms TTL=128
Reply from 192.168.1.10: bytes=32 time&lt;1ms TTL=128
Reply from 192.168.1.10: bytes=32 time&lt;1ms TTL=128
Reply from 192.168.1.10: bytes=32 time&lt;1ms TTL=128

Ping statistics for 192.168.1.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
</pre>

<h3>Teste 2: Resolução de Nomes (nslookup)</h3>
<pre>
PC> nslookup www.aula.com

Server:  192.168.1.10
Address: 192.168.1.10

Name:    www.aula.com
Address: 192.168.1.10
</pre>

<hr/>

<h2>🔬 6. Análise de Protocolos (Modo Simulação)</h2>

<ol>
  <li>No canto inferior direito do Cisco Packet Tracer, alterne o modo de operação de <b>Realtime</b> para <b>Simulation</b>.</li>
  <li>Clique em <b>Show All/None</b> e em seguida em <b>Edit Filters</b>.</li>
  <li>Selecione exclusivamente os protocolos de interesse: <code>DNS</code>, <code>TCP</code>, <code>HTTP</code> e <code>ICMP</code>.</li>
  <li>No <b>PC-Cliente</b>, abra o <b>Web Browser</b>, insira a URL <code>http://www.aula.com</code> na barra de endereços e clique em <b>Go</b>.</li>
  <li>Utilize o botão <b>Capture/Forward</b> para avançar passo a passo e inspecionar o fluxo e encapsulamento das PDUs (Unidades de Dados de Protocolo) nas camadas 4 (Transporte) e 7 (Aplicação).</li>
</ol>

<hr/>

<h2>📥 7. Arquivos do Laboratório</h2>

<p>
  <a href="https://github.com/fer-isa">
    <img src="https://img.shields.io/badge/Download-Laboratório_.PKT-0A84FF?style=for-the-badge&logo=cisco&logoColor=white" alt="Download PKT" />
  </a>
</p>

<blockquote>
  <b>💡 Como baixar o arquivo <code>.pkt</code> no GitHub:</b><br/>
  1. Clique no botão de download acima para abrir a pasta do laboratório no repositório.<br/>
  2. Localize o arquivo <code>lab-servicos-http-dns.pkt</code>.<br/>
  3. No canto superior direito da tela do GitHub, clique no <b>ícone de Download</b> (seta para baixo ⬇️) ao lado do botão <i>Raw</i>.
</blockquote>

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
