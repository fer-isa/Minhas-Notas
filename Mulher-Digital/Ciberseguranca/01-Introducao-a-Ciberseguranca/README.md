<div align="center">

  <img src="../../assets/introduction-to-cybersecurity.png" width="180" alt="Introduction to Cybersecurity" />

  <div align="center">
  <h2>🛡️ Introdução à Cibersegurança — Módulos 1 ao 6</h2>
  <p><b>Formação Mulher Digital • Trilha de Cibersegurança & Infraestrutura</b></p>
</div>

<hr/>

<h3>📌 Visão Geral</h3>
<p>Minhas anotações e resumos sobre os pilares da Segurança da Informação, tipos de ataques, defesa de redes, criptografia e como responder a incidentes. O foco aqui é simplificar os conceitos técnicos fundamentais.</p>

<hr/>

<h3>🏛️ Módulo 1: O Mundo da Cibersegurança & Tríade CIA</h3>

<p><b>A Tríade CIA (Pilares Fundamentais)</b></p>
<table width="100%">
  <thead>
    <tr bgcolor="#1f242c">
      <th align="left">Pilar</th>
      <th align="left">Conceito</th>
      <th align="left">Objetivo Prático</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>Confidencialidade</b></td>
      <td>Sigilo</td>
      <td>Garantir que só quem tem permissão consiga acessar a informação.</td>
    </tr>
    <tr>
      <td><b>Integridade</b></td>
      <td>Precisão</td>
      <td>Garantir que os dados não sejam alterados ou apagados sem autorização.</td>
    </tr>
    <tr>
      <td><b>Disponibilidade</b></td>
      <td>Acesso</td>
      <td>Garantir que o sistema e os dados estejam sempre no ar quando o usuário precisar.</td>
    </tr>
  </tbody>
</table>

<br>

<p><b>Tipos de Hackers</b></p>
<ul>
  <li><b>White Hat (Éticos):</b> Têm autorização para testar sistemas e ajudar a corrigir falhas de segurança.</li>
  <li><b>Black Hat (Maliciosos):</b> Invadem sem permissão para roubar dados, extorquir ou causar danos.</li>
  <li><b>Grey Hat (Neutros):</b> Invadem sem pedir, mas geralmente avisam a empresa sobre a falha (muitas vezes pedindo uma recompensa).</li>
</ul>

<hr/>

<h3>⚠️ Módulo 2: Vulnerabilidades, Malwares e Engenharia Social</h3>

<p><b>Engenharia Social (O Fator Humano)</b></p>
<ul>
  <li><b>Phishing:</b> E-mails ou páginas falsas enviadas em massa para roubar senhas.</li>
  <li><b>Spear Phishing:</b> Um ataque altamente direcionado e personalizado (ex: focado apenas no diretor financeiro).</li>
  <li><b>Vishing & Smishing:</b> Golpes aplicados através de chamadas de voz (Vishing) ou mensagens de SMS (Smishing).</li>
</ul>

<br>

<p><b>Tipos de Malware</b></p>
<table width="100%">
  <thead>
    <tr bgcolor="#1f242c">
      <th align="left">Tipo</th>
      <th align="left">Comportamento</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>Vírus</b></td>
      <td>Gruda em arquivos legítimos e precisa que o usuário clique (execute) para funcionar.</td>
    </tr>
    <tr>
      <td><b>Worm</b></td>
      <td>Se espalha sozinho e de forma automática pela rede, sem precisar de cliques.</td>
    </tr>
    <tr>
      <td><b>Trojan (Cavalo de Troia)</b></td>
      <td>Finge ser um aplicativo útil, mas abre portas nos bastidores para invasores entraentrar.</td>
    </tr>
    <tr>
      <td><b>Ransomware</b></td>
      <td>Sequestra (criptografa) os arquivos do computador e exige pagamento de resgate.</td>
    </tr>
  </tbody>
</table>

<hr/>

<h3>🌐 Módulo 3: Fundamentos de Segurança em Redes</h3>
<ul>
  <li><b>Segmentação de Rede:</b> Dividir a rede em pedaços menores (VLANs e DMZ) para isolar problemas e impedir que o invasor se espalhe facilmente pelas máquinas.</li>
  <li><b>DNS:</b> Transforma nomes de sites em IPs. Pode sofrer ataques para redirecionar o usuário a sites falsos.</li>
  <li><b>DHCP:</b> Entrega IPs automaticamente. Precisa de proteção para evitar que invasores distribuam IPs falsos na rede.</li>
</ul>

<hr/>

<h3>⚔️ Módulo 4: Vetores de Ataque Avançados</h3>
<ul>
  <li><b>Man-in-the-Middle (MitM):</b> O invasor se coloca silenciosamente no meio da comunicação entre duas pessoas para interceptar ou alterar os dados.</li>
  <li><b>DoS & DDoS (Negação de Serviço):</b> Sobrecarga intencional de um sistema para derrubá-lo. O DDoS usa várias máquinas zumbis (botnets) ao mesmo tempo.</li>
  <li><b>SQL Injection (SQLi):</b> Inserir códigos de banco de dados em campos de formulários para roubar ou apagar informações do site.</li>
  <li><b>Cross-Site Scripting (XSS):</b> Injetar scripts maliciosos que acabam sendo executados no navegador de outros usuários legítimos.</li>
</ul>

<hr/>

<h3>🔒 Módulo 5: Mecanismos de Proteção, Perímetro e Criptografia</h3>

<p><b>Criptografia</b></p>
<table width="100%">
  <thead>
    <tr bgcolor="#1f242c">
      <th align="left">Mecanismo</th>
      <th align="left">Estrutura</th>
      <th align="left">Uso Principal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>Simétrica</b></td>
      <td>1 chave única (tranca e destranca)</td>
      <td>Rápida, usada para grandes volumes de dados armazenados.</td>
    </tr>
    <tr>
      <td><b>Assimétrica</b></td>
      <td>2 chaves (Pública e Privada)</td>
      <td>Negociação segura e assinaturas digitais (ex: o cadeado do navegador).</td>
    </tr>
  </tbody>
</table>

<br>

<p><b>MFA (Autenticação Multifator)</b><br>
Exige pelo menos 2 de 3 fatores para liberar o acesso:</p>
<ol>
  <li><b>Algo que você sabe:</b> Senha ou PIN.</li>
  <li><b>Algo que você tem:</b> Celular, aplicativo autenticador ou token.</li>
  <li><b>Algo que você é:</b> Biometria (digital ou reconhecimento facial).</li>
</ol>

<hr/>

<h3>📋 Módulo 6: Gestão de Riscos, Políticas e Resposta a Incidentes</h3>
<ul>
  <li><b>Princípio do Menor Privilégio:</b> Dar a cada usuário apenas as permissões estritamente necessárias para ele fazer o trabalho dele. Nem mais, nem menos.</li>
  <li><b>Gestão de Patches:</b> Manter tudo sempre atualizado para fechar brechas que já são conhecidas pelos hackers.</li>
  <li><b>Resposta a Incidentes:</b> Dividida em Preparação, Detecção, Contenção/Recuperação e Pós-Incidente (aprender com o que deu errado).</li>
  <li><b>Defesa em Profundidade:</b> A segurança nunca depende de uma barreira só. É preciso sobrepor tecnologia, regras da empresa e treinamento humano.</li>
</ul>

<hr/>

<div align="center">
  <h3>👩‍💻 Desenvolvido por</h3>
  <p><b>Fernanda Isabelli Oliveira da Silva</b></p>
  <p>
    <a href="https://github.com/fer-isa">
      <img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white" alt="GitHub" />
    </a>
    <a href="https://www.linkedin.com/in/fernanda-isabelli/">
      <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" />
    </a>
  </p>
</div>
