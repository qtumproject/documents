# [Como realizar Staking en FreeBSD]



# (https://docs.qtum.site/en/)

**Staking Qtum en FreeBSD** 

FreeBSD es un sistema operativo muy potente, tiene una gran historia de confiabilidad, seguridad y estabilidad. Aquí mostramos cómo se puede usar para hacer staking Qtum de una manera segura. 

**Aislando Qtumd en una cárcel (jail) FreeBSD** 

Las cárceles de FreeBSD son una característica muy poderosa, en resumen, su instancia de cárcel está más protegida ya que es como tener un sistema operativo separado solo para Qtum con privilegios reducidos. 

Aquí hay una buena lectura sobre las cárceles:  <https://www.freebsd.org/doc/handbook/jails.html>

**La versión de FreeBSD utilizada para este tutorial es 11.2, descárguelo de los espejos oficiales de FreeBSD:** 

<https://www.freebsd.org/doc/handbook/eresources-web.html>

**Instalando FreeBSD** 

Instale FreeBSD normalmente, sin embargo, se recomiendan las siguientes opciones de seguridad para la instalación: 

![hardening.png](https://docs.qtum.site/en/freebsd/hardening.png)

**Crear usuario** 

Crear un usuario con permisos “Operator wheel” 

![adduser.png](https://docs.qtum.site/en/freebsd/adduser.png)

Por favor, recuerda hacer todos estos comandos como root 

**Anfitrión:** 

**/etc/sysctl.conf** 

**Permitir sockets y actualizaciones en la cárcel** 

`security.jail.allow_raw_sockets=1`

`security.jail.chflags_allowed=1`

![sysctl.png](https://docs.qtum.site/en/freebsd/sysctl.png)

### /etc/rc.conf

`firewall_enable="YES"`

`firewall_quiet="YES"`

`firewall_type="workstation"`

`firewall_myservices="22 3888"`

`firewall_allowservices="any"`

`firewall_logdeny="YES"`

`jail_enable="YES"`

![rcconf.png](https://docs.qtum.site/en/freebsd/rcconf.png)

Tenga en cuenta que hemos agregado algunas configuraciones para el firewall, estas habilitarán IPFW y las configuraciones básicas para asegurar nuestra Cárcel, permitiendo que solo se acceda a los puertos 22 (ssh) y 3888 (Qtum). 

### Límites de recursos para las cárceles

### /boot/loader.conf

`kern.racct.enable=1`

`jail_enable="YES"`

![bootloader.png](https://docs.qtum.site/en/freebsd/bootloader.png)

### Creando nuestra carcel para staking

`zfs create -o mountpoint=/jail zroot/jail`

(Cambia zroot por el nombre que elijas para tu grupo de zfs)

`zfs create -o mountpoint=/jail/qtum zroot/jail/qtum`

![createqtumjail.png](https://docs.qtum.site/en/freebsd/createqtumjail.png)

### Ahora que hemos creado nuestra cárcel para hacer staking Qtum, busquemos e instalemos FreeBSD en ella.

`cd /jail/qtum/ && fetch -o - http://ftp.freebsd.org/pub/FreeBSD/releases/amd64/11.2-RELEASE/base.txz | tar --unlink -xpJf - -C /jail/qtum`

![fetch.png](https://docs.qtum.site/en/freebsd/fetch.png)

#### Ahora hemos instalado FreeBSD en / jail / qtum

Escribir ls / jail / qtum / debe mostrar el sistema de archivos de nuestra cárcel Qtum FreeBSD

Ahora, creemos el archivo de configuración de la cárcel:

### /etc/jail.conf

`qtum {` `host.hostname = qtum.local;` `ip4.addr = 192.168.0.99;` `interface = em0;` `path = /jail/qtum;` `exec.start = "/bin/sh /etc/rc";` `exec.stop = "/bin/sh /etc/rc.shutdown";``exec.clean;` `mount.devfs;` `allow.raw_sockets;` `allow.sysvipc;` `}`

![jailconfig.png](https://docs.qtum.site/en/freebsd/jailconfig.png)

Ok, ahora es el momento de lanzar nuestra cárcel!

`service jail start qtum`

#### Acabamos de comenzar con nuestra cárcel Qtum. Ahora podemos ingresar a nuestra cárcel Qtum para finalizar la configuración, instalar Qtum y abrir la billetera.

`jexec qtum /bin/csh`

`cp /usr/share/zoneinfo/America/YOURTIMEZONE/ /etc/localtime` Esto es muy importante, si la información del tiempo es incorrecta, produciremos bloques huérfanos o no podremos sincronizar

Crea nuestro /etc/rc.conf básico para nuestra Cárcel Qtum

## Carcel Qtum:

### /etc/rc.conf

`syslogd_flags="-s -s"` `sshd_enable=YES` `clear_tmp_enable=YES` `clear_tmp_X=YES``extra_netfs_types=NFS` `dumpdev=NO` `update_motd=NO` `keyrate=fast`

`sendmail_enable=NONE`

`sendmail_submit_enable=NO` `sendmail_outbound_enable=NO` `sendmail_msp_queue_enable=NO`

## Agregue servidores de nombres dns a /etc/resolv.conf

`echo "nameserver 8.8.8.8" >> /etc/resolv.conf` `echo "nameserver 8.8.4.4" >> /etc/resolv.conf`

## Instalando Qtum

Ahora que tenemos nuestra cárcel en funcionamiento, necesitamos instalar Qtum. Hay 2 opciones para hacer esto, podemos usar el repositorio pkg o los poderosos puertos FreeBSD que generalmente se actualizan más rápido:

#### pkg repositorio

`pkg update -f` `pkg install -y qtum`

![pkginstallqtum.png](https://docs.qtum.site/en/freebsd/pkginstallqtum.png)

#### Puertos FreeBSD

`portsnap fetch extract` `cd /usr/ports/net-p2p/qtum && make install clean`

![portsnapfetchextract.png](https://docs.qtum.site/en/freebsd/portsnapfetchextract.png)Lo anterior pedirá muchas opciones de configuración, podría ser mejor usar make config-recursive para establecer todas las opciones antes de compilar. Si desea usar configuraciones predeterminadas solo escriba `cd /usr/ports/net-p2p/qtum && make install clean BATCH="YES"`

### Ejecutando Qtum

El lanzamiento de Qtum es como en cualquier otro sistema operativo * NIX, sin embargo, aquí hay una pequeña diferencia debido a cómo funcionan las cárceles de FreeBSD. Primero, necesitamos crear un archivo qtum.conf con los siguientes contenidos:

![qtumconf.png](https://docs.qtum.site/en/freebsd/qtumconf.png)

Esta configuración es necesaria; de lo contrario, llamar al daemon devolverá los errores.

Entonces podemos lanzar con`qtumd -daemon`

## Consejos de seguridad

- Configure el firewall en el host (no puede configurar un firewall dentro de una cárcel) y habilite solo los puertos que necesita (22 y 3888) Esto se hace en el host rc.conf en la parte superior de este tutorial.
- Deshabilita el historial, esto deshabilitará completamente el historial de la consola y es una manera de ayudar a proteger su staking box, escribe lo siguiente en tu consola de FreeBSD: `unset history; unset savehist`
- Asegure SSH: 
  1. Deshabilitar autenticación de contraseña![ssh2.png](https://docs.qtum.site/en/freebsd/ssh2.png)![ssh4.png](https://docs.qtum.site/en/freebsd/ssh4.png)![ssh5.png](https://docs.qtum.site/en/freebsd/ssh5.png)
- Si usa el cuadro de FreeBSD en su red doméstica,  obliguelo a escuchar solo en la red local.

![ssh1.png](https://docs.qtum.site/en/freebsd/ssh1.png)