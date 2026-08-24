<div align="center">

  <img src="../../assets/introduction-to-cybersecurity.png" width="180" alt="Introduction to Cybersecurity" />

  <h1>🛡️ Introdução à Cibersegurança — Módulos 1 ao 6</h1>
  <p><b>Formação Mulher Digital • Trilha de Cibersegurança & Infraestrutura</b></p>

  <p>
    <img src="https://img.shields.io/badge/Cisco_Networking_Academy-Cybersecurity-005073?style=for-the-badge&logo=cisco&logoColor=white" alt="Cybersecurity" />
    <img src="https://img.shields.io/badge/Trilha-Mulher_Digital-8A2BE2?style=for-the-badge" alt="Mulher Digital" />
    <img src="https://img.shields.io/badge/Fundamentos-Tríade_CIA-30D158?style=for-the-badge" alt="Tríade CIA" />
    <img src="https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge" alt="Status" />
  </p>

</div>

<hr/>

<h2>📌 Visão Geral</h2>

<p>
Resumo teórico e analítico consolidado cobrindo os pilares fundamentais da <b>Segurança da Informação</b>, taxonomia de ameaças cibernéticas, engenharia social, arquitetura defensiva de redes de computadores, criptografia simétrica e assimétrica e metodologias de resposta a incidentes baseadas nos padrões NIST/SANS.
</p>

<hr/>

<details open>
  <summary><h2>🏛️ Módulo 1: O Mundo da Cibersegurança & Tríade CIA</h2></summary>
  <br/>

  <p><b>Definição:</b> Conjunto de práticas, tecnologias, processos e controles desenhados para proteger sistemas, redes, dispositivos, programas e dados contra ataques, danos e acessos não autorizados.</p>

  <h3>A Tríade CIA (Pilares Fundamentais)</h3>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left" width="25%">Pilar</th>
        <th align="left" width="35%">Conceito</th>
        <th align="left" width="40%">Objetivo Central</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>Confidencialidade</b></td>
        <td>Sigilo e privacidade dos dados</td>
        <td>Garantir que a informação seja acessada exclusivamente por entidades e identidades devidamente autorizadas.</td>
      </tr>
      <tr>
        <td><b>Integridade</b></td>
        <td>Confiabilidade e precisão da informação</td>
        <td>Assegurar que os dados permaneçam exatos, completos e protegidos contra modificações, exclusões ou corrupções não autorizadas.</td>
      </tr>
      <tr>
        <td><b>Disponibilidade</b></td>
        <td>Acesso contínuo e garantido</td>
        <td>Garantir que os serviços, redes, servidores e dados estejam prontamente acessíveis aos usuários autorizados quando requisitados.</td>
      </tr>
    </tbody>
  </table>

  <h3>Classificação de Atores de Ameaça (Hackers)</h3>
  <ul>
    <li><b>White Hat (Hackers Éticos):</b> Especialistas em segurança que utilizam seus conhecimentos técnicos para auditar, identificar e corrigir vulnerabilidades com autorização formal da organização.</li>
    <li><b>Black Hat (Hackers Maliciosos):</b> Invasores cibernéticos que violam sistemas sem autorização visando ganhos financeiros, extorsão, sabotagem, vazamento ou espionagem.</li>
    <li><b>Grey Hat (Neutros):</b> Atuam no limiar ético; identificam falhas sem consentimento prévio e posteriormente solicitam recompensas financeiras ou divulgam os problemas publicamente.</li>
  </ul>
</details>

<hr/>

<details open>
  <summary><h2>⚠️ Módulo 2: Vulnerabilidades, Malwares e Engenharia Social</h2></summary>
  <br/>

  <h3>Vetores de Engenharia Social (Fator Humano)</h3>
  <ul>
    <li><b>Phishing:</b> Disparo em larga escala de comunicações fraudulentas (e-mails, páginas falsas) induzindo a vítima a fornecer credenciais ou dados sensíveis.</li>
    <li><b>Spear Phishing:</b> Ataque personalizado e altamente direcionado a indivíduos, departamentos específicos ou cargos de alta relevância (ex: diretores, setor financeiro).</li>
    <li><b>Vishing & Smishing:</b> Golpes de engenharia social conduzidos através de chamadas telefônicas de voz (<i>Vishing</i>) ou mensagens de texto SMS (<i>Smishing</i>).</li>
  </ul>

  <h3>Taxonomia de Códigos Maliciosos (Malwares)</h3>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left" width="20%">Tipo</th>
        <th align="left" width="40%">Comportamento Principal</th>
        <th align="left" width="40%">Vetor de Propagação</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>Vírus</b></td>
        <td>Anexa-se a arquivos e programas legítimos, corrompendo o sistema após a execução.</td>
        <td>Requer intervenção ativa do usuário (execução do arquivo hospedeiro).</td>
      </tr>
      <tr>
        <td><b>Worm</b></td>
        <td>Explora falhas em protocolos de rede para se autorreplicar e propagar entre máquinas.</td>
        <td>Propagação autônoma pela infraestrutura de rede, sem necessidade de ação humana.</td>
      </tr>
      <tr>
        <td><b>Trojan (Cavalo de Troia)</b></td>
        <td>Disfarça-se de aplicativo útil ou legítimo para instalar <i>backdoors</i> no sistema.</td>
        <td>Engenharia social, anexos maliciosos e downloads não verificados.</td>
      </tr>
      <tr>
        <td><b>Ransomware</b></td>
        <td>Cifra arquivos e partições do sistema e exige o pagamento de resgate para recuperação da chave.</td>
        <td>E-mails de phishing, vulnerabilidades em serviços expostos (RDP) e exploits de rede.</td>
      </tr>
    </tbody>
  </table>
</details>

<hr/>

<details open>
  <summary><h2>🌐 Módulo 3: Fundamentos de Segurança em Redes</h2></summary>
  <br/>

  <ul>
    <li><b>Segmentação de Rede:</b> Criação de sub-redes lógicas (VLANs) e zonas desmilitarizadas (DMZ) para isolar tráfegos críticos e impedir a movimentação lateral de agentes maliciosos.</li>
    <li><b>Mapeamento de Protocolos Fundamentais:</b>
      <ul>
        <li><b>DNS (Domain Name System):</b> Serviço hierárquico responsável por resolver nomes de domínio em endereços IP. Requer proteção contra técnicas de <i>DNS Spoofing</i> e <i>Poisoning</i>.</li>
        <li><b>DHCP (Dynamic Host Configuration Protocol):</b> Protocolo de alocação dinâmica de parâmetros de rede (IP, Gateway, Máscara). Requer mitigação de <i>DHCP Snooping</i> e <i>Rogue DHCP</i>.</li>
        <li><b>Modelos OSI e TCP/IP:</b> Abordagem em camadas para análise de tráfego e aplicação de controles defensivos específicos (ex: TLS na Camada de Aplicação, IPsec na Camada de Rede).</li>
      </ul>
    </li>
  </ul>
</details>

<hr/>

<details open>
  <summary><h2>⚔️ Módulo 4: Vetores de Ataque Avançados</h2></summary>
  <br/>

  <ul>
    <li><b>Man-in-the-Middle (MitM):</b> Interceptação e possível manipulação de comunicações confidenciais entre dois pontos na rede sem que as partes percebam a espionagem.</li>
    <li><b>DoS & DDoS (Negação de Serviço):</b> Esgotamento deliberado de recursos de computação ou largura de banda de um alvo, originado de uma única fonte (<i>DoS</i>) ou coordenado por redes zumbis distribuídas (<i>Botnets / DDoS</i>).</li>
    <li><b>Ataques a Aplicações Web:</b>
      <ul>
        <li><b>SQL Injection (SQLi):</b> Inserção de trechos de código SQL em campos de formulário não sanitizados para consultar, manipular ou apagar dados de bancos de dados.</li>
        <li><b>Cross-Site Scripting (XSS):</b> Injeção de scripts JavaScript maliciosos que são executados diretamente no navegador de outros usuários legítimos da aplicação.</li>
      </ul>
    </li>
  </ul>
</details>

<hr/>

<details open>
  <summary><h2>🔒 Módulo 5: Mecanismos de Proteção, Perímetro e Criptografia</h2></summary>
  <br/>

  <h3>Criptografia</h3>

  <table width="100%">
    <thead>
      <tr bgcolor="#1f242c">
        <th align="left" width="25%">Mecanismo</th>
        <th align="left" width="35%">Estrutura de Chaves</th>
        <th align="left" width="40%">Aplicação Típica</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>Criptografia Simétrica</b></td>
        <td>Chave única compartilhada (cifragem e decifragem)</td>
        <td>Cifragem de grandes volumes de dados em repouso ou tráfego de alto desempenho (ex: AES, ChaCha20).</td>
      </tr>
      <tr>
        <td><b>Criptografia Assimétrica</b></td>
        <td>Par de chaves criptográficas (Chave Pública e Chave Privada)</td>
        <td>Negociação segura de chaves de sessão, assinaturas digitais e certificados SSL/TLS (ex: RSA, ECC).</td>
      </tr>
    </tbody>
  </table>

  <h3>Controles de Borda e Autenticação Robusta</h3>
  <ul>
    <li><b>Firewalls & IDS/IPS:</b> Equipamentos e softwares que inspecionam pacotes, filtram tráfego com base em regras de portas/protocolos e detectam ou bloqueiam assinaturas de invasão em tempo real.</li>
    <li><b>MFA (Multi-Factor Authentication):</b> Implementação de autenticação multifator exigindo pelo menos 2 de 3 fatores independentes:
      <ul>
        <li><i>Algo que você sabe</i> (senha ou PIN);</li>
        <li><i>Algo que você tem</i> (aplicativo autenticador, token físico ou chave de segurança FIDO2);</li>
        <li><i>Algo que você é</i> (biometria, reconhecimento facial ou digital).</li>
      </ul>
    </li>
  </ul>
</details>

<hr/>

<details open>
  <summary><h2>📋 Módulo 6: Gestão de Riscos, Políticas e Resposta a Incidentes</h2></summary>
  <br/>

  <ul>
    <li><b>Princípio do Menor Privilégio (<i>Least Privilege</i>):</b> Prática mandatória de conceder a cada usuário, sistema ou processo apenas as permissões estritamente necessárias para a execução de suas funções.</li>
    <li><b>Gestão de Vulnerabilidades e Patches:</b> Monitoramento sistemático e aplicação contínua de atualizações de segurança para neutralizar brechas conhecidas (CVEs).</li>
    <li><b>Fases do Ciclo de Resposta a Incidentes (NIST / SANS):</b>
      <ol>
        <li><b>Preparação:</b> Desenvolvimento de planos de contingência, políticas, treinamentos e configuração de ferramentas analíticas.</li>
        <li><b>Detecção e Análise:</b> Monitoramento contínuo de logs (SIEM) e identificação de Indicadores de Comprometimento (IoCs).</li>
        <li><b>Contenção, Erradicação e Recuperação:</b> Isolamento de ativos contaminados, remoção definitiva dos artefatos da ameaça e restauração segura dos serviços a partir de backups confiáveis.</li>
        <li><b>Pós-Incidente (Lições Aprendidas):</b> Reunião técnica para documentar o vetor de ataque, analisar o tempo de resposta e atualizar os controles defensivos da organização.</li>
      </ol>
    </li>
  </ul>
</details>

<hr/>

<blockquote>
  <b>💡 Defense in Depth (Defesa em Profundidade):</b><br/>
  A segurança da informação não pode depender de uma barreira isolada. Uma postura resiliente exige múltiplas camadas sobrepostas de proteção, articulando tecnologia avançada, políticas corporativas rigorosas e capacitação contínua do fator humano.
</blockquote>

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
