<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Monitoramento%20e%20Recursos%20do%20Windows&fontSize=34&fontColor=FFFFFF&fontAlignY=35&desc=Monitor%20de%20Desempenho%2C%20Servi%C3%A7os%20e%20Logs%20de%20Eventos&descAlignY=55&descSize=15&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Windows_11-161B22?style=for-the-badge&logo=windows11&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Cisco_NetAcad-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Suporte_TI-161B22?style=for-the-badge&logo=windows&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Investigação_SOC-161B22?style=for-the-badge&logo=shield&logoColor=58A6FF" />

</div>

<br>

## 🎯 O que este laboratório resolve na prática

Quando um computador fica lento ou há suspeita de invasão, a equipe técnica precisa saber o que está rodando e quem alterou o sistema. Esse laboratório reúne três ferramentas nativas essenciais do Windows:

* **Monitor de Desempenho (`perfmon`):** mostra em tempo real, em formato de gráfico, o esforço do processador.
* **Serviços (`services.msc`):** lista e controla programas que rodam em segundo plano sem janela aberta.
* **Visualizador de Eventos (`eventvwr.msc`):** registra o histórico com data e hora exatas de cada alteração relevante no sistema.

Para testar na prática, ativei o serviço **Roteamento e Acesso Remoto**, acompanhei o impacto no gráfico de CPU e confirmei o registro oficial da ação nos logs do sistema.

---

## 🧭 Desafios Reais no Windows 11 e Soluções

Durante o teste, a interface do Windows 11 apresentou diferenças em relação ao roteiro padrão da Cisco, exigindo soluções rápidas:

* **Navegação longa no Painel de Controle:** ficar caçando pastas manuais consome tempo desnecessário. Resolvi usando o atalho **Windows + R** com comandos diretos:
  * `ncpa.cpl` para abrir direto a tela de placas de rede.
  * `services.msc` para o gerenciador de serviços.
  * `perfmon` para o Monitor de Desempenho.
  * `eventvwr.msc` para o Visualizador de Eventos.
* **Botão "Limpar" ausente no gráfico:** a opção de limpar pelo botão direito não existe mais nessa versão. Usei os controles da barra superior: pausei a leitura e usei o botão com **X vermelho** para zerar os contadores.
* **Estrutura de pastas no Visualizador de Eventos:** a categoria de Sistema fica oculta dentro de vários menus colapsados. O caminho correto foi expandir **Logs do Windows** e selecionar a subpasta **Sistema** para encontrar os registros.

---

## 🔎 Passo a Passo da Execução

<details open>
  <summary><b>1. Checagem das Placas de Rede (Clique para recolher)</b></summary>
  <br>
  Abri as conexões com <code>ncpa.cpl</code> para conferir os adaptadores locais e validar se o sistema criaria alguma interface nova ao ligar o acesso remoto.
</details>

<details open>
  <summary><b>2. Monitoramento e Ativação do Serviço (Clique para recolher)</b></summary>
  <br>
  Com o gráfico do Monitor de Desempenho rodando, fui em <code>services.msc</code>, mudei o serviço <b>Roteamento e Acesso Remoto</b> para <b>Manual</b> e cliquei em <b>Iniciar</b>. No mesmo instante, a linha de uso do processador deu um pico no gráfico, comprovando o impacto do serviço subindo.
</details>

<details open>
  <summary><b>3. Desativação Preventiva (Clique para recolher)</b></summary>
  <br>
  Finalizado o teste, cliquei em <b>Parar</b> e voltei a inicialização para <b>Desativado</b>. Manter serviços de conexão externa desligados quando não estão em uso é uma boa prática básica de segurança para fechar portas desnecessárias.
</details>

<details open>
  <summary><b>4. Auditoria no Visualizador de Eventos (Clique para recolher)</b></summary>
  <br>
  Acessei <code>Logs do Windows > Sistema</code> e localizei os eventos com origem em <b>Service Control Manager</b>. Eles comprovam exatamente o momento em que o serviço iniciou e quando foi finalizado.
</details>

---

## 💡 O Que Aprendi na Prática

* **Rastreabilidade total:** qualquer serviço iniciado ou finalizado gera um log com hora e data no Windows.
* **Agilidade com atalhos:** usar comandos diretos no Executar é muito mais rápido e profissional do que procurar menus no Painel de Controle.
* **Segurança na prática:** recursos de acesso remoto nunca devem ficar ligados sem necessidade.

---

## 📸 Evidências do Laboratório

<details open>
  <summary><b>1. Central de Rede e Compartilhamento (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Arquivo: Captura de tela 2026-10-01 003941.png -->
    <img width="650" alt="Captura de tela 2026-10-01 003941.png" src="https://github.com/user-attachments/assets/3228a41f-0463-4304-a268-c3635be37783" />
    <p><i>Verificação inicial das conexões de rede ativas.</i></p>
  </div>
</details>

<details open>
  <summary><b>2. Adaptadores de Rede via ncpa.cpl (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Arquivo: Captura de tela 2026-10-01 004203.png -->
    <img width="650" alt="Captura de tela 2026-10-01 004203.png" src="https://github.com/user-attachments/assets/d93b0fdc-ee7c-407d-81ad-3832e9830011" />
    <p><i> Tela de placas de rede aberta pelo comando rápido.</i></p>
  </div>
</details>

<details open>
  <summary><b>3. Ferramentas do Sistema (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Arquivo: Captura de tela 2026-10-01 004252.png -->
    <img width="650" alt="Captura de tela 2026-10-01 004252.png" src="https://github.com/user-attachments/assets/380c1dc1-540a-42bc-94d0-128c212c9434" />
    <p><i>AAtalhos administrativos nativos do Windows.</i></p>
  </div>
</details>

<details open>
  <summary><b>4. Gráfico do Monitor de Desempenho (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Arquivo: image_79e68e.png -->
    <img width="650" alt="image_79e68e.png"  src="https://github.com/user-attachments/assets/832af104-18bc-463f-9e9e-95b1a64829f7" />
    <p><i>Linha vermelha mostrando a oscilação do processador durante o teste do serviço.</i></p>
  </div>
</details>

---

## 📚 Roteiro Oficial da Cisco (NetAcad)

<details>
  <summary><b>📋 Conteúdo Oficial do Laboratório (Clique para expandir)</b></summary>
  <br>
  <ul>
    <li><b>Parte 1:</b> Inicialização e parada do serviço de Roteamento e Acesso Remoto com observação do impacto no Monitor de Desempenho.</li>
    <li><b>Parte 2:</b> Auditoria de logs do sistema via Gerenciamento do Computador e Visualizador de Eventos.</li>
    <li><b>Parte 3:</b> Configuração e acompanhamento de ferramentas administrativas do sistema operacional.</li>
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
