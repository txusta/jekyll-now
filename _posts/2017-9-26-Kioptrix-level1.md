---
layout: post
title: Kioptrix Level 1 WRITE-UP
---

Nos hemos descargado la máquina virtual de Kioptrix level 1 desde la página web de Vulnhub y la arrancaremos junto a la máquina Kali Linux para conseguir el objetivo: Una shell de root en la máquina víctima. 

Vamos a la máquina Kali y con un ifconfig vemos que nuestra ip es: 192.168.56.129

Ejecutamos NMAP para descubrir IP de la víctima:

![NMAP]({{ site.baseurl }}/images/kioptrix-level1-1.png)

La descubrimos en la IP: 192.168.56.128

![NMAP]({{ site.baseurl }}/images/kioptrix-level1-2.png)

Vemos que tiene diferentes puertos abiertos y en este caso nos vamos a centrar en el puerto 139/tcp netbios (samba).

Antes de activar el exploit intentaremos sacar la versión de SAMBA. Para ello haremos uso del comando SMBCLIENT.

![SAMBA]({{ site.baseurl }}/images/kioptrix-level1-3.png)

Vemos que tiene la versión Samba 2.2.1a

Arrancamos Metasploit y buscamos exploit para Samba:

![METASPLOIT]({{ site.baseurl }}/images/kioptrix-level1-4.png)

Vamos a utilizar el de Trans2open. Lo cargamos y entramos en su información para ver con qué versiones de SAMBA se puede utilizar:

![Trans2open]({{ site.baseurl }}/images/kioptrix-level1-5.png)

Vemos que nos puede funcionar, ya que nuestra versión de samba está entre la 2.2.0 y la 2.2.8

Cargamos las opciones del exploit:

![Opciones-exploit]({{ site.baseurl }}/images/kioptrix-level1-6.png)

Vamos a buscar un payload para cargar en el exploit:

![Opciones-exploit]({{ site.baseurl }}/images/kioptrix-level1-7.png)

Vamos a usar el de reverse_tcp y le vamos pasando nuestra IP al parámetro LHOST:

![Reverse-tcp]({{ site.baseurl }}/images/kioptrix-level1-8.png)

Ejecutamos y vemos que ya tenemos una shell:

![shell]({{ site.baseurl }}/images/kioptrix-level1-9.png)

Ejecutamos whoami y vemos que somos ROOT:

![root]({{ site.baseurl }}/images/kioptrix-level1-0.png)


¡Reto conseguido!

