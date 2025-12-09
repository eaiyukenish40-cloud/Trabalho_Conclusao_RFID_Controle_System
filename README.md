# Trabalho_Conclusao_RFID_Controle_System

Gerenciamento e Controle de Estoque usando RFID e IoT
Este repositório contém os códigos e a documentação do projeto de Gerenciamento e Controle de Estoque utilizando Identificação por Radiofrequência (RFID). O sistema foi desenvolvido como Trabalho de Conclusão de Curso (TCC) em Engenharia Elétrica na UNESP - Campus de Ilha Solteira.


📋 Visão Geral do Projeto
O objetivo deste projeto é desenvolver um sistema de baixo custo para o gerenciamento de estoque de uma indústria fictícia de cosméticos (aplicável a outros cenários). O sistema automatiza o controle de entrada e saída de produtos, substituindo processos manuais ou baseados em código de barras, garantindo maior agilidade e reduzindo erros humanos.


O sistema funciona através da leitura de tags RFID passivas fixadas nos produtos. Ao passarem pelos sensores (portais de entrada e saída), os dados são capturados por um microcontrolador com Wi-Fi integrado e enviados em tempo real para um banco de dados em nuvem (Google Planilhas), onde são processados e visualizados.


Principais Funcionalidades
Monitoramento em Tempo Real: Leitura de tags na entrada e saída do estoque.

Conectividade IoT: Envio de dados via Wi-Fi para a nuvem.

Banco de Dados em Nuvem: Uso do Google Planilhas para armazenar logs, cadastrar produtos e visualizar dashboards.


Tratamento de Dados: Lógica para identificar produtos novos, repetidos e controle de fluxo (entrada vs. saída).


Dashboard: Visualização gráfica da proporção de produtos e níveis de estoque.

🛠️ Hardware Utilizado
O projeto foi prototipado utilizando componentes de fácil acesso e baixo custo:


Microcontrolador: NodeMCU ESP8266 (Modelo ESP-12E) - Escolhido pelo Wi-Fi nativo e baixo consumo.



Leitores RFID: 2x Módulos RF-RC522 (Frequência 13.56 MHz - HF).




Tags: Tags passivas (padrão Mifare) em formatos de cartão e chaveiro.



Comunicação: Protocolo SPI para comunicação entre o ESP8266 e os leitores RFID.

Outros: Jumpers, Protoboard e Cabo USB.

💻 Software e Tecnologias Chaves
Linguagem de Programação

C++: Utilizado para a programação do firmware do microcontrolador ESP8266 através da IDE do Arduino.



Google Apps Script (JavaScript): Utilizado no back-end da planilha para receber as requisições HTTP do ESP8266 e manipular as células da planilha (lógica de cadastro e log).

Bibliotecas do Firmware (Arduino IDE)
As seguintes bibliotecas foram fundamentais para o funcionamento do código embarcado :


SPI.h: Para comunicação serial síncrona com os leitores RC522.

MFRC522.h: Para manipulação e leitura dos módulos RFID.

ESP8266WiFi.h: Para gerenciar a conexão Wi-Fi do NodeMCU.

WiFiClientSecure.h: Para realizar conexões seguras (HTTPS) com o servidor do Google.

HTTPSRedirect.h: Auxiliar para o envio de dados para o Google Sheets (redirecionamento de segurança).

🗃️ Estrutura do Banco de Dados (Google Sheets)
O sistema utiliza duas planilhas principais integradas:

Log: Recebe os dados brutos (UID da tag, data, hora, sensor de origem). Realiza o controle de fluxo (entrada/saída).

Produtos: Responsável pelo cadastro de novos produtos, vinculando um UID a um nome de produto específico.

🚀 Como Executar

Hardware: Monte o circuito conforme o esquema de ligação (conectar os pinos SPI do RC522 aos pinos correspondentes do ESP8266 - GPIOs 12, 13, 14, 15 etc.).

Google Script: Crie uma planilha no Google, acesse o Apps Script, cole o código de back-end (não incluído neste repo, verifique a documentação do Google para doGet ou doPost) e publique como aplicativo da web.

Firmware:

Instale a IDE do Arduino.

Adicione as bibliotecas listadas acima.

Insira suas credenciais Wi-Fi (ssid, password) e o ID do Script do Google (GOOGLE_SCRIPT_ID) no código main.ino .

Carregue o código no NodeMCU.

📄 Licença e Autoria

Autor: Gustavo Yuken Kawase Maizatto. Instituição: Universidade Estadual Paulista "Júlio de Mesquita Filho" (UNESP). Ano: 2023.
