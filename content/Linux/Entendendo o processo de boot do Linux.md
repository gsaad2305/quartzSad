---
publish: true
---
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
### MBR
MBR significa Master Boot Record e é responsável por carregar e executar o carregador de inicialização GRUB.
O MBR está localizado no 1° setor do disco inicializável, que normalmente é **/dva/hda** ou **/dev/sda**, dependendo do seu hardware. O MBR também contém informações sobre o GRUB, ou LILO em sistemas muitos antigos.
### Boot Loader (GRUB2)
GRUB2 significa "GRand Unfied Bootloader version 2" e atulmente é o principal Boot Loader da maioria das distribuições Linux.
O GRUB2  foi projetado para ser compatível com o multiboot especification que permite a inicalozação de diversas distribuições LInux.
O GRUB permite a  escolha de diferentes kernels para o LInux, podendo escolher entre um kernel mais antigo ou um mais atual caso apresente algum problema ou seja incompatível. O GRUB ṕde ser configurado atráves do arquivo /boot/grub/grub.conf.
A sua principal função é carregar e executar o kernel do na memória.
Se o seu sistema estiver utilzando UEFI, ele irái operar dentro do ambiente EFI geralmente utilizando GRUB2 ou Systemd-boot.
![[grub-bootloader.jpg|698]]
### Kernel
Todos os kernels estão em formato autoextraível e compactado para economizar espaço. Os kernels estão localizados no diretorio /boot, juntamente com uma imagem do disco RAM e os mapas dos dispositivos do disco rígido.
Após o kernel ter sido carregado na memória e iniciar seu processo de execução. Em seguida ele precisa primeiro se extrair da versão compactada, para realizar qualquer operação útil. Uma vez extraído ele carrega o  [ Systemd](https://wiki.archlinux.org/title/Systemd) , que substituiu o antigo programa [ init SYSV](https://en.wikipedia.org/wiki/Init#SysV-style), e transfere o controle para ele.

### Initrd/Initramfs
Initrd é um acrônimo para Initial Ram Disk. Ele é um arquivo compactado que, assim como o kernel, que fica armazenado dentro do diretório /boot:
![[image-3.png]]

O arquivo **vmlinuz-4.14-x86_64** é o Kernel. Já o arquivo **initramfs-4.14-x86_64.img** é o arquivo de initrd.
A função deste arquivo, é ser um compilador de drivers e dependências para que o sistema operacional normalmente. Por exemplo, se temos um sistema de arquivos Ext4, precisamos de um driver Ext4 rodando para que o sistema operacional consiga se comunicar com o sistema de arquivos.
Então durante o processo de boot , o initrd é montado como um sistema de arquivos **temporário**. Depois, ele é extraído e todos os drivers são carregados para a memória.
Finalizando este processo, com todos os drivers e dependências na memória, finalmente é  montado o sistema de arquivos root, ou o famoso / .

### Init
Depois que tudo está montado e pronto para iniciar o carregamento do sistema, o Kernel entrega a segunda parte para o processo init, o primeiro processo do sistema operacional com **PID 1**.
A função do init é carregar todos os outros serviços como MySQL, Apache, DHCP,  Interface Gráfica, enfim, todos os processos.
Entretanto o init só saberá o que ele deve iniciar com base no nível de execução do sistema padrão que foi definido ( também conhecido como runlevel ).

### Runlevel
O runlevel indica o modo de operação atual da máquina, definindo quais serviços e recursos devem iniciar imediatamente e quais devem permanecer ativos. Basicamente, cada número do runlevel a um conjunto de softwares que irão iniciar juntamente com a máquina naquele momento. A maioria das distros linux inicia com o runlevel 5, ou seja multiusuários, conectado á internet, com o servidor gráfico executando e etc.
No Linux, os runlevels são numerados de 0 a 6. No nível 0 o sistema parado, nenhum processo é executado. Este modo entra em ação quando desligamos o sistema via software com o comando :

```
$#halt 
```

Os níveis são:

| Runlevel | Descrição                                                                                       |
| -------- | ----------------------------------------------------------------------------------------------- |
| 0        | Desligamento do sisetema                                                                        |
| 1        | Modo monousuário                                                                                |
| 2-5      | Modos multiusuário (tem diferentes utilizações variando de acordo com a distribuição utilizada) |
| 6        | Reinicialização do sistema                                                                      |

Para consultar seu runlevel atual, rode no terminal:
```
$runlevel
```

Apesar do SystemD ser o novo daemon gestor de sistema, o scripts do init continua compatíveis e vários deles são reaproveitados por questão de praticidade. O usuário pode trocar de runlevel e qualquer momento utilizando um link simbólico do init para o runlevel do SystemD, com o comando:
```
$sudo init 1
```
Basta trocar por qualquer número entre 0 e 6.
Lembrando das consequências, por exemplo, Init 1 deixará o sistema em modo de segurança enquanto o 6 vai reiniciá-lo.

### Conclusão
Uma vez que os processos iniciam a conexão á internet, servidor de impressão, servidor gráfico, etc, surge sua tela de login. Então você põe sua senha e usufrui de um sistema que carregou em menos de 2 minutos fazendo um esforço hercúleo para se erguer sobre _as próprias botas_.
