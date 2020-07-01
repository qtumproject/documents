# Guia de usuario para Qtum Electrum

Qtum Electrum es una billetera ligera de Qtum basada en la popular billetera de bitcoin [Electrum](https://electrum.org/)。

En comparacion con la billetera Qtum Core, Qtum electrum necesita menos espacio en disco, la sincronizacion de bloques necesita menos tiempo, soporta multiples firmas y billeteras de hardware, al igual que soporta billetera "fria", soporta importacion de billetera mediante palabras "mnemonic". Adopta la validacion SPV para simplificar su uso y asegurar la seguridad de la misma.

## Como usarla

### Instalacion

Abre [https://github.com/qtumproject/qtum-electrum/releases/latest](https://github.com/qtumproject/qtum-electrum/releases/latest) or [https://qtumeco.io/wallet](https://qtumeco.io/wallet) para encontrar la ultima version disponible.


Si estas usando linux, por favor referirse a [https://github.com/qtumproject/qtum-electrum/blob/master/README.md](https://github.com/qtumproject/qtum-electrum/blob/master/README.md).



### Crear y recuperar

La primera vez que abres la billetera, selecciona “Auto Connect” para conectarse a los servidores

A continuacion, selecciona el tipo de billetera que quieres crear.

![](http://ojaivn2ch.bkt.clouddn.com/cfaf17237ff138adf4c601eadedea24b.png)

Se recomienda usar la billetera estandard para la mayoria de usuarios, selecciona "crear nueva semilla" para crear una nueva billetera. O, escoge "Ya tengo una semilla" para recuperar tu billetera existente.

Si quieres recuperar utilizando mnemonic desde una billetera de Qtum Movil, escoge "Compatible con Qtum billetera Movil" 

### Enviar y recibir Qtum

![](http://ojaivn2ch.bkt.clouddn.com/d2ef6659a47a55686b6c6ef2fec58331.png)
Todas las transacciones relacionadas se pueden ver en la pagina de historial
<br>

![](http://ojaivn2ch.bkt.clouddn.com/7cdacbe408a98d3a00a9e128beb26e30.png)
En la pagina de enviar, ingresa la direccion de Qtum a donde quieres enviar y la cantidad de Qtum. Puedes modificar la tarifa por transaccion y luego click en enviar.
<br>

![](http://ojaivn2ch.bkt.clouddn.com/4e994a885963f09389d2c1be10e5924e.png)
Puedes obtener tu codigo QR de direccion en la pagina de recibir.


### QRC20 Token

![](https://s.qtum.site/uploads/9aaa8fa63651af737cceb6b59f339b45.png)
Haga click en Tokens para ir a la pagina de los tokens  
<br>

![](https://s.qtum.site/uploads/213e6caa5a8640e62ab616541de12627.png)
Click derecho en el espacio en blanco, y luego en "Add token".
<br>

![](https://s.qtum.site/uploads/0f92a355a82b1326493e2d643319f383.png)
Ingresa la direccion de contrato de token y selecciona tu direccion de Qtum
Puedes encontrar la direccion de contrato de token en [https://qtum.info/](https://qtum.info/) al buscar el nombre de token 

![](https://s.qtum.site/uploads/4bb33de12c19de3b59f8df2c90a704f1.png)
Puedes ver el balance del token y la historia de transferencias una vez lo agregues.
<br>

![](https://s.qtum.site/uploads/4eaa85f66778d2e051b7f1ddcb5107b9.png)
Click derecho en tu token, escoge las funciones.
<br>

![](https://s.qtum.site/uploads/53eac2382ad17d543c060261497299b5.png)
Ve a la pagina de enviar al hacer click en "send" ingresa la direccion del destinatario y la cantidad que quieres enviar.

## Multisig 

Leer: [http://docs.electrum.org/en/latest/multisig.html](http://docs.electrum.org/en/latest/multisig.html)

### Billetera de hardware

Ledger es un excelente ejemplo:

#### Antes de comenzar
Verifica que tienes:

* Una ledger nano S o una Ledger Azul
* Windows 7+, macOS 10.8+ o Linux;
* Un puerto USB. Utiliza un adaptador para los puertos USB-C
* Google Chrome / Chromium instalado.
* Qtum Electrum instalado.

#### Instalar la aplicacion de Qtum
* Lanza el [Ledger Manager](https://support.ledgerwallet.com/hc/en-us/articles/115005173209-How-to-use-the-Ledger-Manager).

* Conecta y desbloquea tu dispositivo con tu PIN

* Busca Qtum en la lista en la pestana de APPLICACIONES.

* Click en el boton con forma de flecha verde.

* Presiona el boton derecho en tu dispositivo cuando te pregunten: Allow Ledger Manager? 

* Verifica que la aplicacion esta correctamente instalada en tu dispositivo al ver su icono en el panel.

  Nota: Revisa las soluciones en este articulo si el dispositivo muestra un error y no puede instalar la aplicacion.

#### Utiliza Qtum Electrum 

* Conecta y desbloquea tu dispositivo con tu codigo PIN
* En Ledger Azul solamente: Abre la aplicacion de Qtum y coloca el soporte de navegador en "no" en la configuracion de la aplicacion
* Lanza Qtum Electrum en tu computadora. La billetera estara abierta despues de sincronizar.
* Crea nueva billetera, escoge tandard wallet` -> `Use a hardware device` , click `Next para continue.
* ![](http://ojaivn2ch.bkt.clouddn.com/0b2b70d7163e15df5efe59448d54ebc7.png)

## Mas informacion

Qtum Electrum esta bajo version beta actualmente, cualquier bug o falla por favor reportar.  [https://github.com/qtumproject/qtum-electrum/issues](https://github.com/qtumproject/qtum-electrum/issues)



