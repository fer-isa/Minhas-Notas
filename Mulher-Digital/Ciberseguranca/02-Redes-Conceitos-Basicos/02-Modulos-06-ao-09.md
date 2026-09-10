<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Redes:%20Conceitos%20B%C3%A1sicos&fontSize=50&fontColor=FFFFFF&fontAlignY=35&desc=M%C3%B3dulos%206%20ao%209%20%7C%20Forma%C3%A7%C3%A3o%20Mulher%20Digital&descAlignY=55&descSize=20&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Cisco_Academy-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Endereçamento_e_Topologia-161B22?style=for-the-badge&logo=sitemap&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Trilha_Mulher_Digital-161B22?style=for-the-badge&logo=gitbook&logoColor=58A6FF" />

</div>

<br>

## 📌 Visão Geral
Neste resumo, trago a lógica de como os dados são empacotados para viajar, como os computadores ganham "nomes e CPFs" (IP, MAC e DNS) e como as empresas desenham e protegem suas redes na vida real.

---

## 📝 A "Rede de Papel" (Entendendo a Lógica)

### 1. Encapsulamento (A Boneca Russa)
Quando você manda uma mensagem, ela não vai crua pra rede. Ela passa por um processo de empacotamento: o dado ganha um envelope (com os IPs de origem e destino) e depois é colocado dentro de uma "caixa" maior (o Quadro Ethernet, que recebe os endereços MAC) para conseguir viajar pelo cabo até o roteador.

### 2. Identidade na Rede: MAC, IP e DNS
* 🏷️ **Endereço MAC (O Chassi):** É o endereço físico da placa de rede. Ele vem gravado de fábrica e *nunca muda*. Serve para a comunicação local (dentro da mesma sala).
* 🏠 **Endereço IP (O CEP da casa):** É o endereço lógico. Ele *muda* dependendo de onde você está conectado (seu PC tem um IP na sua casa e outro diferente no Wi-Fi do shopping). Serve para achar você na internet.
* 📖 **DNS (A Agenda de Contatos):** Máquinas só entendem números (IPs). Nós preferimos nomes. O DNS é a agenda que traduz `www.google.com` para o IP correto dele.

### 3. O Tamanho da Festa (Intranet, Extranet e Internet)
* **Intranet:** A festa privada da empresa. Só funcionários com crachá (autenticados) podem entrar.
* **Extranet:** A área VIP. A empresa abre uma "porta lateral" segura para parceiros e fornecedores acessarem alguns sistemas.
* **Internet:** A praça pública, onde todo mundo se conecta.

---

## ⚙️ A Prática (O que importa)

### O famoso NAT (A mágica do Roteador)
A internet ficou sem endereços IPv4, então inventaram o NAT. Ele age como o **porteiro de um prédio**: o mundo lá fora só vê o IP do porteiro (o IP público). Quando a correspondência chega, o porteiro traduz o endereço e entrega no apartamento certo (os IPs privados dos nossos celulares e PCs).

### IPv4 vs. IPv6

| Protocolo | Como é? | Qual é a diferença? |
| :--- | :--- | :--- |
| **IPv4** | `192.168.1.10` | O modelo antigo. Tem "só" 4 bilhões de endereços e já esgotou. Usa números e pontos. |
| **IPv6** | `2001:0db8::8a2e:0370` | O modelo novo e infinito. Usa números, letras e dois-pontos. Já vem com segurança nativa. |

<br>

### Desenhos de Rede (Topologias)

| Topologia | Como funciona na prática? |
| :--- | :--- |
| **Estrela 🌟** | Todo mundo ligado num Switch central. Se um cabo quebra, só aquele PC fica sem internet. (É a mais usada!) |
| **Barramento 🚌** | Um cabo central onde todo mundo se pendura. Se o cabo principal partir, a rede inteira cai. |
| **Malha 🕸️** | Todo mundo tem um cabo ligado direto a todo mundo. Se um cabo quebrar, tem vários outros caminhos. Super seguro, mas caríssimo. |

<br>

### Hardening (Deixando a rede casca grossa)
* **Menor Privilégio:** Dar ao funcionário APENAS o acesso que ele precisa para trabalhar. Nada de dar senha de administrador pra todo mundo.
* **Gestão de Patches:** O famoso "manter tudo atualizado" para fechar brechas conhecidas pelos hackers.
* **Criptografia em Trânsito:** Embaralhar a mensagem para que ninguém consiga ler o que está passando no cabo (usar HTTPS, SSH, VPN).

---

## 💡 Minha Visão (Resumo SOC)

> O que fez a minha cabeça explodir nesse módulo foi finalmente entender como a internet não parou, mesmo com os endereços IPv4 acabando há anos. O conceito do NAT é genial! Pensar no roteador da minha casa como um porteiro que recebe as respostas da internet (com um IP público só) e distribui perfeitamente para os meus dispositivos (usando IPs privados que a internet nem faz ideia que existem) fez tudo se encaixar. 
> 
> E sobre as topologias, ficou claro por que a rede em "Estrela" dominou o mercado corporativo: para a segurança e a disponibilidade do negócio, ninguém quer que a empresa inteira pare de trabalhar só porque um único cabo quebrou.

<br>

<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas/tree/main/Mulher-Digital/Ciberseguranca">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Índice_de_Cibersegurança-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2A4365,50:1A365D,100:0B1D3A&height=100&section=footer" width="100%" />
