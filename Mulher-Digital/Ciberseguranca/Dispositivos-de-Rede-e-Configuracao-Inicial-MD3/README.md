# 🌐 Laboratório Prático: Introdução às Redes Hierárquicas (Cisco Packet Tracer)
**Formação Mulher Digital**

## 📌 Visão Geral do Projeto
Este repositório contém a simulação prática de uma arquitetura de rede corporativa baseada no **Modelo Hierárquico de Três Camadas** (Acesso, Distribuição e Núcleo/Core) desenvolvida no **Cisco Packet Tracer**.

O objetivo do laboratório foi implementar a segmentação física e lógica da rede, realizar o cabeamento correto entre os ativos, configurar o endereçamento IP estático nos hosts e habilitar a interface de gateway no roteador principal via CLI.

---

## 🏗️ Arquitetura e Dispositivos Utilizados

A topologia foi dividida nas três camadas do modelo hierárquico Cisco:

* **Camada de Núcleo (Core):** 1x Roteador Cisco 4331
* **Camada de Distribuição:** 1x Switch Cisco Catalyst 3650-24PS
* **Camada de Acesso:** 2x Switches Cisco Catalyst 2960-24TT
* **Dispositivos Finais (End Devices):** 4x PCs (`PC-Lab01`, `PC-Lab02`, `PC-Sec01`, `PC-Sec02`)
* **Meio Físico:** Cabos UTP diretos (*Copper Straight-Through*)

---

## 🗺️ Tabela de Endereçamento IP

| Dispositivo | Interface | Endereço IP | Máscara de Sub-rede | Gateway Padrão |
| :--- | :--- | :--- | :--- | :--- |
| **PC-Lab01** | FastEthernet0 | `192.168.1.10` | `255.255.255.0` | `192.168.1.1` |
| **PC-Lab02** | FastEthernet0 | `192.168.1.11` | `255.255.255.0` | `192.168.1.1` |
| **PC-Sec01** | FastEthernet0 | `192.168.1.20` | `255.255.255.0` | `192.168.1.1` |
| **PC-Sec02** | FastEthernet0 | `192.168.1.21` | `255.255.255.0` | `192.168.1.1` |
| **Roteador-Core** | GigabitEthernet0/0/0 | `192.168.1.1` | `255.255.255.0` | N/A |

---

## 💻 Configurações Realizadas

1. **Montagem Física:** Posicionamento dos switches de acesso, distribuição e roteador core.
2. **Alimentação Energética:** Adição da fonte AC Power Supply ao slot do Switch 3650 de Distribuição.
3. **Mapeamento de Portas:** Conexão rigorosa dos cabos diretos respeitando as interfaces específicas (FastEthernet e GigabitEthernet).
4. **Configuração dos Hosts:** Atribuição manual de IP, máscara e gateway padrão em cada PC.
5. **Configuração via CLI no Roteador:**
   ```text
   Router> enable
   Router# configure terminal
   Router(config)# interface gigabitEthernet 0/0/0
   Router(config-if)# ip address 192.168.1.1 255.255.255.0
   Router(config-if)# no shutdown
   Router(config-if)# exit
   Sem problemas! Ajustei o texto do relatório no Markdown para refletir exatamente o que você fez no vídeo: **a simulação do envio de pacotes ICMP (PDU) passando pelas camadas da rede**, sem mencionar o teste de ping no terminal.

Aqui está o código Markdown atualizado para você copiar e colar no seu arquivo `README.md`:

```markdown
# 🌐 Laboratório Prático: Introdução às Redes Hierárquicas (Cisco Packet Tracer)
**Formação Mulher Digital**

## 📌 Visão Geral do Projeto
Este repositório contém a simulação prática de uma arquitetura de rede corporativa baseada no **Modelo Hierárquico de Três Camadas** (Acesso, Distribuição e Núcleo/Core) desenvolvida no **Cisco Packet Tracer**.

O objetivo do laboratório foi implementar a segmentação física e lógica da rede, realizar o cabeamento correto entre os ativos, configurar o endereçamento IP estático nos hosts e habilitar a interface de gateway no roteador principal via CLI.

---

## 🏗️ Arquitetura e Dispositivos Utilizados

A topologia foi dividida nas três camadas do modelo hierárquico Cisco:

* **Camada de Núcleo (Core):** 1x Roteador Cisco 4331
* **Camada de Distribuição:** 1x Switch Cisco Catalyst 3650-24PS
* **Camada de Acesso:** 2x Switches Cisco Catalyst 2960-24TT
* **Dispositivos Finais (End Devices):** 4x PCs (`PC-Lab01`, `PC-Lab02`, `PC-Sec01`, `PC-Sec02`)
* **Meio Físico:** Cabos UTP diretos (*Copper Straight-Through*)

---

## 🗺️ Tabela de Endereçamento IP

| Dispositivo | Interface | Endereço IP | Máscara de Sub-rede | Gateway Padrão |
| :--- | :--- | :--- | :--- | :--- |
| **PC-Lab01** | FastEthernet0 | `192.168.1.10` | `255.255.255.0` | `192.168.1.1` |
| **PC-Lab02** | FastEthernet0 | `192.168.1.11` | `255.255.255.0` | `192.168.1.1` |
| **PC-Sec01** | FastEthernet0 | `192.168.1.20` | `255.255.255.0` | `192.168.1.1` |
| **PC-Sec02** | FastEthernet0 | `192.168.1.21` | `255.255.255.0` | `192.168.1.1` |
| **Roteador-Core** | GigabitEthernet0/0/0 | `192.168.1.1` | `255.255.255.0` | N/A |

---

## 💻 Configurações Realizadas

1. **Montagem Física:** Posicionamento dos switches de acesso, distribuição e roteador core.
2. **Alimentação Energética:** Adição da fonte AC Power Supply ao slot do Switch 3650 de Distribuição.
3. **Mapeamento de Portas:** Conexão rigorosa dos cabos diretos respeitando as interfaces específicas (FastEthernet e GigabitEthernet).
4. **Configuração dos Hosts:** Atribuição manual de IP, máscara e gateway padrão em cada PC.
5. **Configuração via CLI no Roteador:**
   ```text
   Router> enable
   Router# configure terminal
   Router(config)# interface gigabitEthernet 0/0/0
   Router(config-if)# ip address 192.168.1.1 255.255.255.0
   Router(config-if)# no shutdown
   Router(config-if)# exit

```

6. **Validação:** Simulação visual da transmissão de pacotes ICMP (PDU) percorrendo o fluxo correto entre as camadas de Acesso, Distribuição e Núcleo no modo Simulation.

---

## 📸 Gif de Demonstração do Laboratório

Abaixo está um Gif demonstrando o funcionamento da simulação visual e o fluxo dos pacotes ICMP percorrendo a topologia no Cisco Packet Tracer:



https://github.com/user-attachments/assets/5fd4bf40-0b54-4418-bcfb-ce8ec6173cd6





---

## 🧠 Desafios Encontrados e Aprendizados (Reflexão)

Projetar e configurar redes exige um nível elevado de atenção aos detalhes. Durante a execução deste laboratório, enfrentei alguns percalços valiosos que enriqueceram o meu aprendizado:

1. **Atenção aos Modelos de Hardware:** Inicialmente, selecionei o modelo errado do switch de distribuição por uma diferença de apenas um dígito na numeração. Isso me fez perceber o quão crítico é validar as especificações exatas do equipamento antes de iniciar a montagem, pois modelos diferentes possuem recursos e portas distintas.
2. **Precisão no Mapeamento de Portas e Cabeamento:** Tive dificuldades no momento de passar o cabeamento entre as camadas de Acesso, Distribuição e Núcleo. Conectar a porta errada pode comprometer o fluxo da rede ou inviabilizar a comunicação.
3. **Resolução de Problemas (Troubleshooting):** Precisei pausar, revisar o roteiro passo a passo com mais calma e refazer as conexões. Esse processo reforçou a importância do planejamento, da documentação e da paciência na área de infraestrutura e redes.

---

## 🎯 Conclusão

A prática permitiu consolidar os conceitos teóricos do modelo de três camadas da Cisco. O resultado final foi uma rede totalmente integrada, com simulação de envio de pacotes validada e total compreensão do caminho que a informação percorre do acesso ao núcleo.

```

```
