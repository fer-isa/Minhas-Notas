<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Processos%2C%20Threads%20e%20Registo&fontSize=42&fontColor=FFFFFF&fontAlignY=35&desc=Sysinternals%20Suite%2C%20Process%20Explorer%2C%20Handles%20e%20Regedit%20%7C%20Windows%20Internals%20SOC&descAlignY=55&descSize=16&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Windows_11-161B22?style=for-the-badge&logo=windows11&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Cisco_NetAcad-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Sysinternals_Suite-161B22?style=for-the-badge&logo=microsoft&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/VirusTotal_API-161B22?style=for-the-badge&logo=virustotal&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/SOC_Analysis-161B22?style=for-the-badge&logo=shield&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo
Explorar a arquitetura interna do sistema operativo Windows utilizando ferramentas analíticas avançadas da suite Microsoft Sysinternals (`procexp.exe`) e o editor de registo nativo (`regedit.exe`). O laboratório foca-se na identificação de árvores de processos (relação pai-filho), inspeção de métricas de desempenho e permissões de segurança, rastreio de descritores de sistema (*handles*) e auditoria de configurações persistentes do utilizador.

> **🛡️ Visão de Segurança (SOC):**  
> A monitorização de processos em endpoint (EDR) baseia-se na observação contínua de desvios no comportamento padrão. Analistas de SOC utilizam árvores de processos para detectar injeções de código (*Process Hollowing/Injection*), privilégios de execução anómalos (*Token Impersonation*) e chaves de persistência no Registo (*Run Keys*). A integração direta com o VirusTotal acelera a validação de binários legítimos contra assinaturas maliciosas.

---

## 🧯 O Desafio: Rastreio de Processos e Validação de Reputação

<details open>
  <summary><b>❌ 1. Identificação Visual e Associação de Janelas (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Cenário:</b> Identificar quais os processos ativos no modo de utilizador correspondiam às janelas visíveis no ecrã.</li>
    <li><b>O problema:</b> A ferramenta da mira de arrasto (<i>Find Window's Process</i>) pode sofrer restrições de foco ou permissões quando direcionada a navegadores modernos com múltiplos processos em sandbox.</li>
    <li><b>Resolução prática:</b> Utilização do filtro contextual <code>&lt;Filter by name&gt;</code> no Process Explorer para isolar a árvore hierárquica completa do navegador (processo principal de renderização e filhos dedicados a abas/extensões).</li>
  </ul>
</details>

<details open>
  <summary><b>🛠️ 2. Integração e Verificação no VirusTotal (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li>Durante a inspeção do processo de sistema <code>conhost.exe</code> (Console Window Host), utilizou-se a funcionalidade nativa do Process Explorer para submissão direta do hash do binário à base de inteligência do VirusTotal.</li>
    <li>Após aceitação dos Termos de Serviço da API, o Process Explorer retornou com sucesso a pontuação de reputação (<code>0/76</code>), atestando a integridade e autenticidade da imagem de sistema da Microsoft.</li>
  </ul>
</details>

---

## 🔎 Execução Prática e Análise Técnica

<details open>
  <summary><b>🌳 1. Árvore de Processos e Encerramento em Cascata (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Processos Pai vs. Filho:</b> Ao executar o Prompt de Comando (<code>cmd.exe</code>), este opera como processo filho do <code>explorer.exe</code>. Quando um comando como <code>ping -t 8.8.8.8</code> é iniciado, o <code>cmd.exe</code> gera dinamicamente um novo processo filho transitório denominado <code>PING.EXE</code>.</li>
    <li><b>Destruição de Sessão:</b> O encerramento forçado (<code>Kill Process</code>) aplicado ao processo pai encerra imediatamente todas as dependências e processos filhos associados (como o fecho imediato da janela do navegador ou a terminação em cascata do <code>conhost.exe</code>).</li>
  </ul>
</details>

<details open>
  <summary><b>🧵 2. Auditoria de Desempenho, Permissões e Handles (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Propriedades de Execução (Performance):</b> Monitorização detalhada de ciclos de clock, tempo de execução em modo Kernel vs. Modo Utilizador, alocação de memória virtual e paginação (*Page Faults*).</li>
    <li><b>Identidade e Privilégios (Security):</b> Inspecção dos identificadores de segurança (SID), grupos de pertença do utilizador e privilégios do token (como <code>SeChangeNotifyPrivilege</code>), essenciais para validar o nível de integridade do processo.</li>
    <li><b>Handles (Identificadores de Kernel):</b> Acedidas através do modo <i>Lower Pane View</i> (<code>Ctrl + H</code>). Como as aplicações em modo de utilizador não podem aceder diretamente aos recursos de baixo nível, o Windows fornece <i>handles</i> que atuam como ponteiros seguros para ficheiros no disco (<code>File</code>), chaves do registo (<code>Key</code>), secções de memória (<code>Section</code>) e portas de comunicação assíncronas (<code>ALPC Port</code>).</li>
  </ul>
</details>

<details open>
  <summary><b>🗄️ 3. Estrutura e Modificação do Registo do Windows (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Navegação Estrutural:</b> Acesso à chave de configuração de ambiente de trabalho:</li>
  </ul>
  <pre><code>HKEY_CURRENT_USER\Control Panel\Desktop</code></pre>
  <ul>
    <li><b>Alteração de Parâmetro:</b> Modificação do valor <code>CursorBlinkRate</code> (tipo <code>REG_SZ</code>) do padrão de <code>530</code> milissegundos para <code>200</code> milissegundos para ajuste manual da taxa de intermitência do cursor.</li>
    <li><b>Segregação de Privilégios:</b> Confirmação prática de que alterações no ramo <code>HKEY_CURRENT_USER</code> (HKCU) isolam-se estritamente ao utilizador com sessão iniciada, enquanto diretivas globais de sistema residem sob <code>HKEY_LOCAL_MACHINE</code> (HKLM).</li>
  </ul>
</details>

---

## 💡 O Que Aprendi na Prática (Conceitos Técnicos)
* **Isolamento de Memória (User Mode vs. Kernel Mode):** A razão pela qual os processos dependem de *handles* é a proteção do sistema operativo. Um processo comum nunca toca o hardware diretamente; ele solicita ao kernel permissão para ler um objeto, e o kernel devolve um identificador controlado.
* **Detecção de Anomalias em SOC:** A hierarquia de processos é uma das primeiras fontes de análise contra ataques cibernéticos. Se um processo de sistema como <code>svchost.exe</code> ou <code>conhost.exe</code> surgir fora da sua árvore legítima (ou for iniciado por um documento do Word/Excel), trata-se de um forte indício de execução maliciosa.
* **Reputação Automatizada via EDR/Sysinternals:** A capacidade de cruzar hashes de binários em execução com o VirusTotal diretamente da ferramenta de triagem reduz o tempo de contenção de ameaças (*Mean Time to Respond*).

---

## 🗺️️ Evidências da Execução no Sistema

<details open>
  <summary><b>1. Inicialização do Process Explorer e Mapeamento de Processos (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 1: Foto com a lista geral colorida do Process Explorer e Secure System selecionado -->
    <img width="750" alt="Evidência 1 - Interface Inicial do Process Explorer"  src="https://github.com/user-attachments/assets/df0cbc74-f133-4998-893b-aca4f511228a" />
    <p><i>Execução do <code>procexp.exe</code> exibindo a árvore de processos do Windows, colunas de monitorização e divisão por cores.</i></p>
  </div>
</details>

<details open>
  <summary><b>2. Filtragem e Análise de Processos em Sandbox do Navegador (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 2: Foto com o filtro 'chrome' e múltiplos chrome.exe na lista -->
    <img width="750" alt="Evidência 2 - Isolamento de Processos do Chrome via Filtro" src="https://github.com/user-attachments/assets/80a9d21e-b7cb-4597-bde8-ecb597fcd0d9" />
    <p><i>Utilização do filtro contextual para isolar o processo pai e subprocessos do <code>chrome.exe</code> antes do encerramento forçado.</i></p>
  </div>
</details>

<details open>
  <summary><b>3. Rastreio da Árvore de Linha de Comandos (cmd.exe) (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 3: Foto estreita com o filtro 'cmd' e o cmd.exe listado -->
    <img width="750" alt="Evidência 3 - Identificação do cmd.exe no Process Explorer"  src="https://github.com/user-attachments/assets/6c24311e-9346-405e-bd2b-7b78d5ce3c83" />
    <p><i>Localização do processador de comandos <code>cmd.exe</code> com seu PID e propriedades de consumo de memória.</i></p>
  </div>
</details>

<details open>
  <summary><b>4. Consulta ao VirusTotal e Inspeção de Handles do Kernel (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 4: Foto com a tela dividida ao meio, conhost.exe com score 0/76 e lista de Handles abaixo -->
    <img width="750" alt="Evidência 4 - Verificação VirusTotal e Painel Inferior de Handles"   src="https://github.com/user-attachments/assets/5b80a1e7-6b7f-493e-867d-6f5fa4d86823" />
    <p><i>Verificação com pontuação <code>0/76</code> no VirusTotal para o <code>conhost.exe</code> e inspeção de ficheiros, portas e chaves de registo abertas via painel de Handles.</i></p>
  </div>
</details>

<details open>
  <summary><b>5. Auditoria de Propriedades de Execução (Performance e Segurança) (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 5A: Janela de propriedades conhost.exe aberta na aba Performance -->
    <img width="480" alt="Evidência 5 - Propriedades de Performance do conhost.exe" src="https://github.com/user-attachments/assets/12838cda-ce63-4c12-88fa-ba96930e05d5" />
    <br><br>
</details>

<details open>
  <summary><b>6. Navegação e Modificação no Editor do Registo (regedit.exe) (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 6A: Foto da árvore do Regedit aberta em HKCU\Control Panel\Desktop -->
    <img width="750" alt="Evidência 6A - Navegação na chave HKCU Control Panel Desktop"  src="https://github.com/user-attachments/assets/04a0a2c5-899b-4adc-95f6-e8627e66bd52" />
    <br><br>
    <!-- Evidência 6B: Foto do pop-up 'Editar Cadeia de Caracteres' alterando o CursorBlinkRate para 200 -->
    <img width="500" alt="Evidência 6B - Alteração do valor CursorBlinkRate para 200" src="https://github.com/user-attachments/assets/124a7e2a-f85a-4f48-9c42-cff16e4f297e" />
    <p><i>Acesso ao hive <code>HKEY_CURRENT_USER\Control Panel\Desktop</code> e modificação manual do parâmetro <code>CursorBlinkRate</code> para 200 ms.</i></p>
  </div>
</details>

---

## 📚 Referência Técnica: Roteiro Oficial do Laboratório (Cisco NetAcad)
> ℹ️ Esta secção resume o guião oficial "Laboratório - Explorando Processos, Threads, Handles e Registro do Windows" e serve como **referência técnica**, não como relato do que foi executado.

<details>
  <summary><b>📋 Resumo do Roteiro Oficial (Clique para expandir)</b></summary>
  <br>
  <ul>
    <li><b>Parte 1: Explorando Processos:</b> Descarregamento da suite Sysinternals, identificação de processos com a ferramenta de mira, terminação forçada de processos e observação da criação de subprocessos (<code>cmd.exe</code> gerando <code>PING.EXE</code>).</li>
    <li><b>Parte 2: Explorando Threads e Alças:</b> Consulta das propriedades de execução de tópicos (<i>Threads</i>), submissão de binários ao VirusTotal e visualização em painel duplo de descritores de sistema (<i>Handles</i>) associados a ficheiros e memória.</li>
    <li><b>Parte 3: Explorando o Registro do Windows:</b> Navegação estrutural nas secções do Registo (<i>Hives</i>) com o <code>regedit.exe</code> e modificação manual do valor de intermitência do cursor em <code>HKEY_CURRENT_USER</code>.</li>
  </ul>
</details>

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
