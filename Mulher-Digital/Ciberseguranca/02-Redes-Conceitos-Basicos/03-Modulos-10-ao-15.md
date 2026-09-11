<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Redes:%20Conceitos%20B%C3%A1sicos&fontSize=50&fontColor=FFFFFF&fontAlignY=35&desc=M%C3%B3dulos%2010%20ao%2015%20%7C%20Forma%C3%A7%C3%A3o%20Mulher%20Digital&descAlignY=55&descSize=20&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Cisco_Academy-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Roteamento_e_Protocolos-161B22?style=for-the-badge&logo=sitemap&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Trilha_Mulher_Digital-161B22?style=for-the-badge&logo=gitbook&logoColor=58A6FF" />

</div>

<br>

## 📌 Visão Geral
O fechamento da nossa base de redes! Aqui desmistificamos como os IPs e as máscaras funcionam, os 3 protocolos mágicos que fazem a rede ter vida (DHCP, DNS e ARP), como os roteadores escolhem caminhos e os comandos essenciais para testar se tudo está funcionando na prática.

---

## 📝 A "Rede de Papel" (Entendendo a Lógica)

### 1. Endereço IP e a Máscara (Rua e Casa)
Todo IP é dividido em duas partes. A **Máscara de Sub-rede** é o "muro" que separa essas duas coisas: ela diz aos equipamentos até onde vai o nome da rua (A Rede) e onde começa o número da casa (O Host).

### 2. IPs Públicos vs. Privados
* 🌍 **IP Público:** É o endereço oficial da sua casa na internet. Só existe um no mundo inteiro e é roteável em qualquer lugar.
* 🏠 **IP Privado:** É o apelido que você dá para os cômodos de casa (Quarto 1, Quarto 2). A internet lá fora não faz ideia de quem são eles; só o seu roteador local os conhece.

### 3. O Jeito de Falar (Modos de Transmissão)
* 📞 **Unicast:** Uma ligação telefônica privada. Um fala direto com o outro (1 para 1).
* 📢 **Broadcast:** Pegar um megafone e gritar no meio da sala. Todos os computadores da rede local escutam (1 para Todos).
* 💬 **Multicast:** Mandar mensagem num grupo do WhatsApp. Só recebe quem faz parte daquele grupo específico (1 para Alguns).

---

## ⚙️ A Prática (O que importa)

### Os 3 Protocolos Salva-Vidas

| Protocolo | O que faz na prática? |
| :--- | :--- |
| **DHCP** | O recepcionista automático. Quando você conecta o cabo, ele te empresta um IP, uma máscara e um gateway para você poder navegar sem configurar nada à mão. |
| **DNS** | A agenda telefônica da internet. Transforma nomes fáceis (*google.com*) nos números IP que as máquinas precisam para se achar. |
| **ARP** | O detetive da rede local. Ele grita (Broadcast): *"Quem é o dono do IP 192.168.1.10? Me dê o seu endereço físico (MAC)!"* |

<br>

### Como o Roteador escolhe o caminho (Rotas)
* **Rota Estática:** O administrador digita o caminho na mão. É seguro, mas dá muito trabalho se a rede for grande.
* **Rota Dinâmica (OSPF / RIP):** É o "Waze" dos roteadores. Eles conversam entre si e recalculam a rota sozinhos se um cabo quebrar no meio do caminho.

<br>

### Comandos Mágicos (A "Tela Preta")

```bash
# Mostra o seu IP, sua Máscara e o seu endereço MAC físico
ipconfig /all

# Mostra a lista de quem o seu computador já conhece na rede local (IP associado ao MAC)
arp -a

# Testa se a internet está chegando até o destino (ex: tenta bater na porta do Google)
ping 8.8.8.8

# Mostra o caminho exato e todos os roteadores por onde o pacote passou até o destino
tracert 8.8.8.8
