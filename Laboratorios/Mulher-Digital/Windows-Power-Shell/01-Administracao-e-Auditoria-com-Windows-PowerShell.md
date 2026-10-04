<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Administra%C3%A7%C3%A3o%20e%20Auditoria%20PowerShell&fontSize=38&fontColor=FFFFFF&fontAlignY=35&desc=Cmdlets%2C%20Aliases%2C%20Mapeamento%20de%20Rede%20e%20Correla%C3%A7%C3%A3o%20de%20Processos%20%7C%20SOC&descAlignY=55&descSize=15&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Windows_PowerShell-161B22?style=for-the-badge&logo=powershell&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Windows_11-161B22?style=for-the-badge&logo=windows11&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Cisco_NetAcad-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Network_Auditing-161B22?style=for-the-badge&logo=wireshark&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/SOC_Analysis-161B22?style=for-the-badge&logo=shield&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo
Compreender a arquitetura operacional do Windows PowerShell, suas distinções em relação ao Prompt de Comando tradicional (`cmd.exe`), a estrutura modular de cmdlets orientados a objetos (*verb-noun*) e a aplicação prática de comandos de rede e administração em investigações de segurança e triagem de endpoints.

> **🛡️ Visão de Segurança (SOC):**  
> O PowerShell é uma das principais ferramentas de administração corporativa e, simultaneamente, um dos vetores mais visados por atacantes para execuções sem ficheiro (*living-off-the-land*). Dominar a correlação de portas abertas com identificadores de processo (PIDs), a inspeção de rotas locais e a automação do sistema fornece a base essencial para identificar tráfego anómalo e conexões suspeitas de Command & Control (C2).

---

## 🔎 Execução Prática e Análise Técnica

<details open>
  <summary><b>💻 1. Prompt de Comando vs. PowerShell: Comparação e Aliases (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Interoperabilidade de Comandos:</b> Validação de que utilitários clássicos de rede (<code>ipconfig</code>, <code>ping</code>) funcionam em ambas as consoles com resultados funcionais idênticos.</li>
    <li><b>Comportamento do comando dir:</b> Enquanto o CMD exibe texto formatado simples, o PowerShell utiliza um alias que encapsula o cmdlet nativo <code>Get-ChildItem</code>, gerando objetos estruturados com propriedades detalhadas (<code>Mode</code>, <code>LastWriteTime</code>, <code>Length</code>, <code>Name</code>).</li>
    <li><b>Auditoria de Aliases:</b> Execução de <code>Get-Alias dir</code> para revelar a associação interna da consola.</li>
  </ul>
</details>

<details open>
  <summary><b>🌐 2. Inspeção de Roteamento Local (netstat -r) (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li>Execução de <code>netstat -r</code> no PowerShell elevado para auditar a tabela de encaminhamento IPv4 e IPv6 e a lista de interfaces físicas e virtuais.</li>
    <li>Mapeamento da rota padrão <code>0.0.0.0</code> com máscara <code>0.0.0.0</code>, identificando a interface local ativa (<code>192.168.15.4</code>) e o Gateway predefinido da rede (<code>192.168.15.1</code>).</li>
  </ul>
</details>

<details open>
  <summary><b>🔍 3. Mapeamento de Portas, Binários e PIDs (netstat -abno) (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li>Utilização dos modificadores avançados do <code>netstat</code> sob privilégios administrativos:
      <ul>
        <li><code>-a</code>: Exibe todas as portas em escuta (LISTENING) e conexões ativas.</li>
        <li><code>-b</code>: Mostra o binário executável responsável pelo socket de rede.</li>
        <li><code>-n</code>: Exibe endereços e portas em formato numérico direto.</li>
        <li><code>-o</code>: Exibe o identificador numérico de processo (PID) associado.</li>
      </ul>
    </li>
    <li><b>Correlação com o Gestor de Tarefas:</b> Vinculação direta da porta TCP 445 (SMB) em estado <code>LISTENING</code> ao PID <code>4</code>, validado na aba <i>Detalhes</i> como pertencente ao processo <code>System</code> (NT Kernel & System) sob a conta <code>SISTEMA</code>.</li>
  </ul>
</details>

<details open>
  <summary><b>⚙️ 4. Automação e Limpeza de Sistema com Cmdlets (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li>Aplicação do cmdlet <code>Clear-RecycleBin</code> para automação de tarefas administrativas de higienização de disco.</li>
    <li>Validação da confirmação de segurança e eliminação definitiva de ficheiros temporários do sistema sem dependência de interação pela interface gráfica.</li>
  </ul>
</details>

---

## 💡 O Que Aprendi na Prática (Conceitos Técnicos)
* **Objetos vs. Texto Puro:** Ao contrário do terminal Unix clássico ou do CMD, o PowerShell não canaliza apenas texto formatado; ele transmite objetos completos do .NET Framework com métodos e propriedades manipuláveis por pipelines (`|`).
* **Triagem de Portas Suspeitas em SOC:** O comando `netstat -abno` é uma ferramenta inicial de resposta a incidentes. Permite a um analista identificar uma porta aberta desconhecida, rastrear o executável que a originou e correlacionar com o PID no sistema operacional para isolar o processo malicioso.
* **Tabela de Rotas Local:** A rota padrão (`0.0.0.0`) define para onde qualquer pacote cujo destino não pertença à sub-rede local deve ser enviado (o gateway). O reconhecimento desta tabela é vital para identificar ataques de envenenamento ou rotas não autorizadas no endpoint.

---

## 🗺️ Evidências da Execução no Sistema

<details open>
  <summary><b>1. Comparação de Comandos: dir no CMD vs. PowerShell (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 1A: Captura de tela 2026-09-30 231308.png -->
    <img width="650" alt="Evidência 1A - dir no Prompt de Comando"  src="https://github.com/user-attachments/assets/282b6d06-40fe-4688-a5be-ddbbfeb60335" />
    <br><br>
    <!-- Evidência 1B: Captura de tela 2026-09-30 231401.png -->
    <img width="650" alt="Evidência 1B - dir no PowerShell" src="https://github.com/user-attachments/assets/01607d3d-8a2e-4273-b424-d3d52aa3a21d" />
    <p><i>Comparação da saída textual tradicional do CMD contra a saída orientada a objetos (Mode, LastWriteTime, Length) no PowerShell.</i></p>
  </div>
</details>

<details open>
  <summary><b>2. Execução de Utilitários de Rede: ipconfig e ping (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 2A: Captura de tela 2026-09-30 231434.png / 231509.png -->
    <img width="650" alt="Evidência 2A - ipconfig em ambas as consolas"  src="https://github.com/user-attachments/assets/2fffc0d4-1038-40e7-ad46-9d0c9af0378f" />
    <!-- Evidência 2B: Captura de tela 2026-09-30 231538.png / 231611.png -->
    <img width="650" alt="Evidência 2B - ping 127.0.0.1 loopback" src="https://github.com/user-attachments/assets/c44643d4-f254-45e6-89da-65eb05bf65c0" />
    <p><i>Validação de adaptadores locais via ipconfig e teste da pilha TCP/IP com ping em loopback (127.0.0.1) com 0% de perda.</i></p>
  </div>
</details>

<details open>
  <summary><b>3. Inspeção de Cmdlets e Aliases (Get-Alias) (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 3: Captura de tela 2026-09-30 231708.png -->
    <img width="650" alt="Evidência 3 - Get-Alias dir"  src="https://github.com/user-attachments/assets/74abd9b7-2a71-4677-994e-343bb23e6c20" />
    <p><i>Mapeamento do alias 'dir' apontando para o cmdlet nativo Get-ChildItem.</i></p>
  </div>
</details>

<details open>
  <summary><b>4. Auditoria de Tabela de Rotas (netstat -r) (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 4: Captura de tela 2026-09-30 231935.png / 232038.png -->
    <img width="650" alt="Evidência 4 - Tabela de Rotas netstat -r"  src="https://github.com/user-attachments/assets/d5554e5e-e57e-4222-b404-35a7693ca2eb" />
    <p><i>Inspeção da lista de interfaces e mapeamento da rota padrão IPv4 (0.0.0.0) associada ao gateway 192.168.15.1.</i></p>
  </div>
</details>

<details open>
  <summary><b>5. Correlação de Portas, Binários e PIDs (netstat -abno e Gestor de Tarefas) (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 5A: Captura de tela 2026-09-30 232120.png -->
    <img width="650" alt="Evidência 5A - netstat -abno" src="https://github.com/user-attachments/assets/f2e1f6d2-30e8-4957-8e43-59e21658f8fe" />
    <br><br>
    <!-- Evidência 5B: Captura de tela 2026-09-30 232321.png -->
    <img width="650" alt="Evidência 5B - Gestor de Tarefas Detalhes PID"  src="https://github.com/user-attachments/assets/53fd78bd-3e55-40f6-9dd1-17e8b309465b" />
    <p><i>Mapeamento da porta TCP 445 associada ao PID 4 via netstat e validação correspondente no Gestor de Tarefas sob o processo 'System' (NT Kernel & System).</i></p>
  </div>
</details>

<details open>
  <summary><b>6. Automação de Limpeza com Clear-RecycleBin (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 6: image_77b2c2.png -->
    <img width="650" alt="Evidência 6 - Clear-RecycleBin"  src="https://github.com/user-attachments/assets/d607f6f9-3811-47c0-b6de-45af51b0b762" />
    <p><i>Execução do cmdlet Clear-RecycleBin com confirmação interativa para esvaziamento permanente da Lixeira.</i></p>
  </div>
</details>

---

## 📚 Referência Técnica: Roteiro Oficial do Laboratório (Cisco NetAcad)
> ℹ️ Esta secção resume o guião oficial "Laboratório - Usando o Windows PowerShell" e serve como **referência técnica**, não como relato do que foi executado.

<details>
  <summary><b>📋 Resumo do Roteiro Oficial (Clique para expandir)</b></summary>
  <br>
  <ul>
    <li><b>Parte 1: Acesse o console do PowerShell:</b> Abertura do Windows PowerShell e do Prompt de Comando para configuração do ambiente de testes.</li>
    <li><b>Parte 2: Explore comandos do Prompt de Comando e do PowerShell:</b> Comparação de saídas entre comandos compatíveis (dir, ipconfig, ping).</li>
    <li><b>Parte 3: Explore cmdlets:</b> Identificação de comandos verb-noun e resolução de aliases através de Get-Alias.</li>
    <li><b>Parte 4: Explore o comando netstat usando o PowerShell:</b> Mapeamento de estatísticas de protocolo, tabela de roteamento (netstat -r) e correlação de sockets abertos com PIDs de processos (netstat -abno).</li>
    <li><b>Parte 5: Esvazie a lixeira usando o PowerShell:</b> Demonstração de automação de tarefas administrativas via cmdlet Clear-RecycleBin.</li>
  </ul>
</details>

---

## 💬 Questões de Reflexão (Gabarito Técnico Oficial)

**1. O PowerShell foi desenvolvido para automação de tarefas e gerenciamento de configuração. Usando a internet, pesquise comandos que você poderia usar para simplificar suas tarefas como analista de segurança. Anote suas descobertas.**  
> Em funções de SOC e segurança defensiva, o PowerShell é amplamente utilizado para triagem rápida sem necessidade de instalar ferramentas adicionais:
> * `Get-WinEvent`: Coleta e filtra registos de segurança do Windows Event Viewer, como tentativas sucessivas de logon com falha (Event ID 4625).
> * `Get-Process`: Lista processos ativos permitindo inspecionar executáveis que consomem recursos excessivos ou que foram iniciados a partir de diretórios temporários (`AppData`, `Temp`).
> * `Get-NetTCPConnection`: Cmdlet nativo para inspecionar conexões de rede ativas com estados `Established` ou `Listen`, facilitando a localização de tráfego de rede suspeito.
> * `Get-FileHash`: Gera assinaturas criptográficas (ex.: SHA256) de binários descarregados para comparação imediata com bases de reputação como VirusTotal.

---

<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas/tree/main/Mulher-Digital/Ciberseguranca">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Índice_de_Cibersegurança-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=120&section=footer&animation=fadeIn" width="100%" />

</div>
