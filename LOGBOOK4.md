# Environment Variable and Set-UID Program Lab

## Task 1: Manipulating Environment Variables

> Nesta _task_ aprendemos que com os comandos `printenv` ou `env` conseguimos dar _print_ a uma variável do sistema. O exemplo que nos é apresentado é para a variável **PWD**:

![task1](images/logbook4/task1.png)

## Task 2: Passing Environment Variables from Parent Process to Child Process

> Na segunda _task_ é nos pedido para guardar o output (variáveis ambientais) de um programa **myprintenv.c** de duas maneiras distintas, usando a função `printenv` para o processo filho e depois para o processo pai. Fazendo isso obtemos dois ficheiros **file** e **file2** que são iguais comprovando que todas as variáveis ambientais do processo pai são herdadas pelo processo filho.

![task2](images/logbook4/task2.png)

## Task 3: Environment Variables and execve()

> Nesta _task_ conseguimos observar que quando temos `NULL` como terceiro parâmetro na função `execve()` não existe qualquer output, uma vez que as _environment variables_ não são passadas a este apontador já que é nulo. <br>
> No caso de mudarmos `NULL` para `environ` recebemos um output com as _environment variables_ que vão ser guardadas nesse _array_.

## Task 4: Environment Variables and system()

> Ao usar `system()`, as _environment variables_ do processo anterior são passadas para um novo processo. Isso ocorre porque essa função executa `/bin/sh -c comando`. Basicamente, `system()` utiliza `execl()` para executar o `/bin/sh`, que por sua vez, chama `execve()`, transmitindo as _environment variables_. Assim, ao usar `system()`, as _environment variables_ do processo anterior são transmitidas para o novo programa (/bin/sh).

> Por outro lado, ao chamar `execve()`, o processo atual é substituído pelo comando fornecido, mantendo as _environment variables_ existentes a menos que sejam explicitamente alteradas nos argumentos passados para o `execve()`.

## Task 5: Environment Variable and Set-UID Programs

> Nesta _task_ foi nos pedido para primeiro compilar um programa que dá _print_ a todas as _environment variables_ no processo atual. <br>
> De seguida compilamos o programa e mudamos os privilégios desse programa para _root_ e tornamo-lo num programa Set-UID da seguinte maneira: 
> ````bash
> $ sudo chown root foo 
> $ sudo chmod 4755 foo 
> ````
> Aseguir a isto alteramos algumas _environment variables_ e definimos uma nova.<br>
> ````bash
> $ export PATH=$PATH:/home/seed/Downloads
> $ export LD_LIBRARY_PATH=/home/seed/Desktop/
> $ export TESTING=YES
> ````
> Depois de corrermos o programa de novo conseguimos ver que as _environment variables_ definidas anteriormente compareciam no output, exceto `LD_LIBRARY_PATH`. Isto acontece por questões de segurança, o `LD_LIBRARY_PATH` não é transmitido para programas com permissões de `root`, a fim de evitar potenciais vulnerabilidades.


## Task 6: The PATH Environment Variable and Set-UID Programs

> Nesta _task_ começamos por criar um programa Set_UID e mudar os privilégios desse programa para _root_. Esse programa vai essencialmente usar o comando `ls`:
> ```c 
>  system("ls");
> ```
> De seguida criamos um programa malicioso chamado `ls` em `/home/seed/modifiedls`.
> <br><br> Depois disso mudamos o PATH para o diretório com a versão alterada do `ls`:
> ```bash
> $ export PATH=/home/seed/modifiedls
> ```
> Podemos então concluir que a função `ls` executada foi a maliciosa.
