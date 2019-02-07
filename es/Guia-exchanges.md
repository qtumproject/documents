# Guía e información para instalar Qtum en Exchanges 

## **Instalación**

Puedes descargar una version lista de Qtum de nuestra pagina de lanzamientos de Github:

https://github.com/qtumproject/qtum/releases/

Simplemente extrae el archivo de 64bit de linux .tar.gz. En el directorio "bin" se encontraran los dos programas de interes, `qtum-cli` y `qtumd`

Si ud elige compilar Qtum manualmente, siga estos pasos en Ubuntu:

Instalar los siguientes paquetes:


```
sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils git cmake libboost-all-dev

sudo apt-get install software-properties-common

sudo add-apt-repository ppa:bitcoin/bitcoin

sudo apt-get update

sudo apt-get install libdb4.8-dev libdb4.8++-dev
```



```
git clone https://github.com/qtumproject/qtum --recursive
git checkout mainnet-ignition-v1.0.1 # or use the latest release
./autogen.sh
./configure --with-gui=no --enable-hardening
make -j3
```

Luego, en el directorio "src", encontraras 2 programas mencionados anteriormente,  `qtumd y `qtum-cli`

## Iniciar

Para lanzar qtumd, utiliza lo siguiente:


```
./qtumd -daemon -staking=0
```

opciónes adicionales pueden ser especificadas en `~/.qtum/qtum.conf`, ud tambien puede agregar `-staking=0` en el archivo  de configuracion qtum.conf

Luego, puedes verificar el estado del nodo Qtum:


```
./qtum-cli getinfo
```


Esto mostrara un numero de bloques, cuando el numero de bloques muestre el numero mas reciente en nuestro block explorer: [https://explorer.qtum.org](https://explorer.qtum.org) entonces esto significara que el nodo se ha sincronizado. Si muestra bloque 0 y 0 conexiones por mas de unos minutos, contacte al equipo de Qtum para pedir ayuda. Sincronizando la blockchain puede demorar de 1 - 4 hrs dependiendo de la velocidad de su conexión y especificaciones del servidor.


Para apagar el nodo, simplemente escriba:

```
./qtum-cli stop
```

**NOTA:** `-staking=false` deshabilita staking automatico en la billetera. Esto es  **ALTAMENTE RECOMENDADO** para  exchanges. Staking puede provocar que un numero impredecible de monedas sean inaccesibles por 500 bloques (mas o menos 20 horas) por lo tanto, se recomienda que los exchanges no participen en staking.

## Copia de seguridad de la Billetera

Asegurese de siempre hacer copias de seguridad de la billetera! La ubicación de la billetera en Linux es `~/.qtum/wallet.dat`. Asegurese de detener el nodo antes de hacer una copia de seguridad, esto es para proteger la integridad de los datos.

La billetera también se puede cifrar:


```
./qtum-cli encryptwallet "tu clave"
```

El nodo de Qtum se detendrá automáticamente para cifrar la billetera. deberás ejecutar `./qtumd -daemon -staking=false` nuevamente para volver a iniciar el nodo.

**IMPORTANTE:** luego de cifrar la billetera,  **ES OBLIGATORIO** hacer una nueva copia de seguridad del archivo wallet.dat. Si no haces esto, puedes **PERDER LAS MONEDAS**. Si olvida o pierde la clave para la billetera cifrada,  **NO HABRA FORMA DE RECUPERAR LAS MONEDAS**. Asegurese de hacer backups de ambos wallet.dat al igual que la clave utilizada para cifrar!

Para desbloquear la billetera:


```
./qtum-cli walletpassphrase "your strong password" XXX
```


XXX es la cantidad de segundos que la billetera permanecerá desbloqueada. Así que, especificar "1000" significa que la billetera estará desbloqueada por 1000 segundos.

**NOTA:** Desbloquear la billetera solo es necesario para enviar monedas. Si solamente necesitas recibir y hacer seguimiento de transacciones, esto se puede hacer con una billetera cifrada y bloqueada.

## Recibiendo monedas

Para generar una nueva dirección:


```
./qtum-cli getnewaddress ""
```

Esto va a crear una dirección unica cada vez que se ejecute. Nota que las direcciones de Qtum comienzan con una Q. O direcciones pubkeyhash estandard, y comienzan por M para direcciones Multi-sig.

Para validar una dirección:


```
./qtum-cli validateaddress "dirección aqui"
```

Para ver las monedas recibidas por una dirección particular (nota que la dirección debe pertenecer a esta billetera). Esto no permite revisar direcciones que no pertenecen a esta billetera):


```
./qtum-cli getreceivedbyaddress "dirección aqui" MINCONF
```

En este caso, `MINCONF` es cuántas confirmaciones necesita tener la transaccion en blockchain para que sea incluida en este numero.

###  Cantidades de confirmaciones minimas recomendadas por Qtum:

- 10 confirmaciones para pequenas y grandes cantidades. 

Para listar todas las transacciones (incluyendo las no confirmadas) siendo rastreadas por esta billetera, utiliza esta función:


```
./qtum-cli listtransactions "*" COUNT SKIP
```

COUNT y SKIP pueden ser usados para pasar entre transacciones, si se utiliza un conteo muy largo, el nodo puede completar la solicitud demasiado lento, y por lo tnato se recomienda nunca usar un COUNT de mas de 100.

SKIP se usa para "saltar" los primeros resultados. No se recomienda confiarse solamente en esto para manejar la contabilidad de un exchange. Es posible que mientras ud ejecute este proceso, alguien envie una transaccion a la billetera la cual no sera tenida en cuenta por ese comando. Ademas, este metodo incluye transacciones **NO CONFIRMADAS** y deberá ser usado con precaución.

## Enviando monedas

No es posible dictar desde que dirección se deben enviar las monedas. Si la plataforma de exchange necesita enviar de una dirección fija, seria mejor hacer unos ajustes al sistema para que no sea necesario.

Para enviar monedas:


```
./qtum-cli sendtoaddress "dirección a la que vamos a enviar" AMOUNT "comentario acerca de tx" "comentario acerca de dirección" SUBTRACTFEE
```

Los argumentos de comentario se pueden dejar en blanco si se desea. Estos comentarios se guardan en la billetera y son usados por algunos exchanges para mantener registro de retiros y de usuarios.

La opción SUBTRACTFEE puede ser "true" o "false". Cuando esta opción esta en "true" se resta la tarifa de la cantidad enviada, es decir, si hacemos lo sgte:


```
./qtum-cli sendtoaddress "dirección" 10 "" "" true
```

Y la tarifa de red es 0.1 Qtum, entonces la cantidad total recibida por el usuario sera 9.9 Qtum. Si SUBTRACTFEE esta colocada en falso, entonces recibirán 10 Qtum, pero, la billetera del exchange habra pagado 0.1 Qtum por tarifa de transaccion.

**NOTA:** Usuarios de exchange no deberian poder enviar monedas directamente a una dirección de contrato inteligente (comenzando con 0x). Estas direcciones seran rechazadas por sendtoaddress y su uso correcto requiere muchisima mas precaución.

## Parametros

- Tarifa de transaccion recomendada: 400000sat o 0.004 Qtum por kilobyte de datos de transaccion (2kb es un tamaño razonable pero a veces puede ser mayor)
- Confirmaciones recomendadas 10
- Cantidad minima de retiro recomendada: 0.1 Qtum
- Puerto P2P: 3888 (port forwarding no es necesario o recomendado, pero la billetera debe ser capaz de acceder otros nodos externos mediante este puerto para poder descargar la blockchain.
