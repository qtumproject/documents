# 오프라인 스테이킹

* [슈퍼 스테이커에게 주소 위임](https://github.com/qtumproject/documents/blob/master/kor/OfflineStaking.md#슈퍼-스테이커에게-주소-위임)
* [주소 위임 방법 안내](https://github.com/qtumproject/documents/blob/master/kor/OfflineStaking.md#주소-위임-방법-안내)
* [슈퍼 스테이커 환경 설정](https://github.com/qtumproject/documents/blob/master/kor/OfflineStaking.md#슈퍼-스테이커-환경-설정)
* [슈퍼 스테이커로 퀀텀 코어 실행하기](https://github.com/qtumproject/documents/blob/master/kor/OfflineStaking.md#슈퍼-스테이커로-퀀텀-코어-실행하기)
* [qtumd 슈퍼 스테이커](https://github.com/qtumproject/documents/blob/master/kor/OfflineStaking.md#qtumd-슈퍼-스테이커)
* [슈퍼 스테이커 운영 안내](https://github.com/qtumproject/documents/blob/master/kor/OfflineStaking.md#슈퍼-스테이커-운영-안내)
* [복원](https://github.com/qtumproject/documents/blob/master/kor/OfflineStaking.md#복원)

# 슈퍼 스테이커에게 주소 위임


퀀텀 오프라인 스테이킹은 스테이킹을 하고 있지 않는 지갑의 주소를 슈퍼 스테이커에게 위임할 수 있게끔 하는 기능입니다. 오프라인 스테이킹은 자금 위탁 방식이 아니여서 위임자가 코인과 프라이빗 키에 대한 권한을 이양하지 않고 유지합니다. 스테이킹 위임은 위임자의 지갑에서 스마트 컨트랙트를 통해 이루어지며 해당 지갑을 통해 위임자의 주소, 슈퍼 스테이커의 주소, 그리고 위임자가 지불하기로 동의 한 수수료를 확인할 수 있습니다. 슈퍼 스테이커는 위임자가 설정한 수수료에 동의를 한 후 위임 된 주소의 UTXO 스테이킹을 진행하기 시작합니다.

위임된 주소의 UTXO를 스테이킹하는 일반적인 규칙은 아래와 같습니다. 

* UTXO는 숙성 후 스테이킹에만 사용할 수 있습니다 (500 개의 확인).
* 슈퍼 스테이커는 스테이킹에 사용할 최소 크기의 UTXO를 설정할 수 있으며 기본값은 100 QTUM입니다. 이 금액 미만의 위임 된 UTXO는 거절되게 됩니다.
* UTXO를 각각 100-200 QTUM 크기로 나누는 것이 가장 좋습니다 (수익률 최적화를 위해). 퀀텀코어 지갑 사용자의 경우, 커멘드 라인 버전에서 `splitutxosforaddress` 명령을 활용하여 이를 쉽게 수행 할 수 있습니다(하단 설명 참조).

퀀텀 코어 지갑에서 위임을 실행하려면 스테이킹 – 위임 탭 우측 상단에 있는 "+"버튼을 선택하고 슈퍼 스테이커의 이름, 주소, 희망하는 수수료 및 위임 할 주소 설정를 설정하면 됩니다. 가스 수수료는 특별한 요구사항이 없다면 기본 설정으로 두시면 됩니다. 위임 거래는 최소 0.9 QTUM의 수수료가 요구되며 초과 지불 금액은 환불됩니다.

![1  Add Delegation Assignment - ko](https://user-images.githubusercontent.com/29760787/86301021-c2908980-bbd2-11ea-89c9-b4b343544118.jpg)

설정 후 확인 버튼을 눌러 위임 트랜잭션을 실행합니다. 

Ledger 등 하드웨어 지갑 주소를 지원하는 퀀텀 일렉트럼 지갑을 통해서도 스테이킹 위임을 실행할 수 있습니다. 

# 주소 위임 방법 안내

주소 위임 트랜잭션은 스마트 컨트랙트로 전송되었다가 슈퍼 스테이커에게 할당됩니다. 지갑과 퀀텀 탐색기 [qtum.info] (https://qtum.info/)에서 위임된 주소에 대한 블록 보상을 확인하실 수 있습니다. 

지갑 속 여러 주소에 QTUM을 보유하고 있는 경우 각 주소마다 스테이킹 위임을 별도로 실행해야 하며 수수료도 각각 지정해야 합니다. 그러므로 UTXO를 분할하여 위임하기 전에 단일 주소로 통합하는 것이 좋습니다. 주소를 선택하여 코인을 통합하거나 `sendmanywithdupes` 명령을 사용하여 전체 지갑의 잔액을 적절한 UTXO 크기로 새 주소에 보낼 수 있습니다.

슈퍼 스테이커가 특정 수수료에 대한 위임을 수락 한 후에 최소 수수료를 낮춘 경우, 더 낮은 수수료를 이용하기 위해 위임자는 낮춘 수수료에 맞춰 새롭게 위임 해야 합니다.

스테이킹 위임 내역 확인은 지갑 속 스테이킹 – 위임 페이지 또는 `getdelegationinfoforaddress` 명령으로 확인할 수 있습니다.

wallet.dat 파일 저장을 통해 지갑을 백업하십시오.
 
# 슈퍼 스테이커 환경 설정

퀀텀 코어 지갑은 온라인 스테이킹 기능을 제공할뿐 아니라 기능 활성화를 통해 슈퍼 스테이커를 실행하여 주소를 위임 받고 오프라인 스테이킹 서비스를 제공할 수 있습니다.

슈퍼 스테이커를 위한 Qtum-Qt 지갑을 구성하려면 스테이킹 – 슈퍼 스테이킹 페이지에서 "+"버튼을 선택하여 새로운 슈퍼 스테이커를 추가하세요. 슈퍼 스테이커의 이름을 입력하고 드롭 다운 메뉴를 사용하여 주소를 선택하십시오. (슈퍼 스테이커의 이름은 지갑 내부 식별용입니다. 그림에서는 주소의 앞 부분과 10 % 요금을 표시하기 위해 "10"을 결합한 이름을 사용했습니다) 

![2  Super Staker Setup - ko](https://user-images.githubusercontent.com/29760787/86301037-cc19f180-bbd2-11ea-9012-51f3ed773ddd.jpg)

슈퍼 스테이커를 실행하려는 지갑은 임의의 주소를 확인하고(주소 색인), 스마트 컨트랙트 작업 에 사용 가능한 로그를 보유해야 하며 (로그 이벤트), 스테이킹 기능을 활성화해야 합니다. `-superstaking`를 통해 이 세 가지 설정을 단번에 완료할 수 있게 됩니다. 처음 `-superstaking`를 실행하면 지갑은 블록체인을 다시 스캔하여 데이터베이스를 재구축하고 주소 인덱스와 로그 이벤트를 추가합니다.

그 다음에는 지갑에서 설정 – 옵션 – ‘슈퍼 스테이킹 활성화’를 체크하면 슈퍼 스테이커를 위해 지갑이 재부팅 됩니다. 

![3  Qtum-Qt Enable Super Staker - ko](https://user-images.githubusercontent.com/29760787/86301042-cf14e200-bbd2-11ea-88a7-f2bec8535668.jpg)
 
재부팅시 지갑은 데이터베이스를 스캔하여 재구축 할 것인지를 확인합니다.

![4  Rebuild the Database - ko](https://user-images.githubusercontent.com/29760787/86301045-d1773c00-bbd2-11ea-8e3a-5df6eb9c97ec.jpg)

데이터베이스를 재구축하는 동안 화면에는 "디스크의 블록 인덱싱 ..."및 "헤더 동기화"가 표시될것이며 컴퓨터 사양에 따라 수십 분이 걸릴 수 있습니다.

실행 후 스테이킹 – 슈퍼 스테이킹 페이지로 돌아와서 “슈퍼 스테이커 구성” 버튼(설정 버튼)을 눌러 슈퍼 스테이커 구성을 완료하면됩니다. 페이지에서 기본 권장 사항 (아래 참조)을 확인하거나 사용자 정의로 설정을 완료할 수 있습니다. 

![5  Super Staker Options  -ko](https://user-images.githubusercontent.com/29760787/86301052-d5a35980-bbd2-11ea-9f86-f02ef15a93ab.jpg)

설정 내용은 다음과 같습니다.

* 최소 수수료 – 슈퍼 스테이커가 위임자로부터 받아들일 수 있는 최소 수수료.

* 최소 UTXO 크기 – 슈퍼 스테이커가 스테이킹 서비스를 제공할 최소 크기의 UTXO를 설정합니다. 시간이 지남에 따라 위임 된 주소는 많은 작은 블록 보상 UTXO를 축적하게 되며 이러한 작은 액수를 모두 관리하는 것은 비효율적입니다 (작은 UTXO는 위임자가 재결합해야 함).


* 위임 목록 유형 :
  * 모두 수락 – 설정한 최소 수수료 또는 그 이상을 승인한 모든 위임을 수락합니다.
  * 허용 목록 – 특정 주소의 위임만 수락합니다. 특정 주소에 대해서만 슈퍼 스테이커를 운영하려는 경우, 해당 모드를 사용하세요. 
  * 제외 목록 – 스테이킹에서 제외 할 주소입니다.

그 다음 슈퍼 스테이커가 스테이킹을 확정하기 위해 UTXO를 유효한 액수로 분할합니다. UTXO는 최소 100 QTUM이어야합니다. 슈퍼 스테이커 페이지에서 분할 버튼 (트라이던트 아이콘)을 선택하여 기본값을 사용하거나 액수 조정을 할 수 있습니다. 단 100 QTUM 미만의 UTXO는 스테이킹에 사용될 수 없습니다. 

![6  Split UTXOs GUI - ko](https://user-images.githubusercontent.com/29760787/86301064-d936e080-bbd2-11ea-91ee-213138eeb270.jpg)

위임 된 주소에서도 사용될 수있는 `splitutxosforaddress` 명령을 통해 UTXO를 분할 할 수도 있습니다. UTXO의 최소값과 최대값 범위를 설정하려면 다음 명령을 입력하시면 됩니다.

`splitutxosforaddress "address" minValue maxValue ( maxOutputs )`

예를 들어, 지갑에 40, 50, 60, 70 및 800 QTUM의 UTXO가 있는 경우, 이를 100에서 200 사이의 UTXO로 분할하려면 다음 명령을 사용하시면 됩니다. 

```splitutxosforaddress "qQhm128r4cTuDFSRehLESydnkburYLj9cY" 100 200

{
  "txid": "197a199c3ac9dd8df574ca77da15c5da31db3f7101e2108638a3b2f94248b9f7",
  "selected": "1020.00",
  "splited": "1020.00"
}
```

해당 예시의 총 인풋은 1,020 QTUM이고 분할 후 100 QTUM 크기의 UTXO 9개와 119.99566 QTUM 크기의 UTXO 한 개로 분할됩니다. 이 과정에서 지갑은 "자신과의 거래"를 내보내고0.00434 QTUM의 수수료를 지불합니다.

큰 금액을 가진 지갑들은 최적의 분할을 위해 ‘최대 아웃풋 (Maximum Outputs) 값을 수정해주세요. 위에 그림을 보면 ‘최대 아웃풋’ 란의 기본값은 100이여서 분할 작업을 할 경우 100 QTUM (최소 사이즈 minimum size) x 100 (최대 아웃풋) = 10,000 UTXO 값이 됩니다. 이 보다 많은 금액을 가진 주소들은 최대 아웃풋 값을 500 또는 1,000으로 상향 조정하시길 바랍니다. 1,000으로 설정했을 경우 100,000 UTXO 값을 분할 할 수 있습니다. 큰 액수를 가진 주소들도 이러한 명령어을 반복하면 최적의 상태로 분할할 수 있습니다. 

UTXO 분할을 위해`sendmanywithdupes` 명령어 또한 사용할 수 있지만 해당 명령어는 형식이 복잡했고 새 주소를 사용해야하는 합니다. 어떤 분할 명령이든 실행 후 UTXO는 500 개의 확인을 거친 후 스테이킹에 사용될 수 있습니다.

# 슈퍼 스테이커로 퀀텀 코어 실행하기

위의 단계는 기본 퀀텀 코어 지갑에서 슈퍼 스테이커로의 전환을 보여줍니다. 이런 단계들을 단축시켜 바로 슈퍼 스테이커를 위한 지갑을 실행하는 방법이 있습니다. 이 경우, 초기 블록체인 동기화 과정에서 위에서 언급했던 주소 인덱스와 로그 이벤트에 대한 데이터베이스를 구축하여 지갑이 바로 슈퍼 스테이킹을 수행할 수 있도록 합니다.

퀀텀 코어 지갑에서 위에 언급한 것처럼 “설정 - 옵션 – 메인 – 슈퍼 스테이킹 활성화” 단계를 통해 슈퍼 스테이킹을 활성화하거나 커멘드 라인에서 `-superstaking`를 통해 실현할수도 있습니다. (아래 예시는 테스트넷에서 실현한 것입니다)

![7  Linux Launch - ko](https://user-images.githubusercontent.com/29760787/86301075-db993a80-bbd2-11ea-8610-2e401ea4fe4e.png)

Windows의 기본 프로그램 디렉토리 명령은 다음과 같습니다.

`qtum-qt -testnet -superstaking`

![8  Windows Command Line Launch - ko](https://user-images.githubusercontent.com/29760787/86302962-5fa1f100-bbd8-11ea-823f-9bca65f35d4d.jpg)

해당 작업 후 지갑이 시작되고 블록체인이 동기화되면(주소 인덱스 및 로그 이벤트 생성) 바로 슈퍼 스테이커를 추가 할 수 있습니다. 슈퍼 스테이커를 구성한 다음 설정 – 옵션 – 메인 –“슈퍼 스테이킹 활성화”를 누르면 슈퍼 스테이커가 준비됩니다.

# qtumd 슈퍼 스테이커

슈퍼 스테이커로 실행되는 퀀텀 코어 지갑의 모든 주소는 주소를 위임받아 개별적으로 슈퍼 스테이커로 작동 할 수 있습니다. 데스크탑 GUI 지갑인 Qtum-Qt를 통해 서로 다른 수수료와 최소 UTXO 크기가 설정된 여러 개의 슈퍼 스테이커 주소를 구성 할 수 있습니다. Daemon 또는 서버용 지갑인 qtumd는 지갑 속 모든 슈퍼 스테이커 주소에 동일한 수수료와 최소 UTXO 크기가 적용됩니다. qtumd를 사용하면서 여러 슈퍼 스테이커의 수수료와 최소 UTXO 크기를 상이하게 운영하려면 Qtum-Qt 지갑으로 이를 설정하고 wallet.dat 파일로 저장하여 qtumd로 전송하여 사용할 수 있습니다.

다음은 qtumd에서 단일 슈퍼 스테이커 주소를 사용하는 설정입니다. 

qtumd를 설치 한 후 다음 명령어로 실행하세요. (아래 그림은 테스트넷에서 실현한 모습입니다)

`./qtumd -testnet -superstaking`

기본 수수료 설정(10 %)과 최소 UTXO 값(100 QTUM)을 변경하기 위해 아래와 같은 변수를 추가 할 수 있습니다

`-stakingminfee=12  -stakingminutxovalue=120`

지갑이 블록체인을 동기화하면 QTUM을 보낼 주소를 얻게 됩니다. 이는 슈퍼 스테이커 주소입니다. 그 다음 아래 명령을 사용하세요. 

`./qtum-cli -testnet getnewaddress "legacy"`

그런 다음 이 주소로 1,300 QTUM을 보내세요. 

![9  Getnewaddress Getbalance - ko](https://user-images.githubusercontent.com/29760787/86301085-e3f17580-bbd2-11ea-95e9-036fb23340a5.png)

이 1,300 개의 QTUM은 단일 UTXO로 도착하게 되며 슈퍼 스테이킹 작업을 위해 분할 되어야합니다. `splitutxosforaddress` 명령으로 UTXO 크기 범위를 100-200 크기로 분할해보세요. 

`./qtum-cli -testnet splitutxosforaddress "qdMp2BNpwL6ZmMEQHfLV5wGNVgmPCuzd7d" 100 200`

![10  Split UTXOs for Address qtumd - ko](https://user-images.githubusercontent.com/29760787/86301092-e784fc80-bbd2-11ea-9077-3a27b35a8031.png)

명령어 입력 후 분할을 위해 1,300 개의 QTUM이 선택되었음을 알 수 있습니다. 탐색기로 txid를조회하면 12 개의 UTXO로 분할된 것을 확인할 수 있습니다.

이제 qtumd 지갑은 qdMp2BNpwL6ZmMEQHfLV5wGNVgmPCuzd7d 주소를 통해 슈퍼 스테이킹 작업을 수행 할 준비가 되었으며 다음 명령을 사용하여 위임 내역을 모니터링 할 수 있습니다.

`getdelegationsforstaker "qdMp2BNpwL6ZmMEQHfLV5wGNVgmPCuzd7d"`

# 슈퍼 스테이커 운영 안내

슈퍼 스테이커는 위임된 UTXO를 스테이킹하기 위해 자체적으로 UTXO를 보유해야 합니다. 보유해야 하는 UTXO의 개수(UTXO 최소 크기는 100 QTUM)는 전체 네트워크 무게에서 해당 슈퍼 스테이커가 위임 받은 무게의 비중에 따라 상이합니다. 전체 네트워크 무게의 1%를 스테이킹하는 경우 30 개의 UTXO가 이상적이며, 2.0%일 경우 50개, 5%일 경우 100개, 10%일 경우 160개가 이상적입니다. 

슈퍼 스테이커는 지갑 무게(UTXO 무게에서 현재 스테이킹 금액을 제한 값)를 지속적으로 모니터링하여 UTXO가 일정 수치 이하로 떨어지면 추가 해야합니다.

오프라인 스테이킹 설정은 wallet.dat 파일에 저장되므로 슈퍼 스테이커 추가 또는 위임 추가와 같은 오프라인 스테이킹 설정을 변경 한 후 지갑을 백업하세요(wallet.dat 파일 저장). 백업한 wallet.dat 파일을 유실한 경우, 설정 내역은 아래 표시된 방법에 따라 복원 될 수도 있습니다.

슈퍼 스테이커에 대한 위임은 슈퍼 스테이커 페이지의 "위임…"버튼 또는`getdelegationsforstaker` 명령을 사용하여 확인할 수 있습니다.

# 복원

일반적으로 위임 및 슈퍼 스테이커 설정 정보는 wallet.dat 파일에 저장됩니다. wallet.dat 파일에 문제가 생겼을 경우, 위임 및 슈퍼 스테이커 정보는 슈퍼 스테이커 페이지에 있는 복원 버튼을 통해 복구 될 수 있습니다. 이 경우 지갑은 해당 주소의 오프라인 스테이킹 트랜젝션을 얻기 위해 컨트랙트 "상태" 메모리를 다시 스캔합니다.

![11  Restore super stakers - ko](https://user-images.githubusercontent.com/29760787/86301095-eb188380-bbd2-11ea-8256-74e7b6f2abf1.jpg)
 
***

