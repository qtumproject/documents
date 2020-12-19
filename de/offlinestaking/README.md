# Offline Staking

* [Delegieren einer Adresse zum Super Staker](#delegieren-einer-adresse-zum-super-staker)
* [Delegieren von Adressoperationen](#delegieren-von-adressoperationen)
* [Super Staker Konfiguration](#super-staker-konfiguration)
* [Qtum Core als Super Staker starten](#qtum-core-als-super-stacker-starten)
* [qtumd Super Staker](#qtumd-super-staker)
* [Super Staker Operationen](#super-staker-operationen)
* [Wiederherstellung](#wiederherstellung)

# Delegieren einer Adresse zum Super Staker

Mit Qtum Offline Staking kann die Adresse für ein Non-Staking Wallet (die die Delegierungszuweisungstransaktion durchführen kann) an einen Super Staker delegiert werden. Offline-Staking ist nicht verwahrungspflichtig: Der Delegationsbenutzer behält die volle Kontrolle über seine Coins und privaten Schlüssel. Die Adressdelegierung erfolgt über eine intelligente Vertragstransaktion (Smart Contract) aus dem Wallet des Delegierungsbenutzers, in der die Adresse des Delegators, die Super Staker-Adresse und die vom Delegator zu zahlende Gebühr angegeben sind. Wenn der Super Staker diese Gebühr akzeptiert, beginnt er mit dem Staking der UTXOs für delegierte Adressen.

Für delegierte UTXOs gelten die normalen Regeln für das Staken von UTXOs:

* UTXOs dürfen erst nach ihrer Reife zum Staken verwendet werden (500 Bestätigungen).
* Der Super Staker legt eine Mindestgröße für den Einsatz von UTXOs fest, standardmäßig 100 QTUM. Delegierte UTXOs unterhalb dieses Betrags werden ignoriert.
* Es wird empfohlen, UTXOs (für optimale Renditen) in Größen von jeweils 100 bis 200 QTUM aufzuteilen. Für Benutzer der Qtum Core-Wallet kann dies problemlos mit der unten beschriebenen Befehlszeilenversion von `splitutxosforaddress` erreicht werden.

Um die Delegierungszuweisung aus dem Qtum Core-Wallet vorzunehmen, wählen Sie Stake => Delegations =>  die Schaltfläche Delegation hinzufügen "+" in der oberen rechten Ecke, geben den Staker-Namen (nur als lokale Referenz), die Staker-Adresse, die Gebühr, die Sie zahlen möchten, und ihre zu delegierende Adresse ein. Lassen Sie die Standard-Gaseinstellungen in Ruhe, es sei denn, Sie verstehen, wie Sie diese einstellen. Für die Delegationstransaktion sind Gebühren in Höhe von mindestens 0,9 QTUM erforderlich, und etwaige Überschüsse werden erstattet.

![1  Add Delegation Assignment](https://user-images.githubusercontent.com/29760787/85331894-f8cc5b80-b4a4-11ea-95d1-eb472a5454f1.jpg)

Drücken Sie Confirm und dan Yes, um die Delegierungstransaktion zu senden.

Die Delegierung von Adressen kann auch mithilfe der Qtum Electrum-Wallet erfolgen, die Ledger-Hardware-Wallet-Adressen unterstützt.

# Delegieren von Adressoperationen

Die Transaktion "Delegiertenadresse" wird an einen intelligenten Vertrag gesendet, der die Delegierungszuweisungen beibehält und dort vom Super Staker abgeholt wird. Sie können Belohnungsvorgänge für blockierte delegierte Adressen in der Brieftasche und auch mit dem Explorer [qtum.info] (https://qtum.info/) anzeigen.

Wenn das Wallet QTUM für mehrere Adressen enthält, muss die Delegierung für jede Adresse separat erfolgen (und die für jede Adresse gezahlte Transaktionsgebühr), sodass es möglicherweise sinnvoll ist, die UTXOs vor dem Aufteilen von UTXOs und dem Delegieren auf eine einzige Adresse zu konsolidieren. Verwenden Sie in diesem Fall die Münzauswahl, um die Adressen auszuwählen und zu konsolidieren. Alternativ kann der Befehl "sendmanywithdupes" verwendet werden, um das gesamte Walletguthaben an eine neue Adresse mit UTXOs geeigneter Größe zu senden.

Wenn der Super Staker eine Delegierung für eine bestimmte Gebühr akzeptiert und der Super Staker diese Gebühr reduziert (Aufträge für eine niedrigere Gebühr akzeptiert), muss der Benutzer seine Adresse erneut mit der niedrigeren Gebühr delegieren, um diese niedrigere Gebühr nutzen zu können.

Delegationen aus einem Wallet können auf der Seite "Stake => Delegationen" oder mit dem Befehl "getdelegationinfoforaddress" überprüft werden.

Sichern Sie Ihr Wallet , um eine Kopie der Datei wallet.dat zu speichern.
 

# Super Staker Konfiguration

Das Qtum Core-Wallet bietet einen Online Proof of Stake und kann gestartet und konfiguriert werden, um als Super Staker zu fungieren und Adressdelegationen zu empfangen.

Um das Qtum-Qt-Wallet für einen Super Staker zu konfigurieren, wählen Sie Stake => Super Staking und die Schaltfläche "+", um einen neuen Super Staker hinzuzufügen. Geben Sie den Staker-Namen ein (nur als lokale Referenz, z.b. hier den ersten Teil der Adresse und "10", um eine Gebühr von 10% anzugeben) und wählen Sie die Staker-Adresse in der Dropdown-Liste aus.
![2  Super Staker Setup](https://user-images.githubusercontent.com/29760787/85331902-fc5fe280-b4a4-11ea-9506-84bfc0ecd6d5.jpg)

Um als Super Staker zu arbeiten, muss das Wallet in der Lage sein, beliebige Adressen (Adressindex) zu überprüfen, Protokolle für intelligente Vertragsvorgänge (Protokollereignisse) zu aktivieren, und  für das Staken aktiviert sein. Der einzelne Parameter "Superstaking" setzt diese drei Parameter. Beim ersten Start mit "-superstaking" scannt das Wallet die Blockchain erneut, um die Datenbank neu zu erstellen und den Adressindex und die Protokollereignisse hinzuzufügen.

Als Nächstes wird das Wallet aufgefordert, als Super Staker neu gestartet zu werden. Verwenden Sie dazu Settings - Allgemein- Super Staking aktivieren und OK, um das Wallet neu zu starten.
![3  Qtum-Qt Enable Super Staker](https://user-images.githubusercontent.com/29760787/85331912-008c0000-b4a5-11ea-9901-c4b4433a8746.jpg)

Beim Start bestätigt das Wallet , dass Sie die Datenbank scannen und neu erstellen möchten.

![4  Rebuild the Database](https://user-images.githubusercontent.com/29760787/85331921-041f8700-b4a5-11ea-8990-628f295ff4a9.jpg)

Im Wallet werden "Neuindizieren von Blöcken auf der Festplatte ..." und "Synchronisieren von Headern" angezeigt, während die Datenbank neu erstellt wird. Dies kann je nach Computer mehrere zehn Minuten dauern.

Kehren Sie nach dem Start zur Seite Stake - Super Staking zurück und wählen Sie die Schaltfläche "Configure Super Staker" (das Zahnradsymbol wird jetzt angezeigt), um die Super Staker-Konfiguration zu öffnen. Klicken Sie auf das Feld Benutzerdefiniert, um die Standardempfehlungen (siehe unten) anzuzeigen, oder passen Sie das Setup manuell an. Klicken Sie auf OK, um die Einrichtung abzuschließen.

![5  Super Staker Options](https://user-images.githubusercontent.com/29760787/85331928-084ba480-b4a5-11ea-8434-82f9f140b6b6.jpg)

Die Konfigurationseinstellungen sind:

* Mindestgebühr - die von den Delegatoren angebotene Mindestgebühr, die der Staker akzeptiert.
* Minimale UTXO-Größe - Hiermit wird die minimale UTXO-Größe festgelegt, die vom Staker auf Proof of Stake-Konsens bewertet wird. Im Laufe der Zeit sollte die delegierte Adresse viele UTXOs mit kleinen Blockbelohnungen ansammeln, und es ist ineffizient, all diese kleinen Beträge zu verwalten (die vom Delegator neu kombiniert werden sollten).
* Delegationslistentyp:
  * Alle akzeptieren - Akzeptieren Sie jede Delegation mit der Mindestgebühr oder mehr.
  * Liste zulassen - Akzeptieren Sie nur Delegierungen von bestimmten Adressen. Verwenden Sie diesen Modus, wenn Sie einen Super Staker nur für bestimmte Adressen betreiben, z. B. für Ihre eigenen Coins.
  * Ausschlussliste - Adressen, die von der Annahme zum Staken ausgeschlossen werden sollen.

Teilen Sie als Nächstes die UTXOs in gültige Beträge auf, damit der Super Staker Einsätze festlegt. Die UTXOs müssen mindestens 100 QTUM betragen. Wählen Sie auf der Seite Super Staker die Schaltfläche Split Coins (Dreizack-Symbol) und verwenden Sie die Standardwerte oder nehmen Sie Anpassungen vor. Es werden jedoch keine UTXOs unter 100 QTUM zum Staken verwendet.

![6  Split UTXOs GUI](https://user-images.githubusercontent.com/29760787/85331934-0a156800-b4a5-11ea-9339-eed51b9bddf6.jpg)

Sie können UTXOs auch mit dem Befehl `splitutxosforaddress` teilen, der auch für delegierte Adressen verwendet werden kann. Geben Sie den folgenden Befehl ein, um die UTXOs zwischen einem minimalen und einem maximalen Wert aufzuteilen:

`splitutxosforaddress "address" minValue maxValue ( maxOutputs )`

Wenn ein Wallet beispielsweise UTXOs mit 40, 50, 60, 70 und 800 QTUM enthält, verwenden Sie den folgenden Befehl, um diese in UTXOs mit mindestens 100 und maximal 200 aufzuteilen:

```splitutxosforaddress
{
  "txid": "197a199c3ac9dd8df574ca77da15c5da31db3f7101e2108638a3b2f94248b9f7",
  "selected": "1020.00",
  "splited": "1020.00"
}
```

In diesem Beispiel betrug die Gesamteingabe 1.020 QTUM und die Aufteilung 9 UTXOs von 100,0 und eine von 119,99566, wobei das Wallet eine "Transaktion an sich selbst" sendete und eine Gebühr von 0,00434 QTUM entrichtete.

Bei größeren Wallets muss möglicherweise die Anzahl der "Maximalleistungen" für die Aufteilung angepasst werden. In dem obigen Beispiel, in dem das Feld "Maximale Ausgaben" auf den Standardwert 100 eingestellt ist, wird die Teilungsoperation aufgeteilt, wobei 100 QTUM (minimale Größe) x 100 (maximale Ausgaben) = 10.000 UTXO-Werte erhalten werden. Für Adressen mit mehr Wert kann das Feld "Maximale Ausgabe" höher, auf 500 oder 1000 eingestellt werden. Wenn das Feld "Maximale Ausgabe" auf 1000 eingestellt ist, kann der UTXO-Wert auf bis zu 100.000 aufgeteilt werden. Selbst größere Adressen können diesen Split-Befehlssatz für maximal 1000 Ausgaben einfach wiederholen, bis der Split-Vorgang meldet, dass 0 Münzen ausgewählt und geteilt wurden.

Früher konnten Sie den Befehl `sendmanywithdupes` verwenden, dies erforderte jedoch eine erhebliche Formatierung, und Sie möchten operativ an eine neue Adresse senden. Natürlich müssen die UTXOs nach einem dieser Befehle für 500 Bestätigungen reifen, bevor sie zum Staken verwendet werden können.

# Qtum Core als Super Stacker starten

Die obigen Schritte zeigen den Übergang von einer Standardinstallation des  Qtum Core-Walles zu einem Super Staker. Das Wallet kann auch bereits initial als  Super Staker gestartet werden, um die Schritte zu verkürzen. In diesem Fall wird die anfängliche Blockchain-Synchronisierung von der Erstellung der Datenbank für Adressindex- und Protokollereignisse (wie oben erläutert) begleitet, damit das Wallet für Super Staking bereit ist.

Das Qtum Core-Wallet kann als Super Staker mit Qtum-Qt unter Verwendung von Settings - Optionen - Allgmein - Enable Super Staking (wie oben gezeigt) oder direkt über die Befehlszeile mit dem Parameter `-superstaking` gestartet werden. (im Screenshot wird das Tesnet gezeigt, für das Mainnet muss der Parameter `-testnet` weggelassen werden) 

![7  Linux Launch](https://user-images.githubusercontent.com/29760787/91646311-ca767980-ea1b-11ea-8a0a-aa89cc208c90.png)

Dieser Befehl für das Standardprogrammverzeichnis unter Windows lautet:

`qtum-qt -testnet -superstaking` 

![8  Windows Command Line Launch](https://user-images.githubusercontent.com/29760787/91646313-cd716a00-ea1b-11ea-9586-52adafbea506.jpg)

Wenn das Wallet die Blockchain gestartet und synchronisiert wurde (Adressindex und Protokollereignisse erstellen), können Super Stakers hinzugefügt werden. Konfigurieren Sie einen Super Staker und aktivieren Sie dann Super Staking unter Settings- Optionen - Allgemein - stellen Sie "Enable Super Staking " ein, und der Super Staker ist bereit.

# qtumd Super Staker

Jede Adresse in einem Qtum Core-Wallet , die als Super Staker ausgeführt wird, kann delegierte Adressen erhalten und als einzelner Super Staker fungieren. Das Desktop-GUI-Wallet Qtum-Qt ermöglicht die Konfiguration mehrerer Super Staker-Adressen mit unterschiedlichen Gebühren und minimalen UTXO-Größen. Die Daemon / Server-Brieftasche qtumd führt alle Super Staker-Adressen mit derselben Gebühr und minimaler UTXO-Größe aus. Wenn eine Variation über mehrere Super Staker-Adressen mit qtumd erforderlich ist, können Sie diese mit dem Qtum-Qt-Wallet einrichten und die Datei wallet.dat einfach an qtumd übertragen.

Das folgende Setup für qtumd zeigt die Verwendung einer einzelnen Super Staker-Adresse.

Starten Sie nach der Installation von qtumd mit den folgenden Parametern (im Screenshot wird das Tesnet gezeigt, für das Mainnet muss der Parameter `-testnet` weggelassen werden):

`./qtumd -testnet -superstaking`

Optionale Parameter können hinzugefügt werden, um die Standardgebühr (von 10%) und den minimalen UTXO-Wert (von 100 QTUM) zu ändern, z. B.:

`-stakingminfee=12  -stakingminutxovalue=120`

Once the wallet syncs the blockchain, get an address to send some QTUM. This will be the Super Staker address. Use the command:

`./qtum-cli -testnet getnewaddress "legacy"`

Dann senden Sie QTUM an diese Adresse. ( In unserem Beispiel 1.300 ) 

![9  Getnewaddress Getbalance](https://user-images.githubusercontent.com/29760787/85331969-13063980-b4a5-11ea-8ccc-280092131d18.png)

Diese 1.300 QTUM werden in einem einzigen UTXO ankommen, das für den Super Staker-Betrieb aufgeteilt werden muss. Verwenden Sie den Befehl `splitutxosforaddress` mit der Standardgröße 100 Mindestgröße und 200 Höchstgröße:

`./qtum-cli -testnet splitutxosforaddress "qdMp2BNpwL6ZmMEQHfLV5wGNVgmPCuzd7d" 100 200`

![10  Split UTXOs for Address qtumd](https://user-images.githubusercontent.com/29760787/85331976-15689380-b4a5-11ea-91dd-187b6875f3b2.png)

Die Befehlsantwort zeigt, dass 1.300 QTUM für die Aufteilung ausgewählt wurden, in diesem Fall die Aufteilung in 12 UTXOs, die mit der txid im Explorer angezeigt werden.

Zu diesem Zeitpunkt ist das qtumd-wallet für den Super Staker-Betrieb mit der Adresse qdMp2BNpwL6ZmMEQHfLV5wGNVgmPCuzd7d bereit, und Delegierungen können mit dem folgenden Befehl überwacht werden:

`getdelegationsforstaker "qdMp2BNpwL6ZmMEQHfLV5wGNVgmPCuzd7d"`

# Super Staker Operationen

Der Super Staker muss UTXOs halten, um sich für die delegierten UTXOs, die er setzt, zu Einsätzen zu verpflichten. Die Anzahl der UTXOs (mit einer Mindestgröße von 100 QTUM) basiert auf dem delegierten Gewicht in Prozent des gesamten Netzwerkgewichts. Gute Werte sind 30 UTXOs für den Einsatz von 1% des Netzwerkgewichts, 50 UTXOs für 2,0%, 100 UTXOs für 5% und 160 UTXOs für den Einsatz von 10% des gesamten Netzwerkgewichts.

Super Staker sollten ihr Wallet Gewicht (UTXO-Gewicht abzüglich der derzeit eingesetzten Menge) überwachen und UTXOs hinzufügen, wenn es unter mehrere Tausend fällt.

Erstellen Sie eine Sicherungskopie des Wallets (speichern Sie die Datei wallet.dat), nachdem Sie die Offline-Staking Konfiguration geändert haben, z. B. einen Super Staker hinzugefügt oder eine Delegierung hinzugefügt haben, da das Offline-Staking in der Datei wallet.dat gespeichert wird. Wenn die Datei backup wallet.dat verloren geht, kann die Konfiguration auch mit der Wiederherstellung wiederhergestellt werden (siehe unten).

Delegierungen an einen Super Staker können mit der Schaltfläche "Delegierungen ..." auf der Super Staker-Seite oder mit dem Befehl "getdelegationsforstaker" überprüft werden.

# Wiederherstellung

Normalerweise werden die Delegierung und die Super Staker-Konfiguration in der Datei wallet.dat gespeichert. Wenn Probleme mit der Datei wallet.dat auftreten, können die Delegierungsinformationen und Super-Staker-Informationen mithilfe der Schaltfläche Wiederherstellen auf den Seiten Delegation und Super Staker wiederhergestellt werden. In diesem Fall durchsucht das Wallet den Vertragsspeicher "Status" für Offline-Staking nach den entsprechenden Adressen.

![11  Restore super stakers](https://user-images.githubusercontent.com/29760787/85331982-18638400-b4a5-11ea-9f59-755b2ecd06a6.jpg)

***
