<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Leitura%20de%20Servidor%20de%20Logs&fontSize=42&fontColor=FFFFFF&fontAlignY=35&desc=Inspe%C3%A7%C3%A3o%20via%20CLI%2C%20Monitoriza%C3%A7%C3%A3o%20em%20Tempo%20Real%20e%20Journalctl%20%7C%20Linux%20SOC&descAlignY=55&descSize=16&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Linux_Terminal-161B22?style=for-the-badge&logo=gnubash&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Cisco_NetAcad-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Log_Analysis-161B22?style=for-the-badge&logo=elasticstack&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Systemd_Journalctl-161B22?style=for-the-badge&logo=linux&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Troubleshooting_Linux-161B22?style=for-the-badge&logo=shield&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo
Dominar as ferramentas fundamentais de linha de comandos Linux (`cat`, `more`, `less`, `tail`, `syslog` e `journalctl`) utilizadas na rotina diária de um analista de SOC para inspecionar, auditar e monitorizar ficheiros de registo em tempo real. O laboratório também envolveu a resolução prática de problemas de permissões de utilizadores em sistemas Linux.

> **🛡️ Visão de Segurança (SOC):**  
> Ficheiros de registo (*logs*) são a principal fonte de evidências num processo de triagem ou resposta a incidentes. Compreender a diferença entre ferramentas estáticas e dinâmicas (como o `tail -f`), bem como navegar na estrutura binária indexada do `journald`, permite identificar anomalias no sistema sem sobrecarregar a memória do servidor.

---

## 🧯 O Desafio: Resolução de Permissões no Ambiente Linux

<details open>
  <summary><b>❌ 1. Conflito de Utilizadores na VM (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Cenário:</b> A máquina virtual unificada iniciou com a sessão do utilizador <code>cisco</code>.</li>
    <li><b>O problema:</b> Ao tentar aceder a <code>/home/analyst/lab.support.files/logstash-tutorial.log</code>, o sistema devolveu o erro <code>Permission denied</code>, pois a pasta pertencia exclusivamente ao utilizador <code>analyst</code>.</li>
    <li><b>Tentativa com gravação:</b> O comando <code>echo "..." >> ...</code> exigia permissões de escrita tanto no ficheiro como na directoria.</li>
  </ul>
</details>

<details open>
  <summary><b>🛠️ 2. Solução e Normalização do Acesso (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li>Alternância para o utilizador proprietário do ambiente de análise:</li>
  </ul>
  <pre><code>su analyst
Password: cyberops</code></pre>
  <ul>
    <li>Desbloqueio definitivo das permissões no directório de suporte via utilizador administrativo:</li>
  </ul>
  <pre><code>sudo chmod -R 777 /home/analyst</code></pre>
  <ul>
    <li>Validação da escrita com anexo de linha de teste bem-sucedido:</li>
  </ul>
  <pre><code>echo "this is a new entry to the monitored log file" >> /home/analyst/lab.support.files/logstash-tutorial.log
tail -n 2 /home/analyst/lab.support.files/logstash-tutorial.log</code></pre>
</details>

---

## 🔎 Execução Prática e Análise Técnica

<details open>
  <summary><b>📑 3. Manipulação de Logs com Cat, More, Less e Tail (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b><code>cat</code>:</b> Exibe todo o conteúdo de forma ininterrupta. Inadequado para ficheiros extensos por não possuir paginação, perdendo o cabeçalho inicial.</li>
    <li><b><code>more</code>:</b> Apresenta o ficheiro dividido por páginas. Permite avançar com a Barra de Espaço, mas não suporta retrocesso eficiente entre páginas.</li>
    <li><b><code>less</code>:</b> Utilitário avançado e interactivo. Permite navegar livremente para a frente e para trás através das setas direcionais, libertando o terminal através da tecla <code>q</code>.</li>
    <li><b><code>tail</code> vs <code>tail -f</code>:</b> O comando <code>tail</code> padrão limita a saída às últimas 10 linhas. O parâmetro <code>-f</code> (<i>follow</i>) mantém o processo aberto em primeiro plano, lendo novas entradas em tempo real.</li>
  </ul>
</details>

<details open>
  <summary><b>🖥️ 4. Inspeção de Syslog e Kernel com Journalctl (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b><code>/var/log/syslog</code>:</b> Arquivo restrito pertencente ao utilizador <code>root</code>. Exige <code>sudo</code> para leitura por conter dados sensíveis da operação do sistema.</li>
    <li><b><code>journalctl</code>:</b> Utilitário do daemon <code>systemd-journald</code> para interpretar registos binários indexados.</li>
    <li><b><code>sudo journalctl -b</code>:</b> Filtra estritamente os eventos registados desde o último arranque do sistema.</li>
    <li><b><code>sudo journalctl -k</code>:</b> Isola as mensagens geradas pelo Kernel (drivers, CPU, alocação de memória BIOS).</li>
  </ul>
</details>

---

## 💡 O Que Aprendi na Prática (Conceitos Técnicos)
* **Sincronização Temporal (NTP):** Manter o relógio dos computadores sincronizado é crucial em cibersegurança. Sem carimbos de data/hora (*timestamps*) exactos, torna-se inviável correlacionar eventos entre diferentes servidores numa linha do tempo forense.
* **Syslog vs. Journald:** O Syslog armazena texto simples não estruturado (fácil leitura direta, mas difícil de filtrar e dependente de rotação manual de ficheiros). O Journald utiliza ficheiros binários estruturados (pesquisas mais rápidas e filtros precisos por serviço, mas dependente do comando `journalctl`).
* **Depuração de Permissões Linux:** A gestão correta de `su`, `sudo` e permissões octais (`chmod`) é fundamental para operar estações analíticas sem corromper as políticas de segurança do sistema operativo.

---

## 🗺️ Evidências da Execução no Terminal

<details open>
  <summary><b>1. Diagnóstico do Erro de Permissões e Alternância de Conta (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Insere aqui o link do upload da Imagem 6 (source: 15) -->
    <img width="750" alt="Evidência 1 - Erro de Permissão e su analyst"src="https://github.com/user-attachments/assets/7bfdf65f-c7e8-48e1-92c7-62abd826b7c6" />
    <p><i>Erro <code>Permission denied</code> sob o utilizador <code>cisco</code> e autenticação na conta <code>analyst</code>.</i></p>
  </div>
</details>

<details open>
  <summary><b>2. Desbloqueio com Chmod, Inserção com Echo e Validação com Tail (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Insere aqui o link do upload da Imagem 1 (source: 10) -->
    <img width="750" alt="Evidência 2 - sudo chmod, echo e tail"  src="https://github.com/user-attachments/assets/e92d32e8-0ba6-4568-9a28-56e135bb8cbf" />
    <p><i>Execução de <code>sudo chmod -R 777</code>, inserção de registo via <code>echo</code> e conferência imediata com <code>tail -n 2</code>.</i></p>
  </div>
</details>

<details open>
  <summary><b>3. Validação do Syslog e Navegação no Journalctl (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Insere aqui o link do upload da Imagem 3 (source: 12) -->
    <img width="750" alt="Evidência 3 - Ausência de syslog.1 e execução do journalctl"  src="https://github.com/user-attachments/assets/2983bca3-6d4d-4f79-9c8f-905894a752be" />
    <p><i>Confirmação de que o sistema migrou a rotação tradicional para o <code>systemd-journald</code>.</i></p>
  </div>
</details>

<details open>
  <summary><b>4. Filtragem Avançada de Logs do Sistema (Boot e Kernel) (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Insere aqui o link do upload da Imagem 4 (source: 13) -->
    <img width="750" alt="Evidência 4 - Saída do journalctl -b"  src="https://github.com/user-attachments/assets/76d1aad8-aa32-44d2-86c5-ef436c196715" />
 />
    <p><i>Registos do ciclo de arranque obtidos através de <code>sudo journalctl -b</code>.</i></p>
  </div>
  <br>
  <div align="center">
    <!-- Insere aqui o link do upload da Imagem 5 (source: 14) -->
    <img width="750" alt="Evidência 5 - Saída do journalctl -k"  src="https://github.com/user-attachments/assets/3d6056d3-b236-4c0f-aafb-ac103a49aeed" />
    <p><i>Mensagens directas do Kernel isoladas através de <code>sudo journalctl -k</code>.</i></p>
  </div>
</details>

---

## 📚 Referência Técnica: Roteiro Oficial do Laboratório (Cisco NetAcad)
> ℹ️ Esta secção resume o guião oficial "Laboratório - Leitura de servidor de logs" e serve como **referência técnica**, não como relato do que foi executado.

<details>
  <summary><b>📋 Resumo do Roteiro Oficial (Clique para expandir)</b></summary>
  <br>
  <ul>
    <li><b>Parte 1:</b> Abertura do ficheiro <code>logstash-tutorial.log</code> com <code>cat</code>, <code>more</code>, <code>less</code> e monitorização via <code>tail -f</code>.</li>
    <li><b>Parte 2:</b> Análise de centralização de registos com <code>syslog</code>, necessidade de permissões administrativas e políticas de rotação de ficheiros.</li>
    <li><b>Parte 3:</b> Utilização do utilitário <code>journalctl</code> e parâmetros avançados de filtragem (<code>-b</code>, <code>-k</code>, <code>-u</code>, <code>--since</code>).</li>
  </ul>
</details>
---




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
