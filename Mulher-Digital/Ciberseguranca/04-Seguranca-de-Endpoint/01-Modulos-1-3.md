<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1D3A,50:1A365D,100:2A4365&height=220&section=header&text=Engenharia%20Social%20e%20Malware&fontSize=50&fontColor=FFFFFF&fontAlignY=35&desc=M%C3%B3dulo%20de%20Seguran%C3%A7a%20%7C%20Forma%C3%A7%C3%A3o%20Mulher%20Digital&descAlignY=55&descSize=20&descColor=58A6FF&animation=fadeIn" width="100%" />

<img src="https://img.shields.io/badge/Cibersegurança-161B22?style=for-the-badge&logo=shield&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Hacking_Humano-161B22?style=for-the-badge&logo=hackerone&logoColor=58A6FF" />
<img src="https://img.shields.io/badge/Defesa_SOC-161B22?style=for-the-badge&logo=kali-linux&logoColor=58A6FF" />

</div>

<br>

## 📌 Visão Geral
Documentação focada na compreensão das principais ameaças lógicas (Vírus e Worms) e nas táticas de Engenharia Social ("Hacking Humano") utilizadas para contornar defesas técnicas através da manipulação de pessoas. Inclui a confecção de um Pôster de Conscientização de Segurança.

---

## 🦠 Malware: O Código Malicioso

Malware (*Malicious* + *Software*) é o termo genérico para qualquer programa criado para se infiltrar, causar danos, roubar dados ou extorquir.

### 1. A Diferença Clássica: Vírus x Worm

| Característica | 📎 VÍRUS | 🐛 WORM (Verme) |
| :--- | :--- | :--- |
| **O que é?** | Fragmento de código que se "esconde" em outro arquivo. | Um programa independente e completo. |
| **Precisa de Hospedeiro?** | **SIM**. Depende de um arquivo legítimo (ex: `.exe`, `.docx`). | **NÃO**. É autônomo. |
| **Como se espalha?** | Através do compartilhamento de arquivos infectados. | Aproveita falhas de segurança e varreduras de rede para se propagar sozinho. |
| **Como Inicia?** | Precisa que o **usuário execute** (clique) no arquivo. | É automático, não precisa de ação humana. |
| **Caso Clássico** | *ILOVEYOU* (2000) - Via anexo de e-mail. | *WannaCry* (2017) - Ransomware que usou falhas do Windows. |

### 2. Sinais de Infecção (Visão SOC)
* ⚠️ Processamento de CPU anormal e extrema lentidão.
* ⚠️ Arquivos ocultos, modificados ou inacessíveis (Ransomware).
* ⚠️ Tráfego de rede suspeito (Worms buscando novas vítimas).

---

## 🎭 Engenharia Social (O Hacking Humano)

A arte de manipular pessoas para que revelem informações confidenciais ou realizem ações não autorizadas (como abrir uma porta ou instalar um malware). É contornar o firewall através da ingenuidade humana.

### As Principais Técnicas

* 🎣 **Phishing:** O Golpe do E-mail Falso. E-mails fraudulentos, fingindo ser de entidades confiáveis, enviados em massa para roubar credenciais.
* 🚶 **Tailgating (Carona Física):** Seguir de perto um funcionário autorizado para entrar em áreas restritas (salas de servidores, escritórios) sem possuir credencial.
* 🧲 **Isca (Baiting):** Deixar dispositivos físicos (como pendrives USB) em locais estratégicos para que uma vítima curiosa o conecte à rede da empresa.

---

## 🎨 Projeto Prático: Pôster de Conscientização

Como parte do laboratório, desenvolvi um material visual para conscientização interna focando na ameaça do **Phishing**. 

* **Objetivo:** Educar colaboradores em áreas de alta circulação (copas, recepção e elevadores).
* **Protocolo de Prevenção:**
  1. Verificar sempre o remetente real (não apenas o nome).
  2. Desconfiar de senso de urgência e pânico.
  3. Não clicar em links suspeitos ou plugar USBs desconhecidos.
  4. Na dúvida, sempre relatar ao setor de TI.

<br>
<div align="center">

  <p><b>Poster 1: Fundamentos de Engenharia Social e Vetores de Manipulação</b></p>
  <img width="380" alt="Pôster Engenharia Social" src="https://github.com/user-attachments/assets/72885b96-22c8-40e5-807a-5346b5bb0293" />
  <br><br>
  <p><b>Poster 2: Anatomia e Prevenção contra Ataques de Phishing</b></p>
  <img width="480" alt="Pôster Engenharia Social - Phishing" src="https://github.com/user-attachments/assets/5b19a3f4-fbd1-4717-8920-b65d2b8ede1c" />
  <br><br>
  <p><i>Projeto de conscientização desenvolvido para a Formação Mulher Digital</i></p>

</div>

<br>

---

## 💡 Minha Visão (Resumo SOC)

> O mais interessante de estudar Engenharia Social e Malwares é perceber que o elo mais fraco de qualquer arquitetura de segurança quase sempre é o ser humano. Não adianta ter o melhor firewall e a rede mais segmentada se um colaborador clica em um Phishing ou permite um Tailgating na porta do escritório.
> 
> Entender a diferença estrutural entre um Vírus (que precisa de um "empurrãozinho" do usuário para infectar) e um Worm (que se espalha sozinho como um incêndio pela rede explorando portas abertas) muda completamente a forma como abordamos a mitigação de um incidente dentro de um SOC. A segurança moderna exige não apenas ferramentas potentes, mas processos bem definidos e, acima de tudo, educação constante da equipe!

<br>

<div align="center">
  <a href="https://github.com/fer-isa/Minhas-Notas/tree/main/Mulher-Digital/Ciberseguranca">
    <img src="https://img.shields.io/badge/⬅_Voltar_para_Índice_de_Cibersegurança-161B22?style=for-the-badge&logo=github&logoColor=58A6FF" />
  </a>
</div>

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2A4365,50:1A365D,100:0B1D3A&height=100&section=footer" width="100%" />
