# 제 1장 웹과 네트워크의 기본에 대해 알아보자

## 개요

- 웹이라는 세계가 어떤 기술로 구성되어 있는지
- HTTP의 탄생과 성장
- 배경의 대해 알게 된다.

## 1.1 웹은 HTTP로 나타낸다.

웹브라우저 주소 입력란에 URL을 입력했을 때 어떻게 해서 웹 페이지가 보여지는 알고 있나요?

클라이언트 → 서버 브라우저 주소 입력란에 URL을 입력하여 어딘가에 송신

<p align="center">
  <img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/%EC%9B%B9%EA%B3%BC%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%EC%9D%98%20%EA%B8%B0%EB%B3%B8%EC%97%90%20%EB%8C%80%ED%95%B4%20%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90/img/%EC%BA%A1%EC%B2%98.png">
</p>


클라이언트 ← 서버 어딘가에서 응답이 돌아오면 웹 페이지가 표시 됨

<p align="center">
  <img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/%EC%9B%B9%EA%B3%BC%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%EC%9D%98%20%EA%B8%B0%EB%B3%B8%EC%97%90%20%EB%8C%80%ED%95%B4%20%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90/img/%EC%BA%A1%EC%B2%98%201.png">
</p>

웹 서버로 부터 리소스라고 불리는 파일 등의 정보를 얻어 페이지를 볼 수 있는 것이다.

클라이언트에서 서버까지 일련의 흐름을 결정하고 있는 것은 웹에서 HTTP(HyperText Transfer Protocol)이라 불리는 프로토콜이다.

프로토콜의 의미는 “**약속**”이다. 웹은 HTTP라는 약속을 사용한 통신으로 이루어져 있다. 

## 1.2 HTTP는 이렇게 태어났고 성장했다.

### 1.2.1 웹은 지식 공유를 위해 고안되었다.

- 1989년 HTTP가 탄생
- 세계 곳곳에 있는 연구자들의 지식 공유를 지원하게 위해 제안
- WWW 구성 기술
    - HTML(HyperText Markup Language) : 문서 기술 언어
    - HTTP : 문서 전송 프로토콜
    - URL(Uniform Resource Locator) : 문서의 주소 지정
- WWW = W3 = Web
- 인터넷의 동의어로 취급하는 사람들이 많지만 인터넷은 TCP/IP 프로토콜로 구현된 통신망이고 월드 와이드 웹은 이더넷을 기반으로 대량의 이미지와 문자를 전송하는 프로토콜이다 .

### 1.2.2 웹이 성장한 시대

- 90년 11월에 세계 최초의 웹 서버와 웹 브라우저가 개발
- 세계 최초의 웹페이지 [http://info.cern.ch/hypertext/WWW/TheProject.html](http://info.cern.ch/hypertext/WWW/TheProject.html)
- 95년 마이크로소프트에서 인터넷 익스플로러 1.0 출시…지금은 사라져 버린
- 웹서버 Apach도 생기고 여러가지 브라우저들도 생김

## 1.3 네트워크의 기본은 TCP/IP

인터넷을 포함하여 일반적으로 사용하고 있는 네트워크는 TCP/IP라는 프로토콜에서 움직이고 있다.  HTTP는 그 중 하나이다. 

### 1.3.1 TCP/IP는 프로토콜의 집합

- 컴퓨터와 네트워크 기기가 상호간에 통신하기 위해서는 서로 같은 방법으로 통신해야한다.
- 어떻게 상대를 찾고, 어떻게 상대에게 이야기를 시작하고, 어떤 언어로 이야기를 하며, 어떻게 이야기를 종료할 것인가에 대한 규칙을 결정해야한다.
- 서로 다른 하드웨어와 운영체제를 가지고 통신하기 위해서는 모든 요소에 규칙 필요.
- 이러한 규칙을 프로토콜이라고 부른다.
- 프로토콜은 케이블 규격, IP주소 지정방법, 떨어진 상대를 찾기위한 방법, 그곳에 도달하는 순서, 웹을 표시하기 위한 순서 등등 이다.
- 이렇게 인터넷과 관련된 프로토콜을 모은 것들을 TCP/IP라고 한다.

<p align="center">
  <img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/%EC%9B%B9%EA%B3%BC%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%EC%9D%98%20%EA%B8%B0%EB%B3%B8%EC%97%90%20%EB%8C%80%ED%95%B4%20%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90/img/%EC%BA%A1%EC%B2%98%202.png">
</p>

### 1.3.2 계층으로 관리하는 TCP/IP

- 4 Layer
- 계층화로 나누면 사양이 변경 되었을때 해당 계층만 바꾸면 되고, 연결되어 있는 부분만 결정되어 각 계층의 내부는 자유롭게 설계할 수 있다.

<p align="center">
  <img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/%EC%9B%B9%EA%B3%BC%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%EC%9D%98%20%EA%B8%B0%EB%B3%B8%EC%97%90%20%EB%8C%80%ED%95%B4%20%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90/img/%EC%BA%A1%EC%B2%98%203.png">
</p>

### 1.3.3 TCP/IP 통신의 흐름

<p align="center">
  <img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/%EC%9B%B9%EA%B3%BC%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%EC%9D%98%20%EA%B8%B0%EB%B3%B8%EC%97%90%20%EB%8C%80%ED%95%B4%20%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90/img/%EC%BA%A1%EC%B2%98%204.png">
</p>

예시 :

1. 송신측 클라이언트 애플리케이션 계층(HTTP)에서 HTTP Request 지시
2. 트랜스포트 계층(TCP)에서 HTTP message를 통신하기 쉽게 조각내어 안내 번호와 포트 번호부터 네트워크에 전달
3. 네트워크 계층(IP)에서는 수신지 MAC주소를 추가해서 링크 계층에 전달

캡슐화 : 송신 측은 각 계층을 거칠 때마다 해당 계층에 필요한 정보를 헤더로 추가하여 감싼다.

수신 측은 계층을 거칠 때마다 해당 계층마다 사용한 헤더를 삭제 

<p align="center">
  <img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/%EC%9B%B9%EA%B3%BC%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%EC%9D%98%20%EA%B8%B0%EB%B3%B8%EC%97%90%20%EB%8C%80%ED%95%B4%20%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90/img/%EC%BA%A1%EC%B2%98%205.png">
</p>

## 1.4 IP, TCP, DNS

### 1.4.1 배송을 담당하는 IP

- IP(Internet Protocol) 네트워크 계층
- 인터넷을 활용하는 거의 대부분의 시스템이 IP를 사용
- IP주소와는 다르다 IP는 프로토콜의 명칭
- 역할 : 각각의 패킷을 상대방에서 전달. IP주소와 MAC주소가 중요
    - IP주소 : 각 노드에 부여된 주소(논리 주소)
    - MAC주소 : 각 네트워크 카드에 할당된 고유 주소(물리적 주소)
    - IP주소는 변경 가능하지만 MAC주소는 변경할 수 없다.
- 통신은 ARP를 이용하여 MAC주소에서 한다.
    - IP통신은 MAC주소에 의존해서 통신한다.
    - 여러 대의 컴퓨터와 네트워크 기기를 중계해서 상대방 server에 도착한다. 이렇게 중계하는 동안에 다음 중계할 곳의 MAC주소를 사용하여 목적지를 찾아간다. 이때, ARP(Address Resolution Protocol)이라는 프로토콜을 사용한다.
    - ARP는 수신지의 IP주소를 바탕으로 MAC주소를 조사한다.(택배 배송 예시: 어떤길로 가는 지 전체를 알고 있지 않아도 배송한다.)

## 1.4.2 신뢰성을 담당하는 TCP

- TCP(Transfer Control Protocol) 트랜스포트 계층
- 신뢰성 있는 바이트 스트림 서비스를 제공
- 바이스 스트림 서비스 : 용량이 큰 데이터를 보내기 쉽게 TCP 세그먼트라고 불리는 단위 패킷으로 작게 분해하여 관리하는 것
- 쉽게 말하지면, 대용량의 데이터를 보내기 쉽게 작게 분해하여 상대에게 보내고, 정확하게 도착했는지 확인하는 역할
- TCP의 신뢰성은 3-way handshake 방법을 사용한다.
    
    <p align="center">
  <img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/%EC%9B%B9%EA%B3%BC%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%EC%9D%98%20%EA%B8%B0%EB%B3%B8%EC%97%90%20%EB%8C%80%ED%95%B4%20%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90/img/%EC%BA%A1%EC%B2%98%206.png">
</p>
    

자세한 내용은 저의 블로그를 한번 보는걸 추천

[https://a-mond.tistory.com/24](https://a-mond.tistory.com/24)

## 1.5 이름 해결을 담당한는 DNS

- DNS(Domain Name System)는 HTTP와 같이 응요 계층 시스템에서 도메인 이름과 IP주소 이름 확인을 제공
- 사람 : IP주소를 지정하는 것 보다 영어나 숫자 등으로 표기해 컴퓨터 이름을 지정하는 것이 친숙
- 컴퓨터 : 숫자를 나열하는 방법을 더 선호
- IP주소 : domain

## 한눈에 보기

<p align="center">
  <img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/%EC%9B%B9%EA%B3%BC%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%EC%9D%98%20%EA%B8%B0%EB%B3%B8%EC%97%90%20%EB%8C%80%ED%95%B4%20%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90/img/%EC%BA%A1%EC%B2%98%207.png">
</p>
## 1.7 URI와 URL

### 1.7.1 URI는 리소스 식별자

URI : Unifrom Resource Identifiers

- Unifom : 통일된 서식을 결정, 여러 리소스 지정 방법을 구별없이 취급할 수 있다. 새로운 스키마(http, ftp) 도입을 용이하게 한다.
- Resource : 식별 가능한 모든 것, 도큐먼트, 이미지, 일기예보 등 다른 것과 구별할 수 있는 것은 모두 리소스이다.
- Identifier : 식별 가능한 것을 참조하는 오브젝트, ‘식별자’

⇒ 스키마를 나타내는 리소스를 식별하기 위한 식별자

### 1.7.2 URL 포맷

<p align="center">
  <img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/%EC%9B%B9%EA%B3%BC%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%EC%9D%98%20%EA%B8%B0%EB%B3%B8%EC%97%90%20%EB%8C%80%ED%95%B4%20%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90/img/%EC%BA%A1%EC%B2%98%208.png">
</p>

- 스키마 : 사용할 프로토콜을 뜻하며 웹에서는 http, https를 사용한다.
- 자격정보(크리덴셜) : 서버로부터 리소스를 취득하려면 자격정보가 필요ID 와 Password 지정 옵션이 있다.
- 서버 주소 : 완전 수식 형식인 URI에서는 서버 주소를 지정. 주소는 DNS이름이나 IPv4,IPv6 주소를 대괄호로 묶어서 지정
- 서버 포트 : 접속 대상의 포트 번호 지정
- 계층적 파일 패스 : 특정 리소스를 식별하기 위해서 서버 상의 파일 패스를 지정
- 쿼리 문자열 : 파일 패스로 지정된 리소스에 임의의 파라미터를 넘겨주기 위해 쿼리 문자열을 사용하는 옵션
- 프래그멘트 식별자 : 메인 리소스 내에 존재하는 서브 리소스에 접근할 때 이를 식별하기 위한 정보

## URI와 URL의 차이점

URI는 URL의 의미를 가지고 있다. 

Uniform Resource Locator

자원이 실제로 존재하는 **위치**

Uniform Resource Identifier

자원의 위치 뿐만 아니라 자원에 대한 고유 **식별자**

사전에 알아야할 것

우리가 인터넷 환경에서 자원을 식별하기위해 사용하는 2가지 방법

- Path Variable : 특정한 자원을 보여줘야할때 사용
    
    /user/1
    
    /user/2
    
- Query Parameter : 자원들을 필터링해서 보여줄때 사용
    
    /medicien?page=1
    
    /medicine?page=12
    
    /test?name=minyung
    

### 💚예시

1. http://mond.co.kr/index
    
    mond.co.kr에서 index라는 경로를 가르키고 있다.
    
    서버에서 해당 주소에 알맞은 자원을 전송해줄 것이며 자원이는 자원의 실제 위치이므로 URL이다.
    
2. http://monde.co.kr/medicine/123
    
    mond.co.kr에서 123의 ID값을 가지고 있는 자원을 식별하고 있다.
    
    [http://mond.co.kr/medicine](http://mond.co.kr/medicine/Rkwlsms)/ 까지는 자원의 실제 위치이기 때문에 URI임과 동시에 URL이며 끝의 /123부분은 식별자 이므로  
    
    ### 💡URL을 포함한 URI 이다.
    
    <p align="center">
  <img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/%EC%9B%B9%EA%B3%BC%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%EC%9D%98%20%EA%B8%B0%EB%B3%B8%EC%97%90%20%EB%8C%80%ED%95%B4%20%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90/img/img.png">
</p>
    
3. http://mond.co.kr/medicine?page=2
    
    위의 예시와 비슷하게 [monde.co.kr/mdicine까지는](http://monde.co.kr/mdicine까지는)  자원의 실제 위치이므로 URL이라 하 수 있고 뒤의 쿼리 파라미터 식별자이다. 
    
    위의 에시와 같이 URL을 포함한 URI이다.
