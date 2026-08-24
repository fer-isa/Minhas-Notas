<div align="center">

# 🌐 Dispositivos de Rede & Configuração Inicial — Módulos 1 ao 3
**Formação Mulher Digital • Trilha de Cibersegurança**

</div>

---

## 📌 Visão Geral
Este documento consolida os fundamentos de arquitetura de rede, os pilares do modelo hierárquico corporativo (Acesso, Distribuição e Núcleo), computação em nuvem, tecnologias de virtualização e conversão de endereçamento IPv4 (Decimal para Binário).

---

## 🏗️ 1. Pilares da Arquitetura de Rede

Uma arquitetura de rede bem estruturada é projetada com base em quatro características fundamentais:

| Pilar | Conceito & Aplicação |
| :--- | :--- |
| **Tolerância a Falhas** | Estrutura com redundância desenhada para rápida recuperação caso um link ou dispositivo falhe, redirecionando o tráfego por caminhos alternativos. |
| **Escalabilidade** | Capacidade de expandir a rede (adicionando novos usuários, serviços e equipamentos) sem degradar a performance. |
| **Qualidade de Serviço (QoS)** | Conjunto de técnicas que prioriza e gerencia o tráfego de dados sensíveis a atrasos (como voz sobre IP e vídeo). |
| **Segurança** | Proteção da infraestrutura, dos equipamentos e dos dados contra acessos não autorizados e ameaças (Tríade CIA). |

---

## 🏢 2. Modelo de Rede Hierárquica

A arquitetura hierárquica organiza a rede corporativa em camadas modulares para simplificar o gerenciamento e garantir alta disponibilidade:

[ Roteador / Switch Core ]  <--- Camada de Núcleo (Core)
                 |
     [ Switch de Distribuição ]   <--- Camada de Distribuição
                 |
       [ Switch de Acesso ]       <--- Camada de Acesso
        /        |        \
    [PC 1]    [PC 2]    [AP Wi-Fi] <--- Hosts / Dispositivos Finais
    ### Funções das Camadas e Equipamentos

* **Camada de Acesso (Onde estão os usuários):**
  * **Função:** Conecta os dispositivos finais (PCs, impressoras, telefones IP, APs) à infraestrutura local.
  * **Exemplo de Equipamento:** *Cisco Catalyst 2960-XR* (Switch Camada 2/3 de acesso).
* **Camada de Distribuição (Organiza e controla o tráfego):**
  * **Função:** Interliga a camada de acesso ao núcleo, agregando links, aplicando listas de controle de acesso (ACLs) e políticas de roteamento.
  * **Exemplo de Equipamento:** *Cisco Catalyst 9300 Series* (Switches modulares com suporte a empilhamento e Layer 3).
* **Camada de Núcleo / Core (Transporte em alta velocidade):**
  * **Função:** *Backbone* da rede de altíssima velocidade responsável por encaminhar grandes volumes de tráfego sem aplicar filtros pesados.
  * **Exemplo de Equipamento:** *Cisco Catalyst 9600 Series* (Chassis com alta densidade de portas e redundância avançada).

---

## ☁️ 3. Computação em Nuvem

### Modelos de Implantação
* **Nuvem Pública:** Recursos compartilhados e mantidos pelo provedor via Internet pública (ex: AWS, Google Drive, Microsoft 365).
* **Nuvem Privada:** Infraestrutura dedicada exclusivamente a uma única organização, com controle estrito de segurança e conformidade.
* **Nuvem Híbrida:** Combinação integrada de nuvens públicas e privadas com tráfego e dados compartilhados com segurança.
* **Nuvem Comunitária:** Infraestrutura compartilhada por organizações com objetivos ou requisitos regulatórios em comum (ex: rede integrada de hospitais).

### Modelos de Serviço

| Modelo | Definição | Exemplos de Mercado |
| :--- | :--- | :--- |
| **SaaS** (*Software as a Service*) | Aplicação completa disponibilizada diretamente via web. | Google Drive, Microsoft 365, Canva. |
| **PaaS** (*Platform as a Service*) | Ambiente pronto para desenvolvedores publicarem aplicações sem gerenciar SO/servidor. | AWS Elastic Beanstalk, Heroku, Google App Engine. |
| **IaaS** (*Infrastructure as a Service*) | Aluguel de recursos brutos de infraestrutura (máquinas virtuais, rede e armazenamento). | AWS EC2, Microsoft Azure VMs, Google Compute Engine. |

---

## 💻 4. Virtualização e Hipervisores

* **Conceito:** Tecnologia que particiona os recursos físicos do computador hospedeiro (*Host*) para executar múltiplos sistemas convidados (*Guests*) simultaneamente e de forma isolada.
* **Hipervisor Tipo 1 (Bare-Metal):** Instalado diretamente no hardware físico sem sistema operacional intermediário. Focado em servidores corporativos e data centers (ex: *Microsoft Hyper-V*, *VMware ESXi*).
* **Hipervisor Tipo 2 (Hosted):** Aplicativo instalado sobre um sistema operacional convencional. Ideal para estudos e simulações de teste (ex: *Oracle VirtualBox*).

---

## 🔢 5. Conversão de Endereçamento: Decimal para Binário

O IPv4 é composto por 4 octetos (32 bits), onde cada octeto varia de `0` a `255`:

### Tabela de Pesos Posicionais (8 bits)
| $2^7$ | $2^6$ | $2^5$ | $2^4$ | $2^3$ | $2^2$ | $2^1$ | $2^0$ |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **128** | **64** | **32** | **16** | **8** | **4** | **2** | **1** |

### Exemplo Prático: IP `192.168.10.5`
* **1º Octeto (192):** $128 + 64$ $\rightarrow$ `11000000`
* **2º Octeto (168):** $128 + 32 + 8$ $\rightarrow$ `10101000`
* **3º Octeto (10):** $8 + 2$ $\rightarrow$ `00001010`
* **4º Octeto (5):** $4 + 1$ $\rightarrow$ `00000101`

**Resultado em Binário:** `11000000.10101000.00001010.00000101`
