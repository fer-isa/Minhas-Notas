<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Provisionamento%20da%20VM%20Cisco&fontSize=44&fontColor=FFFFFF&fontAlignY=35&desc=Troubleshooting%20de%20Download%2C%20Importa%C3%A7%C3%A3o%20e%20Valida%C3%A7%C3%A3o%20%7C%20VirtualBox&descAlignY=55&descSize=18&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Oracle_VirtualBox-161B22?style=for-the-badge&logo=virtualbox&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Cisco_NetAcad-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Troubleshooting_curl-161B22?style=for-the-badge&logo=gnubash&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Diagnóstico_de_Erros-161B22?style=for-the-badge&logo=shield&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo
Baixar a máquina virtual oficial do curso da Cisco (`Cybersecurity_Lab_VM.ova`) e importá-la no **Oracle VM VirtualBox** para usar nos laboratórios de Redes e Cibersegurança (NetAcad / Cisco / Mulher Digital). O caminho não foi direto: o primeiro download falhou e o **troubleshooting do erro de importação** virou a parte central deste laboratório.

> **🛡️ Visão de Segurança (SOC):**  
> Executar um arquivo que chegou incompleto ou corrompido é um risco operacional. Diagnosticar o erro a partir da mensagem do sistema, entender a causa e adotar uma forma de download mais estável é o tipo de raciocínio de investigação esperado em Suporte Técnico e SOC Nível 1.

---

## 🧯 O Problema: Erro na Importação

<details open>
  <summary><b>❌ 1. Ponto de partida e primeiro erro (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>O que eu queria fazer:</b> baixar o <code>Cybersecurity_Lab_VM.ova</code> e importá-lo no VirtualBox.</li>
    <li><b>O que deu errado:</b> tentei baixar direto pelo navegador e o download falhou ou terminou incompleto.</li>
    <li><b>O erro do VirtualBox ao importar:</b> <code>VERR_TAR_BAD_CHKSUM_FIELD</code>.</li>
    <li><b>Minha dúvida:</b> por que o erro aparecia se o arquivo parecia ter sido baixado, e como resolver.</li>
  </ul>
</details>

<details open>
  <summary><b>🔎 2. Diagnóstico da causa (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li>O formato <code>.ova</code> é essencialmente um arquivo <b>tar</b> que contém as imagens de disco e o descritor <code>.ovf</code>.</li>
    <li>O erro <code>VERR_TAR_BAD_CHKSUM_FIELD</code> indicou que o arquivo estava <b>corrompido</b> e com tamanho menor que o original.</li>
    <li>A URL de download da Cisco fica em servidores da <b>AWS S3</b> com tokens temporários. Esses tokens expiravam no meio da transferência pelo navegador, cortando o fluxo de dados sem avisar explicitamente.</li>
  </ul>
</details>

---

## 🛠️ A Solução: Download pela Linha de Comando

<details open>
  <summary><b>⬇️️ 3. Download com curl (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Estratégia:</b> excluir o arquivo danificado e baixar pelo terminal com o <code>curl</code>, que é mais estável, em vez de insistir no navegador.</li>
    <li><b>Dificuldade com o link:</b> as URLs do portal da Cisco têm chaves de autenticação longas e redirecionamentos automáticos. Um comando simples baixaria apenas uma página de erro em HTML.</li>
    <li><b>Solução:</b> gerar um link novo no portal e rodar:</li>
  </ul>
  <pre><code>curl -L -o "Cybersecurity_Lab_VM.ova" "&lt;LINK_ASSINADO_DA_CISCO&gt;"</code></pre>
  <ul>
    <li><code>-L</code> (<code>--location</code>): segue os redirecionamentos até a gravação final do arquivo.</li>
    <li><code>-o</code>: grava exatamente com o nome e a extensão <code>.ova</code>.</li>
  </ul>
</details>

---

## 💡 O Que Aprendi na Prática (Conceitos Técnicos)
* **OVA = tar:** o `.ova` empacota o descritor `.ovf` e os discos virtuais em um único arquivo tar. Um erro de checksum de tar indica arquivo truncado ou corrompido.
* **URLs pré-assinadas (AWS S3):** o acesso ao arquivo depende de um token temporário. Se ele expira durante a transferência, o download é cortado sem aviso claro.
* **`curl -L` e `curl -o`:** seguir redirecionamentos e controlar o nome do arquivo de saída são essenciais para baixar corretamente links assinados.

---

## 🗺️ Evidências: VM Importada e em Funcionamento
Após o download íntegro, a máquina virtual **importou sem o erro de checksum** e iniciou normalmente, com o ambiente Linux CyberOps.

<div align="center">
  <img width="800" alt="Evidência 1 - Desktop da Cybersecurity LabVM em execução no VirtualBox" src="https://github.com/user-attachments/assets/5f84a570-3b62-4f3c-9662-f900617f750c" />
  <p><i>Cybersecurity LabVM Workstation 20250409 com status <b>[Executando]</b> no Oracle VirtualBox (build NetAcad CSE Lab VM 2025-04-09).</i></p>
</div>

<details open>
  <summary><b>⌨️ 4. Checagem de rede no terminal da VM (Clique para recolher)</b></summary>
  <br>
  <p>No Terminal da VM, executei <code>ip address</code> para validar as interfaces. Na primeira tentativa, um erro de digitação (<code>addressS</code>) retornou <code>Object "addressS" is unknown, try "ip help"</code>; corrigi o comando e segui.</p>
  <div align="center">
    <img width="700" alt="Evidência 2 - Terminal da VM com o comando ip addressS" src="https://github.com/user-attachments/assets/8074294f-686d-451b-83af-600c263b7a55" />
    <p><i>Terminal aberto na VM (<code>cisco@labvm</code>) com o comando digitado incorretamente.</i></p>
  </div>
  <div align="center">
    <img width="700" alt="Evidência 3 - Mensagem de erro e comando corrigido" src="https://github.com/user-attachments/assets/9c6515bf-ca1c-4620-860f-a8bfcb70f8fa" />
    <p><i>Mensagem de erro do <code>ip</code> e correção do comando para <code>ip address</code>.</i></p>
  </div>
  <div align="center">
    <img width="800" alt="Evidência 4 - Saída do comando ip address" src="https://github.com/user-attachments/assets/b6f6be59-6da8-476d-b91e-48f67ba21ba0" />
    <p><i>Interface <code>enp0s3</code> ativa com <code>10.0.2.15/24</code> (dinâmico) e loopback <code>127.0.0.1/8</code>.</i></p>
  </div>
</details>

<details open>
  <summary><b>🔥 5. Teste de navegação e conectividade (Clique para recolher)</b></summary>
  <br>
  <p>Abri o Firefox dentro da própria VM e acessei <code>https://www.google.com</code>, confirmando que a máquina tem acesso à internet.</p>
  <div align="center">
    <img width="800" alt="Evidência 5 - Firefox da VM acessando o Google" src="https://github.com/user-attachments/assets/3f6882b7-6a1f-47ed-a9c7-44f258690cef" />
    <p><i>Navegação bem-sucedida a partir da VM, validando a conectividade externa.</i></p>
  </div>
</details>

<details open>
  <summary><b>🔑 6. Conferência das credenciais padrão (Clique para recolher)</b></summary>
  <br>

| Usuário | Senha | Propósito no Laboratório |
| :--- | :--- | :--- |
| `cisco` | `password` | Acesso básico de usuário de estação |
| `analyst` | `cyberops` | Atividades de SOC, inspeção de pacotes e análise de incidentes |

  <blockquote>Credenciais padrão da imagem de laboratório, sem uso fora deste ambiente isolado.</blockquote>
</details>

---

## 📚 Referência Técnica: Roteiro Oficial do Laboratório (Cisco NetAcad)
> ℹ️ Esta seção resume o roteiro oficial "Instalação de uma máquina virtual em um computador pessoal" e serve como **referência técnica**, não como relato do que executei.

<details>
  <summary><b>📋 Requisitos e conceitos do roteiro (Clique para expandir)</b></summary>
  <br>
  <ul>
    <li>Computador de <b>64 bits</b> com no mínimo <b>4 GB de RAM</b> e <b>50 GB de espaço livre</b> em disco.</li>
    <li><b>Virtualização de hardware ativada na BIOS</b> para executar VMs de 64 bits.</li>
    <li>O arquivo de imagem tem cerca de 2,5 GB e pode expandir até 5 GB durante o uso no VirtualBox.</li>
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
