# Permissões de Arquivos
O comando  **chmod  -R 777**   defini que um  arquivo possui permissões de leitura, gravação e execução para proprietário, grupo e quaisquer usuários. Na forma :
```
-rwxrwxrwx
```

## Entendendo permissões
No mundo **Linux**  o acesso aos arquivos é controlada pelo Sistema Operacional usando permissões de arquivos, atributos e propriedades. Este modelo permite restringer acesso a arquivos e diretórios, permitindo somente usuários e processo autorizados.
### Tipos de Permissão
Existem três tipos de permissão
- Permiisão de leitura
	-  O usuário só pode ler o conteúdo do arquivo
- Permissão de gravação:
	- O arquivo pode ser alterado ou modificado, podendo criar um novo arquivo, excluir arquivos, mover, copiar, etc.
- Permissão de execução:
	- O usuário pode executar um script binário.

Para visualizar o tipo de permissão utilizamos o comando **ls**

``` shell
	ls -l forteste.py
```

``` saida
-rw-r-r --1 user group 288 set 14 23:43 forteste.py
```

O primeiro caractere indica o tipo do arquivo que pode ser, arquivo regular(-) , diretório(-d), link simbólico(-l) ou qualquer outro tipo especial de arquivo.
Os trẽs primeiros caractere a seguir representam as permissões de arquivo sendo o priemiro mostrado as permissões de proprietário, o segundo sendo de groupo e o terceiro de outros usuários.

### Números de permissões
São representados em formato númerico ou simbólico.
Os números vão de  0 a 7:
- r (read) = 4
- w (write) = 2
- x (execute) = 1
- no permission = 0
Cada número é somado por exemplo as permissões do arquivo mostrado anteriormente é um 644.

Quando um número de 4 digitos é usado o priemeiro dígito represeta permissões especiais:
- setuid = 4: Quando definido em um executável, ele é executado com privilégios do arquivo.
- setguid = 2: Ele é executado em privilégio de grupo.
- sticky = 1: Apenas o proprietário do diretório ou root pode excluir ou renomear arquivos.

## Nunca utilize o chmod 777
O chmod significa que o arquivo é legível, gravável e executado por quaisquer usuário, isso é um grande risco de segurança.
Em servidores web devemos definir 644 para arquivos e 755 para diretórios
A propriedade do arquivo pode ser alterado com o comando chown e permissões com o comando chmod.
Digamos que eu tenha um aplicativo PHP em meu servidor de execução
```
chown -R linuxize: /var/www
find /var/www -type d -exec chmod 755 {} \;
find /var/www -type f -exec chmod 644 {} \;
```
Somente a raiz, o proprietário  ou usuários com privilégios sudo podem alterar as permissões de arquivos

## Entendendo Umask
O **umask** controla as permissões de arquivo e diretórios. Programas comumente solicitam 666 para arquivos e 777 para diretórios. O processo umask limpa os bits que são definidos na mascára. Se o diretório pai tiver um **ACL** padrão, esse ACL determinará o resultado o resultado. Com uma umask comum de 002 .
- Arquivos 644(leitura/escrita para proprietário, leitura para grupo e outros usuários).
- Arquivos 755(leitura/escirta/execução para proprietário, leitura/escrita para grupo e outros usuários).
``` Terminal
	umask
```

## Exemplos de permissão em comum

| Permissão    | Númerico | Significado                                                                   | Uso comum                                  |
| ------------ | -------- | ----------------------------------------------------------------------------- | ------------------------------------------ |
| -rwx------ - | 700      | Proprietário pode ler, escrever e executar                                    | Roteiros privados, diretórios domésticos.  |
| -rwxr-xr-x   | 755      | Proprietário pode ler, escrever, executar; grupo e outros pode ler e executar | Diretórios e scrips executáveis            |
| -rw-r--r--   | 644      | Proprietário pode ler e escrever; grupos e outros podem ler                   |                                            |
| -rw-rw-r-- - | 664      | Proprietário e grupos pode ler e escrever;  outros podem ler                  | Arquivos de projeto compartilhado          |
| -rw------- - | 600      | Proprietário pode ler e escrever                                              | Arquivos de configuração privados como SSH |
| -rw-rw---- - | 660      | Proprietário e grupos  pode ler e escrever                                    | Arquivos sensíveis compartilhados          |
| -rwxrwxrwx   | 777      | Todos podem ler, escrever e executar                                          | Nunca recomendado                          |
