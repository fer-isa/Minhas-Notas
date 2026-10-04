<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Gest%C3%A3o%20de%20Contas%20e%20Permiss%C3%B5es&fontSize=42&fontColor=FFFFFF&fontAlignY=35&desc=Contas%20Locais%2C%20Grupos%20de%20Seguran%C3%A7a%20e%20Auditoria%20NTFS%20%7C%20Windows%20Admin%20SOC&descAlignY=55&descSize=16&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Windows_11-161B22?style=for-the-badge&logo=windows11&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Cisco_NetAcad-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Access_Control-161B22?style=for-the-badge&logo=auth0&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Windows_CLI-161B22?style=for-the-badge&logo=gnubash&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/SOC_Fundamentals-161B22?style=for-the-badge&logo=shield&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo
Compreender os mecanismos fundamentais de controle de acesso, criação de contas locais, herança de permissões no sistema de arquivos NTFS e gerenciamento de grupos de segurança no sistema operacional Windows. O laboratório aborda a transição de privilégios entre usuário padrão e administrativo, além do gerenciamento tanto via interface gráfica quanto via linha de comando (`net user` e `net localgroup`).

> **🛡️ Visão de Segurança (SOC):**  
> O Princípio do Menor Privilégio (*Principle of Least Privilege - PoLP*) determina que nenhum usuário ou processo deve operar com direitos administrativos de forma contínua. Contas padrão mitigam o impacto de malwares e tentativas de movimentação lateral, impedindo que executáveis maliciosos alterem arquivos de sistema, instalem drivers ou comprometam outros perfis da estação de trabalho sem uma elevação explícita de privilégios (UAC).

---

## 🧯 O Desafio: Restrições de Snap-in no Windows Home e Alternativas Administrativas

<details open>
  <summary><b>❌ 1. Limitação do Utilitário lusrmgr.msc (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Cenário:</b> Tentativa de acesso à gestão granular de contas através do snap-in do console de gerenciamento <code>lusrmgr.msc</code> (Usuários e Grupos Locais).</li>
    <li><b>O problema:</b> No Windows 11 Home Edition, este snap-in é bloqueado nativamente pelo sistema operacional, impedindo o fluxo visual convencional de alteração de grupos.</li>
    <li><b>Resolução prática:</b> Utilização coordenada da ferramenta <code>netplwiz</code> (Contas de Usuário) para ajustes via GUI e domínio das ferramentas nativas de CLI administrativa (<code>net.exe</code>), essenciais para scripts de resposta a incidentes e automação de suporte.</li>
  </ul>
</details>

<details open>
  <summary><b>🛠️ 2. Ciclo de Vida da Pasta de Perfil no Disco (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li>A simples criação da conta no banco de dados SAM não instancia de imediato a estrutura de diretórios em <code>C:\Users</code>.</li>
    <li>A inicialização do perfil exigiu um primeiro logon do novo usuário no sistema operacional para que o subsistema do Windows gerasse as chaves de registro do usuário (<code>NTUSER.DAT</code>) e as ACLs (Listas de Controle de Acesso) exclusivas de sua pasta pessoal.</li>
  </ul>
</details>

---

## 🔎 Execução Prática e Análise Técnica

<details open>
  <summary><b>👤 1. Criação e Isolamento de Diretórios de Perfil (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Criação de Conta Local:</b> Configuração do usuário <code>Usuário1</code> desvinculado de conta Microsoft, estabelecendo um identificador local com privilégios restritos.</li>
    <li><b>Isolamento de Diretórios NTFS:</b> Ao auditar a pasta <code>C:\Users\Usuário1</code>, o sistema de arquivos bloqueia o acesso direto sem elevação prévia. As permissões de <b>Controle Total</b> são delegadas exclusivamente a:
      <ul>
        <li><code>SISTEMA</code> (Kernel/Serviços essenciais do SO)</li>
        <li><code>Administradores</code> (Grupo de gerenciamento da máquina)</li>
        <li><code>Usuário1</code> (Proprietário legítimo do perfil)</li>
      </ul>
    </li>
  </ul>
</details>

<details open>
  <summary><b>🛡️ 2. Auditoria e Elevação de Privilégios (GUI e CLI) (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Associação Inicial:</b> Identificação do usuário no grupo restrito <code>*Usuários</code>.</li>
    <li><b>Promoção de Privilégio:</b> Elevação da conta ao grupo <code>*Administradores</code> tanto através da aba de propriedades do <code>netplwiz</code> quanto via instrução direta no terminal elevado:</li>
  </ul>
  <pre><code>net localgroup Administradores Usuário1 /add</code></pre>
  <ul>
    <li><b>Auditoria Detalhada de Contas:</b> Execução de <code>net user Usuário1</code> para inspecionar parâmetros de segurança, incluindo expiração de senha, bloqueio de conta, scripts de logon atribuídos e associações de grupo ativas.</li>
  </ul>
</details>

<details open>
  <summary><b>🧹 3. Revogação de Acesso e Higienização do Host (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Despromoção de Privilégios:</b> Remoção da conta do grupo administrativo respeitando a segregação de funções:</li>
  </ul>
  <pre><code>net localgroup Administradores Usuário1 /delete</code></pre>
  <ul>
    <li><b>Eliminação Definitiva:</b> Descomissionamento da conta temporária de testes:</li>
  </ul>
  <pre><code>net user Usuário1 /delete</code></pre>
</details>

---

## 💡 O Que Aprendi na Prática (Conceitos Técnicos)
* **Estrutura de ACLs e Herança:** O Windows aplica listas de controle de acesso discricionárias (DACLs) aos diretórios de usuários. Mesmo que o disco esteja na partição raiz `C:`, as subpastas em `C:\Users` quebram a herança aberta para impedir que usuários comuns leiam dados confidenciais de outros colaboradores.
* **Agilidade Operacional via Linha de Comando:** Compreender a sintaxe dos comandos `net user` e `net localgroup` permite que um operador execute triagens e revogações emergenciais de contas comprometidas em segundos, sem depender da interface gráfica.
* **Importância de Senhas Fortes e Contas Padrão:** Senhas fracas ou inexistentes viabilizam ataques de força bruta locais ou via SMB/RDP. Manter usuários padrão como regra operacional impede que ameaças executem binários em nível de anel privilegiado do sistema.

---

## 🗺️ Evidências da Execução no Sistema

<details open>
  <summary><b>1. Provisionamento Inicial da Conta de Utilizador Local (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 1: Captura de tela 2026-09-30 130958.png -->
    <img width="600" alt="Evidência 1 - Criação do Usuário1"  src="https://github.com/user-attachments/assets/5bbb833c-1b23-4f58-8cc8-1d9b47e014eb" />
    <p><i>Criação da conta local <code>Usuário1</code> sem vínculo com serviços em nuvem.</i></p>
  </div>
</details>

<details open>
  <summary><b>2. Bloqueio de Acesso e Auditoria de ACLs Avançadas em C:\Users (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 2A: Captura de tela 2026-09-30 131825.png -->
    <img width="500" alt="Evidência 2A - Bloqueio de Leitura Inicial"  src="https://github.com/user-attachments/assets/ae5aa8d1-aaf8-44fb-8662-8b321b9670ec" />
    <br><br>
    <!-- Evidência 2B: Captura de tela 2026-09-30 131950.png -->
    <img width="750" alt="Evidência 2B - Permissões Avançadas NTFS"   src="https://github.com/user-attachments/assets/68912424-3d2b-46fc-97c1-ffc6dc7ce520" />
    <p><i>Restrição inicial de leitura na pasta de perfil e validação do Controle Total delegado a <b>SISTEMA</b>, <b>Administradores</b> e ao próprio <b>Usuário1</b>.</i></p>
  </div>
</details>

<details open>
  <summary><b>3. Diagnóstico de Restrição de Snap-in no Windows Home (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 3: Captura de tela 2026-09-30 132118.png -->
    <img width="750" alt="Evidência 3 - Bloqueio lusrmgr.msc"   src="https://github.com/user-attachments/assets/85f4a96c-4a5f-48d3-a97c-2ecfb4b0354e" />
    <p><i>Mensagem do sistema operacional indicando a indisponibilidade do <code>lusrmgr.msc</code> na edição Home.</i></p>
  </div>
</details>

<details open>
  <summary><b>4. Associação de Grupos via Interface Gráfica (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 4A: Captura de tela 2026-09-30 132245.png -->
    <img width="500" alt="Evidência 4A - Associação Inicial de Usuário Padrão"  src="https://github.com/user-attachments/assets/80ad6d12-33f7-49d4-ba5e-245650f0cd39" />
    <br><br>
    <!-- Evidência 4B: Captura de tela 2026-09-30 132254.png -->
    <img width="500" alt="Evidência 4B - Promoção a Administrador via GUI"  src="https://github.com/user-attachments/assets/7dca9cf2-2f8a-499a-8cb5-58ad78568b92" />

    <p><i>Inspeção do nível padrão no grupo de <b>Usuários</b> e transição para o grupo de <b>Administradores</b>.</i></p>
  </div>
</details>

<details open>
  <summary><b>5. Auditoria e Gestão de Privilégios via Prompt de Comando (CLI) (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 5: Captura de tela 2026-09-30 132346.png -->
    <img width="750" alt="Evidência 5 - Auditoria net user Usuário1" src="https://github.com/user-attachments/assets/57d2cae0-c2d0-47ec-82e7-25b21c563a24" />
    <p><i>Saída do utilitário <code>net user</code> validando parâmetros da conta e filiação ao grupo <code>*Administradores</code>.</i></p>
  </div>
</details>

<details open>
  <summary><b>6. Despromoção de Privilégios e Exclusão Segura da Conta (Clique para recolher)</b></summary>
  <br>
  <div align="center">
    <!-- Evidência 6A: Captura de tela 2026-09-30 132444.png -->
    <img width="750" alt="Evidência 6A - Remoção do Grupo de Administradores"  src="https://github.com/user-attachments/assets/4bc2e4d6-60cf-4ae6-87f3-9a98d37d998e" />
    <br><br>
    <!-- Evidência 6B: Captura de tela 2026-09-30 132522.png -->
    <img width="750" alt="Evidência 6B - Exclusão Definitiva net user /delete"  src="https://github.com/user-attachments/assets/29aa6988-ac87-4cc1-9a66-2aed863aff40" />
    <p><i>Revogação administrativa com <code>net localgroup Administradores Usuário1 /delete</code> e eliminação do usuário de testes via <code>net user Usuário1 /delete</code>.</i></p>
  </div>
</details>

---

## 📚 Referência Técnica: Roteiro Oficial do Laboratório (Cisco NetAcad)
> ℹ️ Esta secção resume o guião oficial "Laboratório - Criar contas de usuário" e serve como **referência técnica**, não como relato do que foi executado.

<details>
  <summary><b>📋 Resumo do Roteiro Oficial (Clique para expandir)</b></summary>
  <br>
  <ul>
    <li><b>Parte 1: Criando uma nova conta de usuário local:</b> Criação de conta local sem vínculo corporativo/nuvem, validação do primeiro início de sessão e conferência de permissões NTFS na pasta <code>C:\Users</code>.</li>
    <li><b>Parte 2: Revisando Propriedades da Conta de Usuário:</b> Utilização das ferramentas administrativas para mapear grupos aos quais a conta pertence.</li>
    <li><b>Parte 3: Modificação de contas de usuário local:</b> Elevação de privilégios para o grupo de Administradores, teste de permissões elevadas, reversão dos privilégios e exclusão definitiva da conta.</li>
  </ul>
</details>

---

## 💬 Questões de Reflexão (Gabarito Técnico Oficial)

**1. Por que é importante proteger todas as contas com senhas fortes?**  
> Se uma conta não utilizar senha ou adotar uma combinação fraca, qualquer invasor local ou através da rede poderá autenticar-se, roubar dados confidenciais e comprometer a máquina para fins não autorizados.

**2. Por que criar um usuário com privilégios padrão?**  
> Uma conta de usuário padrão opera sob o princípio do menor privilégio. Ela não possui autorização para instalar componentes de baixo nível, alterar diretivas globais de segurança ou violar a privacidade e os arquivos de outros usuários da estação.

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
