
<div align="center">

  <h1>🧪 Laboratório: Configuração de Servidor DHCP no Roteador</h1>
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

<h2>📌 1. Objetivo da Atividade</h2>

<p>
Configurar um roteador Cisco para atuar como <b>Servidor DHCP (Dynamic Host Configuration Protocol)</b>, distribuindo de forma automatizada os parâmetros fundamentais de rede (<b>Endereço IP</b>, <b>Máscara de Sub-rede</b>, <b>Gateway Padrão</b> e <b>Servidor DNS</b>) para os computadores da rede local (LAN), eliminando a necessidade de configuração estática manual e prevenindo conflitos de IP.
</p>

<hr/>

<h2>🏗️ 2. Topologia & Montagem Física</h2>

<h3>📦 Equipamentos Utilizados</h3>
<ul>
  <li><b>Roteador:</b> Cisco 2911 (1 unidade)</li>
  <li><b>Switch de Acesso:</b> Cisco Catalyst 2960 (1 unidade)</li>
  <li><b>Hosts Finais:</b> 2 PCs genéricos (<code>PC0</code> e <code>PC1</code>)</li>
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
      <th align="left">Tipo de Mídia</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>PC0</b></td>
      <td><code>FastEthernet0</code></td>
      <td><b>Switch 2960</b></td>
      <td><code>FastEthernet0/1</code></td>
      <td>Cabo Direto (100 Mbps)</td>
    </tr>
    <tr>
      <td><b>PC1</b></td>
      <td><code>FastEthernet0</code></td>
      <td><b>Switch 2960</b></td>
      <td><code>FastEthernet0/2</code></td>
      <td>Cabo Direto (100 Mbps)</td>
    </tr>
    <tr>
      <td><b>Switch 2960</b></td>
      <td><code>FastEthernet0/24</code></td>
      <td><b>Roteador 2911</b></td>
      <td><code>GigabitEthernet0/0</code></td>
      <td>Cabo Direto (Uplink)</td>
    </tr>
  </tbody>
</table>

<blockquote>
  <b>ℹ️ Nota Técnica:</b> Os computadores operam em interfaces <i>FastEthernet (100 Mbps)</i>, enquanto o enlace de uplink com o roteador Cisco 2911 utiliza a porta <i>GigabitEthernet (1 Gbps)</i>.
</blockquote>

<hr/>

<h2>💻 3. Configuração no Roteador (Cisco IOS CLI)</h2>

<p>Acesse o CLI do roteador <b>Cisco 2911</b>, recuse a auto-configuração inicial digitando <code>no</code> e aplique os comandos abaixo:</p>

<details open>
  <summary><b>A. Configuração da Interface LAN & Ativação do Gateway</b></summary>
  <br/>
  <pre>
Router> enable
Router# configure terminal
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
  </pre>
</details>

<details open>
  <summary><b>B. Criação e Parametrização do Pool DHCP</b></summary>
  <br/>
  <pre>
# 1. Excluir o IP do Gateway para evitar duplicidade na rede
Router(config)# ip dhcp excluded-address 192.168.1.1

# 2. Criar e nomear o pool DHCP
Router(config)# ip dhcp pool POOL-LAN

# 3. Definir a faixa de rede e máscara
Router(dhcp-config)# network 192.168.1.0 255.255.255.0

# 4. Definir o Gateway Padrão e Servidor DNS para os clientes
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# exit
  </pre>
</details>

<details>
  <summary><b>C. Salvamento da Configuração na NVRAM</b></summary>
  <br/>
  <pre>
Router(config)# exit
Router# copy running-config startup-config
Destination filename [startup-config]? [Enter]
[OK]
  </pre>
</details>

<hr/>

<h2>🔍 4. Validação e Testes nos Dispositivos Finais</h2>

<h3>Etapa 1: Ativação do DHCP nos Clientes</h3>
<ol>
  <li>Clique no <b>PC0</b> → aba <b>Desktop</b> → <b>IP Configuration</b>.</li>
  <li>Mude a opção de <i>Static</i> para <b>DHCP</b> e aguarde a mensagem <code>DHCP request successful</code>.</li>
  <li>Repita o mesmo processo no <b>PC1</b>.</li>
</ol>

<h3>Etapa 2: Verificação de IP via Linha de Comando (PC0)</h3>
<pre>
PC> ipconfig /all

FastEthernet0 Connection:
   IP Address......................: 192.168.1.2
   Subnet Mask.....................: 255.255.255.0
   Default Gateway.................: 192.168.1.1
   DNS Server......................: 8.8.8.8
   DHCP Server.....................: 192.168.1.1
</pre>

<h3>Etapa 3: Testes de Conectividade ICMP (Ping)</h3>

<p><b>A. Teste PC0 $\to$ Gateway (Roteador <code>192.168.1.1</code>):</b></p>
<pre>
PC> ping 192.168.1.1

Pinging 192.168.1.1 with 32 bytes of data:

Reply from 192.168.1.1: bytes=32 time&lt;1ms TTL=255
Reply from 192.168.1.1: bytes=32 time&lt;1ms TTL=255
Reply from 192.168.1.1: bytes=32 time&lt;1ms TTL=255
Reply from 192.168.1.1: bytes=32 time&lt;1ms TTL=255

Ping statistics for 192.168.1.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
</pre>

<p><b>B. Teste PC0 $\to$ PC1 (Host para Host <code>192.168.1.3</code>):</b></p>
<pre>
PC> ping 192.168.1.3

Pinging 192.168.1.3 with 32 bytes of data:

Reply from 192.168.1.3: bytes=32 time&lt;1ms TTL=128
Reply from 192.168.1.3: bytes=32 time&lt;1ms TTL=128
Reply from 192.168.1.3: bytes=32 time&lt;1ms TTL=128
Reply from 192.168.1.3: bytes=32 time&lt;1ms TTL=128

Ping statistics for 192.168.1.3:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
</pre>

<hr/>

<h2>🔬 5. Auditoria de Concessão no Roteador</h2>

<p>Para auditar os endereços atribuídos dinamicamente pelo servidor, utilize no CLI do roteador:</p>

<pre>
Router# show ip dhcp binding

IP address       Client-ID/              Lease expiration        Type
                 Hardware address
192.168.1.2      0001.42A1.8C01          --                      Automatic
192.168.1.3      0060.702B.9F12          --                      Automatic
</pre>

<blockquote>
  <b>✅ Conclusão dos Testes:</b> O servidor DHCP alocou os IPs automaticamente a partir de <code>192.168.1.2</code>, preservando o endereço <code>192.168.1.1</code> para o Gateway conforme instruído na regra de exclusão.
</blockquote>

<hr/>

<h2>📥 6. Arquivos do Laboratório</h2>

<p>
  <a href="https://github.com/fer-isa">
    <img src="https://img.shields.io/badge/Download-lab--dhcp--router--cisco.pkt-0A84FF?style=for-the-badge&logo=cisco&logoColor=white" alt="Download PKT" />
  </a>
</p>

<blockquote>
  <b>💡 Como baixar o arquivo <code>.pkt</code> no GitHub:</b><br/>
  1. Localize o arquivo <code>lab-dhcp-router-cisco.pkt</code> nesta mesma pasta do repositório.<br/>
  2. Clique nele e, na barra de ferramentas à direita, clique no <b>ícone de Download</b> (seta para baixo ⬇️) para salvar o arquivo de simulação.
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

```
