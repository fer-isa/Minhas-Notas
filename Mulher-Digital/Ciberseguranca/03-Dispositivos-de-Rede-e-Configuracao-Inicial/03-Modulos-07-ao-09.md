<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Camadas%20de%20Rede%20e%20Endere%C3%A7amento&fontSize=42&fontColor=FFFFFF&fontAlignY=35&desc=M%C3%B3dulos%207%20ao%209%20%7C%20Dispositivos%20de%20Rede&descAlignY=55&descSize=20&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Cisco_Academy-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Modelo_OSI-161B22?style=for-the-badge&logo=sitemap&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Trilha_Mulher_Digital-161B22?style=for-the-badge&logo=gitbook&logoColor=58A6FF" />

</div>

<br>

## 📌 Visão Geral
Neste módulo, mergulhamos fundo no Modelo OSI para entender como a informação é "empacotada" para viajar pela rede. Além disso, exploramos a matemática por trás dos endereços IPv4, sua evolução para o IPv6 e consolidamos o papel de serviços essenciais como DHCP e DNS.

---

## 📝 A "Rede de Papel" (Entendendo a Lógica)

### 1. Modelo OSI e Encapsulamento (Caixas dentro de Caixas)
Quando enviamos uma informação, ela passa por 7 camadas, do nosso aplicativo até virar um sinal físico no cabo.
* **Encapsulamento (Envio):** A informação vai descendo e ganhando "envelopes" (cabeçalhos) novos a cada camada. O dado vira Segmento (Transporte), depois Pacote (Rede), depois Quadro (Enlace) até virar Bits (Física).
* **Desencapsulamento (Recebimento):** O caminho inverso. O computador que recebe vai abrindo os envelopes até entregar a informação pura para o usuário na camada de Aplicação.

### 2. A Matemática do IPv4 (Classes e Hosts)
Todo IP precisa de uma máscara para separar o que é "Rede" e o que é "Host" (Máquina). Quanto mais espaço damos para a rede, menos computadores cabem nela.
* **A Regra de Ouro:** Para calcular quantos computadores cabem numa rede, usamos a fórmula matemática da potência de 2 e **sempre subtraímos 2** no final.
* **Por que subtrair 2?** Porque o primeiro endereço identifica a própria Rede, e o último é o Broadcast (usado para gritar para todo mundo).

---

## ⚙️ A Prática (O que importa)

### 🔒 IPv4 vs. IPv6 (O Fator Segurança)
Além do número absurdo de novos endereços (128 bits contra os velhos 32 bits do IPv4), a maior mudança está na segurança:
* **No IPv4:** O recurso de segurança IPsec é opcional e precisa ser configurado manualmente como um "acessório".
* **No IPv6:** A criptografia e a autenticação já nasceram nativas e integradas ao protocolo. A segurança é de fábrica!

<br>

### 🛠️ Os Serviços Fundamentais da Rede

| Serviço | A Analogia Prática | O que faz tecnicamente? |
| :--- | :--- | :--- |
| **DHCP** | O recepcionista do hotel. | Entrega IP, máscara e gateway automaticamente. Funciona baseado no processo DORA. |
| **DNS** | A agenda do celular. | Converte URLs em IPs legíveis pelas máquinas. Trabalha usando a porta 53. |
| **NAT** | O atendente dos correios. | Converte múltiplos IPs privados da rede local em apenas um IP público para sair para a internet. |
| **Gateway** | A porta de saída do prédio. | É o IP do roteador que encaminha pacotes para redes externas e diferentes da nossa. |

---

## 💡 Minha Visão (Resumo SOC)

> O maior aprendizado deste módulo foi entender o **Modelo OSI** como uma verdadeira ferramenta de investigação, e não apenas como teoria para provas. Em um SOC, se eu estiver analisando um tráfego criptografado malicioso e entender que o IPsec protegeu os dados, preciso saber em qual camada buscar indicadores de comprometimento. 
> 
> Além disso, a tabela de analogias dos serviços (DHCP, DNS, NAT) clareia perfeitamente a visão investigativa: se o DNS falha, a máquina não sabe para quem ligar; se o DHCP falha, a máquina nem sequer ganha um crachá de identificação na nossa rede corporativa!

<br>

<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas/tree/main/Mulher-Digital/Ciberseguranca">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Índice_de_Cibersegurança-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2A4365,50:1A365D,100:0B1D3A&height=100&section=footer" width="100%" />
