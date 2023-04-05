
# Processos necessários de instalação de uma conta Bitrix24

>  ### **AVISO: Nunca instalar PHP 8 antes da instalação da conta. Apenas depois da conta ter sido instalada com sucesso**
  
    Todos os processos recomendados serão indicados neste documento.

<br>

# Pre-instalação

> A verificação do espaço do disco requer que esteja conectado ao servidor

###  Conectar ao VPN indicado pelo cliente, se instruído para tal pelo cliente.
 
- **Verificações necessárias** 
	- Verificar se a porta 22 está aberta ou se o cliente especificou a [utilização de outra porta](#outra-porta) no caso de VPN
	- [Verificar espaço do disco](#verificar-espaço-do-disco)
	
<br>

##  Verificar espaço do disco

> A bitrix recomenda 10 GB de espaço mínimo, **contudo** estes 10GB são
> **gerais** e sem partições.
> **Este passo requer que esteja [conectado](#conectar-ao-servidor) ao servidor**

Para verificar o espaço do disco do servidor é necessário executar o comando `df -h`
É também possível ver os discos montados e os tipos com o comando `lsblk`
Para verificar o espaço que uma pasta ocupa existe o comando: `du -sh {DIRETORIO}`

<br>

### Listagem/descrição de comandos

| ``df -h`` | ``lsblk``| ``du -sh {DIRETORIO}`` |
|--|--|--|
| Lista as partições e o espaço ocupado por cada | Lista as partições em hierarquia e o tipo de disco da partição | Verifica o espaço usado por um diretório|

<br>

# Instalação

> Apenas realizar a instalação após concluir a [pre-instalação](#pre-instalação) com sucesso

 1. [Conectar ao servidor](#conectar-ao-servidor)
 2. [Instalar bitrix - servidor](#instalar-bitrix24-parte-1---servidor) 
 3. [Instalar bitrix - web](#instalar-bitrix24-parte-2---web)
 4. [Instalar smtp](#instalar-smtp)

<br>

## Conectar ao servidor

>Esta secção será apenas a máquinas Windows
	
Para conectar ao servidor é necessário abrir o `cmd`. Para tal pode apenas pesquisar pelo `cmd` no menu inicio do windows ou usar `Windows + R` e digitar `cmd` e carregar na tecla `Enter`.

Após ter o `cmd` aberto digite o comando `ssh {CONTA}@{IP}`.

> Normalmente a conta é root

Substitua a conta e o ip pelas que foram indicadas pelo cliente.


### Outra porta

> Por predefinição o ssh tenta conectar na porta 22, se for necessário outra porta
> pode usar o comando adicional `ssh {CONTA}@{IP} -p {PORTA}`

<br>
	
# Instalar Bitrix24: Parte 1 - Servidor

> Esta secção só deve ser seguida se conectou ao servidor com sucesso.
> **NOTA:** Ao correr um comando espere sempre que o comando acabe.
> Tal é indicado pela **falta de nome** na linha de comandos.

Após servidor numa conta com privilégios máximos realize a seguinte ordem de comandos:

1. **Para garantir compatibilidade execute o comando:** `yum install wget -y`

2. De seguida deve buscar o repositório bitrix com o comando: 
`wget http://repos.1c-bitrix.ru/yum/bitrix-env.sh`

3. Após concluir o download do repositório use o seguinte comando para poder executar o ficheiro:
`chmod +x bitrix-env.sh`

4. De seguida execute o ficheiro com o comando: `./bitrix-env.sh`

> **Nota:** Este passo requer algum tempo

5. Após concluir este passo é necessário dar reboot ao servidor com o comando: `reboot`

> **Outra nota:** A sua conexão irá abaixo, mas isso é esperado

6. De seguida [conecte](#conectar-ao-servidor) novamente ao servidor e execute o seguinte comando outra vez: `./bitrix-env.sh`

7. Após concluido dê novamente `reboot` ao servidor.

<br>

## Parametros adicionais

> Se o cliente não tiver provido um dominio (**apontado para o servidor**)
> passe para a [parte 2](#instalar-bitrix24-parte-2---web)

Se tem o dominio obtenha o certificado **HTTPS** `"Let's encrypt"`

<br>

Para tal é necessário estar no modo **virtual appliance** da bitrix ou também conhecido como o menu inicial que aparece.

> Se não estiver no menu é possível aceder ao menu com o comando `/root/menu.sh`
> ou `./menu.sh`

<br>

 1. Digite `8` (o texto deve ser: **8. Manage pool web servers**) e carrege `Enter`
 2. Após carregar as opções digite `3` (**3. Configure certificates**) e carrege `Enter` de novo
 3. De seguida a opção `1` (**Configure "Let's encrypt" certificate**) e carregue `Enter` de novo.

<br>

Após concluir estes 3 passos o sistema perguntará qual site quer configurar.
O cliente provavelmente só terá um site e será esse o `default`.
**De seguida** carregue enter.

<br>

> Para este passo é necessário o dominio que o cliente tenha provido, e se der erro ao configurar o certificado é possível que o cliente não tenha apontado o **domínio** para o **servidor**

Agora digite o(s) dominio(s) a configurar, e se for vários dominios separar por virgula:
`www.example.org, www.example2.org`

Após digitar todos os dominios providos pelo cliente carregue `Enter` e de seguida insira o e-mail para as notificações e carregue `Enter`

<br>

# Instalar Bitrix24: Parte 2 - Web

1. [Licensa](#licensa)
2. [Registro do produto](#registro-do-produto)
3. [Verificação preliminar](#verificação-preliminar)
4. [Criação de base de dados](#criação-de-base-de-dados)
5. [Instalação de sistema](#instalação-de-sistema)
6. [Criar conta de administrador](#criar-conta-de-administrador)

<br>

### Licensa

Neste passo só tem de aceitar os termos da licensa e clicar em `Next` 

<br>

### Registro do produto

> Neste passo é necessário uma chave de licensa, ou, alternativamente ative o modo demo.

As opções vão depender dos requisitos do cliente:

**Se** o cliente o indicar, ative o `modo de desenvolvimento`

Ao averiguar que corresponde tudo aos requisitos do cliente clique em `Next`

<br>

### Verificação preliminar



### Criação de base de dados

### Instalação de sistema

### Criar conta de administrador


# Instalar SMTP

> Esta secção só deve ser seguida se conectou ao servidor com sucesso.

1. [Instalar nano](#instalar-nano)
2. [Editar ficheiro de configuração](#editar-ficheiro-de-configuração)

<br>

## Instalar nano

> Este passo é opcional, mas é recomendado para facilitar a edição de ficheiros

Para instalar o nano use o comando: `yum install nano -y`

<br>

## Editar ficheiro de configuração

> NOTA: deve substituir tudo o que está entre chaves `{}` pelas informações que o cliente lhe deu

Após ter o nano instalado use o comando: `/etc/msmtprc`

No editor nano digite o seguinte:

```
# smtp account configuration for default
account default
logfile /home/bitrix/msmtp_default.log
host {HOST}
port 465
auth on
user {USER}
password {PASSWORD}
from {USER|FROM}
keepbcc off
tls on
tls_certcheck off
tls_starttls off
```
