# Staking fuera de linea 

* [Delegar dirección a Super Stacker](https://github.com/qtumproject/documents/tree/master/en/Qtum-Wallet-Tutorial/README.md#delegating-address-to-super-staker)
* [Delegar operaciones de dirección](https://github.com/qtumproject/documents/tree/master/en/Qtum-Wallet-Tutorial/README.md#delegating-aAddress-operations)
* [Configuración Super Stacker](https://github.com/qtumproject/documents/tree/master/en/Qtum-Wallet-Tutorial/README.md#super-staker-configuration)
* [Lanzamiento de Qtum Core como Super Stacker](https://github.com/qtumproject/documents/tree/master/en/Qtum-Wallet-Tutorial/README.md#launching-qtum-core-as-a-super-staker)
* [qtumd Super Staker](https://github.com/qtumproject/documents/tree/master/en/Qtum-Wallet-Tutorial/README.md#qtumd-super-staker)
* [Operaciones Super Stacker ](https://github.com/qtumproject/documents/tree/master/en/Qtum-Wallet-Tutorial/README.md#super-staker-operations)
* [Restaurar](https://github.com/qtumproject/documents/tree/master/en/Qtum-Wallet-Tutorial/README.md#restore)

# Dirección elegible para Super Stacker

Qtum Staking Fuera de linea permite que se delegue la dirección de una billetera no-staking (capaz de realizar la transacción de asignación de delegación) a un Super Staker. El Staking fuera de linea no es de custodia: el usuario de la delegación mantiene el control total de sus monedas y claves privadas. La delegación de dirección se realiza a través de una transacción de contrato inteligente de la billetera del usuario de la delegación que identifica la dirección del delegador, la dirección de Super Staker y la tarifa que el delegador acepta pagar. Si el Super Staker acepta esta tarifa, comenzará a staking los UTXO de la dirección delegada.

Las reglas normales para staking UTXOs aplican a UTXOs delegadas:

* Los UTXO solo se pueden usar para staking después de que maduren (500 confirmaciones)
* El Super Staker establecerá un tamaño mínimo de UTXO para stake, por defecto a 100 QTUM. Los UTXO delegados por debajo de esta cantidad serán ignorados.
* Es una buena práctica (para obtener rendimientos óptimos) dividir los UTXO en tamaños de 100 a 200 QTUM cada uno. Para los usuarios de la billetera Qtum Core, esto se puede lograr fácilmente con la versión de línea de comandos de `splitutxosforaddress`, que se describe a continuación.

Para realizar la asignación de delegación desde la billetera Qtum Core, seleccione Stake- Delegaciones, el botón Agregar delegación "+" en la esquina superior derecha, ingrese el nombre del Staker (solo para referencia local), la dirección del Staker, la tarifa que acepta pagar y Su dirección para ser delegada. Deje en paz la configuración predeterminada de Gas a menos que comprenda cómo configurarla. La transacción de delegación requerirá al menos 0,9 QTUM en tarifas y se reembolsará cualquier exceso.

![1  Add Delegation Assignment](https://user-images.githubusercontent.com/29760787/85331894-f8cc5b80-b4a4-11ea-95d1-eb472a5454f1.jpg)

Presione Confirmar y Sí para enviar la transacción de delegación.

La delegación de direcciones también se puede lograr utilizando la billetera Qtum Electrum, que admite direcciones de billetera de hardware Ledger.

# Delegar operaciones de dirección

La transacción de la Dirección de delegado se envía a un contrato inteligente que mantiene las asignaciones de delegación y el Super Staker la recogerá allí. Puede ver las transacciones de recompensa de bloque de Dirección delegada en la billetera y también con el explorador [qtum.info] (https://qtum.info/).

Si la billetera tiene QTUM en varias direcciones, la delegación debe hacerse por separado para cada dirección (y la tarifa de transacción pagada por cada dirección), por lo que puede tener sentido consolidar los UTXO en una sola dirección antes de dividir UTXO y delegar. En este caso, use la selección de monedas para seleccionar y consolidar las direcciones. Alternativamente, el comando `sendmanywithdupes` podría usarse para enviar todo el saldo de la billetera a una nueva dirección con UTXO de tamaño apropiado.

Si el Super Staker acepta una delegación por una tarifa particular, y luego el Super Staker reduce esa tarifa (acepta asignaciones por una tarifa más baja), para aprovechar esa tarifa más baja, el usuario debe delegar su dirección nuevamente con la tarifa más baja establecida.

Las delegaciones de una billetera se pueden verificar en la página Estaca - Delegaciones o con el comando `getdelegationinfoforaddress`.

Haga una copia de seguridad de su billetera para guardar una copia del archivo wallet.dat.
 

# Configuración Super Stacker

La billetera Qtum Core proporciona Prueba de participación en línea y se puede iniciar y configurar para operar como Super Staker y recibir delegaciones de direcciones.

Para configurar la billetera Qtum-Qt para un Super Staker, seleccione Stake - Super Staking y el botón "+" para agregar un nuevo Super Staker. Ingrese el nombre del Staker (solo para referencia local, aquí usando la primera parte de la dirección y "10" para indicar una tarifa del 10%) y seleccione la dirección del Staker usando el menú desplegable.

![2  Super Staker Setup](https://user-images.githubusercontent.com/29760787/85331902-fc5fe280-b4a4-11ea-9506-84bfc0ecd6d5.jpg)

Para operar como Super Staker, la billetera debe poder verificar direcciones arbitrarias (índice de direcciones), tener registros habilitados para operaciones de contratos inteligentes (eventos de registro), estar habilitados para staking y el único parámetro `-superstaking = true` establece estos tres parámetros La primera vez que se inicia con `-superstaking = true`, la billetera volverá a escanear la blockchain para reconstruir la base de datos para agregar el índice de direcciones y los eventos de registro.

A continuación, la billetera solicitará que se reinicie como Super Staker usando Configuración - Opciones - Habilitar la superestabilización y OK para reiniciar la billetera.

![3  Qtum-Qt Enable Super Staker](https://user-images.githubusercontent.com/29760787/85331912-008c0000-b4a5-11ea-9901-c4b4433a8746.jpg)

Al inicio, la billetera confirmará que desea escanear y reconstruir la base de datos.

![4  Rebuild the Database](https://user-images.githubusercontent.com/29760787/85331921-041f8700-b4a5-11ea-8990-628f295ff4a9.jpg)

La billetera mostrará "Reindexando bloques en el disco ..." y "Sincronizando encabezados" mientras reconstruye la base de datos, esto puede tomar varias decenas de minutos dependiendo de su computadora.

Después del lanzamiento, regrese a la página Stake - Super Staking y seleccione el botón "Configurar súper staker" (el símbolo del engranaje ahora estará visible) para competir con la configuración de Super Staker. Haga clic en el cuadro Personalizado para ver las recomendaciones predeterminadas (que se muestran a continuación) o personalizar la configuración. Haga clic en Aceptar para completar la configuración.

![5  Super Staker Options](https://user-images.githubusercontent.com/29760787/85331928-084ba480-b4a5-11ea-8434-82f9f140b6b6.jpg)

Los ajustes de configuración son:

* Tarifa mínima: la tarifa mínima ofrecida por los delegadores que aceptará el Staker.
* Tamaño mínimo de UTXO: establece el UTXO de tamaño mínimo que el Staker evaluará para el consenso de Prueba de participación. Con el tiempo, la dirección delegada debe acumular muchos UTXO de recompensa de bloque pequeño y es ineficiente administrar todas estas pequeñas cantidades (que el delegador debe recombinar).
* Tipo de lista de delegación:
  * Aceptar todo: acepte cualquier delegación con la tarifa mínima o más.
  * Permitir lista: solo acepta delegaciones de direcciones específicas. Use este modo si opera un Super Staker solo para direcciones específicas, como sus monedas.
  * Lista de exclusión: direcciones para excluir de ser aceptado para staking.

A continuacion, separemos los UTXOs a cantidades validas para enviar Stakes por el Super Staker. Los UTXO deben tener una cantidad mínima de 100 QTUM. En la página Super staker, seleccione el botón de monedas divididas (icono de tridente) y use los valores predeterminados o realice ajustes, pero no se utilizarán UTXOs inferiores a 100 QTUM para el staking.

![6  Split UTXOs GUI](https://user-images.githubusercontent.com/29760787/85331934-0a156800-b4a5-11ea-9339-eed51b9bddf6.jpg)

También puede dividir UTXO con el comando `splitutxosforaddress`, que también se puede usar para direcciones delegadas. Para dividir los UTXO entre un valor mínimo y máximo, ingrese el comando:

`splitutxosforaddress" dirección "minValue maxValue (maxOutputs)`

Por ejemplo, si una billetera contenía UTXO de 40, 50, 60, 70 y 800 QTUM, para dividirlos en UTXO de un mínimo de 100 y un máximo de 200 usaría el comando:

```splitutxosforaddress
{
  "txid": "197a199c3ac9dd8df574ca77da15c5da31db3f7101e2108638a3b2f94248b9f7",
  "selected": "1020.00",
  "splited": "1020.00"
}
```

Para este ejemplo, la entrada total fue de 1.020 QTUM, y la división fue de 9 UTXO de 100.0 y uno de 119.99566, la billetera envió una "transacción a sí mismo" y pagó una tarifa de 0.00434 QTUM.

Anteriormente, podía usar el comando `sendmanywithdupes` pero eso requería un formato significativo y operacionalmente querría enviarlo a una nueva dirección. Por supuesto, después de cualquiera de estos comandos, los UTXO deben madurar para 500 confirmaciones antes de que puedan usarse para staking.

# Lanzamiento de Qtum Core como Super Stacker

Los pasos anteriores muestran la transición de una billetera Qtum Core de instalación predeterminada a un Super Staker. La billetera también se puede lanzar inicialmente como un Super Staker para acortar los pasos. En este caso, la sincronización inicial de blockchain se acompaña de la construcción de la base de datos para el índice de direcciones y los eventos de registro (como se discutió anteriormente) para que la billetera esté lista para Super Staking.

La billetera Qtum Core puede iniciarse como un Super Staker con Qtum-Qt usando Configuración - Opciones - Principal - Habilite los pasos de superestabilización como se muestra arriba, o directamente a través de la línea de comando usando el parámetro `-superstaking = true` (testnet se muestra aquí) .

![7  Linux Launch](https://user-images.githubusercontent.com/29760787/85331947-0da8ef00-b4a5-11ea-961a-33fe19df19d9.png)

Este comando para el directorio predeterminado del programa en Windows sería:

`qtum-qt -testnet -superstaking=true`

![8  Windows Command Line Launch](https://user-images.githubusercontent.com/29760787/85331962-113c7600-b4a5-11ea-84e3-81e030c91ac5.jpg) 

Cuando la billetera se inicia y sincroniza la blockchain (creando índice de direcciones y eventos de registro), todo está listo para agregar Super Stakers. Configure un Super Staker y luego habilite el super staking en Configuración - Opciones - Principal - configure "Habilitar el super staking" y el Super Staker estará listo.

# Qtum Super Staker

Cualquier dirección en una billetera Qtum Core que se ejecute como Super Staker puede recibir direcciones delegadas y operar como un Super Staker individual. La billetera de escritorio GUI Qtum-Qt permite la configuración de múltiples direcciones de Super Staker con diferentes tarifas y tamaños mínimos UTXO. La billetera del demonio / servidor qtumd ejecuta todas sus direcciones de Super Staker con la misma tarifa y el tamaño mínimo UTXO. Si se necesita una variación en varias direcciones de Super Staker con qtumd, es posible configurarlas con la billetera Qtum-Qt y simplemente transferir el archivo wallet.dat a qtumd.

La siguiente configuración para qtumd muestra el uso de una sola dirección Super Staker.

Después de instalar qtumd, inicie con los siguientes parámetros (se muestra testnet):

`./qtumd -testnet -superstaking=true`

Se pueden agregar parámetros opcionales para cambiar la tarifa predeterminada (del 10%) y el valor mínimo de UTXO (de 100 QTUM), por ejemplo, como:

`-stakingminfee=12  -stakingminutxovalue=120`

Una vez que la billetera sincroniza la blockchain, obtenga una dirección para enviar algo de QTUM. Esta será la dirección de Super Staker. Usa el comando:

`./qtum-cli -testnet getnewaddress "legacy"`

Luego envíe 1,300 QTUM a esta dirección.

![9  Getnewaddress Getbalance](https://user-images.githubusercontent.com/29760787/85331969-13063980-b4a5-11ea-8ccc-280092131d18.png)

Este 1.300 QTUM llegará en un solo UTXO, que debe dividirse para la operación Super Staker. Utilice el comando `splitutxosforaddress` con el tamaño mínimo predeterminado de 100 y el tamaño máximo de 200:

`./qtum-cli -testnet splitutxosforaddress "qdMp2BNpwL6ZmMEQHfLV5wGNVgmPCuzd7d" 100 200`

![10  Split UTXOs for Address qtumd](https://user-images.githubusercontent.com/29760787/85331976-15689380-b4a5-11ea-91dd-187b6875f3b2.png)

La respuesta del comando muestra que se seleccionaron 1.300 QTUM para dividir, en este caso dividir en 12 UTXO que se pueden ver con el txid en el Explorador.

En este punto, la billetera qtumd está lista para la operación Super Staker con la dirección qdMp2BNpwL6ZmMEQHfLV5wGNVgmPCuzd7d, y las delegaciones se pueden monitorear usando el comando:

`getdelegationsforstaker "qdMp2BNpwL6ZmMEQHfLV5wGNVgmPCuzd7d"`

# Operaciones Super Stacker 

El Super Staker debe tener UTXO para comprometerse con las stakes para los UTXO delegados que está staking. El número de UTXO (de tamaño mínimo 100 QTUM) se basa en el peso delegado como un porcentaje del peso total de la red, y los buenos valores son 30 UTXO para el 1% del peso de la red, 50 UTXO para el 2.0%, 100 UTXO para el 5% y 160 UTXO para representar el 10% del peso total de la red.

Los Super Stakers deben controlar su peso de Wallet (peso UTXO menos la cantidad que está actualmente staking) y agregar UTXO si cae por debajo de varios miles.

Haga una copia de seguridad de la billetera (guarde el archivo wallet.dat) después de los cambios en la configuración de staking fuera de linea, como agregar un Super Staker o una delegación, porque la configuración de staking fuera de linea se guarda en el archivo wallet.dat. Si el archivo de copia de seguridad wallet.dat se pierde, la configuración también se puede restaurar con la recuperación como se muestra a continuación.

Las delegaciones a un Super Staker se pueden verificar usando el botón "Delegaciones ..." en la página de Super Staker o con el comando `getdelegationforstaker`.

# Restaurar

Normalmente, la configuración de delegación y Super Staker se almacena en el archivo wallet.dat. Si hay problemas con el archivo wallet.dat, la información de delegación y la información de super staker se pueden recuperar utilizando el botón Restaurar en las páginas de delegación y Super Staker. En este caso, la billetera volverá a escanear la memoria del contrato de "estado" para las transacciones de staking fuera de línea para las direcciones apropiadas.

![11  Restore super stakers](https://user-images.githubusercontent.com/29760787/85331982-18638400-b4a5-11ea-9f59-755b2ecd06a6.jpg)

***