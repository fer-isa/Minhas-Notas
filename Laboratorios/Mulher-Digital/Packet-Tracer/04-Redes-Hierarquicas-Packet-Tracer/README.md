<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Redes%20Hier%C3%A1rquicas&fontSize=60&fontColor=FFFFFF&fontAlignY=35&desc=Modelo%20de%203%20Camadas%20%7C%20Laborat%C3%B3rio%20Cisco&descAlignY=55&descSize=20&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Cisco_Packet_Tracer-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Networking_CCST-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Topologia_Hierárquica-161B22?style=for-the-badge&logo=sitemap&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo do Laboratório
O objetivo deste projeto foi sair das redes pequenas e estruturar a base de uma rede corporativa de grande porte, utilizando o modelo clássico de **Três Camadas da Cisco**. A prática envolveu segmentar o ambiente fisicamente, respeitar as velocidades das portas e configurar o endereçamento IP estático para o roteamento correto.

> **🛡️ Visão de Segurança (SOC):** 
> Conhecer o modelo de 3 camadas (Acesso, Distribuição e Núcleo) é a base para criar políticas de segurança eficientes (ACLs). Se um atacante compromete um PC na camada de **Acesso**, o analista de SOC precisa saber como esse tráfego sobe para a **Distribuição** para tentar bloquear a ameaça antes que ela se espalhe lateralmente para outros departamentos ou atinja o **Núcleo** (Core) da empresa.

---

## 🏗️ A Topologia e os Equipamentos
<div align="center">
  <img width="792" height="647" alt="image" src="https://github.com/user-attachments/assets/00918893-4a6b-452d-8a0f-d82ab08b951b" />
  <p><i>A divisão clássica: Roteador no topo (Núcleo), Switch parrudo no meio (Distribuição) e Switches menores na base (Acesso).</i></p>
</div>

<br>

Em uma rede hierárquica, cada equipamento tem uma função bem definida. A estrutura utilizada foi:

| Camada | Dispositivo / Modelo | Função na Rede |
| :--- | :--- | :--- |
| **Núcleo (Core)** | 1x Roteador Cisco 4331 | É o "chefe". Faz o encaminhamento rápido e é a porta de saída. |
| **Distribuição** | 1x Switch Catalyst 3650 | O "gerente". Junta os cabos que vêm da base e organiza o tráfego. |
| **Acesso** | 2x Switches Catalyst 2960 | A "linha de frente". Onde os PCs dos usuários são conectados. |
| **Dispositivos Finais** | 4x PCs Genéricos | Estações de trabalho divididas (Laboratório e Secretaria). |

<br>

### 📍 Tabela de Endereçamento IP (Estático)

| Aparelho | Interface | Endereço IPv4 | Máscara | Gateway |
| :--- | :--- | :--- | :--- | :--- |
| **PC-Lab01** | FastEthernet0 | `192.168.1.10` | `255.255.255.0` | `192.168.1.1` |
| **PC-Lab02** | FastEthernet0 | `192.168.1.11` | `255.255.255.0` | `192.168.1.1` |
| **PC-Sec01** | FastEthernet0 | `192.168.1.20` | `255.255.255.0` | `192.168.1.1` |
| **PC-Sec02** | FastEthernet0 | `192.168.1.21` | `255.255.255.0` | `192.168.1.1` |
| **Roteador-Core** | GigabitEthernet0/0/0 | `192.168.1.1` | `255.255.255.0` | *-* |

---

## ⚙️ Passo a Passo da Configuração

1. **Organização e Energia:** Posicionei os equipamentos respeitando a hierarquia visual. Um detalhe crítico: no simulador, o Switch 3650 (Distribuição) vem desligado de fábrica; foi necessário inserir fisicamente o módulo da fonte de energia nele para iniciar o boot.
2. **Cabeamento Lógico:** Os PCs foram conectados aos switches de Acesso usando portas `FastEthernet`. A ligação de subida (uplink) entre os switches e o roteador exigiu as portas `GigabitEthernet` para suportar o gargalo de tráfego sem lentidão.
3. **Ligando o Roteador (CLI):** Configuração da interface principal do roteador via terminal para atuar como Gateway da rede:

```text
Router> enable
Router# configure terminal
Router(config)# interface GigabitEthernet0/0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

````


## 💡 Meus Desafios e Aprendizados Reais

<p>Executar este laboratório foi um ótimo teste de atenção aos detalhes de hardware e estruturação:</p>

<ul>
  <li>
    <b>O Mistério da Porta Gigabit 24:</b> Na hora de montar a topologia, selecionei o switch modelo 3550 por engano. Fiquei presa na etapa de cabeamento porque não conseguia achar a porta "Gigabit 24" para fazer a conexão principal. Após investigar, percebi o erro e troquei para o Catalyst 3650 correto. Foi uma lição muito real sobre a importância de validar as especificações do hardware antes de iniciar a montagem.
  </li>
  <li>
    <b>A Lógica e a Ordem do Cabeamento:</b> Tive dúvidas sobre a direção de plugar os cabos (do roteador para o switch ou vice-versa). Fui orientada que a ordem de conexão importa! Seguir a hierarquia topológica na hora de ligar os cabos ajuda a organizar visualmente as portas e evita bugs no sistema de avaliação do Packet Tracer.
  </li>
</ul>

---

## 🎥 Teste Prático (Validação de Tráfego)

<p>Para comprovar a eficácia da configuração física e lógica, registrei a simulação da comunicação de ponta a ponta na rede:</p>

https://github.com/user-attachments/assets/954627db-564b-43d2-9a32-46759071eee7

<div align="center">
  <p><i>Fluxo de pacotes ICMP percorrendo corretamente os switches de Acesso, subindo para a Distribuição e sendo roteados pelo Core.</i></p>
</div>

<br>

<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Minhas_Notas-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2A4365,50:1A365D,100:0B1D3A&height=100&section=footer" width="100%" />
