<div align="center">
  <h2>🌐 Laboratório Prático: Introdução às Redes Hierárquicas</h2>
  <p><b>Construindo uma rede corporativa dividida em 3 camadas: Acesso, Distribuição e Núcleo</b></p>
  
  <br>
  
  <p>
    <img src="https://img.shields.io/badge/Cisco%20Packet%20Tracer-005073?style=for-the-badge&logo=cisco&logoColor=white" alt="Cisco Packet Tracer" />
    <img src="https://img.shields.io/badge/Topologia-Hierárquica-0A84FF?style=for-the-badge" alt="Topologia" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>
</div>

<hr/>

<h3>📌 1. O Que Eu Fiz Neste Projeto</h3>
<p>O objetivo deste laboratório foi sair das redes pequenas e montar a base de uma rede de empresa grande. Para isso, usei o modelo de <b>Três Camadas da Cisco</b>.</p>

<p>A ideia aqui é organizar a casa: segmentar o ambiente fisicamente, passar os cabos corretamente respeitando as velocidades das portas e configurar o endereçamento IP estático para que os computadores consigam chegar até o roteador de saída (Core).</p>

<div align="center">
  <!-- ARRASTE A FOTO DA SUA TOPOLOGIA AQUI E APAGUE ESTA LINHA -->
  <p><i>A divisão clássica: Roteador no topo (Núcleo), Switch parrudo no meio (Distribuição) e Switches menores na base (Acesso).</i></p>
</div>

<hr/>

<h3>🏗️ 2. Os Equipamentos Usados</h3>
<p>Em uma rede hierárquica, cada equipamento tem uma função bem definida. Usei a seguinte estrutura:</p>

<table width="100%">
  <thead>
    <tr bgcolor="#1f242c">
      <th align="left">Camada</th>
      <th align="left">Dispositivo / Modelo</th>
      <th align="left">Função na Rede</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>Núcleo (Core)</b></td>
      <td>1x Roteador Cisco 4331</td>
      <td>É o "chefe". Faz o encaminhamento rápido e é a porta de saída.</td>
    </tr>
    <tr>
      <td><b>Distribuição</b></td>
      <td>1x Switch Cisco Catalyst 3650</td>
      <td>O "gerente". Junta os cabos que vêm da base e organiza o tráfego.</td>
    </tr>
    <tr>
      <td><b>Acesso</b></td>
      <td>2x Switches Cisco Catalyst 2960</td>
      <td>A "linha de frente". Onde os PCs dos usuários são conectados.</td>
    </tr>
    <tr>
      <td><b>Dispositivos Finais</b></td>
      <td>4x Computadores Genéricos</td>
      <td>Estações de trabalho divididas (Laboratório e Secretaria).</td>
    </tr>
  </tbody>
</table>

<br>

<p><b>Tabela de Endereçamento IP</b></p>
<table width="100%">
  <thead>
    <tr bgcolor="#1f242c">
      <th align="left">Aparelho</th>
      <th align="left">Interface</th>
      <th align="left">Endereço IPv4</th>
      <th align="left">Máscara</th>
      <th align="left">Gateway</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>PC-Lab01</b></td>
      <td>FastEthernet0</td>
      <td><code>192.168.1.10</code></td>
      <td><code>255.255.255.0</code></td>
      <td><code>192.168.1.1</code></td>
    </tr>
    <tr>
      <td><b>PC-Lab02</b></td>
      <td>FastEthernet0</td>
      <td><code>192.168.1.11</code></td>
      <td><code>255.255.255.0</code></td>
      <td><code>192.168.1.1</code></td>
    </tr>
    <tr>
      <td><b>PC-Sec01</b></td>
      <td>FastEthernet0</td>
      <td><code>192.168.1.20</code></td>
      <td><code>255.255.255.0</code></td>
      <td><code>192.168.1.1</code></td>
    </tr>
    <tr>
      <td><b>PC-Sec02</b></td>
      <td>FastEthernet0</td>
      <td><code>192.168.1.21</code></td>
      <td><code>255.255.255.0</code></td>
      <td><code>192.168.1.1</code></td>
    </tr>
    <tr>
      <td><b>Roteador-Core</b></td>
      <td>GigabitEthernet0/0/0</td>
      <td><code>192.168.1.1</code></td>
      <td><code>255.255.255.0</code></td>
      <td><i>-</i></td>
    </tr>
  </tbody>
</table>

<hr/>

<h3>⚙️ 3. Passo a Passo da Configuração</h3>

<ul>
  <li>
    <b>Etapa 1: Organização e Energia:</b> Posicionei os equipamentos respeitando a hierarquia visual. Um detalhe importante aqui foi o Switch 3650 (Distribuição): no simulador, ele vem desligado de fábrica e precisei inserir fisicamente o módulo da fonte de energia nele para que pudesse ligar.
  </li>
  <li>
    <b>Etapa 2: Cabeamento:</b> Liguei os PCs nos switches de Acesso usando as portas normais (FastEthernet). Já a ligação entre os switches e o roteador foi feita nas portas mais rápidas (GigabitEthernet) para evitar lentidão no tráfego.
  </li>
  <li>
    <b>Etapa 3: Ligando o Roteador (CLI):</b> Pela "tela preta", configurei o IP na interface do roteador e a ativei para que ela pudesse receber o tráfego dos computadores:
  </li>
</ul>

<pre>
Router> enable
Router# configure terminal
Router(config)# interface GigabitEthernet0/0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
</pre>

<hr/>

<h3>🚧 4. Meus Desafios e Aprendizados Reais</h3>
<p>Fazer esse laboratório em conjunto com a turma e a professora em um ritmo mais acelerado foi um ótimo teste de atenção. Durante o processo, enfrentei algumas "pegadinhas" práticas:</p>

<ul>
  <li>
    <b>O mistério da Porta Gigabit 24:</b> Na hora de montar a topologia, acabei selecionando o switch 3550 por engano. Fiquei super encucada porque não conseguia achar a porta "Gigabit 24" para fazer a conexão principal de jeito nenhum! Só depois de investigar, percebi o erro e troquei para o modelo correto (Catalyst 3650). Foi uma lição muito real sobre como validar o modelo exato do hardware antes de começar.
  </li>
  <li>
    <b>A lógica do cabeamento:</b> Tive um pouco de dificuldade na hora de puxar os cabos, na dúvida se deveria conectar primeiro do roteador para o switch ou o contrário. Acabei descobrindo que o cabo direto não tem um "lado certo" para começar a plugar, mas esse momento de dúvida me ajudou a fixar melhor como o simulador organiza as portas.
  </li>
</ul>

<hr/>

<h3>🎥 5. Teste Prático (Vídeo)</h3>
<p>Para provar que a configuração física e lógica funcionou, em vez de usar telas estáticas, gravei um pequeno vídeo do modo de simulação.</p>

<div align="center">

https://github.com/user-attachments/assets/954627db-564b-43d2-9a32-46759071eee7

  <br>
  <p><i>Fluxo de pacotes ICMP percorrendo os switches de Acesso, Distribuição e Roteador Core.</i></p>
</div>

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
