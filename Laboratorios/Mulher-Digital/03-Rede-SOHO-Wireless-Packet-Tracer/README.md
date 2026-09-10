<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Rede%20SOHO%20(Wi-Fi)&fontSize=64&fontColor=FFFFFF&fontAlignY=35&desc=Infraestrutura%20%7C%20Laborat%C3%B3rio%20Cisco&descAlignY=55&descSize=20&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Cisco_Packet_Tracer-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Networking_CCST-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Infraestrutura_SOHO-161B22?style=for-the-badge&logo=ubiquiti&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo do Laboratório
Neste projeto, minha missão foi construir a infraestrutura de rede de um pequeno escritório (SOHO - *Small Office/Home Office*) totalmente do zero no Packet Tracer. A topologia exigiu a seleção de equipamentos, realização de cabeamento físico, configuração de roteamento e serviços sem fio.

> **🛡️ Visão de Segurança (SOC):** 
> Para defender uma rede, primeiro é preciso saber como ela é construída. Entender a topologia física (onde os cabos estão ligados) e lógica (quem fornece o Wi-Fi e como o WPA2 autentica os usuários) é o que permite a um analista de SOC mapear a superfície de ataque, isolar dispositivos móveis comprometidos e rastrear atividades suspeitas a partir do IP do roteador.

---

## 🗺️ A Topologia da Rede
<div align="center">
  <img width="756" height="507" alt="topologia" src="https://github.com/user-attachments/assets/505bf828-08be-4683-bddb-9859fa9681ad" />
  <p><i>Topologia Física: A planta do nosso escritório com a distribuição de todos os aparelhos conectados (Nuvem, Modem, Roteador Wi-Fi, PCs, Impressora, Notebook e Smartphone).</i></p>
</div>

---

## ⚙️ Como a Rede Foi Configurada
Para colocar essa infraestrutura para funcionar, executei os seguintes passos práticos:

* **Cabeamento Físico:** Conectei a nuvem do provedor ao Modem (cabo coaxial) e liguei os computadores e a impressora diretamente nas portas do roteador (cabo par trançado direto).
* **Criação da Rede Wi-Fi:** Acessei a interface do roteador, nomeei a rede como <code>Escritorio_Firma</code> e apliquei a segurança WPA2-Personal com senha.
* **Adaptação de Hardware:** No simulador, desliguei o Notebook virtual fisicamente, removi sua placa de rede cabeada e instalei um módulo Wi-Fi para captação de sinal.
* **IP Automático (DHCP):** Configurei computadores, impressora e celular para solicitarem e receberem seus endereços IP automaticamente do roteador.

---

## 💡 Meus Desafios e Aprendizados Reais
Durante a montagem, esbarrei em obstáculos que me ensinaram muito sobre resolução de problemas (troubleshooting) e o comportamento dos equipamentos:

* **O "Sumo" da Configuração WPA2:** Após configurar a segurança da rede sem fio com a senha, o roteador não transmitia o sinal. Aprendi na marra que, na interface gráfica, é obrigatório rolar a tela até o final e clicar em "Save Settings" a cada alteração de aba, senão a configuração é descartada!
* **A Troca da Placa do Notebook:** Eu sabia que precisava trocar a conexão para uma antena Wi-Fi, mas tive que relembrar uma regra básica de hardware (físico e simulado): precisamos obrigatoriamente "desligar" a máquina no botão de energia antes de trocar qualquer componente.
* **A "Pegadinha" do Tempo:** Após configurar o Wi-Fi, o celular parecia não conectar de jeito nenhum. A configuração estava exata; o segredo foi clicar no botão de avançar o tempo (<i>Fast Forward Time</i>) para o simulador processar a comunicação e as ondas do Wi-Fi serem estabelecidas.

---

## ✅ Testes e Validação Final
Para comprovar que a rede está se comunicando corretamente em todos os seus nós, realizei validações direto do Smartphone via Wi-Fi:

<details>
  <summary><b>📱 Teste 1: Validação de IP Automático (DHCP) (Clique para expandir)</b></summary>
  <br>
  <div align="center">
    <img width="947" height="997" alt="dhcp-smartphone" src="https://github.com/user-attachments/assets/bb192a06-3603-4833-8e15-4e5ed9600157" />
    <p><i>O Smartphone solicitou um IP e o roteador entregou perfeitamente o endereço <code>192.168.0.101</code> de forma automática, sem necessidade de configuração manual.</i></p>
  </div>
</details>

<details>
  <summary><b>🔍 Teste 2: Conectividade com o Gateway (Ping) (Clique para expandir)</b></summary>
  <br>
  <div align="center">
    <img width="945" height="986" alt="ping-Smartfone" src="https://github.com/user-attachments/assets/72089515-d0cf-4cf0-a851-e57b3811b6b2" />
    <p><i>Usando o terminal do Smartphone, o comando <code>ping</code> confirmou a comunicação direta e sem perdas com o roteador principal da rede (Gateway <code>192.168.0.1</code>).</i></p>
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
