<div align="center">
  <h1>🌐 Laboratório Prático: Rede de Pequeno Escritório (SOHO)</h1>
  <p><b>Montando uma rede do zero com Wi-Fi, cabo e distribuição automática de IPs (DHCP)</b></p>
  
  <p>
    <img src="https://img.shields.io/badge/Cisco%20Packet%20Tracer-005073?style=for-the-badge&logo=cisco&logoColor=white" alt="Cisco Packet Tracer" />
    <img src="https://img.shields.io/badge/Topologia-SOHO-0A84FF?style=for-the-badge" alt="SOHO" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>
</div>

<hr/>

### 📌 1. O Que Eu Fiz Neste Projeto
Neste laboratório, construí a infraestrutura de rede de um pequeno escritório (SOHO) literalmente do zero no Packet Tracer! Minha missão foi selecionar os equipamentos, realizar o cabeamento físico e configurar os serviços.

A topologia conta com um acesso à internet simulado (Nuvem e Modem), um Roteador Wi-Fi central, equipamentos conectados por cabo (PCs e Impressora) e dispositivos móveis via rede sem fio (Notebook e Smartphone).

<div align="center">

  <img width="756" height="507" alt="topologia" src="https://github.com/user-attachments/assets/505bf828-08be-4683-bddb-9859fa9681ad" />

  <p><i>Topologia Física: A planta do nosso escritório com a distribuição de todos os aparelhos que adicionei e conectei.</i></p>
</div>

<hr/>

### ⚙️ 2. Como a Rede Foi Configurada
Para colocar essa rede para funcionar, executei os seguintes passos práticos:

* **Cabeamento Físico:** Conectei a nuvem do provedor ao Modem (usando cabo coaxial) e liguei os computadores e a impressora diretamente nas portas do roteador (usando cabo par trançado direto).
* **Criação da Rede Wi-Fi:** Acessei a interface do roteador, nomeei a rede como <code>Escritorio_Firma</code> e apliquei a segurança WPA2-Personal com senha.
* **Adaptação de Hardware:** No simulador, precisei desligar o Notebook virtual, remover sua placa de rede cabeada e instalar um módulo Wi-Fi para que ele pudesse captar o sinal.
* **IP Automático (DHCP):** Configurei os computadores, a impressora e o celular para receberem seus endereços IP automaticamente do roteador.

<hr/>

### 🚧 3. Meus Desafios e Aprendizados Reais
Durante a montagem, esbarrei em alguns obstáculos que me ensinaram muito sobre resolução de problemas (troubleshooting) e o comportamento dos equipamentos:

<ul>
  <li>
    <b>O "Sumo" da Configuração WPA2:</b> Após configurar a segurança da rede sem fio com a senha, percebi que o roteador não estava transmitindo o sinal e as opções apareciam como "desabilitadas". Aprendi na marra que, na interface gráfica do roteador, é obrigatório rolar a tela até o final e clicar em "Save Settings" a cada mínima alteração de aba, senão a configuração é descartada!
  </li>
  <li>
    <b>A Troca da Placa do Notebook:</b> Eu sabia que precisava trocar a conexão de cabo do laptop para uma antena Wi-Fi, mas tive que pesquisar para relembrar uma regra básica de hardware: no simulador (assim como na vida real), precisamos "desligar" a máquina no botão físico antes de trocar qualquer peça.
  </li>
  <li>
    <b>A "Pegadinha" do Tempo:</b> Após configurar o Wi-Fi, o celular parecia não conectar de jeito nenhum. Minha configuração estava certa; o segredo era apenas clicar no botão de avançar o tempo (<i>Fast Forward Time</i>) para o simulador processar a comunicação e as ondas do Wi-Fi aparecerem.
  </li>
</ul>

### ✅ 4. Testando se Tudo Funciona
Para provar que a rede realmente está se comunicando e entregando o que promete, fiz dois testes práticos direto do Smartphone conectado no Wi-Fi:

<div align="center">
  <img width="947" height="997" alt="dhcp-smartphone" src="https://github.com/user-attachments/assets/bb192a06-3603-4833-8e15-4e5ed9600157" />
  <p><i><b>Teste 1 (DHCP):</b> O Smartphone solicitou um IP e o roteador entregou perfeitamente o endereço <code>192.168.0.101</code> de forma automática. Nenhuma configuração manual foi necessária.</i></p>
</div>

<br>

<div align="center">
  <img width="945" height="986" alt="ping-Smartfone" src="https://github.com/user-attachments/assets/72089515-d0cf-4cf0-a851-e57b3811b6b2" />
  <p><i><b>Teste 2 (Conectividade):</b> Usando o terminal do Smartphone, o comando <code>ping</code> confirmou a comunicação direta e sem perdas com o roteador (Gateway <code>192.168.0.1</code>).</i></p>
</div>

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
