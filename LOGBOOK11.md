# Public-Key Infrastructure (PKI) Lab

## Environment Setup

> Primeiramente para resolver este _lab_ adicionamos a seguinte entrada ```10.9.0.80 www.bank32.com``` usando ```sudo nano /etc/hosts``` aos _hosts_ conhecidos pela _VM_ e executamos os containers com ```docker-compose build``` e ```docker-compose up```.

## Task 1: Becoming a Certificate Authority (CA)

> Para resolver esta tarefa começamos por copiar o ficheiro de certificado padrão localizado em ```/usr/lib/ssl/openssl.cnf``` para uma pasta que criamos no ambiente de trabalho. Em seguida, executámos os seguintes comandos para criar o ambiente da nossa própria _CA_:
> ```bash
> mkdir ca 
> cd ca
> mkdir certs 
> mkdir crl 
> mkdir newcerts
> touch index.txt
> echo "1000" >> serial
> ```
> Depois, procedemos à configuração da _CA_:
> ```bash
> openssl req -x509 -newkey rsa:4096 -sha256 -days 3650 -keyout ca.key -out ca.crt
> ```
> Durante o processo, inserimos os seguintes dados:
> <br><br>PEM pass phrase: abcd
![dados](images/logbook11/dados.png)
> Para analisar o conteúdo dos ficheiros gerados, decodificámos o certificado X509 e a chave RSA:
> ```bash
> openssl x509 -in ca.crt -text -noout
> openssl rsa -in ca.key -text -noout
> ```
> Confirmámos que é um certificado de _CA_, pois na secção _basic_ _constraints_ existe um atributo _CA_ verdadeiro:
![catrue](images/logbook11/caTrue.png)
> Este certificado é _self-signed_, dado que o campo _issuer_ e o campo _subject_ são iguais:
![issuersubject](images/logbook11/issuersubject.png)
> O conteúdo do ficheiro gerado relativo à criptografia é este:
```
RSA Private-Key: (4096 bit, 2 primes)
modulus:
    00:a0:cf:45:dd:f2:b8:9c:d1:33:e4:b4:10:2e:7e:
    8a:ea:5b:0e:f9:56:89:f6:d1:29:4e:6b:7f:d6:49:
    d4:05:97:e3:2b:e9:ea:e5:c6:ef:53:cf:d9:d4:af:
    5d:1e:5e:f8:ce:24:6c:39:f3:b2:8e:26:9d:90:dd:
    a9:0e:d1:97:e1:87:5d:8c:f3:a0:0e:24:ff:de:62:
    b0:ec:1f:12:45:b9:bd:0e:4e:ac:ab:6f:bd:83:63:
    f2:74:17:3e:71:a1:c1:d0:19:21:12:06:22:05:4e:
    c5:ec:62:d7:d3:54:ab:30:7a:c8:96:4e:f7:83:73:
    5c:7c:05:dc:2a:0f:06:9d:9b:b1:a4:a0:ca:23:ce:
    a7:cc:0e:a9:da:37:2d:d3:b3:d1:e5:55:32:20:89:
    12:29:f2:59:ae:c2:b8:83:8a:29:79:8b:87:dc:a6:
    f6:d5:e4:b4:ce:77:68:91:f8:a9:71:0d:14:0d:6d:
    90:cb:cb:3c:a1:af:6d:44:3d:57:e1:bf:8d:79:3b:
    a4:2a:46:2a:8b:64:55:01:5c:0c:02:5b:3c:67:71:
    ce:f1:bc:ef:07:9e:8f:67:ba:03:cf:e9:66:45:99:
    04:41:50:8c:9a:30:9a:e4:7d:34:37:bc:6a:33:78:
    51:1f:ff:d9:08:c3:14:57:ec:44:41:d1:63:6b:b3:
    e5:22:6c:4a:8a:36:e4:e7:7b:d0:6f:c5:87:0c:fa:
    33:9e:c0:08:d6:fd:ac:6b:64:f0:dd:c6:0d:e3:bd:
    9a:9a:62:2b:bc:d4:fd:22:6f:81:1e:82:a9:3b:28:
    24:fe:49:7d:2a:ff:17:df:c3:2e:5b:b7:fe:f2:bb:
    dc:1d:3f:81:da:66:e4:1d:ff:73:fa:a2:e4:52:5e:
    d5:a2:4f:1b:49:1e:22:57:f7:8f:c2:bf:65:72:cb:
    b8:0c:ea:bc:37:56:5e:e6:95:87:32:cd:20:de:bc:
    32:33:7d:ac:7e:e0:09:4a:96:b3:a6:7b:fb:5a:02:
    f2:fb:3a:c9:22:d5:de:20:76:72:4a:44:90:29:51:
    fd:18:85:4b:21:20:c4:7a:b7:4b:a3:67:04:5b:c6:
    2d:12:c2:c1:88:de:77:51:16:43:86:46:e7:75:6c:
    83:5b:e0:c2:72:12:43:68:af:c1:53:63:10:d4:10:
    c2:12:2a:86:d6:8e:f1:0a:dc:3f:89:fe:07:b3:22:
    d0:72:6e:5b:2c:71:bf:06:4f:1b:96:f8:e0:ed:e1:
    34:d7:b3:97:01:7b:60:93:26:45:fb:bc:38:51:4f:
    e1:1c:32:bc:e4:fa:c5:60:c4:06:5d:e8:50:ef:9a:
    47:ed:c8:05:04:aa:9a:7f:8a:47:17:0e:08:e2:ee:
    41:68:df
publicExponent: 65537 (0x10001)
privateExponent:
    43:04:1e:69:d0:ad:7f:2c:f0:23:6f:a7:0e:b9:4d:
    cb:3d:07:90:81:b0:1d:5c:2d:8a:b0:e2:25:bb:be:
    d0:55:ec:26:70:e5:a3:bc:b4:20:89:8e:8e:44:46:
    da:51:59:ff:0e:ce:cb:97:f3:e1:a9:d6:20:79:3f:
    eb:1d:0d:de:bf:3b:0d:72:ba:51:2a:ba:37:43:89:
    d7:dd:5b:10:13:c7:e6:1e:83:77:2e:aa:1c:07:9b:
    13:26:5c:af:9e:69:d6:ff:a1:f8:90:f5:bc:a0:87:
    7b:6b:f5:e5:ec:73:2b:51:00:27:23:e1:a2:b6:80:
    e4:6e:cc:c1:fa:61:17:6d:bb:2a:90:97:ad:34:82:
    59:58:03:11:1d:cd:cb:5c:35:2d:0d:c4:46:2a:d9:
    97:01:98:be:6c:07:d9:49:ca:df:0c:77:22:4d:b2:
    b0:91:0f:88:bb:da:a8:7a:a8:a2:a4:80:a6:d7:f2:
    6f:fb:d2:d8:ce:f3:0a:6d:46:22:9e:61:a7:14:63:
    e5:fa:37:e0:bf:7f:6d:81:9e:bf:9c:a6:1f:b6:1e:
    38:40:34:9d:48:47:1b:43:3a:33:7b:61:53:bf:e1:
    36:17:0b:81:76:a0:16:78:d7:3a:23:1b:5f:37:d5:
    17:30:d8:91:fe:3a:8c:29:ba:88:73:6a:ab:87:dd:
    05:42:3b:95:16:6b:f3:b4:df:97:79:d3:d5:9c:18:
    02:03:a1:22:db:3f:9b:34:d8:9c:3a:ce:2e:bf:8b:
    f6:47:93:6a:d9:76:0a:69:b8:09:de:3f:4a:db:44:
    35:45:34:98:0c:58:f0:6c:38:7d:c6:2c:01:42:50:
    be:4e:08:15:0a:b8:5a:be:94:fb:a8:5f:76:02:1c:
    f8:ac:46:2b:32:14:05:39:5d:4f:bc:99:c5:48:9f:
    fb:0d:ea:32:1d:3d:ad:cb:38:75:58:2c:84:d6:b5:
    58:73:d9:61:9a:28:48:b5:3a:ef:5e:3f:7a:97:fa:
    59:d0:6c:b3:77:ff:5a:21:9b:29:db:c8:fd:0b:17:
    a2:89:46:7e:14:94:e0:1c:73:fa:76:3e:42:ea:0f:
    80:db:05:fd:01:ea:78:76:62:3f:2b:0e:bb:01:f9:
    98:d7:78:d8:48:a1:a4:d3:d4:4d:58:35:cc:87:94:
    6e:e4:dd:cd:20:81:db:fa:5a:2b:c5:02:ca:e2:e8:
    88:d1:d5:5f:ae:33:81:4b:db:40:dd:76:fc:38:a5:
    4a:a1:5a:46:3b:80:cd:6c:24:6a:82:ff:f8:4c:a5:
    d3:e6:fe:fe:0b:b6:21:fe:8f:5f:43:93:40:06:45:
    4e:98:7b:d0:88:95:52:05:ec:e4:7a:01:43:c9:6a:
    63:01
prime1:
    00:d3:41:7d:06:74:4b:be:dc:42:6b:16:a4:c0:4f:
    82:f9:4e:e5:2e:90:52:71:a1:42:5e:f0:3c:01:27:
    60:39:08:df:75:2d:73:ec:80:d4:fc:3d:42:2c:c7:
    37:36:0f:8d:e8:31:85:d5:58:34:03:75:0f:6b:87:
    4b:f6:66:7d:28:a2:ca:f0:0f:08:59:6d:65:13:cd:
    22:e8:36:ae:1b:93:0b:bf:a7:c2:20:18:b7:7a:c3:
    f6:e6:35:23:2c:05:21:aa:22:23:41:c9:a4:d1:d2:
    bc:4d:ff:23:f1:fa:d1:3f:78:dc:0b:7a:39:4f:0b:
    c2:32:b5:fd:15:16:75:e8:13:ed:a5:5f:81:e0:49:
    79:a2:45:32:52:92:eb:c1:42:9f:3a:67:86:a7:33:
    ec:68:6c:aa:79:90:ff:ed:83:5b:bd:0e:72:c8:7d:
    c2:bd:30:1f:cb:5d:18:78:da:e0:54:a2:1d:81:dc:
    97:79:f9:17:25:c0:7b:22:b8:76:52:22:f2:59:da:
    d9:4d:ad:89:43:78:0c:9b:d3:ca:ad:f3:0e:89:14:
    55:82:e8:97:bf:f0:7a:dc:9d:8f:59:f6:8b:94:94:
    2e:93:36:e4:57:09:60:07:da:ad:92:1e:20:0b:60:
    f4:75:47:93:c0:08:7d:d7:51:bf:4d:78:fc:2c:e2:
    25:59
prime2:
    00:c2:de:8a:8b:c3:25:b4:13:1a:f7:f3:c9:68:67:
    80:25:c7:3b:2d:b7:db:45:4f:25:a4:ce:61:92:35:
    3c:13:bf:dc:80:f2:49:e2:35:a4:a5:fa:cf:30:ea:
    25:2b:54:be:86:2b:37:d6:5b:89:0c:7a:d2:3b:9d:
    d8:f2:10:63:37:3b:1f:da:e8:39:8c:3f:4d:8f:3d:
    ef:a4:b1:18:75:4b:71:49:21:0e:53:a0:19:06:84:
    c5:f3:fb:4e:48:cb:f1:87:01:79:91:52:74:86:18:
    d6:54:da:4b:99:87:c5:ff:c3:38:94:f5:45:ac:f5:
    4d:a0:62:4b:a6:ce:fe:ae:43:42:76:38:ab:74:81:
    da:44:45:00:65:ef:ad:64:86:7a:1a:fb:fa:62:bc:
    c2:5f:aa:93:a2:77:b0:fb:82:53:81:78:12:87:ef:
    26:b3:87:13:6c:e6:2f:eb:61:1d:4e:4a:60:33:1a:
    f5:47:4e:24:35:02:67:44:a4:90:4e:06:7f:58:26:
    3a:8c:86:2e:51:f0:bf:37:bc:a7:eb:06:3a:14:79:
    dc:42:a1:be:8f:ba:ff:1f:0c:8a:9b:bf:57:88:ed:
    8a:ac:18:06:d6:89:08:ca:1a:e9:99:0f:d5:77:c1:
    bc:4e:4b:14:31:73:9c:f6:9a:f6:81:ab:aa:aa:be:
    60:f7
exponent1:
    05:7e:26:6a:0c:8c:0b:a2:5e:77:ba:56:fe:49:12:
    f6:b8:7e:6c:ff:83:a5:40:b4:21:13:cd:fb:99:b2:
    7e:c9:24:46:3f:b0:4b:ed:ed:9b:c1:5b:ff:1e:0e:
    e9:70:ee:17:a3:71:ff:62:13:b8:23:4b:0b:58:b1:
    38:ee:e1:42:35:39:61:94:82:7b:10:c5:18:06:b5:
    69:a4:42:52:a5:38:20:fb:93:a8:91:fb:f3:4d:35:
    16:37:3b:7a:e1:87:46:8d:2c:ad:81:38:af:db:f2:
    d9:74:50:d2:f1:da:8e:f3:ed:84:be:e0:ce:95:57:
    af:49:dc:12:b8:4a:c8:85:fc:1f:d8:a3:df:d9:09:
    38:96:e4:00:11:a1:df:9c:83:d7:58:e9:bf:5f:32:
    3e:64:d4:e9:e4:43:43:41:af:18:f3:4f:38:b7:4c:
    60:ee:e7:64:ba:3e:f0:a5:80:3f:b3:17:61:51:02:
    ff:40:e2:c1:30:88:03:17:18:bc:79:fc:23:29:f5:
    8c:77:7e:a2:2a:74:e9:78:50:44:c5:95:13:2b:5c:
    2d:d3:2e:5e:e7:39:ca:92:ae:2f:80:a1:90:73:69:
    e2:9a:02:c5:e0:90:86:a3:c0:ef:93:a8:f1:a2:cb:
    b8:60:ec:0e:8a:29:fb:77:3c:aa:1f:03:2f:87:91:
    c1
exponent2:
    62:c2:62:38:de:d7:f6:e1:4f:e3:a5:fb:c7:1b:dd:
    48:48:26:67:cf:2c:23:7e:2f:37:cd:18:89:fe:cc:
    c9:bd:8c:c5:15:05:f8:cc:f2:fa:e3:97:a9:d4:a0:
    ad:cb:2f:1b:d4:3f:62:35:d5:c9:2b:5d:ec:b4:dc:
    c4:21:26:07:51:c1:9d:31:e0:28:81:d4:8e:e9:f6:
    cf:e2:a8:e0:99:31:7a:bc:74:04:51:b9:1d:22:a1:
    28:3b:8e:bb:3a:10:d8:39:19:21:5b:46:8e:c7:7b:
    a8:59:51:c3:27:9a:63:3a:cf:2c:3e:f9:e6:e4:13:
    49:5b:47:b7:ec:64:0a:71:2f:f7:b6:54:be:a1:28:
    bb:3c:b5:2c:f4:41:4e:17:11:3f:27:c1:07:d5:5e:
    35:19:bf:e4:b1:00:53:17:03:b7:33:e1:40:5f:25:
    a0:0a:ae:ff:9b:d1:61:5b:40:7c:f3:18:ba:0d:c9:
    8d:2f:bf:0d:d6:7f:fb:bb:e3:1e:88:10:75:de:3a:
    02:09:e6:e3:c4:3d:44:c4:29:dd:e4:b3:fe:b8:9b:
    b6:71:3e:a0:9d:46:ba:b7:a2:6f:b8:93:66:63:ec:
    c9:b7:0b:90:22:b6:ff:a6:90:08:f0:8b:61:3c:20:
    71:15:7f:d0:68:25:7e:9d:9e:9c:ad:21:bb:92:ec:
    95
coefficient:
    75:c7:6c:2a:42:0b:bf:02:11:91:c1:7f:8d:04:98:
    b2:47:23:17:6a:80:7f:47:e0:f7:86:38:05:f7:4f:
    22:92:ca:84:18:d9:ad:72:70:f0:56:fd:bc:3b:79:
    a6:ab:9d:8c:bf:0a:34:bd:01:66:47:56:ff:2f:5d:
    22:c7:56:1d:79:03:d2:06:18:19:c5:fe:7c:d0:50:
    77:37:c4:b0:7e:2d:8a:a4:c4:68:87:5e:a3:dc:3c:
    3b:f9:08:5b:a3:b6:e6:99:09:ff:f9:8d:d8:00:39:
    77:76:7e:7a:09:23:c2:66:b0:00:89:d4:33:73:9e:
    52:b7:3f:0d:47:3f:be:4c:f3:27:7c:24:35:01:fc:
    cf:76:85:58:53:fb:dd:cd:20:34:c4:77:b3:65:0e:
    a3:72:94:86:a1:31:b8:9f:9d:1a:08:53:93:7b:2f:
    1b:7b:09:7e:ab:69:20:21:f5:35:60:59:41:42:2d:
    eb:56:f1:7e:2e:27:33:f0:30:d5:31:5d:cf:ca:5e:
    e4:51:9b:cc:29:44:8e:00:91:0e:01:da:b3:9e:55:
    9a:03:7b:a5:7e:cb:d2:69:cb:a2:9a:89:2f:1b:35:
    44:a9:81:c3:69:22:00:cc:cf:30:5c:af:02:02:8d:
    3b:26:11:80:d4:10:a9:f9:9d:15:be:b0:ea:3d:41:
    ac
```
> Nele, podemos identificar os seguintes elementos:
1. Os dois números primos (campo ```prime1``` e ```prime2```).
2. O _modulus_ (campo ```modulus```).
3. Os expoentes públicos e privados (campo ```publicExponent``` e ```privateExponent```).
4. O coeficiente (campo ```coeficient```).

## Task 2: Generating a Certificate Request for your Web Server






