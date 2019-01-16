---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-10"

---

# 대상 추가

대상은 특정 온프레미스 또는 클라우드 리소스에 연결하는 방법에 대한 정의입니다. 대상이 작성되면 {{site.data.keyword.SecureGateway}} 서버는 해당 대상에 게이트웨이가 연결되어 있는 동안 연결을 청취할 고유 공용 엔드포인트를 제공합니다.

![대상이 없는 대시보드](./images/emptyDestinations.png?raw=true "대상이 없는 대시보드")

대상 추가 패널을 열려면 새 게이트웨이 내에 있는 대상 탭에서 대상 추가 단추를 클릭하십시오. 대상을 작성하기 위한 두 가지 방법이 존재합니다. 하나는 각각의 조각을 전체 아키텍처에 맞추는 방법을 보여주는 안내 설정이고 다른 하나는 단일 패널에서 모든 필드 및 옵션을 제공하는 고급 설정입니다.  

안내 설정의 경우 프록시 정보의 구성, 서버 이름 표시기 또는 대상 특정 인증서/키 쌍의 업로드를 허용하지 <b>않습니다</b>. 작성된 후에는 대상 편집 패널을 통해 모든 필드를 사용할 수 있습니다.

## 안내 패널

![안내 설정](./images/guidedLanding.png?raw=true "안내 설정 랜딩 패널")

## 고급 패널

![고급 설정](./images/advancedLanding.png?raw=true "고급 설정 랜딩 패널")

## 온프레미스 대 클라우드 대상
{: #dest-types}

대상을 작성할 때 답변할 첫 번째 질문은 연결해야 하는 리소스가 상주하는 위치입니다.

### 온프레미스 대상
온프레미스 대상은 공용 영역에 있는 애플리케이션이 온프레미스에 배치된 제한된 리소스에 액세스해야 하는 유스 케이스를 위한 것입니다.
![온프레미스 대상](./images/onPremDestination.png?raw=true "온프레미스 대상")

### 클라우드 대상
클라우드 대상은 제한된 네트워크에 있는 애플리케이션이 공용 영역에서 사용 가능한 리소스에 액세스해야 하는 유스 케이스를 위한 것입니다.
![역방향 대상](./images/reverseDestination.png?raw=true "클라우드 대상")

## 대상 정의
두 가지 유형의 대상 모두에 대해 다음과 같은 정보가 필요합니다.

- <b>리소스 호스트 이름</b>: 이 항목은 연결해야 하는 리소스의 IP 또는 호스트 이름입니다.
- <b>리소스 포트</b>: 이 항목은 리소스에서 청취하는 포트입니다.
- <b>프로토콜</b>: 이 항목은 애플리케이션에서 작성할 연결의 유형입니다. 다음 표에서 다양한 [프로토콜 옵션](#protocols)에 대해 참조하십시오. 리소스에 필요한 연결 유형을 구성하려면 [리소스 인증](#resource-auth) 절을 확인하십시오.

클라우드 대상을 선택한 경우 <b>클라이언트 포트</b>도 제공해야 합니다. 이 항목은 연관된 리소스 호스트 이름 및 포트에 대한 연결을 허용하기 위해 {{site.data.keyword.SecureGateway}} 클라이언트에서 청취할 포트입니다.

## 프로토콜 옵션
{: #protocols}

이 표에서는 애플리케이션이 {{site.data.keyword.SecureGateway}}에 대한 연결/요청을 시작하기 위해 사용할 수 있는 모든 옵션을 제공합니다.

프로토콜 |설명
-- | --
TCP | 인증이 없습니다. 애플리케이션에서 인증서 없이 {{site.data.keyword.SecureGateway}} 서버와 직접 통신할 수 있습니다.
TLS: 서버 측 | TLS(Transport Layer Security)가 사용으로 설정되어 있으며 서버에서 신뢰성을 입증하기 위해 인증서를 제공합니다.
TLS: 상호 인증 | 서버에서 인증서 세트를 제공하며 애플리케이션에서도 해당 연결 중에 인증서를 제공해야 합니다.
HTTP | 온프레미스 호스트 이름과 일치하도록 호스트 헤더가 재작성된 TCP 연결입니다.
HTTPS | 온프레미스 호스트 이름과 일치하도록 호스트 헤더가 재작성된 TLS: 서버 측 연결입니다.
HTTPS: 상호 인증 | 온프레미스 호스트 이름과 일치하도록 호스트 헤더가 재작성된 TLS: 상호 인증 연결입니다.


## 상호 인증 구성
{: #mutual-auth}

상호 인증을 적용하는 프로토콜의 경우 자체 인증서를 업로드해야 하거나 서버에서 자동으로 사용할 애플리케이션을 위한 자체 서명 인증서/키 쌍을 작성합니다. 이 쌍은 서버 인증서와 함께 다운로드할 수 있습니다.
![상호 인증 패널](./images/mutualAuth.png?raw=true "상호 인증 패널")

### 사용자 인증
{: #user-auth}

사용자 인증 섹션은 {{site.data.keyword.SecureGateway}}를 통해 요청/연결 애플리케이션의 권한을 관리하기 위한 것입니다. 이 필드는 애플리케이션에서 연결/요청과 함께 제공할 인증서인 단일 인증서를 허용합니다.

### 리소스 인증
{: #resource-auth}

리소스 인증은 {{site.data.keyword.SecureGateway}}에서 정의된 리소스에 연결하기 위해 시도할 방법을 판별합니다. 없음, TLS(서버 측) 및 상호 인증이라는 세 가지 옵션을 사용할 수 있습니다. 사용자의 선택에 따라 서로 다른 인증 옵션을 사용할 수 있게 됩니다.

리소스에 연결 시 TLS를 사용으로 설정하는 작업은 사용자 인증에 사용되는 TLS와 별개입니다. 사용자 인증용 TLS는 초기 요청 애플리케이션과 {{site.data.keyword.SecureGateway}} 간의 액세스(예: {{site.data.keyword.Bluemix_notm}} 앱과 {{site.data.keyword.SecureGateway}} 서버 간의 액세스)에 보안을 적용하는 반면 리소스 인증용 TLS는 {{site.data.keyword.SecureGateway}}와 정의된 리소스 간의 액세스(예: {{site.data.keyword.SecureGateway}} 클라이언트와 온프레미스 데이터베이스 간의 액세스)에 보안을 적용합니다.

#### 클라우드/온프레미스 인증

이 옵션은 리소스 인증을 위해 TLS 또는 상호 인증을 선택함으로써 사용할 수 있게 됩니다. 필드의 이름은 사용자가 선택한 [대상의 유형](#dest-types)과 일치합니다. 이 필드는 연결할 리소스의 인증서를 유효성 검증하기 위해 최대 6개의 인증서를 업로드할 수 있도록 해줍니다. 이 파일은 해당 리소스에 대한 연결의 CA에 추가되며 리소스에서 제공할 인증서 또는 인증서 체인이 포함되어 있어야 합니다.

#### 서버 이름 표시기(SNI)
이 옵션은 리소스 인증을 위해 TLS 또는 상호 인증을 선택함으로써 사용할 수 있게 됩니다. 이 항목은 리소스 연결의 TLS 핸드쉐이크에 별도의 호스트 이름을 제공할 수 있도록 허용하기 위해 사용됩니다.

### 클라이언트 인증서 및 키
클라이언트 인증서 및 키 필드가 표시되는 위치는 사용자가 선택한 [대상의 유형](#dest-types)에 따라 달라집니다. 두 가지 상황 모두 여기에서 제공되는 파일은 SG 클라이언트에서 TLS 연결을 위해 자신을 식별하는 데 사용됩니다. 파일이 업로드되지 않을 경우 {{site.data.keyword.SecureGateway}} 서버에서 `localhost`의 CN이 포함된 자체 서명 쌍을 자동으로 생성합니다. 인증서/키 쌍을 생성하는 방법에 대한 지시사항을 확인하려면 [여기를 클릭](./securegateway_keygen.html)하십시오.

온프레미스 대상에서 리소스 인증: 상호 인증을 선택한 경우 리소스 인증 아래에 표시됩니다. 이 경우 클라이언트에서 정의된 리소스에 대한 아웃바운드 연결을 위해 이 인증서/키 쌍을 사용합니다. 이 연결의 CA에는 [클라우드/온프레미스 인증](#resource-auth) 필드에서 제공된 인증서가 포함됩니다.

클라우드 대상에서 TLS 프로토콜을 선택한 경우 사용자 인증 아래에 표시됩니다. 이 경우 클라이언트에서 CA의 [사용자 인증](#user-auth)에 업로드된 파일을 사용하여 TLS 리스너를 설정하기 위해 이 인증서/키 쌍을 사용합니다.  

## 네트워크 보안 구성
특정 IP 주소를 제외한 모든 IP 주소에서 클라우드 호스트 및 포트에 연결하지 못하도록 차단하기 위해 온프레미스 대상에서 iptable 규칙을 적용하도록 선택할 수 있습니다.
![네트워크 보안 패널](./images/networkSecurity.png?raw=true "네트워크 보안 패널")

iptable 규칙을 적용하려면 네트워크 보안 패널에서 <b>iptable 규칙을 사용하여 이 대상에 대한 클라우드 액세스 제한</b> 상자를 선택하십시오. 해당 상자를 선택한 후에는 연결하도록 허용할 IP 추가를 시작할 수 있습니다. IP가 제공되지 않을 경우 <b>클라우드 액세스 제한</b> 상자가 선택되어 있는 한 이 클라우드 호스트 및 포트에 대한 모든 연결이 거부됩니다.

<b>참고</b>: 제공되는 IP 또는 포트는 요청을 작성하는 시스템의 로컬 IP 주소가 아닌 {{site.data.keyword.SecureGateway}} 서버에서 참조할 외부 IP 주소여야 합니다.

### iptable 규칙 추가
iptable에 규칙을 추가하는 경우 단일 포트 또는 포트 범위와 함께 개별 IP 또는 IP 범위를 제공할 수 있습니다. 제공되는 모든 범위의 마지막 부분도 포함됩니다. 다음 표에는 몇 가지 예제 및 해당 예제가 iptable 내에서 분석되는 방법이 포함되어 있습니다.

IP 주소 |포트 | 결과
-- | -- | --
1.2.3.4 | 5000 | 포트 5000에서 IP 1.2.3.4만 허용됩니다.
1.2.3.4-2.3.4.5 | 5000 | 포트 5000에서 1.2.3.4 - 2.3.4.5 사이의 IP가 모두 허용됩니다.
1.2.3.4 | 5000:10000 | 포트 5000 - 10000에서 IP 1.2.3.4만 허용됩니다.
1.2.3.4-2.3.4.5 | 5000:10000 | 포트 5000 - 10000에서 1.2.3.4 - 2.3.4.5 사이의 IP가 모두 허용됩니다.
1.2.3.4 | | 임의의 포트에서 IP 1.2.3.4만 허용됩니다.
| 5000 | 포트 5000에서 임의의 IP가 허용됩니다.

특정 규칙이 애플리케이션과 연관될 수도 있습니다. 연관된 규칙을 작성하는 방법에 대한 자세한 정보는 [앱에 대한 iptable 규칙을 작성하는 방법](./iptables.html)을 참조하십시오.

## 프록시 옵션 구성
온프레미스 대상이 SOCKS 프록시 뒤에 배치되는 경우 프록시 옵션 패널에서 대상의 프록시 설정을 구성할 수 있습니다.
![프록시 옵션 패널](./images/proxyOptions.png?raw=true "프록시 옵션 패널")

프록시 설정을 구성하기 위해서는 프록시에서 청취할 호스트 이름 및 포트와 사용할 SOCKS 프로토콜(4, 4a, 5)만 제공하면 됩니다.

## 대상 설정
대상이 작성된 후에는 설정 아이콘을 클릭하여 다음과 같은 정보를 확인할 수 있습니다.

- API를 사용하기 위해 필요한 대상 ID 
- <b>온프레미스 대상에는 클라우드 호스트 및 포트가 있습니다. 이 정보는 애플리케이션에서 온프레미스 리소스에 연결하기 위해 필요합니다.</b>
- <b>클라우드 대상에는 클라이언트 포트가 있습니다. 이 항목은 {{site.data.keyword.SecureGateway}} 클라이언트에서 온프레미스 애플리케이션을 클라우드 리소스에 연결하기 위해 청취할 포트입니다.</b>
- 이 대상이 지시하는 리소스 호스트 및 포트 
- 대상이 작성된 시점 및 작성한 사용자 
- 대상이 마지막으로 수정된 시점 및 수정한 사용자 