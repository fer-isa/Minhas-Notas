<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=An%C3%A1lise%20de%20Logs%20no%20Linux&fontSize=42&fontColor=FFFFFF&fontAlignY=35&desc=Auditoria%20do%20Syslog%2C%20Journalctl%20e%20Monitoramento%20em%20Tempo%20Real%20%7C%20SOC%20Analyst&descAlignY=55&descSize=16&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Linux-161B22?style=for-the-badge&logo=linux&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Cisco_NetAcad-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Syslog_Audit-161B22?style=for-the-badge&logo=gnubash&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Journalctl-161B22?style=for-the-badge&logo=redhat&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/SOC_Fundamentals-161B22?style=for-the-badge&logo=shield&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo
Compreender a estrutura, os métodos de inspeção e a monitorização operacional de ficheiros de registo (*logs*) em ambientes Linux orientados a operações de Segurança da Informação. O laboratório abrange o manuseamento de utilitários clássicos de linha de comando (`cat`, `more`, `less`, `tail`), a compreensão do ciclo de rotação do serviço `syslog` e a filtragem granular de eventos indexados no subsistema `systemd-journald` através do utilitário `journalctl`.

> **🛡️ Visão de Segurança (SOC):**  
> Ficheiros de registo constituem a principal fonte de evidências para análise forense, deteção de anomalias e resposta a incidentes. A habilidade de realizar triagens rápidas sem carregar ficheiros maciços na memória, monitorizar ficheiros em tempo real contra ataques ativos (ex.: tentativas contínuas de autenticação via SSH) e correlacionar eventos temporais com carimbos cronológicos sincronizados (NTP/UTC) é um requisito essencial para analistas de SOC Tier 1 e Tier 2.

---

## 🧯 O Desafio: Sobrecarga Visual em Ficheiros Extensos e Limitações Estruturais

<details open>
  <summary><b>❌ 1. Ineficiência do Despejo Contínuo via cat (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Cenário:</b> Leitura de ficheiros de registos volumosos contendo milhares de linhas operacionais acumuladas.</li>
    <li><b>O problema:</b> A execução de <code>cat</code> despeja todo o fluxo de texto diretamente no terminal sem suporte a paginação ou interrupção. O início do registo perde-se devido ao buffer de rolagem do ecrã, gerando fadiga visual e ocultando vetores iniciais de intrusão.</li>
    <li><b>Resolução prática:</b> Adoção de paginadores interativos (<code>less</code>) para navegação bidirecional e pesquisas por palavras-chave com expressões regulares, reservando o <code>cat</code> apenas para inspeção rápida de ficheiros curtos de configuração.</li>
  </ul>
</details>

<details open>
  <summary><b>🛠️ 2. Restrições de Privilégios e Formato Binário do Journald (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Controlo de Acesso ao Syslog:</b> O diretório <code>/var/log</code> e ficheiros críticos de auditoria pertencem exclusivamente ao utilizador <code>root</code> para impedir que agentes não autorizados apaguem rastros de atividade ilícita, exigindo privilégios elevados via <code>sudo</code>.</li>
    <li><b>Leitura de Registos Binários:</b> Diferente do Syslog (texto plano desestruturado), os registos do <code>journald</code> são armazenados em formato binário indexado. A extração exige o uso do <code>journalctl</code>, que viabiliza filtros avançados por serviço, mensagens exclusivas do kernel ou apenas a sessão de inicialização (*boot*) atual.</li>
  </ul>
</details>

---

## 🔎 Execução Prática e Análise Técnica

<details open>
  <summary><b>📄 1. Avaliação Comparativa de Utilitários de Leitura (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>cat:</b> Execução de <code>cat logstash-tutorial.log</code> comprovando a incapacidade de analisar eventos extensos devido ao despejo imediato de todo o conteúdo.</li>
    <li><b>more:</b> Teste de paginação com <code>more</code>, permitindo avanço por ecrã (Barra de Espaço) e linha a linha (Enter), porém evidenciando a limitação estrutural de não permitir retorno suave a páginas anteriores.</li>
    <li><b>less:</b> Validação do utilitário ideal para investigação forense estática. Permite rolagem bidirecional fluida através das setas direcionais, navegação por blocos e busca de termos arbitrários através da sintaxe <code>/termo</code>.</li>
    <li><b>tail:</b> Inspeção dos 10 registos finais com <code>tail logstash-tutorial.log</code> para triagem rápida de ocorrências recentes.</li>
  </ul>
</details>

<details open>
  <summary><b>📡 2. Monitorização em Tempo Real de Eventos Ativos (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Execução em Background:</b> Utilização do parâmetro de rastreamento contínuo no primeiro terminal:</li>
  </ul>
  <pre><code>sudo tail -f /var/log/syslog</code></pre>
  <ul>
    <li><b>Simulação de Incidente:</b> Em um segundo terminal simultâneo, realizou-se a injeção manual de um alerta no subsistema de registo:</li>
  </ul>
  <pre><code>logger "ALERTA SOC: TENTATIVA DE INVASAO DETECTADA!"</code></pre>
  <ul>
    <li><b>Confirmação Operacional:</b> A entrada foi imediatamente projetada na janela de escuta sem necessidade de atualização manual da tela, demonstrando o fluxo aplicado em centrais de monitoramento contra ataques de força bruta ou quebra de serviços.</li>
  </ul>
</details>

<details open>
  <summary><b>📊 3. Inspeção do Syslog e Filtragem Cirúrgica com Journalctl (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Auditoria de Syslog Rotacionado:</b> Inspeção de ficheiros arquivados através de <code>sudo cat /var/log/syslog.1</code>, validando a preservação do histórico operacional após procedimentos automáticos de limpeza e rotação de disco.</li>
    <li><b>Filtros Avançados via journalctl:</b>
      <ul>
        <li><code>journalctl -k</code>: Triagem de anomalias e erros emitidos unicamente pelo kernel.</li>
        <li><code>journalctl -b</code>: Segmentação de registos gerados exclusivamente durante a sessão de arranque ativa.</li>
        <li><code>journalctl -u nginx.service --since today</code>: Consulta direcionada aos eventos de um serviço específico dentro de uma janela temporal definida.</li>
        <li><code>journalctl --utc</code>: Padronização da marcação temporal para o horário universal coordenado, garantindo correlação fidedigna entre diferentes ativos de rede.</li>
      </ul>
    </li>
  </ul>
</details>

---

## 💡 O Que Aprendi na Prática (Conceitos Técnicos)
* **Sincronização Cronológica Obrigatória:** O alinhamento rigoroso de data e hora (via protocolo NTP) em todos os endpoints e servidores é indispensável. Registos com carimbos divergentes inviabilizam a reconstituição da linha do tempo de ataques complexos e a correlação em soluções SIEM.
* **Vigilância Ativa de Ameaças:** O parâmetro `-f` (follow) em comandos de inspeção transforma o terminal numa consola de telemetria em tempo real, permitindo a observação imediata de atividades maliciosas no instante da sua ocorrência.
* **Syslog vs. Journald:** O Syslog destaca-se pela interoperabilidade em rede e formato legível por humanos, enquanto o Journald oferece integridade de dados e indexação de metadados binários que conferem alta velocidade a investigações forenses.

---

## 🗺️ Evidências da Execução no Sistema

<details open>
  <summary><b>1. Limitação Operacional do Despejo de Ficheiros com cat (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 1: 01-leitura-cat.png -->
    <img width="750" alt="01-leitura-cat.png" src="https://github.com/user-attachments/assets/d3b605ef-90d8-43c6-9f2b-b51c7305bda3" />
    <p><i>Execução de <code>cat</code> em ficheiro de log extenso demonstrando a perda de visualização do cabeçalho.</i></p>
  </div>
</details>

<details open>
  <summary><b>2. Paginação Básica e Restrição de Retorno via more (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 2: 02-paginacao-more.png -->
    <img width="750" alt="02-paginacao-more.png" src="https://github.com/user-attachments/assets/3da38ce9-c4d1-45e0-9a31-da2cce3a38a9" />
    <p><i>Pausa de execução do utilitário <code>more</code> apresentando a percentagem de leitura concluída.</i></p>
  </div>
</details>

<details open>
  <summary><b>3. Navegação Interativa e Busca de Evidências com less (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 3: 03-navegacao-less.png -->
    <img width="750" alt="03-navegacao-less.png" src="https://github.com/user-attachments/assets/1d0be4e0-6abc-4aa7-bfef-16360a9bc4ee" />
    <p><i>Exploração bidirecional e indexação de termos no ficheiro de log utilizando a interface limpa do <code>less</code>.</i></p>
  </div>
</details>

<details open>
  <summary><b>4. Monitorização de Fim de Ficheiro com tail e tail -f (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 4: 04-monitorizacao-tail-f.png -->
    <img width="750" alt="04-monitorizacao-tail-f.png"  src="https://github.com/user-attachments/assets/7b069c77-b410-4327-9de4-423dc320a50d" />
    <p><i>Execução contínua do comando <code>tail -f</code> mantendo o terminal em escuta ativa de eventos.</i></p>
  </div>
</details>

<details open>
  <summary><b>5. Simulação e Captura de Incidente em Tempo Real (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 5: image_973089.png -->
    <img width="750" alt="05-evento-tempo-real" src="https://github.com/user-attachments/assets/8d4c84a5-566d-4716-8cad-6e28e7cb0a49" />
    <p><i>Injeção manual de alerta via <code>logger</code> e receção simultânea na janela monitorizada pelo <code>tail -f</code>.</i></p>
  </div>
</details>

<details open>
  <summary><b>6. Análise de Ficheiro Rotacionado e Filtragem com journalctl (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 6: 08-leitura-journalctl.png -->
    <img width="750" alt="08-leitura-journalctl.png" src="https://github.com/user-attachments/assets/805644be-d564-465a-9086-6246c25b8a29" />
    <img width="727" height="490" alt="08-leitura-journalctl-b" src="https://github.com/user-attachments/assets/a9aacd32-dde4-4144-a8ee-92e22255ab8f" />
    <p><i>Utilização do <code>journalctl</code> com parâmetros cirúrgicos para filtragem de eventos de sistema e kernel.</i></p>
  </div>
</details>

---

## 📚 Referência Técnica: Roteiro Oficial do Laboratório (Cisco NetAcad)
> ℹ️ Esta secção resume o guião oficial "Laboratório - Leitura de servidor de logs" e serve como **referência técnica**, não como relato do que foi executado.

<details>
  <summary><b>📋 Resumo do Roteiro Oficial (Clique para expandir)</b></summary>
  <br>
  <ul>
    <li><b>Parte 1: Leitura de Arquivos de Log com Cat, More, Less e Tail:</b> Avaliação das ferramentas padrão de visualização de texto plano, comparação de comportamentos e validação do rastreamento ativo com o parâmetro <code>-f</code>.</li>
    <li><b>Parte 2: Arquivos de log e Syslog:</b> Investigação de registos originados pelo sistema operacional, análise do mecanismo de rotação de ficheiros para conservação de espaço e relevância de sincronização temporal.</li>
    <li><b>Parte 3: Arquivos de log e Journalctl:</b> Operação sobre a infraestrutura binária do <code>journald</code>, aplicação de filtros cronológicos e restrição de escopo operacional de eventos.</li>
  </ul>
</details>

---

## 💬 Questões de Reflexão (Gabarito Técnico Oficial)

**1. Qual é a desvantagem de usar cat com arquivos de texto grandes?**  
> O comando não suporta paginação ou controlo de rolagem. Ao carregar ficheiros extensos, o fluxo de texto passa imediatamente para o final, fazendo com que o analista perca os eventos e cabeçalhos iniciais.

**2. Qual é a desvantagem de usar more?**  
> Embora ofereça quebra de página, a aplicação não permite retroceder confortavelmente para rever linhas e ecrãs que já foram exibidos anteriormente.

**3. O que está diferente na saída de tail e tail -f? Explique.**  
> O comando `tail` comum exibe apenas as últimas 10 linhas e devolve a linha de comandos. Já o `tail -f` mantém o processo aberto em execução contínua, bloqueando o prompt e projetando novas entradas na tela em tempo real no exato momento em que são gravadas.

**4. Por que o comando cat teve que ser executado como root para ler o syslog?**  
> Por motivos de segurança e integridade de auditoria, ficheiros como `/var/log/syslog` possuem permissões restritivas pertencentes ao superutilizador `root`, evitando que utilizadores comuns leiam dados confidenciais ou manipulem rastros operacionais.

**5. Você consegue pensar em um motivo pelo qual é tão importante manter a data e a hora dos computadores corretamente sincronizadas?**  
> Os mecanismos de auditoria dependem de carimbos temporais precisos. Caso os relógios das máquinas estejam dessincronizados, torna-se extremamente difícil correlacionar eventos entre diferentes servidores, identificar a ordem cronológica real de um incidente ou validar evidências forenses.

**6. Compare Syslog e Journald. Quais são as vantagens e desvantagens de cada um?**  
> O Syslog é uma solução tradicional baseada em ficheiros de texto simples, com ampla compatibilidade entre sistemas, mas carece de indexação avançada e depende de processos de rotação para não esgotar o disco. O Journald utiliza uma arquitetura binária integrada ao systemd, permitindo filtragens rápidas por processos, unidades ou horários, embora exija utilitários específicos (como o `journalctl`) para leitura e análise.

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
