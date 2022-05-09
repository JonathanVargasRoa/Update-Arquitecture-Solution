# Update-Arquitecture-Solution binary-armhf / Packages



¿Cómo solucionar un error "Error al recuperar binary-armhf / Packages" durante la actualización de apt-get?

Cuando ejecuto _Sudo apt-get update_ me sale el siguiente error:

_W: Failed to fetch http://archive.ubuntu.com/ubuntu/dists/trusty/main/binary-armhf/Packages  404  Not Found [IP: 91.189.91.15 80]

E: Some index files failed to download. They have been ignored, or old ones used instead.
_

He intentado buscar en _/etc/apt/sources.list.d/_ para ver si se puede eliminar algo en ese directorio, pero todo lo que hay allí es

_nodesource.list
nodesource.list.save
_

En mi archivo _sources.list_ tengo:

_deb http://ports.ubuntu.com/ubuntu-ports/ trusty main
deb-src http://ports.ubuntu.com/ubuntu-ports/ trusty main
deb http://ports.ubuntu.com/ubuntu-ports/ trusty-updates main
deb-src http://ports.ubuntu.com/ubuntu-ports/ trusty-updates main
deb http://ports.ubuntu.com/ubuntu-ports/ trusty-security main
deb-src http://ports.ubuntu.com/ubuntu-ports/ trusty-security main
deb http://archive.ubuntu.com/ubuntu trusty main
# deb-src http://archive.ubuntu.com/ubuntu trusty main
_

¿Alguien puede recomendar una forma de corregir este error?
aptarm
10
4 dic. 2015henrywright

La línea ofensiva era de la lista fuente x86. Eliminarlo eliminó el error. La siguiente es la lista correcta para la arquitectura armf.

deb http://ports.ubuntu.com/ubuntu-ports/ trusty main
deb-src http://ports.ubuntu.com/ubuntu-ports/ trusty main
deb http://ports.ubuntu.com/ubuntu-ports/ trusty-updates main
deb-src http://ports.ubuntu.com/ubuntu-ports/ trusty-updates main
deb http://ports.ubuntu.com/ubuntu-ports/ trusty-security main
deb-src http://ports.ubuntu.com/ubuntu-ports/ trusty-security main

2
4 dic. 2015
mikewhatever

Puede instalar las herramientas cruzadas armhf que agregan armhf como arquitectura extranjera (su arquitectura puede ser i386 o AMD64). Puede iniciar este comando para verificar:

dpkg --print-foreign-architectures

Si el resultado incluye armhf, simplemente puede eliminarlo ejecutando el comando:

Sudo dpkg --remove-architecture armhf

Finalmente, inicie su Sudo apt-get update nuevamente.
