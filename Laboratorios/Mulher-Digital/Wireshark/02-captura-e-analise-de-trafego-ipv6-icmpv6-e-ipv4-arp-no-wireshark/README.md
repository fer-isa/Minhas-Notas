<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Análise%20IPv6%20vs%20IPv4&fontSize=46&fontColor=FFFFFF&fontAlignY=35&desc=Captura%20de%20Pacotes,%20ICMPv6,%20NDP%20e%20ARP%20%7C%20Wireshark&descAlignY=55&descSize=18&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Wireshark-161B22?style=for-the-badge&logo=wireshark&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Networking_CCST-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/IPv6_&_ICMPv6-161B22?style=for-the-badge&logo=internetexplorer&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Análise_de_Tráfego_SOC-161B22?style=for-the-badge&logo=shield&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo
O foco deste laboratório prático foi capturar, dissecar e analisar o tráfego de rede real em tempo de execução utilizando o **Wireshark**. O exercício explorou as diferenças estruturais entre a pilha de protocolos **IPv6** e **IPv4**, investigando desde a composição dos cabeçalhos de Camada 3 até à substituição definitiva do broadcast legado do **ARP** pelo protocolo moderno **ICMPv6 Neighbor Discovery Protocol (NDP)**.

> **🛡️ Visão de Segurança (SOC):**  
> Em monitorização de segurança e triagem de alertas, a análise de pacotes crus é a fonte primária de verdade. Compreender a transição entre ARP e NDP é crucial para identificar anomalias: enquanto no IPv4 os ataques de envenenamento de cache (*ARP Spoofing/Poisoning*) exploram broadcasts não autenticados para interceptar dados (Man-in-the-Middle), no IPv6 o tráfego de resolução baseia-se em *Multicast* e mensagens ICMPv6 específicas (*Neighbor Solicitation* e *Neighbor Advertisement*), exigindo que o analista de SOC saiba filtrar mensagens do tipo 135/136 para detetar comportamentos maliciosos como *Rogue Router Advertisements* ou tentativas de redirecionamento de vizinhos.

---

## 🗺️ O Ambiente de Captura
O laboratório foi realizado num ambiente de rede real, analisando a comunicação entre a interface de rede sem fios (Wi-Fi) da estação de trabalho e o router/gateway da rede local, além do encaminhamento de pacotes para a Internet pública:

<div align="center">
  <!-- EVIDÊNCIA 1: Interface Wi-Fi ativa no Wireshark -->
  <img width="1267" height="1013" alt="Captura de tela 2026-09-30 000246" src="https://github.com/user-attachments/assets/978a6f24-a679-4ee5-affe-7bf4f2923756" alt="Evidência 1 - Seleção da Interface Ativa no Wireshark"/>
  <p><i>Seleção da placa de rede Wi-Fi ativa no Wireshark apresentando oscilação contínua de tráfego antes de iniciar a recolha de pacotes.</i></p>
</div>

---

## 💡 O Que Aprendi na Prática (Conceitos Técnicos)
* **Estrutura de Cabeçalho Fixa no IPv6:** Ao contrário do IPv4 (cujo cabeçalho varia de 20 a 60 bytes e exige processamento do campo IHL), o IPv6 possui um cabeçalho estritamente padronizado em 40 bytes. Isto agiliza o encaminhamento pelos routers em hardware.
* **Fim do Broadcast e Chegada do Multicast no NDP:** O IPv6 extinguiu completamente o tráfego em broadcast (`255.255.255.255` ou `ff:ff:ff:ff:ff:ff`). A resolução de camada 2 utiliza mensagens ICMPv6 direcionadas a grupos específicos de Multicast (*Solicited-Node Multicast*), evitando interromper desnecessariamente todas as estações do segmento local.
* **Next Header (58) vs. Protocol (1):** No IPv4, o tipo de carga útil de rede é identificado pelo campo `Protocol`. No IPv6, este processo é encadeado pelo campo `Next Header`, que aponta para o protocolo seguinte (como o valor `58` para mensagens de controlo ICMPv6 ou `6` para TCP).
* **Hop Limit vs. Time to Live (TTL):** O contador de saltos foi renomeado de TTL para `Hop Limit` no IPv6, mantendo o objetivo de descartar pacotes em rota circular antes de congestionarem a rede.

---

## ⚙️ Procedimentos, Filtros e Dissecação de Pacotes

<details open>
  <summary><b>🔍 1. Captura e Análise de IPv6 e ICMPv6 NDP (Clique para recolher)</b></summary>
  <br>
  <p>Com a captura em execução, filtrei o tráfego com <code>icmpv6</code> e executei o diagnóstico direcionado ao endereço <i>Link-Local</i> do router via Prompt de Comando, informando o identificador da interface (<code>%5</code>):</p>
  <pre><code>ping fe80::ca8c:bb2e:391a:2f5%5</code></pre>
  
  <div align="center">
    <!-- EVIDÊNCIA 2: Tabela de pacotes ICMPv6 -->
    <img width="1906" height="447" alt="Captura de tela 2026-09-30 000457" src="https://github.com/user-attachments/assets/2440e3d8-a10b-43e2-b9f7-c1af3a8db1db" alt="Evidência 2 - Tabela de Pacotes ICMPv6 Capturados" />
    <p><i>Captura de pacotes ICMPv6 exibindo a troca de mensagens Neighbor Solicitation (pedido) e Neighbor Advertisement (resposta de vizinho).</i></p>
  </div>
  <br>
  <div align="center">
    <!-- EVIDÊNCIA 3: Cabeçalho IPv6 e ICMPv6 expandidos -->
    <img width="1037" height="392" alt="Captura de tela 2026-09-30 001411" src="https://github.com/user-attachments/assets/169167f4-bc47-4620-bc25-947b657405ba" alt="Evidência 3 - Dissecação dos Cabeçalhos IPv6 e ICMPv6" />
    <p><i>Estrutura do pacote dissecada: confirmação da versão 6 (0110), Next Header 58 (ICMPv6), escopo Link-Local (fe80::) e Global Unicast (2804:7f0:...) com resposta Neighbor Advertisement (Type 136).</i></p>
  </div>
</details>

<details open>
  <summary><b>🔎 2. Captura e Análise de IPv4 e Resolução ARP (Clique para recolher)</b></summary>
  <br>
  <p>Para correlacionar o funcionamento com o modelo IPv4 legado, executei testes de conectividade via Prompt de Comando/PowerShell direcionados para o servidor DNS da Google e para o gateway local:</p>
  
  <div align="center">
    <!-- EVIDÊNCIA 4: Ping 8.8.8.8 no terminal (Captura de tela 2026-09-30 001736.png) -->
    <img width="817" height="307" alt="Captura de tela 2026-09-30 001736" src="https://github.com/user-attachments/assets/50a25eba-6274-4be6-b2b5-23b6677ca935" alt="Evidência 4 - Teste de Ping no Terminal"/>
    <p><i>Execução do utilitário ping para o endereço 8.8.8.8 retornando tempo de resposta e TTL=116.</i></p>
  </div>
  <br>
  <p>No Wireshark, apliquei o filtro de exibição <code>icmp or arp</code> para capturar simultaneamente os dois comportamentos:</p>
  
  <div align="center">
    <!-- EVIDÊNCIA 5: Tabela com linhas amarelas (ARP) e rosas (ICMP) (Captura de tela 2026-09-30 002033.png) -->
    <img width="1907" height="547" alt="Captura de tela 2026-09-30 002033" src="https://github.com/user-attachments/assets/e6d24b4d-45f0-4692-9d18-af9f357c8fd4" alt="Evidência 5 - Captura Comparativa com Tráfego ARP e ICMP IPv4"/>
    <p><i>Tabela do Wireshark evidenciando as linhas amarelas de resolução ARP (Who has...?) e as linhas rosas de dados ICMP (Echo request/reply).</i></p>
  </div>
  <br>
  <p>Dissecação dos cabeçalhos em detalhe:</p>

  <div align="center">
    <!-- EVIDÊNCIA 6: Cabeçalho IPv4 expandido (Captura de tela 2026-09-30 002900.png) -->
    <img width="655" height="307" alt="Captura de tela 2026-09-30 002900" src="https://github.com/user-attachments/assets/112dca31-d3ea-4e77-b1e9-98948e327a1e"alt="Evidência 6 - Dissecação do Cabeçalho IPv4" />
    <p><i>Cabeçalho Internet Protocol Version 4 em detalhe: identificação de Version: 4, Header Length: 20 bytes, Time to Live: 116 e Protocol: ICMP (1).</i></p>
  </div>
  <br>
  <div align="center">
    <!-- EVIDÊNCIA 7: Cabeçalho ARP expandido (Captura de tela 2026-09-30 002954.png) -->
    <img width="727" height="226" alt="Captura de tela 2026-09-30 002954" src="https://github.com/user-attachments/assets/8572c86b-24ff-4364-87fb-f100a577135f" lt="Evidência 7 - Dissecação do Pacote ARP"/>
    <p><i>Estrutura do pacote ARP (request): operação em Camada 2, solicitando o endereço físico para o IP alvo (192.168.15.201).</i></p>
  </div>
</details>

---

## 📊 Matriz Comparativa Estrutural (IPv4 vs. IPv6)

| Característica / Parâmetro | Pilha IPv4 (Legado) | Pilha IPv6 (Moderno) |
| :--- | :--- | :--- |
| **Formato e Tamanho de Endereço** | 32 bits em formato decimal (`192.168.15.7`) | 128 bits em notação hexadecimal (`2804:7f0:...`) |
| **Dimensão do Cabeçalho Base** | Variável (20 a 60 bytes) | Fixo em 40 bytes |
| **Resolução de Endereço Físico (MAC)**| **ARP** via tráfego de *Broadcast* (`ff:ff:ff:ff:ff:ff`) | **ICMPv6 NDP** via tráfego de *Multicast* |
| **Protocolo de Diagnóstico** | ICMP (Protocol `1`) | ICMPv6 (Next Header `58`) |
| **Prevenção de Ciclos em Rota** | `Time to Live (TTL)` | `Hop Limit` |
| **Checksum em Camada 3** | Sim (`Header Checksum` verificado em cada salto) | Não (eliminado do cabeçalho base para ganho de desempenho) |

---

## 🚧 Desafios Enfrentados e Resolução Prática
Durante o desenvolvimento do laboratório, surgiram barreiras reais de execução que exigiram depuração técnica:

1. **Sintaxe do Ping em Endereços Link-Local (`fe80::`):**  
   * *O problema:* A tentativa de ping direto num IP de enlace local falhava ou gerava erro de sintaxe, porque o sistema operacional não sabia por qual placa física encaminhar o pacote.  
   * *A solução:* Identificar o escopo da interface no Windows via `ipconfig` e anexar o identificador de zona no final do IP (`%5`), permitindo a comunicação correta com a rota local.
2. **Wireshark sem Pacotes na Captura Inicial:**  
   * *O problema:* Ao abrir a ferramenta, o ecrã permaneceu em branco e não listava tráfego.  
   * *A solução:* Diagnosticar que a captura não havia sido iniciada na placa correta; o software estava na página de abertura e foi necessário aceder à placa com atividade de pacotes (`Wi-Fi`) dando dois cliques sobre a interface.
3. **Comportamento da Cache ARP:**  
   * *O problema:* A ausência momentânea de pacotes de resposta ARP na tabela de pacotes gerou dúvida sobre a integridade da recolha.  
   * *A solução:* Compreender o ciclo de vida da cache ARP; uma vez mapeada a relação IP/MAC na tabela temporária do sistema operativo, as mensagens de consulta deixam de ser emitidas até que o temporizador expire ou que ocorra comunicação com um novo endereço.
4. **Interface e Painel de Dissecação Oculto:**  
   * *O problema:* A janela do Wireshark exibia apenas a listagem geral de tráfego, sem o detalhe dos cabeçalhos e campos de camada.  
   * *A solução:* Ajustar a divisória de redimensionamento no rodapé da janela para revelar o painel de detalhes dos pacotes e expandir as árvores estruturais de protocolo.

<br>

<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Minhas_Notas-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2A4365,50:1A365D,100:0B1D3A&height=100&section=footer" width="100%" />
