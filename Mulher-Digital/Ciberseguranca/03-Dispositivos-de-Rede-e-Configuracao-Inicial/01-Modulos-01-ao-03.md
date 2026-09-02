<div align="center">
 <img width="200" height="200" alt="networking-devices-and-initial-configuration" src="https://github.com/user-attachments/assets/9f6350dd-27e1-4f96-873e-49dc052ffb73" 
 alt="Emblema do Módulo" />
  
  <h2>🛠️ Dispositivos de Rede & Arquitetura — Módulos 1 ao 3</h2>
  <p><b>Formação Mulher Digital • Trilha de Cibersegurança & Infraestrutura</b></p>
  
  <p>
    <img src="https://img.shields.io/badge/Cisco_Networking_Academy-Arquitetura_%26_Nuvem-005073?style=for-the-badge&logo=cisco&logoColor=white" alt="Arquitetura" />
    <img src="https://img.shields.io/badge/Trilha-Mulher_Digital-8A2BE2?style=for-the-badge" alt="Mulher Digital" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>
</div>

<hr/>

<h3>📌 Visão Geral</h3>
<p>Um resumo prático de como montar uma rede que não cai, como organizar os equipamentos (o famoso modelo de 3 camadas da Cisco), como funciona a Computação em Nuvem e como traduzir os endereços IP para a linguagem das máquinas (os zeros e uns).</p>

<hr/>

<details open>
  <summary><h3>📝 A "Rede de Papel" (Entendendo a Lógica)</h3></summary>
  <br/>

  <p><b>1. Os 4 Pilares de uma Boa Rede</b></p>
  <ul>
    <li>🛡️ <b>Tolerância a Falhas:</b> Se um cabo partir, a rede acha outro caminho sozinha. Ela não pode parar!</li>
    <li>📈 <b>Escalabilidade:</b> A rede precisa conseguir crescer (colocar mais computadores e filiais) sem precisarmos jogar os aparelhos antigos fora e recomeçar do zero.</li>
    <li>🚦 <b>Qualidade de Serviço (QoS):</b> Dar passagem "VIP" para o que importa. Por exemplo, a rede não deixa uma chamada de vídeo travar só porque alguém na outra sala está baixando um arquivo pesado.</li>
    <li>🔒 <b>Segurança:</b> Proteger os dados e garantir que só quem tem crachá consiga entrar.</li>
  </ul>

  <p><b>2. O Prédio da Cisco (Modelo de 3 Camadas)</b></p>
  <ul>
    <li>🏢 <b>Camada de Acesso (O Nosso Andar):</b> Onde ligamos o cabo no nosso PC, na impressora ou no Wi-Fi. É a linha de frente de contato com o usuário.</li>
    <li>🔌 <b>Camada de Distribuição (O Quadro de Força):</b> O "gerente". Ele junta os cabos que vêm de todos os andares de Acesso e aplica as regras de segurança e roteamento.</li>
    <li>🚀 <b>Camada de Núcleo / Core (A Via Expressa):</b> O "chefão". Liga prédios e servidores inteiros. Ele não perde tempo checando regrinhas; a única função dele é transportar um volume gigante de dados de um lado para o outro o mais rápido possível.</li>
  </ul>
</details>

<hr/>

<details open>
  <summary><h3>⚙️ A Prática (O que importa)</h3></summary>
  <br/>

  <p><b>A Nuvem (O Computador dos Outros)</b></p>
  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left">Serviço (A Sigla)</th>
        <th align="left">O que é na prática?</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>SaaS (Software)</b></td>
        <td>Tudo pronto. Você só abre o navegador e usa sem instalar nada (Ex: Canva, Google Workspace).</td>
      </tr>
      <tr>
        <td><b>PaaS (Plataforma)</b></td>
        <td>O ambiente montadinho para quem é programador só chegar e colocar o aplicativo no ar.</td>
      </tr>
      <tr>
        <td><b>IaaS (Infraestrutura)</b></td>
        <td>Você aluga a "máquina virtual" crua e configura exatamente do seu jeito (Ex: AWS, Azure).</td>
      </tr>
    </tbody>
  </table>

  <br>

  <p><b>Máquinas Virtuais (Hipervisores)</b></p>
  <ul>
    <li><b>Tipo 1 (Bare-Metal):</b> Vai direto no hardware "seco" do servidor da empresa, sem Windows por baixo. É super rápido e profissional.</li>
    <li><b>Tipo 2 (Hosted):</b> Aquele que a gente instala como se fosse um joguinho no nosso PC para estudar (Ex: VirtualBox).</li>
  </ul>

  <br>

  <p><b>Matemática Binária: Como o PC lê o IP (Ex: 192.168.10.5)</b></p>
  <p>Usamos a "Tabelinha Mágica" <code>(128, 64, 32, 16, 8, 4, 2, 1)</code>. Se o número da tabela servir para somar e chegar no valor do pedaço do IP, colocamos <b>1</b> (Ligado). Se ele for muito grande e não servir, colocamos <b>0</b> (Desligado).</p>
  
  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="center">128</th>
        <th align="center">64</th>
        <th align="center">32</th>
        <th align="center">16</th>
        <th align="center">8</th>
        <th align="center">4</th>
        <th align="center">2</th>
        <th align="center">1</th>
        <th align="left">Matemática (Resultado)</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td align="center"><b>1</b></td>
        <td align="center"><b>1</b></td>
        <td align="center">0</td>
        <td align="center">0</td>
        <td align="center">0</td>
        <td align="center">0</td>
        <td align="center">0</td>
        <td align="center">0</td>
        <td><code>192</code> (128 + 64)</td>
      </tr>
      <tr>
        <td align="center"><b>1</b></td>
        <td align="center">0</td>
        <td align="center"><b>1</b></td>
        <td align="center">0</td>
        <td align="center"><b>1</b></td>
        <td align="center">0</td>
        <td align="center">0</td>
        <td align="center">0</td>
        <td><code>168</code> (128 + 32 + 8)</td>
      </tr>
      <tr>
        <td align="center">0</td>
        <td align="center">0</td>
        <td align="center">0</td>
        <td align="center">0</td>
        <td align="center"><b>1</b></td>
        <td align="center">0</td>
        <td align="center"><b>1</b></td>
        <td align="center">0</td>
        <td><code>10</code> (8 + 2)</td>
      </tr>
      <tr>
        <td align="center">0</td>
        <td align="center">0</td>
        <td align="center">0</td>
        <td align="center">0</td>
        <td align="center">0</td>
        <td align="center"><b>1</b></td>
        <td align="center">0</td>
        <td align="center"><b>1</b></td>
        <td><code>5</code> (4 + 1)</td>
      </tr>
    </tbody>
  </table>
</details>

<hr/>

<h3>💡 Minha Visão (O Resumo da Fer)</h3>
<p><i>
O que mais me ajudou a fixar esse módulo foi desenhar as três camadas da Cisco na minha cabeça. Fica muito mais fácil entender a rede quando a gente pensa num prédio comercial: a Camada de Acesso é a mesa do nosso andar, a Distribuição é o quadro de força do prédio que junta todos os andares, e o Core é a avenida expressa lá fora ligando um prédio no outro. Outro "clique" maravilhoso foi aprender a converter IPs para binário. Tinha muito texto nos cursos e no começo assusta, mas quando a gente monta a tabelinha do 128 ao 1 e vai só encaixando os números na soma (ligando ou desligando a "luz"), fica super divertido! É muito legal saber que a gente consegue traduzir a linguagem da máquina na ponta do lápis, tirando de vez o medo de mexer com zeros e uns!
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
