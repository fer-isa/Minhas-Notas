<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=HTTP%20e%20DNS&fontSize=64&fontColor=FFFFFF&fontAlignY=35&desc=Como%20a%20Internet%20Funciona%20%7C%20Laborat%C3%B3rio%20Cisco&descAlignY=55&descSize=20&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Cisco_Packet_Tracer-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Networking_CCST-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Troubleshooting-161B22?style=for-the-badge&logo=quicklook&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo do Laboratório
Neste exercício, o foco foi entender o que acontece "por baixo dos panos" quando digitamos o endereço de um site no navegador. O objetivo prático foi configurar um Servidor Central para hospedar uma página Web (serviço HTTP) e atuar como um tradutor de nomes (serviço DNS), permitindo que o computador cliente acesse o site pelo nome em vez de decorar números de IP.

> **🛡️ Visão de Segurança (SOC):** 
> Compreender o fluxo de DNS e HTTP é vital para a defesa cibernética. Em um SOC, analisar consultas DNS suspeitas é uma das principais formas de descobrir se uma máquina da rede foi infectada e está se comunicando com um invasor (C2). Da mesma forma, o tráfego HTTP é o vetor principal para investigar ataques a aplicações web.

---

## 🗺️ A Topologia da Rede
<div align="center">
  <img width="637" height="550" alt="topologia" src="https://github.com/user-attachments/assets/21401005-685a-45b1-8422-5d32db5ecd30" />
  <p><i>Cenário: 1 Switch de Acesso (2960), 1 Servidor Central e 1 PC Cliente conectados via cabo direto.</i></p>
</div>

---

## 💡 O Que Aprendi e Meus Desafios Reais

Documentar quando as coisas dão errado é a melhor forma de aprender. Durante a montagem deste laboratório, enfrentei obstáculos práticos que me ajudaram a entender como a investigação (troubleshooting) funciona na vida real:

*   **A "Pegadinha" do Serviço DNS:** Em determinado momento, os testes de resolução de nomes falharam. Eu tinha certeza de que havia configurado os IPs corretos na tabela. O problema? Havia esquecido de marcar a opção "On" para ativar o serviço no servidor. O aprendizado: não basta preencher as tabelas, é preciso garantir que o serviço esteja ativado. Atenção aos detalhes básicos é essencial.
*   **Atenção à Sintaxe no Terminal:** Tive dificuldade com a sintaxe exata dos comandos. Ao tentar investigar o domínio, digitei <code>nslookup [www.aula.com]</code>. O terminal retornou um erro de domínio inexistente porque interpretou os colchetes como parte do nome do site. Aprendi na prática que o prompt (CLI) exige comandos limpos e diretos.
*   **Adaptação à "Tela Preta":** A própria navegação e uso do terminal (Command Prompt) tem sido um ótimo exercício de paciência e foco investigativo, me ensinando a interpretar mensagens de erro no meio de várias linhas de execução.

---

## ⚙️ Configurações Passo a Passo

<details>
  <summary><b>🛠️ 1. Endereçamento IP e Apontamento DNS (Clique para expandir)</b></summary>
  <br>
  <div align="center">
    <img width="945" height="860" alt="ip-configuration" src="https://github.com/user-attachments/assets/eb5627ba-2299-451a-b511-2bf6fb02be9e" />
    <p><i>Configuração estática do PC-Cliente. O detalhe fundamental aqui foi apontar o campo "DNS Server" para o IP do nosso Servidor (192.168.1.10). Sem esse apontamento, o PC não saberia a quem pedir a tradução dos nomes.</i></p>
  </div>
</details>

<details>
  <summary><b>💻 2. Subindo a Página Web - HTTP (Clique para expandir)</b></summary>
  <br>
  <div align="center">
    <img width="952" height="852" alt="Captura de tela 2026-09-01 203519" src="https://github.com/user-attachments/assets/33fddfa3-0edc-4ee4-ba01-e18ffcac42ed" />
    <p><i>Edição do arquivo <code>index.html</code> dentro do serviço HTTP do servidor. Personalizei o código HTML para confirmar visualmente que o serviço estava entregando o arquivo correto.</i></p>
  </div>
</details>

<details>
  <summary><b>📖 3. Cadastrando o Domínio - DNS (Clique para expandir)</b></summary>
  <br>
  <div align="center">
    <img width="952" height="816" alt="configuração-dns" src="https://github.com/user-attachments/assets/c728f7f7-a12a-4949-9b01-c83c56206843" />
    <p><i>Criação do registro (A Record) no serviço DNS do servidor, vinculando o domínio <code>www.aula.com</code> ao IP <code>192.168.1.10</code>.</i></p>
  </div>
</details>

---

## ✅ Testes e Validação Final

Para provar que a teoria funcionou na prática, executei os seguintes testes a partir do PC-Cliente:

<details>
  <summary><b>🔍 Teste de Conectividade (Ping) e Resolução (nslookup) (Clique para expandir)</b></summary>
  <br>
  <div align="center">
    <img width="906" height="372" alt="tela certa" src="https://github.com/user-attachments/assets/3f413d55-d3b8-489a-b853-2a204910fb01" />
    <p><i>O <code>ping</code> confirmou a comunicação física com o servidor. Já no <code>nslookup</code>, o primeiro teste falhou pelo uso acidental de colchetes (erro de sintaxe). Ao digitar o comando limpo, comprovei que o DNS estava ativo e traduzindo o nome perfeitamente!</i></p>
  </div>
</details>

<details>
  <summary><b>🌐 Acessando o Site pelo Navegador (Clique para expandir)</b></summary>
  <br>
  <div align="center">
    <img width="947" height="822" alt="Captura de tela 2026-09-01 215042" src="https://github.com/user-attachments/assets/e6aad443-33d6-4f31-82d6-a45400700a1f" />
    <p><i>O teste definitivo: o navegador solicitou o domínio, o DNS traduziu para o IP, e o serviço HTTP entregou a nossa página personalizada perfeitamente.</i></p>
  </div>
</details>

<br>

<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Minhas_Notas-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2A4365,50:1A365D,100:0B1D3A&height=100&section=footer" width="100%" />
