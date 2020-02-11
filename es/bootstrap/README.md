# Cómo usar bootstrap.dat

## ¿Qué es bootstrap.dat?

`bootstrap.dat` es un archivo que contiene la copia de blockchain del bloque génesis a un cierto punto de tiempo. Este archivo comprimido `bootstrap.dat` se usa para acelerar los tiempos iniciales de descarga de blockchain. Su cliente de billetera descarga y verifica cada bloque de la red P2P. Esto suele ser lento y, especialmente, si está utilizando la billetera por primera vez, entonces el proceso de sincronización puede llevar bastante tiempo.

En lugar de utilizar la comunicación entre pares, su cliente de billetera puede leer datos de blockchain de este archivo de arranque comprimido que contiene la copia de datos de blockchain hasta una cierta altura de bloque. Una vez que el cliente de billetera completa la lectura de datos del archivo de arranque, utilizará la conexión P2P para descargar los bloques restantes. Este método es más rápido y además consume menos ancho de banda en comparación con el proceso de sincronización estándar. Sin embargo, el método de arranque todavía lleva algún tiempo, ya que su cliente de billetera necesita validar cada bloque individual.

## ¿Cómo generar bootstrap.dat?

Construya una mejor versión lineal, sin fork, de la blockchain Qtum. Los scripts se ejecutan con Python 3 pero son compatibles con Python 2.

### Paso 1: descargar archivos de script

Clone el repositorio oficial qtum e ingrese al directorio `contrib / linearize`

```
git clone https://github.com/qtumproject/qtum.git
cd qtum/contrib/linearize
```

### Paso 2: descargue la lista hash

```
./linearize-hashes.py linearize.cfg > hashlist.txt
```

Configuración de archivo de configuración requerida para linearize-hashes:

- RPC: `datadir` (obligatorio si no se especifican` rpcuser` y `rpcpassword`)
- RPC: `rpcuser`,` rpcpassword` (obligatorio si no se especifica `datadir`)

Configuración opcional del archivo de configuración para linearize-hashes:

- RPC: `host` (Default: `127.0.0.1`)
- RPC: `port` (Default: `3889`)
- Blockchain: `min_height`,` max_height`
- `rev_hash_bytes`: si es verdadero, la lista de hash de bloque escrita se revertirá en bytes. (En otras palabras, el hash devuelto por getblockhash tendrá sus bytes invertidos). Falso por defecto. Destinado a la generación de listas de hash independientes, pero seguro de usar con linearize-data.py, que generará los mismos datos sin importar qué formato de byte se elija.

El script `linearize-hashes` requiere una conexión, local o remota, a un servidor JSON-RPC. Ejecutar `qtumd` o` qtum-qt -server` será suficiente.

### Paso 3: copie los datos del bloque local

```
./linearize-data.py linearize.cfg
```

Configuración de archivo requerida:

- `output_file`: el archivo que contendrá la blockchain final. o
- `output`: Directorio de salida para la salida lineal de` blocks / blkNNNNN.dat`.

Configuración opcional del archivo de configuración para linealizar datos:

- `debug_output`: algunas impresiones pueden no ser siempre deseadas. Si es verdadero, se imprimirá dicha salida.
- `file_timestamp`: establece las horas de último acceso y última modificación de cada archivo, respectivamente, a la hora actual y a la marca de tiempo del bloque más reciente escrito en la blockchain del script.
- `génesis`: el hash del bloque génesis en la blockchain
- `input`: qtumd blocks / directorio que contiene blkNNNNN.dat
- `hashlist`: archivo de texto que contiene la lista de hashes de bloque creados por linearize-hashes.py.
- `max_out_sz`: Tamaño máximo para archivos creados por la opción` output_file`. (Predeterminado: `1000 * 1000 * 1000` bytes)
- `netmagic`: número mágico de la red.
- `out_of_order_cache_sz`: si se leen bloques fuera de orden, el bloque puede escribirse en un caché para que la blockchain no tenga que buscarse nuevamente. Esta opción especifica el tamaño del caché. (Predeterminado: `100 * 1000 * 1000` bytes)
- `rev_hash_bytes`: si es verdadero, la lista de hash de bloque escrita por linearize-hashes.py se invertirá en bytes cuando se lea por linearize-data.py. Vea la entrada linearize-hashes para más información.
- `split_timestamp`: divide los archivos de blockchain cuando se ve un nuevo mes por primera vez, además de alcanzar un tamaño máximo de archivo (` max_out_sz`).

## Cómo usar bootstrap.dat

1. Descargue el archivo `bootstrap.dat` de` https: // s.qtum.site / bootstrap.dat`.

2. Moverse

    

   ```
   bootstrap.dat
   ```

    

   en el directorio de datos qtum, las rutas predeterminadas de datadir son diferentes para diferentes sistemas operativos:

   - Linux: `~/.qtum`
   - OSX: `~/Library/Application Support/Qtum`
   - Windows: `% APPDATA% \ Qtum` (pegue esta ruta en su explorador de Windows, la ruta se resolverá automáticamente)

3. Reinicie la billetera y espere a reindexar.

[
](https://docs.qtum.site/en/Qtum-RPC-API/)