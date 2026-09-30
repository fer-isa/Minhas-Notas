<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Ataque%20SQL%20Injection%20no%20Wireshark&fontSize=40&fontColor=FFFFFF&fontAlignY=35&desc=An%C3%A1lise%20Forense%20de%20PCAP%2C%20Extra%C3%A7%C3%A3o%20e%20Quebra%20de%20Hashes%20%7C%20SOC%20N1&descAlignY=55&descSize=16&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Wireshark-161B22?style=for-the-badge&logo=wireshark&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Cisco_NetAcad-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/PCAP_Analysis-161B22?style=for-the-badge&logo=wireshark&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/SQL_Injection-161B22?style=for-the-badge&logo=mysql&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/CrackStation-161B22?style=for-the-badge&logo=keycdn&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo
Investigar uma captura de tráfego de rede (`SQL_Lab.pcap`) no **Wireshark** para reconstruir as fases de um ataque real de Injeção de SQL (*SQLi*) contra uma base de dados MySQL. Em vez de realizar o ataque, o papel desempenhado foi o de analista de SOC: inspecionar o fluxo HTTP pacote a pacote, identificar os vectores de exploração, analisar os dados exfiltrados da tabela de utilizadores e realizar a quebra dos hashes de palavra-passe obtidos.

> **🛡️ Visão de Segurança (SOC):**  
> Um ataque de SQL Injection raramente acontece num único disparo. Ele segue uma sequência lógica de reconhecimento: teste de vulnerabilidade (`1=1`), recolha de metadados (versão e utilizador da base de dados), enumeração do esquema (`information_schema`) e extração de credenciais. Identificar essa cadência nos fluxos TCP/HTTP é fundamental para determinar o impacto e a gravidade de um incidente de segurança.

---

## 🧯 Investigação Passo a Passo (Análise do PCAP)

<details open>
  <summary><b>🌐 1. Identificação dos Endereços IP Envolvidos (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Ficheiro analisado:</b> <code>/home/analyst/lab.support.files/SQL_Lab.pcap</code> (duração de 441 segundos de ataque).</li>
    <li><b>Endereço IP de Origem (Atacante):</b> <code>10.0.2.4</code>.</li>
    <li><b>Endereço IP de Destino (Servidor Web / BD):</b> <code>10.0.2.15</code>.</li>
  </ul>
</details>

<details open>
  <summary><b>🔍 2. Reconhecimento e Mapeamento da Base de Dados (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Pacote 13 (Teste de Injeção):</b> O invasor inseriu a condição booleana <code>1=1</code> num pedido <code>HTTP GET</code>. Como o servidor devolveu registos válidos em vez de erro de sintaxe, a vulnerabilidade ficou confirmada.</li>
    <li><b>Pacote 19 (Utilizador e Base):</b> Execução de <code>1' or 1=1 union select database(), user() #</code> revelando a base de dados <code>dvwa</code> sob a conta <code>root@localhost</code>.</li>
    <li><b>Pacote 22 (Identificação do SGBD):</b> Execução de <code>1' or 1=1 union select null, version() #</code>. Identificada a versão <b>MySQL 5.7.12</b> (<code>5.7.12-0ubuntu1.1</code>).</li>
    <li><b>Pacote 25 (Enumeração de Tabelas):</b> O atacante consultou o <code>INFORMATION_SCHEMA.tables</code> e filtrou especificamente por <code>WHERE table_name='users'</code> para obter apenas as colunas da tabela de credenciais.</li>
  </ul>
</details>

<details open>
  <summary><b>🔑 3. Exfiltração e Quebra de Credenciais (Pacote 28) (Clique para recolher)</b></summary>
  <br>
  <p>No <b>Pacote 28</b>, ao seguir o fluxo HTTP (<i>Follow > HTTP Stream</i>), o comando <code>1' or 1=1 union select user, password from users#</code> despejou utilizadores e hashes MD5 de senhas:</p>
  <ul>
    <li><b>Registo Localizado:</b> <code>First name: 1337 | Surname: 8d3533d75ae2c3966d7e0d4fcc69216b</code>.</li>
    <li><b>Utilizador associado ao hash:</b> <code>1337</code>.</li>
    <li><b>Quebra do Hash (CrackStation):</b> A submissão da hash MD5 revelou a palavra-passe em texto simples: <b><code>charley</code></b>.</li>
  </ul>
</details>

---

## 💡 O Que Aprendi na Prática (Conceitos Técnicos)
* **Reconstrução Forense com Wireshark:** O recurso *Follow HTTP Stream* é essencial para analisar o payload da camada de aplicação exactamente como o servidor web e o utilizador o visualizaram.
* **Risco de Funções de Resumo Fracas:** A base de dados armazenava palavras-passe com resumo MD5 simples e sem *salt*, permitindo a recuperação instantânea da palavra-passe através de tabelas arco-íris (*rainbow tables*).
* **Mitigação e Defesa em Profundidade:**
  1. Utilização mandatória de **consultas parametrizadas** (*Prepared Statements* / *Stored Procedures*), separando instruções de código dos dados de entrada.
  2. Implementação de validação rigorosa de entradas (*Input Validation*) associada a um Firewall de Aplicações Web (**WAF**) e aplicação do princípio do menor privilégio na base de dados.

---

## 🗺️ Evidências da Investigação

<details open>
  <summary><b>📸 Captura do Fluxo HTTP no Pacote 28 (Clique para recolher)</b></summary>
  <br>
  <p>Visualização das credenciais exfiltradas via <code>UNION SELECT</code> com o hash MD5 identificado na mesma linha do utilizador correspondente:</p>
  <div align="center">
    <img width="850" alt="Evidência Wireshark - Exfiltração do hash do usuário 1337"  src="https://github.com/user-attachments/assets/b4bbfdf8-12ae-4713-9762-b72c1171def7" />
    <p><i>Janela do Wireshark exibindo a resposta do servidor com o utilizador <code>1337</code> e o hash <code>8d3533d75ae2c3966d7e0d4fcc69216b</code>.</i></p>
  </div>
</details>

---

## 📚 Referência Técnica: Roteiro Oficial do Laboratório (Cisco NetAcad)
> ℹ️ Esta secção resume o guião oficial "Laboratório - Atacando um banco de dados MySQL" e serve como **referência técnica**, não como relato do que foi executado.

<details>
  <summary><b>📋 Resumo do Roteiro Oficial (Clique para expandir)</b></summary>
  <br>
  <ul>
    <li><b>Parte 1:</b> Carregamento do arquivo <code>SQL_Lab.pcap</code> e mapeamento inicial dos IPs <code>10.0.2.4</code> e <code>10.0.2.15</code>.</li>
    <li><b>Parte 2:</b> Análise da solicitação <code>HTTP GET</code> na linha 13 contendo o teste booleano <code>1=1</code>.</li>
    <li><b>Parte 3 e 4:</b> Inspeção dos pacotes 19 e 22 para obtenção do utilizador activo e versão do MySQL (5.7.12).</li>
    <li><b>Parte 5 e 6:</b> Mapeamento estrutural das tabelas e extração dos registos de senhas criptografadas.</li>
  </ul>
</details>
