# Comandos

La billetera Qtum Core tiene un amplio conjunto de comandos que brindan un control integral de la billetera y las transacciones de blockchain. Hay dos conjuntos de comandos que se pueden usar con las billeteras Qtum Core:

- Los comandos de la consola se dan a una billetera que ya se está ejecutando.
- Los comandos de inicio se utilizan al iniciar una billetera.

Este manual se enfoca en los comandos de la consola que se dan a una billetera que se está ejecutando y se pueden enviar usando RPC (Llamadas de procedimiento remoto) o en la línea de comandos a la billetera del servidor qtumd o se pueden entregar a la GUI de escritorio qtum-qt (Interfaz gráfica de usuario ) usando la línea de comando de la consola de la ventana de depuración (consulte la Figura 1).

![2019-1 Mac Debug Window with Prompt](https://i.imgur.com/K0uCLVr.jpg) Figura 1. La consola qtum-qt

Tenga en cuenta el mensaje de advertencia en rojo en la Figura 1 y tenga cuidado al usar los comandos de clave privada (`dumpprivkey` y` dumpwallet`) con las billeteras Mainnet.

Para la billetera del servidor qtumd, los comandos de la consola se proporcionan mediante la aplicación de interfaz de línea de comandos qtum-cli en el indicador de línea de comandos del sistema (consulte la Figura 2).

![2019-2 Command Line Win](https://i.imgur.com/m1xp3ng.jpg) Figura 2. Indicador de línea de comando del sistema

Siempre puede obtener una lista de los comandos de consola actuales utilizando el comando de ayuda (consulte la Figura 3.)

![2019-3 Help Command Mac](https://i.imgur.com/w8yGO2G.jpg) Figura 3. El comando de ayuda

## Comandos de consola :hammer_and_wrench:

Los comandos de la consola se entregan a una billetera Qtum Core en ejecución y proporcionan información y control adicionales. Los comandos de la consola y son necesarios para operar la billetera del servidor qtumd, que es una billetera "sin cabeza" sin interfaz gráfica de usuario.

Hay 136 comandos de consola con algunas buenas referencias para el 112 heredado de bitcoin. Hay 13 comandos "ocultos" que utilizan los desarrolladores y que no aparecerán en la lista de "ayuda".

Los comandos pueden tener parámetros obligatorios u opcionales y los parámetros más numerosos se ingresan en formato JSON (JavaScript Object Notation) con comillas dobles escapadas (\ ") como se muestra a continuación.

Los parámetros comunes para estos comandos son direcciones Qtum, hashes de bloque, direcciones de contrato, etc. Algunos de los comandos tendrán un parámetro opcional "minconf" (confirmaciones mínimas) que le permite obtener una respuesta para una transacción o bloque que tenga al menos eso Número de confirmaciones.

La referencia de la cadena de consulta de bitcoin API http://chainquery.com/bitcoin-api explica los parámetros y da ejemplos con respuestas para los comandos heredados de bitcoin. La reverencia API de consulta de cadena de bitcoin proporciona 67 comandos, de los cuales 2 no están en Qtum (`Estimación prioritaria`,` getgenerate`) y dos (`gettransaction`,` walletpassphrase`) tienen un parámetro adicional para Qtum. Ver también https://bitcoin.org/en/developer-reference#remote-procedure-calls-rpcs.

Las interfaces avanzadas para la billetera Qtum Core (nodo completo) pueden usar estos "comandos de consola" como RPC (Llamadas de procedimiento remoto) a través de una conexión de puerto dedicada al nodo. Para construir una billetera activa de intercambio o un nodo de servidor para una DAPP (aplicación distribuida) móvil, puede usar RPC, que siguen estos mismos comandos de consola. El nodo cliente ofrece una interfaz JSON-RPC a través de sockets HTTP para realizar diversas funciones operativas y administrar el nodo local.

Un comentario rápido sobre "cuentas". Las cuentas eran una forma desafortunada de Bitcoin para rastrear los saldos de lo que realmente son valores basados en transacciones UTXO, y las "cuentas" están en desuso y se eliminarán gradualmente en la versión 0.18.

Aquí hay algunos grupos de comandos que son útiles para diversas tareas:

- Conexiones entre pares: `getconnectioncount`, `getpeerinfo`, `addnodes`, `getnetworkinfo`
- Staking: `getstakinginfo`, `getwalletinfo`, `getnetworkinfo`
- Enviando: `listaddressgroupings`, `sendtoaddress`, `sendmany`, `sendmanywithdupes`
- Transacciones sin procesar:`crearterawtransaction`, `signrawtransaction`, `combinerawtransactoins`, `sendrawtransaction`
- Transacciones de contratos inteligentes:`createcontract`, `callcontract`, `sendtocontract`, `getaccountinfo`, `getstorage`, `searchlogs`, `waitforlogs`

## Comandos de inicio

Los comandos de inicio ofrecen opciones adicionales de control y recuperación al iniciar la billetera. Por ejemplo, puede usar comandos de inicio para varios tipos de técnicas de recuperación de blockchain, registro de depuración adicional o controles adicionales. Si va a utilizar estos comandos de inicio, asegúrese de tener una buena copia de seguridad del archivo wallet.dat.

Vea los comandos de inicio en la billetera qtum-qt con Ayuda - Opciones de línea de comandos:

![2019-4 Startup Commands Win](https://i.imgur.com/CryGF13.jpg) Figura 4. Comandos de inicio

y en la línea de comando con "qtumd -?":

![2019-5 Startup Commands Command Line Win](https://i.imgur.com/KCmxFaC.jpg) Figura 5. Comandos de inicio desde la línea de comandos

## Comandos de consola A - Z

Para estos comandos de consola documentados a continuación, se proporcionan respuestas para los parámetros predeterminados (Qtum versión 0.16 - invierno 2018/2019). Los comandos marcados como DEPRECATED no deben usarse porque se eliminarán y reemplazarán en futuras versiones de la billetera, por ejemplo, los comandos que usan "cuenta" se eliminarán en la versión 0.18.

El uso del comando "help \" le dará información completa sobre el comando y los parámetros relevantes, formateados de manera que pueda copiarlos y pegarlos (reemplazando las direcciones, ID de transacciones, etc., según sea necesario). El siguiente formato muestra el comando con parámetros seguidos de la respuesta, en algunos casos, los parámetros o las respuestas se truncan con el término "\". Donde se indique, algunos comandos solo funcionan con la red regtest (Prueba de regresión). Muchos comandos devolverán "nulo" para qtum-qt y no devolverán nada para los sistemas de línea de comandos.

### abandontransaction "txid"

Funciona en transacciones que no están en blockchain o mempool, utilizadas en pruebas.

```
abandontransaction "0cc99a30bc2064041ea4263835b4ed594ff500c56d6b14e4970aeee548e71389"

Transaction not eligible for abandonment (code -5)
```

### abortrescan

Detiene una nueva exploración de billetera activada por un comando como `importprivkey`. Este comando puede emitirse abriendo una segunda ventana de línea de comando (donde se escanea la primera ventana), en cuyo caso el comando detendrá el escaneo y devolverá "verdadero".

```
qtum-cli abortrescan

true
```

### addmultisigaddress nrequired ["key",...] ( "account" "address_type" )

Agregue una dirección de múltiples firmas a la billetera para que pueda recibir y enviar desde esa dirección. Ejecute el comando en cada máquina que firmará y haga una copia de seguridad del archivo wallet.dat. La dirección puede ser una dirección Qtum o una clave pública codificada en hexadecimal. Use `importaddress` para agregar la dirección multigrado en cada billetera de firma.

Esta funcionalidad solo está diseñada para usarse con direcciones que no sean de vigilancia. Consulte `importaddress` para ver solo el soporte de la dirección p2sh. El uso de la cuenta está DEPRECADO). Ver también `validateaddress`.

```
addmultisigaddress 2 "[\"QgdaD9b3ppKowoC45EZMtepjjBfnvEe6m\",\"QFmr8vY29reHj73XSHfdWvkV3mD57Kqd8\"]"

{
  "address": "mHB9w64hHbm2YtCxyqS8kG3g77b2gbSvK",
  "redeemScript": "5321538ef45ab52bd53508adfda3cfe82ebcaf0495963729e5ff2a8e5aeecdd4cdd23daea03cf4394ad4c578caff2d297ce937c3afba5bc56f31c786b2addf56c72ab"
}
```

### addnode "nodo" "agregar | eliminar | onetry"

Intenta agregar un nodo con una dirección IP conocida. Este comando es útil para nuevas billeteras que tienen problemas para hacer conexiones entre pares. Aquí hay algunas buenas direcciones IP para agregar, puede poner estos comandos uno tras otro, luego la billetera intentará durante unos minutos establecer una conexión entre pares. Qtumd no devuelve nada:

```
addnode 35.200.159.68:3888 add
addnode 35.197.138.163:3888 add
addnode 35.226.31.206:3888 add
addnode 35.200.130.53:3888 add
addnode 35.192.54.161:3888 add
```

Qtum-qt devuelve "nulo" después de cada uno (ver Figura 6).

![2019-6 addnode Mac](https://i.imgur.com/RjRkiP8.jpg) Figura 6. Ingresando el comando addnode

### addwitnessaddress "dirección" ( p2sh )

Comando oculto OBSOLETO. Este comando era una forma de generar una dirección SegWit a partir de una dirección heredada existente, generalmente una dirección P2SH-P2WPKH: secuencia de comandos Pay-to-Witness-Public-Key-Hash (P2WPKH) incrustada en una secuencia Pay-to-Script-Hash (P2SH) ) habla a. Este comando está deshabilitado principalmente en la versión 0.16 y se eliminará en la versión 0.17. En su lugar, use el comando `getnewaddress` con el tipo de dirección" p2sh-segwit "o" bech32 ".

Ejecute v 0.16 qtumd con `-deprecatedrpc = addwitnessaddress` para ejecutar el comando:

```
addwitnessaddress QkSc3wcAJ59Nk4X9mvd258ycVxJ7XWhp9

MHa57hGwD48SZQjh23MZbq24tFwTu7Q3c
```

### backupwallet "destino"

El destino puede ser un nombre de archivo o ruta con un nombre de archivo. La billetera debe estar completamente descifrada (no solo para replantear) para que este comando funcione. qtum-qt devolverá "nulo", qtumd no devolverá nada. En Windows:

```
backupwallet "C:\Users\<username>\Desktop\Backups\backup2018-10-21.dat"

null
```

### bumpfee "txid" (opciones)

Topa la tarifa de una transacción, reemplazándola por una nueva transacción ajustando el cambio. La nueva tarifa se puede calcular automáticamente o utilizando varias opciones.

```
bumpfee "cae25062777fca1bce7f860dd238af2be4495f4aef1b5a15bbee260b4c3cde2"

{
  "txid": "ecbc798c140b5104ae3d5828493e8e5ef04131dd0e44eb7fa7e1abba24901a5",
  "origfee": 0.00090400,
  "fee": 0.00093061,
  "errors": [
  ]
}
```

### callcontract "dirección" "datos" (dirección)

Argumentos:

1. "dirección" (cadena, requerida) La dirección de la cuenta
2. "data" (cadena, requerida) La cadena hexadecimal de datos
3. dirección (cadena, opcional) La cadena hexadecimal de la dirección del remitente
4. gasLimit (cadena, opcional) El límite de gas para ejecutar el contrato

POR VENIR.

### clearbanned

Borre todas las IP de nodos prohibidos. Qtum-qt devuelve "nulo", qtumd no responde.

```
clearbanned

null
```

### combinerawtransaction ["hexstring",...]

Combine múltiples transacciones sin procesar parcialmente firmadas en una sola transacción. La transacción combinada puede ser otra transacción parcialmente firmada o una transacción totalmente firmada. Aquí se combinan dos transacciones en bruto:

```
combinerawtransaction "[\"0200000001b<snip>000000\", \"0200000001c<snip>000000\"]"

0200000001b<snip>000000
```

### createcontract "bytecode" (emisión de "senderaddress" de gaslimit gasprice)

Publique un contrato inteligente para el código de bytes dado, utilizando el precio de gas predeterminado de 0.00000040 y la cantidad de gas de 2.500.000. Devuelve el ID de la transacción y la dirección del contrato hash.

```
createcontract 60606040<snip>41701d0029

{
  "txid": "a1d823cb5ce776200dcbe729d901d4e1d31ad5bb8d835db0f704g73ac8e74d3",
  "sender": "QfdR8vwd69oMi2xeeSe8XBgv3mku27ukh",
  "hash160": "efe574bu5ce54a7eb33f96e4336accbed826ffe",
  "address": "4853cd349027fe239fed85837456b3c48aae42a"
}
```

### createmultisig nrequired ["clave", ...]

OBSOLETO. Utilice `addmultisigaddress`.

### createrawtransaction [{"txid":"id","vout":n},...] {"address":amount,"data":"hex",...} ( locktime ) ( replaceable )

Cree una transacción sin formato codificada en hexadecimal enviando algunas entradas a las salidas. La transacción debe ser firmada y enviada a la red, ver `signrawtransaction` y` sendrawtransaction`. Devuelve una transacción sin formato codificada en hexadecimal. Si está enviando monedas, asegúrese de crear una dirección de cambio para que se pueda devolver el cambio; cualquier diferencia entre los valores de entrada y los valores de salida se tomarán como tarifa de transacción. Si no resuelve las matemáticas, podría pagar una gran tarifa de transacción.

```
createrawtransaction "[{\"txid\":\"17b3f9ef530695ef2e0368e445a3b59bf12811bdfd42325bb14248e72deb7e2\",\"vout\":0}]" "{\"Qd5eHho389mJMCxSzAbe31w2vntTc7192\":1.0, \"QdXtq55Bf443Lkme2hdj4mD8KKepk32f6\":0.99}"

020000001d637cf207c6418fb6220cfcb2b141ba5d230f0ba0a43c68b358aff9a8a6000000000fffffff0509e5f50480000001983a952d5fb15a70832ffdc3cadd3dc7749a49bf053ed6defacd09ef6060000000187aa814bd4ae4167bebbf56bb7c51c5eabf35d50a5c6e7f33ad0000000
```

### decoderawtransaction "hexstring" ( iswitness )

Da los datos decodificados de una transacción sin codificar en hexadecimal. Aquí decodificamos los resultados de `createrawtransaction` arriba.

```
decoderawtransaction 0200000<snip>f33ad0000000

{
  "txid": "c93dace459f5ac38c9d28ded224e47364abdde5e3fa947dc2d9c4422afb8852",
  "hash": "c93dace459f5ac38c9d28ded224e47364abdde5e3fa947dc2d9c4422afb8852",
  "version": 2,
  "size": 119,
  "vsize": 119,
  "locktime": 0,
  "vin": [
    {
      "txid": "17b3f9ef530695ef2e0368e445a3b59bf12811bdfd42325bb14248e72deb7e2",
      "vout": 0,
      "scriptSig": {
        "asm": "",
        "hex": ""
      },
      "sequence": 4384362583
    }
  ],
  "vout": [
    {
      "value": 1.00000000,
<snip>
    }
  ]
}
```

### decodescript "hexstring"

Decodifique un script codificado en hexadecimal, por ejemplo, decodifique el script para una dirección mulitsig:

```
decodescript 52460396bc49812bad50949fbc0bbd44e95bf32a5695519b3ff267a5d93cba3bd169b2393cd4864da4c2786dd3322fcfcb239c3db185ef33fa14836b8fecf36c68bb84ddac92f2

{
  "asm": "2 0396c2483bbc207827fbc06fb32f48bf28450b5fb973032b742aeedd98dadcf3ba 02ba529ef3455bcc4339dbd7269acc2de135ff65a33c706a9beef48c37ab2a95ab 2 OP_CHECKMULTISIG",
  "reqSigs": 2,
  "type": "multisig",
  "addresses": [
    "Qgw5Ds4Py6J2oBX3EKP3kyde2UpnWn7eV",
    "QK3bx79fzkei5XF7h2q7wB4s6MK99u29x"
  ],
  "p2sh": "mKa7c52cX97eK4vdk35jV442p3j59hk3R"
}
```

### disconnectnode "[dirección]" [nodeid]

Desconecta un par (nodo) utilizando la dirección IP o el número de nodo. Qtum-qt devolverá "nulo", qtumd no devolverá nada.

```
disconnectnode "35.198.0.76:3888"

null
```

### "dirección" dumpprivkey

Muestra la clave privada para una dirección determinada en WIF (Formato de importación de billetera). La billetera debe estar desbloqueada (y no solo para "staking") para que este comando funcione.

```
dumpprivkey "QXfSbN8DaT21Z6L3Pw52UexuP8zW4mY6h"

L3vaEHms4VpciP85UsufQf3Gfa9p5gatBGm6Z4rD8FxzFLdXE5V
```

### dumpwallet "nombre de archivo"

Escribe todas las claves privadas de la billetera en un archivo en formato de texto claro (sin cifrar). La billetera debe estar completamente descifrada (no solo para replantear) para que este comando funcione. Devuelve el nombre del archivo. Dumpwallet guardará todas las claves privadas y sus direcciones; no guardará solo las direcciones de vigilancia (que no tienen claves privadas en la billetera). Este archivo contiene todas las claves privadas en la billetera (1,000 o más), tenga mucho cuidado y no almacene el archivo de volcado en línea.

En PC:

```
dumpwallet "C:\Users\<username>\Desktop\Backups\dump 2018-10-30.txt"

{
  "filename": "C:\\Users\\<username>\\Desktop\\Backups\\dump 2018-10-30.txt"
}
```

Archivo:

```
  Wallet dump created by Qtum v0.16.1.0-0806c12c4-dirty
  * Created on 2018-10-31T01:56:32Z
  * Best block at time of backup was 241161 (b11d5169d66d39cbcd848e2ea3f9adfcee1c22af945f100aec9e762d88609e2e),
    mined on 2018-10-31T01:55:28Z

  extended private masterkey: <snip>
```

En Mac:

```
dumpwallet /Users/<USERNAME>/Desktop/dump_2018-12-15.txt

{

  "filename": "/Users/<USERNAME>/Desktop/dump_2018-12-15.txt"

}
```

Archivo:

```
  Wallet dump created by Qtum v0.16.2.0-47a30461d-dirty
  * Created on 2018-12-16T02:22:59Z
  * Best block at time of backup was 148510 
(ca8a9457a69882b395bf56671e3661e148d3aca4a7b6c77398804229e7fb58f4),
    mined on 2018-05-06T02:45:52Z

  extended private masterkey: <snip>
```

### encriptar "frase de contraseña"

Cifra la billetera con "frase de contraseña" para el cifrado por primera vez. Después del cifrado, cualquier llamada que interactúe con claves privadas como el envío o la firma requerirá una entrada de frase de contraseña para habilitar estas funciones. Consulte también `walletpassphrase`,` walletlock` y `walletpassphrasechange`. Después de que se ejecute este comando, la billetera se cerrará.

```
encryptwallet "you should always use a long and strong passphrase"
```

(salida de billetera)

### echo "mensaje"

Comando oculto Simplemente repita los argumentos de entrada. Este comando es para probar.

La diferencia entre `echo` y` echojson` es que `echojson` tiene habilitada la conversión de argumentos en la tabla del lado del cliente en qtum-cli y la GUI. No hay diferencia del lado del servidor. Aquí hacemos eco de los parámetros utilizados para configurar una dirección multisig.

```
echo "[\"qghwDvb1pyJoqoAD2ESMTevvvjUfNvReDn\",\"qfKr7vXdmroHi61XUUHedXvgV2mDx9Kudb\"]"

[
  "[\"qghwDvb1pyJoqoAD2ESMTevvvjUfNvReDn\",\"qfKr7vXdmroHi61XUUHedXvgV2mDx9Kudb\"]"
]
```

### "mensaje" echojson

Comando oculto Simplemente repita los argumentos de entrada. Este comando es para probar.

La diferencia entre `echo` y` echojson` es que `echojson` tiene habilitada la conversión de argumentos en la tabla del lado del cliente en qtum-cli y la GUI. No hay diferencia del lado del servidor. Aquí hacemos eco de los parámetros utilizados para configurar una dirección multisig.

```
echojson
"[\"qghwDvb1pyJoqoAD2ESMTevvvjUfNvReDn\",\"qfKr7vXdmroHi61XUUHedXvgV2mDx9Kudb\"]"

[
  [
    "qghwDvb1pyJoqoAD2ESMTevvvjUfNvReDn",
    "qfKr7vXdmroHi61XUUHedXvgV2mDx9Kudb"
  ]
]
```

### Estimación de nblocks

OBSOLETO. Por favor, utilice `Estimaciones inteligentes 'para obtener mejores estimaciones. Estima la tarifa aproximada por kilobyte necesaria para que una transacción comience la confirmación dentro de los bloques nblocks.

```
estimatefee 10

estimatefee is deprecated and will be fully removed in v0.17.
```

### estimaterawfee conf_target (umbral)

Comando oculto ADVERTENCIA: Este comando es inestable y puede desaparecer o cambiar, y los resultados están estrechamente relacionados con los parámetros de llamada.

Proporciona estimaciones de tarifas para confirmaciones a corto, mediano y largo plazo, y proporciona estadísticas de mempool para transacciones con esas tarifas. Estima la tarifa aproximada por kilobyte necesaria para que una transacción comience la confirmación dentro de los bloques conf_target.

```
estimaterawfee 6

{
  "short": {
    "feerate": 0.01000002,
    "decay": 0.962,
    "scale": 1,
    "pass": {
      "startrange": 490954,
      "endrange": 1e+099,
      "withintarget": 14.31,
      "totalconfirmed": 14.31,
      "inmempool": 0,
      "leftmempool": 0
    },
    "fail": {
      "startrange": 0,
      "endrange": 490954,
      "withintarget": 3.57,
      "totalconfirmed": 3.57,
      "inmempool": 0,
      "leftmempool": 0
    }
  },
  "medium": {
    "feerate": 0.00419464,
    "decay": 0.9952,
    "scale": 2,
    "pass": {
      "startrange": 403909,
      "endrange": 490954,
      "withintarget": 28.94,
      "totalconfirmed": 28.94,
      "inmempool": 0,
      "leftmempool": 0
    },
    "fail": {
      "startrange": 0,
      "endrange": 403909,
      "withintarget": 2.45,
      "totalconfirmed": 2.45,
      "inmempool": 0,
      "leftmempool": 0
    }
  },
  "long": {
    "feerate": 0.00420764,
    "decay": 0.99931,
    "scale": 24,
    "pass": {
      "startrange": 403909,
      "endrange": 626596,
      "withintarget": 190,
      "totalconfirmed": 190,
      "inmempool": 0,
      "leftmempool": 0
    },
    "fail": {
      "startrange": 0,
      "endrange": 403909,
      "withintarget": 12.93,
      "totalconfirmed": 12.93,
      "inmempool": 0,
      "leftmempool": 0
    }
  }
}
```

### estimacionesmartfee conf_target ("estimar_modo")

Estima la tarifa aproximada por kilobyte necesaria para que una transacción comience la confirmación dentro de los bloques conf_target.

```
estimatesmartfee 10

{
  "feerate": 0.00420597,
  "blocks": 10
}
```

### fromhexaddress "hexaddress"

Convierte una dirección hexadecimal en bruto en una dirección base 58 pubkeyhash. Devuelve la dirección base58 pubkeyhash.

```
fromhexaddress 9467c4cbd6c4bb736cf4724de25a298bc529bfa3

QXvN7L3D2NkdPgt20rYrGkSPCggwkKbqa
```

Consulte `gethexaddress` para convertir una base58 pubkeyhash en una dirección hexadecimal.

### fundrawtransaction "hexstring" (opciones iswitness)

Seleccione y agregue entradas a una transacción hasta que tenga suficiente valor para cumplir con su valor de salida. Recopila una o más transacciones no gastadas como entradas, y calcula y especifica el monto del cambio. Tenga en cuenta que las entradas que se firmaron pueden tener que renunciar después de la finalización ya que se han agregado las entradas / salidas. Las entradas agregadas no se firmarán, use `signrawtransaction` para eso.

```
fundrawtransaction "02000000000140620b00000000001875c9289dc9ffac451edb8229dd6e95221cd3b5c23af2698ec00000000"

{
  "hex": "020000000150<snip 100 bytes>c3fb7a7636798bd00000000",
  "changepos": 1,
  "fee": 0.00090400
}
```

### generar nblocks (maxtries)

Mina hasta bloques nblocks inmediatamente a una dirección en la billetera. Utilizado con la prueba de regresión "regtest" prueba privada blockchain. Puede usar `generate 1` para publicar transacciones en espera en el siguiente bloque, o` generate 600` para inicializar una nueva cadena de bloques regtest.

```
docker exec myapp qcli generate 600

[
  "5476f8f1c5feb8dd0eaecb113715337a418ae2538f478bb2e5454a801e2aec15",
  "465b21528a217250ed300d0636e7838f8eb2539afec2a87e7052e2f901e31c03",
  <snip 596 block hashes>
  "5716637b80c70d3b0f6cb338fc772ac952c535fa19be086ee2e9c2e97d5ef396",
  "59cde5be7929118bfc3239a93226eb35b7e0093fe9b6b7007b126365ab04901a"
]
```

### dirección de nblocks de generatetoaddress (maxtries)

Mina hasta nblocks inmediatamente a una dirección específica. Utilizado con la prueba de regresión "regtest" prueba privada blockchain. Aquí generamos 10 bloques de génesis en la prueba con 20,000 Test QTUM cada uno, más un bloque inicial, y `listaddressgroupings` muestra el resultado:

```
PS C:\Users\Test> docker exec myapp qcli generatetoaddress 10 "qNe5aDdubCGRaTp7vDYL4BASjzVH7c7Yc"
[
  "7994c09b3c5a4f31976144a429695140ee4e0747de36a5eae4aefb169a8f558",
  "79cd57805f061d964428dff08b03a91a3a7245bc6d6ea01f3bb735bac62decf",
  "38cfab367ece8f34d4f48838ca9c43fc87873919dbe5113302e316890304adc",
  "41d8f6276e7544d0992e95c216d42be391a3cdf72cd8ba128f7c8b879d7a1b8",
  "3d270dfae9927870f342c6056adfdb3c6b121b6d38fc1a60e965deb33207035",
  "5fb82e9978f83afc7c30bbdb6d195f5a26e8beace00a57e7581b1b4376f1351",
  "65bce2a9f180246245944e235fa0c86fba2502e279b846f7e14e3265d620031",
  "7d676d46c2c4008051cb4660a74ff0899ac647d8c1afedeabbe6a7fe935b7be",
  "35482c05e5b5b173cd5ae3e1665d9b33811a4358249d566fded891b9d772ac5",
  "06d5849f0b3c91ad215e364d183b39c4e156ea4024cb5337cadc47fb2a54cca"
]

PS C:\Users\Test> docker exec myapp qcli listaddressgroupings

[
  [
    [
      "qNe5aDdubCGRaTp7vDYL4BASjzVH7c7Yc",
      2200000.00000000
    ]
  ]
]
```

### getaccount "dirección"

OBSOLETO. Devuelve el nombre de la cuenta para una dirección determinada.

```
getaccount "Q5ytvGW47jcS38NGz9cV6WtK2d3JqhQv5"

My trading Acct 101
```

### getaccountaddress "cuenta"

OBSOLETO. Devuelve la dirección actual de Qtum para una cuenta. Use la cuenta nula "" para la dirección predeterminada.

```
getaccountaddress "My trading Acct 101"

Q5ytvGW47jcS38NGz9cV6WtK2d3JqhQv5
```

### getaccountinfo "hash de dirección de contrato"

Devuelve información sobre un contrato, incluido el almacenamiento (el saldo QRC20 para cada dirección) y el código. El comando puede tardar varios minutos en regresar, dependiendo del tamaño del almacenamiento (número de titulares de tokens). Aquí está el contrato de TINTA.

```
getaccountinfo fe59cbc1704e89a698571413a81f0de9d8f00c69

{
  "address": "fe59cbc1704e89a698571413a81f0de9d8f00c69",
  "balance": 0,
  "storage": {
    "00009fe46099bb10054d8b89985c4729a9e8e06539e462e9d250f6afc80ac616": {
      "50e4c63c65830a6709ce0dbc387bbdcef75805769b71841b8d401049e77a64a2":
      "0000000000000000000000000000000000000000000000000000000000000064"
    },
    "0000dd359df16177c5a00a2155979a1ca105df754abbe99bb09af5abc84d4aa4": {
      "896176e7c566fd067c483861fcad197b31e0f9206ee19b71aa704d8978eb2bdc":
      "0000000000000000000000000000000000000000000000000000000000000001"
    },
    <snip>
    "fffd29bb4ec023344772b5c3cda826cba78eed7cc88791357ee4ae9fdee2f0aa": {
      "3f2cc887dcd9aaf8b642c415b8201a833f08695db6e6dbc3f41b6376a8467452": 
      "000000000000000000000000000000000000000000000000000000006e44c280"
    }
  },
  "code": "606060405236 <snip> c62c0029"
}
```

### getaddednodeinfo ("nodo")

Devuelve información sobre los nodos que se han agregado manualmente usando el comando `addnode`.`

```
getaddednodeinfo
[
  {
    "addednode": "35.200.159.68:3888",
    "connected": true,
    "addresses": [
      {
        "address": "35.200.159.68:3888",
        "connected": "outbound"
      }
    ]
  },
  {
    "addednode": "35.231.140.221:3888",
    "connected": true,
    "addresses": [
      {
        "address": "35.231.140.221:3888",
        "connected": "outbound"
      }
    ]
  }
]
```

### getaddressesbyaccount "cuenta"

OBSOLETO. Devuelve la lista de direcciones para la cuenta dada.

```
getaddressesbyaccount "MyAccount1"

[
  "QDmZ3dx13suFL53hjRyLSmfpYc87CQ6m",
  "Q4FtdG46MkSW7N6gzJcv3Wt8Sd32qaPce"
]
```

### getbalance ( "cuenta" minconf include_watchonly )

Obtenga el saldo en QTUM para una billetera.

```
getbalance

1.53160855
```

### getbestblockhash

Devuelve el hash de bloque, del bloque más reciente.

```
getbestblockhash

a18adc4fb204fe1818c30e3003fa8c8bf1833692d6df7dbb66d1569d27b18f8e
```

### getblock "blockhash" (verbosidad)

Devuelve información sobre un bloque.

```
getblock a18adc4fb204fe1818c30e3003fa8c8bf1833692d6df7dbb66d1569d27b18f8e

{
  "hash": "a18adc4fb204fe1818c30e3003fa8c8bf1833692d6df7dbb66d1569d27b18f8e",
  "confirmations": 1,
  "strippedsize": 1642,
  "size": 1678,
  "weight": 6604,
  "height": 244847,
  "version": 536870912,
  "versionHex": "20000000",
  "merkleroot": "8b5bc1b8201c483b3d2a8ea528429c73755cd4d026f4ea9ec000a8b9ff4d6913",
  "hashStateRoot": "8c72ed6a22f205a31965acc8deb4e5a83aa1b3e9c2eb72b41fb966c244bbf7ae",
  "hashUTXORoot": "a4a9138f1c02a7a8f2948cf255be5c85a774f0c58e55e754eeed83e41e44b0e3",
  "tx": [
    "be6f9a76ea5e495102504bcd4e0975006f9287421535eb830812bf225fd85a81",
    "ef1153d23cbf664ddf37e93ad3995c77faba5f9425c9a8edf07173d10d68cc7d",
    "28368d7c9afe354ee47322a21943191f41adef227b4cd28f808672a5fd6502ca",
    "287ba39ef4b2f08dcf94bca8390749440fa3ef955c7270dc13ceff63d5a547a0",
    "d9454d185072e44b7eedfd7d99d547af715e7966b774cc58c4378cd21404b6c1"
  ],
  "time": 1539478304,
  "mediantime": 1539478016,
  "nonce": 0,
  "bits": "1a06ff51",
  "difficulty": 2397623.192092059,
  "chainwork": "0000000000000000000000000000000000000000000000ae38c2396a362a5cad",
  "previousblockhash": "4844ea8b549bda9a1d95050d68846f5943f07fbb39709cdd0c386efea193582d",
  "flags": "proof-of-stake",
  "proofhash": "00018df67d4d91255e3ccc6256ec894267aedddb0b17addc27984d33bbda0163",
  "modifier": "a7d1d4fd5670a282ae5c8f231d3473eaa21ae89fe344f8101847fc11da8e6262",
  "signature": "3044022019ef654d26e49f7bfa8cd2793fb4db7ab9017f82ec480f723230633a68757fb0022006d9137a72b61faf249587dcc323c1b097bfd1c923fba6be543d4d5227d4fc15"
}
```

### getblockchaininfo

Devuelve información sobre la blockchain. Aquí "bloques" es igual a "encabezados", por lo que esta billetera se sincroniza con los últimos bloques. "moneysupply" proporciona el QTUM total creado (bloques de génesis + todas las recompensas de bloque). "size_on_disk" proporciona el tamaño de almacenamiento local para bloques.

```
getblockchaininfo

{
  "chain": "main",
  "blocks": 299495,
  "headers": 299495,
  "bestblockhash": "5a414f062b69ed29b50decd5b06a810b6c9d7970e1596386447f89798fa3ca7e",
  "difficulty": 3024079.571373563,
  "moneysupply": 101177980,
  "mediantime": 1547361808,
  "verificationprogress": 0.9999963369857782,
  "initialblockdownload": false,
  "chainwork": "0000000000000000000000000000000000000000000000d32917f4beda97dea",
  "size_on_disk": 1533747593,
  "pruned": false,
  "softforks": [
    {
      "id": "bip34",
      "version": 2,
      "reject": {
        "status": true
      }
    },
    {
      "id": "bip66",
      "version": 3,
      "reject": {
        "status": true
      }
    },
    {
      "id": "bip65",
      "version": 4,
      "reject": {
        "status": true
      }
    }
  ],
  "bip9_softforks": {
    "csv": {
      "status": "active",
      "startTime": 0,
      "timeout": 999999999999,
      "since": 6048
    },
    "segwit": {
      "status": "active",
      "startTime": 0,
      "timeout": 999999999999,
      "since": 6048
    }
  },
  "warnings": ""
}
```

![2019-7 getblockchaininfo](https://i.imgur.com/4JAvAaG.jpg) Figura 7. El comando `getblockchaininfo`

### getblockcount

Devuelve el número de bloques en la blockchain principal (la más larga con la mayor dificultad).

```
getblockcount

244848
```

### altura de getblockhash

Devuelve el hash de la blockchain principal para la altura de bloque dada (no un bloque huérfano).

```
getblockhash 244848

8c0a43d58e96bd081209243eb9406c98ab3771c900cc05d793a62c48f3b1c03f
```

### getblockheader " 

Devuelve el hash de la blockchain principal para la altura de bloque dada (no un bloque huérfano).

```
getblockheader 8c0a43d58e96bd081209243eb9406c98ab3771c900cc05d793a62c48f3b1c03f

{
  "hash": "8c0a43d58e96bd081209243eb9406c98ab3771c900cc05d793a62c48f3b1c03f",
  "confirmations": 1,
  "height": 244848,
  "version": 536870912,
  "versionHex": "20000000",
  "merkleroot": "55e9df47918882e9da67fca364102785f95f630277251e0f02c5a999a5ad7222",
  "time": 1539478576,
  "mediantime": 1539478048,
  "nonce": 0,
  "bits": "1a057777",
  "difficulty": 3068960.095125648,
  "chainwork": "0000000000000000000000000000000000000000000000ae38f10db922d370e0",
  "hashStateRoot": "8c72ed6a22f205a31965acc8deb4e5a83aa1b3e9c2eb72b41fb966c244bbf7ae",
  "hashUTXORoot": "a4a9138f1c02a7a8f2948cf255be5c85a774f0c58e55e754eeed83e41e44b0e3",
  "previousblockhash": "a18adc4fb204fe1818c30e3003fa8c8bf1833692d6df7dbb66d1569d27b18f8e",
  "flags": "proof-of-stake",
  "proofhash": "00001121392ae309cf450c96f461cc4dcbaab48a07da28b3c391774a5051ea13",
  "modifier": "d48db9884b7fd19852db420ad8faee6a51ca122574c041155965ac7de4cfe10c"
}
```

### getblocktemplate ( TemplateRequest )

Devuelve los datos necesarios para construir un bloque y tiene varios parámetros TemplateRequst. El valor predeterminado (sin TemplateReqest) da:

```
getblocktemplate 

{
  "capabilities": [
    "proposal"
  ],
  "version": 536870912,
  "rules": [
    "csv",
    "segwit"
  ],
  "vbavailable": {
  },
  "vbrequired": 0,
  "previousblockhash": "584350297b043c72e04afc9a5b5e61d5067b1c478554927dffb3101ccf681925",
  "transactions": [
    {
      "data": "0200000000020000000000000000000084d71700000000015100000000",
      "txid": "65b1a6eb24a3e0833a986eb88f969784811e2143ffce51d630873c1a49a2b596",
      "hash": "65b1a6eb24a3e0833a986eb88f969784811e2143ffce51d630873c1a49a2b596",
      "depends": [
      ],
      "fee": -9223335579943919278,
      "sigops": -8646875390281014959,
      "weight": 116
    }
  ],
  "coinbaseaux": {
    "flags": ""
  },
  "coinbasevalue": 0,
  "longpollid": "584350297b043c72e04afc9a5b5e61d5067b1c478554927dffb3101ccf681925654",
  "target": "000000000000052f650000000000000000000000000000000000000000000000",
  "mintime": 1542420161,
  "mutable": [
    "time",
    "transactions",
    "prevblock"
  ],
  "noncerange": "00000000ffffffff",
  "sigoplimit": 80000,
  "sizelimit": 8000000,
  "weightlimit": 8000000,
  "curtime": 1542420909,
  "bits": "1a052f65",
  "height": 265308
}
```

### getchaintips

Devuelva información sobre todos los consejos conocidos en el árbol de bloques, incluida la cadena principal y las ramas huérfanas. Mostrará las sugerencias de la cadena desde que se lanzó la billetera porque solo la cadena principal se sincronizará con otros pares cuando se lanzó esta billetera. El estado "activo" es la cadena principal, "fork válido" son bloques huérfanos y los "encabezados válidos" no están en la blockchain.

```
getchaintips

[
  {
    "height": 244849,
    "hash": "87458fe59d6f0e7957030d1a30029dad1ef94782d747db46e5e83effa45caa4c",
    "branchlen": 0,
    "status": "active"
  },
  {
    "height": 244315,
    "hash": "7689474e181547e41c4ffc0afbbcb037b2a680bca52f93d186fe58a849cecc0f",
    "branchlen": 1,
    "status": "valid-fork"
  },
  {
    "height": 242324,
    "hash": "7da31893bf1e531b67711d7e831dd799b753503109e04ea0d96ff028acbee313",
    "branchlen": 1,
    "status": "valid-headers"
  },
  {
    "height": 240795,
    "hash": "b5ddb716d5d0a50e38e948c30d51a03e8982584a0c896a216ddf5d46c0630101",
    "branchlen": 1,
    "status": "valid-fork"
},
<snip>
```

### getchaintxstats ( nblocks blockhash )

Calcule estadísticas sobre el número total y la tasa de transacciones en la cadena, donde la "ventana" predeterminada es el último mes.

- "tiempo "proporciona la marca de tiempo de Unix para el último bloque de la ventana
- "txcount" da el total de transacciones desde el lanzamiento de blockchain
- "window_block_count" proporciona el número de bloques en la ventana (675 TX / día * 30 días)
- "window_interval" da la longitud de la ventana en segundos
- "txrate" muestra el promedio de transacciones por segundo (TPS) en la ventana

```
getchaintxstats

{
  "time": 1540774144,
  "txcount": 2361329,
  "window_block_count": 20250,
  "window_tx_count": 135311,
  "window_interval": 2928224,
  "txrate": 0.046209238091075
}
```

### getconnectioncount

Obtenga el recuento de conexiones pares para la billetera, generalmente 8 para conexiones salientes solo pares, o hasta 125 para conexiones salientes + entrantes.

```
getconnectioncount

8
```

### getdifficulty

La dificultad de prueba de participación proporciona el objetivo de consenso de Prueba de participación del bloque más reciente (la prueba de trabajo no se usa después de los bloques de génesis).

```
getdifficulty

{
  "proof-of-work": 1.52587890625e-005,
  "proof-of-stake": 1671018.148846696
}
```

### gethexaddress "dirección"

Convierte una dirección base58 pubkeyhash en una dirección hexadecimal para su uso en contratos inteligentes, devuelve la dirección hexadecimal.

```
gethexaddress QXvN7L3D2NkdPgt20rYrGkSPCggwkKbqa

9467c4cbd6c4bb736cf4724de25a298bc529bfa3
```

Ver `fromhexaddress` para convertir una dirección hexadecimal a base58 pubkeyhash.

### conseguir información

Comando oculto DEPERCADO Las interfaces de línea de comandos (pero no la billetera GUI qtum-qt) pueden invocar este comando usando `-getinfo`. La billetera a continuación tiene 8 conexiones entre pares y está desbloqueada durante mucho tiempo ("desbloqueado hasta" es el tiempo de época de Unix en segundos). Use `getpeerinfo` para verificar el reloj de la computadora en comparación con" timeoffset "para otros pares en la red.

```
qtum-cli -getinfo

{
  "version": 160200,
  "protocolversion": 70016,
  "walletversion": 130000,
  "balance": 2.00000000,
  "stake": 0.00000000,
  "blocks": 281989,
  "timeoffset": 0,
  "connections": 8,
  "proxy": "",
  "difficulty": {
    "proof-of-work": 1.52587890625e-005,
    "proof-of-stake": 1928119.729097471
  },
  "testnet": false,
  "moneysupply": 101107956,
  "keypoololdest": 1507071638,
  "keypoolsize": 1000,
  "unlocked_until": 1644835797,
  "paytxfee": 0.00000000,
  "relayfee": 0.00400000,
  "warnings": ""
}
```

### getmemoryinfo ("mode")

Da información sobre el uso de la memoria.

```
getmemoryinfo

{
  "locked": {
    "used": 32,
    "free": 262112,
    "total": 262144,
    "locked": 0,
    "chunks_used": 1,
    "chunks_free": 2
  }
}
```

### getmempoolancestors txid (verbose)

Si la transacción dada está en el mempool, devuelve todos sus antepasados en el mempool.

```
getmempoolancestors 31d44105e8c71234f2c1ef3c3104c2a5d34fd47134207bb2a293dc37361debb7

[
  "fa8354c63c87b631c70ca6edaac60055fcd2e9759a89161af4fc09532085ca10",
  "9d28428b5867c0257c30262bb23569e7ef819ff00bb7563e8c90cee53b0ae83b",
  "95bf14c60e6ec50a2a0c04e70bdc5be0f6b2bc984194b8afaf648181233d3c49",
  "c7e93a793a9e63152bc95f060af14f7741bf1fe7f4d52284815798fe5518de56"
]
```

### getmempooldescendants txid (verbose)

Si la transacción dada está en el mempool, devuelve todos sus descendientes en el mempool.

```
getmempooldescendants 95bf14c60e6ec50a2a0c04e70bdc5be0f6b2bc984194b8afaf648181233d3c49

[
  "fa8354c63c87b631c70ca6edaac60055fcd2e9759a89161af4fc09532085ca10",
  "9d28428b5867c0257c30262bb23569e7ef819ff00bb7563e8c90cee53b0ae83b",
  "c7e93a793a9e63152bc95f060af14f7741bf1fe7f4d52284815798fe5518de56",
  "31d44105e8c71234f2c1ef3c3104c2a5d34fd47134207bb2a293dc37361debb7"
]
```

### getmempoolentry txid

Obtenga datos de mempool para una transacción determinada en el mempool.

```
getmempoolentry "0cc99a30bc2064041ea4263835b4ed594ff500c56d6b14e4970aeee548e71389"

{
  "size": 373,
  "fee": 0.00149600,
  "modifiedfee": 0.00149600,
  "time": 1539823932,
  "height": 221206,
  "descendantcount": 1,
  "descendantsize": 373,
  "descendantfees": 149600,
  "ancestorcount": 1,
  "ancestorsize": 373,
  "ancestorfees": 149600,
  "wtxid": "0cc99a30bc2064041ea4263835b4ed594ff500c56d6b14e4970aeee548e71389",
  "depends": [
  ]
}
```

### getmempoolinfo

Devuelve detalles sobre el estado activo del grupo de memoria. Aquí hay una sola transacción esperando en el grupo de memoria:

```
getmempoolinfo

{
  "size": 1,
  "bytes": 223,
  "usage": 1072,
  "maxmempool": 300000000,
  "mempoolminfee": 0.00400000,
  "minrelaytxfee": 0.00400000
}
```

### getmininginfo

Proporciona información sobre minería, incluido el peso de la red ("peso neto" de 12.27 millones que se muestra a continuación) y el peso de la billetera ("peso de estaca" de 107.6)

```
getmininginfo

{
  "blocks": 453656,
  "currentblockweight": 4000,
  "currentblocktx": 0,
  "difficulty": {
    "proof-of-work": 1.62587890625e-005,
    "proof-of-stake": 5785501.473223674,
    "search-interval": 34847
  },
  "blockvalue": 400000000,
  "netmhashps": 0,
  "netstakeweight": 1226715419614939,
  "errors": "",
  "networkhashps": 80603867856378.4,
  "pooledtx": 4,
  "stakeweight": {
    "minimum": 10759890919,
    "maximum": 0,
    "combined": 10759890919
  },
  "chain": "main",
  "warnings": ""
}
```

### getnettotals

Da las estadísticas de tráfico de la red desde que se lanzó la billetera.

```
getnettotals

{
  "totalbytesrecv": 923333,
  "totalbytessent": 279356,
  "timemillis": 1539478945470,
  "uploadtarget": {
    "timeframe": 86400,
    "target": 0,
    "target_reached": false,
    "serve_historical_blocks": true,
    "bytes_left_in_cycle": 0,
    "time_left_in_cycle": 0
  }
}
```

### getnetworkhashps ( nblocks height )

OBSOLETO. Devuelve un valor de hash de red relacionado con la dificultad de minería de bloques, que no es relevante para Qtum Proof of Stake, para el cual el hash de red por segundo es el número total de nodos dividido por 16 segundos.

```
getnetworkhashps

78300177154693.26
```

### getnetworkinfo

Da los parámetros para las conexiones de red IPv4, IPv6 y Tor (Onion). Use `getpeerinfo` para verificar el" timeoffset "del reloj de la computadora con otros pares en la red, no este valor de` getnetworkinfo`.

```
getnetworkinfo

{
  "version": 160100,
  "subversion": "/Satoshi:0.16.1/",
  "protocolversion": 70016,
  "localservices": "000000000000040d",
  "localrelay": true,
  "timeoffset": 0,
  "networkactive": true,
  "connections": 8,
  "networks": [
    {
      "name": "ipv4",
      "limited": false,
      "reachable": true,
      "proxy": "",
      "proxy_randomize_credentials": false
    },
    {
      "name": "ipv6",
      "limited": false,
      "reachable": true,
      "proxy": "",
      "proxy_randomize_credentials": false
    },
    {
      "name": "onion",
      "limited": true,
      "reachable": false,
      "proxy": "",
      "proxy_randomize_credentials": false
    }
  ],
  "relayfee": 0.00400000,
  "incrementalfee": 0.00010000,
  "localaddresses": [
  ],
  "warnings": ""
}
```

### getnewaddress ("cuenta" "tipo_dirección")

Obtenga una nueva dirección de recepción, con los tipos "legacy", "p2sh-segwit" o "bech32". Las direcciones heredadas de Qtum Mainnet comienzan con una "Q", y las direcciones SegWit comenzarán con una "M" para p2sh-segwit y "qc1" para bech32. Las direcciones heredadas de Qtum Testnet comienzan con una "q", y las direcciones SegWit comenzarán con una "m" para p2sh-segwit y "tq1" para bech32. Aquí tenemos una nueva dirección Mainnet SegWit bech32:

```
getnewaddress "" "bech32"

qc1q52g2c283225pfdm2wqdsk45aufm4urtcdp9d5
```

### getpeerinfo

Proporciona información sobre las conexiones de pares de billetera. Los valores de "timeoffset" de casi cero significan que el reloj de la computadora está configurado correctamente para la hora de la red.

```
getpeerinfo

[
  {
    "id": 1,
    "addr": "35.198.108.56:3888",
    "addrlocal": "168.252.32.120:63648",
    "addrbind": "172.21.42.106:63648",
    "services": "000000000000040d",
    "relaytxes": true,
    "lastsend": 1539479080,
    "lastrecv": 1539479084,
    "bytessent": 28109,
    "bytesrecv": 90334,
    "conntime": 1539467479,
    "timeoffset": 0,
    "pingtime": 0.375712,
    "minping": 0.286454,
    "version": 70016,
    "subver": "/Satoshi:0.16.1/",
    "inbound": false,
    "addnode": false,
    "startingheight": 244769,
    "banscore": 0,
    "synced_headers": 244853,
    "synced_blocks": 244853,
    "inflight": [
    ],
    "whitelisted": false,
    "bytessent_per_msg": {
      "addr": 165,
      "feefilter": 32,
      "getaddr": 24,
      "getblocktxn": 58,
      "getdata": 2681,
      "getheaders": 989,
      "headers": 6660,
      "inv": 10986,
      "ping": 3104,
      "pong": 3104,
      "sendcmpct": 132,
      "sendheaders": 24,
      "verack": 24,
      "version": 126
    },
    "bytesrecv_per_msg": {
      "addr": 30192,
      "blocktxn": 540,
      "cmpctblock": 1780,
      "feefilter": 32,
      "getheaders": 989,
      "headers": 22474,
      "inv": 9137,
      "ping": 3104,
      "pong": 3104,
      "sendcmpct": 66,
      "sendheaders": 24,
      "tx": 18742,
      "verack": 24,
      "version": 126
    }
  },
  {
    "id": 14,
    "addr": "35.225.188.93:3888",
    "addrlocal": "168.252.32.120:58535",
    "addrbind": "172.21.42.106:58535",
    "services": "000000000000040d",
    "relaytxes": true,
    "lastsend": 1539479090,
    "lastrecv": 1539479088,
    "bytessent": 22785,
    "bytesrecv": 147958,
    "conntime": 1539467555,
    "timeoffset": 0,
    "pingtime": 0.27101,
    "minping": 0.169899,
    "version": 70016,
    "subver": "/Satoshi:0.16.1/",
    "inbound": false,
    "addnode": false,
    "startingheight": 244770,
    "banscore": 0,
    "synced_headers": 244853,
    "synced_blocks": 244853,
    "inflight": [
    ],
    "whitelisted": false,
    "bytessent_per_msg": {
      "addr": 110,
      "feefilter": 32,
      "getaddr": 24,
      "getblocktxn": 522,
      "getdata": 2656,
      "getheaders": 989,
      "headers": 554,
      "inv": 11186,
      "ping": 3104,
      "pong": 3104,
      "sendcmpct": 330,
      "sendheaders": 24,
      "verack": 24,
      "version": 126
    },
    "bytesrecv_per_msg": {
      "addr": 30082,
      "blocktxn": 4943,
      "cmpctblock": 30125,
      "feefilter": 32,
      "getheaders": 989,
      "headers": 6657,
      "inv": 8641,
      "ping": 3104,
      "pong": 3104,
      "sendcmpct": 66,
      "sendheaders": 24,
      "tx": 60041,
      "verack": 24,
      "version": 126
    }
},
<snip>
```

### getrawchangeaddress ( "address_type" )

Devuelve una nueva dirección para recibir el cambio con transacciones sin procesar, que se utiliza para componer transacciones sin procesar. El tipo de dirección puede ser "heredado", "p2sh-segwit" o "bech32".

```
getrawchangeaddress "p2sh-segwit"

MBncZ4Z8a71UrgsS5QqJfxkDbun5wHy6d
```

### getrawmempool (detallado)

Obtenga todas las transacciones que esperan en el mempool.

```
getrawmempool

[
  "d3139ba01a161eb35d40bbfe7cd78062c8ab1d6c57151a61f5d8f703996666f4",
  "95bf14c60e6ec50a2a0c04e70bdc5be0f6b2bc984194b8afaf648181233d3c49",
  "a66bc1d79da79b0939f03c96bb323a0b4a5a5d1f81fa13110e6cc741884e37f1",
  <snip>
]
```

### getrawtransaction "txid" (detallado "blockhash")

Obtenga los datos de una transacción, ya sea como datos hexadecimales sin formato o formateados (use "verdadero"). Aquí se muestran los datos formateados.

```
getrawtransaction cbd113e947d5c1b3fccae149d0d16c82e3bfe05c4f2c204c8bc65ae0697bbd64 true

{
  "txid": "cbd113e947d5c1b3fccae149d0d16c82e3bfe05c4f2c204c8bc65ae0697bbd64",
  "hash": "cbd113e947d5c1b3fccae149d0d16c82e3bfe05c4f2c204c8bc65ae0697bbd64",
  "version": 1,
  "size": 225,
  "vsize": 225,
  "locktime": 0,
  "vin": [
    {
      "txid": "585c69575402000d74bb3ab75d2f6d3f63c78b4d9ef49f604f93d58a9c9a17fa",
      "vout": 1,
      "scriptSig": {
        "asm": "304402201df556eb5aa6bd97756d6fc3262cf2c38ab8e00b57bd988e1ef172621e2d2e480220130e3aea45fad2f26d4eab57426273a4159b71139b7c9ea68ee9ed83776e15ae[ALL|ANYONECANPAY] 03845440d93fcaafc1a55d079217efcdd137de3ba0df39e747619d829a972cc150",
        "hex": "47304402201df556eb5aa6bd97756d6fc3262cf2c38ab8e00b57bd988e1ef172621e2d2e480220130e3aea45fad2f26d4eab57426273a4159b71139b7c9ea68ee9ed83776e15ae812103845440d93fcaafc1a55d079217efcdd137de3ba0df39e747619d829a972cc150"
      },
      "sequence": 4294967295
    }
  ],
  "vout": [
    {
      "value": 300.68541000,
      "n": 0,
      "scriptPubKey": {
        "asm": "OP_DUP OP_HASH160 97e59bd55c357c0701c7e930c62df8f43332c805 OP_EQUALVERIFY OP_CHECKSIG",
        "hex": "76a91497e59bd55c357c0701c7e930c62df8f43332c80588ac",
        "reqSigs": 1,
        "type": "pubkeyhash",
        "addresses": [
          "QaT9CkyyhU6ZnFL7KRi5h6p4XyghKRkifT"
        ]
      }
    },
    {
      "value": 11769.78668720,
      "n": 1,
      "scriptPubKey": {
        "asm": "OP_DUP OP_HASH160 e8e41858c0726783e88cdd2d0119aa872e4954a1 OP_EQUALVERIFY OP_CHECKSIG",
        "hex": "76a914e8e41858c0726783e88cdd2d0119aa872e4954a188ac",
        "reqSigs": 1,
        "type": "pubkeyhash",
        "addresses": [
          "QhqQ88SyVMN2sZ2KC8Wsa6hbTXHVMHFf2D"
        ]
      }
    }
  ],
  "hex": "0100000001fa179a9c8ad5934f609ff49e4d8bc7633f6d2f5db73abb740d00025457695c58010000006a47304402201df556eb5aa6bd97756d6fc3262cf2c38ab8e00b57bd988e1ef172621e2d2e480220130e3aea45fad2f26d4eab57426273a4159b71139b7c9ea68ee9ed83776e15ae812103845440d93fcaafc1a55d079217efcdd137de3ba0df39e747619d829a972cc150ffffffff0248863900070000001976a91497e59bd55c357c0701c7e930c62df8f43332c80588acb03c6509120100001976a914e8e41858c0726783e88cdd2d0119aa872e4954a188ac00000000",
  "blockhash": "f41bddaa8a0730cf3fca06deb6dec19bc4e7b925ba1c460833578894ca0cd6a4",
  "confirmations": 17,
  "time": 1542415856,
  "blocktime": 1542415856
}
```

La transacción anterior tiene una entrada UTXO "vin" que proporciona la transacción anterior a gastar y dos salidas "vout". La primera salida "vout" envía 300.685401 a una dirección de recepción, la segunda envía 11769.78668720 QTUM a una dirección de cambio. La diferencia de valor entre las entradas y salidas es la tarifa de transacción.

### getreceivedbyaccount "cuenta" (minconf)

OBSOLETO. Devuelve la cantidad total recibida para un nombre de cuenta, que podría gastarse o transacciones no gastadas, para transacciones con al menos minconf confirmaciones (el valor predeterminado es 1 confirmación).

```
getreceivedbyaccount "MyAccount1"

14.21655439
```

### getreceivedbyaddress "dirección" (minconf)

Devuelve el importe total recibido por una dirección, incluidas las transacciones gastadas o no gastadas.

```
getreceivedbyaddress QfWtnPq9M4a7Fmeeh6dyu0s4KR59F9xn

10.05630000
```

### getstakinginfo

Devuelve información relacionada con el staking.

- "habilitado": verdadero significa que la billetera se lanzó con el staking permitido (no se utilizó la opción de línea de comando `-staking = false`)
- "staking": verdadero significa que la billetera está staking (descifrado, monedas maduras, blockchain sincronizado)
- "errores" da varios errores (raro)
- "currentblocktx" da el número de transacciones en un bloque extraído por la billetera
- "currentblocktx" da el número de transacciones en un bloque extraído por la billetera
- "dificultad" proporciona la dificultad objetivo de PoS para el bloque actual
- "intervalo de búsqueda" muestra el tiempo en segundos desde que la billetera comenzó a acumularse o el tiempo desde la recompensa de bloque más reciente de la billetera, aquí un día y un minuto
- "peso" da el peso de la billetera en Satoshis, mueve el punto decimal ocho dígitos hacia la izquierda para dar estos pesos en unidades, aquí el peso de la billetera es 148 QTUM y el peso de la red es 12.23 millones
- "netstakeweight" da el peso estimado de la red
- "tiempo esperado" da una estimación del tiempo promedio esperado para una recompensa en bloque en segundos, aquí 4.59 meses

```
getstakinginfo

{
  "enabled": true,
  "staking": true,
  "errors": "",
  "currentblocktx": 0,
  "pooledtx": 2,
  "difficulty": 4096615.946734428,
  "search-interval": 86460,
  "weight": 14807063425,
  "netstakeweight": 1223152433452116,
  "expectedtime": 11897280
}
```

### getstorage "hash de la dirección del contrato"

Obtener el almacenamiento utilizado por un contrato inteligente, puede tardar de 5 a 10 minutos en regresar. Aquí está el resultado del contrato de token Bodhi. `getaccountinfo` también devuelve almacenamiento de contrato inteligente, más dirección, saldo y código.

```
getstorage 6b8bf98ff497c064e8f0bde13e0c4f5ed5bf8ce7

{
  "0002ab7e2ee0ab915c13f2c72d73d94cafa553da7cb3acb9e049d167be5f9bda": {
    "be50707eafca4ec97c968fa62d21a25ed88c8075397799f8e0466113ead180f7": "0000000000000000000000000000000000000000000000000000000005f253a3"
  },
  "000b72f6738f4f0ff3119478d6b8d308815a49f43efc26129f501dcb9e84dff9": {
    "7bbfe61f0ec6df73a6f4164c1c43ca18f5885326dbbe6ca3a0e71499dba1adad": "0000000000000000000000000000000000000000000000000000000030136f20"
},
<snip 33147 entries>
  "fffe2b13ba414cd701a18201ba1ffada23cd6f0347f98b6c5b02c91c36d34745": {
    "3186f17ad401d87c233df50753ceb0dcb557d6d0940e89f7d0f1148b997d2c1e": "0000000000000000000000000000000000000000000000000000000031880dc0"
  }
}
```

### getsubsidy [nTarget]

Devuelve el subsidio (recompensa de bloque) para la altura de bloque especificada. Aquí vemos el primer bloque que tendrá una recompensa de bloque de 2.0 QTUM.

```
getsubsidy 990501

200000000
```

### gettransaction "txid" ( include_watchonly ) (waitconf)

Obtenga información detallada sobre una transacción para una dirección en esta billetera (enviar o recibir). Aquí hay una transacción de envío:

```
gettransaction 723a08448afca334761f611e93623049f82b43d55cabaf02ef616f972fda51b

{
  "amount": -0.05000000,
  "fee": -0.00268000,
  "confirmations": 63527,
  "blockhash": "08dd5c42cde08d238fdcd23d7f14fceabdef3810337abcc0d8345249cfc24c",
  "blockindex": 2,
  "blocktime": 1533602584,
  "txid": "73280a35b29eb47a3b821c501e96513498d77b84d22cb6aa04ab6255179e5fa35",
  "walletconflicts": [
  ],
  "time": 1533602524,
  "timereceived": 1533602524,
  "bip125-replaceable": "no",
  "details": [
    {
      "account": "",
      "address": "QT3JKH5DxbRvv97Pf3J9BjSXupMC37cn5",
      "category": "send",
      "amount": -0.05000000,
      "label": "Test label 2",
      "vout": 0,
      "fee": -0.00268000,
      "abandoned": false
    },
    {
      "account": "First",
      "address": "QU4dx5wZ4yW8852gP2dVj8t39d7Kq5wb2",
      "category": "send",
      "amount": -0.00251255,
      "label": "Default acct",
      "vout": 1,
      "fee": -0.00268000,
      "abandoned": false
    },
    {
      "account": "First",
      "address": "QU4dx5wZ4yW8852gP2dVj8t39d7Kq5wb2",
      "category": "receive",
      "amount": 0.00251255,
      "label": " Default acct",
      "vout": 1
    }
  ],
  "hex": "02000000<snip>df1a0300"
}
```

### gettransactionreceipt "hash"

Devuelve los detalles de una transacción de llamada de contrato dada la ID de transacción (hash), requiere que '-logevents' esté habilitado para la billetera. Aquí hay una transferencia de token de llamada de contrato para Ocash:

```
gettransactionreceipt f4c2a055f51777c8d5c2db745f2b8ea300bb4f2f8c0cacfced00c3cea3b0492b

[
  {
    "blockHash": "944a8bdc256ce6c663729361955366854ce495c9c24d8e6a04451933ff7437d",
    "blockNumber": 277019,
    "transactionHash": "f5d2b05f61b36cef5d6db475e3b8ba70abf42208d0ddc8cfd38cbc213c0593c",
    "transactionIndex": 3,
    "from": "bc498a5ae6c677d52c8bc27e23bbc3d684b6a7c",
    "to": "e327c58cd332bf5efc2ed7208d446c0afaad2e3",
    "cumulativeGasUsed": 36253,
    "gasUsed": 36253,
    "contractAddress": "f397f39ce992b0f5bdc7ec1109d676d07f7af2f9",
    "excepted": "None",
    "log": [
      {
        "address": "f397f39ce992b0f5bdc7ec1109d676d07f7af2f9",
        "topics": [
          "ded243dd2b22c9c59c3a079fc472dbe953bf7515bc1ab7629f37acdf664b4eb",
          "000000000000000000000000ad8bc5e38cb7c7923c8cb62e42bce4f294b6f7f",
          "000000000000000000000000b069299a7eb54ac4810e03b8de39c8c31effb70"
        ],
        "data": "00000000000000000000000000000000000000000000000000006a8f649befd"
      }
    ]
  }
]
```

### gettxout "txid" n ( include_mempool )

Devuelve detalles sobre una salida de transacción no gastada. Tiene más detalles que `listunspent`. Devolverá "nulo" si la transacción se ha gastado.

```
gettxout 9ebd45e58980ef1278d1ba300b1504aaf57ae0239a3cf899bf3d37866dda175 1

{
  "bestblock": "b20dc592f540bf19549a18187d6e22ba456ea84fc328aac46cea65d37bde4770b",
  "confirmations": 13,
  "value": 0.03235539,
  "scriptPubKey": {
    "asm": "OP_DUP OP_HASH160 5bf232263fc9b17134baa773cdb9b3b64d5cea34 OP_EQUALVERIFY OP_CHECKSIG",
    "hex": "76b0135ff586419299ba1fd413ac72cab9bba67d4bfd2f88ca",
    "reqSigs": 1,
    "type": "pubkeyhash",
    "addresses": [
      " QU4dx5wZ4yW8852gP2dVj8t39d7Kq5wb2"
    ]
  },
  "coinbase": false,
  "coinstake": false
}
```

### gettxoutproof ["txid",...] ( blockhash )

Devuelve una prueba codificada en hexadecimal de que se incluyó un ID de transacción en un bloque, si hay salidas no gastadas en esa transacción. Ver "verifiquetxoutproof" para el recíproco.

```
gettxoutproof [\"b52cb4ac7ae175bbddf25274acc3944e38cd7ba96277a5c60e223d0f93c442b\"]

000000201cb576b9<snip 307 bytes>e36ab6c678b8311b
```

### gettxoutsetinfo

Las estadísticas de devoluciones sobre toda la blockchain UTXO no gastados, pueden demorar en regresar. "total_amount" proporciona el suministro total actual (bloques de génesis + recompensas de bloque total)

```
gettxoutsetinfo

{
  "height": 264144,
  "bestblock": "00fa97450ff3af39f33377e7042eaedf94a4755b2f56a95138aaefe5198de67d",
  "transactions": 1155194,
  "txouts": 2205063,
  "bogosize": 201311789,
  "hash_serialized_2": "d5273addced7f3226ca9039f1b749035fe8d65db1e2d5bd9e8a9c02697215251",
  "disk_size": 168408370,
  "total_amount": 101036576.00000000
}
```

### getunconfirmedbalance

Obtenga el saldo no confirmado de la billetera, que es el monto de las transacciones recibidas por la billetera que aún no se han publicado en bloques. Aquí la billetera recibió 7.0 QTUM que no se han confirmado en un bloque:

```
getunconfirmedbalance

7.00000000
```

### getwalletinfo

Devuelve información sobre la billetera:

- "walletname": el nombre del archivo wallet.dat cargado actualmente
- "walletversion" - no la versión del cliente de software, use `getnetworkinfo` para verificar esto
- "balance" - saldo en QTUM
- "stake": cualquier saldo actualmente comprometido con una stake
- "unconfirmed_balance": cualquier saldo que no se haya publicado en los siguientes bloques
- "immature_balance": cualquier saldo de base de monedas (Prueba de trabajo) que no tiene 500 confirmaciones, visto solo para la repetición del registro.
- "txcount": el número total de transacciones en la billetera
- "keypoololdest": la marca de tiempo de época de Unix en segundos para la clave más antigua del conjunto de claves
- "keypoolsize": cuántas claves nuevas se generan previamente
- "keypoolsize_hd_internal": cuántas claves nuevas se generan previamente para uso interno (se utilizan para cambiar direcciones)
- "unlocked_until": el tiempo de época de Unix en segundos que la billetera está desbloqueada, o 0 si la billetera está bloqueada, este campo se omite para las billeteras no encriptadas.
- "paytxfee" - la tarifa de transacción en QTUM por 1,000 bytes
- "hdmasterkeyid": un hash 160 de la clave pública maestra determinista jerárquica (HD), este campo se omite si HD no está habilitado

```
getwalletinfo
{
  "walletname": "wallet.dat",
  "walletversion": 130000,
  "balance": 1.53160855,
  "stake": 0.00000000,
  "unconfirmed_balance": 0.00000000,
  "immature_balance": 0.00000000,
  "txcount": 94,
  "keypoololdest": 1507072726,
  "keypoolsize": 952,
  "unlocked_until": 0,
  "paytxfee": 0.00000000,
  "hdmasterkeyid": "c1c081490c4dc42b3e3431683052df36bc583fbe5"
}
```

### help ( "command" )

Proporciona ayuda y ejemplos para un comando específico o enumera todos los comandos (sin un parámetro). Los ejemplos están formateados para que pueda copiarlos y pegarlos para dar el comando (reemplazando los parámetros según corresponda).

```
help

== Blockchain ==
callcontract "address" "data" ( address )
getaccountinfo "address"
getbestblockhash
getblock "blockhash" ( verbosity )
getblockchaininfo
getblockcount
<snip>
```

### importaddress "address" ( "label" rescan p2sh )

Agrega una dirección Qtum de 34 caracteres o una dirección de clave pública de 66 caracteres hexadecimales que se puede ver como si estuviera en su billetera pero no se puede usar para gastar. La billetera se volverá a explorar después de ingresar este comando y se debe hacer una copia de seguridad después de agregar direcciones. Qtum-qt devuelve "nulo" y muestra el saldo "Solo observación", qtumd no devuelve nada.

```
importaddress QaL29jcCZ39pWcA334dA4BN3peVhnc42D

null
```

### importmulti "requests" ( "options" )

Importe múltiples direcciones / scripts (con claves privadas o públicas, canjee script (P2SH)), volviendo a escanear la blockchain para todas las nuevas direcciones en una sola pasada. Las marcas de tiempo opcionales pueden controlar qué tan atrás comienza el escaneo para cada dirección. Requiere una nueva copia de seguridad de la billetera después de agregar las direcciones.

Aquí importamos dos direcciones de solo reloj y escaneamos la blockchain desde las 00:00:00 horas GMT del 1 de junio de 2018 (marca de tiempo 1527811200). Después de ingresar el comando, la billetera tardará varios minutos en volver a escanear la blockchain para las nuevas direcciones:

```
importmulti '[{ "scriptPubKey": { "address": "QX4kcv3ZWZpax2tb44tpiv7q3wEB8Sek5" }, "timestamp":1527811200 }, { "scriptPubKey": { "address": "QN3BkewbR37fQs226ZA2qkh83mKS529B" }, "timestamp": 1527811200 }]'

importmulti(Ö)

[
  {
    "success": true
  },
  {
    "success": true
  }
]
```

### importprivkey "qtumprivkey" ( "label" ) ( rescan )

Agrega una clave privada WIF a su billetera, por ejemplo, tal como la devuelve dumpprivkey o de otra billetera Qtum. La billetera debe estar desbloqueada y requiere una nueva copia de seguridad de la billetera después. La billetera volverá a escanear durante unos minutos para agregar saldo a la nueva dirección y devolverá "nulo" si tiene éxito.

```
importprivkey cThA5YBGQggmpjSsBFLT1NXR18Fk16YBNd1kCVoERjbQ4d4TRMFf

null
```

### importprunedfunds

Importa fondos sin reescanear. La dirección o secuencia de comandos correspondiente se debe incluir previamente en la billetera. Enfocado hacia billeteras purgadas. El usuario final es responsable de importar transacciones adicionales que luego gastan los resultados importados o vuelven a explorar después del punto en la blockchain en que se incluye la transacción.

Ejemplo POR VENIR.

### importpubkey "pubkey" ( "label" rescan )

"Agrega una clave pública que se puede ver como si estuviera en su billetera pero no se puede usar para gastarla. La clave pública tiene 66 caracteres hexadecimales, y se puede obtener usando el comando` validateaddress`. Después de ingresar este comando, la billetera reescaneado durante unos minutos, qtum-qt devuelve "nulo" y qtumd no devuelve nada. Se debe hacer una copia de seguridad de la billetera después de importar una clave pública.

```
importpubkey 0381dc63bc14d32743a7741dc6a2993b8384dc3aa848332194bc851ff2a371b827

null
```

### importwallet "filename"

Importa claves desde una descarga de archivo de billetera (ver `dumpwallet`). Requiere una nueva copia de seguridad de la billetera después de este comando. Use la ruta completa de descarga de archivo. Qtum-qt mostrará un estado de "Importando" por un tiempo, luego "Escaneando" mientras vuelve a escanear la blockchain. Este comando puede tardar cinco minutos o más en regresar, y puede parecer que la billetera se congela durante este tiempo.

En una PC con la descarga de archivo en una carpeta "Copias de seguridad" en el escritorio:

```
importwallet "C:\Users\<username>\Desktop\Backups\dump 2019-01-14.txt"

null
```

### invalidateblock "blockhash"

Comando oculto. Marca permanentemente un bloque como no válido, como si violara una regla de consenso. Se usa para pruebas de software o en algunos escenarios de forking de blockchain manuales raros. Use `reconsiderblock` para revertir este comando. Devuelve "nulo" si tiene éxito.

```
invalidateblock 263f7ab042135cb0e5479afd8385a237f8eb44b86135d29b34eb0fa82cc815f

null
```

### keypoolrefill ( newsize )

Rellena el conjunto de claves con nuevas claves privadas, con un tamaño predeterminado de 100. El tamaño normal del conjunto de claves es 1,000 y la billetera llena de manera oportunista el conjunto de claves a medida que se usan las direcciones, por lo que este comando debe usar un tamaño de 1,100, etc. significativo. La billetera debe estar desbloqueada. qtum-qt devuelve "nulo", qtumd no devuelve nada.

```
keypoolrefill 1100

null
```

### listaccounts ( minconf include_watchonly)

OBSOLETO. Devuelve información sobre nombres de cuentas y saldos de cuentas. Da el saldo en Satoshis (QTUM x 0.00000001), incluida la cuenta predeterminada no definida.

Esta "cuenta" fue un intento de rastrear manualmente los saldos de bitcoin que se eliminarán con la versión 0.17, porque no funciona bien, por ejemplo, devolviendo valores negativos:

```
listaccounts
{
  "": -20077.14454684,
  "First": 9512.20615539,
  "Second": 0.00000000,
  "Third": 10564.97000000
}
```

### listaddressgroupings

Enumera las direcciones de recepción de la billetera y su saldo. Algunas direcciones pueden mostrar un saldo cero.

```
listaddressgroupings
[
  [
    [
      "QWfzQsi4rFA6u3zCguC9t3wYjd6Sm693g7",
      0.00000000
    ],
    [
      "QNf6fad5wLyeMT5e3hYy4qWnxcbV6GenWK",
      0.00000000
    ],
    [
      "QUytYGp47McSy8N6GzycV2Wt92d8JqHWCy",
      0.03160855,
      "MyAccount 1"
    ],
    <snip>
  ]
]
```

### Listbanned

Enumere todas las direcciones IP pares que han sido prohibidas.

```
listbanned

[
  {
    "address": "79.137.70.15/32",
    "banned_until": 1554322856,
    "ban_created": 1522786856,
    "ban_reason": "manually added"
  }
]
```

### listcontracts (start maxDisplay)

Enumera el hash de la dirección de los contratos inteligentes para la billetera y el saldo de los tokens asociados.

```
listcontracts

{
  "0162b1247a37af180eefba02b85df40d6d5d8e45": 0.00000000,
  "2c6734f611b46cc37eaafcc1e0d6b9953b7ae2cd": 0.08470000,
  "eb1939b4196ff26af3f7a379329ecf1caf0a47ab": 0.00000000,
  "26f6c6092c85f99649e08c4bc3ee8fab6b4aa905": 0.00000000,
  "988b1b1b42bb4f80935a6adf7efe2ba9aa6888bb": 0.00000001,
  "a181bf8cf9b1418a8ecba244aea70b4f4fbbea1e": 0.00000000,
  "68a203b2252dd6ebd3d90ff643fa47deae007e9e": 0.00000000
}
```

### listlockunspent

Devuelve una lista de salidas bloqueadas temporalmente (no utilizables). Vea también los comandos `lockunspent` y` unlock`. Si se reinicia la billetera, se desbloquean todos los bloqueos.

```
listlockunspent

[
  {
    "txid": "9fc384b55230ca1899dd1acf081033ebf57ae0335abf692c4f8a6336befc2f6",
    "vout": 1
  }
]
```

### listreceivedbyaccount ( minconf include_empty include_watchonly)

OBSOLETO. Liste el saldo de las cuentas.

```
listreceivedbyaccount

[
  {
    "account": "",
    "amount": 185.29137380,
    "confirmations": 23926
  },
  {
    "account": "Account 1",
    "amount": 8.82579750,
    "confirmations": 23927
  }
]
```

### listreceivedbyaddress ( minconf include_empty include_watchonly)

Lista de saldos por dirección de recepción.

```
listreceivedbyaddress

[
  {
    "address": "Qry5Ygp57Rcsy7N5gzYc32W49Ad9J2HjC5",
    "account": "First,
    "amount": 12.29616322,
    "confirmations": 12946,
    "label": "First",
    "txids": [
      "6478fc4d0ef0081e902f5f90A2483c82195ff18b7c38dcb9f2a388hdba94ae08",
      "5346419fac6dc35cag8aVc3172caeef59bD4cb50c8V773dc2c5e362F6bA20505",
      "6d8481be243fard24e69de6e49Z8442259b65fa9wed404be2fDb7w7free60565",
      "72w0016116v5b4fb5527110C73519fk868u22977f670M04b46641w11bpe331B8",
      "d303S6b3dAdc32479e5928eatdw6e45d5p64Q4686d23a4j7b4bB4ed1b9f81LeP"
    ]
  },
  {
    "address": "QH38kkF694yqy8a9enxQd3m3ekb87Kf7",
    "account": "",
    "amount": 0.60927503,
    "confirmations": 55329,
    "label": "",
    "txids": [
      "a93f5fa60bd753914fb72bf5bce8042cb66272c09495afcb7638397bd40abff94"
    ]
  },
  <snip>
]
```

### listsinceblock ( "blockhash" target_confirmations include_watchonly include_removed )

Enumere todas las transacciones para su billetera desde el blockhash dado, o una lista de todas las transacciones desde el bloque 1 si no se proporciona blockhash. Las siguientes transacciones muestran una transacción de envío y recepción.

```
listsinceblock 9957c2abcb56dead1cc7390acd50f52703fcd010aa5fd4a7c3ed7facb38cd287

{
  "transactions": [
    {
      "account": "",
      "address": "QX4c59CWVszq48kre57tmi4sjd2e59SrX5",
      "category": "send",
      "amount": -5.23000000,
      "label": "",
      "vout": 1,
      "fee": -0.00090400,
      "confirmations": 4,
      "blockhash": "4a1582348a59781cabfdd23551057a75faee481035c5dae395a5b522acff8db",
      "blockindex": 2,
      "blocktime": 1547693528,
      "txid": "c3da0be5b78ev626e6b8fb63ff366sa872d545a8c132267829c185f432acd938",
      "walletconflicts": [
      ],
      "time": 1547693438,
      "timereceived": 1547693438,
      "bip125-replaceable": "no",
      "abandoned": false
    },
    {
      "account": "",
      "address": "Qv5xGkDw89dpBAxn67k3ySawUtqna3fA3",
      "category": "receive",
      "amount": 4.50000000,
      "label": "",
      "vout": 0,
      "confirmations": 2,
      "blockhash": "8a5f521afb1437831aeffc4e5418521e9b37b029889a1ccdea249e23df6c35a",
      "blockindex": 2,
      "blocktime": 1547693720,
      "txid": "3a2df47bc22fea2e3aae416fe932cbe28c833e97b44f6dc03d903268a8bb2c2",
      "walletconflicts": [
      ],
      "time": 1547693638,
      "timereceived": 1547693638,
      "bip125-replaceable": "no"
    }
  ],
  "removed": [
  ],
  "lastblock": "835ca632a5bba30a0c836dfa497a43e5316acdf8b8437e42bcfa7e3554a61af"
}
```

### listtransactions ( "account" count skip include_watchonly)

Retorna hasta "contar" las transacciones mas recientes para tu billetera (predeterminado = 10) con varias opciones. Utilizar "cuenta" ha sido descartado

```
listtransactions

[
  {
    "account": "",
    "address": "Qd5tX39X2bjL9mvF2q5jkuD3Kre2ky79P",
    "category": "receive",
    "amount": 8.50000000,
    "label": "",
    "vout": 1,
    "confirmations": 3532,
    "blockhash": "0bc940fbfc7f66af8c4e11f9d3325a5ec42c69a2ecbd1d870338baeccf3e95d",
    "blockindex": 2,
    "blocktime": 1575639472,
    "txid": "95cf7a43c6ea87348fe1f8b365fcbed5579ea4422b16cbad0377ef6ee2f99af",
    "walletconflicts": [
    ],
    "time": 1575639440,
    "timereceived": 1575639472,
    "bip125-replaceable": "no"
  },
  {
    "account": "",
    "address": "QxW4S91mx3HM3qMB446ovoeT3VC341nr9",
    "category": "send",
    "amount": -1.58540000,
    "label": "",
    "vout": 0,
    "fee": -0.02003200,
    "confirmations": 1680,
    "blockhash": "6c6cbeaa5b480a39ad92d484bd3bcae4aa334b923b614f4b897ed736ad9e21f",
    "blockindex": 2,
    "blocktime": 1542934848,
    "txid": "55dc28cbff0ff7a94e5cb51a928703911baac60892bc6dea575bbdb9b3302673",
    "walletconflicts": [
    ],
    "time": 1542934828,
    "timereceived": 1542934828,
    "bip125-replaceable": "no",
    "abandoned": false
  },
<snip 8 more transactions>
]
```

### listunspent ( minconf maxconf ["addresses",...] [include_unsafe] [query_options])

Devuelve una matriz de salidas de transacciones no gastadas, que se pueden ordenar por número de confirmaciones o por una dirección específica.

```
listunspent

[
  {
    "txid": "d36ba8beb38c7118b3bc6e8c90d54b58d7d53ef603c49039df2abb5d160ea",
    "vout": 1,
    "address": "QU5nyP844LKcmpk244jmd06CEep828h",
    "account": "",
    "scriptPubKey": "76a914bd3b1563bedea856a7ca5df8aac54a0ab56f2985ad",
    "amount": 1.10000000,
    "confirmations": 2632,
    "spendable": true,
    "solvable": true,
    "safe": true
  },
  {
    "txid": "2c55ecdb59be333ad04df5a97ca2f536ed16351de344db94a326f65f7560c54",
    "vout": 10,
    "address": "Qx9N8Lz26NduP4e39gpJ33EYd22Ms9vsp",
    "account": "",
    "scriptPubKey": "76a914986c8cbd67dbb55dcaf261be37a528c6868fee0723s",
    "amount": 2.40000000,
    "confirmations": 15843,
    "spendable": true,
    "solvable": true,
    "safe": true
  },
  <snip>
]
```

### listwallets

Da el archivo wallet.dat cargado actualmente, generalmente "wallet.dat" a menos que pueda cargar un archivo diferente con "Restaurar billetera".

```
listwallets

[
  "wallet1132019.dat"
]
```

### lockunspent unlock ([{"txid":"txid","vout":n},...])

Actualiza la lista de salidas temporalmente inutilizables. Bloquee temporalmente (desbloqueo = falso como se muestra a continuación) o desbloquee (desbloqueo = verdadero) las salidas de transacción especificadas. Si no se especifican transacciones al desbloquear, se desbloquean todas las transacciones bloqueadas actuales.

Una salida de transacción bloqueada no se elegirá mediante la selección automática de monedas al gastar QTUM.

Los bloqueos se almacenan solo en la memoria. Las billeteras se inician con cero salidas bloqueadas y la lista de salidas bloqueadas siempre se borra (en virtud de la salida del proceso) cuando una billetera se detiene o falla. Vea también la llamada `listunspent`.

```
lockunspent false "[{\"txid\":\"9fc384b55230ca1899dd1acf081033ebf57ae0335abf692c4f8a6336befc2f6\",\"vout\":1}]"

true
```

### logging ( )

Obtiene y establece la configuración de registro para el archivo debug.log. Cuando se llama sin argumento, devuelve la lista de categorías con el estado que actualmente se está depurando o no. Cuando se llama con argumentos, agrega o elimina categorías del registro de depuración. Los argumentos se evalúan en orden "incluir" y luego "excluir". Si un artículo está incluido y excluido, terminará siendo excluido.

Las categorías de registro válidas son: net, tor, mempool, http, bench, zmq, db, rpc, Estimatefee, addrman, selectcoins, reindex, cmpctblock, rand, prune, proxy, mempoolrej, libevent, coindb, qt, leveldb, coinstake, y http-poll.

Aquí activamos el registro de "mempool" y "mempoolrej" (se enumeran primero para "incluir") y desactivamos "http". Devuelve el estado actual de registro de depuración.

```
logging "[\"mempool\", \"mempoolrej\"]" "[\"http\"]"

{
  "net": 0,
  "tor": 0,
  "mempool": 1,
  "http": 0,
  "bench": 0,
  "zmq": 0,
  "db": 0,
  "rpc": 0,
  "estimatefee": 0,
  "addrman": 0,
  "selectcoins": 0,
  "reindex": 0,
  "cmpctblock": 0,
  "rand": 0,
  "prune": 0,
  "proxy": 0,
  "mempoolrej": 1,
  "libevent": 0,
  "coindb": 0,
  "qt": 0,
  "leveldb": 0,
  "coinstake": 0,
  "http-poll": 0
}
```

### move "fromaccount" "toaccount" amount ( minconf "comment" )

OBSOLETO. Mueva una cantidad específica de una cuenta en su billetera a otra. Devuelve "verdadero" si el comando se puede analizar, ya sea que existan o no las cuentas o que se haya producido el movimiento.

```
move "Test Addr" "LTCp2shsegwit" 1.1

true
```

### ping

Solicita que se envíe un ping a otros pares, para medir el tiempo de ping. Los resultados se proporcionan en los campos `getpeerinfo`," pingtime "y" pingwait "son segundos decimales (no proporciona un resultado directo como usar" ping "desde un símbolo del sistema). El comando ping se maneja en la cola con todos los demás comandos, por lo que mide el procesamiento del trabajo acumulado, no solo el ping de la red.

```
ping

null
```

### preciousblock "blockhash"

Prioriza un bloque con un tiempo anterior para bloques a la misma altura. Utilizado en situaciones de horquilla dura. Ver también `invalidateblock`. qtum-qt devuelve "nulo" si tiene éxito, qtumd no devuelve nada si tiene éxito.

```
preciousblock 854d57da75ba7550aebe83c1cdf539ac685d735684b7c40cfd639582abf43b

null
```

### prioritisetransaction

Acepta la transacción en bloques minados con una prioridad más alta (o más baja). En realidad, no se paga una tarifa más alta, el algoritmo para seleccionar transacciones en un bloque (que está tratando de maximizar las tarifas) considera que la transacción ha pagado una tarifa más alta. Qtum-qt y qtumd devuelven "verdadero":

```
prioritisetransaction "01b347eb32bca5cde81444f6a6d4311f02ae3f3da25394e0f144fca525218dd" 0.0 10000

true
```

### pruneblockchain

Pode la blockchain hasta un bloque determinado. La poda elimina las transacciones gastadas para reducir el tamaño de almacenamiento de la blockchain. Devuelve el último bloque purgado. La billetera debe iniciarse en modo de poda con espacio de trabajo en disco reservado, al menos 550 MB, aquí con 2 GB de espacio de trabajo:

```
qtum-qt.exe -prune=2000
```

Entonces puedes dar el comando

```
pruneblockchain 125000

125000
```

No purgue la blockchain si su billetera acepta conexiones entrantes (más de 8 pares) porque su billetera necesita poder enviar todos los bloques para arrancar nuevos pares que se conectan.

### reconsiderblock "blockhash"

Comando oculto Elimina el estado de invalidez de un bloque y sus descendientes, utilizado para pruebas de código o en la reorganización manual de blockchain. Este comando puede revertir los efectos de `invalidateblock`. Devuelve "nulo" si tiene éxito:

```
reconsiderblock 263f7ab042135cb0e5479afd8385a237f8eb44b86135d29b34eb0fa82cc815f

null
```

### removeprunedfunds "txid"

Elimina la transacción especificada de la billetera. Destinado a su uso con billeteras purgadas y como acompañante de `importfunedfunds`. Esto afectará los saldos de billetera. Qtum-cli devuelve "nulo".

```
removeprunedfunds "535e2bf90fda10c8c8186c4c73ac2861cb19312507b9e4552e78a6148030f19f"

null
```

### rescanblockchain ("start_height") ("stop_height")

Vuelva a escanear la blockchain local para transacciones de billetera. Se puede usar una altura de inicio y una altura de detención opcionales, o escanear por defecto toda la blockchain. Este comando escaneará la blockchain en busca de transacciones de su billetera, y puede usarse si el saldo de la billetera no parece ser correcto después de una restauración de la billetera o al agregar claves privadas. Devuelve el inicio y la altura superior escaneada.

```
rescanblockchain 100000 200000

{
  "start_height": 100000,
  "stop_height": 200000
}
```

### resendwallettransactions

Comando oculto Retransmita inmediatamente las transacciones de billetera no confirmadas a todos sus pares. La billetera se retransmite periódicamente de forma automática, por lo que se puede usar para realizar pruebas. Aquí se reenviaron dos transacciones después de estar atascadas en el mempool local después de reiniciar la billetera.

```
resendwallettransactions

[
  "8b4c25d4959cd43f6ee2ce5ab397ca32860dd6c4f2c0d83e9631aa137803124ed",
  "f5c615ca95bc324bebca4823a4ff972dc0a3950d6d7d398f238df935c5bb713c4"
]
```

### reservebalance [ [amount]]

Establece la cantidad de monedas que no se utilizarán para el staking y se pueden enviar de inmediato frente a esperar 500 confirmaciones después de desactivar el staking. Devuelve el estado de reserva y el importe.

```
reservebalance true 50

{
  "reserve": true,
  "amount": 50.00000000
}
```

### savemempool

Escribe el grupo de memoria en el disco en el archivo mempool.dat. Qtum-qt devuelve "nulo", qtumd no tiene respuesta.

```
savemempool

null
```

### searchlogs (address) (topics)

Devuelva los eventos de registro de contrato inteligente entre dos bloques (inclusive). El comando requiere que '-logevents' esté habilitado en el inicio de la billetera. Use el hash de la dirección del contrato si lo desea.

```
searchlogs 274690 274700

[
  {
    "blockHash": "d3168805de880ff19108c119f3701604b71fc6f5c3586b9d6f5b137d70e76ca7",
    "blockNumber": 274690,
    "transactionHash": "5d957c6b03557b514f03b0f68ef0e9bb140c99b5e9a00186f36eb4b3213463c1",
    "transactionIndex": 2,
    "from": "1854f76267a1e142dccc6c5697066f6a09a7c069",
    "to": "2e1b8528c07539b5dd9a76f3374adf09f1ab6075",
    "cumulativeGasUsed": 37968,
    "gasUsed": 37968,
    "contractAddress": "2e1b8528c07539b5dd9a76f3374adf09f1ab6075",
    "excepted": "None",
    "log": [
      {
        "address": "2e1b8528c07539b5dd9a76f3374adf09f1ab6075",
        "topics": [
          "ddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
          "0000000000000000000000001854f76267a1e142dccc6c5697066f6a09a7c069",
          "000000000000000000000000e57e4a5f9ac130defb33a057729f10728fcdb9cb"
        ],
        "data": "0000000000000000000000000000000000000000000316d984535eb922280000"
      }
    ]
  },
  {
    "blockHash": "b35295f75e57b1a9dd0c4797c8f090a8d4bc7d6fc936208616d00c9c079e82aa",
    "blockNumber": 274696,
    "transactionHash": "de6e0bf79c04386ba05f8c83bea025451492bd0140b3cf1ba4e010c2339adf9b",
    "transactionIndex": 8,
    "from": "f30a2e96271180258aaac50956f0af94c4610beb",
    "to": "f2033ede578e17fa6231047265010445bca8cf1c",
    "cumulativeGasUsed": 36423,
    "gasUsed": 36423,
    "contractAddress": "f2033ede578e17fa6231047265010445bca8cf1c",
    "excepted": "None",
    "log": [
      {
        "address": "f2033ede578e17fa6231047265010445bca8cf1c",
        "topics": [
          "ddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
          "000000000000000000000000f30a2e96271180258aaac50956f0af94c4610beb",
          "000000000000000000000000e57e4a5f9ac130defb33a057729f10728fcdb9cb"
        ],
        "data": "00000000000000000000000000000000000000000000000000000059c78d0fff"
      }
    ]
  }
]
```

### sendfrom "fromaccount" "toaddress" amount ( minconf "comment" "comment_to" )

DEPRECATED (use `sendtoaddress`). Enviar una cantidad a una dirección Qtum, requiere que la billetera esté desbloqueada. La "cuenta" es para notación, no controla la fuente de UTXO. Si tiene éxito, devuelve la identificación de la transacción.

```
sendfrom "" QcEz4erq5gH6sa3ujWsqpZW4869MwrQf5 1.0

3e5ae45efbde38318a3a8af1d5c4d3bb844c58fab745f21d42a449ad923af3f
```

### sendmany "fromaccount" {"address":amount,...} ( minconf "comment" ["address",...] replaceable conf_target "estimate_mode")

Enviar a múltiples direcciones, requiere que la billetera esté desbloqueada. Las cantidades son de coma flotante en QTUM. No ponga espacios en blanco entre los parámetros. Si tiene éxito, devuelve una única ID de transacción que contiene todas las salidas. Aquí enviamos a dos direcciones diferentes:

```
sendmany "" "{\"QcEz4erq5gH6sa3ujWsqpZW4869MwrQf5\":0.5,\"QM5yJs3v3u9vAVE5XseFa9g63ke6Ld9Wp\":0.77}"

7a5077ac6e42acbed182c35eb034702e1fadd5c7d1547a85ae63dc0e151ed5
```

### sendmanywithdupes "fromaccount" {"address":amount,...} ( minconf "comment" ["address",...] )

Enviar a múltiples direcciones, requiere que la billetera esté desbloqueada. Las cantidades son de coma flotante en QTUM. No ponga espacios en blanco entre los parámetros. Si tiene éxito, devuelve una única ID de transacción que contiene todas las salidas. Aquí enviamos a dos direcciones diferentes:

```
sendmanywithdupes "" "{\"QFKw7VXsm23Hi71KUU5dXvpV3mDc9Au29\":200.0,\"QFKw7VXsm23Hi71KUU5dXvpV3mDc9Au29\":250.0}"

7d90b8365ba85de8c4bd19e1a94ebe9c8a5b9938385e5b10496a0ad5359824f
```

### sendrawtransaction "hexstring" ( allowhighfees )

Transmite una transacción sin codificar hexadecimal a la red. También vea `createrawtransaction` y` signrawtransaction`. Devuelve el hash de la transacción en hexadecimal, que es el ID de la transacción.

```
sendrawtransaction 020000003d6b5df207d94bafb4520adca3871fdaf397afd20f60f0a39c6fc353ae18000000006b5734040229999abc42d6d1e095b07b4538cb8a1b4ea2c42852feffcfb36dc8494b5238f24402100514aab22c8be9458056bb14f755adae12adf15721eb0b6cd314230237c26707210dd486ffc6e7ea92f2b30e428c1f3726e3dfc09418bb815f64bd32d7d5836f89fffffff0301e1d505420000002976b414d4fcc597395462ec3fdab4d6b49bc9af53fed3d87add09fe60400000001986a824dcead1313bfdde586b8bc3cd2ace54d4fa4b6f6887ad0000000

8f2cb4f0363ac5b4d3b5492722c5ab9eb91ab635b5d62354b3f1b42f73dc84
```

### sendtoaddress "address" amount ( "comment" "comment_to" subtractfeefromamount replaceable conf_target "estimate_mode" "sender address" changeToSender )

Envía a una dirección, con opciones para varios comentarios y especificando la dirección desde la cual enviar las monedas. La billetera debe estar desbloqueada. Si tiene éxito, devuelve la identificación de la transacción.

```
sendtoaddress QDYtmXP2X4b3fKmt2hujwmD74tdPkF4oH 0.1

04efe64bfd72f82c7ce94702fe1a2c946934efb46ed8e0772bad36ea45ce3c8d
```

### sendtocontract "contractaddress" "data" (amount gaslimit gasprice senderaddress broadcast)

Enviar fondos y datos a un contrato.

Argumentos:

1. "contractaddress" (cadena, requerida) La dirección del contrato que recibirá los fondos y los datos
2. datos "datahex" (cadena, necesarios) para enviar
3. "monto" (numérico o cadena, opcional) El monto en QTUM para enviar, predeterminado: 0
4. gasLimit (numérico o cadena, opcional) gasLimit, predeterminado: 250000, máx .: 40000000
5. gasPrice (numérico o cadena, opcional) gasPrice QTUM precio por unidad de gas, predeterminado: 0.0000004, min: 0.0000004
6. "senderaddress" (cadena, opcional) La dirección Qtum que se utilizará como remitente
7. "broadcast" (bool, opcional, default = true) Si se transmite la transacción o no
8. "changeToSender" (bool, opcional, predeterminado = verdadero) Devuelve el cambio al remitente

Devuelve información de la transacción:

```
sendtocontract "0bf3bca874ddf209dae6863743d749d83bfded4" "53e62baf"

{
  "txid": "cb3c85a8282afb599edcd421d053b824383ca593aeb328ad7628f20a2c38abe",
  "sender": "QdB38N29nc3zb3pb238PWzs3Sbp88ew4m",
  "hash160": "dc7a88381e7d027d0becf368557acbf624a7b82"
}
```

### setaccount "address" "account"

OBSOLETO. Asigna y nombre de cuenta a la dirección dada. Qtum-qt devolverá "nulo" si tiene éxito.

```
setaccount "QJv3YhWxG6EC2cpqZM5E3fjGzXYgakezm" "My New Account"

null
```

### setban "subnet" "add|remove" (bantime) (absolute)

Intenta agregar o eliminar una dirección IP de la lista prohibida. Use "agregar" para agregar una prohibición y especifique la duración de la prohibición en segundos. Devuelve "nulo" si tiene éxito. Aquí agregamos una prohibición por un día y confirmamos el resultado con `listbanned`:

```
setban "116.61.213.45" "add" 86400

null


listbanned

[
  {
    "address": "116.61.213.45/32",
    "banned_until": 1547586400,
    "ban_created": 1547500000,
    "ban_reason": "manually added"
  }
]
```

### setmocktime timestamp

Comando oculto Establezca la hora local en la marca de tiempo dada, solo funciona para la nueva prueba. Dé un tiempo de época en segundos, o 0 para volver a la hora del sistema. La interfaz de línea de comando no tiene retorno.

```
docker exec myapp qcli setmocktime 1547319783
```

### setnetworkactive true|false

Se usa para habilitar / deshabilitar las conexiones de red de igual. Devuelve el estado de la conexión de red. Para deshabilitar las conexiones de red:

```
setnetworkactive false

false
```

### settxfee amount

Establezca la tarifa de transacción por kilobyte del mensaje de transacción. Sobrescribe el parámetro paytxfee visto en `getwalletinfo`. La tarifa mínima predeterminada por 1,000 bytes es 0.004 QTUM. Devuelve verdadero si tiene éxito.

```
settxfee 0.01

true
```

`getwalletinfo` mostraría" paytxfee ": 0.01000000,

### signmessage "address" "message"

Firme un mensaje usando la clave privada de una dirección, la billetera debe estar desbloqueada. Devuelve un hash de firma base 64.

```
signmessage "Qg3WDvb1Ey2oqAW2EpM5evdv3Ufnvre3n" "message"

IJTWLjS9oma8M+EsXVnESR12jONwjMky4YimE0cQnvtAcQyim3lJPQ58Q6IADifR3I10LyMctNAe+2Kc274AqLu=
```

Utilice `verifique el mensaje` para verificar un mensaje.

### signmessagewithprivkey "privkey" "message"

Firme un mensaje con la clave privada de una dirección, la billetera debe estar desbloqueada. Devuelve un hash de firma base 64.

```
signmessagewithprivkey "cSxP62VDq527SWRddkX5D49mNekwNz9nexaikk55RG5X2AXEFvq" "hello world"

signmessagewithprivkey(Ö)

H3SBMeQUvo82A63wegSNT582Puziba54sCGt6notPb3xHm3WwM2OuIwV4E9Ya38TMCqe2aV7rmuFrc9A2Qb+t3A=
```

Utilice el mensaje de verificación para verificar un mensaje.

### signrawtransaction "hexstring" ( [{"txid":"id","vout":n,"scriptPubKey":"hex","redeemScript":"hex"},...] ["privatekey1",...] sighashtype )

Firma una transacción sin procesar en preparación para enviarla a la red. La billetera debe estar desbloqueada. Consulte `createrawtransaction` y` sendrawtransaction`.

```
signrawtransaction 020000001d637cf207c6418fb6220cfcb2b141ba5d230f0ba0a43c68b358aff9a8a6000000000fffffff0509e5f50480000001983a952d5fb15a70832ffdc3cadd3dc7749a49bf053ed6defacd09ef6060000000187aa814bd4ae4167bebbf56bb7c51c5eabf35d50a5c6e7f33ad0000000

{
  "hex": "020000003d6b5df207d94bafb4520adca3871fdaf397afd20f60f0a39c6fc353ae18000000006b5734040229999abc42d6d1e095b07b4538cb8a1b4ea2c42852feffcfb36dc8494b5238f24402100514aab22c8be9458056bb14f755adae12adf15721eb0b6cd314230237c26707210dd486ffc6e7ea92f2b30e428c1f3726e3dfc09418bb815f64bd32d7d5836f89fffffff0301e1d505420000002976b414d4fcc597395462ec3fdab4d6b49bc9af53fed3d87add09fe60400000001986a824dcead1313bfdde586b8bc3cd2ace54d4fa4b6f6887ad0000000",
  "complete": true
}
```

### stop

Se cierra y sale de la billetera. Sin valor de retorno: la billetera se cierra.

```
stop
```

### submitblock "hexdata" ( "dummy" )

Intenta enviar un nuevo bloque a la red. Ver https://en.bitcoin.it/wiki/BIP_0022 para la especificación completa. Use `getblocktemplate` para construir un bloque junto con el encabezado del bloque y las transacciones.

Argumentos

1. "hexdata" (cadena, requerida) los datos del bloque codificado en hexadecimal para enviar
2. valor ficticio "ficticio" (opcional), para compatibilidad con BIP22. Este valor es ignorado.

Ejemplo POR VENIR.

### syncwithvalidationinterfacequeue

Comando oculto Espera a que se completen todas las filas de validación asincrónicas (para blockchain, mempool, etc.). Para uso de los desarrolladores. Qtum-qt devuelve "nulo", qtumd no devuelve nada.

```
syncwithvalidationinterfacequeue

null
```

### uptime

Da el tiempo de actividad de la billetera (desde el inicio) en segundos.

```
uptime

12592
```

### validateaddress "address"

Devuelva información detallada sobre una dirección, aquí la dirección multigrado de `addmultisigaddress`:

```
validateaddress mKa7c52cX97eK4vdk35jV442p3j59hk3R

{
  "isvalid": true,
  "address": "mKa7c52cX97eK4vdk35jV442p3j59hk3R",
  "scriptPubKey": "a813bcd644a82f494ae0ef442a5253c0ebde7b20b2f29",
  "ismine": true,
  "iswatchonly": false,
  "isscript": true,
  "iswitness": false,
  "script": "multisig",
  "hex": "52460396bc49812bad50949fbc0bbd44e95bf32a5695519b3ff267a5d93cba3bd169b2393cd4864da4c2786dd3322fcfcb239c3db185ef33fa14836b8fecf36c68bb84ddac92f2",
  "sigsrequired": 2,
  "pubkeys": [
    "03a64c40c2d385306afcc08fd56b35bfe38626df29b3ef6a935bbf8523afb1fa5",
    "03bf3874f4c496cb472ccb2c9b3fce6f2a6bc09ff1b826cba33f2ac83ab2495fe"
  ],
  "addresses": [
    " Qgw5Ds4Py6J2oBX3EKP3kyde2UpnWn7eV",
    " QK3bx79fzkei5XF7h2q7wB4s6MK99u29x"
  ],
  "account": ""
}
```

### verifychain ( checklevel nblocks )

Verifica la base de datos de blockchain para un valor predeterminado de 6 bloques, devuelve verdadero o falso.

```
verifychain

true
```

### verifymessage "address" "signature" "message"

Verifique un mensaje firmado. Devuelve verdadero o falso.

```
verifymessage "Qg3WDvb1Ey2oqAW2EpM5evdv3Ufnvre3n" "IJTWLjS9oma8M+EsXVnESR12jONwjMky4YimE0cQnvtAcQyim3lJPQ58Q6IADifR3I10LyMctNAe+2Kc274AqLu=" "hello world"

true
```

Consulte `signmessage` para crear una firma de mensaje.

### verifytxoutproof "proof"

Verifica que una prueba apunta a una transacción en un bloque, devolviendo la transacción si se encuentra o dando una tring vacía o un error que no se encuentra en la mejor cadena. La "prueba" es la cadena hexadecimal de `gettxoutproof`.

```
verifytxoutproof 00000020a8/<snip/>d38abf491d

[
  "cb0ef481c7be99a23686abfca6c671acc21b9aa35bc34bcc29b22effbacc610b"
]
```

### waitforblock (timeout)

Comando oculto Se usa para monitorear cuando la recarga de blockchain ha alcanzado un bloque determinado. Para interfaces de línea de comandos como qtumd (no para la billetera GUI qtum-qt), el comando regresa después de cargar el bloque dado. Este ejemplo espera el bloque Mainnet 150,000:

```
qtum-cli waitforblock ae4699ac0a8f4d1170767167fd3b0639312850ce33dcb55a0afd0f5c1a88406f

{
  "hash": "ae4699ac0a8f4d1170767167fd3b0639312850ce33dcb55a0afd0f5c1a88406f",
  "height": 150000
}
```

### waitforblockheight (timeout)

Comando oculto Espera (al menos) la altura del bloque y devuelve la altura y el blockhash de la punta actual (bloque más alto). Devuelve el bloque actual en el tiempo de espera o la salida. El tiempo de espera se da en milisegundos, 0 o el valor predeterminado es sin tiempo de espera. Este comando solo funciona desde la línea de comando (no con la billetera qtum-qt GUI) y se usa para el desarrollo.

En Docker regtest:

```
docker exec myapp qcli waitforblockheight 7210

{
  "hash": "b5bd2dfa428effb185a31513315bbae6284ab59b9942759e07d9110770ae9c61",
  "height": 7210
}
```

En Mainnet con qtumd:

```
qtum-cli waitforblockheight 281985

{
  "hash": "44f6a6909b255f9932e28322174c6eec201790d84e7d4f9c201c92594914d240",
  "height": 281985
}
```

### waitforlogs (fromBlock) (toBlock) (filter) (minconf)

requiere que '-logevents' esté habilitado

Espera un nuevo registro y devuelve entradas de registro coincidentes. Cuando la llamada regresa, también especifica el siguiente número de bloque para comenzar a esperar nuevos registros. Al llamar a waitforlogs repetidamente utilizando el número devuelto `nextBlock`, un cliente puede recibir una secuencia de entradas de registro actualizadas.

Esta llamada es diferente de los `registros de búsqueda` de nombre similar. Esta llamada devuelve entradas de registro coincidentes individuales, `searchlogs` devuelve un recibo de transacción si una de las entradas de registro de esa transacción coincide con las condiciones del filtro.

Argumentos:

1. fromBlock (int | "latest", opcional, default = null) El número de bloque para comenzar a buscar registros. ()
2. toBlock (int | "latest", opcional, default = null) El número de bloque para dejar de buscar registros. Si es nulo, esperará indefinidamente en el futuro.
3. filtro ({direcciones ?: Hex160String [], temas ?: Hex256String []}, opcional predeterminado = {}) Condiciones de filtro para registros. Las direcciones y los temas se especifican como una matriz de cadenas hexadecimales
4. minconf (uint, opcional, predeterminado = 6) Número mínimo de confirmaciones antes de que se devuelva un registro

Ejemplo POR VENIR.

### waitfornewblock (timeout)

Comando oculto Espera un nuevo bloque y devuelve el blockhash y la altura. Devuelve el bloque actual en el tiempo de espera o la salida. Este comando funciona solo en la línea de comando (no con la billetera GUI qtum-qt) y se utiliza para el desarrollo. El parámetro de tiempo de espera se da en milisegundos y 0 indica que no hay tiempo de espera.

En Docker con regtest:

```
waitfornewblock

{
  "hash": "47f1ddc856ba47a242cbdc771d198296f3a1343f81aad21d454bec438972868c",
  "height": 7207
}
```

En Mainnet con qtumd:

```
qtum-cli waitfornewblock

{
  "hash": "b4caac261c4f5386076bbb07e0dc94b92fb67ca740b8a5d7b49cddcaffd6f103",
  "height": 281981
}
```

### walletlock

Bloquea una billetera encriptada.

```
walletlock

null
```

qtum-cli no devuelve ninguna respuesta, pero puede verificar con `getwalletinfo` para" unlocked_until ": 0 y verificar el icono del candado en qtum-qt.

### walletpassphrase "passphrase" timeout ( true )

Desbloquee una billetera encriptada para transacciones que requieren el uso de una clave privada, como enviar monedas, estacar o exportar claves privadas. El tiempo de espera proporciona el tiempo en segundos para desbloquear y el "verdadero" booleano opcional permite el desbloqueo solo para staking.

Este comando desbloqueará la billetera durante 10 minutos:

```
walletpassphrase "you should always use a long and strong passphrase" 600
```

Este comando desbloqueará la billetera durante 10 minutos:

```
walletpassphrase "you should always use a long and strong passphrase" 99999999 true
```

La billetera qtum-qt mostrará el estado de bloqueo con el icono del candado y la consola devolverá "nulo". qtum-cli no devuelve ningún estado, pero puede verificar el estado de desbloqueo con `getwalletinfo` para" unlocked_until ":

### walletpassphrasechange "oldpassphrase" "newpassphrase"

Cambia la frase de contraseña de la billetera de "oldpassphrase" a "newpassphrase", qtum-qt devuelve "null", qtumd no devuelve nada.

```
walletpassphrasechange "you should always use a long and strong passphrase" "please use a strong and long passphrase"

null
```

\```

[
](https://docs.qtum.site/en/Adding-Nodes/)