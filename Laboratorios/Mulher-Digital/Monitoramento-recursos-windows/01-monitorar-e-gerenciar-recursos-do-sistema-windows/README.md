<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Monitoramento%20de%20Recursos%20no%20Windows&fontSize=38&fontColor=FFFFFF&fontAlignY=35&desc=Servi%C3%A7os%20do%20Sistema%2C%20Performance%20Monitor%20e%20Event%20Viewer%20%7C%20Windows%20Admin%20SOC&descAlignY=55&descSize=15&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Windows_11-161B22?style=for-the-badge&logo=windows11&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Cisco_NetAcad-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Performance_Monitor-161B22?style=for-the-badge&logo=databricks&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Event_Viewer-161B22?style=for-the-badge&logo=target&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/SOC_Fundamentals-161B22?style=for-the-badge&logo=shield&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo
Compreender a administração, monitoramento e diagnóstico de recursos no sistema operacional Windows por meio de ferramentas administrativas essenciais: gestão de serviços locais (`services.msc`), análise de impacto de hardware com o Monitor de Desempenho (`perfmon.msc`) e auditoria forense de ocorrências do sistema via Visualizador de Eventos (`eventvwr.msc`).

> **🛡️ Visão de Segurança (SOC):**  
> Em investigação de incidentes e triagem de telemetria em endpoints, o analista de SOC avalia serviços iniciados fora do padrão e correlações no Visualizador de Eventos (como Event ID 7036 e 7040 do *Service Control Manager*). Identificar a transição não autorizada de serviços de rede (ex.: Roteamento e Acesso Remoto) é um indicador crucial de tentativas de persistência, criação de túneis ou movimentação lateral por atores de ameaça.

---

## 🧯 O Desafio: Rastreamento do Impacto de Serviços e Logs de Transição

<details open>
  <summary><b>❌ 1. Dependências e Exposição de Interfaces de Rede (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Cenário:</b> Ativação sob demanda do serviço nativo <code>RemoteAccess</code> (Roteamento e Acesso Remoto).</li>
    <li><b>O problema:</b> Serviços de rede modificam dinamicamente a superfície de ataque e o stack de comunicação da máquina sem que haja notificação visual direta no desktop.</li>
    <li><b>Resolução prática:</b> Inspeção do painel de <b>Conexões de Rede</b>, comprovando a instanciação temporária de adaptadores de recepção (<i>Conexões de Entrada</i>) e seu desaparecimento imediato após a paralisação do serviço.</li>
  </ul>
</details>

<details open>
  <summary><b>🛠️ 2. Auditoria e Telemetria no Registro de Eventos (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li>Alterações de inicialização de serviços deixam rastros imutáveis nos logs de <code>Sistema</code>.</li>
    <li>A análise via <code>eventvwr.msc</code> permitiu validar o ciclo de vida completo: alteração do tipo de inicialização (ID 7040), ativação do serviço (ID 7036), parada do processo (ID 7036) e desativação definitiva de volta ao estado seguro (ID 7040).</li>
  </ul>
</details>

---

## 🔎 Execução Prática e Análise Técnica

<details open>
  <summary><b>⚙️ 1. Controle de Ciclo de Vida do Serviço RemoteAccess (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Configuração Inicial:</b> Transição do tipo de inicialização de <code>Desativado</code> para <code>Manual</code> via console de serviços.</li>
    <li><b>Impacto em Conexões:</b> A inicialização do serviço gera dinamicamente a interface <code>Conexões de Entrada</code> no subsistema de rede.</li>
    <li><b>Finalização e Limpeza:</b> O encerramento do serviço através da interface administrativa revoga imediatamente o adaptador e retorna o status a <code>Parado</code> e tipo <code>Desativado</code>.</li>
  </ul>
</details>

<details open>
  <summary><b>📊 2. Coleta de Métricas no Monitor de Desempenho (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Amostragem em Tempo Real:</b> Monitoramento contínuo da métrica <code>% Tempo do Processador</code> (objeto <i>Informações do Processador</i>, instância <i>_Total</i>).</li>
    <li><b>Captura do Pico de Execução:</b> Identificação clara do consumo de CPU gerado durante a inicialização e encerramento de processos em background.</li>
    <li><b>Conjunto de Coletores de Dados:</b> Criação de coletor personalizado para métricas de memória física (<i>MBytes Disponíveis</i>) com gravação estruturada em formato CSV (<code>DataCollector01.csv</code>) no diretório <code>C:\PerfLogs</code>.</li>
  </ul>
</details>

<details open>
  <summary><b>🔍 3. Auditoria Forense no Visualizador de Eventos (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Rastreamento de Trilha de Auditoria:</b> Navegação em <i>Logs do Windows > Sistema</i> filtrando pela fonte <code>Service Control Manager</code>.</li>
    <li><b>Validação dos Event IDs:</b>
      <ul>
        <li><b>Event ID 7040:</b> Registro da mudança de inicialização de desativado para iniciar demanda.</li>
        <li><b>Event ID 7036:</b> Transição de estado operacional para "em execução".</li>
        <li><b>Event ID 7036:</b> Notificação de parada do serviço.</li>
        <li><b>Event ID 7040:</b> Reversão final do serviço para estado desativado.</li>
      </ul>
    </li>
  </ul>
</details>

---

## 💡 O Que Aprendi na Prática (Conceitos Técnicos)
* **Auditoria de Serviços como Vetor de Ameaça:** Serviços locais desnecessários ou configurados como automáticos ampliam a superfície de ataque. O monitoramento contínuo via Event Log permite correlacionar comandos maliciosos executados para levantar portas e túneis remotos.
* **Mapeamento de Linha de Base (Baseline) de Hardware:** Utilizar o Monitor de Desempenho e coletores de dados automatizados em CSV permite estabelecer métricas de normalidade (CPU, memória e disco), viabilizando a identificação de comportamentos anômalos (como criptomineração ou exfiltração massiva).
* **Estruturação de Logs do Windows:** Compreender a taxonomia dos logs (`Sistema`, `Aplicativo`, `Segurança`) e a correlação entre provedores e IDs de eventos acelera investigações de triagem em incidentes corporativos.

---

## 🗺️ Evidências da Execução no Sistema

<details open>
  <summary><b>1. Estado Inicial dos Adaptadores de Rede (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="750" alt="Evidência 1 - Conexões de Rede Antes do Serviço"  src="https://github.com/user-attachments/assets/2de36c25-2b61-43d7-9322-dbba04183478" />
    <p><i>Janela Conexões de Rede antes da inicialização do serviço RemoteAccess, exibindo apenas adaptadores convencionais.</i></p>
  </div>
</details>

<details open>
  <summary><b>2. Instanciação Dinâmica de Interface de Entrada (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="750" alt="Evidência 2 - Conexões de Entrada Criadas"  src="https://github.com/user-attachments/assets/91e66b40-283a-428e-bf7e-31d5abe00749" />
    <p><i>Surgimento da interface <b>Conexões de Entrada</b> imediatamente após a inicialização do serviço de Roteamento e Acesso Remoto.</i></p>
  </div>
</details>

<details open>
  <summary><b>3. Interrupção Controlada do Serviço (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="750" alt="Evidência 3 - Parando Serviço RemoteAccess"  src="https://github.com/user-attachments/assets/7f714367-d5d8-444e-9e05-07c21b057c26" />
    <p><i>Execução da parada do serviço no console de gerenciamento do Windows.</i></p>
  </div>
</details>

<details open>
  <summary><b>4. Validação de Propriedades e Estado Parado/Desativado (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="500" alt="Evidência 4 - Propriedades do Serviço Desativado"  src="https://github.com/user-attachments/assets/a7fccf20-30ae-488e-a67e-aee4b00f8356" />
    <p><i>Configuração do serviço <b>RemoteAccess</b> revertida para Tipo de Inicialização: <b>Desativado</b> e Status: <b>Parado</b>.</i></p>
  </div>
</details>

<details open>
  <summary><b>5. Telemetria no Monitor de Desempenho (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="750" alt="Evidência 5 - Gráfico de Utilização de CPU" src="https://github.com/user-attachments/assets/5b11b9fd-89dc-415f-864d-e2d9568f95f1" />
    <p><i>Monitoramento da métrica <b>% Tempo do Processador</b> registrando o pico de utilização associado às operações do sistema.</i></p>
  </div>
</details>

<details open>
  <summary><b>6. Auditoria de Eventos do Sistema no Event Viewer (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="750" alt="Evidência 6 - Lista de Eventos no Log de Sistema"   src="https://github.com/user-attachments/assets/a21668c8-771d-4510-a69a-5c690e41f90a" />
    <p><i>Listagem dos eventos gerados pelo <b>Service Control Manager</b> no log de Sistema.</i></p>
  </div>
</details>

<details open>
  <summary><b>7. Detalhamento Forense da Transição de Inicialização (ID 7040) (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="600" alt="Evidência 7 - Detalhe Event ID 7040"/>
    <p><i>Propriedades do <b>Evento 7040</b> comprovando o registro de alteração no tipo de inicialização do serviço RemoteAccess.</i></p>
  </div>
</details>

---

## 📚 Referência Técnica: Roteiro Oficial do Laboratório (Cisco NetAcad)
> ℹ️ Esta secção resume o guião oficial "Laboratório - Monitorar e gerenciar recursos do sistema no Windows" e serve como **referência técnica**, não como relato do que foi executado.

<details>
  <summary><b>📋 Resumo do Roteiro Oficial (Clique para expandir)</b></summary>
  <br>
  <ul>
    <li><b>Parte 1: Iniciando e interrompendo o serviço de roteamento e acesso remoto:</b> Configuração do serviço, verificação de interfaces de rede ativas e rastreamento de uso de CPU no Monitor de Desempenho.</li>
    <li><b>Parte 2: Trabalhando no Utilitário de Gerenciamento do Computador:</b> Navegação na árvore do console e análise detalhada dos 4 eventos de transição registrados no Visualizador de Eventos.</li>
    <li><b>Parte 3: Configurando Ferramentas Administrativas:</b> Criação de Coletor de Dados personalizado para registro em CSV de MBytes disponíveis de memória e auditoria do arquivo resultante.</li>
  </ul>
</details>

---

## 💬 Questões de Reflexão e Análise (Gabarito Técnico Oficial)

**1. Que alterações aparecem na janela Conexões de Rede depois de iniciar o serviço Roteamento e Acesso Remoto?**  
> Surge um novo adaptador/conexão denominado **Conexões de Entrada** (*Incoming Connections*).

**2. Quais alterações aparecem após o serviço ser interrompido?**  
> O adaptador **Conexões de Entrada** é removido da janela, retornando apenas as interfaces normais de rede do host.

**3. Qual contador é registrado no gráfico do Monitor de Desempenho e quais valores são exibidos?**  
> O contador é **% Tempo do Processador** (instância `_Total`). São exibidos os valores estatísticos de *Último*, *Médio*, *Mínimo* e *Máximo* de utilização da CPU.

**4. Quais são as descrições dos quatro eventos registrados no Visualizador de Eventos para o serviço?**  
> 1. *O tipo de inicialização do serviço Roteamento e Acesso Remoto foi alterado de desativado para iniciar demanda.* (Evento 7040)  
> 2. *O serviço Roteamento e Acesso Remoto entrou no estado em execução.* (Evento 7036)  
> 3. *O serviço Roteamento e Acesso Remoto entrou no estado parado.* (Evento 7036)  
> 4. *O tipo de inicialização do serviço Roteamento e Acesso Remoto foi alterado de iniciar demanda para desativado.* (Evento 7040)

**5. Qual é o caminho completo do arquivo de log criado pelo Coletor de Dados de Memória e o que é exibido em sua coluna mais à direita?**  
> O caminho é `C:\PerfLogs\Logs de Memória\DataCollector01.csv`. A coluna mais à direita armazena as amostragens periódicas de **MBytes Disponíveis** de memória RAM livre ao longo do teste.

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
