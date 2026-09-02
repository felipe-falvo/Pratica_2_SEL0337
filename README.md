# SEL0337 — Projetos em Sistemas Embarcados
## Prática 2: Instalação e Configuração de Sistema Operacional em Sistemas Embarcados

Repositório de documentação, comandos executados e respostas teóricas da Prática 2 da disciplina SEL0337 (EESC-USP).

---

## 📋 Informações Gerais

- **Plataforma Hardware:** Raspberry Pi 3 Model B Plus Rev 1.3 (Broadcom BCM2837B0)
- **Sistema Operacional:** Debian GNU/Linux 13 (trixie) aarch64 (Raspberry Pi OS 64-bit)
- **Identificação do Kit:** Kit Nº RPI3B+#7
- **Integrantes:**
  - Felipe Assis Bernardes Falvo — Nº USP: 15004433
  - Kayke Malaquias Gregorio — Nº USP: 15651561

---

## 🎯 Objetivos

1. Gravação de imagem do Raspberry Pi OS.
2. Configuração do Wi-Fi.
3. Habilitação de comunicação remota (SSH e VNC).
4. Análise das informações de hardware (fastfetch, pinout).
5. Atualização com commit com rpi-update.

---

## 🛠️ Roteiro

### 1. Gravação do Sistema Operacional
1. Cartão MicroSD conectado ao PC da bancada.
2. No Raspberry Pi Imager:
   - Dispositivo: Raspberry Pi 3
   - Sistema Operacional: Raspberry Pi OS (64-bit) (com interface gráfica)
3. Configurações prévias:
   - Hostname: raspberrypi
   - Usuário: sel
   - Senha: usp
4. Gravação executada com sucesso.

---

### 2. Primeiro Boot e Hardening de Segurança (Root)
Com os periféricos e o MicroSD conectados, a placa foi ligada. No terminal local, a senha do usuário administrador foi alterada imediatamente para evitar acessos não autorizados assim que a placa se conectasse à rede:

sudo passwd root

---

### 3. Conexão à Rede Wi-Fi e Habilitação de Interfaces
A placa foi conectada à rede LabMicros e as interfaces de comunicação foram habilitadas através do painel de configuração:

sudo raspi-config

(Opções ativadas: SSH e VNC).

Após o reinício (reboot), os endereços de rede foram verificados:

ifconfig
# Endereço IP obtido na interface wlan0: 192.168.1.106 / 192.168.1.102

---

### 4. Diagnóstico de Hardware e Software

Atualização dos repositórios e instalação da ferramenta de telemetria:

sudo apt update
sudo apt install neofetch   # Pacote indisponível no repositório atual
sudo apt install fastfetch  # Executado com sucesso
fastfetch
pinout

Síntese dos Dados Extraídos:
- OS: Debian GNU/Linux 13 (trixie) aarch64
- Host: Raspberry Pi 3 Model B Plus Rev 1.3
- Kernel: Linux 6.18.34+rpt-rpi-v8
- SoC: BCM2837 (4) @ 1.40 GHz
- RAM: 1GB
- Rede: Gigabit Ethernet over USB 2.0 (máx. 300Mbps) e Wi-Fi nativo

Requisito Chave para rodar Linux Embarcado:
Para rodar um SO complexo como o Linux, o hardware exige obrigatoriamente uma MMU (Memory Management Unit). A MMU viabiliza o uso de memória virtual, isolando os processos de usuário (User Space) do núcleo do sistema (Kernel Space). Microcontroladores não rodam Linux completo (como o Debian) pois não contam com MMU, operando diretamente na memória física.

---

### 5. Acesso Remoto (SSH)

Validação do acesso remoto partindo de outro terminal na mesma rede:

ssh sel@192.168.1.102
ssh sel@192.168.1.106

A autenticidade dos hosts foi confirmada e o acesso via terminal remoto foi estabelecido com sucesso.

---

### 6. Atualização Específica de Kernel e Exportação

Para nivelar a versão do kernel com as próximas práticas, executou-se a atualização via commit fixo:

sudo rpi-update cac01bed1224743104cb2a4103605f269f207b1a#6.1.54

*Observação sobre o registro de comandos:* Ao executar o comando `history` no final da prática, o terminal não exibiu a totalidade dos comandos inseridos durante a sessão (como as tentativas de conexão SSH). Os comandos ausentes no log automático foram documentados manualmente ao longo deste roteiro para refletir todos os passos realizados.

Finalizada a prática, o sistema foi desligado com segurança:

sudo poweroff

---

## 📸 Evidências Práticas (Anexos)

Junto a esta entrega, estão anexadas as imagens comprobatórias da execução da prática no laboratório, incluindo:
- **WhatsApp Image 2026-08-31 at 11.25.34(2)_2.jpeg**: Execução bem-sucedida do `fastfetch` detalhando o sistema operacional e uso de memória.
- **WhatsApp Image 2026-08-31 at 11.25.48_2.jpeg**: Execução do `pinout` mapeando as especificações da placa Raspberry Pi 3B+.
- **WhatsApp Image 2026-08-31 at 11.26.17_2.jpeg / 11.29.03_2.jpeg**: Retorno dos comandos `ifconfig` e `ip addr` confirmando os IPs alocados via Wi-Fi.
- **WhatsApp Image 2026-08-31 at 11.27.36_2.jpeg**: Autenticação e acesso remoto confirmados via SSH.
- **WhatsApp Image 2026-08-31 at 11.27.49(1)_2.jpeg**: Histórico parcial do terminal (`history`) registrando configurações de root, atualização de kernel e ferramentas instaladas.

---
