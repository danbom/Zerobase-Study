# CHAPTER1
## _웹과 네트워크의 기본에 대해 알아보자_
![image](https://user-images.githubusercontent.com/52441697/175770382-89086876-21d3-4c19-a588-e2d6df0a147e.png)

- 💡 HTTP
- ✨ TCP/IP
- 📣 URI & URL
<br>

## 📑 HTTP

사용자가 브라우저 주소 입력란에 `URL`을 입력하면 어딘가에서 응답이 돌아와 웹 페이지가 표시된다. 정리해보면, 클라이언트가 주소로 지정한 서버의 리소스(파일 등의 정보)를 가지러 가거나 건네면 서버가 `HTTP`를 사용한 통신으로 응답을 보낸다. 이렇게 클라이언트에서 서버까지 일련의 흐름을 결정하고 있는 것을 `HTTP(HyperText Transfer Protocol)`라고 한다.
> 프로토콜 : 약속을 의미, 즉 웹은 HTTP라는 약속을 사용한 통신으로 이루어져있다

CERN(유럽 입자 물리학 연구소)가 세계 곳곳에 있는 연구자들의 지식 공유를 지원하기 위해 최초의 `웹(WWW, World Wide Web)`을 제안했다. 이러한 `WWW`를 구성하는 기술로서, 문서 기술 언어로는 [SGML](https://www.iso.org/standard/16387.html)을 베이스로한 `HTML(HyperText Markup Language)`, 문서 전송 프로토콜로는 `HTTP`, 문서의 주소를 지정하는 방법으로 `URL(Uniform Resource Locator)`이 제안되었다.

<br>

## 📑 TCP/IP
인터넷을 포함한 우리가 일반적으로 사용하고 있는 네트워크는 `TCP/IP`라는 프로토콜의 집합에서 움직인다. `HTTP`가 그 중 하나이다. 

컴퓨터와 네트워크 기기가 상호간에 통신하기 위해서는 서로 같은 방법으로 통신해야하고 다음과 같은 규칙을 결정할 필요가 있다. 그리고 이러한 규칙을 `프로토콜`이라고 부른다.
- 어떻게 상대를 찾고
- 어떻게 상대에게 이야기를 시작하고
- 어떠한 언어로 이야기를 하며
- 어떻게 이야기를 종료할까

<br>

`프로토콜`엔 케이블 규격, IP 주소 지정 방법, 떨어진 상대를 찾기 위한 방법, 그 곳에 도달하는 순서, 웹을 표시하기 위한 순서 등 여러가지가 있다. 이렇게 인터넷과 관련된 프로토콜들을 모은 것을 `TCP/IP`라고 부른다. `TCP`와 `IP` 프로토콜을 가리켜 `TCP/IP`라고 부르기도 하지만, IP 프로토콜을 사용한 통신에서 사용되는 프로토콜을 총칭해 `TCP/IP`라는 이름이 사용되고 있다.

<br>

`TCP/IP`는 다음과 같은 4계층(Layer)으로 나뉜다.
- 애플리케이션 계층
- 트랜스포트 계층
- 네트워크 계층
- 링크 계층

이러한 계층화의 장점은 첫째, 사양이 변경된 경우 사양이 변경된 해당 계층만 바꿔주면 된다. 둘째, 설계를 편하게 할 수 있다. 애플리케이션 층에서 애플리케이션은 자기 자신이 담당하는 부분을 고려하면 되고 다른 것들은 고려하지 않아도 된다.

<br>

### 📌 애플리케이션 계층
애플리케이션 계층은 사용자에게 제공되는 애플리케이션에서 사용하는 통신의 움직임을 결정한다. `FTP`, `DNS`, `HTTP`가 이 계층에 포함된다.

### 📌 트랜스포트 계층
트랜스포트 계층은 애플리케이션 계층에 네트워크로 접속되어 있는 컴퓨터 사이의 데이터 흐름을 제공한다. `TCP(Transmission Control Protocol)`와 `UDP(User Data Protocol)` 두 가지 프로토콜이 여기에 해당된다.

### 📌 네트워크(인터넷) 계층
네트워크 계층은 네트워크 상에서 패킷의 이동을 다룬다. 패킷이란 전송하는 데이터의 최소 단위이다. 이 계층에선 어떠한 경로를 거쳐 상대의 컴퓨터까지 패킷을 보낼지 결정하기도 한다. 인터넷의 경우라면 상대 컴퓨터에 도달하는 동안 여러 대의 컴퓨터와 네트워크 기기를 거쳐 상대에게 전달된다. 이러한 여러 선택지 중 하나의 길을 결정하는 것이 네트워크 계층의 역할이다.

### 📌 링크 계층
네트워크에 접속하는 하드웨어적인 면을 다룬다. 운영체제가 하드웨어를 제어하기 때문에 디바이스 드라이버와 네트워크 인터페이스 카드(NIC)를 포함한다. 케이블과 같이 물리적으로 보이는 부분(커넥트 등을 포함한 여러 가지 전송 매체)들도 여기에 포함된다.

<br>

`TCP/IP` 통신의 흐름은 계층을 순서대로 거치게 된다. `HTTP`를 예시로 설명하자면 먼저 송신측 클라이언트의 애플리케이션 계층(HTTP)에서 어느 웹 페이지를 보고 싶다라는 HTTP 리퀘스트를 지시한다. 그 다음에 잇는 트랜스포트 계층(TCP)에서는 애플리케이션 계층에서 받은 데이터(HTTP 메세지)를 통신하기 쉽게 조각내어 안내 번호와 포트 번호를 붙여 네트워크 계층에 전달한다. 네트워크 계층(IP)에서는 수신지 MAC 주소를 추가해 링크 계층에 전달해 송신 준비를 완료한다. 수신측 서버는 링크 계층에서 데이터를 받아들여 순서대로 위 계층에 전달해 애플리케이션 계층까지 도달한다. 애플리케이션 계층에 도달하게 되면 드디어 클라이언트가 발신했던 HTTP 리퀘스트 내용을 수신할 수 있다.

![image](https://user-images.githubusercontent.com/52441697/175770011-a2875589-a1bb-4af0-a8b3-5644a32d4253.png)

송신 과정에서 각 계층을 거칠 때 헤더에 필요한 정보를 추가한다. 반대로 수신 측에선 각 계층을 거칠 때마다 사용한 헤더를 삭제한다. 이렇게 정보를 감싸는 것을 `캡슐화`라고 부른다.

<br>

다음으론 `HTTP`와 관계가 깊은 프로토콜 3가지에 대해 알아보자.
- 배송을 담당하는 `IP`
- 신뢰성을 담당하는 `TCP`
- 이름 해결을 담당하는 `DNS`

<br>

### 📌 배송을 담당하는 IP
`IP(Internet Protocol)`는 네트워크 계층에 해당된다. `IP`의 역할은 개개의 패킷을 상대방에게 전달하는 것이다. 이 전달엔 여러 요소가 필요한데 그 중 핵심 요소는 IP 주소와 MAC(Media Access Control Address) 주소이다. IP 주소는 각 노드에 부여된 주소를 가리키고 MAC 주소는 각 네트워크 카드에 할당된 고유 주소이다. IP 주소는 MAC 주소와 결부되며 IP 주소는 변경 가능하지만 MAC 주소는 변경할 수 없다.

IP 통신은 여러 컴퓨터와 네트워크 기기를 거쳐 상대방에게 도착하는데 이 과정에서 MAC 주소에 사용해 다음 목적지를 찾는다. 이때 `ARP(Address Resolution Protocol)`이라는 프로토콜이 사용된다. `ARP`는 주소를 해결하기 위한 프로토콜 중 하나인데 수신지의 IP 주소를 바탕으로 MAC 주소를 조사할 수 있다.

![image](https://user-images.githubusercontent.com/52441697/175808498-912f98e3-1a53-43df-8b32-c29b3699b206.png)

이런 식으로 중간 목적지를 거쳐 가는 과정 속 컴퓨터와 라우터 등 네트워크 기기는 최종 목적지가 아닌 다음 목적지만을 알고 있으며 이런 시스템을 `라우팅`이라고 부른다. 결국 어떠한 컴퓨터와 네트워크 기기도 인터넷 전체를 상세하게 파악하고 있지는 못한다는 것이다.

### 📌 신뢰성을 담당하는 TCP
`TCP`는 트랜스포트 층에 해당하며 신뢰성 있는 바이트 스트림 서비스를 제공한다. 바이트 스트림 서비스란 용량이 큰 데이터를 보내기 쉽게 TCP 세그먼트 단위 패킷으로 작게 분해해 관리하는 것을 말한다. 결국 `TCP`는 대용량의 데이터를 보내기 쉽게 작게 분해해 전달하고, 정확하게 도착했는지 확인하는 역할을 담당한다.

상대에게 정확하게 데이터를 보내기 위해 `TCP`는 `쓰리웨이 핸드셰이킹(three way handshaking)`이라는 방법을 포함해 다양한 시스템을 사용한다. `쓰리웨이 핸드셰이킹` 방법은 패킷을 보내고, 패킷이 보내졌는지 여부를 상대에게 확인하는 과정도 포함된다. 여기서 `SYN`와 `ACK`이라는 TCP 플래그를 사용한다. 송신측에서는 최초 `SYN` 플래그로 상대와의 연결과 동시에 패킷을 전달하고 수신측에서는 `SYN/ACK` 플래그로 패킷을 수신했다는 사실을 전달한다. 마지막으로 송신측이 `ACK` 플래그를 보내 패킷 교환 완료를 알린다. 

이러한 과정 중 어디선가 통신이 끊어지게 되면 `TCP`는 다시 같은 방법으로 패킷을 재전송한다.

![image](https://user-images.githubusercontent.com/52441697/175499805-0e11b3bc-1e7b-4bf8-ac1e-7098a3019aa4.png)

### 📌 이름 해결을 담당하는 DNS
`DNS(Domain Name System)`은 `HTTP`와 같이 애플리케이션 계층 시스템에서 도메인 이름과 IP 주소 이름 확인 기능을 제공한다. 컴퓨터는 IP 주소와는 별도로 호스트 이름과 도메인 이름을 붙일 수 있으며 사용자는 숫자의 나열인 IP 주소 대신 영어와 숫자로 표기된 도메인 이름을 사용해 상대 컴퓨터를 지정하는 것을 선호한다. 이 문제를 해결하기 위해 `DNS`는 도메인 이름에서 IP 주소를 조사하거나 IP 주소에서 도메인 이름을 조사하는 기능을 제공한다.

<br>

전체 흐름을 정리하면 다음 그림과 같다.

![image](https://user-images.githubusercontent.com/52441697/175754943-1663084f-21fc-411a-a542-bd85915f08e3.png)

<br>

## 📑 URI & URL
`URI`가 `URL`의 상위개념으로 `URI`는 Uniform Resource Identifier(통합 자원 식별자), `URL`은 Uniform Resource Locator(통합 자원 위치), `URN`은 Uniform Resource Name(통합 자원 이름)를 의미한다.

### 📌 URI
`URI`(Uniform Resource Identifier, 통합 자원 식별자)는 인터넷에 있는 자원을 나타내는 유일한 주소이다. `URI`의 존재는 인터넷에서 요구되는 기본조건으로서 인터넷 프로토콜에 항상 붙어 다닌다. `URI`의 하위 개념으로 `URL`, `URN`이 있다

### 📌 URL
`URL`(Uniform Resource Locator, 문화어: 파일식별자, 유일자원지시기)은 네트워크 상에서 자원이 어디 있는지를 알려주기 위한 규약이다. 즉, 컴퓨터 네트워크와 검색 메커니즘에서의 위치를 지정하는, 웹 리소스에 대한 참조이다. 흔히 웹 사이트 주소로 알고 있지만, `URL`은 웹 사이트 주소뿐만 아니라 컴퓨터 네트워크상의 자원을 모두 나타낼 수 있다. 그 주소에 접속하려면 해당 `URL`에 맞는 프로토콜을 알아야 하고, 그와 동일한 프로토콜로 접속해야 한다.

### 📌 URN
`URN`(Uniform Resource Name, 통합 자원 이름)은 urn:scheme을 사용하는 `URI`를 위한 역사적인 이름이다. `URN`은 영속적이고, 위치에 독립적인 자원을 위한 지시자로 사용하기 위해 1997년도 RFC 2141 문서에서 정의되었다.

![image](https://user-images.githubusercontent.com/52441697/175769289-a57aef0c-8a96-4dcb-865c-1e110cf305e2.png)
![image](https://user-images.githubusercontent.com/52441697/175769841-912b209c-63f1-4bf3-93bf-4435d90cc249.png)

<br>

<hr>
참조 : 
https://velog.io/@jch9537/URI-URL
