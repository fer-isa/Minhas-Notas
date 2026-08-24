<div align="center">
  <img src="../../assets/introduction-to-cybersecurity.png" width="180">
</div>

# 🛡️ Introdução à Cibersegurança — Módulos 1 ao 6
**Formação Mulher Digital • Trilha de Cibersegurança**

---

## 📌 Visão Geral
Resumo teórico consolidado cobrindo os pilares essenciais de segurança da informação, taxonomia de ameaças, engenharia social, arquitetura defensiva de redes, criptografia e resposta a incidentes.

---

## 🏛️ Módulo 1: O Mundo da Cibersegurança & Tríade CIA

* **Definição:** Conjunto de práticas, tecnologias e processos desenhados para proteger redes, dispositivos, programas e dados contra ataques e acessos não autorizados.

### A Tríade CIA (Pilares Fundamentais)

| Pilar | Conceito | Objetivo Central |
| :--- | :--- | :--- |
| **Confidencialidade** | Sigilo dos dados | Garantir acesso exclusivo a identidades e entidades autorizadas. |
| **Integridade** | Confiabilidade da informação | Assegurar que os dados não sofram alterações ou corrupções indevidas. |
| **Disponibilidade** | Acesso garantido | Assegurar que sistemas, redes e dados estejam acessíveis quando necessários. |

### Classificação de Atores de Ameaça (Hackers)

* **White Hat (Éticos):** Especialistas que utilizam suas habilidades para identificar e corrigir vulnerabilidades com autorização prévia.
* **Black Hat (Maliciosos):** Invasores que exploram falhas visando ganhos financeiros, sabotagem ou espionagem sem autorização.
* **Grey Hat (Neutros):** Navegam no limiar ético; descobrem falhas sem permissão e divulgam ou cobram por sua resolução.

---

## ⚠️ Módulo 2: Vulnerabilidades, Malwares e Engenharia Social

### Vetores de Engenharia Social (Fator Humano)
* **Phishing:** Disparo em massa de comunicações fraudulentas simulando fontes confiáveis para captura de credenciais.
* **Spear Phishing:** Ataque altamente customizado e direcionado a indivíduos ou cargos de alta relevância (ex: diretores, setor financeiro).
* **Vishing & Smishing:** Engenharia social aplicada via chamadas telefônicas de voz (*Vishing*) ou mensagens de SMS (*Smishing*).

### Taxonomia de Malwares

| Tipo | Comportamento Principal | Vetor de Propagação |
| :--- | :--- | :--- |
| **Vírus** | Anexa-se a arquivos legítimos e corrompe o sistema. | Depende da execução direta pelo usuário. |
| **Worm** | Explora vulnerabilidades para se autorreplicar pela rede. | Autônomo (não necessita de intervenção humana). |
| **Trojan** | Disfarça-se de software legítimo para abrir *backdoors*. | Engenharia social / downloads não verificados. |
| **Ransomware** | Sequestra o sistema cifrando arquivos e cobrando resgate. | E-mails de phishing, exploits e portas expostas. |

---

## 🌐 Módulo 3: Fundamentos de Segurança em Redes

* **Segmentação de Rede:** Criação de perímetros e sub-redes isoladas para conter a propagação lateral de invasores.
* **Mapeamento de Protocolos:**
  * **DNS:** Resolução hierárquica de nomes de domínio para endereços IP.
  * **DHCP:** Alocação automatizada e dinâmica de configurações IP.
  * **Modelos OSI / TCP/IP:** Estrutura de análise em camadas para aplicação de controles específicos (ex: TLS na camada de aplicação, IPsec na camada de rede).

---

## ⚔️ Módulo 4: Vetores de Ataque Avançados

* **Man-in-the-Middle (MitM):** Interceptação ativa e espionagem de comunicações entre dois pontos sem o conhecimento das partes.
* **DoS & DDoS (Denegação de Serviço):** Esgotamento intencional dos recursos de um servidor/serviço por sobrecarga de requisições originadas de uma única fonte (*DoS*) ou via *Botnet* distribuída (*DDoS*).
* **Ataques a Aplicações Web:**
  * **SQL Injection (SQLi):** Injeção de comandos SQL maliciosos em campos de entrada para manipulação indevida de bancos de dados.
  * **Cross-Site Scripting (XSS):** Execução de scripts maliciosos no navegador de usuários legítimos via inputs vulneráveis.

---

## 🔒 Módulo 5: Mecanismos de Proteção, Perímetro e Criptografia

### Criptografia

| Mecanismo | Chaves | Aplicação Típica |
| :--- | :--- | :--- |
| **Simétrica** | Chave única compartilhada | Cifragem em massa de alto desempenho (ex: AES, ChaCha20). |
| **Assimétrica** | Par de chaves (Pública / Privada) | Troca segura de chaves e assinaturas digitais (ex: RSA, ECC). |

### Controles de Borda e Autenticação
* **Firewalls & IDS/IPS:** Monitoramento contínuo de fluxos de tráfego, inspeção de pacotes e bloqueio de comportamentos anômalos.
* **MFA (Multi-Factor Authentication):** Camada adicional que combina algo que você sabe (senha), algo que possui (token/app) e algo que você é (biometria).

---

## 📋 Módulo 6: Gestão de Riscos, Políticas e Resposta a Incidentes

* **Princípio do Menor Privilégio (*Least Privilege*):** Concessão exclusiva dos privilégios mínimos necessários para o exercício de cada função.
* **Gestão de Patches:** Processo sistemático de aplicação de correções de segurança em sistemas operacionais e softwares.
* **Fases da Resposta a Incidentes (NIST / SANS):**
  1. **Preparação:** Definição de políticas, ferramentas e equipes de prontidão.
  2. **Detecção e Análise:** Identificação e validação de indicadores de comprometimento (IoCs).
  3. **Contenção, Erradicação e Recuperação:** Isolamento dos sistemas afetados, eliminação da ameaça e restauração segura.
  4. **Pós-Incidente (Lições Aprendidas):** Documentação técnica e aprimoramento dos controles defensivos.

---

> 💡 **Defense in Depth (Defesa em Profundidade):** A segurança não depende de uma barreira única, mas de múltiplas camadas coordenadas abrangendo tecnologia, processos rigorosos e conscientização contínua do fator humano.
