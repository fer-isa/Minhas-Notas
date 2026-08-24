<div align="center">

  <h1>🌐 Dispositivos de Rede & Configuração Inicial — Módulos 1 ao 3</h1>
  <p><b>Formação Mulher Digital • Trilha de Cibersegurança & Infraestrutura</b></p>

  <p>
    <img src="https://img.shields.io/badge/Cisco_Networking_Academy-Fundamentos_de_Rede-005073?style=for-the-badge&logo=cisco&logoColor=white" alt="Fundamentos" />
    <img src="https://img.shields.io/badge/Arquitetura-Modelo_Hierárquico-0A84FF?style=for-the-badge" alt="Modelo Hierárquico" />
    <img src="https://img.shields.io/badge/Cloud_%26_Virtualização-IaaS_%7C_PaaS_%7C_SaaS-30D158?style=for-the-badge" alt="Cloud" />
    <img src="https://img.shields.io/badge/Trilha-Mulher_Digital-8A2BE2?style=for-the-badge" alt="Mulher Digital" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>

</div>

<hr/>

<h2>📌 Visão Geral</h2>

<p>
Este documento consolida os fundamentos estruturais de arquitetura de redes corporativas dos <b>Módulos 1 ao 3</b>, cobrindo os pilares de resiliência e desempenho, a anatomia do <b>Modelo Hierárquico Cisco de Três Camadas</b> (Acesso, Distribuição e Núcleo), os modelos de implantação e serviços de <b>Computação em Nuvem</b>, princípios de <b>Virtualização</b> e hipervisores, além do processo matemático de conversão posicional de <b>Endereçamento IPv4 (Decimal para Binário)</b>.
</p>

<hr/>

<details open>
  <summary><h2>🏗️ 1. Pilares da Arquitetura de Rede</h2></summary>
  <br/>

  <p>O planejamento de uma infraestrutura corporativa robusta baseia-se em quatro pilares fundamentais de engenharia:</p>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left" width="28%">Pilar</th>
        <th align="left" width="72%">Conceito & Aplicação Prática</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>Tolerância a Falhas</b></td>
        <td>Projeto com enlaces redundantes e protocolos de convergência rápida (como Spanning Tree e HSRP) desenhado para manter os serviços ativos caso um cabo, porta ou dispositivo sofra avaria física.</td>
      </tr>
      <tr>
        <td><b>Escalabilidade</b></td>
        <td>Capacidade de expandir a malha física e lógica (adicionando novas filiais, usuários, switches e serviços) de forma modular, sem exigir reestruturações completas ou degradar a performance.</td>
      </tr>
      <tr>
        <td><b>Qualidade de Serviço (QoS)</b></td>
        <td>Mecanismos de priorização de filas e garantia de largura de banda para aplicações sensíveis à latência e perdas (ex: tráfego de Voz sobre IP - VoIP, videoconferências e sistemas críticos).</td>
      </tr>
      <tr>
        <td><b>Segurança da Informação</b></td>
        <td>Blindagem contínua de perímetros, equipamentos e tráfego de dados contra acessos indevidos e ameaças externas, garantindo Confidencialidade, Integridade e Disponibilidade (Tríade CIA).</td>
      </tr>
    </tbody>
  </table>
</details>

<hr/>

<details open>
  <summary><h2>🏢 2. Modelo de Rede Hierárquica da Cisco</h2></summary>
  <br/>

  <p>
    A segmentação hierárquica organiza a rede em camadas modulares com funções bem delimitadas, otimizando o fluxo de dados, simplificando o gerenciamento e isolando domínios de falha:
  </p>

  <pre>
       [ Roteador / Switch Core ]       <--- Camada de Núcleo (Core: Alta Velocidade)
                    |
        [ Switch de Distribuição ]       <--- Camada de Distribuição (Políticas & Roteamento)
                    |
          [ Switch de Acesso ]          <--- Camada de Acesso (Conexão de Estações)
          /         |        \
      [PC 1]     [PC 2]   [AP Wi-Fi]    <--- Dispositivos Finais (End Devices)
  </pre>

  <h3>Funções e Especificações dos Equipamentos</h3>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left" width="25%">Camada</th>
        <th align="left" width="45%">Função Operacional</th>
        <th align="left" width="30%">Equipamento Típico</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>Camada de Acesso</b></td>
        <td>Ponto de conexão física direta dos usuários finais (estações de trabalho, impressoras, câmeras IP e Access Points) à rede corporativa.</td>
        <td><i>Cisco Catalyst 2960-XR / 1000 Series</i></td>
      </tr>
      <tr>
        <td><b>Camada de Distribuição</b></td>
        <td>Agregação de múltiplos switches de acesso, controle de domínios de broadcast (VLANs), aplicação de listas de acesso (ACLs) e políticas de roteamento.</td>
        <td><i>Cisco Catalyst 9300 Series</i> (Switches L3 empilháveis)</td>
      </tr>
      <tr>
        <td><b>Camada de Núcleo (Core)</b></td>
        <td><i>Backbone</i> central de altíssima velocidade responsável pelo transporte maciço de pacotes entre prédios/data centers sem a aplicação de filtros pesados que gerem latência.</td>
        <td><i>Cisco Catalyst 9600 Series / Roteadores 4000</i></td>
      </tr>
    </tbody>
  </table>
</details>

<hr/>

<details open>
  <summary><h2>☁️ 3. Computação em Nuvem (Modelos de Implantação e Serviço)</h2></summary>
  <br/>

  <h3>Modelos de Implantação</h3>
  <ul>
    <li><b>Nuvem Pública:</b> Recursos de hardware, rede e software provisionados e mantidos por um provedor terceiro sobre a infraestrutura da Internet (ex: AWS, Google Cloud, Microsoft Azure).</li>
    <li><b>Nuvem Privada:</b> Infraestrutura computacional dedicada com exclusividade a uma única organização, oferecendo máximo controle e isolamento regulatório.</li>
    <li><b>Nuvem Híbrida:</b> Orquestração integrada que combina nuvens públicas e privadas, permitindo que dados e cargas de trabalho trafeguem de forma interoperável e segura.</li>
    <li><b>Nuvem Comunitária:</b> Estrutura compartilhada entre organizações com missões, exigências jurídicas ou requisitos de segurança em comum (ex: consórcio inter-hospitalar ou setor financeiro).</li>
  </ul>

  <h3>Modelos de Serviço</h3>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left" width="22%">Modelo</th>
        <th align="left" width="48%">Definição de Responsabilidade</th>
        <th align="left" width="30%">Exemplos de Mercado</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>SaaS</b><br/><i>Software as a Service</i></td>
        <td>Software completo entregue diretamente ao usuário final via navegador; o provedor gerencia toda a infraestrutura subjacente.</td>
        <td>Google Workspace, Microsoft 365, Canva.</td>
      </tr>
      <tr>
        <td><b>PaaS</b><br/><i>Platform as a Service</i></td>
        <td>Ambiente de execução e desenvolvimento (runtime, banco de dados, middleware) pronto para criação e publicação de aplicações sem gerenciar o SO.</td>
        <td>AWS Elastic Beanstalk, Heroku, Google App Engine.</td>
      </tr>
      <tr>
        <td><b>IaaS</b><br/><i>Infrastructure as a Service</i></td>
        <td>Fornecimento sob demanda de recursos de computação brutos (máquinas virtuais, capacidade de armazenamento, roteadores virtuais e firewalls).</td>
        <td>AWS EC2, Azure VMs, Google Compute Engine.</td>
      </tr>
    </tbody>
  </table>
</details>

<hr/>

<details open>
  <summary><h2>💻 4. Virtualização e Hipervisores</h2></summary>
  <br/>

  <p>
    A <b>virtualização</b> é a tecnologia que permite abstrair o hardware físico através de uma camada de software (<b>Hipervisor / VMM</b>), permitindo que múltiplos sistemas operacionais independentes (<i>Guests</i>) executem concorrentemente sobre um único servidor físico (<i>Host</i>).
  </p>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left" width="25%">Tipo de Hipervisor</th>
        <th align="left" width="45%">Arquitetura Operacional</th>
        <th align="left" width="30%">Ambiente Típico & Exemplos</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>Tipo 1 (Bare-Metal)</b></td>
        <td>Instalado diretamente sobre o hardware físico, sem sistema operacional hospedeiro intermediário; oferece máxima performance e baixa latência.</td>
        <td>Data centers e servidores corporativos.<br/><i>Ex: VMware ESXi, Microsoft Hyper-V, KVM.</i></td>
      </tr>
      <tr>
        <td><b>Tipo 2 (Hosted)</b></td>
        <td>Executado como uma aplicação comum sobre um sistema operacional convencional já existente no computador do usuário.</td>
        <td>Estações de trabalho, testes e laboratórios de estudo.<br/><i>Ex: Oracle VirtualBox, VMware Workstation.</i></td>
      </tr>
    </tbody>
  </table>
</details>

<hr/>

<details open>
  <summary><h2>🔢 5. Conversão de Endereçamento: Decimal para Binário</h2></summary>
  <br/>

  <p>
    O endereço IPv4 é formado por <b>32 bits</b> agrupados em <b>4 octetos (8 bits cada)</b> separados por pontos. Cada octeto varia na base decimal de <code>0</code> a <code>255</code>.
  </p>

  <h3>Tabela de Pesos Posicionais de Base 2 (Octeto de 8 bits)</h3>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="center">$2^7$</th>
        <th align="center">$2^6$</th>
        <th align="center">$2^5$</th>
        <th align="center">$2^4$</th>
        <th align="center">$2^3$</th>
        <th align="center">$2^2$</th>
        <th align="center">$2^1$</th>
        <th align="center">$2^0$</th>
      </tr>
    </thead>
    <tbody>
      <tr align="center">
        <td><b>128</b></td>
        <td><b>64</b></td>
        <td><b>32</b></td>
        <td><b>16</b></td>
        <td><b>8</b></td>
        <td><b>4</b></td>
        <td><b>2</b></td>
        <td><b>1</b></td>
      </tr>
    </tbody>
  </table>

  <h3>Exemplo Prático de Decomposição: Endereço IP <code>192.168.10.5</code></h3>
  <ul>
    <li><b>1º Octeto (192):</b> $128 + 64$ $\rightarrow$ <code>11000000</code></li>
    <li><b>2º Octeto (168):</b> $128 + 32 + 8$ $\rightarrow$ <code>10101000</code></li>
    <li><b>3º Octeto (10):</b> $8 + 2$ $\rightarrow$ <code>00001010</code></li>
    <li><b>4º Octeto (5):</b> $4 + 1$ $\rightarrow$ <code>00000101</code></li>
  </ul>

  <blockquote>
    <b>🎯 Representação Binária Consolidada:</b><br/>
    <code>11000000.10101000.00001010.00000101</code>
  </blockquote>
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
