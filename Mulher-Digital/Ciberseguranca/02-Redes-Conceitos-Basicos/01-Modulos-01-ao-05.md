  <div align="center">
  <img src="../../assets/introduction-to-cybersecurity.png" width="180" alt="Conceitos Básicos de Redes" />
  
  <h2>🌐 Conceitos Básicos de Redes — Módulos 1 ao 5</h2>
  <p><b>Formação Mulher Digital • Trilha de Cibersegurança & Infraestrutura</b></p>
  
  <p>
    <img src="https://img.shields.io/badge/Cisco_Networking_Academy-Redes_de_Computadores-005073?style=for-the-badge&logo=cisco&logoColor=white" alt="Redes" />
    <img src="https://img.shields.io/badge/Modelos-OSI_%7C_TCP%2FIP-0A84FF?style=for-the-badge" alt="OSI e TCP/IP" />
    <img src="https://img.shields.io/badge/Trilha-Mulher_Digital-8A2BE2?style=for-the-badge" alt="Mulher Digital" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>
</div>

<hr/>

<h3>📌 O que tem neste resumo?</h3>
<p>Aqui juntei os conceitos que são o "feijão com arroz" da infraestrutura de redes. O objetivo é explicar de forma simples como os computadores conversam entre si, os tipos de redes, os equipamentos que usamos e como funcionam os modelos de camadas (OSI e TCP/IP).</p>

<hr/>

<details open>
  <summary><h3>🏗️ Módulo 1: Fundamentos, Escopo e Tamanho</h3></summary>
  <br/>

  <ul>
    <li><b>O que é uma Rede?</b> São equipamentos conectados entre si (por cabo ou Wi-Fi) para compartilhar coisas (arquivos, internet, impressora, etc.).</li>
    <li><b>Tamanhos de Rede:</b>
      <ul>
        <li><b>Doméstica:</b> A rede da nossa casa, geralmente com um roteador Wi-Fi simples conectando celulares e TVs.</li>
        <li><b>SOHO (Pequeno Escritório):</b> Uma rede um pouco mais estruturada para pequenos negócios ou quem trabalha de casa (Home Office).</li>
        <li><b>Empresa (Média/Grande):</b> Redes complexas, divididas em vários pedaços, com equipamentos pesados e segurança forte.</li>
      </ul>
    </li>
  </ul>

  <p><b>Unidades de Medida</b></p>
  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left">Unidade</th>
        <th align="center">Símbolo</th>
        <th align="left">O que é?</th>
        <th align="left">Onde usamos?</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>Bit</b></td>
        <td align="center"><code>b</code> (minúsculo)</td>
        <td>A menor pecinha de informação do computador (0 ou 1).</td>
        <td>Para medir a <b>velocidade</b> da internet (ex: 100 Mbps).</td>
      </tr>
      <tr>
        <td><b>Byte</b></td>
        <td align="center"><code>B</code> (maiúsculo)</td>
        <td>Um pacotinho com 8 bits juntos.</td>
        <td>Para medir o <b>tamanho</b> de um arquivo (ex: 2 GB).</td>
      </tr>
    </tbody>
  </table>
</details>

<hr/>

<details open>
  <summary><h3>🖥️ Módulo 2: Como a Rede se Organiza</h3></summary>
  <br/>

  <p><b>Como eles conversam?</b></p>
  <ul>
    <li><b>Cliente-Servidor:</b> Um lado pede (o celular) e o outro lado entrega (o servidor do Google). É como um cliente num restaurante fazendo o pedido ao garçom.</li>
    <li><b>Ponto a Ponto (P2P):</b> Todo mundo é cliente e servidor ao mesmo tempo. As máquinas trocam arquivos diretamente umas com as outras.</li>
  </ul>

  <p><b>Os Equipamentos</b></p>
  <ul>
    <li><b>Dispositivos Finais:</b> Onde a informação nasce ou termina. São os nossos aparelhos (PC, celular, impressora).</li>
    <li><b>Dispositivos Intermediários:</b> Os "guardas de trânsito" da rede. Eles decidem o melhor caminho para os dados passarem (Switches e Roteadores).</li>
  </ul>

  <p><b>Classificação por Distância</b></p>
  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left">Sigla</th>
        <th align="left">Nome</th>
        <th align="left">Qual é o tamanho?</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>PAN</b></td>
        <td>Rede Pessoal</td>
        <td>Curtíssimo alcance, pertinho do seu corpo (ex: fone Bluetooth).</td>
      </tr>
      <tr>
        <td><b>LAN</b></td>
        <td>Rede Local</td>
        <td>Tamanho de uma casa, sala de aula ou escritório.</td>
      </tr>
      <tr>
        <td><b>MAN</b></td>
        <td>Rede Metropolitana</td>
        <td>Tamanho de uma cidade inteira.</td>
      </tr>
      <tr>
        <td><b>WAN</b></td>
        <td>Rede de Longa Distância</td>
        <td>Conecta países e continentes (a própria Internet é uma WAN).</td>
      </tr>
    </tbody>
  </table>
</details>

<hr/>

<details open>
  <summary><h3>📡 Módulo 3: Cabos e Wi-Fi</h3></summary>
  <br/>

  <ul>
    <li><b>Wi-Fi (Redes Sem Fio):</b> Usa ondas de rádio invisíveis no ar para enviar os dados, dando mobilidade pra gente andar pela casa.</li>
    <li><b>Cabos (Meios Físicos):</b>
      <ul>
        <li><b>Cabo de Cobre (Trançado):</b> O famoso cabo de rede azul. Usa energia elétrica para enviar dados até 100 metros. Os fios são trançados por dentro para evitar chiados (interferência).</li>
        <li><b>Fibra Óptica:</b> Usa luz para enviar dados em vez de energia. É super rápida, imune a interferências de energia e consegue viajar por quilômetros de distância.</li>
      </ul>
    </li>
  </ul>
</details>

<hr/>

<details open>
  <summary><h3>📐 Módulos 4 & 5: Modelos OSI e TCP/IP</h3></summary>
  <br/>

  <p>Para computadores de marcas diferentes conseguirem conversar, eles precisam falar as mesmas "línguas" (os protocolos). Para organizar isso, usamos modelos divididos em camadas.</p>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left">Modelo OSI (Na Teoria)</th>
        <th align="left">TCP/IP (Na Prática)</th>
        <th align="left">O que rola aqui? (Exemplos)</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>7. Aplicação</b></td>
        <td rowspan="3" valign="middle"><b>Aplicação</b><br/><i>(Os programas e a tela)</i></td>
        <td rowspan="3" valign="middle">É onde a gente clica e interage. Protocolos de site (<code>HTTP</code>), e-mail e <code>DNS</code>.</td>
      </tr>
      <tr>
        <td><b>6. Apresentação</b></td>
      </tr>
      <tr>
        <td><b>5. Sessão</b></td>
      </tr>
      <tr>
        <td><b>4. Transporte</b></td>
        <td valign="middle"><b>Transporte</b><br/><i>(Controle da entrega)</i></td>
        <td>Controla se o pacote chegou inteiro ou quebrado (<code>TCP</code> e <code>UDP</code>).<br/><b>Pacotinho chama:</b> Segmento.</td>
      </tr>
      <tr>
        <td><b>3. Rede</b></td>
        <td valign="middle"><b>Internet</b><br/><i>(Endereços IP e rotas)</i></td>
        <td>É o "correio". Usa o <code>IPv4</code> ou <code>IPv6</code> para achar o melhor caminho.<br/><b>Pacotinho chama:</b> Pacote.</td>
      </tr>
      <tr>
        <td><b>2. Enlace de Dados</b></td>
        <td rowspan="2" valign="middle"><b>Acesso à Rede</b><br/><i>(Placa de rede e cabos)</i></td>
        <td rowspan="2" valign="middle">A parte física. O cabo de rede, a placa Wi-Fi, luzes piscando e o endereço <code>MAC</code>.</td>
      </tr>
      <tr>
        <td><b>1. Física</b></td>
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
