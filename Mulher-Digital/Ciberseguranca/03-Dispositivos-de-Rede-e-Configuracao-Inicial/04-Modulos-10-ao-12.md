<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Comunica%C3%A7%C3%A3o%20e%20Portas&fontSize=50&fontColor=FFFFFF&fontAlignY=35&desc=M%C3%B3dulos%2010%20ao%2012%20%7C%20Dispositivos%20de%20Rede&descAlignY=55&descSize=20&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Cisco_Academy-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Transporte_e_Portas-161B22?style=for-the-badge&logo=sitemap&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Trilha_Mulher_Digital-161B22?style=for-the-badge&logo=gitbook&logoColor=58A6FF" />

</div>

<br>

## 📌 Visão Geral
Neste módulo, respondemos à pergunta clássica: "Como o computador sabe para qual aplicativo enviar a informação?"[cite: 2]. Exploramos os protocolos da Camada de Transporte, o mapa das portas essenciais para o exame CCST e como monitorar o tráfego usando o Wireshark[cite: 2].

---

## 📝 A "Rede de Papel" (Entendendo a Lógica)

### 1. TCP vs. UDP (Os Entregadores)
Eles moram na Camada de Transporte, mas trabalham de formas opostas[cite: 2]:
* 🤝 **TCP (A Entrega Registrada):** É confiável, garante a ordem dos pacotes e retransmite o que for perdido[cite: 2]. Ele usa o processo de três etapas (*Three-Way Handshake*: SYN ➔ SYN+ACK ➔ ACK) para estabelecer conexão antes de enviar os dados[cite: 2]. **Atenção:** TCP traz confiabilidade, mas não traz criptografia (segurança é com o HTTPS/TLS)[cite: 2]!
* 🚀 **UDP (O Megafone):** Não exige conexão, não confirma recebimento e não retransmite nada[cite: 2]. É muito mais rápido e leve (menor overhead), ideal para chamadas de vídeo, jogos e streaming[cite: 2].

### 2. Portas e Sockets (A Porta da Casa)
* **A Lógica:** O IP encontra o computador na rede; a Porta encontra qual aplicação/serviço deve receber os dados dentro daquele computador[cite: 2]. 
* **O Socket:** É a junção do IP com a Porta (Ex: `192.168.1.10:443`)[cite: 2].
* **Portas Temporárias:** O computador usa portas altas e temporárias (ex: `52134`) para diferenciar várias conexões acontecendo ao mesmo tempo (como múltiplas abas do navegador abertas)[cite: 2].

---

## ⚙️ A Prática (O que importa)

### 📋 Tabela de Portas Essenciais (Foco CCST)
As portas de 0 a 1023 são conhecidas e reservadas para serviços padrão[cite: 2].

| Porta | Protocolo | Transporte | O que faz na prática? |
| :--- | :--- | :--- | :--- |
| **20/21** | FTP | TCP | Transferência de arquivos[cite: 2]. |
| **22** | SSH | TCP | Acesso remoto seguro (criptografado)[cite: 2]. |
| **23** | Telnet | TCP | Acesso remoto SEM segurança[cite: 2]. |
| **25** | SMTP | TCP | Envio de e-mails[cite: 2]. |
| **53** | DNS | UDP/TCP | Traduz nomes (URLs) para endereços IP[cite: 2]. |
| **67/68** | DHCP | UDP | Entrega endereços IP automaticamente aos dispositivos[cite: 2]. |
| **80** | HTTP | TCP | Navegação em sites sem criptografia[cite: 2]. |
| **443** | HTTPS | TCP | Navegação em sites COM criptografia[cite: 2]. |
| **110 / 143** | POP3 / IMAP | TCP | Recebimento e leitura de e-mails[cite: 2]. |
| **161/162** | SNMP | UDP | Monitoramento de equipamentos de rede[cite: 2]. |
| **3389** | RDP | TCP/UDP | Acesso remoto à tela do Windows[cite: 2]. |

<br>

### 🦈 Wireshark (O Microscópio da Rede)
* É uma ferramenta que captura os dados (pacotes) passando pela rede local[cite: 2].
* Permite ver tudo o que entra e sai da máquina[cite: 2].
* Usa **Filtros** para isolar protocolos (TCP, UDP) ou portas específicas, facilitando a investigação[cite: 2].

---

## 💡 Minha Visão (Resumo SOC)

> Memorizar as portas lógicas é vital para o exame CCST, mas o seu verdadeiro poder brilha dentro do SOC! 
> 
> Se eu abro o **Wireshark** e filtro o tráfego identificando uma comunicação saindo pela **Porta 23 (Telnet)**[cite: 2], eu imediatamente ligo um alerta vermelho: alguém está acessando equipamentos remotamente sem criptografia[cite: 2], e qualquer atacante interceptando a rede poderia ler as senhas em texto puro. Entender a diferença entre a entrega garantida do TCP e a velocidade sem checagem do UDP[cite: 2] também me ajuda a perfilar ataques, como os de negação de serviço (DDoS).

<br>

<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas/tree/main/Mulher-Digital/Ciberseguranca">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Índice_de_Cibersegurança-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2A4365,50:1A365D,100:0B1D3A&height=100&section=footer" width="100%" />
