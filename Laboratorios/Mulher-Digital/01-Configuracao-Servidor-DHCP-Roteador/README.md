<div align="center">

  <h1>🧪 Laboratório: Configuração de Servidor DHCP no Roteador Cisco</h1>
  <p><b>Implementação e distribuição dinâmica de endereçamento IPv4 em roteadores Cisco via CLI</b></p>

  <p>
    <img src="https://img.shields.io/badge/Cisco-Packet_Tracer-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white" alt="Cisco Packet Tracer" />
    <img src="https://img.shields.io/badge/Protocolo-DHCP-2ea44f?style=for-the-badge" alt="DHCP" />
    <img src="https://img.shields.io/badge/CLI-Cisco_IOS-0A84FF?style=for-the-badge" alt="Cisco IOS" />
    <img src="https://img.shields.io/badge/Trilha-Mulher_Digital_Redes-8A2BE2?style=for-the-badge" alt="Mulher Digital" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>

</div>

<hr/>
<h2>🎯 1. Propósito & Objetivos Técnicos</h2>

<p>
O objetivo deste laboratório prático é consolidar as habilidades de configuração de serviços essenciais de camada de rede e aplicação no ambiente <b>Cisco IOS</b>. A atividade foca na implementação do serviço <b>DHCP (Dynamic Host Configuration Protocol)</b> em um roteador de borda para automação da entrega de parâmetros de rede (IPv4, Gateway, DNS e Máscara).
</p>

<ul>
  <li><b>Objetivo Principal:</b> Eliminar o esforço operacional de endereçamento estático e mitigar erros humanos e duplicação de endereços IP na LAN.</li>
  <li><b>Propósito Arquitetural:</b> Estruturar um pool de endereçamento com reserva segura para gateways/servidores e garantir conectividade ponta a ponta.</li>
</ul>

<hr/>
<h2>🏗️ 2. Topologia & Montagem Física</h2>

<h3>📦 Inventário de Equipamentos</h3>
<ul>
  <li><b>Roteador de Borda:</b> Cisco 2911 (1 unidade) — Interface <code>GigabitEthernet0/0</code></li>
  <li><b>Switch de Acesso:</b> Cisco Catalyst 2960-24TT (1 unidade)</li>
  <li><b>Hosts Finais:</b> 2 PCs (<code>PC0</code> e <code>PC1</code>)</li>
  <li><b>Meio de Transmissão:</b> Cabos de par trançado direto (<i>Copper Straight-Through</i>)</li>
</ul>

<h3>🗺️ Tabela de Endereçamento e Planejamento</h3>

<table>
  <thead>
    <tr>
      <th>Dispositivo</th>
      <th>Interface</th>
      <th>Endereço IP</th>
      <th>Máscara de Sub-rede</th>
      <th>Gateway Padrão</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>Router0</b></td>
      <td>Gig0/0</td>
      <td><code>192.168.1.1</code></td>
      <td><code>255.255.255.0</code> (/24)</td>
      <td>N/A</td>
    </tr>
    <tr>
      <td><b>PC0</b></td>
      <td>FastEthernet0</td>
      <td><i>DHCP (Ex: 192.168.1.11)</i></td>
      <td><code>255.255.255.0</code></td>
      <td><code>192.168.1.1</code></td>
    </tr>
    <tr>
      <td><b>PC1</b></td>
      <td>FastEthernet0</td>
      <td><i>DHCP (Ex: 192.168.1.12)</i></td>
      <td><code>255.255.255.0</code></td>
      <td><code>192.168.1.1</code></td>
    </tr>
  </tbody>
</table>

<!-- ================= ESPAÇO: PRINT DA TOPOLOGIA ================= -->
<div align="center" style="margin: 25px 0;">
  <div style="border: 2px dashed #1BA0D7; padding: 20px; border-radius: 8px; background-color: #f8fafc; max-width: 720px;">
    <h3>📸 [PRINT 1]: Topologia da Rede no Cisco Packet Tracer</h3>
    <p><i>Cole aqui a imagem da topologia física com Router, Switch e PCs conectados (links verdes).</i></p>
    <img src="./assets/topologia-packet-tracer.png" alt="Topologia da Rede no Cisco Packet Tracer" width="100%" style="border-radius: 6px;" />
  </div>
</div>

<hr/>
<h2>⚙️ 3. Procedimento Passo a Passo via CLI</h2>

<h3>Passo 3.1: Configuração da Interface LAN do Roteador</h3>
<p>Habilitar e atribuir o IP de gateway na interface local:</p>

<pre><code>Router&gt; enable
Router# configure terminal
Router(config)# hostname R1
R1(config)# interface GigabitEthernet 0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# no shutdown
R1(config-if)# exit</code></pre>

<h3>Passo 3.2: Definição da Faixa de Exclusão (Reserva de IPs)</h3>
<p>Garantir que os endereços de <code>.1</code> a <code>.10</code> fiquem reservados para infraestrutura e servidores:</p>

<pre><code>R1(config)# ip dhcp excluded-address 192.168.1.1 192.168.1.10</code></pre>

<h3>Passo 3.3: Criação e Escopo do Pool DHCP</h3>
<p>Definição do bloco de rede, gateway padrão e servidor DNS:</p>

<pre><code>R1(config)# ip dhcp pool POOL_LAN
R1(dhcp-config)# network 192.168.1.0 255.255.255.0
R1(dhcp-config)# default-router 192.168.1.1
R1(dhcp-config)# dns-server 8.8.8.8
R1(dhcp-config)# end
R1# write memory</code></pre>

<!-- ================= ESPAÇO: PRINT DO CLI ================= -->
<div align="center" style="margin: 25px 0;">
  <div style="border: 2px dashed #0A84FF; padding: 20px; border-radius: 8px; background-color: #f8fafc; max-width: 720px;">
    <h3>📸 [PRINT 2]: Comandos de Configuração na CLI do Roteador</h3>
    <p><i>Cole aqui a imagem do terminal do Roteador mostrando os comandos digitados e o salvamento.</i></p>
    <img src="./assets/cli-config-dhcp.png" alt="Comandos de Configuração na CLI" width="100%" style="border-radius: 6px;" />
  </div>
</div>

<hr/>
<h2>🔍 4. Validação, Testes & Comandos de Diagnóstico</h2>

<h3>Passo 4.1: Obtenção de Endereço nos Endpoints</h3>
<p>Nos PCs, acesse <code>Desktop &gt; IP Configuration</code> e marque <b>DHCP</b> para receber os parâmetros.</p>

<!-- ================= ESPAÇO: PRINT DHCP NOS PCS ================= -->
<div align="center" style="margin: 25px 0;">
  <div style="border: 2px dashed #2ea44f; padding: 20px; border-radius: 8px; background-color: #f8fafc; max-width: 720px;">
    <h3>📸 [PRINT 3]: Atribuição Dinâmica nos Computadores (PC0 e PC1)</h3>
    <p><i>Cole aqui o print da janela IP Configuration mostrando a mensagem "DHCP request successful".</i></p>
    <img src="./assets/pc-dhcp-success.png" alt="IP Configuration via DHCP no PC" width="100%" style="border-radius: 6px;" />
  </div>
</div>

<h3>Passo 4.2: Auditoria de Leases no Roteador</h3>
<p>Verificação das concessões ativas na memória do roteador:</p>

<pre><code>R1# show ip dhcp binding
R1# show ip dhcp pool</code></pre>

<!-- ================= ESPAÇO: PRINT SHOW IP DHCP BINDING ================= -->
<div align="center" style="margin: 25px 0;">
  <div style="border: 2px dashed #8A2BE2; padding: 20px; border-radius: 8px; background-color: #f8fafc; max-width: 720px;">
    <h3>📸 [PRINT 4]: Tabela de Concessões Ativas (show ip dhcp binding)</h3>
    <p><i>Cole aqui a saída do comando com a lista de IPs e MAC Addresses vinculados.</i></p>
    <img src="./assets/show-ip-dhcp-binding.png" alt="Saída do comando show ip dhcp binding" width="100%" style="border-radius: 6px;" />
  </div>
</div>

<h3>Passo 4.3: Teste de Conectividade (ICMP Ping)</h3>
<p>Validação da conectividade bidirecional entre os hosts e o gateway:</p>

<!-- ================= ESPAÇO: PRINT DO PING ================= -->
<div align="center" style="margin: 25px 0;">
  <div style="border: 2px dashed #30363d; padding: 20px; border-radius: 8px; background-color: #f8fafc; max-width: 720px;">
    <h3>📸 [PRINT 5]: Teste de Ping com 0% de Perda</h3>
    <p><i>Cole aqui a tela do Command Prompt executando ping com sucesso para o gateway e entre PCs.</i></p>
    <img src="./assets/teste-ping-sucesso.png" alt="Teste de Ping com Sucesso no Command Prompt" width="100%" style="border-radius: 6px;" />
  </div>
</div>

<hr/>
<h2>💡 5. Aprendizados & Conclusões Técnicas</h2>

<ul>
  <li><b>Compreensão do Ciclo DORA:</b> Análise prática das quatro fases fundamentais de negociação (<i>Discover, Offer, Request, Acknowledgment</i>).</li>
  <li><b>Gestão Segura de Escopo:</b> Entendimento da importância de configurar <code>ip dhcp excluded-address</code> antes do pool para blindar endereços de infraestrutura.</li>
  <li><b>Troubleshooting com Cisco IOS:</b> Prática com comandos de inspeção e auditoria (<code>show ip dhcp binding</code>, <code>show ip dhcp pool</code>).</li>
  <li><b>Domínio de CLI:</b> Fortalecimento da fluência na linha de comando e boas práticas de persistência de configuração (<code>write memory</code>).</li>
</ul>
<hr/>

<div align="center" style="margin-top: 30px; padding: 15px;">
  <p style="font-size: 1.1em; color: #2d3748; margin-bottom: 8px;">
    🚀 <b>Desenvolvido por Fernanda</b> | <i>Trilha Mulher Digital & Cisco Networking</i>
  </p>
  <p>
    <img src="https://img.shields.io/badge/Autor-Fernanda-8A2BE2?style=flat-square&logo=cisco&logoColor=white" alt="Autor Fernanda" />
    <img src="https://img.shields.io/badge/Foco-Redes%20%26%20Infra-0A84FF?style=flat-square" alt="Foco" />
  </p>
</div>
