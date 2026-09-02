<div align="center">
  <h2>🌐 Conceitos Básicos de Redes — Módulos 6 ao 9</h2>
  <p><b>Formação Mulher Digital • Trilha de Cibersegurança & Infraestrutura</b></p>
  
  <p>
    <img src="https://img.shields.io/badge/Cisco_Networking_Academy-Redes_de_Computadores-005073?style=for-the-badge&logo=cisco&logoColor=white" alt="Redes" />
    <img src="https://img.shields.io/badge/Trilha-Mulher_Digital-8A2BE2?style=for-the-badge" alt="Mulher Digital" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>
</div>

<hr/>

<h3>📌 Visão Geral</h3>
<p>Neste resumo, trago a lógica de como os dados são empacotados para viajar, como os computadores ganham "nomes e CPFs" (IP, MAC e DNS) e como as empresas desenham e protegem suas redes na vida real.</p>

<hr/>

<details open>
  <summary><h3>📝 A "Rede de Papel" (Entendendo a Lógica)</h3></summary>
  <br/>

  <p><b>1. Encapsulamento (A Boneca Russa)</b><br>
  Quando você manda uma mensagem, ela não vai crua pra rede. Ela passa por um processo de empacotamento: o dado ganha um envelope (com os IPs de origem e destino) e depois é colocado dentro de uma "caixa" maior (o Quadro Ethernet, que recebe os endereços MAC) para conseguir viajar pelo cabo até o roteador.</p>

  <p><b>2. Identidade na Rede: MAC, IP e DNS</b></p>
  <ul>
    <li>🏷️ <b>Endereço MAC (O Chassi):</b> É o endereço físico da placa de rede. Ele vem gravado de fábrica e <i>nunca muda</i>. Serve para a comunicação local (dentro da mesma sala).</li>
    <li>🏠 <b>Endereço IP (O CEP da casa):</b> É o endereço lógico. Ele <i>muda</i> dependendo de onde você está conectado (seu PC tem um IP na sua casa e outro diferente no Wi-Fi do shopping). Serve para achar você na internet.</li>
    <li>📖 <b>DNS (A Agenda de Contatos):</b> Máquinas só entendem números (IPs). Nós preferimos nomes. O DNS é a agenda que traduz <code>www.google.com</code> para o IP correto dele.</li>
  </ul>

  <p><b>3. O Tamanho da Festa (Intranet, Extranet e Internet)</b></p>
  <ul>
    <li><b>Intranet:</b> A festa privada da empresa. Só funcionários com crachá (autenticados) podem entrar.</li>
    <li><b>Extranet:</b> A área VIP. A empresa abre uma "porta lateral" segura para parceiros e fornecedores acessarem alguns sistemas.</li>
    <li><b>Internet:</b> A praça pública, onde todo mundo se conecta.</li>
  </ul>
</details>

<hr/>

<details open>
  <summary><h3>⚙️ A Prática (O que importa)</h3></summary>
  <br/>

  <p><b>O famoso NAT (A mágica do Roteador)</b><br>
  A internet ficou sem endereços IPv4, então inventaram o NAT. Ele age como o <b>porteiro de um prédio</b>: o mundo lá fora só vê o IP do porteiro (o IP público). Quando a correspondência chega, o porteiro traduz o endereço e entrega no apartamento certo (os IPs privados dos nossos celulares e PCs).</p>

  <p><b>IPv4 vs. IPv6</b></p>
  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left">Protocolo</th>
        <th align="left">Como é?</th>
        <th align="left">Qual é a diferença?</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>IPv4</b></td>
        <td><code>192.168.1.10</code></td>
        <td>O modelo antigo. Tem "só" 4 bilhões de endereços e já esgotou. Usa números e pontos.</td>
      </tr>
      <tr>
        <td><b>IPv6</b></td>
        <td><code>2001:0db8::8a2e:0370</code></td>
        <td>O modelo novo e infinito. Usa números, letras e dois-pontos. Já vem com segurança nativa.</td>
      </tr>
    </tbody>
  </table>

  <br>
  
  <p><b>Desenhos de Rede (Topologias)</b></p>
  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left">Topologia</th>
        <th align="left">Como funciona na prática?</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>Estrela 🌟</b></td>
        <td>Todo mundo ligado num Switch central. Se um cabo quebra, só aquele PC fica sem internet. (É a mais usada!)</td>
      </tr>
      <tr>
        <td><b>Barramento 🚌</b></td>
        <td>Um cabo central onde todo mundo se pendura. Se o cabo principal partir, a rede inteira cai.</td>
      </tr>
      <tr>
        <td><b>Malha 🕸️</b></td>
        <td>Todo mundo tem um cabo ligado direto a todo mundo. Se um cabo quebrar, tem vários outros caminhos. Super seguro, mas caríssimo.</td>
      </tr>
    </tbody>
  </table>

  <br>
  
  <p><b>Hardening (Deixando a rede casca grossa)</b></p>
  <ul>
    <li><b>Menor Privilégio:</b> Dar ao funcionário APENAS o acesso que ele precisa para trabalhar. Nada de dar senha de administrador pra todo mundo.</li>
    <li><b>Gestão de Patches:</b> O famoso "manter tudo atualizado" para fechar brechas conhecidas pelos hackers.</li>
    <li><b>Criptografia em Trânsito:</b> Embaralhar a mensagem para que ninguém consiga ler o que está passando no cabo (usar HTTPS, SSH, VPN).</li>
  </ul>
</details>

<hr/>

<h3>💡 Minha Visão (O Resumo da Fer)</h3>
<p><i>
O que fez a minha cabeça explodir nesse módulo foi finalmente entender como a internet não parou, mesmo com os endereços IPv4 acabando há anos. O conceito do NAT é genial! Pensar no roteador da minha casa como um porteiro que recebe as respostas da internet (com um IP público só) e distribui perfeitamente para o meu celular, para a minha TV e para o meu PC (usando IPs privados que a internet nem faz ideia que existem) fez tudo se encaixar. E sobre as topologias, ficou claro por que a rede em "Estrela" dominou o mercado: ninguém quer que a empresa inteira pare de trabalhar só porque um único cabo quebrou.
</i></p>

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
