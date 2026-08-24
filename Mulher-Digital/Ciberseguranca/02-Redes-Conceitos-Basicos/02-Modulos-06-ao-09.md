<div align="center">

  <h1>🌐 Conceitos Básicos de Redes — Módulos 6 ao 9 (Avançado)</h1>
  <p><b>Formação Mulher Digital • Trilha de Cibersegurança & Infraestrutura</b></p>

  <p>
    <img src="https://img.shields.io/badge/Cisco_Networking_Academy-Redes_Avançadas-005073?style=for-the-badge&logo=cisco&logoColor=white" alt="Redes Avançadas" />
    <img src="https://img.shields.io/badge/Camadas-L2_%7C_L3_%7C_L7-0A84FF?style=for-the-badge" alt="Camadas OSI" />
    <img src="https://img.shields.io/badge/Trilha-Mulher_Digital-8A2BE2?style=for-the-badge" alt="Mulher Digital" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>

</div>

<hr/>

<h2>📌 Visão Geral</h2>

<p>
Este documento consolida o aprofundamento técnico em comunicação e infraestrutura de redes corporativas dos <b>Módulos 6 ao 9</b>, cobrindo os processos de <b>encapsulamento de dados</b>, esquemas de endereçamento e identificação (<b>MAC, IPv4, IPv6 e DNS</b>), segmentação corporativa (<b>Intranet, Extranet e NAT</b>), análise comparativa de topologias físicas e fundamentos de segurança defensiva.
</p>

<hr/>

<details open>
  <summary><h2>📦 1. Modelos de Rede & Processo de Encapsulamento</h2></summary>
  <br/>

  <ul>
    <li><b>Encapsulamento de Dados:</b> Processo sequencial no qual cada camada do modelo OSI/TCP/IP adiciona cabeçalhos (<i>headers</i>) e terminadores (<i>trailers</i>) com informações de controle à PDU à medida que os dados descem na pilha até a conversão final em bits físicos.</li>
    <li><b>Quadro Ethernet (Layer 2 - Enlace):</b> Estrutura de dados que envelopa o pacote IP, adicionando endereços de controle de acesso ao meio (<b>MAC Address</b> de origem e destino) e códigos de verificação de redundância cíclica (CRC/FCS) para entrega física no mesmo segmento de rede.</li>
    <li><b>Camada de Acesso:</b> Ponto de entrada que conecta os hosts finais à infraestrutura de agregação/núcleo, provendo autenticação, controle de portas e serviços locais.</li>
    <li><b>Ethernet vs. Internet:</b>
      <ul>
        <li><b>Ethernet (IEEE 802.3):</b> Padrão físico e de enlace para transmissão e comutação de dados em redes locais (LAN).</li>
        <li><b>Internet:</b> Malha global descentralizada de redes interconectadas que utiliza a pilha TCP/IP, sistemas autônomos (ASN) e roteamento de borda (BGP).</li>
      </ul>
    </li>
  </ul>
</details>

<hr/>

<details open>
  <summary><h2>🆔 2. Identificação e Resolução na Rede: MAC, IP e DNS</h2></summary>
  <br/>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left" width="20%">Mecanismo</th>
        <th align="center" width="18%">Camada OSI</th>
        <th align="left" width="27%">Formato / Exemplo</th>
        <th align="left" width="35%">Função Principal</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>Endereço MAC</b></td>
        <td align="center">Enlace (Camada 2)</td>
        <td>Hexadecimal (48 bits)<br/><code>00:1A:2B:3C:4D:5E</code></td>
        <td>Identificador físico universal gravado permanentemente na placa de rede (NIC) para comunicação local.</td>
      </tr>
      <tr>
        <td><b>Endereço IP</b></td>
        <td align="center">Rede (Camada 3)</td>
        <td>Decimal pontuado (IPv4) ou Hexadecimal (IPv6)</td>
        <td>Identificador lógico, hierárquico e globalmente roteável de localização do nó na topologia de rede.</td>
      </tr>
      <tr>
        <td><b>DNS</b></td>
        <td align="center">Aplicação (Camada 7)</td>
        <td>Nomes FQDN<br/><code>www.cisco.com</code></td>
        <td>Sistema de resolução que converte nomes de domínio amigáveis para endereços IP numéricos compreendidos pelas máquinas.</td>
      </tr>
    </tbody>
  </table>
</details>

<hr/>

<details open>
  <summary><h2>🏢 3. Escopo Corporativo e Tradução de Endereços (NAT)</h2></summary>
  <br/>

  <h3>Segmentação de Acesso Corporativo</h3>
  <ul>
    <li><b>Intranet:</b> Rede interna privada, isolada por firewalls e destinada exclusivamente a colaboradores autenticados para acesso a sistemas e documentos internos.</li>
    <li><b>Extranet:</b> Extensão controlada e segura da rede interna que permite o acesso autenticado a parceiros de negócios, fornecedores, terceiros ou clientes autorizados (frequentemente via VPNs).</li>
  </ul>

  <h3>NAT (<i>Network Address Translation</i>)</h3>
  <ul>
    <li><b>Objetivo Técnico:</b> Mapear e traduzir endereços IP privados internos (RFC 1918) para um ou mais endereços IP públicos válidos e roteáveis na Internet.</li>
    <li><b>Benefícios Principais:</b> Mitigação do esgotamento do espaço IPv4 público e reforço de segurança por ofuscação da topologia e dos endereços dos hosts internos.</li>
  </ul>
</details>

<hr/>

<details open>
  <summary><h2>🗺️ 4. Topologias Físicas & Protocolos IPv4 vs. IPv6</h2></summary>
  <br/>

  <h3>Comparativo de Topologias Físicas de Rede</h3>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left" width="18%">Topologia</th>
        <th align="left" width="30%">Estrutura Física</th>
        <th align="left" width="26%">Vantagens</th>
        <th align="left" width="26%">Desvantagens</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>Estrela (Star)</b></td>
        <td>Todos os nós são conectados individualmente a um concentrador central (Switch).</td>
        <td>Isolamento simples de falhas; queda de um cabo não afeta os outros hosts.</td>
        <td>Ponto único de falha no dispositivo central (switch/hub).</td>
      </tr>
      <tr>
        <td><b>Barramento (Bus)</b></td>
        <td>Todos os dispositivos compartilham uma linha física única de comunicação (<i>backbone</i>).</td>
        <td>Baixo consumo de cabeamento e custo inicial reduzido de implantação.</td>
        <td>Alto risco de colisão de pacotes e interrupção total em caso de rompimento do cabo central.</td>
      </tr>
      <tr>
        <td><b>Malha (Mesh)</b></td>
        <td>Enlaces redundantes ponto a ponto diretos entre múltiplos dispositivos.</td>
        <td>Máxima tolerância a falhas, alta resiliência e rotas alternativas automáticas.</td>
        <td>Custo elevado de cabeamento e alta complexidade de expansão e manutenção.</td>
      </tr>
    </tbody>
  </table>

  <h3>Diferenciais: Endereçamento IPv4 vs. IPv6</h3>
  <ul>
    <li><b>IPv4:</b> Arquitetura de <b>32 bits</b> (representada em 4 octetos decimais separados por pontos, ex: <code>192.168.1.10</code>), totalizando aproximadamente 4,3 bilhões de endereços.</li>
    <li><b>IPv6:</b> Arquitetura de <b>128 bits</b> (representada em 8 grupos de 4 dígitos hexadecimais separados por dois-pontos, ex: <code>2001:0db8:85a3::8a2e:0370:7334</code>), oferecendo espaço de endereçamento praticamente inesgotável ($3.4 \times 10^{38}$ endereços), cabeçalhos simplificados e suporte nativo ao protocolo IPsec.</li>
  </ul>
</details>

<hr/>

<details open>
  <summary><h2>🛡️ 5. Fundamentos de Segurança e Hardening de Rede</h2></summary>
  <br/>

  <ul>
    <li><b>Firewalls (Borda e Host):</b> Sistemas de inspeção e filtragem de pacotes (<i>Stateless</i>, <i>Stateful Inspection</i> e <i>Next-Generation Firewalls - NGFW</i>) que controlam o fluxo com base em políticas de segurança, portas, protocolos e assinaturas de aplicações.</li>
    <li><b>Hardening & Boas Práticas Operacionais:</b>
      <ol>
        <li><b>Gestão de Patches (Patch Management):</b> Aplicação contínua e homologada de atualizações de segurança para firmwares de roteadores/switches e sistemas operacionais.</li>
        <li><b>Autenticação Forte & MFA:</b> Imposição de senhas complexas associadas a múltiplos fatores de autenticação para acessos administrativos.</li>
        <li><b>Princípio do Menor Privilégio (Least Privilege):</b> Concessão estrita dos níveis mínimos de permissão indispensáveis para a execução de cada rotina.</li>
        <li><b>Criptografia em Trânsito:</b> Desativação de protocolos inseguros em texto claro (como <code>Telnet</code> e <code>HTTP</code>) e adoção obrigatória de protocolos criptografados (<code>SSH</code>, <code>HTTPS</code> e <code>IPsec VPN</code>).</li>
        <li><b>Auditoria e Monitoramento Contínuo:</b> Centralização e análise contínua de logs de tráfego (Syslog/SIEM) para identificação precoce de anomalias e tentativas de invasão.</li>
      </ol>
    </li>
  </ul>
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
