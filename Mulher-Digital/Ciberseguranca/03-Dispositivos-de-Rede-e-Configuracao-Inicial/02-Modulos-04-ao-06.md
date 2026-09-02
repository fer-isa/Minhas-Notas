<div align="center">
  <h2>🌐 Comutação Ethernet & Camada de Rede — Módulos 4 ao 6</h2>
  <p><b>Formação Mulher Digital • Trilha de Cibersegurança & Infraestrutura</b></p>
  
  <p>
    <img src="https://img.shields.io/badge/Cisco_Networking_Academy-Comutação_%26_IP-005073?style=for-the-badge&logo=cisco&logoColor=white" alt="Comutação e IP" />
    <img src="https://img.shields.io/badge/Trilha-Mulher_Digital-8A2BE2?style=for-the-badge" alt="Mulher Digital" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>
</div>

<hr/>

<h3>📌 Visão Geral</h3>
<p>Neste resumo, vamos entender como os dados viajam fisicamente pelo cabo da rede (Ethernet), como um Switch usa sua memória para aprender caminhos e como o protocolo IP age como o "entregador dos correios" da internet.</p>

<hr/>

<details open>
  <summary><h3>📝 A "Rede de Papel" (Entendendo a Lógica)</h3></summary>
  <br/>

  <p><b>1. O Envelope (O Quadro Ethernet)</b><br>
  Quando a mensagem sai do seu PC para o cabo de rede, ela vira um "Quadro". Ele tem um tamanho limite (se for muito pequeno, a rede acha que é lixo de colisão; se for muito grande, a rede rejeita). O que tem nesse envelope?</p>
  <ul>
    <li><b>Aviso:</b> "Atenção, lá vai mensagem!" (Sincroniza o relógio das máquinas).</li>
    <li><b>Endereços MAC:</b> Quem está mandando (Origem) e quem vai receber (Destino).</li>
    <li><b>O Pacote:</b> A mensagem em si.</li>
    <li><b>O Selo de Garantia (FCS):</b> Um código matemático no final do envelope. Se chegar rasgado ou com erro físico, a máquina descarta na hora.</li>
  </ul>

  <p><b>2. O Chassi (Endereço MAC)</b><br>
  Todo endereço MAC tem 48 bits e é dividido bem no meio (metade/metade):</p>
  <ul>
    <li><b>A Marca (OUI):</b> A primeira metade diz quem fabricou a placa de rede (ex: Cisco, Intel, Dell).</li>
    <li><b>O Número de Série:</b> A segunda metade é o número de identificação único daquela placa no mundo.</li>
  </ul>

  <p><b>3. Como o Switch "Pensa" (A Tabela MAC)</b><br>
  O switch é super inteligente, mas quando ele liga na tomada, ele não conhece ninguém. Ele aprende sozinho em 3 passos:</p>
  <ul>
    <li><b>Anota o Remetente (Aprendizado):</b> "Opa, o PC 1 mandou mensagem pela Porta 2. Vou anotar o MAC dele na minha caderneta."</li>
    <li><b>Entrega Direta (Encaminhamento):</b> Se ele já conhece o destinatário, ele manda a mensagem <i>só</i> para a porta daquela pessoa.</li>
    <li><b>O Grito (Inundação):</b> Se ele não sabe onde o destinatário está, ele manda a mensagem para <i>todas as portas</i> (menos a que enviou). Quem for o dono responde, e aí o switch anota na caderneta.</li>
  </ul>
</details>

<hr/>

<details open>
  <summary><h3>⚙️ A Prática (O que importa)</h3></summary>
  <br/>

  <p><b>O Protocolo IP (O Carteiro da Camada 3)</b></p>
  <ul>
    <li><b>Sem Conexão:</b> Ele não liga antes para avisar que a carta está chegando. Ele simplesmente manda.</li>
    <li><b>Melhor Esforço:</b> O IP faz o possível para entregar, mas <i>não garante</i> nada! Se o pacote sumir, ele não manda de novo (quem faz o trabalho de cobrar e retransmitir é o protocolo TCP, na camada de cima).</li>
    <li><b>Independente:</b> O IP não liga se a mensagem vai viajar por Wi-Fi, cabo de cobre ou fibra óptica. O formato dele é sempre o mesmo.</li>
  </ul>

  <br>

  <p><b>A Evolução: IPv4 vs. IPv6 (Por baixo dos panos)</b></p>
  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left">O que mudou?</th>
        <th align="left">IPv4</th>
        <th align="left">IPv6</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>Endereços</b></td>
        <td>4 bilhões (já acabou).</td>
        <td>Praticamente infinito (trilhões de trilhões).</td>
      </tr>
      <tr>
        <td><b>Cabeçalho (A Capa)</b></td>
        <td>Varia de tamanho (de 20 a 60 bytes).</td>
        <td>Tamanho fixo de 40 bytes (muito mais rápido para o roteador ler).</td>
      </tr>
      <tr>
        <td><b>Quebrar o pacote (Fragmentação)</b></td>
        <td>Qualquer roteador no meio do caminho pode quebrar o pacote em pedaços menores.</td>
        <td>Só o PC que está enviando a mensagem tem permissão de quebrar o pacote. Deixa a rede mais rápida!</td>
      </tr>
    </tbody>
  </table>
</details>

<hr/>

<h3>💡 Minha Visão (O Resumo da Fer)</h3>
<p><i>
O que fez a minha cabeça explodir nesse módulo foi entender como o Switch é absurdamente eficiente. Antes eu achava que a rede era uma bagunça onde todo computador recebia a mensagem de todo mundo o tempo todo. Entender que o Switch tem uma memória (Tabela MAC) e que ele fica "escutando" as portas para mapear quem está onde, enviando as mensagens depois apenas para as portas corretas, me fez ver como a tecnologia de redes é elegante. Outra coisa que adorei foi a revelação sobre o protocolo IP: ele faz o "Melhor Esforço", mas não garante a entrega. É muito legal perceber que as funções são divididas e que a internet só funciona bem porque os protocolos trabalham em equipe!
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

