# Docker: Ferramenta essencial para Desenvolvedores (Udemy)

https://www.udemy.com/curso-docker/learn/v4/overview

"No curso você aprenderá os principais conceitos do Docker com vários exercícios práticos, todos descritos detalhadamente na apostila que será disponibilizada no curso. Tudo que for ministrado no curso estará disponível na apostila, e ter esse suporte a mais, será um diferencial fantástico."

## <a name="indice">Índice</a>

1. [Seção: 1 - Introdução (5)](#parte1)     
2. [Seção: 2 - Conceitos (6)](#parte2)     
3. [Seção: 3 - Instalação (4)](#parte3)     
4. [Seção: 4 - Uso Básico do Docker (14)](#parte4)     
5. [Seção: 5 - Deixando de Ser Apenas um Usuário (11)](#parte5)     
6. [Seção: 6 - Redes (4)](#parte6)     
7. [Seção: 7 - Coordenando Múltiplos Containers (2)](#parte7)     
8. [Seção: 8 - Projeto Cadastro Simples (3)](#parte8)     
9. [Seção: 9 - Projeto para Envio de E-mails com Workers (11)](#parte9)     
---

## <a name="parte1">Seção: 1 - Introdução (5)</a>

- [Mateiral do Curso/Instrutor](https://github.com/josemalcher/curso-docker)

- [PDF do curso](http://files.cod3r.com.br/apostila-docker.pdf)[ ou PDF do curso local](https://github.com/ClaudioMendonca-Eng/Udemy-Docker-Ferramenta-essencial-para-Desenvolvedores/blob/main/pdf/Apostila-Docker.pdf)

[Voltar ao Índice](#indice)

---

## <a name="parte2"> Seção: 2 - Conceitos (6)</a>

#### 1.1. O que é Docker?

É uma ferramenta que se apoia em recursos existentes no kernel, inicialmente Linux, para isolar a execução de processos. As ferramentas que o Docker traz são basicamente uma camada de administração de containers, baseado originalmente no LXC.

Alguns isolamentos possíveis:
- Limites de uso de memória
- Limites de uso de CPU
- Limites de uso de I/O
- Limites de uso de rede
- Isolamento da rede (que redes e portas são acessíveis)
- Isolamento do file system
- Permissões e Políticas
- Capacidades do kernel

Podemos concluir dizendo que estes recursos já existiam no kernel a um certo tempo, o que o Docker nos trouxe foi uma maneira simples e efetiva de utiliza-los.
- https://www.docker.com/what-docker

Containers Docker empacotam componentes de software em um sistema de arquivos completo, que contêm tudo necessário para a execução: código, runtime, ferramentas de sistema - qualquer coisa que possa ser instalada em um servidor.

Isto garante que o software sempre irá executar da mesma forma, independente do seu ambiente.

#### 1.2. Por que não uma VM?

O Docker tende a utilizar menos recursos que uma VM tradicional, um dos motivos é não precisar de uma pilha completa como vemos em Comparação VMs × Containers. O Docker utiliza o mesmo
kernel do host, e ainda pode compartilhar bibliotecas.

Mesmo utilizando o mesmo kernel é possível utilizar outra distribuição com versões diferentes das bibliotecas e aplicativos.

![](img/comparacao-vms×containers.png)

Virtual Machine (máquina virtual), recurso extremamente usado atualmente para isolamento de serviços, replicação e melhor aproveitamento do poder de processamente de uma máquina física.

Devo trocar então minha VM por um container? Nem sempre, os containers Docker possuem algumas limitações em relação as VMs:
- Todas as imagens são linux, apesar do host poder ser qualquer SO que use ou emule um kernel linux, as imagens em si serão baseadas em linux.
- Não é possível usar um kernel diferente do host, o Docker Engine estará executando sob uma determinada versão (ou emulação) do kernel linux, e não é possível executar uma versão diferente, pois as imagens não possuem kernel.

#### 1.3. O que são containers?

Container é o nome dado para a segregação de processos no mesmo kernel, de forma que o processo seja isolado o máximo possível de todo o resto do ambiente.

Em termos práticos são File Systems, criados a partir de uma "imagem" e que podem possuir também algumas características próprias.

![](img/o-que-sao-containers.png)

- https://www.docker.com/what-container

#### 1.4. O que são imagens Docker?

Uma imagem Docker é a materialização de um modelo de um sistema de arquivos, modelo este produzido através de um processo chamado build.

Esta imagem é representada por um ou mais arquivos e pode ser armazenada em um repositório.

**Docker File Systems**

O Docker utiliza file systems especiais para otimizar o uso, transferência e armazenamento das imagens, containers e volumes.

O principal é o AUFS, que armazena os dados em camadas sobrepostas, e somente a camada mais recente é gravável.
- https://pt.wikipedia.org/wiki/Aufs
- https://docs.docker.com/engine/userguide/storagedriver/aufs-driver/

#### 1.5. Arquitetura

De maneira simplificada podemos dizer que o uso mais básico do Docker consiste em:
- Ter o serviço Docker Engine rodando
- Ter acesso a API Rest do Docker Engine, normalmente através do Docker Client
- Baixar uma imagem do Docker Registry, normalmente do registry público oficial: https://hub.docker.com
- Instanciar um container a partir da imagem baixada

![](img/arquitetura.png)

Figura 2. Arquitetura do Docker

#### 1.6. Crescimento do Docker

A primeira versão do Docker é de 13 de março de 2013, tendo um pouco mais de 4 anos (na epóca que este curso foi escrito).

Nestes 4 anos ele tem se tornado cada vez mais popular e uma solução real para desenvolvedores (manter o seu ambiente mais simples e próximo à produção), administradores de sistema e ultimamente para uso enterprise, sendo avaliado pelos principais players do mercado uma alternativa mais econômica em relação as soluções atuais. Em sua maioria virtualização.

![](img/crescimento-do-docker.png)


[Voltar ao Índice](#indice)

---

## <a name="parte3"> Seção: 3 - Instalação (4)</a>

#### 2.1. Docker Engine e Docker Machine

- Instalação (Linux, Microsoft Windows e MacOS)
- Uso do Docker Machine
- Uso do Docker na nuvem, Amazon, possivelmente outros

[Voltar ao Índice](#indice)

---


## <a name="parte4"> Seção: 4 - Uso Básico do Docker (14)</a>

#### 3.1. Introdução ao Docker Client

Conforme vimos em Arquitetura, o Docker Engine expõe uma API Rest que pode ser consumida pelas mais diversas ferramentas. A ferramenta inicial fornecida com a própria engine é o Docker Client, utilitário de linha de comando.

#### 3.2. Hello World: Meu Docker funciona !

Vamos confirmar o funcionamento do nosso Docker.

```
# docker container run hello-world
Hello from Docker!
This message shows that your installation appears to be working correctly.
To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash
Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/
For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

Na documentação oficial, o passo para verificação da instalação é este Hello World, porém até a publicação deste curso a documentação ainda utilizava a sintaxe antiga: docker run hello-world
- https://docs.docker.com/engine/getstarted/step_one/#step-3-verify-your-installation

Testar correto funcionamento do Docker, incluindo a recuperação de imagens e execução de containers.

#### 3.3. Meu querido amigo run

O comando run é a nossa porta de entrada no Docker, agrupando diversas funcionalidades básicas, como:
- Download automático das imagens não encontradas: docker image pull
- Criação do container: docker container create
- Execução do container: docker container start
- Uso do modo interativo: docker container exec

A partir da versão 1.13, o Docker reestruturou toda a interface da linha de comando, para agrupar melhor os comandos por contexto.

Apesar dos comandos antigos continuarem válidos, o conselho geral é adotar a nova sintaxe.
- https://blog.docker.com/2017/01/whats-new-in-docker-1-13/#h.yuluxi90h1om

Até a versão 17.03 (corrente na publicação do curso), ainda é possível utilizarmos a sintaxe antiga, porém precisamos pensar nela como atalhos:

```
docker pull
    docker image pull
docker create
    docker container create
docker start
    docker container start
docker exec
    docker container exec
```


#### 3.4. Modo interativo

Podemos usar containers em modo interativo, isto é extremamente útil para processos experimentais, estudo dinâmico de ferramentas e de desenvolvimento.

Exemplos de Uso
- Avaliação do comportamento ou sintaxe de uma versão específica de linguagem.
- Execução temporária de uma distribuição linux diferente
- Execução manual de um script numa versão diferente de um interpretador que não a instalada no host.

Principais opções do Docker para este fim
- docker container run -it
- docker container start -ai
- docker container exec -t

Exercício 2 - Ferramentas diferentes

```
# bash --version
GNU bash, version 4.4.19(1)-release (x86_64-alpine-linux-musl)
Copyright (C) 2016 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>

This is free software; you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
# docker container run debian bash --version
Unable to find image 'debian:latest' locally
latest: Pulling from library/debian
f606d8928ed3: Pull complete
Digest: sha256:e538a2f0566efc44db21503277c7312a142f4d0dedc5d2886932b92626104bff
Status: Downloaded newer image for debian:latest
GNU bash, version 5.1.4(1)-release (x86_64-pc-linux-gnu)
Copyright (C) 2020 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>

This is free software; you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
```

Confirmar que o conjunto de ferramentas disponíveis em um container são diferentes das disponíveis no host.

**Exercício 3 - run cria sempre novos containers**

```
# docker container run -it debian bash
root@53a6df47194e:/# touch /curso-docker.txt
root@53a6df47194e:/# exit
exit
# docker container run -it debian bash
root@85d396adffcf:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@85d396adffcf:/# ls /curso-docker.txt
ls: cannot access '/curso-docker.txt': No such file or directory
```

Demonstrar que o run sempre irá instanciar um novo container.
Como vimos em Docker File Systems, o container e a imagem são armazenados em camadas, o processo de instanciar um container basicamente cria uma nova camada sobre a imagem existente, para que nessa camada as alterações sejam aplicadas.

Assim sendo o consumo de espaço em disco para instanciar novos containers é relativamente muito baixo.

**Exercício 4 - Containers devem ter nomes únicos**

```
# docker container run --name mydeb -it debian bash
root@b6b62dbe8453:/# exit
exit
# docker container run --name mydeb -it debian bash
docker: Error response from daemon: Conflict. The container name "/mydeb" is already in use by container "b6b62dbe84539c2dd13a5feddf9bd29682b0d5913cf18694396428fc3f8bbbb3". You have to remove (or rename) that container to be able to reuse that name.
See 'docker run --help'.
```

**Exercício 5 - Reutilizar containers**

```
# docker container start -ai mydeb
root@b6b62dbe8453:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@b6b62dbe8453:/# touch /curso-docker.txt
root@b6b62dbe8453:/# ls
bin   curso-docker.txt  etc   lib    media  opt   root  sbin  sys  usr
boot  dev               home  lib64  mnt    proc  run   srv   tmp  var
root@b6b62dbe8453:/# exit
exit
# docker container start -ai mydeb
root@b6b62dbe8453:/# ls /curso-docker.txt
/curso-docker.txt
root@b6b62dbe8453:/# exit
exit
```

Demonstrar o uso do start em modo interativo, reutilizando um container previamente criado, além de confirmar que o mesmo consegue reter modificações em seu file system.

**Remover depois que executar (não salav na lista de containers) -> --rm**

```
# docker container ps -a
CONTAINER ID   IMAGE               COMMAND                  CREATED         STATUS                       PORTS     NAMES
b6b62dbe8453   debian              "bash"                   3 minutes ago   Exited (0) 51 seconds ago              mydeb
85d396adffcf   debian              "bash"                   6 minutes ago   Exited (127) 3 minutes ago             nice_gates
53a6df47194e   debian              "bash"                   7 minutes ago   Exited (0) 6 minutes ago               vigorous_varahamihira
831a32f8c858   debian              "bash --version"         8 minutes ago   Exited (0) 8 minutes ago               fervent_wright
# docker container run --rm debian bash --version
GNU bash, version 5.1.4(1)-release (x86_64-pc-linux-gnu)
Copyright (C) 2020 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software; you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
#  docker container ps -a
CONTAINER ID   IMAGE               COMMAND                  CREATED         STATUS                       PORTS     NAMES
b6b62dbe8453   debian              "bash"                   5 minutes ago   Exited (0) 2 minutes ago               mydeb
85d396adffcf   debian              "bash"                   8 minutes ago   Exited (127) 5 minutes ago             nice_gates
53a6df47194e   debian              "bash"                   8 minutes ago   Exited (0) 8 minutes ago               vigorous_varahamihira
831a32f8c858   debian              "bash --version"         9 minutes ago   Exited (0) 9 minutes ago               fervent_wright
```

#### 3.5. Cego, surdo e mudo, só que não !

Um container normalmente roda com o máximo de isolamento possível do host, este isolamento é possível através do Docker Engine e diversas características provídas pelo kernel.

Mas normalmente não queremos um isolamento total, e sim um isolamento controlado, em que os recursos que o container terá acesso são explicitamente indicados. Principais recursos de controle do isolamento
- Mapeamento de portas
- Mapeamento de volumes
- Copia de arquivos para o container ou a partir do container
- Comunicação entre os containers

#### 3.5.1. Mapeamento de portas

É possível mapear tanto portas TCP como UDP diretamente para o host, permitindo acesso através de toda a rede, não necessitando ser a mesma porta do container. O método mais comum para este fim é o parâmetro -p no comando docker container run, o -p recebe um parâmetro que normalmente é composto por dois números separados por : (dois pontos). O primeiro é no host e o segundo é no container

```
# docker container run -p 8080:80 nginx
172.17.0.1 - - [18/Octo/2022:19:31:00 +0000] "GET / HTTP/1.1" 200 612 "-" "Mozilla/5.0 (X11; Fedora; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/74.0.3729.169 Safari/537.36" "-"
2022/10/18 19:31:01 [error] 9#9: *1 open() "/usr/share/nginx/html/favicon.ico" failed (2: No such file or directory), client: 172.17.0.1, server: localhost, request: "GET /favicon.ico HTTP/1.1", host: "localhost:8080", referrer: "http://localhost:8080/"
172.17.0.1 - - [18/Octo/2022:19:31:01 +0000] "GET /favicon.ico HTTP/1.1" 404 556 "http://localhost:8080/" "Mozilla/5.0 (X11; Fedora; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) ...
```

Mapeamento de portas
- Acessar a url http://localhost:8080 por um browser
- Receber a mensagem: Welcome to nginx no browser
- Verificar o log de acesso no terminal executando
- Tentar acessar a url http://localhost ou http://localhost:80
- Receber um erro do browser
- Parar a execução do container

#### 3.5.2. Mapeamento de volumes

#### 3.6. Modo daemon

#### 3.7. Manipulação de containers em modo daemon

#### 3.8. Nova sintaxe do Docker Client

[Voltar ao Índice](#indice)

---


## <a name="parte5"> Seção: 5 - Deixando de Ser Apenas um Usuário (11)</a>



[Voltar ao Índice](#indice)

---


## <a name="parte6"> Seção: 6 - Redes (4)</a>



[Voltar ao Índice](#indice)

---


## <a name="parte7"> Seção: 7 - Coordenando Múltiplos Containers (2)</a>



[Voltar ao Índice](#indice)

---


## <a name="parte8"> Seção: 8 - Projeto Cadastro Simples (3)</a>



[Voltar ao Índice](#indice)

---


## <a name="parte9"> Seção: 9 - Projeto para Envio de E-mails com Workers (11)</a>



[Voltar ao Índice](#indice)
