# 🚩 WriteUp: Lame Machine

## Resolution:
**1. Enumeration with nmap:**

Primero, usamos la herramienta nmap para mapear todos los puertos abiertos en la maquina victima de ip 10.129.12.160. Las opciones a utilizar son -sV para ver la versión del servicio corriendo en dicho puerto y -sC para la ejecución de scripts seguros asi sacar mas información.

![alt text](screenshots_lame/image.png)

[more details of nmap report](resource_lame/nmap.md)

**2. Exploit VSFTPd version 2.3.4:**

Logramos localizar 4 puertos abiertos donde nos centraremos en el puerto ftp (21) porque su version del servicio tiene un "exploit" muy conocido de "backdoor".

https://www.exploit-db.com/exploits/17491

![alt text](<screenshots_lame/image copy.png>)

**3. Using metasploit for exploit VSFTPd:**

Usando metasploit iniciaremos el ataque no sin antes revisar los parametros y modificarlos en caso no sean las correctas o esten en blanco.

![alt text](<screenshots_lame/image copy 2.png>)
![alt text](<screenshots_lame/image copy 3.png>)

Modificamos el parametro RHOSTS:

![alt text](<screenshots_lame/image copy 4.png>)

El error que obtenemos tambien lo podemos visualizar en el codigo del exploit donde el id 331 indica que el servidor no responde como se espera puesto que te pide un password.

![alt text](<screenshots_lame/image copy 5.png>)

**4. Exploit Samba version 3.0.20:**

Probaremos otra vía de ataque llendo por el servicio Samba en el puerto smb (445 y 139).

https://www.exploit-db.com/exploits/16320

![alt text](<screenshots_lame/image copy 6.png>)

**5. Using metasploit for exploit Samba:**

Usando metasploit iniciaremos el ataque no sin antes revisar los parametros y modificarlos en caso no sean las correctas o esten en blanco.

![alt text](<screenshots_lame/image copy 7.png>)
![alt text](<screenshots_lame/image copy 8.png>)

Modificamos los parametros de RHOSTS y LPORT:

![alt text](<screenshots_lame/image copy 9.png>)

El exploit funciona y obtenemos una revershell como el usuario root.

![alt text](<screenshots_lame/image copy 10.png>)

**6. Phase Post-Explotation looking for flags:**

Ya estando dentro solo nos queda buscar las banderas para ello usaremos los comandos de find para encontrar posibles nombre comunes de banderas en estos entornos.
```bash
pwd
find . -name "user*.txt"
find . -name "admin*.txt"
find . -name "root*.txt"
```
![alt text](<screenshots_lame/image copy 11.png>)

**7. Flags:**

user.txt: c4c90e0cef57469fd2e3dc3f39b4f707

root.txt: a8dd8096206146b4f9629a97fddfdd50