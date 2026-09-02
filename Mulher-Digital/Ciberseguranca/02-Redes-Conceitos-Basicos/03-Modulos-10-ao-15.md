<div align="center">
  <h2>🌐 Conceitos Básicos de Redes — Módulos 10 ao 15</h2>
  <p><b>Formação Mulher Digital • Trilha de Cibersegurança & Infraestrutura</b></p>
  
  <p>
    <img src="https://img.shields.io/badge/Cisco_Networking_Academy-Roteamento_%26_IP-005073?style=for-the-badge&logo=cisco&logoColor=white" alt="Roteamento" />
    <img src="https://img.shields.io/badge/Protocolos-DHCP_%7C_DNS_%7C_ARP-0A84FF?style=for-the-badge" alt="Protocolos" />
    <img src="https://img.shields.io/badge/Trilha-Mulher_Digital-8A2BE2?style=for-the-badge" alt="Mulher Digital" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>
</div>

<hr/>

<h3>📌 Visão Geral</h3>
<p>O fechamento da nossa base de redes! Aqui desmistificamos como os IPs e as máscaras funcionam, os 3 protocolos mágicos que fazem a rede ter vida (DHCP, DNS e ARP), como os roteadores escolhem caminhos e os comandos essenciais para testar se tudo está funcionando.</p>

<hr/>

<details open>
  <summary><h3>📝 A "Rede de Papel" (Entendendo a Lógica)</h3></summary>
  <br/>

  <p><b>1. Endereço IP e a Máscara (Rua e Casa)</b><br>
  Todo IP é dividido em duas partes. A <b>Máscara de Sub-rede</b> é o "muro" que separa essas duas coisas: ela diz aos equipamentos até onde vai o nome da rua (A Rede) e onde começa o número da casa (O Host).</p>

  <p><b>2. IPs Públicos vs. Privados</b></p>
  <ul>
    <li>🌍 <b>IP Público:</b> É o endereço oficial da sua casa na internet. Só existe um no mundo inteiro e é roteável em qualquer lugar.</li>
    <li>🏠 <b>IP Privado:</b> É o apelido que você dá para os cômodos de casa (Quarto 1, Quarto 2). A internet lá fora não faz ideia de quem são eles; só o seu roteador local os conhece.</li>
  </ul>

  <p><b>3. O Jeito de Falar (Modos de Transmissão)</b></p>
  <ul>
    <li>📞 <b>Unicast:</b> Uma ligação telefônica privada. Um fala direto com o outro (1 para 1).</li>
    <li>📢 <b>Broadcast:</b> Pegar um megafone e gritar no meio da sala. Todos os computadores da rede local escutam (1 para Todos).</li>
    <li>💬 <b>Multicast:</b> Mandar mensagem num grupo do WhatsApp. Só recebe quem faz parte daquele grupo específico (1 para Alguns).</li>
  </ul>
</details>

<hr/>

<details open>
  <summary><h3>⚙️ A Prática (O que importa)</h3></summary>
  <br/>

  <p><b>Os 3 Protocolos Salva-Vidas</b></p>
  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left">Protocolo</th>
        <th align="left">O que faz na prática?</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>DHCP</b></td>
        <td>O recepcionista automático. Quando você conecta o cabo, ele te empresta um IP, uma máscara e um gateway para você poder navegar sem configurar nada à mão.</td>
      </tr>
      <tr>
        <td><b>DNS</b></td>
        <td>A agenda telefônica da internet. Transforma nomes fáceis (<i>google.com</i>) nos números IP que as máquinas precisam para se achar.</td>
      </tr>
      <tr>
        <td><b>ARP</b></td>
        <td>O detetive da rede local. Ele grita (Broadcast): <i>"Quem é o dono do IP 192.168.1.10? Me dê o seu endereço físico (MAC)!"</i></td>
      </tr>
    </tbody>
  </table>

  <br>

  <p><b>Como o Roteador escolhe o caminho (Rotas)</b></p>
  <ul>
    <li><b>Rota Estática:</b> O administrador digita o caminho na mão. É seguro, mas dá muito trabalho se a rede for grande.</li>
    <li><b>Rota Dinâmica (OSPF / RIP):</b> É o "Waze" dos roteadores. Eles conversam entre si e recalculam a rota sozinhos se um cabo quebrar no meio do caminho.</li>
  </ul>

  <br>
<p><b>Comandos Mágicos (A "Tela Preta")</b></p>
  <pre>
    
 #### Mostra o seu IP, sua Máscara e o seu endereço MAC físico
ipconfig /all

 #### Mostra a lista de quem o seu computador já conhece na rede local (IP associado ao MAC)
arp -a

 #### Testa se a internet está chegando até o destino (ex: tenta bater na porta do Google)
ping 8.8.8.8

 #### Mostra o caminho exato e todos os roteadores por onde o seu pacote passou até o destino
tracert 8.8.8.8
  </pre>

<hr/>

<h3>💡 Minha Visão (O Resumo da Fer)</h3>
<p><i>
O maior "clique" que eu tive ao fechar esses módulos foi ver a mágica acontecendo por trás dos panos quando a gente liga um computador novo na rede. Entender que o PC entra "cego", grita na rede pedindo um IP pro DHCP e depois usa o detetive ARP para descobrir com quem ele precisa falar, me fez perceber que a rede é uma grande conversa constante entre as máquinas. Outra coisa que adorei foi usar o comando <code>tracert</code> no Packet Tracer. Ver o caminho exato, pulando de roteador em roteador até chegar no destino, tira a internet daquela "nuvem abstrata" e mostra que tudo é físico e muito bem arquitetado!
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
