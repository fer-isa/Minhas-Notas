<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Dispositivos%20e%20Arquitetura&fontSize=50&fontColor=FFFFFF&fontAlignY=35&desc=M%C3%B3dulos%201%20ao%203%20%7C%20Forma%C3%A7%C3%A3o%20Mulher%20Digital&descAlignY=55&descSize=20&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Cisco_Academy-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Arquitetura_e_Nuvem-161B22?style=for-the-badge&logo=sitemap&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Trilha_Mulher_Digital-161B22?style=for-the-badge&logo=gitbook&logoColor=58A6FF" />

</div>

<br>

## 📌 Visão Geral
Um resumo prático de como montar uma rede que não cai, como organizar os equipamentos (o famoso modelo de 3 camadas da Cisco), como funciona a Computação em Nuvem e como traduzir os endereços IP para a linguagem das máquinas (os zeros e uns).

---

## 📝 A "Rede de Papel" (Entendendo a Lógica)

### 1. Os 4 Pilares de uma Boa Rede
* 🛡️ **Tolerância a Falhas:** Se um cabo partir, a rede acha outro caminho sozinha. Ela não pode parar!
* 📈 **Escalabilidade:** A rede precisa conseguir crescer (colocar mais computadores e filiais) sem precisarmos jogar os aparelhos antigos fora e recomeçar do zero.
* 🚦 **Qualidade de Serviço (QoS):** Dar passagem "VIP" para o que importa. Por exemplo, a rede não deixa uma chamada de vídeo travar só porque alguém na outra sala está baixando um arquivo pesado.
* 🔒 **Segurança:** Proteger os dados e garantir que só quem tem crachá consiga entrar.

### 2. O Prédio da Cisco (Modelo de 3 Camadas)
* 🏢 **Camada de Acesso (O Nosso Andar):** Onde ligamos o cabo no nosso PC, na impressora ou no Wi-Fi. É a linha de frente de contato com o usuário.
* 🔌 **Camada de Distribuição (O Quadro de Força):** O "gerente". Ele junta os cabos que vêm de todos os andares de Acesso e aplica as regras de segurança e roteamento.
* 🚀 **Camada de Núcleo / Core (A Via Expressa):** O "chefão". Liga prédios e servidores inteiros. Ele não perde tempo checando regrinhas; a única função dele é transportar um volume gigante de dados de um lado para o outro o mais rápido possível.

---

## ⚙️ A Prática (O que importa)

### ☁️ A Nuvem (O Computador dos Outros)

| Serviço (A Sigla) | O que é na prática? |
| :--- | :--- |
| **SaaS (Software)** | Tudo pronto. Você só abre o navegador e usa sem instalar nada (Ex: Canva, Google Workspace). |
| **PaaS (Plataforma)** | O ambiente montadinho para quem é programador só chegar e colocar o aplicativo no ar. |
| **IaaS (Infraestrutura)** | Você aluga a "máquina virtual" crua e configura exatamente do seu jeito (Ex: AWS, Azure). |

<br>

### 💻 Máquinas Virtuais (Hipervisores)
* **Tipo 1 (Bare-Metal):** Vai direto no hardware "seco" do servidor da empresa, sem Windows por baixo. É super rápido e profissional.
* **Tipo 2 (Hosted):** Aquele que a gente instala como se fosse um joguinho no nosso PC para estudar (Ex: VirtualBox).

<br>

### 🔢 Matemática Binária: Como o PC lê o IP (Ex: 192.168.10.5)
Usamos a "Tabelinha Mágica" `(128, 64, 32, 16, 8, 4, 2, 1)`. Se o número da tabela servir para somar e chegar no valor do pedaço do IP, colocamos **1** (Ligado). Se ele for muito grande e não servir, colocamos **0** (Desligado).

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 | Matemática (Resultado) |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :--- |
| **1** | **1** | 0 | 0 | 0 | 0 | 0 | 0 | `192` (128 + 64) |
| **1** | 0 | **1** | 0 | **1** | 0 | 0 | 0 | `168` (128 + 32 + 8) |
| 0 | 0 | 0 | 0 | **1** | 0 | **1** | 0 | `10` (8 + 2) |
| 0 | 0 | 0 | 0 | 0 | **1** | 0 | **1** | `5` (4 + 1) |

---

## 💡 Minha Visão (Resumo SOC)

> O que mais me ajudou a fixar esse módulo foi desenhar as três camadas da Cisco na minha cabeça. Fica muito mais fácil entender a rede quando a gente pensa num prédio comercial: a Camada de Acesso é a mesa do nosso andar, a Distribuição é o quadro de força do prédio que junta todos os andares, e o Core é a avenida expressa lá fora ligando um prédio no outro. 
> 
> Outro "clique" maravilhoso foi aprender a converter IPs para binário. Tinha muito texto nos cursos e no começo assusta, mas quando a gente monta a tabelinha do 128 ao 1 e vai só encaixando os números na soma (ligando ou desligando a "luz"), fica super divertido! É muito legal saber que a gente consegue traduzir a linguagem da máquina de forma visual e lógica, tirando de vez o medo de mexer com zeros e uns!

<br>

<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas/tree/main/Mulher-Digital/Ciberseguranca">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Índice_de_Cibersegurança-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2A4365,50:1A365D,100:0B1D3A&height=100&section=footer" width="100%" />
