<div align="center">

  <h1>🌐 Laboratório 2: Serviços HTTP & DNS</h1>
  <p><b>Configuração de serviços de aplicação e análise de protocolos nas camadas 4 e 7 do Modelo OSI</b></p>

  <p>
    <img src="https://img.shields.io/badge/Cisco-Packet_Tracer-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white" alt="Cisco Packet Tracer" />
    <img src="https://img.shields.io/badge/Protocolos-HTTP%20%7C%20DNS-0A84FF?style=for-the-badge" alt="HTTP e DNS" />
    <img src="https://img.shields.io/badge/Modelo_OSI-Camadas_4_e_7-blue?style=for-the-badge" alt="Modelo OSI" />
    <img src="https://img.shields.io/badge/Trilha-Mulher_Digital_Redes-8A2BE2?style=for-the-badge" alt="Mulher Digital" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>

</div>

<hr/>

<h2>🎯 1. Propósito & Objetivos Técnicos</h2>

<p>
Este laboratório aborda a implementação e validação prática dos serviços fundamentais da camada de aplicação em ambiente local. O objetivo é demonstrar como o protocolo <b>DNS (Domain Name System - UDP/53)</b> atua na resolução de nomes para endereços IP e como o protocolo <b>HTTP (Hypertext Transfer Protocol - TCP/80)</b> estabelece a sessão cliente-servidor para entrega de páginas Web.
</p>

<ul>
  <li><b>Objetivo Principal:</b> Configurar serviços integrados de Web e Resolução de Nomes em um servidor centralizado e inspecionar a troca de mensagens na pilha TCP/IP.</li>
  <li><b>Propósito Arquitetural:</b> Compreender o fluxo de encapsulamento e desencapsulamento de PDUs e a relação de dependência entre DNS e requisições HTTP.</li>
</ul>

<hr/>
<h2>🏗️ 2. Topologia & Montagem Física</h2>

<h3>📦 Inventário de Equipamentos</h3>
<ul>
  <li><b>Switch de Acesso:</b> Cisco Catalyst 2960-24TT (1 unidade)</li>
  <li><b>Dispositivo Final (Cliente):</b> 1 PC genérico (<code>PC-Cliente</code>)</li>
  <li><b>Servidor de Aplicação:</b> 1 Servidor dedicado (<code>Servidor-Central</code>)</li>
  <li><b>Meio de Transmissão:</b> Cabos de par trançado direto (<i>Copper Straight-Through</i>)</li>
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

<!-- ================= ESPAÇO: PRINT DA TOPOLOGIA ================= -->
<div align="center" style="margin: 25px 0;">
  <div style="border: 2px dashed #1BA0D7; padding: 20px; border-radius: 8px; background-color: #f8fafc; max-width: 720px;">
    <h3>📸 [PRINT 1]: Topologia do Laboratório no Cisco Packet Tracer</h3>
    <p><i>Cole aqui a captura do diagrama completo com Switch, Servidor e PC com os links verdes ativos.</i></p>
    <img src="./assets/topologia-http-dns.png" alt="Topologia HTTP e DNS no Packet Tracer" width="100%" style="border-radius: 6px;" />
  </div>
</div>

<hr/>
<h2>⚙️ 3. Plano de Endereçamento IP</h2>

<p>Configurações estáticas atribuídas em <b>Desktop</b> &rarr; <b>IP Configuration</b>:</p>

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
      <td><code>255.255.255.0</code> (/24)</td>
      <td><i>N/A</i></td>
      <td><code>127.0.0.1</code> / <code>192.168.1.10</code></td>
    </tr>
    <tr>
      <td><b>PC-Cliente</b></td>
      <td><code>192.168.1.5</code></td>
      <td><code>255.255.255.0</code> (/24)</td>
      <td><i>N/A</i></td>
      <td><code>192.168.1.10</code></td>
    </tr>
  </tbody>
</table>

<!-- ================= ESPAÇO: PRINT IP CONFIG ================= -->
<div align="center" style="margin: 25px 0;">
  <div style="border: 2px dashed #0A84FF; padding: 20px; border-radius: 8px; background-color: #f8fafc; max-width: 720px;">
    <h3>📸 [PRINT 2]: Configuração Estática de IP no PC-Cliente e Servidor</h3>
    <p><i>Cole aqui a captura da janela de IP Configuration do PC-Cliente destacando o apontamento do IP do Servidor DNS (192.168.1.10).</i></p>
    <img src="./assets/ip-configuration-pc-server.png" alt="Configuração de IP do PC e Servidor" width="100%" style="border-radius: 6px;" />
  </div>
</div>

<hr/>
<h2>🛠️ 4. Configuração dos Serviços de Aplicação (Servidor-Central)</h2>

<h3>4.1. Serviço Web (HTTP / HTTPS)</h3>
<ol>
  <li>No <b>Servidor-Central</b>, acesse a aba <b>Services</b> &rarr; menu <b>HTTP</b>.</li>
  <li>Verifique se os botões <b>HTTP</b> e <b>HTTPS</b> estão marcados como <code>On</code>.</li>
  <li>Na lista de arquivos gerenciados, localize o arquivo <code>index.html</code> e clique em <b>Edit</b>.</li>
  <li>Insira o código HTML personalizado e salve as alterações:</li>
</ol>

<pre><code>&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;Laboratório de Redes&lt;/title&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;h1&gt;Bem-vinda à aula de Redes!&lt;/h1&gt;
    &lt;p&gt;Esta é a nossa primeira página web configurada e testada no laboratório!&lt;/p&gt;
  &lt;/body&gt;
&lt;/html&gt;</code></pre>

<!-- ================= ESPAÇO: PRINT SERVIÇO HTTP ================= -->
<div align="center" style="margin: 25px 0;">
  <div style="border: 2px dashed #2ea44f; padding: 20px; border-radius: 8px; background-color: #f8fafc; max-width: 720px;">
    <h3>📸 [PRINT 3]: Edição e Habilitação do Serviço HTTP</h3>
    <p><i>Cole aqui o print da tela de edição do arquivo index.html dentro da aba Services &gt; HTTP do Servidor.</i></p>
    <img src="./assets/http-service-config.png" alt="Configuração do Serviço HTTP" width="100%" style="border-radius: 6px;" />
  </div>
</div>

<h3>4.2. Serviço de Resolução de Nomes (DNS)</h3>
<ol>
  <li>Acesse a aba <b>Services</b> &rarr; menu <b>DNS</b> e marque o serviço como <code>On</code>.</li>
  <li>Cadastre o registro de mapeamento preenchendo os parâmetros:
    <ul>
      <li><b>Name:</b> <code>www.aula.com</code></li>
      <li><b>Type:</b> <code>A Record</code></li>
      <li><b>Address:</b> <code>192.168.1.10</code></li>
    </ul>
  </li>
  <li>Clique no botão <b>Add</b> para inserir o registro na tabela autoritativa.</li>
</ol>

<!-- ================= ESPAÇO: PRINT SERVIÇO DNS ================= -->
<div align="center" style="margin: 25px 0;">
  <div style="border: 2px dashed #8A2BE2; padding: 20px; border-radius: 8px; background-color: #f8fafc; max-width: 720px;">
    <h3>📸 [PRINT 4]: Registro A Record no Serviço DNS</h3>
    <p><i>Cole aqui a tela do serviço DNS demonstrando o registro www.aula.com associado ao IP 192.168.1.10.</i></p>
    <img src="./assets/dns-service-config.png" alt="Configuração do Registro DNS" width="100%" style="border-radius: 6px;" />
  </div>
</div>

<hr/>
<h2>🔍 5. Validação com Utilitários de Rede & Navegação</h2>

<p>Testes executados a partir do <b>PC-Cliente</b> (aba <b>Desktop</b>):</p>

<h3>Teste 5.1: Teste de Conectividade ICMP (Ping)</h3>
<pre><code>PC&gt; ping 192.168.1.10

Pinging 192.168.1.10 with 32 bytes of data:

Reply from 192.168.1.10: bytes=32 time&lt;1ms TTL=128
Reply from 192.168.1.10: bytes=32 time&lt;1ms TTL=128
Reply from 192.168.1.10: bytes=32 time&lt;1ms TTL=128
Reply from 192.168.1.10: bytes=32 time&lt;1ms TTL=128

Ping statistics for 192.168.1.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)</code></pre>

<h3>Teste 5.2: Consulta de Resolução DNS (nslookup)</h3>
<pre><code>PC&gt; nslookup www.aula.com

Server:  192.168.1.10
Address: 192.168.1.10

Name:    www.aula.com
Address: 192.168.1.10</code></pre>

<!-- ================= ESPAÇO: PRINT TERMINAL (PING & NSLOOKUP) ================= -->
<div align="center" style="margin: 25px 0;">
  <div style="border: 2px dashed #30363d; padding: 20px; border-radius: 8px; background-color: #f8fafc; max-width: 720px;">
    <h3>📸 [PRINT 5]: Respostas do Ping e Consulta nslookup no Terminal</h3>
    <p><i>Cole aqui a tela do Command Prompt do PC-Cliente mostrando a execução dos comandos ping e nslookup com sucesso.</i></p>
    <img src="./assets/terminal-ping-nslookup.png" alt="Comandos de Diagnóstico no Prompt" width="100%" style="border-radius: 6px;" />
  </div>
</div>

<h3>Teste 5.3: Acesso Web via Browser</h3>
<p>No <b>PC-Cliente</b>, abra o <b>Web Browser</b>, insira a URL <code>http://www.aula.com</code> e valide a renderização da página HTML hospedada.</p>

<!-- ================= ESPAÇO: PRINT WEB BROWSER ================= -->
<div align="center" style="margin: 25px 0;">
  <div style="border: 2px dashed #0A84FF; padding: 20px; border-radius: 8px; background-color: #f8fafc; max-width: 720px;">
    <h3>📸 [PRINT 6]: Renderização da Página Web no Navegador do PC</h3>
    <p><i>Cole aqui a captura do Web Browser exibindo o título e parágrafo configurados no arquivo index.html.</i></p>
    <img src="./assets/web-browser-sucesso.png" alt="Navegador exibindo a página Web" width="100%" style="border-radius: 6px;" />
  </div>
</div>

<hr/>

<h2>🔬 6. Análise de Protocolos & Tráfego (Modo Simulação)</h2>

<ol>
  <li>No Packet Tracer, alterne do modo <b>Realtime</b> para <b>Simulation</b>.</li>
  <li>Em <b>Edit Filters</b>, filtre apenas pelos protocolos: <code>DNS</code>, <code>TCP</code>, <code>HTTP</code> e <code>ICMP</code>.</li>
  <li>No navegador do PC, requisite <code>http://www.aula.com</code> e avance o tráfego com <b>Capture/Forward</b>:</li>
</ol>

<table width="100%">
  <thead>
    <tr bgcolor="#1f242c">
      <th align="left">Etapa</th>
      <th align="left">Protocolo</th>
      <th align="left">Porta / Camada</th>
      <th align="left">Operação Técnica Realizada</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>1. Consulta DNS</b></td>
      <td><code>DNS</code></td>
      <td>UDP 53 (Camadas 4 e 7)</td>
      <td>O cliente envia consulta de registro A para obter o IP correspondente ao domínio.</td>
    </tr>
    <tr>
      <td><b>2. Three-Way Handshake</b></td>
      <td><code>TCP</code></td>
      <td>TCP 80 (Camada 4)</td>
      <td>Estabelecimento de conexão de transporte confiável via sincronização <code>SYN</code>, <code>SYN-ACK</code> e <code>ACK</code>.</td>
    </tr>
    <tr>
      <td><b>3. Requisição Web</b></td>
      <td><code>HTTP</code></td>
      <td>TCP 80 (Camadas 4 e 7)</td>
      <td>Envio da mensagem <code>GET / HTTP/1.1</code> e retorno do servidor com status <code>200 OK</code> contendo o payload HTML.</td>
    </tr>
  </tbody>
</table>

<!-- ================= ESPAÇO: PRINT SIMULAÇÃO PDU ================= -->
<div align="center" style="margin: 25px 0;">
  <div style="border: 2px dashed #e11d48; padding: 20px; border-radius: 8px; background-color: #f8fafc; max-width: 720px;">
    <h3>📸 [PRINT 7]: Inspecionando a PDU no Modo Simulação</h3>
    <p><i>Cole aqui a captura do Simulation Panel mostrando as camadas do Modelo OSI e os pacotes DNS/HTTP trafegando.</i></p>
    <img src="./assets/simulation-osi-layers.png" alt="Inspeção de PDU no Modo Simulação" width="100%" style="border-radius: 6px;" />
  </div>
</div>

<hr/>
<h2>💡 7. Aprendizados & Conclusões Técnicas</h2>

<ul>
  <li><b>Resolução de Nomes na Prática:</b> Visualização do papel crítico do DNS na abstração de endereços IP para nomes legíveis para humanos.</li>
  <li><b>Encapsulamento e Transporte:</b> Observação clara da diferença no uso do protocolo de transporte — DNS operando sobre UDP (foco em velocidade/baixo overhead) e HTTP operando sobre TCP (foco em confiabilidade e integridade).</li>
  <li><b>Diagnóstico e Troubleshooting:</b> Utilização assertiva do utilitário <code>nslookup</code> para isolar falhas de resolução antes de testar a camada de aplicação HTTP.</li>
  <li><b>Análise com o Modelo OSI:</b> Compreensão prática da descida e subida das camadas de rede durante o carregamento de uma página web.</li>
</ul>

<hr/>

<h2>📥 8. Arquivos do Laboratório</h2>

<p>
  <a href="https://github.com/fer-isa">
    <img src="https://img.shields.io/badge/Download-Laboratório_.PKT-0A84FF?style=for-the-badge&logo=cisco&logoColor=white" alt="Download PKT" />
  </a>
</p>

<blockquote>
  <b>💡 Como baixar o arquivo <code>.pkt</code> no repositório:</b><br/>
  1. Clique no botão de download acima para acessar a pasta do projeto.<br/>
  2. Localize o arquivo <code>lab-servicos-http-dns.pkt</code>.<br/>
  3. No canto superior direito, clique no <b>ícone de Download</b> (seta para baixo ⬇️) ao lado do botão <i>Raw</i>.
</blockquote>

<hr/>

<!-- ================= CARD DE AUTORIA ================= -->
<div align="center" style="margin-top: 40px; padding: 25px; border-radius: 12px; background: linear-gradient(135deg, #f6f8fa 0%, #ede9fe 100%); border: 1px solid #d8b4fe; max-width: 720px; box-shadow: 0 4px 12px rgba(138, 43, 226, 0.08);">
  
  <p style="margin: 0; font-size: 0.9em; text-transform: uppercase; letter-spacing: 2px; color: #7c3aed; font-weight: 700;">
    ✨ Autoria & Documentação ✨
  </p>
  
  <h3 style="margin: 8px 0 12px 0; color: #1e1b4b; font-size: 1.4em;">
    Desenvolvido por <b>Fernanda Isabelli Oliveira da Silva</b> 💜
  </h3>
  
  <p style="margin: 0 0 16px 0; color: #4b5563; font-size: 0.95em;">
    <i>Explorando infraestrutura de redes, telecomunicações e tecnologias Cisco.</i>
  </p>

  <p style="margin: 0;">
    <a href="https://www.linkedin.com/in/fernanda-isabelli/" target="_blank">
      <img src="https://img.shields.io/badge/LinkedIn-Fernanda%20Isabelli-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" />
    </a>
    <a href="https://github.com/fer-isa" target="_blank">
      <img src="https://img.shields.io/badge/GitHub-fer--isa-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub" />
    </a>
    <img src="https://img.shields.io/badge/Made%20with-Cisco%20Packet%20Tracer-8A2BE2?style=for-the-badge" alt="Feito com Packet Tracer" />
  </p>

</div>

