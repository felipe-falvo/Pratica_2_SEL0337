# SEL0337 — Projetos em Sistemas Embarcados
## Prática 2: Instalação e Configuração de Sistema Operacional em Sistemas Embarcados

---

## Informações

- **Plataforma Hardware:** Raspberry Pi 3 Model B Plus Rev 1.3 (Broadcom BCM2837B0)
- **Sistema Operacional:** Debian GNU/Linux 13 (trixie) aarch64 (Raspberry Pi OS 64-bit)
- **Identificação do Kit:** Kit Nº RPI3B+#7
- **Integrantes:**
  - Felipe Assis Bernardes Falvo — Nº USP: 15004433
  - Kayke Malaquias Gregorio — Nº USP: 15651561

---

## Prática

### 1. Gravação do Sistema Operacional e Boot
1. Cartão MicroSD conectado ao PC.
2. Utilizado o Raspberry Pi Imager com as definições:
   - Dispositivo: Raspberry Pi 3
   - Sistema Operacional: Raspberry Pi OS (64-bit) 
3. Configurações:
   - Hostname: raspberrypi
   - Usuário: sel
   - Senha: usp
4. Gravação executada com sucesso.
5. A senha do usuário administrador foi alterada com o comando:

    sudo passwd root

---

### 2. Conexão à Rede Wi-Fi e Habilitação de Interfaces
A placa foi conectada à rede sem fio LabMicros. Em seguida, o painel de configuração foi usado para habilitar as comunicações SSH e VNC:

    sudo raspi-config

Após reiniciado, os endereços IP foram verificados para possibilitar o acesso remoto posterior:

    ifconfig
    ip addr

---

### 3. Informações de hardware e software
Como o neofetch estava indisponível, foi usado o fastfetch.

    sudo apt install fastfetch
    fastfetch
    pinout

**Dados:**
- **OS:** Debian GNU/Linux 13 (trixie) aarch64
- **Host:** Raspberry Pi 3 Model B Plus Rev 1.3
- **Kernel:** Linux 6.18.34+rpt-rpi-v8
- **Arquitetura / Versão ARM:** aarch64 (ARMv8 64-bit)
- **SoC:** Broadcom BCM2837
- **CPUs:** 4 núcleos (Quad-Core) @ 1.40 GHz
- **RAM:** 1GB
- **Armazenamento:** MicroSD
- **Rede:** Gigabit Ethernet over USB 2.0 (máx. 300Mbps) e Wi-Fi nativo

**Requisito para rodar Linux Embarcado:**

Analisando as informações do fastfetch, nota-se um sistema operacional robusto e de multitarefa, que é o Debian GNU/Linux. Assim, tem-se que é necessário possuir uma MMU (Memory Management Unit) no processador para conseguir rodar um SO dessa complexidade.

Portanto, a relação entre possuir o Linux e a necessidade de ter uma MMU está na ideia do isolamento de memória, visto que para organizar diversos de processos ao mesmo tempo e de forma estável, o sistema operacional precisa garantir que um programa não interfira na memória de outro. Logo, A MMU cria uma ideia de que o software possui uma memória RAM própria, contínua e exclusiva para ele (memória virtual). Na prática, os programas dividem o esforço da CPU e rodam juntos de forma isolada nas suas memórias virtuais, não podendo acessar o hardware (pinos da placa) diretamente. Assim, sempre que for necessário mexer em um pino, é necessário pedir para o núcleo do sistema, o que acaba gerando atraso de processamento.

Já os microcontroladores que não possuem MMU, acessam a memória física de forma direta. Assim, sem a MMU, eles não conseguem criar memória virtual, não podendo isolar os programas, o que torna impossível rodar sistemas operacionais como o Linux.

---

### 4. Acesso Remoto (VNC e SSH)
Para validar a comunicação na rede, foram realizados testes práticos de acesso remoto em duas etapas:

1. Primeiro, foi realizado o acesso gráfico com o celular utilizando o aplicativo do VNC Viewer, como visto na imagem remoto.jpeg.
2. Em seguida, foi estabelecido o acesso via terminal remoto (SSH) conectando em outra placa Raspberry Pi do laboratório:

    ssh sel@192.168.1.102

3. Dentro da sessão SSH na placa remota, foi criado um arquivo de texto para a validação:

    nano teste.txt

4. Por fim, foi feita a verificação presencial diretamente no monitor onde a placa remota estava conectada. Confirmou-se (com o comando ls) que o arquivo teste.txt foi criado (conforme visto na imagem teste_outra_rasp).

---

### 5. Geração de Histórico e Atualização de Kernel

O histórico dos comandos da sessão foi solicitado:

history

*Observação importante:* Vale mencionar que o comando `history` no terminal não mostrou corretamente os comandos de forma correta, ou seja, ele ignorou praticamente todos os comandos realizados. Por isso que foi criado esse repositório, para mostrar as fotos tiradas durante a prática, servindo como prova de que todos os testes foram realizados.

Em seguida, foi executada a atualização.

sudo rpi-update cac01bed1224743104cb2a4103605f269f207b1a#6.1.54

Finalizada a prática, a placa foi desligada.

sudo poweroff

---

## 📸 Imagens da prática

- **fastfetch.jpeg**: Execução do fastfetch mostrando o sistema operacional e uso de memória.
- **pinout.jpeg**: Execução do pinout para mostrar as especificações da placa Raspberry Pi 3B+.
- **ipconfig.jpeg** e **teste_outra_rasp.jpeg**: Retorno dos comandos ifconfig e ip addr
- **ssh.jpeg**: Autenticação e acesso do SSH.
- **remoto.jpeg**: Comprovação do acesso remoto com o celular com o VNC Viewer.
- **history.jpeg**: Histórico do terminal.

---

## 💻 Histórico

Aqui seria o histórico certo caso ao aplicar o `history` certo no terminal, deveria aparecer:


    1  sudo passwd root
    2  sudo raspi-config
    3  reboot
    4  sudo apt update
    5  sudo apt install neofetch
    6  sudo apt install fastfetch
    7  fastfetch
    8  pinout
    9  ifconfig
    10  ip addr
    11  sudo raspi-config
    12  ssh sel@192.168.1.102
    13  hostname -
    14  hostname -i
    15  hostname -I
    16  cd Desktop/
    17  ls
    18  nano
    19  cd ..
    20  ssh sel@192.168.1.106
    21  cd Documents/
    22  ls
    23  sudo rpi-update cac01bed1224743104cb2a4103605f269f207b1a#6.1.54
    24  history
    25  sudo poweroff

---
