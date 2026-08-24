<div align="center">

  <h1>🌐 Comutação Ethernet & Camada de Rede — Módulos 4 ao 6</h1>
  <p><b>Formação Mulher Digital • Trilha de Cibersegurança & Infraestrutura</b></p>

  <p>
    <img src="https://img.shields.io/badge/Cisco_Networking_Academy-Ethernet_%26_Switching-005073?style=for-the-badge&logo=cisco&logoColor=white" alt="Ethernet" />
    <img src="https://img.shields.io/badge/Camada_2-Tabela_CAM_%7C_MAC-0A84FF?style=for-the-badge" alt="Camada 2" />
    <img src="https://img.shields.io/badge/Trilha-Mulher_Digital-8A2BE2?style=for-the-badge" alt="Mulher Digital" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>

</div>

<hr/>

<h2>📌 Visão Geral</h2>

<p>
Este documento aborda os fundamentos operacionais da tecnologia <b>Ethernet</b> nas Camadas 1 (Física) e 2 (Enlace de Dados) do modelo OSI, detalhando a estrutura anatômica dos quadros de dados (<i>Frames</i>), a mecânica de aprendizagem e comutação da <b>Tabela CAM (MAC Table)</b> em switches e os princípios de entrega do protocolo <b>IP</b> na Camada 3 (Rede).
</p>

<hr/>

<details open>
  <summary><h2>🔌 1. Tecnologia Ethernet & Divisão em Subcamadas (Padrões IEEE)</h2></summary>
  <br/>

  <p>A tecnologia Ethernet opera de forma integrada nas camadas Física e de Enlace, sendo dividida em duas subcamadas padronizadas pelo IEEE:</p>

  <ul>
    <li><b>Subcamada LLC (<i>Logical Link Control</i> — IEEE 802.2):</b> Interface em software que atua como ponte de comunicação com os protocolos da Camada 3 (Rede), identificando o tipo de protocolo de rede encapsulado no pacote.</li>
    <li><b>Subcamada MAC (<i>Media Access Control</i> — IEEE 802.3):</b> Responsável direta pelo controle de acesso ao meio físico compartilhado, temporização de sinais, montagem/desmontagem do quadro e inserção dos endereços físicos de hardware.</li>
  </ul>
</details>

<hr/>

<details open>
  <summary><h2>📦 2. Estrutura do Quadro Ethernet (Ethernet Frame)</h2></summary>
  <br/>

  <p>
    O tamanho total do quadro Ethernet varia entre o limite mínimo de <b>64 bytes</b> e o limite máximo de <b>1518 bytes</b> (sem considerar tags VLAN 802.1Q). Quadros menores que 64 bytes são denominados <i>Runt Frames</i> (frequentemente resultantes de colisões), enquanto quadros maiores que 1518 bytes são denominados <i>Giant Frames</i>; ambos são descartados automaticamente pelas placas de rede (NICs) por erro.
  </p>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left" width="25%">Campo</th>
        <th align="center" width="18%">Tamanho</th>
        <th align="left" width="57%">Função Operacional</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>Preâmbulo & SFD</b></td>
        <td align="center">8 bytes (7 + 1)</td>
        <td>Sincroniza o relógio de recepção e notifica a placa de rede receptora sobre o início do quadro (SFD = <i>Start Frame Delimiter</i>).</td>
      </tr>
      <tr>
        <td><b>MAC de Destino</b></td>
        <td align="center">6 bytes (48 bits)</td>
        <td>Endereço físico de hardware da interface do nó que receberá o quadro (Unicast, Multicast ou Broadcast).</td>
      </tr>
      <tr>
        <td><b>MAC de Origem</b></td>
        <td align="center">6 bytes (48 bits)</td>
        <td>Endereço físico de hardware da placa de rede transmissora do quadro.</td>
      </tr>
      <tr>
        <td><b>Tipo / EtherType</b></td>
        <td align="center">2 bytes</td>
        <td>Identifica qual protocolo da camada superior está contido na carga útil (ex: <code>0x0800</code> para IPv4 ou <code>0x86DD</code> para IPv6).</td>
      </tr>
      <tr>
        <td><b>Dados / Payload</b></td>
        <td align="center">46 a 1500 bytes</td>
        <td>Carga útil que transporta o pacote encapsulado da Camada 3 (PDU de rede).</td>
      </tr>
      <tr>
        <td><b>FCS (<i>Frame Check Sequence</i>)</b></td>
        <td align="center">4 bytes</td>
        <td>Campo de controle com código CRC-32 (<i>Cyclic Redundancy Check</i>) para detecção de erros físicos na transmissão.</td>
      </tr>
    </tbody>
  </table>
</details>

<hr/>

<details open>
  <summary><h2>🏷️ 3. Endereçamento MAC & Modos de Transmissão</h2></summary>
  <br/>

  <p>
    O endereço MAC possui <b>48 bits</b> (6 bytes) representados por 12 dígitos hexadecimais (ex: <code>00:1A:2B:3C:4D:5E</code>):
  </p>

  <ul>
    <li><b>OUI (<i>Organizationally Unique Identifier</i>):</b> Primeiros 24 bits (3 primeiros octetos), atribuídos pelo IEEE para identificar com exclusividade o fabricante do chip de rede.</li>
    <li><b>Device Identifier (Número de Série):</b> Últimos 24 bits (3 últimos octetos), alocados pelo fabricante para garantir que cada placa produzida possua um identificador físico exclusivo.</li>
  </ul>

  <h3>Modos de Comunicação em Camada 2</h3>
  <ul>
    <li><b>Unicast:</b> Quadro direcionado para a interface de um único host específico.</li>
    <li><b>Broadcast:</b> Quadro destinado a todas as estações do segmento local, preenchendo todos os bits em 1 (<code>FF:FF:FF:FF:FF:FF</code>).</li>
    <li><b>Multicast:</b> Quadro direcionado a um grupo específico de nós assinantes (endereços MAC iniciando com prefixos reservados como <code>01:00:5E</code> para IPv4).</li>
  </ul>
</details>

<hr/>

<details open>
  <summary><h2>🔄 4. Funcionamento do Switch & Tabela MAC (CAM)</h2></summary>
  <br/>

  <p>O switch opera com base no ciclo contínuo de três mecanismos essenciais:</p>

  <ol>
    <li><b>Aprendizado (Learning):</b> Ao receber um quadro, o switch inspeciona o <b>MAC de Origem</b> e a porta física de entrada. Se a combinação ainda não existir na sua <b>Tabela CAM (<i>Content Addressable Memory</i>)</b>, ele registra o endereço e inicia o temporizador de expiração (<i>aging timer</i>).</li>
    <li><b>Encaminhamento Direto (Forwarding / Filtering):</b> O switch analisa o <b>MAC de Destino</b>. Se o endereço já estiver mapeado na tabela CAM, o quadro é comutado e enviado <b>exclusivamente para a porta correspondente</b>.</li>
    <li><b>Inundação (Flooding):</b> Se o MAC de destino não estiver na tabela (situação de <i>Unknown Unicast</i>) ou for um <i>Broadcast</i>, o switch replica e envia o quadro para <b>todas as portas ativas</b> pertencentes àquela VLAN, exceto a porta por onde o quadro foi recebido.</li>
  </ol>
</details>

<hr/>

<details open>
  <summary><h2>🌍 5. Camada 3: Protocolo IP & Comparativo de Cabeçalhos</h2></summary>
  <br/>

  <p>O protocolo IP fornece o serviço de entrega lógica de pacotes entre hosts remotos com base em três pilares:</p>

  <ul>
    <li><b>Sem Conexão (<i>Connectionless</i>):</b> Não estabelece uma sessão ou handshake prévio antes do envio dos pacotes.</li>
    <li><b>Melhor Esforço (<i>Best Effort / Unreliable</i>):</b> Não possui mecanismos de confirmação de entrega ou retransmissão no nível de rede (essa responsabilidade é delegada a protocolos de transporte como o TCP).</li>
    <li><b>Independente de Mídia:</b> O pacote IP mantém seu formato inalterado independentemente do meio físico de transmissão utilizado no trajeto (cobre, fibra óptica ou sem fio).</li>
  </ul>

  <h3>Comparativo de Arquitetura: IPv4 vs. IPv6</h3>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left" width="28%">Característica</th>
        <th align="left" width="36%">IPv4</th>
        <th align="left" width="36%">IPv6</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>Comprimento do Endereço</b></td>
        <td>32 bits (ex: <code>192.168.0.1</code>)</td>
        <td>128 bits (ex: <code>2001:0db8::1</code>)</td>
      </tr>
      <tr>
        <td><b>Espaço de Endereçamento</b></td>
        <td>~4,3 bilhões de endereços</td>
        <td>~$3,4 \times 10^{38}$ endereços</td>
      </tr>
      <tr>
        <td><b>Tamanho do Cabeçalho</b></td>
        <td>Variável (20 a 60 bytes, devido a opções)</td>
        <td>Fixo em 40 bytes (otimização de processamento)</td>
      </tr>
      <tr>
        <td><b>Fragmentação de Pacotes</b></td>
        <td>Executada no host emissor e em roteadores intermediários</td>
        <td>Executada exclusivamente no host de origem (<i>Path MTU Discovery</i>)</td>
      </tr>
      <tr>
        <td><b>Checksum de Cabeçalho</b></td>
        <td>Presente (recalculado a cada salto)</td>
        <td>Removido para acelerar o roteamento</td>
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
      <img src="
