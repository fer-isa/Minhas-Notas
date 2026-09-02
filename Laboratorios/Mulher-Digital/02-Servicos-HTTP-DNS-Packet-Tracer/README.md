<div align="center">
  <h2>🌐 Laboratório de Redes: Como a Internet Funciona (HTTP & DNS)</h2>
  <p><i>Meus estudos práticos sobre como os computadores encontram e carregam sites na rede</i></p>
  
  <img src="https://img.shields.io/badge/Cisco_Packet_Tracer-049CE4?style=for-the-badge&logo=cisco&logoColor=white" />
  <img src="https://img.shields.io/badge/Networking-CCST-success?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Skills-DNS%20|%20HTTP%20|%20Troubleshooting-blue?style=for-the-badge">
</div>

<br>

### 🎯 O Objetivo do Laboratório
Neste exercício, o foco foi entender o que acontece "por baixo dos panos" quando digitamos o endereço de um site no navegador. O objetivo prático foi configurar um Servidor Central para hospedar uma página Web (serviço HTTP) e atuar como um tradutor de nomes (serviço DNS), permitindo que o computador cliente acesse o site pelo nome em vez de decorar números de IP.

### 🗺️ A Topologia da Rede
<div align="center">
  <!-- PRINT 1: Topologia -->
 <img width="637" height="550" alt="topologia " src="https://github.com/user-attachments/assets/21401005-685a-45b1-8422-5d32db5ecd30" />
  <p><i>Cenário: 1 Switch de Acesso (2960), 1 Servidor Central e 1 PC Cliente conectados via cabo direto.</i></p>
</div>

<br>

### 💡 O Que Eu Aprendi e Meus Desafios Reais

Documentar quando as coisas dão errado é a melhor forma de aprender. Durante a montagem deste laboratório, enfrentei alguns obstáculos práticos que me ajudaram a entender como a investigação de redes (troubleshooting) funciona na vida real:

<ul>
  <li>
    <b>A "Pegadinha" do Serviço DNS:</b> Em determinado momento, os testes de resolução de nomes falharam. Eu tinha certeza de que havia configurado os IPs corretos na tabela. O problema? Eu havia esquecido de marcar a opção "On" para ativar o serviço no servidor. O aprendizado aqui foi sobre atenção aos detalhes básicos: não basta preencher as tabelas, é preciso garantir que o serviço esteja de fato rodando.
  </li>
  <li>
    <b>Atenção à Sintaxe no Terminal:</b> Tive um pouco de dificuldade com a sintaxe exata dos comandos. Ao tentar investigar o domínio, digitei <code>nslookup [www.aula.com]</code>. O terminal retornou um erro de domínio inexistente porque ele interpretou os colchetes como parte do nome do site. Aprendi na marra que o prompt de comando (CLI) não perdoa erros de digitação e exige comandos limpos e diretos.
  </li>
  <li>
    <b>Adaptação à "Tela Preta":</b> A própria navegação e uso do terminal (Command Prompt) ainda é um desafio para mim. Entender como interpretar um erro no meio de várias linhas de código tem sido um ótimo exercício de paciência e foco investigativo.
  </li>
</ul>

<br>

### ⚙️ Configurações Passo a Passo

<details>
  <summary><b>🛠️ 1. Endereçamento IP e Apontamento (Clique para expandir)</b></summary>
  <br>
  <div align="center">
    <!-- PRINT 2: Configuração IP do PC -->
    <img width="945" height="860" alt="ip-configuration" src="https://github.com/user-attachments/assets/eb5627ba-2299-451a-b511-2bf6fb02be9e" />
    <p><i>Configuração estática do PC-Cliente. O detalhe fundamental aqui foi apontar o campo "DNS Server" para o IP do nosso Servidor (192.168.1.10). Sem esse apontamento, o PC não saberia a quem pedir a tradução dos nomes.</i></p>
  </div>
</details>

<details>
  <summary><b>💻 2. Subindo a Página Web - HTTP (Clique para expandir)</b></summary>
  <br>
  <div align="center">
    <!-- PRINT 3: Edição do index.html -->
   <img width="952" height="852" alt="Captura de tela 2026-09-01 203519" src="https://github.com/user-attachments/assets/33fddfa3-0edc-4ee4-ba01-e18ffcac42ed" />
    <p><i>Edição do arquivo <code>index.html</code> dentro do serviço HTTP do servidor. Personalizei o código HTML para confirmar visualmente que o serviço estava entregando o arquivo correto.</i></p>
  </div>
</details>

<details>
  <summary><b>📖 3. Cadastrando o Domínio - DNS (Clique para expandir)</b></summary>
  <br>
  <div align="center">
    <!-- PRINT 4: Registro no DNS -->
    <img width="952" height="816" alt="configuração-dns" src="https://github.com/user-attachments/assets/c728f7f7-a12a-4949-9b01-c83c56206843" />
    <p><i>Criação do registro (A Record) no serviço DNS do servidor, vinculando o domínio <code>www.aula.com</code> ao IP <code>192.168.1.10</code>.</i></p>
  </div>
</details>

<br>

### ✅ Testes e Validação Final
Para provar que a teoria funcionou na prática, executei os seguintes testes a partir do PC-Cliente:

<details>
  <summary><b>🔍 Teste de Conectividade (Ping) e Resolução (nslookup) (Clique para expandir)</b></summary>
  <br>
  <div align="center">
    <!-- PRINT 5: Tela preta do Prompt -->
   <img width="906" height="372" alt="tela certa" src="https://github.com/user-attachments/assets/3f413d55-d3b8-489a-b853-2a204910fb01" />
<p><i>O <code>ping</code> confirmou a comunicação física com o servidor. Já no <code>nslookup</code>, o primeiro teste falhou porque acabei usando colchetes por engano (erro de sintaxe). Assim que digitei o comando limpo, comprovei que o DNS estava ativo e traduzindo o nome perfeitamente!</i></p>
  </div>
</details>

<details>
  <summary><b>🌐 Acessando o Site pelo Navegador (Clique para expandir)</b></summary>
  <br>
  <div align="center">
    <!-- PRINT 6: Navegador abrindo a página -->
  
<img width="947" height="822" alt="Captura de tela 2026-09-01 215042" src="https://github.com/user-attachments/assets/e6aad443-33d6-4f31-82d6-a45400700a1f" />
    <p><i>O teste definitivo: o navegador solicitou o domínio, o DNS traduziu para o IP, e o serviço HTTP entregou a nossa página personalizada perfeitamente!</i></p>
  </div>
</details>

<br>

---
<div align="center">
  <i>Documentação do meu aprendizado contínuo. Focada em entender os fundamentos da camada de aplicação e processos de investigação técnica.</i>
</div>










