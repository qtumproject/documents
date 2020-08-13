**¡IMPORTANTE!**  Cuando use una billetera web como esta, asegúrese de estar 100% seguro de que está ingresando la URL correcta que es

[https://qtumwallet.org](https://qtumwallet.org/)

No se utiliza ninguna otra URL para la billetera web, asegúrese de verificar el candado verde con "Seguro" en el campo URL que valida el sitio:

![0. Secure site EN](https://i.imgur.com/yaCSQSu.jpg)

Bienvenido a la documentación del usuario de la billetera web Qtum que mostrará

- [Introducción a la billetera web](https://docs.qtum.site/en/QTUM-WebWallet-usage/#introduction-to-the-web-wallet)
- [Cómo generar una nueva billetera o restaurar direcciones de otras billeteras](https://docs.qtum.site/en/QTUM-WebWallet-usage/#generate-new-wallet---restore-wallet)
- [Cómo recibir y enviar monedas QTUM, envío con Ledger, envío seguro](https://docs.qtum.site/en/QTUM-WebWallet-usage/#receive-and-send-qtum-coins)
- [Cómo recibir y enviar tokens QRC20](https://docs.qtum.site/en/QTUM-WebWallet-usage/#send-and-receive-qrc20-tokens)
- [Cómo agregar un nuevo token QRC20 a la billetera](https://docs.qtum.site/en/QTUM-WebWallet-usage/#adding-a-qrc20-token)
- [Cómo publicar contratos inteligentes](https://docs.qtum.site/en/QTUM-WebWallet-usage/#how-to-publish-smart-contracts)

------

# Introducción a la billetera web

La billetera web Qtum se ejecuta en su navegador y se conecta a la red Qtum a través de una interfaz de nodo completo. La billetera web no almacena sus claves privadas, por lo que debe administrarlas con un archivo de claves descargado o palabras clave. Esto es completamente tu responsabilidad.

La billetera web se puede iniciar navegando al sitio mencionado anteriormente y haciendo clic en el botón ** `Web` **:

![A. Select Web Wallet EN](https://i.imgur.com/jE89N81.jpg)

Desplácese hacia abajo y haga clic en el botón azul grande `` Visitar sitio web` **:

![B. Select Visit Website EN](https://i.imgur.com/yNLtnZR.jpg)

Al cargar la billetera web, recibimos esta advertencia muy importante, tómese unos segundos y léala.

![Warning](https://i.imgur.com/ZGBb9u6.jpg)

¡Bienvenido a la billetera web Qtum! Como se muestra a continuación, el panel izquierdo ofrece un menú con varias opciones para crear o restaurar una billetera y otras acciones. La parte superior del menú ofrece siete opciones para crear o restaurar una billetera. La parte inferior del menú ofrece varias operaciones y opciones de configuración. La parte central de la página de billetera presenta formularios para la entrada de datos, visualización y administración de los activos de la billetera.

La opción de menú ** `Configuración` ** permitirá seleccionar el idioma y configurar la billetera para que funcione en Mainnet o Testnet. Seleccione la red deseada ** antes ** de restaurar una billetera o ingresar una contraseña.

La billetera web Qtum funciona con direcciones estándar Qtum que comienzan con una "Q" (heredada) y no es compatible con las direcciones SegWit (Segregated Witness) que comienzan con una "M" (p2sh-segwit) o "qc1" (bech32) .

------

# Generar una nueva billetera - Restaurar billetera

Hay 7 formas de generar o restaurar una billetera.

1. [Generar nueva billetera](https://docs.qtum.site/en/QTUM-WebWallet-usage/#1-generate-new-wallet) crea una nueva dirección y descarga un archivo de clave
2. [Crea desde Mnemonic](https://docs.qtum.site/en/QTUM-WebWallet-usage/#2-create-from-mnemonic) crea 12 palabras iniciales y una nueva dirección
3. [Restaurar desde Mnemonic](https://docs.qtum.site/en/QTUM-WebWallet-usage/#3-restore-from-mnemonic) restaura una dirección usando 12 palabras iniciales de una billetera de escritorio
4. [Restaurar desde WIF](https://docs.qtum.site/en/QTUM-WebWallet-usage/#4-restore-from-wif) restaura una dirección desde una clave privada
5. [Restaurar desde la billetera móvil](https://docs.qtum.site/en/QTUM-WebWallet-usage/#5-restore-from-mobile-wallet) restaura una dirección de 12 palabras iniciales desde una billetera móvil compatible
6. [Restaurar desde archivo de clave](https://docs.qtum.site/en/QTUM-WebWallet-usage/#6-restore-from-key-file) restaura una dirección de un archivo de clave creado por la billetera web
7. [Restaurar desde Ledger](https://docs.qtum.site/en/QTUM-WebWallet-usage/#7-restore-from-ledger) utiliza una billetera de hardware Ledger para firmar y verificar transacciones

![2. Generate New Wallet](https://i.imgur.com/5LdWl0r.jpg)

### 1. Generar una nueva billetera

Ahora elija la primera opción en la pantalla del menú de arriba y haga clic en el botón rojo ** `GENERATE NEW WALLET` **. A continuación, ingresará una contraseña que se utilizará para crear una serie de claves privadas. Escriba una nueva contraseña larga y segura, ingrese la contraseña y haga clic en el botón azul ** `CONFIRMAR` **:

![3. Enter Password](https://i.imgur.com/6cFzE2p.jpg)

Luego haga clic en el botón verde grande para descargar el archivo de clave:

![4. Download Key File](https://i.imgur.com/MPlJCXK.jpg)

El archivo de claves se descargará en su computadora, guardará el archivo en una ubicación que pueda encontrar nuevamente y haga una copia de respaldo del archivo sin conexión. El nombre del archivo de clave tendrá un formato como "1529379436736.txt" donde el número largo es el tiempo de creación del archivo como tiempo de época Unix en milisegundos. Necesitará este archivo de clave y la contraseña para volver a cargar la billetera. Si pierde el archivo de clave o la contraseña, se perderán los fondos en su billetera.

La página * Ver información de la billetera * aparecerá para su billetera donde podrá ver:

1. Dirección: dirección de recepción de la billetera
2. Saldo - monedas confirmadas
3. Saldo no confirmado: monedas que esperan ser confirmadas en el siguiente bloque
4. Clave privada: la clave privada para esta dirección

![5. View Wallet Info](https://i.imgur.com/nW88f0h.jpg)

### 2. Crea desde Mnemonic

Haga clic en la opción de menú ** `Crear desde Mnemonic` **, **` GENERAR NUEVA CARTERA` **, ingrese una contraseña y haga clic en ** `CONFIRMAR ** **. La billetera creará una nueva dirección a partir de 12 palabras iniciales aleatorias:

![6. Generate Seed Words](https://i.imgur.com/ioGSwbq.jpg)

Anote y guarde estas palabras iniciales, solo usted, como usuario de la billetera, tiene acceso a estas palabras iniciales (las palabras iniciales y las claves privadas no se almacenan en el servidor, si pierde estas palabras iniciales perderá el acceso a sus fondos. )

A continuación, debe ingresar las palabras iniciales manualmente para confirmar que las ha guardado. Haga clic en el botón azul ** `HE RECORDADO TODO. COMPROBEMOS` **, ingrese su contraseña, vuelva a ingresar las palabras clave y haga clic en el botón verde ** `CONFIRM` **:

![7. Confirm Seed Words](https://i.imgur.com/1ClZwHq.jpg)

Luego verá la página * Ver información de billetera * como se muestra arriba. Es posible que desee descargar un archivo de clave para la billetera utilizando la opción de menú ** `Depositar como archivo de clave` ** que le dará otra forma de restaurar la billetera como se describe en el paso 6 a continuación.

### 3. Restaurar desde Mnemonic

Para la opción de menú ** `Restaurar desde Mnemonic` ** ingresará las palabras semilla guardadas en el paso 2 anterior. Asegúrese de ingresar las palabras iniciales correctamente (sin errores tipográficos o espacios en blanco adicionales), haga clic en el botón verde ** `CONFIRMAR` **:

![8. Enter Seed Words](https://i.imgur.com/DAU5res.jpg)

Después de ingresar una nueva contraseña, verá la página * Ver información de billetera *. Verifique que se haya creado la dirección esperada. Es posible que desee hacer una copia de seguridad de la billetera utilizando la opción de menú ** `Deposite como archivo clave` **.

### 4. Restaurar desde WIF

Esta opción permite restaurar la billetera desde una clave privada de formato de entrada de billetera (WIF) como la billetera web, la billetera Qtum Core o la billetera Qtum Electrum. Una clave privada WIF tendrá una longitud de 52 caracteres y tendrá una comprobación y codificación de errores (para reducir el tamaño) en comparación con una clave privada original, que tendrá 64 caracteres hexadecimales.

Copie la clave privada WIF de otra billetera. Seleccione la opción de menú ** `Restaurar desde WIF` **, pegue la clave privada en el campo * WIF * y haga clic en el botón verde **` CONFIRM` **:

![9. Restore from WIF](https://i.imgur.com/UxnrajH.jpg)

Se mostrará la página * Ver información de billetera *. Verifique que restauró la dirección esperada. Es posible que desee hacer una copia de seguridad de la billetera utilizando la opción de menú ** `Deposite como archivo clave` **.

### 5. Restaurar desde la billetera móvil

Restaurar desde Mobile Wallet permite restaurar una dirección de billetera desde una billetera móvil compatible, como la billetera móvil Qtum, la billetera Qbao o la billetera Qtum Electrum (si la billetera Qtum Electrum se inicializó para ser compatible con las billeteras móviles Qtum).

Seleccione la opción de menú ** `Restaurar desde billetera móvil` ** e ingrese las 12 palabras iniciales de su otra billetera. Ingrese las palabras cuidadosamente en minúsculas (nunca en MAYÚSCULAS) y asegúrese de que no haya espacios en blanco después de las palabras, y haga clic en el botón verde ** `CONFIRMAR` **:

![10. Restore from Mobile Wallet EN](https://i.imgur.com/4BS3jFi.jpg)

Luego, elija la dirección para restaurar, probablemente será la fila de direcciones superior a menos que esté usando varias direcciones en su dispositivo móvil. Si no ve la dirección correcta, vuelva a ingresar las palabras de inicio con cuidado. Haga clic en el botón verde ** `ELEGIR` ** para la dirección deseada:

![11. Choose Address EN](https://i.imgur.com/tUo4mGY.jpg)

Se mostrará la página * Ver información de billetera *. Es posible que desee hacer una copia de seguridad de la billetera utilizando la opción de menú ** `Deposite como archivo clave` **.

### 6. Restaurar desde archivo de clave

Seleccione la opción de menú ** `Restaurar desde archivo de clave` **, **` CARGAR` **, seleccione el archivo de clave para cargar y haga clic en ** `Abrir` **. Ingrese su contraseña y haga clic en el botón azul ** `CONFIRMAR` **. Se mostrará la página * Ver información de billetera *.

![12. Restore from Key File EN](https://i.imgur.com/xcaPvzh.jpg)

### 7. Restaurar desde Ledger

Para usar su Ledger Nano S o Ledger Blue con Qtum, primero deberá ejecutar el Ledger Manager e instalar la aplicación Qtum en su Ledger siguiendo estas instrucciones: https://support.ledgerwallet.com/hc/en-us/articles / 115003776913-Install-and-use-Qtum-QTUM- '

![13. Qtum App EN](https://i.imgur.com/th4IymV.jpg)

En la billetera web, seleccione la opción de menú ** `Restaurar desde Ledger` **, conecte su Ledger, y en el Ledger ingrese el código PIN y abra la aplicación Qtum, luego en la página de la billetera web * Restaurar desde Ledger * haga clic en el rojo ** Botón `CONNECT` **:

![14. Restore from Ledger EN](https://i.imgur.com/1wSYpgR.jpg)

En la siguiente página * Restaurar desde el libro mayor *, haga clic en el icono del candado verde para seleccionar la ruta predeterminada:

![15. Choose Path Default EN](https://i.imgur.com/3IErrFG.jpg)

En la página * Ruta predeterminada m / 44 '/ 88' / 0 '/ 0 *, elija la dirección que desea usar haciendo clic en el icono del candado verde en esa fila. Esta será probablemente la fila superior a menos que haya elegido otras direcciones en la billetera Ledger Live.

![16. Choose Address EN](https://i.imgur.com/2M4XSCb.jpg)

Se mostrará la página * Ver información de billetera *. Tenga en cuenta que al usar el Ledger no existe la opción de ver o copiar la clave privada porque la billetera de hardware del Ledger administra las claves privadas y no las envía a su computadora. La opción ** `Restaurar desde el libro mayor` ** no está disponible para Testnet.

![17. View Wallet Info EN](https://i.imgur.com/LiJRR7C.jpg)

Puede enviar tokens QRC20 a una dirección administrada por la billetera Ledger, como Ledger Live, pero la billetera Ledger actualmente no permite (noviembre de 2018) mostrar o administrar tokens QRC20. Puede usar ** `Restaurar desde Ledger` ** con la billetera web para mostrar y administrar los tokens QRC20 que se encuentran en su dirección de Ledger, en cuyo caso la página * Ver información de la billetera * mostrará estos tokens:

![18. View Wallet Info QRC20 EN](https://i.imgur.com/PFktEEy.jpg)

------

# Reciba y envíe monedas QTUM

### Recibir

Puede recibir monedas para la billetera web enviándolas a la dirección de la billetera. Antes de enviar monedas a la billetera, asegúrese de poder cerrar y volver a abrir la billetera con la misma dirección de recepción. Usar la opción de menú ** `Deposite como archivo de clave` ** y **` Restaurar desde archivo de clave` ** es una forma segura de hacerlo. Usar la opción de menú para restaurar desde palabras iniciales para volver a abrir la billetera es más riesgoso porque ingresar un error tipográfico para las palabras iniciales o la contraseña creará una dirección aleatoria inesperada.

En la página * Ver información de la billetera *, haga clic en el botón azul de la dirección ** `COPIA` ** y luego pegue esta dirección como la dirección de recepción en la billetera o cuenta de envío, y luego envíe las monedas. Espere unos minutos para que se publique el siguiente bloque y vuelva a cargar la billetera web para ver el nuevo saldo. También puede hacer clic en la opción de menú ** `Ver Wallet Txs` ** para ver la transacción de recepción:

![19. View Wallet Txs EN](https://i.imgur.com/xjIFSvx.jpg)

### Enviar

Desde su billetera o cuenta receptora, copie la dirección receptora. En el menú de la billetera web, haga clic en ** `Enviar` ** y pegue la dirección de recepción en el campo * Dirección **, luego ingrese la cantidad a enviar en el campo * Cantidad ** (si está enviando una cantidad menor a 1.0 , use un cero a la izquierda, como "0.5", no ".5"). Puede dejar el campo * Tarifa * configurado por defecto en 0.01 (o establecer una tarifa más baja si entiende cómo hacerlo) y hacer clic en el botón verde ** `CONFIRMAR` **:

![20. Send tokens EN](https://i.imgur.com/GpzinKD.jpg)

Aparecerá la página * Ingrese la dirección nuevamente (Verificación doble) *. Copie y pegue la dirección de recepción en el campo * Dirección * y haga clic en el botón azul ** `CONFIRMAR` **:

![21. Please enter address again... EN](https://i.imgur.com/db4zBHD.jpg)

Se mostrará la página * que va a enviar *, después de verificar la información, haga clic en el botón azul ** `CONFIRMAR` **:

![22. You are going to send... EN](https://i.imgur.com/v3zoaka.jpg)

En la parte inferior de la pantalla, verá la barra de confirmación verde con un enlace para mostrar la transacción en el Explorador:

![23. Successful send EN](https://i.imgur.com/fqqIIce.jpg)

La página * Ver información de la billetera * mostrará un * Saldo no confirmado * por el monto que se envía (+ tarifa). Después de que la transacción se publique en el siguiente bloque, puede volver a cargar la billetera para ver el saldo actualizado y también ver la transacción utilizando la opción de menú ** `Ver Txs de billetera` **

### Envío con Ledger

Enviar cuando la billetera ha sido restaurada desde Ledger tiene unos pocos pasos más.

Desde su billetera o cuenta receptora, copie la dirección receptora. En el menú de la billetera web, haga clic en ** `Enviar` ** y pegue la dirección de recepción en el campo * Dirección **, luego ingrese la cantidad a enviar en el campo * Cantidad **. Puede dejar el campo * Tarifa ** establecido en el valor predeterminado de 0.01 (o establecer una tarifa más baja si comprende cómo hacerlo) y hacer clic en el botón verde ** `CONFIRMAR` **:

![L1 Send Tokens](https://i.imgur.com/T7mIXiL.jpg)

Aparecerá la página * Ingrese la dirección nuevamente (Verificación doble) *. Copie y pegue la dirección de recepción en el campo * Dirección * y haga clic en el botón azul ** `CONFIRMAR` **:

![L2 Address again](https://i.imgur.com/qCeSZHH.jpg)

Verá el * que va a enviar ... Confirme tx en su pagina Ledger:

![L3 You are going to send](https://i.imgur.com/CbqxuWc.jpg)

Siempre que haya conectado la billetera de hardware Ledger, ingrese el código PIN y seleccione la aplicación Qtum, en la pantalla Ledger verá detalles de desplazamiento de la transacción para que pueda confirmar la dirección y la cantidad:

![L4 Address and amount](https://i.imgur.com/K8aYMas.jpg)

En el Libro mayor, presione el botón derecho sobre la marca de verificación en la pantalla para confirmar la salida # 1, que es la transacción principal, en este caso enviando 2.0 QTUM. También deberá presionar este botón nuevamente para confirmar la salida # 2, que está enviando el cambio nuevamente a su billetera, y presionar el botón por tercera vez para confirmar la transacción general:

![L5 Confirm output 1](https://i.imgur.com/3KDySJ0.jpg)

Ahora en la billetera web, verá la transacción sin procesar en la página * que va a enviar *. Después de verificar la información, haga clic en el botón azul ** `CONFIRMAR` **:

![L6 You are going to send raw transaction](https://i.imgur.com/ugFkTS4.jpg)

En la parte inferior de la pantalla, verá la barra de confirmación verde con un enlace para mostrar la transacción en el Explorador:

![L7 Successful send](https://i.imgur.com/fMas7Ld.jpg)

La página * Ver información de billetera * mostrará un * Saldo no confirmado * por el monto que se envía (+ tarifa). Después de que la transacción se publique en el siguiente bloque, puede volver a cargar la billetera para ver el saldo actualizado y también ver la transacción utilizando la opción de menú ** `Ver Txs de billetera` **

### Envío seguro

Una transacción básica de Qtum se compone de tres pasos:

1. Componga la transacción base: desde, hasta, monto, tarifa.
2. Firme la transacción con la clave privada.
3. Transmita la transacción firmada a la red.

"Envío seguro" aísla estos pasos entre dos computadoras / billeteras, donde el paso 2 se realiza con una billetera fuera de línea cuyas claves privadas nunca están expuestas a Internet. La billetera web "Envío seguro" recorre estos 3 pasos para hacer una transacción muy segura usando la billetera fuera de línea.

#### Configurar billetera sin conexión

Para un envío seguro, primero configure la billetera fuera de línea obteniendo una copia de la billetera web y el software del navegador. Este ejemplo utilizará Google Chrome en Windows, y puede ajustarlo a su navegador y sistema operativo preferido.

En la computadora en línea, usando el navegador Chrome, vaya a [https://qtumwallet.org] (https://qtumwallet.org/). En la esquina superior derecha del navegador, seleccione los tres puntos verticales para el menú, seleccione ** `Más herramientas` ** y luego **` Guardar página como ... `** para guardar el archivo HTML de Qtum Web Wallet. Este archivo contiene todo el código JavaScript para ejecutar la billetera web:

![1 The Web Wallet HTML File](https://i.imgur.com/ZdCBdhu.jpg) El archivo HTML de Web Wallet

Para hacer una copia sin conexión de Chrome, navegue para encontrar la carpeta de instalación de Chrome en su computadora. Para Windows, generalmente se encuentra en Archivos de programa (x86) - Google:

![2019-42 Chrome Folder](https://i.imgur.com/us44CuH.png) Copiar carpeta de Chrome

Copie la carpeta Chrome y el archivo HTML de Web Wallet en una memoria USB y luego cópielos en la computadora fuera de línea.

Esto proporciona una copia del actual Chrome y la billetera web para la computadora fuera de línea, y no recibirá actualizaciones de versiones futuras. Puede realizar una actualización con estos mismos pasos, pero no debería ser necesario para estas operaciones básicas.

#### Inicie la billetera en modo sin conexión

En la computadora sin conexión, inicie el navegador Chrome: en la carpeta Chrome copiada, seleccione Datos de usuario - Aplicación - Chrome.exe:

![2019-43 Select Chrome.exe](https://i.imgur.com/vZ4oSZ1.jpg) (aquí en una carpeta llamada "billetera sin conexión")

#### Inicie la billetera web sin conexión

Con el cursor en la barra de direcciones URL de Chrome, presione Control - "O" (para Abrir) y luego navegue y abra el archivo Qtum Web Wallet.html:

![2019-44 Open Qtum Web Wallet.html](https://i.imgur.com/EyE4B1x.jpg)

Usando el menú de la billetera web, seleccione Configuración y en el menú desplegable  seleccione ** `Fuera de línea` ** y **` CONFIRMAR ** **:

![2019-45 Set Offine Mode](https://i.imgur.com/JLAvVTO.jpg)

Tenga en cuenta el encabezado dorado de la billetera en modo fuera de línea. Desde este punto, puede generar una nueva billetera y guardar (y hacer una copia de seguridad) el archivo de clave. El menú mostrará * Solicitar pago * y la página * Solicitar pago * mostrará la dirección de recepción de la billetera fuera de línea:

![2019-46 Request Payment page](https://i.imgur.com/ova1s8W.jpg)

Copie la dirección de recepción en un archivo de texto y cópiela en la memoria USB para transferirla a la computadora en línea. Ahora puede enviar QTUM a esta dirección para financiar la billetera fuera de línea.

Esto funciona para enviar QTUM a la dirección de la billetera fuera de línea porque las monedas QTUM en realidad se almacenan como transacciones no gastadas en la blockchain (nunca se almacenan monedas en ninguna billetera). Sin embargo, la billetera fuera de línea contiene la clave privada para su dirección, y solo la billetera fuera de línea puede firmar transacciones para enviar QTUM desde su dirección.

Ahora podemos usar los 3 pasos de transacción para un envío seguro.

1. Componer la transaccion base con la billetera online

En el menú de la billetera en línea, seleccione ** `Envío seguro` ** y para el paso 1 complete las direcciones y la cantidad. * From Address ** es la dirección de la billetera desconectada. La billetera en línea consultará a la blockchain para la "Dirección de origen" y seleccionará una transacción o transacciones anteriores que tengan QTUM suficiente para la cantidad que se envía. Use 0.01 para la tarifa a menos que sepa cómo elegir tarifas más bajas.

Después de completar todos los campos, presione ** `CONFIRM` **, vuelva a ingresar la * A la dirección **, presione **` CONFIRM` ** y ** `CONFIRM` ** nuevamente para crear el archivo de transacción sin procesar:

![2019-47 Step 1 Safe Send page](https://i.imgur.com/5Z24gc5.jpg) Paso 1: creación de la transacción sin procesar

La billetera en línea creará un archivo de texto de transacción sin procesar, por ejemplo:

```
{"from":"","to":"","amount":"5.0","fee":"0.01", "utxo":[{"address":"","txid":"","confirmations":4, "isStake":false,"amount":10,"value":1000000000,"hash":"","pos":0}]}
```

Aquí la billetera en línea ha seleccionado una transacción no gastada apropiada propiedad de la "Dirección de origen" que tiene 10.0 QTUM.

Debe dejar la billetera en línea ejecutándose al final del paso 1 mientras completa el paso 2 con la computadora desconectada, luego regrese para el paso 3. Salir de la billetera en línea en este punto y volver a cargar para el paso 3 cancelará la secuencia.

Copie el archivo de transacción sin procesar en la computadora desconectada. Para la billetera desconectada, inicie Chrome y la billetera en modo desconectada como en "Iniciar la billetera desconectada" arriba. Use la opción de menú ** `Restaurar desde archivo de clave` ** para cargar la dirección anterior. La billetera desconectada no sabrá ni mostrará ningún saldo.

1. En el menú de la billetera desconectada, seleccione ** `Envío seguro` ** y en la página * Envío seguro * en el paso 1, presione **` NEXT` ** para comenzar el paso 2.

En el paso 2, seleccione ** `CARGAR` ** y abra el archivo de transacción sin procesar copiado de la billetera en línea. Verá los campos de transacción tal como se ingresaron en la computadora en línea. Seleccione ** `CONFIRM` **, vuelva a ingresar * To Address ** y **` CONFIRM` **, y luego ** `CONFIRM` ** nuevamente para crear el archivo tx firmado:

![2019-48 Step 2](https://i.imgur.com/90qZsLa.jpg) Paso 2: firme el archivo de transacción sin procesar para crear el archivo tx (transmisión)

La billetera desconectada generará un archivo tx firmado, por ejemplo:

```
{"from":"","to":"","amount":"5.0", "fee":"0.01","rawTx":""}
```

Copie este archivo en una memoria USB y transfiéralo a la computadora billetera en línea.

Tenga en cuenta que la billetera fuera de línea está completamente desconectada de Internet y solo puede firmar la transacción con sus claves privadas. La billetera sin conexión ni siquiera puede mostrar el saldo de su dirección, pero puede ver el saldo con el Explorador.

1. De vuelta en la billetera en línea (todavía en la página * Envío seguro *) en el paso 2, seleccione ** `NEXT` ** para avanzar al paso 3.

En el paso 3, seleccione ** `CARGAR` ** y abra el archivo tx firmado. Verá los campos de transacción tal como se ingresaron en el paso 1. Presione ** `CONFIRM` **, vuelva a ingresar la dirección * Enviar a ** y seleccione **` CONFIRM` **, y ** `CONFIRM` ** nuevamente para enviar la transacción a la red:

![2019-49 Step 3](https://i.imgur.com/w9eCAo8.jpg) Paso 3: envíe el archivo tx a la red para completar la transacción

En la parte inferior de la pantalla, verá la barra de confirmación verde, y después de que la transacción se publique en el siguiente bloque, seleccione el enlace Explorador para ver la transacción en la blockchain.

------

# Enviar y recibir tokens QRC20

Si no ha hecho esto, asegúrese de que puede hacer una copia de seguridad de la billetera usando la opción de menú ** `Deposite como archivo de clave` **, y luego vuelva a abrir en la misma dirección usando **` Restaurar desde archivo de clave` **.

### Reciba tokens QRC20

Para recibir tokens QRC20, en la billetera web * Vea la página de Información de billetera * y copie el campo * Dirección * haciendo clic en el botón azul ** `COPIAR` **, pegue esta dirección en la billetera o el intercambio de envío y envíe los tokens. Después de que se publique el siguiente bloque, vuelva a cargar la billetera para ver los tokens:

![24. Receive QRC20 Tokens EN](https://i.imgur.com/pozYh4S.jpg)

### Enviar tokens QRC20

Para enviar tokens QRC20 debe tener suficientes monedas QTUM en la dirección vinculada a ese token. La tarifa predeterminada de la billetera web para enviar tokens es 0.00000040 precio del gas x 250,000 gas = 0.1 QTUM más la tarifa de transacción predeterminada de 0.01 QTUM, para una tarifa total de 0.11 QTUM. Puede usar estos valores predeterminados a menos que comprenda cómo establecer valores más bajos, pero no se preocupe, cualquier exceso de gas se reembolsará como una cantidad extraída (la cantidad extraída debe madurar durante 500 bloques antes de que pueda enviarse o usarse para gas / matrícula).

![25. Send QRC20 Token EN](https://i.imgur.com/ttRyUqK.jpg)

------

# Agregar un token QRC20

La billetera web tendrá capacidad incorporada para tokens QRC20 populares, y puede agregar tokens adicionales ingresando la información del contrato inteligente del token. Por ejemplo, si desea agregar el token XYZ, busque ese token en el Explorador qtum.info, copie el campo contrato * Dirección Hash *:

![26. Copy Address Hash EN](https://i.imgur.com/fW00puB.jpg)

En la billetera web, seleccione la opción de menú ** `Enviar` **, haga clic en el menú desplegable junto a" QTUM ", desplácese hasta la parte inferior de la lista Moneda / Token y haga clic en el botón **` Más ... `** :

![27. Add QRC20 Token EN](https://i.imgur.com/PSCBSjP.jpg)

Pegue el hash de dirección copiado del Explorador en el campo * Dirección del contrato de token * y haga clic en el botón azul ** `BUSCAR` **:

![28. Enter Address Hash EN](https://i.imgur.com/i8vYHE4.jpg)

Los detalles del contrato deben mostrarse en la página * Token *, verificar y hacer clic en el botón ** `CONFIRM` ** para agregar este token a su billetera. El nuevo token estará disponible en la billetera durante 30 días, después de lo cual puede agregarlo nuevamente si es necesario.

------

# Cómo publicar contratos inteligentes

La billetera tiene la capacidad de publicar contratos inteligentes creando tokens QRC20 con ** `Create Token` ** o cualquier otro contrato que use **` Create Contract` **.

### Crear token

La opción de menú ** `Crear token` ** ofrece una manera fácil de crear tokens QRC-20 utilizando una transacción de creación de contrato incorporada.

Seleccione ** `Crear token` ** en el menú y complete el formulario * Crear token *:

![2019-10 Create Token](https://i.imgur.com/KYOgnEd.jpg)

Para * Nombre del token * ingrese un nombre descriptivo, aquí "Mi token de prueba". Para * Símbolo de token * ingrese un símbolo apropiado. Los símbolos no son únicos, puede reutilizar cualquier nombre de símbolo existente o crear uno nuevo.

Deje * Decimales * establecido en el 8 recomendado a menos que tenga una buena razón para cambiar. Con 8 decimales, las fichas se crearán en Satoshis, donde la cantidad de 1.0 estará representada por 100,000,000 en el contrato inteligente (mueva el punto decimal 8 lugares a la izquierda para convertir Satoshis a unidades).

Ingrese el * Suministro total * de tokens para crear, 100 millones es un número típico.

Deje el * Precio de la gasolina *, el * Límite de gasolina * y la * Tarifa * configurados como están, a menos que comprenda cómo hacer cambios. Si * Límite de gas * se establece demasiado bajo, la transacción de creación del contrato se quedará sin gas y fallará. Para la configuración predeterminada, la tarifa total para el contrato de creación de tokens será de 2,500,000 x 0.00000040 + 0.01 = 1.01 QTUM, por lo que la billetera debe tener al menos esta cantidad y se reembolsará el exceso de gas.

Presione el botón verde ** `CONFIRM` **. En la pantalla * ¿Confirmas para crear este Token *, revisa la transacción sin procesar y presiona el botón azul ** `CONFIRMAR` **.

![2019-11 Do you confirm to create this token](https://i.imgur.com/UvD5aVc.jpg)

Verá la barra verde * Envío exitoso * en la parte inferior de la pantalla:

![2019-12 Send Successful bar](https://i.imgur.com/ZbXEaF4.jpg)

Siga el enlace para ver la transacción de creación de contrato en la blockchain (después de que se publique el siguiente bloque).

Tenga en cuenta que los contratos se referencian utilizando su hash de dirección, que es una dirección hexadecimal de 40 caracteres y solo otra forma de representar una dirección Qtum "Q".

Desde este punto, puede agregar el nuevo token a su billetera como se muestra arriba [Agregar un token QRC20] (https://github.com/qtumproject/documents/tree/master/en/QTUM-WebWallet-usage#adding-a -qrc20-token).

### Crear contrato

** `Crear contrato` ** permite la publicación de cualquier tipo de contrato inteligente. Para crear el contrato, comience escribiendo el código de Solidity y compílelo a bytecode usando un IDE web (Entorno de desarrollo integrado) como [qmix] (https://qmix.blockchainspaceman.com/) o [remix] (http: // remix. ethereum.org/) o una herramienta de línea de comando como [solar] (https://github.com/qtumproject/solar).

Aquí hay un ejemplo usando el sitio web remix en [http://remix.ethereum.org] (http://remix.ethereum.org/) para un contrato que rastrea el nombre y la edad:

```
pragma solidity >= 0.5.1 < 0.6.0;   // use only these versions of Solidity

contract NameAndAge{

    string private name = "null";
    uint256 private yearsAge = 0;

    // set the age - transaction, requires gas
    function setAge(uint256 newAge) public {
        yearsAge = newAge;
    }

    // set the name - transaction, requires gas
    function setName(string memory newName) public {
        name = newName;
    }

    // get the age - not a transaction, no gas required 
    function getAge() public view returns (uint256) {
        return yearsAge;
    }

    // get the name - not a transaction, no gas required
    function getName() public view returns (string memory) {
        return name;
    }
}
```

Para ingresar este contrato en la billetera, el código fuente debe compilarse en bytecode y crearse el ABI (Application Binary Interface).

Copie y pegue el código de Solidity en * remix * y presione el botón ** `Bytecode` ** para copiar el bytecode en el portapapeles, luego guarde los resultados en un archivo de texto.

![2019-13 remix](https://i.imgur.com/6Db8Xay.png)

El bytecode real (delineado en rojo a continuación) comienza con "6080" y tiene una longitud de aproximadamente 1.200 bytes.

![2019-14 bytecode](https://i.imgur.com/61fwWHg.jpg)

Además, presione el botón ** `ABI` ** para copiar el texto ABI en el portapapeles y guardar en el mismo archivo de texto con el código de bytes.

Ahora podemos publicar el contrato. En el menú de la billetera web, seleccione ** `Crear contrato` **, copie y pegue el código de bytes (la cadena hexadecimal dada por" objeto "como se muestra arriba) en el campo * Código de bytes *. Deje los campos * Precio de gas *, * Límite de gas * y * Tarifa * configurados como predeterminados a menos que comprenda cómo cambiarlos. La configuración predeterminada dará una tarifa de 2,500,000 x 0.0000004 + 0.01 = 1.01 QTUM. Su billetera necesitará al menos esta cantidad de QTUM para publicar el contrato. Presione el botón verde ** `CONFIRM` ** para continuar:

![2019-15 Create Contract](https://i.imgur.com/dJAyKga.jpg)

En la página siguiente * ¿Confirma publicar este contrato? * Revise la transacción sin procesar y presione el botón azul ** `CONFIRMAR` **:

![2019-16 Do you confirm to publish this contract](https://i.imgur.com/nayWRoW.jpg)

Vea la barra verde * Envío exitoso * en la parte inferior de la pantalla. Puede seguir el enlace para ver la transacción de creación de contrato en el Explorador (después de que se publique el siguiente bloque).

![2019-17 Successful send](https://i.imgur.com/Ao1Dfek.jpg)

Desde la transacción de creación del contrato en el Explorador, copie la * Dirección del contrato * (40 caracteres hexadecimales) para usar en los siguientes pasos:

![2019-18 Contract Address](https://i.imgur.com/Gpuc61C.jpg)

### Enviar a contrato

** `Enviar al contrato` ** se usa para cambiar los valores de memoria del contrato, por ejemplo, transfiriendo tokens o cambiando el almacenamiento de variables en la base de datos de estado del contrato. La transacción de envío a contrato requiere una tarifa y pago de gas, por lo que necesitará suficiente QTUM en la billetera. Continuando con el ejemplo anterior, lo enviaremos al contrato para establecer el nombre y la edad.

En el menú, presione ** `Enviar al contrato` **. En la página * Enviar al contrato *, copie y pegue la * Dirección del contrato * y el * ABI * en sus campos (el ABI para este contrato es de aproximadamente 60 líneas de texto, las pocas líneas inferiores son visibles en la ventana de desplazamiento a continuación).

En la fila * Método * (no se muestra a continuación), haga clic en la flecha desplegable y seleccione el método * setName *, y en el campo * newName * ingrese el nombre para establecer, aquí "Nakamoto". Presione el botón verde ** `CONFIRM` ** para continuar.

![2019-19 Send to Contract](https://i.imgur.com/S0QDtdR.jpg)

En la siguiente página * ¿Confirma? * Revise la transacción sin procesar y presione el botón azul ** `CONFIRMAR` ** para enviar la transacción:

![2019-20 Do you confirm](https://i.imgur.com/izdC8ci.jpg)

Vea la barra verde * Envío exitoso *, y puede seguir el enlace al Explorador para ver la transacción (después de que se publique el siguiente bloque).

Utilice los mismos pasos ** `Enviar al contrato` ** para seleccionar el método * setAge *, ingrese un * newAge * de 25 y envíe la transacción.

### Llamada de contrato

Al llamar al contrato, se leen las variables de estado en la copia local de la blockchain (en la base de datos de Qtum State) para el nodo del servidor de la billetera web (sin la necesidad de una transacción con gas) y se obtiene un resultado inmediato ya que no hay necesidad de esperar siguiente bloque para publicar. Para llamadas de contrato, ingrese la dirección del contrato y la interfaz ABI.

En el menú de la billetera web, seleccione ** `Contrato de llamada` **. En la página * Contrato * pegue la dirección del contrato y ABI. En la fila * Método * (no se muestra a continuación) presione la flecha desplegable y seleccione el método * getName *. Tenga en cuenta que no hay campos para el gas o las tarifas, ya que ninguno es obligatorio. Presione el ** botón verde CONFIRMAR **:

![2019-21 Call Contract](https://i.imgur.com/2aAR0QL.jpg)

El resultado volverá de inmediato:

![2019-22 Result for getName](https://i.imgur.com/WlT49Bb.jpg)

Los datos del contrato están en hexadecimal, la conversión de "4e616b616d6f746f" hexadecimal a ASCII da "Nakamoto" como se establece anteriormente.

Usando los mismos pasos de ** `Contrato de llamada` ** para seleccionar * getAge * se devolverá:

![2019-23 Result for getAge](https://i.imgur.com/goLbJfH.jpg)

La conversión de hexadecimal 19 a decimal da 25 como se establece anteriormente.

[
](https://docs.qtum.site/en/How-to-use-Qtum-Android-Wallet/)