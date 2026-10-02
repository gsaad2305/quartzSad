---
publish: true
---
# Entendendo o processo de boot do Linux
Entender o processo de boot e startup dos  prrocessos são importantes tanto para configuração , como para resolver problemas de inicialização.
Existem duas sequências de eventos para inicializar um computador LInux e torna-lo utilizável boot e startup. O boot começa quando o computador é ligado e termina quando o **Kernel** é inicializado e o **systemd** é executado. O processo startup assume o controle e finaliza a tarefa de colocar o sistema Linux em estado executável.
O sistema de boot do sistema e start é bastante simples de compreender. É  composto pelos seguintes passos que serão mais detalhados neste arquvio:
- BIOS POST
-  Boot Loader( GRUB2)
- Kernel Inicalization
- Systemd, The Parent of all Process.
##  The boot process
O processo de boot pode ser executado de duas maneiras ao ligar o computador ou ao ser renicialozado. O primeiro componente ae ntrar em ação é a BIOS(Basic/ Input/ Output System) ou o UEFI (Unified Extensible Firmware Interface).
### BIOS POST
O primeiro process a entrar em ação é a BIOS(Basic / Input / Output System) ou o UEFI(Unified Extensible Firmware Interface). Neste primeiro processo ocoore:
 - Incizalização e verficação dos componentes  de hadware, como processador, memória e dispositivos de entrada e saída.
 - Execução de Power-on Self Test (POST) para detectar possíveis falhas no hadware.
 - Identificação de dispostivos de inicalização.
 -  Transferência dos processos para o Boot Loader do Sistema Operacional.
### Boot Loader (GRUB2)
GRUB2 significa "GRand Unfied Bootloader version 2" e atulmente é o principal Boot Loader da maioria das distribuições Linux.
O GRUB2  foi projetado para ser compatível com o multiboot especification que permite a inicalozação de diversas distribuições LInux.
O GRUB permite a  escolha de diferentes kernels para o LInux, podendo escolher entre um kernel mais antigo ou um mais atual caso apresente algum problema ou seja incompatível. O GRUB ṕde ser configurado atráves do arquivo /boot/grub/grub.conf.
A sua principal função é carregar e executar o kernel do na memória.
Se o seu sistema estiver utilzando UEFI, ele irái operar dentro do ambiente EFI geralmente utilizando GRUB2 ou Systemd-boot.

### Kernel
Todos os kernels estão em formato autoextraível e compactado para economizar espaço. Os kernels estão localizados no diretorio /boot, juntamente com uma imagem do disco RAM e os mapas dos dispositivos do disco rígido.
Após o kernel ter sido carregado na memória e iniciar seu processo de execução. Em seguida ele precisa primeiro se extrair da versão compactada, para realizar qualquer operação útil. Uma vez extraído ele carrega o  [ Systemd](https://wiki.archlinux.org/title/Systemd) , que substituiu o antigo programa [ init SYSV](https://en.wikipedia.org/wiki/Init#SysV-style), e transfere o controle para ele.

## O processso de inicialização
### systemd
Após encontrar o sistema de arquivos raiz “real”, será verificado se há erros nele e se ele foi montado. Se esse procedimento for bem-sucedido, o `initramfs` será limpo e o **daemon `systemd`** no sistema de arquivos raiz será executado. O `systemd` é um gerenciador de serviços e sistemas do Linux. Trata-se do processo pai que é iniciado como **PID 1** e age como um sistema init que ativa e mantém os serviços no espaço do usuário
