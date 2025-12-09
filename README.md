# Gerenciamento e Controle de Estoque usando RFID e IoT

Este repositório contém os códigos fonte e a documentação técnica do projeto de **Gerenciamento e Controle de Estoque utilizando Identificação por Radiofrequência (RFID)**.

Este projeto foi desenvolvido como Trabalho de Conclusão de Curso (TCC) em Engenharia Elétrica na **UNESP - Campus de Ilha Solteira**.

## 📋 Visão Geral do Projeto

O objetivo deste projeto é desenvolver um sistema de baixo custo para o gerenciamento de estoque, utilizando como estudo de caso uma indústria fictícia de cosméticos. O sistema visa substituir processos manuais e códigos de barras por uma solução automatizada que garante maior agilidade na contagem e reduz erros humanos.

### Como Funciona
O sistema utiliza tags RFID passivas fixadas nos produtos. Ao passarem pelos portais de leitura (entrada e saída), os dados são capturados por um microcontrolador ESP8266 e enviados via Wi-Fi para um banco de dados em nuvem (Google Planilhas).

### Principais Funcionalidades
* **Monitoramento Automático:** Leitura de tags na entrada e saída do estoque sem necessidade de "visada direta" (como no código de barras).
* **Conectividade IoT:** Envio de dados em tempo real via Wi-Fi.
* **Banco de Dados em Nuvem:** Integração direta com Google Planilhas para armazenamento e tratamento de dados.
* **Dashboard de Gestão:** Visualização da proporção de produtos, níveis de estoque e histórico de movimentação.

## 🛠️ Hardware Utilizado

O protótipo foi construído utilizando componentes de hardware livre e acessível:

* **Microcontrolador:** NodeMCU ESP8266 (Modelo ESP-12E) - Responsável pelo processamento e conexão Wi-Fi.
* **Leitores RFID:** 2x Módulos MFRC522 (Frequência 13.56 MHz - HF).
* **Tags RFID:** Tags passivas padrão Mifare (Cartão e Chaveiro).
* **Outros:** Jumpers, Protoboard e Cabo USB para alimentação e programação.

## 💻 Tecnologias e Software

### Linguagem de Programação
* **C++:** Utilizado para o firmware do ESP8266 através da IDE do Arduino.
* **Google Apps Script (JavaScript):** Utilizado no back-end da planilha para receber as requisições HTTP, processar os dados e gerenciar as abas da planilha.

### Bibliotecas Principais (Firmware)
As seguintes bibliotecas foram utilizadas no código do microcontrolador:

* `SPI.h`: Para comunicação serial síncrona com os leitores RC522.
* `MFRC522.h`: Para controle e leitura dos módulos RFID.
* `ESP8266WiFi.h`: Para gerenciamento da conexão Wi-Fi do ESP8266.
* `WiFiClientSecure.h`: Para realizar conexões seguras (HTTPS) com o Google.
* `HTTPSRedirect.h`: Auxilia no redirecionamento e envio de dados para o Google Sheets.

## 🗃️ Estrutura do Banco de Dados

O sistema opera com planilhas integradas no Google Sheets:

1.  **Log (Dados Brutos):** Registra data, hora, UID da tag e qual sensor realizou a leitura (Entrada/Sensor 0 ou Saída/Sensor 1).
2.  **Produtos (Cadastro):** Vincula o UID da tag ao nome do produto específico.
3.  **Dashboards:** Tabelas dinâmicas e gráficos para visualização do status do estoque.

## 🚀 Instalação e Configuração

### 1. Montagem do Hardware
Conecte os leitores RC522 ao ESP8266 via protocolo SPI. O projeto utiliza pinos compartilhados para `RST`, `CLK`, `MISO`, `MOSI`, com pinos `SDA` (SS) dedicados para cada leitor.

### 2. Configuração do Google Sheets
1.  Crie uma nova planilha no Google.
2.  Acesse `Extensões > Apps Script`.
3.  Implemente o script para receber requisições `GET`/`POST`.
4.  Publique o script como "Aplicativo da Web" e copie o **Script ID**.

### 3. Firmware (ESP8266)
1.  Abra o arquivo `.ino` na Arduino IDE.
2.  Instale as bibliotecas necessárias listadas acima.
3.  Altere as variáveis de credenciais:
    ```cpp
    const char* ssid = "SEU_WIFI";
    const char* password = "SUA_SENHA";
    String GOOGLE_SCRIPT_ID = "SEU_SCRIPT_ID";
    ```
4.  Faça o upload para a placa.

## 📄 Licença e Autoria

**Autor:** Gustavo Yuken Kawase Maizatto.
**Orientadora:** Profa. Suely Cunha Amaro Mantovani.
**Instituição:** UNESP - Faculdade de Engenharia de Ilha Solteira.
**Ano:** 2023.

---
*Este projeto foi desenvolvido para fins acadêmicos como requisito para obtenção do título de Engenheiro Eletricista.*
