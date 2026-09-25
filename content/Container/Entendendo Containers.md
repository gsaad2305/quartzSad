---
publish: false
---
Este documento começou a ser escrito em 14/09/2026, tem como finalidade documentar estudos sobres  **containers** e pontuar as diferenças entre containeres e virutalizações de máquinas.

## 1 . Definições
#### O que é o Docker?
O Docker é uma ferramenta projeta para facilitar a criação, implementação e execução de aplicativos utilizando containers. Docker foi feito para Linux, o Docker roda de forma nativa no kernel do Linux como os  **namespaces** (para isolamento)  e os **cgroups** (para controle de recursos)  ,enquanto Windows e Mac , precisam rodar uma "Virtualização" do kernel  Linux por de baixos dos panos para  rodar Docker por não ser nativos em seus Sistemas Operacionais.


![[schema.png]]

####  Diferenças entre VMs e Containers

De forma bastante resumida uma Máquina Virtual  recria um sistema operacional om tudo que o sistema operacional precisa, containers reaproveita a arquitertura do kernel da máquina.

## 2 - O que são  imagens de container?
Um container utiliza o padrão de imagens, uma imagem reune todos os componentes necessários para criar um container em um sistema operacional e compreende diferentes camadas de imagens empilhadas umas sobre as outras. As imagens de containers são imutáveis e compartilham as mesmas funções que os modelos.
### Como as imagens de containers são geradas
Imagens de containers é um acúmulo reunido de uma sucessão de camadas do sistema de arquivos é adicionada e empilhada  sobre a imagem base:
 - Bibliotecas: padrões de algoritimos e modelos de classes que os programadores podem utilizar para criar estruturas de dados comuns.
 - Binários: são  necessários para que arquivos executáveis para a implementação de diferentes programas e comandos.
 - Dependências:  governam a criação e a operação de containers
 - Arquivos de configuração:  configurações necessárias para executar o contâiner em questão

 A imagem de base é onde a maioria dos fluxos de trabalho de desenvolvimento baseados em containers começam. Muitas imagens compreendem dustibuições Linux básicas ou minímas O processo de criação de imagens de base permite que os desenvolvedores construam um ambiente compativel com imagens de containers padronizados.
#### Padrão OCI de imagens de containers
O OCI(Open Container Inciative) trata-se de uma especificação de código aberto que padroniza o formato das imagens de container para garantir que funciona de maneira idêntica em qualquer plataforma.
O padrão define em arquivo **JSON** que descreve os componentes das imagens.
Metadados que determinam como o container deve rodar em variáveis de ambientes, camadas de inicialização e arquitetura de CPU.

## 3 - Como funciona?

Um container é executado a partir de uma imagem. Uma imagem é construída usando um Dockerfile. Alguns comandos úteis:
 - Docker Hub um local que contém imagens base que você pode usar para executar um container
 - Execute um container:
	 ```
	 docker run -di --name saddev alpine:latest
	 -d desapegar
	 -i interativo
	 ```
- Conecta-se a um contâiner interativo com um shell
	 ```
	 docker run -ti saddev sh
	 -t: terminal
	 -i iterativo
	 ```
- Contentores de lista:
	```
	docker ps -a
	```
 - Criar imagens a partir do Dockerfile:
	  ```
	  docker build -t myimage:version
	  ```
 - Listar imagens:
	 ```
	 docker images
	 ```
- Remover imagem
	```
	docker image rm saddev:v1.0
	```

#### Pontos-chave:
 - Por padrão, qualquer container é executado com privilégios raiz. Isso significa que qualquer usuário que tenha acesso ao Docker Daemon tem privilégios de root do container.
 -  As vezes se quer remover um container e executa-lo novamente porque atualizou a imagem ou alterou o Dockerfile.


Agora, vamos supor que você é o administrador e você quer que seu amigo seja capaz de executar um container sem qualquer motivo. Você  o adiciona  ao seu grupo "docker" ou da a ele a capacidade de executar o docker como um sudo. Agora ele é capaz de lidar com ou site que você deseja que ele executa / mantenha.
Mas e se ele executar o comando: docker run -tid -v /etc/:mnt/ --name saddev alpine:latest bash.

É aqui onde surge um grande problema de segurança por que agora, o sistema de arquivo do container tem acesso aos arquivos de fora, toda a sua pasta raiz (/) está no diretório mnt. É possível criar um novo usuário root inserindo-o internamente no /etc/passwd arquivo.
(https://gtfobins.org/gtfobins/docker/)

## 4 - [Docker Compose](https://docs.docker.com/compose/)

O Docker Compose utiliza a configuração de arquivo YAML, para configurar os serviços de sua aplicação , criar e iniciar todos os serviços  que estão configurados, é uma forma bastante eficiente de definir e rodar múltiplos containers  para a aplicação obtendo uma experiência de desenvolvimento simples e eficiente.
O compose facilita o gerenciamento de services, networks e volumes dentro do arquivo de configuração  .yaml ou yml.

#### Exemplo de um arquivo compose
Digamos que você está criando um projeto que precise de um Banco de Dados PostgreSQL, você pode criar dentro da pasta do seu projeto um arquivo  **compose.yml** . Peguei este exemplo de um projeto pessoal meu onde utilizo um arquivo docker compose:

```docker-compose.yml
services:

	postgres:

		image: postgres:17-alpine

		container_name: postgres_db

		restart: always

		environment:

			POSTGRES_USER: USER

			POSTGRES_PASSWORD: PASS

				POSTGRES_DB: DB

		ports:

			- "5432:5432"

		volumes:

			- postgres_data:/var/lib/postgresql/data

volumes:

postgres_data:
```

Para iniciar o compose digite:
```
docker compose -up
```

 Para parar  um arquivo compose digite:
 ```
 docker compose down
 ```

Monitoramento das saídas dos container em execução e problemas de depuração:
```
docker compose logs
```

Listar todos os serviços que estão rodando:
```
docker compose ps
```
