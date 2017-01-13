---
title: Ansible for dummies
date: '2017-01-10 00:00:00'
tags: [ansible]
published: false
---



Uno de los problemas más comunes para un administrador a la hora de configurar, administrar o mantener su granja de servidores es mantener sus configuraciones idénticas o lo más parecidas posible. En entornos pequeños, en los que tenemos 1, 2 o 5 servidores, es totalmente factible llevar una administración individual de cada uno de ellos. Aunque en los tiempos que corren y con la mayoría de aplicaciones ya funcionando de manera distribuida, no es nada extraño encontrarse granjas con 10, 20 o 50 servidores iguales e imposibles de manejar de forma individual. ¡Imaginemos tener que cambiar un parámetro en un determinado fichero de configuración a 37 servidores!



Otra cosa que también puede suceder es que, después de 1 año y por el motivo que sea, quieras o debas montar n servidores más en tu granja. ¿Qué hacemos? ¿Empezamos a revisar la documentación (en el mejor de los casos)?¿Miramos como están configurados actualmente nuestros servidores para reproducirlo en los nuevos? O lo que es peor: ¿nos ponemos de nuevo a googlear e investigar cómo montar un nuevo servidor X?



Ansible puede ser la solución. Ansible es una herramienta de automatización IT que nos permite realizar acciones masivas basadas en un archivo de definición llamado playbook. Un playbook es simplemente una definición de las instrucciones que queremos que se ejecuten sobre nuestros servidores.





¿Por qué Ansible?

La mayor diferencia con otros productos de automatización IT es la arquitectura sin agentes. Ansible solo utiliza SSH (bueno, también Python, que ya viene por defecto en la mayoría de distribuciones modernas). En contraste con Chef o Puppet, por ejemplo, que tienen dependencias que deben instalarse en los servidores antes de que puedan ejecutarse, con Ansible simplemente utilizando SSH nos podemos conectar a los servidores remotos y ejecutar los comandos deseados.



Ansible tiene una ventaja sobre otros productos debido a su simplicidad. Los playbooks usan un lenguaje descriptivo simple, basado en YAML y gracias a eso conseguimos una suave curva de aprendizaje.





Con lo de ser padre, me hizo mucha gracia esta foto ;)

Otra de las ventajas que ofrece esta herramienta son los módulos, unidades de trabajo en Ansible. Cada módulo es autosuficiente y puede ser escrito en el lenguaje estándar de scripting, como Python, Perl, Ruby, Bash, etc. Una de las propiedades principales de los módulos es la idempotencia, la cual asegura que ninguna operación se realizará una vez el sistema haya alcanzado el estado deseado.



Empecemos!!

Instalación

Para este laboratorio he utilizado una distribución de CentOS 7, pero Ansible se puede instalar sobre Debian, Gentoo, BSD, Mac OSX, Solaris, etc.



yum install ansible


1.PNG


2.PNG


3.PNG


El path de instalación por defecto es /etc/ansible, así que éste será nuestro directorio de trabajo.

4.PNG


Para realizar el inventario de servidores, a mí me gusta crear mis propios ficheros y no utilizar el de hosts que viene por defecto:


7.PNG


Captura%2Bde%2Bpantalla%2B2016-01-28%2Ba%2Blas%2B9.35.56.png




Claves SSH

Como comentábamos al principio, Ansible utiliza claves SSH para conectarse con los "clientes".



Para generar la clave SSH en el servidor de Ansible, simplemente deberemos seguir el asistente:



ssh-keygen



5.PNG


Una vez tengamos el certificado, deberemos copiarlo en todos los servidores que queremos manejar con Ansible.

ssh-copy-id -i /root/.ssh/id_rsa.pub root@test-lab01


9.PNG


Si las claves se han copiado correctamente y tenemos bien configurado nuestro fichero de inventario, ya deberíamos poder ejecutar comandos remotamente en nuestros servidores:

10.PNG


Y hasta aquí por hoy. En próximos posts veremos el funcionamiento de los roles y playbooks con más profundidad.

¡Gracias por leernos!

¡Un saludo!

Miquel.