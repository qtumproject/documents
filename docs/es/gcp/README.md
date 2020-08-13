# Cómo implementar Qtum en el marketplace de Google Cloud

Primero, busque "Qtum-Core" o "Qtum" en Google Cloud Marketplace. Una vez que lo encuentre, haga clic en "Iniciar en Compute Engine"

![1](https://docs.qtum.site/en/gcpgettingstarted/1.png)

### Implementar Qtum Compute Engine

Qtum no está demasiado hambriento de recursos, por lo que debería poder implementar una VM con solo 1 gb de ram y funcionará bien. Siempre se recomienda agregar SWAP para garantizar una mayor estabilidad.

Al momento de escribir, la blockchain Qtum pesa 4.4GB, elija al menos 8GB para su disco.

![2](https://docs.qtum.site/en/gcpgettingstarted/2.png)

### El servidor de Qtum en Google Cloud ha sido desplegado

Ahora nuestro motor de cómputo se ha implementado y se puede acceder a través de ** ssh **.

![4](https://docs.qtum.site/en/gcpgettingstarted/4.png)

![6](https://docs.qtum.site/en/gcpgettingstarted/6.png)

Todas las herramientas están disponibles y listas para usar en el primer arranque. Puede configurar permisos de acuerdo a sus necesidades.

![8](https://docs.qtum.site/en/gcpgettingstarted/8.png)

### Accediendo a Qmix

Qmix se inicia automáticamente en el arranque, para acceder a él, debe ir a [http: // gceinstanceip: 5555] (http: // gceinstanceip: 5555 /)

Asegúrese de especificar el puerto 5555, ya que es el puerto utilizado por Qmix

![9](https://docs.qtum.site/en/gcpgettingstarted/9.png)

[
](https://docs.qtum.site/en/Qtum-AWS/)