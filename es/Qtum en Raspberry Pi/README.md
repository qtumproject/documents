# Qtum en Raspberry Pi

Al igual que hicimos con Debian, tenemos que descargar e instalar la llave pública de Qtum.

`wget -qO - https://repo.qtum.info/apt/public.key | sudo apt-key add -`

Esto descarga e instala la llave pública Qtum

### Agregar repositorio a sus fuentes APT.

`sudo su` - primero, hagan "sudo a root"

`echo "deb https://repo.qtum.info/apt/raspbian/ jessie main" >> /etc/apt/sources.list` or`echo "deb https://repo.qtum.info/apt/raspbian/ stretch main" >> /etc/apt/sources.list`

Esto agregará el repositorio a su archivo de fuentes APT.

### Refrescando fuentes APT e instalando Qtum

`sudo apt update && sudo apt install qtum`

Al hacer esto, actualizaremos nuestras fuentes e instalaremos Qtum en nuestro raspberry Box, que puede actuar ahora como un servidor de staking / nodo.

## Cambiar la contraseña predeterminada

Esta opción se recomienda por razones de seguridad, la contraseña predeterminada en el pi es bien conocida, se recomienda encarecidamente cambiarla al primer inicio de sesión.

Para cambiarla solo escribe: `passwd`

El aviso le pedirá que escriba y repita la nueva contraseña para confirmar.

## Protección de acceso con un firewall básico

Bueno, nuestra raspberry es solo para staking, no hay necesidad de tener todos esos puertos abiertos, cerremos todo lo que no necesitamos y solo permitamos el acceso a los servicios necesarios.

Primero, instalemos UFW (firewall sin complicaciones) que es una interfaz fácil de usar para iptables

`sudo apt install ufw`

Una vez que esto esté instalado, procedemos con los permisos de acceso, definiremos qué puertos serán accesibles. Veamos primero lo que está abierto:

`sudo ufw status` Esto debería mostrar algo como esto: 

`Status: active`

`To Action From`

`-- ------ ----`

`22 ALLOW Anywhere`

#### Ok, entonces es hora de comenzar a cerrar el acceso, escriba lo siguiente:

`sudo ufw default deny incoming`

`sudo ufw allow 3888/tcp`

`sudo ufw allow 3889/tcp`

Aquí hemos definido los conceptos básicos, cerrando todo excepto el puerto 3888 y 3889 que Qtum usa para funcionar.

Si está utilizando SSH, se recomienda permitir solo el acceso desde la red local..

`sudo ufw allow from 196.168.0.0/24 to any port 22`

## Lanzando Qtum daemon

Todo lo que necesitamos hacer para iniciar el daemon Qtum es escribir: `qtumd -daemon`

Tan pronto como escriba esto, la billetera creará el archivo wallet.dat entre otros archivos (si aún no están allí). La billetera se ejecutará y comenzará a sincronizarse instantáneamente desde los otros nodos de Blockchain, esto puede tardar unas horas en completarse, asi que preparate y toma una taza de café y deja que se sincronice.

## Encriptación de la billetera

Podemos encriptar la billetera en cualquier momento, es mejor hacerlo antes de seguir adelante.

Para hacer esto, escriba lo siguiente en la línea de comando:

`qtum-cli encryptwallet yourpassword`

Esto encriptara la billetera que a su vez cierra el daemon, verá el siguiente mensaje:

`wallet encrypted; Qtum server stopping, restart to run with encrypted wallet.` Si ya hizo una copia de seguridad antes de encriptar, **necesita hacer una nueva copia de seguridad.** 

`qtum-cli getaccountaddress` "" -> Inmediatamente después de iniciar el daemon, puede obtener su dirección de billetera escribiendo esto.

Puede enviar monedas de Qtum a la dirección que acabamos de obtener del daemon, recuerde que esas transacciones requieren al menos 500 confirmaciones antes de que sean lo suficientemente maduras para staking.

## Staking

Ahora que hemos esperado hasta que tengamos al menos 501 confirmaciones en nuestra transacción recibida, somos elegibles para staking, sin embargo, si nuestra billetera está encriptada (que lo hicimos por razones de seguridad) no podremos hacer staking, vamos a abrir nuestra billetera para staking usando la línea de comando!.

`qtum-cli walletpassphrase password 999999999 true`

¡El comando anterior desbloqueará la billetera durante 31.6 años! eso debería ser suficiente por ahora. Tenga en cuenta que esto no desbloqueará su copia de seguridad, solo la billetera que se está ejecutando en este momento.

Ahora que hemos desbloqueado nuestra billetera, debemos esperar hasta que tengamos más de 501 confirmaciones para ser elegibles para el staking, si ya lo hacemos, es una cuestión de tiempo que variará según el peso de la red y el peso de su billetera.

## Comprobando el Saldo

Para verificar su saldo, escriba qtum-cli getinfo esto le mostrará información general, incluido su saldo y saldo disponible en staking.

## Verificar Transacciones

Para verificar sus transacciones (entrantes y salientes) escriba qtum-cli listtransactions

## Verificar información de staking

Para verificar la información de staking de Qtum, escriba qtum-cli getstakinginfo

## Consejos para Staking

El staking depende realmente del peso de la red y del peso de tu billetera, que se basa en la cantidad de monedas que tengas, un mayor peso aumenta tus posibilidades de hacer staking por un bloque.

Si tiene una gran cantidad de monedas, es una buena idea dividirlas en transacciones separadas, por ejemplo, si tiene 10,000 QTUM, es mejor enviar 10 transacciones de 1000 QTUM cada una a su billetera, cada una genera una entrada UTXO que tomará parte en el staking. Esto optimiza el proceso de replanteo y funciona mucho mejor que solo una gran entrada 10.000 QTUM.

Si desea dividir sus monedas en diferentes direcciones dentro de su billetera VPS, escriba lo siguiente para obtener nuevas direcciones dentro de su billetera: qtum-cli getnewaddress Cada vez que escriba esto, obtendrá una nueva dirección, QTUM puede generar cualquier cantidad de direcciones que desee, pero por favor tenga en cuenta que si se pasa de 100 direcciones nuevas, es posible que tenga que hacer una nueva copia de seguridad de su billetera.

## Actualización de la billetera

Siempre estamos lanzando nuevas actualizaciones, a veces es para agregar nuevas características o corregir errores. De todas formas la actualización es muy sencilla, todo lo que tienes que hacer es escribir `sudo apt update && sudo apt install —only-upgrade qtum`
