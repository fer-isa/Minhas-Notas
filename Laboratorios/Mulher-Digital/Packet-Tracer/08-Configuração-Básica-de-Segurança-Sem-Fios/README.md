<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=WLAN%20Security%20Hardening&fontSize=44&fontColor=FFFFFF&fontAlignY=35&desc=Configura%C3%A7%C3%A3o%20de%20WPA2-Personal%20%7C%20Cisco%20Packet%20Tracer&descAlignY=55&descSize=18&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Cisco_Packet_Tracer-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/WPA2--Personal-161B22?style=for-the-badge&logo=wi-fi&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Wireless_Security-161B22?style=for-the-badge&logo=shield&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Cisco_NetAcad-161B22?style=for-the-badge&logo=cisco&logoColor=58A6FF" />

</div>

<br>

## 🎯 O Objetivo
Proteger o tráfego e o acesso a uma rede sem fios corporativa numa pequena empresa utilizando **WPA2 Personal com encriptação AES**, eliminando o perfil de rede aberta. O processo exigiu autenticação inicial no router sem fios via browser, implementação de cifras robustas e reconfiguração do perfil de ligação cliente no computador portátil.

> **🛡️ Visão de Segurança (SOC):**  
> Redes sem fios sem autenticação ou com protocolos obsoletos (como WEP ou autenticação aberta) permitem interceção passiva de pacotes de dados e ataques *Man-in-the-Middle* (MitM) sem que o invasor necessite de acesso físico às instalações. O *hardening* da WLAN assegura confidencialidade e controlo de admissão à rede local.

<h2>🔍 A Metodologia de Troubleshooting Aplicada</h2>

<p>Para evitar diagnósticos precipitados, o problema foi abordado em 4 etapas analíticas baseadas no modelo em camadas:</p>

<pre><code>[1. Delimitar Escopo]     --&gt; Falha local no host ou na rede inteira?
[2. Camada Física/Enlace] --&gt; O rádio/Wi-Fi está associado? Há sinal?
[3. Camada de Rede]        --&gt; O IP é válido? Há conflito com o Gateway?
[4. Camada de Aplicação]   --&gt; A resolução DNS e o HTTP respondem?</code></pre>

<hr>
---

## 🧯 O Problema: Exposição da Rede Sem Fios

<details open>
  <summary><b>❌ 1. Ponto de partida e cenário de risco (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Cenário inicial:</b> O cliente conectava-se livremente à WLAN sem recurso a credenciais ou cifras de proteção.</li>
    <li><b>Risco operacional:</b> O perímetro de radiofrequência ultrapassa os limites físicos do escritório, permitindo que utilizadores não autorizados acedam a recursos internos e intercetem tráfego em texto claro.</li>
    <li><b>Objetivo do laboratório:</b> Configurar autenticação robusta no router sem fios e reconectar a estação final de forma segura.</li>
  </ul>
</details>

---

## 🛠️ A Solução: Implementação Passo a Passo

<details open>
  <summary><b>🌐 2. Verificação de conectividade e acesso de gestão (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li><b>Acesso inicial ao teste:</b> No <b>Laptop</b>, validação da resolução Web navegando para <code>www.cisco.pka</code>.</li>
    <li><b>Painel administrativo:</b> Acesso à interface gráfica do router através do browser em <code>http://192.168.1.1</code> com as credenciais administrativas (<code>admin</code> / <code>admin</code>).</li>
  </ul>
</details>

<details open>
  <summary><b>🔐 3. Configuração de segurança no Router Sem Fios (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li>Navegação pelo menu: <b>Wireless > Wireless Security</b>.</li>
    <li><b>Modo de segurança selecionado:</b> Alteração de <i>Disabled</i> para <b>WPA2 Personal</b> na banda de 2.4 GHz.</li>
    <li><b>Criptografia e Chave Pré-Partilhada:</b> Definição do algoritmo <b>AES</b> com a palavra-passe:</li>
  </ul>
  <pre><code>Network123</code></pre>
  <ul>
    <li>As configurações foram gravadas em <b>Save Settings</b>, resultando na perda temporária de sinal do portátil devido à alteração de parâmetros.</li>
  </ul>
</details>

<details open>
  <summary><b>💻 4. Associação e autenticação do Cliente Sem Fios (Clique para recolher)</b></summary>
  <br>
  <ul>
    <li>No portátil, abertura da ferramenta <b>Desktop > PC Wireless</b>.</li>
    <li>No separador <b>Connect</b>, localização do SSID corporativo <b>Academy</b>.</li>
    <li>Inserção da chave pré-partilhada <code>Network123</code> e clique em <b>Connect</b>.</li>
    <li>Validação do restabelecimento do feixe de ligação de rádio entre o cliente e o ponto de acesso.</li>
  </ul>
</details>


## 💡 O Que Aprendi na Prática (Conceitos de Troubleshooting)
* **Ping vs. Tracert no Diagnóstico:** O `ping` é o teste primário de acessibilidade fim a fim (valida se o host responde); o `tracert` detalha salto a salto onde a rota é interrompida.
* **Perigo de IPs Estáticos não Documentados:** Configurar manualmente o mesmo IP do Gateway Padrão paralisa a máquina local e gera riscos de instabilidade na tabela ARP do roteador.
* **Dependência do DNS:** O erro "Host Name Unresolved" em browsers não significa necessariamente queda do site; na maioria das vezes, indica ausência de conectividade L3 com o resolvedor DNS.
* **Segurança de Gateways:** Manter as credenciais de fábrica (`admin`/`admin`) permite que qualquer estação cabeada altere regras de segurança do roteador, tornando o *hardening* de senhas uma prioridade básica.

---

## 🗺️ Evidências: Validação do Acesso Seguro

<details open>
  <summary><b>✅ 5. Teste final de navegação (Clique para recolher)</b></summary>
  <br>
  <p>Com a associação restabelecida sob cifra WPA2, o <b>Web Browser</b> do portátil foi reaberto com o pedido a <code>www.cisco.pka</code>, obtendo resposta bem-sucedida e validando a comunicação completa fim a fim.</p>
  <div align="center">
    <!-- INSIRA A IMAGEM DE EVIDÊNCIA DO NAVEGADOR CARREGANDO WWW.CISCO.PKA AQUI -->
    <img width="800" alt="Evidência do teste final bem sucedido carregando a página www.cisco.pka" src="https://github.com/user-attachments/assets/6148a5b0-4da4-4af3-9fc9-67bf5287e17b" />
    <p><i>Acesso autenticado ao servidor Web corporativo após associação sem fios via WPA2-Personal.</i></p>
  </div>
</details>

---- 
<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas/tree/main/Mulher-Digital/Ciberseguranca">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Índice_de_Cibersegurança-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=120&section=footer&animation=fadeIn" width="100%" />

</div>
