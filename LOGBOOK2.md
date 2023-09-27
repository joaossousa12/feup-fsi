# Internet Explorer: Vulnerabilidade crítica de execução remota de código (CVE-2019-1367)

## Identificação

- [CVE-2019-1367](https://www.cvedetails.com/cve/CVE-2019-1367/) é uma falha de execução remota de código no motor de scripts do Internet Explorer, permitindo controle do sistema.

- A única aplicação afetada por esta vulnerabilidade foi o Internet Explorer corrido em Windows, abrangendo várias das suas versões.

- As versões do Internet Explorer afetadas foram: Internet Explorer 11 no Windows 7/8.1/10, Internet Explorer 9 no Windows Server 2008 e Internet Explorer 10 no Windows Server 2012.

## Catalogação

- Foi catalogada e publicamente divulgada em Setembro de 2019 por Clément Lecigne (Google’s Threat Analysis Group).

- Relativamente a Bug Bounties não há nenhuma informação já que esta vulnerabilidade foi descoberta pela própria fornecedora do browser (Microsoft).

- Esta vulnerabilidade foi considerada de alta gravidade devido ao potencial de execução de código remoto por um atacante.

- Esta vulnerabilidade está classificada no sistema CWE como CWE-787 ("Out-of-bounds Write"). Esta classificação consiste numa vulnerabilidade em que ocorre a escrita de dados para além dos limites permitidos numa área de memória.

## Exploit

- Um atacante conseguia redirecionar a sua vítima para um website malicioso feito por ele que daria "trigger" a um "remote code execution attack".

- O atacante poderia fazer log-in com "administrative user rights" na máquina da vitima podendo instalar programas, ver/apagar dados, etc.

## Ataques

- Não houve registo de ataques, uma vez que quando descoberto este exploit foi logo resolvido pela Microsoft.

- Um potencial ataque permitiria ao atacante ter acesso remoto sobre a máquina da vítima.

### Fontes consultadas

- https://nvd.nist.gov/vuln/detail/CVE-2019-1367
- https://www.bleepingcomputer.com/news/security/microsoft-issues-windows-security-update-for-0day-vulnerability/
- https://www.tenable.com/blog/cve-2019-1367-critical-internet-explorer-memory-corruption-vulnerability-exploited-in-the-wild
