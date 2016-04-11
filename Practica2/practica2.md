# Pr�ctica 2 - Clonar la informaci�n de un sitio web

IP Maquina1: 192.168.1.51  
IP Maquina2: 192.168.1.52  
Sistema Operativo: Debian 8  

**-Comenzamos instalando la herramienta rsync:**   
apt-get install rsync

**-Ahora configuraremos el acceso sin contrase�a mediante claves:**  
Ejecutamos el comando:  
ssh-keygen -t dsa  
Y generamos las claves en la m�quina 2  
Una vez generadas las copiamos en la m�quina 1  
ssh-copy-id -i .ssh/id_dsa.pub root@192.168.1.51  
Una vez copiada comprobamos si funciona correctamente:  
ssh root@192.168.1.51  
Vemos que entra correctamente sin pedirnos contrase�a.
  
**Ahora comprobaremos el correcto funcionamiento de rsync:**  
Hemos creado un archivo test.html en nuestra maquina1 y en nuestra maquina2 ejecutamos:  
rsync -avz -e ssh root@192.168.1.51:/var/www/html/ /var/www/html/  
Revisamos la carpeta /var/www/html/ en nuestra maquina2 y observamos que tenemos el nuevo archivo. Despues de realizar varios test con modificaciones de archivos y eliminaci�n de archivos estamos seguros de que funciona correctamente.

**-Ahora pasaremos a automatizar el proceso:**  
Para esto programaremos una tarea automatica con la herramienta crontab  
Editamos el archivo /etc/crontab agregando la siguiente linea:  
*/5 * * * *		root	rsync -avz -e ssh root@192.168.1.51:/var/www/html/ /var/www/html/  






