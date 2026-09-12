<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=ARP%20no%20Wireshark&fontSize=50&fontColor=FFFFFF&fontAlignY=35&desc=Laborat%C3%B3rio%20de%20Redes%20%7C%20An%C3%A1lise%20de%20Tr%C3%A1fego&descAlignY=55&descSize=20&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Wireshark-161B22?style=for-the-badge&logo=wireshark&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/ARP-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Network_Analysis-161B22?style=for-the-badge&logo=wireshark&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo

Neste laboratório, explorei o Wireshark para observar o tráfego da minha própria rede Wi-Fi.

O foco foi utilizar o filtro `arp` para visualizar mensagens do protocolo ARP e entender melhor a relação entre endereços IP e MAC.

> **🛡️ Visão de Segurança (SOC):**  
> Comecei a entender como filtros podem ajudar a encontrar informações específicas em meio a uma grande quantidade de tráfego.

---

## 🔍 Analisando o Tráfego ARP

Após iniciar a captura no Wireshark, uma grande quantidade de pacotes começou a aparecer.

Para visualizar apenas o tráfego relacionado ao protocolo que estava estudando, utilizei o filtro:

<pre><code>
arp
</code></pre>


<!-- 🖼️🖼️🖼️ FOTO 1 - COLE AQUI 🖼️🖼️🖼️ -->
<!-- FOTO: Wireshark com filtro ARP -->
<!-- É A PRIMEIRA FOTO QUE VOCÊ ME MANDOU -->

<div align="center">

<img width="1245" height="1022" alt="Captura de tela 2026-09-11 015734" src="https://github.com/user-attachments/assets/f6c77dde-ac3a-4f5b-bab6-4ff699f5b5ca" />



<p><i>Captura realizada na interface Wi-Fi com o filtro ARP aplicado.</i></p>

</div>

<!-- 🖼️🖼️🖼️ FIM DA FOTO 1 🖼️🖼️🖼️ -->


Na captura, pude observar mensagens como:

<pre><code>
Who has 192.168.15.11? Tell 192.168.15.1
</code></pre>

---

## 💡 O Que Aprendi na Prática

* **ARP:** Comecei a entender que o protocolo ajuda a relacionar um endereço IP com um endereço físico (MAC) dentro da rede local.

* **Broadcast:** Observei solicitações ARP sendo enviadas para Broadcast enquanto um dispositivo procurava descobrir o endereço MAC relacionado a um IP.

* **Filtros:** Utilizar `arp` me ajudou a reduzir a quantidade de informações exibidas e focar apenas no tráfego que estava estudando.

* **Wireshark:** Por ser uma interface nova para mim, precisei explorar a ferramenta e entender melhor como selecionar a interface de rede e iniciar uma captura.

---

## ⚙️ Comandos e Ferramentas Utilizados

<details>

<summary><b>🦈 1. Capturando o Tráfego no Wireshark</b></summary>

<br>

Meu computador já estava conectado automaticamente ao Wi-Fi, então inicialmente tive dificuldade para entender como utilizar essa conexão dentro do Wireshark.

Durante a prática, comecei a entender que preciso selecionar a interface de rede para observar o tráfego que está passando por ela.

Também utilizei o botão da barbatana de tubarão para iniciar a captura de pacotes.

</details>

---

<details>

<summary><b>🔍 2. Analisando os Pacotes ARP</b></summary>

<br>

Ao selecionar um pacote, comecei a explorar informações como:

* Frame
* Ethernet
* Address Resolution Protocol


<!-- 🖼️🖼️🖼️ FOTO 2 - COLE AQUI 🖼️🖼️🖼️ -->
<!-- FOTO: Segunda imagem do Wireshark -->
<!-- É A SEGUNDA FOTO QUE VOCÊ ME MANDOU -->

<div align="center">

<img width="1307" height="995" alt="Captura de tela 2026-09-11 015748" src="https://github.com/user-attachments/assets/d0971aeb-fa6b-4dca-a406-ac36b18b8d36" width="900px"/>


<p><i>Detalhes observados durante a captura no Wireshark.</i></p>

</div>

<!-- 🖼️🖼️🖼️ FIM DA FOTO 2 🖼️🖼️🖼️ -->


</details>

---

<details>

<summary><b>💻 3. Verificando a Tabela ARP</b></summary>

<br>

Também utilizei o Prompt de Comando para visualizar a tabela ARP com o comando:

<pre><code>
arp -a
</code></pre>


<!-- 🖼️🖼️🖼️ FOTO 3 - COLE AQUI 🖼️🖼️🖼️ -->
<!-- FOTO: Prompt de Comando com arp -a -->
<!-- É A TERCEIRA FOTO QUE VOCÊ ME MANDOU -->

<div align="center">

<img src="<img width="1467" height="752" alt="image" src="https://github.com/user-attachments/assets/ea3d1e28-a7c6-4482-b84c-1fd1efe9e9e3" width="900px" />


<p><i>Resultado do comando <code>arp -a</code>, mostrando endereços IP, endereços físicos (MAC) e o tipo de entrada.</i></p>

</div>

<!-- 🖼️🖼️🖼️ FIM DA FOTO 3 🖼️🖼️🖼️ -->


</details>

---

## 🚨 Dificuldades Durante o Laboratório

Durante a prática, minha principal dificuldade foi utilizar uma ferramenta completamente nova.

Como meu Wi-Fi já conecta automaticamente, inicialmente fiquei confusa sobre como o Wireshark utilizaria essa conexão. Também precisei me familiarizar com a interface e entender melhor a função dos botões.

Outra dificuldade foi a quantidade de informações exibidas durante a captura.

O filtro `arp` foi importante porque me ajudou a perceber que não preciso tentar entender tudo ao mesmo tempo. Posso primeiro definir o que estou procurando e utilizar filtros para facilitar a análise.

> **💡 Principal aprendizado:** Achei muito interessante conseguir visualizar o tráfego da rede acontecendo e perceber como um filtro pode ajudar a destacar informações específicas em meio a muitos pacotes.

---

<br>

<div align="center">

<a href="https://github.com/fer-isa/Minhas-Notas">

<img src="https://img.shields.io/badge/⬅_Voltar_para_Minhas_Notas-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />

</a>

</div>

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2A4365,50:1A365D,100:0B1D3A&height=100&section=footer" width="100%" />
