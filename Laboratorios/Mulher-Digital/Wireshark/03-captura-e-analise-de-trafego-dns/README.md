<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Análise%20de%20Tráfego%20DNS&fontSize=46&fontColor=FFFFFF&fontAlignY=35&desc=Resolução%20de%20Nomes,%20UDP%20Port%2053%20e%20Registos%20%7C%20Wireshark&descAlignY=55&descSize=18&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Wireshark-161B22?style=for-the-badge&logo=wireshark&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Networking_CCST-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/DNS_&_UDP_53-161B22?style=for-the-badge&logo=internetexplorer&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Segurança_Defensiva-161B22?style=for-the-badge&logo=shield&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo
O foco deste laboratório prático foi capturar e dissecar pacotes do protocolo **DNS (Domain Name System)** em tempo real através do **Wireshark**. O exercício explorou o fluxo completo de resolução de nomes iniciado pelo utilitário `nslookup`, analisando desde o encapsulamento em **UDP (porta 53)** e cabeçalhos de Camada 2/3 até à estrutura das mensagens de consulta (*Standard query*) e resposta (*Standard query response*), inspecionando registos **A** e apontamentos canónicos **CNAME**.

> **🛡️️ Visão de Segurança (SOC):**  
> O tráfego DNS não cifrado (porta UDP 53) é um dos vetores mais visados em ataques cibernéticos e um canal indispensável de auditoria em operações de SOC. Através da análise profunda dos pacotes DNS, um analista consegue detetar atividades de **Comando e Controlo (C2 / Botnets)** que utilizam algoritmos de geração de domínio (DGA), tentativas de **DNS Tunneling** (onde dados confidenciais são fragmentados e exfiltrados por meio de subdomínios ou registos TXT) e ataques de **DNS Spoofing / Poisoning**, nos quais respostas forjadas redirecionam tráfego legítimo para servidores controlados por agentes maliciosos.

---

## 🗺️ O Ambiente e Testes de Resolução
O procedimento iniciou com a limpeza da memória temporária do sistema operativo (`ipconfig /flushdns`) para forçar o computador a consultar a rede. Em seguida, foi executado o diagnóstico interativo via `nslookup`:

<div align="center">
  <!-- FOTO 1: Início do nslookup (image_e048cb.png) -->
  <img width="500" alt="Evidência 1 - Execução do nslookup no Terminal"  src="https://github.com/user-attachments/assets/1f27e016-58d2-4a26-8ab4-6bb99a63fb26" />
  <p><i>Inicialização do utilitário nslookup identificando o gateway local (fe80::4689:6dff:fe7a:ed70) como o servidor DNS recursivo padrão.</i></p>
</div>

<br>

<div align="center">
  <!-- FOTO 2: Resposta final do nslookup (image_dff4f3.png) -->
  <img width="500" alt="Evidência 2 - Resposta Textual do Domínio www.cisco.com" src="https://github.com/user-attachments/assets/7d84ffcb-8d25-4c9b-a65b-c370b0f827d0" />
  <p><i>Saída do terminal: resolução não autoritativa exibindo os aliases CNAME (akadns, edgekey, akamaiedge), endereços IPv6 e o endereço IPv4 público final 2.17.128.103.</i></p>
</div>

---

## 💡 O Que Aprendi na Prática (Conceitos Técnicos)
* **Operação sobre UDP:** Consultas rotineiras de DNS operam na Camada de Transporte através de **UDP** na porta padrão **53**, priorizando a baixa sobrecarga e velocidade sem necessidade de estabelecer handshake prévio.
* **Portas Efêmeras de Origem:** Enquanto o servidor aguarda na porta de serviço fixa `53`, o sistema operativo cliente aloca dinamicamente uma porta alta e temporária (no caso capturado, a porta `65186`) para receber o retorno dos dados.
* **Cadeia de Aliases CNAME:** Um único domínio pode apontar para múltiplos nomes canónicos intermediários até alcançar o servidor de destino, estratégia amplamente empregada por redes de distribuição de conteúdo (CDN da Akamai) para balanceamento de carga e redução de latência.
* **Recursividade e Flags:** O cabeçalho DNS traz parâmetros de controlo específicos, como o bit `RD` (*Recursion Desired*), onde a estação solicita formalmente que o servidor resolva todo o caminho hierárquico na Internet em seu nome.

---

## ⚙️ Captura, Filtros e Dissecação de Pacotes

<details open>
  <summary><b>🔍 1. Filtragem e Localização da Consulta no Wireshark (Clique para recolher)</b></summary>
  <br>
  <p>Com a captura em execução, filtrei o tráfego pela porta de serviço do protocolo através de <code>udp.port == 53</code> e localizei a consulta correspondente ao registo <b>A</b> gerada pelo cliente:</p>

  <div align="center">
    <!-- FOTO 3: Pacote 1880 selecionado (image_dff540.png) -->
    <img width="900" alt="Evidência 3 - Pacote 1880 de Consulta Standard query A www.cisco.com"  src="https://github.com/user-attachments/assets/ad653e6d-8db1-412f-9f75-c6c49e64b190" />
    <p><i>Tabela de pacotes capturados destacando a linha 1880: envio da requisição Standard query com identificador de transação 0x0002 para www.cisco.com.</i></p>
  </div>
</details>

<details open>
  <summary><b>🔎 2. Dissecação da Resposta DNS e Cabeçalhos de Camada (Clique para recolher)</b></summary>
  <br>
  <p>Na sequência do fluxo, selecionei o pacote de resposta associado (linha <b>1881</b>) e analisei a pilha de protocolos de rede:</p>

  <div align="center">
    <!-- FOTO 4: Pacote 1881 selecionado na lista (image_dff59b.png) -->
    <img width="900" alt="Evidência 4 - Pacote 1881 de Resposta DNS"  src="https://github.com/user-attachments/assets/20b40b3f-c470-4d71-a4ce-834ca38593ee" />
    <p><i>Seleção da resposta DNS (pacote 1881) confirmando o tamanho do payload capturado e a correlação direta com a pergunta efetuada.</i></p>
  </div>
  <br>
  <div align="center">
    <!-- FOTO 5: Painel de detalhes das camadas expandido (image_e0481a.png) -->
    <img width="900" alt="Evidência 5 - Dissecação dos Cabeçalhos L2, L3, L4 e L7"  src="https://github.com/user-attachments/assets/f16754db-0180-4625-a5e6-c202fc8fd868" />
    <p><i>Inspeção detalhada: Ethernet II identificando o MAC do gateway (origem) e do host (destino), porta UDP 53 retornando para a porta 65186, código No error e 4 registos de resposta (Answer RRs).</i></p>
  </div>
  <br>
  <p>Expansão do bloco <b>Answers</b> revelando o caminho estrutural de resolução do nome:</p>

  <div align="center">
    <!-- FOTO 6: Answers expandido (image_e048b7.png) -->
    <img width="900" alt="Evidência 6 - Secção Answers com CNAMEs e Registo A" src="https://github.com/user-attachments/assets/fc7c7e37-9668-4ef9-80de-6457155760f1" />
    <p><i>Cadeia de resolução completa: www.cisco.com redirecionado via CNAME para akadns, edgekey e akamaiedge, culminando no IP de destino final 2.17.128.103.</i></p>
  </div>
</details>

---

## 📊 Matriz Comparativa: Pacote de Consulta (Query) vs. Resposta (Response)

| **Porta de Destino (L4)** | `53` (Porta de escuta do servidor DNS) | `65186` (Porta cliente de retorno) |
| **Endereço MAC de Origem** | `c8:cb:9e:9f:a4:c5` (Placa de rede do host) | `44:89:6d:7a:ed:70` (Interface do gateway local) |
| **Flag QR (Query / Response)**| `0` (Identifica envio de pergunta) | `1` (Identifica mensagem de resposta) |
| **Código de Status** | Ausente (apenas parâmetros de pedido) | `No error (0)` (Sucesso na consulta) |
| **Bloco Answers** | Vazio (`Answer RRs: 0`) | Preenchido com 4 registos (`3 CNAMEs + 1 Registo A`) |

---

## 🚧 Desafios Enfrentados e Resolução Prática
1. **Cache Local Impedindo a Geração de Tráfego:**  
   * *O problema:* Ao executar a consulta de um domínio visitado recentemente, o computador utilizava as informações guardadas em memória local, sem emitir pacotes de saída na rede.  
   * *A solução:* Executar o comando `ipconfig /flushdns` no Prompt de Comando com privilégios adequados, forçando a limpeza do cache de DNS antes de iniciar os testes.
2. **Múltiplas Respostas no Wireshark (A vs. AAAA):**  
   * *O problema:* A captura retornava várias linhas quase simultâneas para o mesmo domínio, gerando dúvida sobre qual pacote representava a resposta necessária para o laboratório.  
   * *A solução:* Analisar a coluna *Info* e o campo *Transaction ID* (`0x0002`), diferenciando a resposta do registo **A** (IPv4) das consultas e respostas do registo **AAAA** (IPv6).
3. **Associação de Endereçamento Link-Local em IPv6:**  
   * *O problema:* A comunicação entre o host e o roteador ocorreu primariamente através de endereços de escopo local (`fe80::`), tornando indispensável verificar a correlação física de camada 2.  
   * *A solução:* Confirmar o endereço físico do adaptador via `ipconfig /all` para validar a correspondência dos endereços MAC da placa Wi-Fi com o quadro dissecado no analisador de pacotes.

<br>

<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Minhas_Notas-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2A4365,50:1A365D,100:0B1D3A&height=100&section=footer" width="100%" />
