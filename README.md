<div align="center">

<img src="./assets/banner.gif" alt="Banner animado — Entrega Automatizada de Conteúdo" width="100%" />

# 📩 Entrega Automatizada de Conteúdo

### Captação, organização e distribuição de materiais com fluxos condicionais no n8n

<p align="center">
  <img src="https://img.shields.io/badge/n8n-Automação-EA4B71?style=for-the-badge&logo=n8n&logoColor=white&labelColor=111827" alt="n8n" height="25" />
  <img src="https://img.shields.io/badge/n8n_Forms-Formulário-00DDEF?style=for-the-badge&labelColor=111827" alt="Formulário n8n" height="25" />
  <img src="https://img.shields.io/badge/Google_Sheets-Dados-34A853?style=for-the-badge&logo=googlesheets&logoColor=white&labelColor=111827" alt="Google Sheets" height="25" />
  <img src="https://img.shields.io/badge/Gmail-Envio_de_e--mail-EA4335?style=for-the-badge&logo=gmail&logoColor=white&labelColor=111827" alt="Gmail" height="25" />
</p>

**Do preenchimento do formulário ao envio de um guia por e-mail — automaticamente e conforme o interesse do usuário.**

[![VER DEMONSTRAÇÃO](https://img.shields.io/badge/▶_VER_DEMONSTRAÇÃO-LINKEDIN-4CFB2B?style=for-the-badge&labelColor=111827)](https://lnkd.in/p/dpBYTAqu)

</div>

---

## 01 // Visão geral

A **Entrega Automatizada de Conteúdo** é uma solução desenvolvida durante a imersão **Jornada de Dados** para organizar respostas recebidas por formulário e enviar materiais relevantes de acordo com o interesse declarado por cada pessoa.

Com o **n8n** orquestrando o processo, os dados são registrados no **Google Sheets** e uma condição determina se o usuário receberá um **guia de automações com n8n por e-mail**, enviado pelo **Gmail**.

O projeto demonstra a integração de ferramentas, a automação de rotinas repetitivas e o uso de regras de negócio para direcionar ações sem intervenção manual.

## 02 // Problema e solução

Distribuir conteúdo manualmente exige acompanhar formulários, organizar cadastros e conferir quais pessoas solicitaram determinado material.

A automação centraliza esse processo em um único fluxo:

| Etapa | Resultado |
|---|---|
| Captação | Usuário preenche o formulário do n8n |
| Organização | As respostas são registradas no Google Sheets |
| Validação | Uma condição verifica a resposta de interesse |
| Entrega | Gmail envia o guia para quem respondeu **“Sim, quero aprender mais”** |
| Encerramento | Quando a condição não é atendida, o fluxo termina sem envio |

## 03 // Arquitetura da solução

O fluxo segue uma sequência simples: **captar → registrar → verificar → agir**.

<div align="center">

```mermaid
flowchart TD
    A["📝 Formulário enviado"] --> B["📊 Registrar resposta no Google Sheets"]
    B --> C{"✅ Respondeu: Sim, quero aprender mais?"}
    C -->|Sim| D["📧 Gmail envia o guia de n8n"]
    C -->|Não| E["⏹️ Encerrar sem envio"]

    classDef entrada fill:#122737,stroke:#00DDEF,color:#fff
    classDef registro fill:#132b23,stroke:#4CFB2B,color:#fff
    classDef decisao fill:#382908,stroke:#FFE600,color:#fff
    classDef envio fill:#341729,stroke:#FF008C,color:#fff
    class A entrada
    class B registro
    class C decisao
    class D,E envio
```
</div>

### Componentes da automação

| Nó do n8n | Responsabilidade |
|---|---|
| **On form submission** | Inicia a execução quando o formulário é enviado |
| **Append row in sheet** | Adiciona as respostas à planilha do Google Sheets |
| **If** | Avalia a condição de interesse em receber o material |
| **Send a message (Gmail)** | Dispara o e-mail com o guia quando a condição é verdadeira |
| **No Operation, do nothing** | Finaliza o ramo em que a condição não foi atendida |

## 04 // Funcionamento na prática

### Cenário A — Usuário quer receber o guia

1. A pessoa preenche e envia o formulário.
2. O n8n grava suas respostas na planilha.
3. A condição identifica **“Sim, quero aprender mais”**.
4. O Gmail envia automaticamente o guia de automações com n8n.

```mermaid
flowchart LR
    A["Formulário"] --> B["Google Sheets"] --> C["Interesse confirmado"] --> D["Gmail: envio do guia"]
    classDef etapa fill:#14212e,stroke:#00DDEF,color:#fff
    classDef final fill:#142a1c,stroke:#4CFB2B,color:#fff
    class A,B,C etapa
    class D final
```

### Cenário B — Usuário não solicita o guia

1. A pessoa preenche e envia o formulário.
2. O n8n grava suas respostas na planilha.
3. A condição não é atendida.
4. O fluxo encerra a execução sem enviar o material.

```mermaid
flowchart LR
    A["Formulário"] --> B["Google Sheets"] --> C["Interesse não confirmado"] --> D["Fim do fluxo"]
    classDef etapa fill:#14212e,stroke:#00DDEF,color:#fff
    classDef final fill:#302108,stroke:#FFE600,color:#fff
    class A,B,C etapa
    class D final
```

## 05 // Tecnologias utilizadas

| Tecnologia | Aplicação no projeto |
|---|---|
| **n8n** | Orquestração do fluxo e execução das condições |
| **n8n Forms** | Captura das respostas do formulário |
| **Google Sheets** | Armazenamento centralizado das informações |
| **Gmail** | Envio automatizado do guia aos interessados |

## 06 // Decisões técnicas

**Registro antes da decisão.** A resposta é salva no Google Sheets antes da verificação de interesse. Assim, o registro de submissões não depende do envio do material.

**Separação entre cadastro e entrega.** A captação de dados e o envio de conteúdo têm responsabilidades próprias, conectadas por uma condição simples e explícita.

**Roteamento condicional.** O nó `If` determina se o Gmail será acionado. A decisão segue uma regra de negócio objetiva, sem necessidade de intervenção manual.

**Integrações nativas.** O uso dos nós do n8n para Google Sheets e Gmail simplifica a comunicação entre serviços e a manutenção do fluxo.

---

<div align="center">

<img src="./assets/HUD Cyberpunk Fim da Transmissão Animado.gif" alt="Fim da Trasmissão" width="100%" />

</div>
