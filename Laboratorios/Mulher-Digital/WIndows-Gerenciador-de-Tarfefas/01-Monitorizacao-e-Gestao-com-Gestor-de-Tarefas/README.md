<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Monitoramento%20com%20Gerenciador%20de%20Tarefas&fontSize=34&fontColor=FFFFFF&fontAlignY=35&desc=Processos%2C%20Servi%C3%A7os%2C%20M%C3%A9tricas%20de%20Hardware%20e%20Triagem%20de%20Endpoints&descAlignY=55&descSize=15&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Windows_11-161B22?style=for-the-badge&logo=windows11&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Cisco_NetAcad-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Endpoint_Triage-161B22?style=for-the-badge&logo=target&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Process_Auditing-161B22?style=for-the-badge&logo=speedtest&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/SOC_Fundamentals-161B22?style=for-the-badge&logo=shield&logoColor=58A6FF" />

</div>

<br>

## 🎯 Objetivo e Visão Operacional

Quando um computador apresenta lentidão repentina, instabilidade de sistema ou indícios de infecção após execução de arquivos não autorizados, o **Gerenciador de Tarefas** é a primeira ferramenta nativa acionada para diagnosticar o que está operando nos bastidores do Windows.

Neste laboratório, o foco foi inspecionar o ecossistema do Windows 11 de forma prática e detalhada:
* **Mapeamento de Processos Ativos:** Identificação do consumo em tempo real de cada aplicação sobre o processador (CPU) e memória RAM.
* **Inspeção de Serviços do Sistema:** Auditoria das rotinas que executam em segundo plano sem janela visível, validando quais processos são componentes nativos e quais podem representar comportamento anômalo.
* **Controle e Encerramento Forçado:** Localização de tarefas travadas ou processos suspeitos com finalização imediata para restabelecimento da máquina.
* **Métricas de Desempenho:** Interpretação direta dos gráficos de hardware para distinguir gargalos operacionais normais de vazamentos de memória ou atividade maliciosa.

> **🛡️ Importância na Rotina de SOC e Suporte a Incidentes:**  
> Antes de aplicar ferramentas pesadas de análise forense, a triagem no endpoint requer agilidade. Se um processo oculto consumir volume excessivo de hardware ou utilizar nomes semelhantes aos binários originais do sistema, o Gerenciador de Tarefas permite validar o caminho do executável na pasta protegida `System32`, conferir seu PID e cortar a execução de forma cirúrgica.

---

## 🔎 Análise Técnica e Prática das Etapas

<details open>
  <summary><b>📊 1. Avaliação de Memória e Ordenação de Processos (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Organização por Impacto:</b> Clicando sobre a coluna <i>Memória</i>, a exibição foi invertida para posicionar os maiores consumidores no topo, permitindo isolar gargalos de recursos em segundos.</li>
    <li><b>Leitura Absoluta vs. Percentual:</b> A conversão da unidade de megabytes (MB) para porcentagem (%) forneceu uma leitura direta do peso relativo de cada programa perante o total de memória física instalada no computador.</li>
    <li><b>Validação de Integridade do Binário:</b> Foi localizado e auditado o processo <code>Host da Janela do Console</code> (<code>conhost.exe</code>), verificando que sua origem é o caminho oficial <code>C:\Windows\System32</code>, descartando binários camuflados em diretórios temporários.</li>
  </ul>
</details>

<details open>
  <summary><b>🛑 2. Controle e Encerramento Forçado de Tarefas (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Encerramento Limpo:</b> Por meio do recurso <i>Finalizar tarefa</i>, os ciclos de processamento foram interrompidos e os dados da aplicação descarregados da memória de forma imediata.</li>
    <li><b>Comprovação Prática:</b> O encerramento forçado do processo do <code>Microsoft Edge</code> eliminou simultaneamente todas as instâncias e abas ativas vinculadas ao navegador.</li>
  </ul>
</details>

<details open>
  <summary><b>⚙️ 3. Auditoria de Serviços e Leitura de Hardware (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Estados Operacionais de Serviços:</b> Na aba <i>Serviços</i>, verificou-se a separação operacional entre serviços com status <code>Em execução</code> (rotinas ativas de sistema e terceiros) e <code>Parado</code> (serviços em espera ou sob demanda).</li>
    <li><b>Métricas de Processamento:</b> Na aba <i>Desempenho</i>, realizou-se a leitura da frequência da CPU (GHz), a contagem de threads e processos ativos, além da memória em uso e dados de tráfego de rede.</li>
  </ul>
</details>

---

## 💡 O Que Aprendi na Prática
* **Diferenciação entre Camadas do Sistema:** Aplicativos possuem interface e interação com o usuário; processos em segundo plano oferecem sustentação a essas tarefas; e serviços gerenciam conexões de rede, controles de segurança e rotinas de baixo nível de forma contínua.
* **Identificação de Falsos Processos:** Conhecer os executáveis originais do Windows (como `conhost.exe`, `svchost.exe` e `System`) e seus diretórios autênticos é o primeiro passo para flagrar ameaças que usam nomes parecidos para tentar se esconder de analistas.
* **Diagnóstico Assertivo de Lentidão:** Avaliar memória em porcentagem (%) traz velocidade na hora de responder se uma lentidão decorre de um aplicativo mal programado consumindo memória sem liberar (*memory leak*) ou se a estação simplesmente atingiu a capacidade máxima de hardware.

---

## 🗺️ Evidências da Execução no Sistema

<details open>
  <summary><b>1. Localização e Auditoria do Processo do Sistema (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="650" alt="Evidência 1 - Host da Janela do Console em MB" src="https://github.com/user-attachments/assets/88315bf3-d002-4d0e-a6b8-cecba545ea35" />
    <p><i>Localização do processo <b>Host da Janela do Console</b> (conhost.exe) com consumo exibido em megabytes (MB).</i></p>
  </div>
</details>

<details open>
  <summary><b>2. Ordenação por Memória e Visualização em Porcentagem (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="650" alt="Evidência 2 - Consumo de Memória em Porcentagem" src="https://github.com/user-attachments/assets/133ba6f8-9af2-4417-a11e-097c93cc55dd" />
    <p><i>Ajuste da coluna Memória para exibir valores em porcentagem (%), facilitando a visualização de impacto na máquina.</i></p>
  </div>
</details>

<details open>
  <summary><b>3. Encerramento Forçado de Processos (Finalizar Tarefa) (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="650" alt="Evidência 3 - Finalizar Tarefa no Microsoft Edge" src="https://github.com/user-attachments/assets/81e27661-bb45-4ae0-bbe9-3e21a915075f" />
    <p><i>Interrupção controlada de um aplicativo em execução através do botão <b>Finalizar tarefa</b>.</i></p>
  </div>
</details>

<details open>
  <summary><b>4. Monitoramento de Serviços em Segundo Plano (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="650" alt="Evidência 4 - Aba de Serviços" src="https://github.com/user-attachments/assets/3843f93d-56c4-4bc5-b751-9ece8c10a9c0" />
    <p><i>Auditoria de serviços do sistema identificando os estados operacionais <b>Parado</b> e <b>Em execução</b>.</i></p>
  </div>
</details>

<details open>
  <summary><b>5. Leitura de Métricas de Desempenho do Processador (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="650" alt="Evidência 5 - Desempenho do CPU" src="https://github.com/user-attachments/assets/7afdf65e-aa0d-4a6a-8c08-36d8a36f7eb8" />
    <p><i>Gráfico em tempo real de utilização da CPU, velocidade base, threads e processos ativos na aba Desempenho.</i></p>
  </div>
</details>

---

## 📚 Referência Técnica: Roteiro Oficial do Laboratório (Cisco NetAcad)
> ℹ️ Esta seção resume o roteiro oficial "Laboratório - Gerenciador de Tarefas do Windows" e serve como **referência teórica**, não como relato das ações práticas individuais.

<details>
  <summary><b>📋 Resumo do Roteiro Oficial (Clique para expandir)</b></summary>
  <br>
  <ul>
    <li><b>Parte 1: Trabalhando na guia Processos:</b> Abertura do Prompt de Comando e do navegador, identificação do processo Host da Janela do Console, ordenação por consumo de memória, conversão de unidades para porcentagem e encerramento forçado de programas.</li>
    <li><b>Parte 2: Trabalhando na guia Serviços:</b> Navegação na lista de serviços do Windows para identificação de rotinas em segundo plano e seus estados (Parado e Em execução).</li>
    <li><b>Parte 3: Trabalhando na guia Desempenho:</b> Acompanhamento de gráficos de hardware para medição de CPU, memória física disponível e interfaces de rede ativas.</li>
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
