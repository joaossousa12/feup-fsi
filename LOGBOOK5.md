# Buffer Overflow Attack Lab (Set-UID Version)

## Environment Setup

> Primeiramente para resolver este _lab_ começamos por desativar as _countermeasures_ do _Ubuntu_ de modo a simplificar os nossos ataques. Vamos desativar a randomização de espaços de endereços, uma vez que, com esta ativada seria difícil advinhar os endereços exatos de memória. Também vamos desativar a proibição Depois desativamos a proibição na _shell_ para permitir a execução por processos com _Set-UID_.
>```bash
> $ sudo sysctl -w kernel.randomize_va_space=0
> $ sudo ln -sf /bin/zsh /bin/sh
>```

##  Task 1: Getting Familiar with Shellcode

> Iniciamos o processo executando um programa simples que inicia uma shell através do comando ```execve```. Esse programa utiliza uma abordagem convencional, onde são definidos os argumentos e a chamada de sistema ```execve``` é feita.
> ```c
> char *name[2];
> name[0] = "/bin/sh";
> name[1] = NULL;
> execve(name[0], name, NULL);
> ```
> Posteriormente, replicamos o mesmo comportamento usando o _shellcode_ correspondente para ambas as arquiteturas, 32 bits e 64 bits. Esse _shellcode_ foi invocado a partir da _stack_, permitindo que a execução também resultasse na abertura de uma nova _shell_.

##  Task 2: Understanding the Vulnerable Program


