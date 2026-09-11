<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Redes:%20Conceitos%20B%C3%A1sicos&fontSize=50&fontColor=FFFFFF&fontAlignY=35&desc=M%C3%B3dulos%201%20ao%205%20%7C%20Forma%C3%A7%C3%A3o%20Mulher%20Digital&descAlignY=55&descSize=20&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Cisco_Academy-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/OSI_e_TCP/IP-161B22?style=for-the-badge&logo=sitemap&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Trilha_Mulher_Digital-161B22?style=for-the-badge&logo=gitbook&logoColor=58A6FF" />

</div>

<br>

## 📌 Visão Geral
Um guia rápido e sem complicação sobre como os computadores conversam entre si, passando pelos tipos de rede, os equipamentos que usamos e as regras "invisíveis" que fazem a internet funcionar.

---

## 📝 A "Rede de Papel" (Entendendo a Lógica)

### 1. Tamanho das Redes (Do quarto para o mundo)
* 🏠 **LAN (Rede Local):** É a rede da nossa casa ou da nossa sala de aula. Fica tudo num espaço físico pequeno.
* 🏢 **SOHO:** Uma rede um pouco mais arrumadinha para pequenos negócios e home office.
* 🌍 **WAN (Rede Ampla):** É a rede que conecta cidades e países. A própria Internet é uma WAN gigante!

### 2. Quem é quem na festa?
* **Dispositivos Finais (Os Convidados):** É quem manda ou recebe a informação. Nossos PCs, notebooks e celulares.
* **Dispositivos Intermediários (Os Garçons):** São os Switches e Roteadores. Eles não criam a mensagem, o trabalho deles é só garantir que ela chegue no destino certo pelo melhor caminho.

---

## ⚙️ A Prática (O que importa)

### 🔌 Os Caminhos Físicos (Meios de Transmissão)

| Tipo | Como funciona na prática? |
| :--- | :--- |
| **Wi-Fi (Sem fio)** | Usa ondas de rádio no ar. Dá mobilidade, mas pode sofrer interferência de paredes e outros eletrônicos. |
| **Cabo de Cobre (UTP)** | O famoso cabo azul de rede. Usa energia (pulsos elétricos) para mandar os dados do seu PC até o Switch. |
| **Fibra Óptica** | Usa feixes de luz! É absurdamente rápida, não pega interferência de energia e alcança quilômetros de distância. |

<br>

### 📚 Modelos OSI e TCP/IP (A Língua das Redes)

| Camada Principal | O que faz? |
| :--- | :--- |
| **Aplicação (A Tela)** | Onde tudo começa. É o nosso navegador pedindo para abrir um site (usando HTTP ou HTTPS). |
| **Transporte (A Entrega)** | O controle de qualidade. Verifica se o pacote vai ser entregue inteiro (TCP) ou o mais rápido possível (UDP). |
| **Rede (O Correio)** | É aqui que moram os endereços IP. O roteador olha para esse IP e decide a melhor rota. |
| **Física (O Cabo)** | A parte palpável. Os bits (0 e 1) virando luz na fibra óptica ou eletricidade no cabo de cobre. |

---

## 💡 Minha Visão (Resumo SOC)

> O maior "clique" que eu tive estudando os modelos (OSI e TCP/IP) foi perceber que a internet não tem nada de mágica: é tudo uma questão de **"envelopamento"**! 
> 
> Quando eu digito um endereço, meu pedido vai ganhando várias camadas de proteção, como envelopes um dentro do outro, até virar luz ou pulso elétrico. Aprender a dividir a rede em camadas mentais é o **segredo de ouro para fazer um bom troubleshooting**. Se a internet caiu, eu não tento adivinhar do zero: eu olho se o cabo está ligado (Física), se o PC pegou IP (Rede) ou se o DNS falhou (Aplicação).

<br>

<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas/tree/main/Mulher-Digital/Ciberseguranca">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Índice_de_Cibersegurança-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2A4365,50:1A365D,100:0B1D3A&height=100&section=footer" width="100%" />
