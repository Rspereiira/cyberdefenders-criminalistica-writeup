# 🕵️ DFIR Investigation - The Crime Lab

## 📌 Overview

Este projeto documenta uma investigação forense digital realizada a partir da análise de artefatos extraídos de um dispositivo Android.

A investigação foi conduzida com a ferramenta **ALEAPP (Android Logs Events And Protobuf Parser)**, com foco na identificação de evidências, correlação de artefatos e reconstrução da sequência de eventos observada no caso.

---

## 🎯 Objective

O objetivo deste projeto foi analisar os dados extraídos do dispositivo para identificar elementos relevantes da investigação, como:

* aplicativos instalados
* mensagens SMS
* contatos
* localização
* arquivos de mídia
* dados recuperados de arquivos **SQLite WAL**

---

## 🛠️ Tools Used

* ALEAPP
* SQLite Database Analysis
* SHA-256 Hash
* Android Artifact Analysis

---

## 📂 Evidence Source

Os artefatos analisados foram extraídos de um dispositivo Android e incluem diferentes fontes de evidência, como:

* aplicativos instalados no dispositivo
* banco de dados SQLite contendo SMS e contatos
* diretórios de mídia e downloads
* arquivos **WAL (Write-Ahead Logging)**

Esses dados foram processados e interpretados com apoio da ferramenta **ALEAPP**.

---

## 🔍 Step 1 - Installed Applications Analysis

A análise inicial foi feita sobre os aplicativos instalados no dispositivo.

Foi identificado o aplicativo:

* **Olymp Trade**
* Package: `com.ticno.olymptrade`

A presença desse aplicativo pode indicar atividade financeira relevante dentro do contexto investigativo.

![Installed Apps](screenshots/olymp_trade.png)

Após a identificação do aplicativo, foi observado o **SHA-256 Hash**, permitindo validar a integridade do artefato e possibilitando futura correlação com outras fontes de análise.

![SHA-256 Hash](screenshots/sha256_hash.png)

---

## 📩 Step 2 - SMS Analysis

Na análise dos registros de mensagens SMS, foi encontrada uma mensagem com possível conteúdo de coerção financeira.

* Valor mencionado: **250.000 EGP**

Esse artefato sugere a existência de uma cobrança com tom de ameaça ou pressão, o que torna a mensagem relevante para a investigação.

![SMS Evidence](screenshots/sms_threat.png)

---

## 👤 Step 3 - Contact Identification

A partir da base de contatos do dispositivo, foi identificado um contato relevante para o caso:

* **Nome:** Shady Wahab
* **Telefone:** +20 117 213 7258

Esse contato pode estar relacionado aos demais elementos encontrados durante a investigação, especialmente no contexto da cobrança identificada anteriormente.

![Contact](screenshots/contact_shady_wahab.png)

---

## 📍 Step 4 - Location Analysis

Na análise da seção de **Recent Activity**, foi encontrada uma imagem indicando uma possível localização associada ao dispositivo:

* **Local:** The Nile Ritz-Carlton
* **Cidade:** Cairo

Esse artefato sugere que o usuário esteve, ou ao menos registrou atividade, nessa localização durante o período analisado.

![Location](screenshots/location_cairo.png)

---

## ✈️ Step 5 - Travel Evidence

Durante a análise do sistema de arquivos, foi identificado um artefato relevante dentro do diretório de downloads:

* Caminho encontrado:
  `/data/media/0/Download/PlaneTicket.png`

A imagem encontrada corresponde a uma passagem aérea com o seguinte trajeto:

* **Origem:** Cairo
* **Destino:** Las Vegas

Essa evidência indica deslocamento internacional e amplia a relevância dos achados anteriores.

![Flight Ticket](screenshots/flight_ticket.png)

---

## 🧪 Step 6 - SQLite WAL Analysis

A etapa mais avançada da análise envolveu arquivos **SQLite Journal & WAL**, com foco na recuperação de dados não persistidos no banco principal.

Os arquivos **WAL (Write-Ahead Logging)** podem armazenar informações temporárias ou residuais que ainda não foram gravadas definitivamente no banco SQLite, sendo uma fonte valiosa em análise forense.

Durante essa etapa, foi localizado o arquivo `a-wal`, que foi aberto para investigação adicional.

Imagem da análise inicial do arquivo WAL:

![WAL Extraction](screenshots/wal_extraction.png)

Em seguida, foi aplicado um filtro de busca utilizando a palavra-chave **"meet"**.

Como resultado, foi identificada a seguinte informação:

> "We'll meet at The Mob Museum"

Esse achado indica o planejamento de um encontro em local específico, o que adiciona contexto importante à investigação.

Resultado da busca por palavra-chave:

![WAL Keyword Search](screenshots/wal_keyword.png)

---

## 📊 Timeline Reconstruction

| Ordem | Evento                                                |
| ----- | ----------------------------------------------------- |
| 1     | Identificação de mensagem com cobrança de dívida      |
| 2     | Identificação do aplicativo Olymp Trade               |
| 3     | Identificação do contato Shady Wahab                  |
| 4     | Registro de possível localização em Cairo             |
| 5     | Descoberta de passagem aérea para Las Vegas           |
| 6     | Identificação de encontro planejado no The Mob Museum |

---

## 🧠 Analysis

A correlação dos artefatos analisados permite construir uma sequência lógica de eventos.

Primeiro, foi identificada uma mensagem SMS com referência a uma dívida no valor de **250.000 EGP**, sugerindo um cenário de pressão financeira. Em seguida, foi localizado um contato relevante, **Shady Wahab**, potencialmente relacionado ao contexto da mensagem.

Na continuidade da análise, foi observada uma possível localização vinculada ao dispositivo em **The Nile Ritz-Carlton**, no Cairo. Depois disso, foi encontrada uma imagem de passagem aérea indicando viagem de **Cairo para Las Vegas**, o que sugere deslocamento internacional associado ao caso.

Por fim, a análise do arquivo **SQLite WAL** revelou a frase **"We'll meet at The Mob Museum"**, indicando um encontro previamente planejado.

Em conjunto, esses artefatos sugerem um cenário envolvendo coerção financeira, movimentação internacional e organização de encontro em local específico.

---

## 🚨 Key Findings

* Identificação de aplicativo com possível relevância financeira
* Evidência de possível coerção financeira via SMS
* Identificação de contato potencialmente relacionado ao caso
* Registro de possível localização do usuário em Cairo
* Evidência de deslocamento internacional para Las Vegas
* Indício de encontro planejado no local **The Mob Museum**

---

## 🔐 Evidence Validation

* Os artefatos foram analisados com a ferramenta **ALEAPP**
* A integridade de evidências foi observada por meio de **SHA-256 Hash**
* Dados adicionais foram recuperados a partir de arquivos **SQLite WAL**
* As evidências foram correlacionadas entre diferentes fontes do dispositivo

---

## 🧠 Skills Demonstrated

* Mobile Forensics (Android)
* Artifact Analysis with ALEAPP
* SQLite Database Analysis
* WAL File Investigation
* Evidence Correlation
* Timeline Reconstruction
* Investigative Documentation

---

## 📎 Conclusion

A investigação permitiu identificar uma sequência consistente de evidências digitais envolvendo comunicação suspeita, contato relevante, possível localização, viagem internacional e planejamento de encontro.

Este projeto demonstra a capacidade de conduzir uma análise forense estruturada em ambiente Android, correlacionando múltiplos artefatos para reconstrução de um cenário investigativo.
