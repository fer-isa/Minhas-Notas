<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Arquivos%20de%20Texto%20na%20CLI%20Linux&fontSize=40&fontColor=FFFFFF&fontAlignY=35&desc=Editores%20CLI%2C%20Vari%C3%A1veis%20de%20Ambiente%20e%20Configura%C3%A7%C3%A3o%20de%20Servi%C3%A7os%20%7C%20Linux%20Admin%20SOC&descAlignY=55&descSize=15&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Linux_LabVM-161B22?style=for-the-badge&logo=linux&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Cisco_NetAcad-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/GNU_nano-161B22?style=for-the-badge&logo=gnubash&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/NGINX-161B22?style=for-the-badge&logo=nginx&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/SOC_Fundamentals-161B22?style=for-the-badge&logo=shield&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo
Dominar a manipulação de arquivos de texto e arquivos de configuração no ambiente Linux via terminal (CLI) e interface gráfica (GUI). O laboratório exercita o uso de editores de texto essenciais para administração e investigação forense (`nano` e `scite`), a personalização de variáveis de ambiente do usuário (`.bashrc`) e a reconfiguração segura de serviços corporativos em `/etc` com privilégios administrativos delegados (`sudo`).

> **🛡️ Visão de Segurança (SOC):**  
> No Linux, o paradigma operacional fundamental é: *"Tudo é um arquivo"*. Praticamente todos os serviços (da pilha de rede a regras de firewalls e daemons web) são controlados exclusivamente por arquivos de texto simples. Um analista de segurança precisa ser capaz de auditar configurações, inspecionar scripts e analisar arquivos remotos via SSH sem depender de interfaces gráficas.

---

## 🧯 O Desafio: Administração Remota sem GUI e Gestão de Privilégios

<details open>
  <summary><b>❌ 1. Dependência de Interface Gráfica em Servidores Headless (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Cenário:</b> Aplicações como o SciTE exigem servidor X / interface gráfica ativa e bloqueiam o terminal ao rodar em primeiro plano.</li>
    <li><b>O problema:</b> Em servidores de produção e estações de resposta a incidentes acessadas via SSH, não há ambiente de janelas disponível.</li>
    <li><b>Resolução prática:</b> Domínio do editor de texto baseado em console <code>GNU nano</code>, operado integralmente via atalhos de teclado (<code>Ctrl+O</code>, <code>Ctrl+W</code>, <code>Ctrl+X</code>), permitindo manutenção crítica sob qualquer conexão de rede.</li>
  </ul>
</details>

<details open>
  <summary><b>🛠️ 2. Segregação de Diretórios de Configuração (/home vs. /etc) (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li>Arquivos de configuração do usuário residem ocultos no diretório pessoal (ex.: <code>~/.bashrc</code>) e não requerem privilégios elevados.</li>
    <li>Arquivos de configuração de serviços de rede globais residem sob <code>/etc</code> (ex.: <code>/etc/nginx/custom_server.conf</code>), exigindo elevação mandatória via <code>sudo</code> para evitar alterações indevidas ou não autorizadas no sistema.</li>
  </ul>
</details>

---

## 🔎 Execução Prática e Análise Técnica

<details open>
  <summary><b>📝 1. Manipulação com SciTE e GNU nano (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Criação de Documento:</b> Criação e manipulação do arquivo <code>space.txt</code> via redirecionamento de stream e abertura nos editores de texto.</li>
    <li><b>Comportamento em Primeiro Plano:</b> Ao invocar <code>scite space.txt</code> diretamente no terminal sem o operador de background (<code>&</code>), o prompt fica retido até que a aplicação gráfica seja finalizada.</li>
    <li><b>Inspeção via nano:</b> Validação do indicador de quebra de linha visual representada pelo caractere <code>$</code> quando linhas longas ultrapassam as dimensões horizontais da janela do console.</li>
  </ul>
</details>

<details open>
  <summary><b>🎨 2. Auditoria e Customização do Shell via .bashrc (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Mapeamento de Arquivos Ocultos:</b> Uso de <code>ls -la</code> para auditar dotfiles (arquivos iniciados por ponto) no diretório <code>/home/cisco</code>.</li>
    <li><b>Customização do Prompt (PS1):</b> Edição da variável de ambiente no <code>.bashrc</code>, alterando a sequência ANSI de controle de cores de <code>32m</code> (verde) para <code>31m</code> (vermelho).</li>
    <li><b>Persistência de Sessão:</b> Validação técnica de que sessões já abertas não herdam modificações automaticamente até que o arquivo seja relido com um novo shell <code>bash</code> ou comando <code>source</code>.</li>
  </ul>
</details>

<details open>
  <summary><b>🌐 3. Reconfiguração do Servidor Web NGINX com sudo (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Elevação de Privilégios:</b> Edição com numeração de linha ativada em arquivo restrito do sistema:</li>
  </ul>
  <pre><code>sudo nano -l /etc/nginx/custom_server.conf</code></pre>
  <ul>
    <li><b>Parâmetros Modificados:</b>
      <ul>
        <li>Porta de escuta na linha 39: alterada de <code>listen 81;</code> para <code>listen 8080;</code>.</li>
        <li>DocumentRoot na linha 47: apontado para <code>/usr/share/nginx/html/text_ed_lab/;</code>.</li>
      </ul>
    </li>
    <li><b>Execução e Teste:</b> Inicialização do serviço chamando o arquivo customizado:</li>
  </ul>
  <pre><code>sudo nginx -c custom_server.conf</code></pre>
  <ul>
    <li><b>Validação de Acesso:</b> Conexão local no navegador em <code>http://127.0.0.1:8080</code> com carregamento bem-sucedido da página do laboratório.</li>
    <li><b>Encerramento de Processo:</b> Finalização do daemon com <code>sudo pkill nginx</code> e validação da indisponibilidade da porta.</li>
  </ul>
</details>

---

## 💡 O Que Aprendi na Prática (Conceitos Técnicos)
* **Arquivos de Configuração como Base do Sistema:** Entender que o comportamento de daemons, servidores web e ferramentas de análise no Linux depende unicamente da leitura de arquivos de texto torna a depuração e o hardening muito mais diretos e auditáveis.
* **Agilidade com Editores CLI:** O domínio do `nano` e a compreensão de atalhos e numeração de linhas aceleram a modificação de arquivos de regras (como Snort, Suricata e iptables) em cenários de resposta a incidentes.
* **Segregação de Permissões e Segurança de Arquivos:** Manter configurações de sistema restritas a `/etc` e sob posse do usuário `root` protege os serviços contra modificações acidentais ou maliciosas executadas por contas não privilegiadas.

---

## 🗺️ Evidências da Execução no Sistema

<details open>
  <summary><b>1. Validação de Binários e Abertura em Background do SciTE (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="600" alt="Evidência 1 - Verificação do SciTE e Usuário cisco"<img width="552" height="530" src="https://github.com/user-attachments/assets/c11d77bd-ef57-4c1b-8e25-471776189217" />
    <p><i>Execução de <code>which scite</code>, lançamento em background e conferência do usuário <code>cisco</code> e diretório <code>/home/cisco</code>.</i></p>
  </div>
</details>

<details open>
  <summary><b>2. Edição de Linha de Comando com GNU nano (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="700" alt="Evidência 2 - Edição no GNU nano"  src="https://github.com/user-attachments/assets/d1280468-fd08-4fa2-8e9a-3032384a2a83" />
    <p><i>Documento <code>space.txt</code> aberto no editor <b>GNU nano 6.2</b> demonstrando os comandos de controle pelo teclado no rodapé.</i></p>
  </div>
</details>

<details open>
  <summary><b>3. Auditoria de Arquivos Ocultos no Diretório Home (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="750" alt="Evidência 3 - Listagem ls -la" src="https://github.com/user-attachments/assets/eb7e01d9-9df4-4599-849c-35d5d68932d1" />
    <p><i>Listagem completa com <code>ls -la</code> revelando arquivos de configuração ocultos como o <code>.bashrc</code> e o arquivo <code>space.txt</code>.</i></p>
  </div>
</details>

<details open>
  <summary><b>4. Customização da Variável de Prompt PS1 (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="750" alt="Evidência 4 - Configuração do PS1 no nano"  src="https://github.com/user-attachments/assets/757ecc75-46c4-41a5-912a-82ad3244e9bf" />
    <p><i>Edição do arquivo <code>.bashrc</code> inserindo a string de formatação com código de cor ANSI para vermelho (<code>31m</code>).</i></p>
  </div>
</details>

<details open>
  <summary><b>5. Recarregamento do Shell e Validação do Prompt Vermelho (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="500" alt="Evidência 5 - Prompt com Cor Alterada"  src="https://github.com/user-attachments/assets/3d032ba3-c5f2-47fd-b021-9d2e76b8b81f" />
    <p><i>Invocação do comando <code>bash</code> carregando a nova sessão com o prompt colorido em vermelho.</i></p>
  </div>
</details>

<details open>
  <summary><b>6. Configuração Administrativa do NGINX (/etc/nginx) (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="750" alt="Evidência 6 - Edição do custom_server.conf"  src="https://github.com/user-attachments/assets/49bc2951-8145-4c5f-9b6a-5459c2d28892" />
    <p><i>Ajuste da porta <code>listen 8080;</code> e DocumentRoot <code>/usr/share/nginx/html/text_ed_lab/;</code> no nano com numeração de linha.</i></p>
  </div>
</details>

<details open>
  <summary><b>7. Inicialização e Teste do Serviço Web no Firefox (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="750" alt="Evidência 7 - Página do NGINX em 127.0.0.1:8080"  src="https://github.com/user-attachments/assets/f97dd7ab-bad4-4f13-8dc8-2ea368593433" />
    <p><i>Carregamento com sucesso da página de confirmação no navegador através de <code>http://127.0.0.1:8080</code>.</i></p>
  </div>
</details>

<details open>
  <summary><b>8. Trilha de Execução e Encerramento com pkill (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <img width="750" alt="Evidência 8 - Finalização com pkill nginx" src="https://github.com/user-attachments/assets/8c7c162e-f908-443e-aeb7-865cc8454c02" />
    <p><i>Inicialização do daemon via <code>sudo nginx -c</code> e parada controlada do processo com <code>sudo pkill nginx</code>.</i></p>
  </div>
</details>

---

## 📚 Referência Técnica: Roteiro Oficial do Laboratório (Cisco NetAcad)
> ℹ️ Esta secção resume o guião oficial "Laboratório - Trabalhando com arquivos de texto na CLI" e serve como **referência técnica**, não como relato do que foi executado.

<details>
  <summary><b>📋 Resumo do Roteiro Oficial (Clique para expandir)</b></summary>
  <br>
  <ul>
    <li><b>Parte 1: Editores Gráficos de Texto:</b> Uso do SciTE via interface e terminal, comportamento de processos em primeiro plano e filtros de extensões.</li>
    <li><b>Parte 2: Editores de texto de linha de comando:</b> Navegação, salvamento e fechamento de arquivos no GNU nano através de comandos de teclado.</li>
    <li><b>Parte 3: Trabalhando com Arquivos de Configuração:</b> Localização de arquivos de usuário (`~/.bashrc`) e de sistema (`/etc/nginx`), modificação de variáveis de ambiente e subida de serviço web em porta customizada.</li>
  </ul>
</details>

---

## 💬 Questões de Reflexão e Análise (Gabarito Técnico Oficial)

**1. Você poderia encontrar imediatamente o arquivo space.txt na janela Abrir Arquivo do SciTE?**  
> Não, pois por padrão o SciTE aplica um filtro de exibição apenas para extensões de arquivos conhecidas de código-fonte, ocultando arquivos `.txt` até que o seletor seja alterado para "Todos os arquivos (*)".

**2. Por que o prompt de comando não é exibido no terminal ao iniciar o SciTE?**  
> Porque a aplicação foi executada em primeiro plano (*foreground*). O terminal bloqueia seu próprio fluxo de entrada aguardando a conclusão do processo filho antes de devolver o cursor ao usuário.

**3. Que caractere o nano utiliza para representar que uma linha continua além dos limites horizontais da tela?**  
> O caractere de cifrão (`$`) exibido na margem direita da janela.

**4. Por que arquivos de configuração de usuário ficam no diretório home e os de sistema sob /etc?**  
> Por segregação de privilégios e segurança. O usuário comum só tem permissão de escrita dentro de seu próprio diretório (`/home/usuario`), impedindo que altere configurações de outros usuários ou desconfigure serviços globais essenciais da máquina que exigem privilégios de `root` sob `/etc`.

**5. A janela do terminal que já estava aberta mudou de cor automaticamente após alterar o .bashrc?**  
> Não. O arquivo `.bashrc` só é processado durante a inicialização de uma nova instância de shell. A sessão aberta mantém o ambiente carregado em memória até que seja reiniciada ou recarregada com `source ~/.bashrc` ou executando `bash`.

**6. Como editar o arquivo /etc/nginx/custom_server.conf utilizando o SciTE?**  
> Executando o SciTE com privilégios de superusuário através do terminal com o comando `sudo scite /etc/nginx/custom_server.conf`, informando a senha administrativa para que a interface gráfica tenha permissão de gravar alterações no diretório `/etc`.

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
