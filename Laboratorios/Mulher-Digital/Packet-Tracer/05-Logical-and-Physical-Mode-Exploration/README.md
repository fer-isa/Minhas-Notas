<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Packet%20Tracer:%20Modo%20F%C3%ADsico%20e%20L%C3%B3gico&fontSize=50&fontColor=FFFFFF&fontAlignY=35&desc=Laborat%C3%B3rio%20Pr%C3%A1tico%20%7C%20Ciberseguran%C3%A7a%20Mulher%20Digital%20Turma%2003&descAlignY=55&descSize=20&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Cisco_Packet_Tracer-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Infraestrutura_de_Redes-161B22?style=for-the-badge&logo=server&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Evolução_Técnica-161B22?style=for-the-badge&logo=trendmicro&logoColor=58A6FF" />

</div>

<br>

## 📌 Visão Geral da Atividade
Esta documentação registra a exploração prática dos ambientes de simulação, focando na transição entre a topologia e as conexões do Modo Físico e Lógico. O objetivo foi vivenciar o dia a dia de infraestrutura: desde a visão global da rede até a instalação real de cabos e equipamentos em um rack.

---

## ⚙️ Detalhamento do Laboratório (Passo a Passo)

O laboratório "Logical and Physical Mode Exploration" é dividido em etapas práticas que simulam a rotina de um profissional de infraestrutura operando fisicamente os dispositivos:

### 1. Navegação Lógica vs. Física
* **Modo Lógico:** Análise da topologia da rede no painel principal, observando como os roteadores, switches e PCs estão interligados teoricamente.
* **Modo Físico:** Transição para a visão geográfica. A navegação passa pela visão da cidade (Intercity), entra no prédio da Filial (Branch Office) e acessa a sala do Armário de Telecomunicações (Wiring Closet).

### 2. Exploração do Wiring Closet (Armário de Telecom)
* Inspeção visual do rack de equipamentos, da mesa de trabalho (onde ficam os PCs) e da prateleira de estoque (Inventory).
* Análise dos LEDs de status dos Switches e Roteadores em tempo real para verificar a conectividade e o fornecimento de energia.

### 3. Cabeamento de Dispositivos (O Desafio Prático)
* **Conexão Física:** O laboratório exige a seleção da mídia correta para conectar os equipamentos através da paleta de conexões (Pegboard).
* **Patch Panels e Switches:** Conectar cabos diretos de cobre (Copper Straight-Through) nas portas corretas (como FastEthernet ou GigabitEthernet).
* *Nota de Simulação:* O Packet Tracer valida fisicamente se o cabo selecionado é compatível com a interface escolhida.

### 4. Instalação de um Roteador de Backup
* **Mão na Massa:** Retirar um roteador reserva da prateleira de inventário e arrastá-lo para instalá-lo fisicamente em um espaço vazio do Rack.
* **Energização:** Ligar os cabos de energia e acionar o botão físico de "Power" do equipamento.

### 5. Configuração Básica via Console
* Conectar um **Cabo Console** da porta RS-232 do PC de gerenciamento na mesa até a porta Console do Roteador recém-instalado no rack.
* Abrir o aplicativo de Terminal no PC para acessar a linha de comando (CLI) do roteador e aplicar as primeiras configurações (como alterar o *Hostname*).

<br>

---

## 💡 Minha Visão (Evolução Pessoal e Técnica)

> Quando fiz essa atividade pela primeira vez, lá no comecinho do curso de introdução ao Packet Tracer, eu tive muita dificuldade. Fiquei um bom tempo tentando escolher o cabo correto e errando as conexões nas portas. Tive que insistir até o próprio simulador me dar uma ajudinha para eu conseguir destravar e seguir adiante.
>
> Mas o mais incrível foi quando esse mesmo laboratório apareceu novamente, agora no módulo de Segurança de Endpoint. Dessa segunda vez, eu já sabia exatamente o que fazer, qual cabo pegar e onde conectar!
>
> Perceber essa diferença foi uma injeção de confiança gigante. Refazer os testes com facilidade me provou o quanto eu aprendi e evoluí desde o início do programa. Compreender a infraestrutura física e como as conexões reais funcionam me dá uma base muito mais sólida para estruturar minha carreira, sabendo valorizar os processos de base e enxergando a Cibersegurança a partir de uma ótica realista de suporte à infraestrutura.

<br>

<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas/tree/main/Mulher-Digital/Ciberseguranca">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Índice_de_Cibersegurança-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2A4365,50:1A365D,100:0B1D3A&height=100&section=footer" width="100%" />
