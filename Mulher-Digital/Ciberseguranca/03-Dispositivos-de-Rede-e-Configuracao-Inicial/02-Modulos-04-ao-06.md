<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Comuta%C3%A7%C3%A3o%20e%20Camada%20de%20Rede&fontSize=45&fontColor=FFFFFF&fontAlignY=35&desc=M%C3%B3dulos%204%20ao%206%20%7C%20Forma%C3%A7%C3%A3o%20Mulher%20Digital&descAlignY=55&descSize=20&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Cisco_Academy-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Comutação_e_IP-161B22?style=for-the-badge&logo=sitemap&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Trilha_Mulher_Digital-161B22?style=for-the-badge&logo=gitbook&logoColor=58A6FF" />

</div>

<br>

## 📌 Visão Geral
Neste resumo, vamos entender como os dados viajam fisicamente pelo cabo da rede (Ethernet), como um Switch usa sua memória para aprender caminhos e como o protocolo IP age como o "entregador dos correios" da internet.

---

## 📝 A "Rede de Papel" (Entendendo a Lógica)

### 1. O Envelope (O Quadro Ethernet)
Quando a mensagem sai do seu PC para o cabo de rede, ela vira um "Quadro". Ele tem um tamanho limite (se for muito pequeno, a rede acha que é lixo de colisão; se for muito grande, a rede rejeita). O que tem nesse envelope?
* **Aviso:** "Atenção, lá vai mensagem!" (Sincroniza o relógio das máquinas).
* **Endereços MAC:** Quem está mandando (Origem) e quem vai receber (Destino).
* **O Pacote:** A mensagem em si.
* **O Selo de Garantia (FCS):** Um código matemático no final do envelope. Se chegar rasgado ou com erro físico, a máquina descarta na hora.

### 2. O Chassi (Endereço MAC)
Todo endereço MAC tem 48 bits e é dividido bem no meio (metade/metade):
* **A Marca (OUI):** A primeira metade diz quem fabricou a placa de rede (ex: Cisco, Intel, Dell).
* **O Número de Série:** A segunda metade é o número de identificação único daquela placa no mundo.

### 3. Como o Switch "Pensa" (A Tabela MAC)
O switch é super inteligente, mas quando ele liga na tomada, ele não conhece ninguém. Ele aprende sozinho em 3 passos:
* **Anota o Remetente (Aprendizado):** "Opa, o PC 1 mandou mensagem pela Porta 2. Vou anotar o MAC dele na minha caderneta."
* **Entrega Direta (Encaminhamento):** Se ele já conhece o destinatário, ele manda a mensagem *só* para a porta daquela pessoa.
* **O Grito (Inundação):** Se ele não sabe onde o destinatário está, ele manda a mensagem para *todas as portas* (menos a que enviou). Quem for o dono responde, e aí o switch anota na caderneta.

---

## ⚙️ A Prática (O que importa)

### 📨 O Protocolo IP (O Carteiro da Camada 3)
* **Sem Conexão:** Ele não liga antes para avisar que a carta está chegando. Ele simplesmente manda.
* **Melhor Esforço:** O IP faz o possível para entregar, mas *não garante* nada! Se o pacote sumir, ele não manda de novo (quem faz o trabalho de cobrar e retransmitir é o protocolo TCP, na camada de cima).
* **Independente:** O IP não liga se a mensagem vai viajar por Wi-Fi, cabo de cobre ou fibra óptica. O formato dele é sempre o mesmo.

<br>

### 🔄 A Evolução: IPv4 vs. IPv6 (Por baixo dos panos)

| O que mudou? | IPv4 | IPv6 |
| :--- | :--- | :--- |
| **Endereços** | 4 bilhões (já acabou). | Praticamente infinito (trilhões de trilhões). |
| **Cabeçalho (A Capa)** | Varia de tamanho (de 20 a 60 bytes). | Tamanho fixo de 40 bytes (muito mais rápido para o roteador ler). |
| **Fragmentação** | Qualquer roteador no meio do caminho pode quebrar o pacote em pedaços menores. | Só o PC que está enviando a mensagem tem permissão de quebrar o pacote. Deixa a rede mais rápida! |

---

## 💡 Minha Visão (Resumo SOC)

> O que fez a minha cabeça explodir nesse módulo foi entender como o Switch é absurdamente eficiente. Antes eu achava que a rede era uma bagunça onde todo computador recebia a mensagem de todo mundo o tempo todo. Entender que o Switch tem uma memória (Tabela MAC) e que ele fica "escutando" as portas para mapear quem está onde, enviando as mensagens depois apenas para as portas corretas, me fez ver como a tecnologia de redes é elegante. 
> 
> Outra coisa que adorei foi a revelação sobre o protocolo IP: ele faz o "Melhor Esforço", mas não garante a entrega. É muito legal perceber que as funções são divididas e que a internet só funciona bem porque os protocolos trabalham em equipe!

<br>

<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas/tree/main/Mulher-Digital/Ciberseguranca">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Índice_de_Cibersegurança-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2A4365,50:1A365D,100:0B1D3A&height=100&section=footer" width="100%" />
