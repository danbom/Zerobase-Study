# 제 2장 간단한 프로토콜 HTTP

## 2.1 HTTP는 클라이언트와 서버 간에 통신을 한다. 
http는 클라이언트와 서버의 역할을 명확하게 정확하게 정하고 구별

## 2.2 request와 response를 교환하여 성립
서버는 request를 수신하지 않으면 response가 발생하지 않는다.
<p align="center"><img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/%EA%B0%84%EB%8B%A8%ED%95%9C%20%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C%20HTTP/img/1.PNG">
</p>

   
### 1. 클라이언트 -> 서버 (request 메세지)   
  <p align="center"><img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/%EA%B0%84%EB%8B%A8%ED%95%9C%20%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C%20HTTP/img/2.PNG">
  </p>
    리퀘스트 메시지 : 메소드, URI, 프로토콜 버전, 옵션 리퀘스트 헤더 필드, 엔티티   


### 2. 서버 -> 클라이언트(response 메세지)   
  <p align="center"><img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/%EA%B0%84%EB%8B%A8%ED%95%9C%20%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C%20HTTP/img/3.PNG">
  </p>  




## 2.3 HTTP는 상태를 유지하지 않는 프로토콜

Http는 request와 response를 교환하는 동안에 status 관리를 하지 않는 stateless 프로토콜이다.   
http프로토콜 레벨에서 이전에 보냈던 리퀘스트나 이미 되돌려준 리스폰스에 대해 알 수 없다.   
데이터를 매우 빠르고 확실하게 처리하는 범위성을 확보한 간단한 설계   
웹이 진화함에 따라 상태를 유지해야하는 필요성 발생( ex : 로그인 상태) -> Cookie 도입   


## 2.4 request URI로 리소스를 식별

HTTP는 URI를 사용하여 인터넷 상의 리소스를 지정하고 호출한다.   
request URI 지정 방법

#### 1.모든 URI를 request URI에 포함
   GET htttp://mond.com/htm HTTP/1.1

#### 2. Host 헤더 필드에 네트워크 로케이션을 포함
  GET /index.htm HTTP /1.1
  Host: www.mond.com

#### 3. 특정 리소스가 아닌 서버 자신에게 request를 송신하는 경우
  OPTIONS * HTTP/1.1  

## 2.5 서버에 임무를 부여하는 HTTP 메소드

### 💙 GET : 리소스 획득
request URI로 식별된 리소스를 요청   
소스가 text이면 그대로 반환 GGI와 같은 프로그램이면 실행해서 출력된 내용을 돌려준다.   

### 💙 POST : 엔티티 전송
  GET으로 엔티티를 전송할 수 있지만 자주 사용하지 않고 일반적으로 POST를 사용한다.      

### 💙 PUT : 파일 전송
  FTP에 의한 파일 업로드와 같이, request에 포함된 엔티티를 리퀘스트 URI로 지정한 곳에 보존하도록 요구    

### 💙 HEAD : 메시지 헤더 취득
  GET과 비슷, 메시지 바디는 돌려주지 않는다.      
  URI 유효성과 리소스 갱신 시간을 확인하는 목적으로 사용   

### 💙 DELETE : 파일 삭제
  PUT과 반대로 동작 request URI로 지정된 리소스의 삭제를 요구   
  PUT메소드와 같이 인증 기능이 없기 때문에 일반적인 웹사이트에서 사용 X

### 💙 OPTIONS : 제공하고 있는 메소드 문의
  지정한 리소스가 제공하고 있는 리소스를 알아보기 위해      
  OPTIONS요청은 브라우저가 서버에게 지원하는 옵션들을 미리 요청하고 허가된 요청만 전송하기 위해 많이 사용한다.    

### 💙 TRACE : 경로 조사
  Web서버에 접속해서 자신에게 통신을 되돌려 받는 루프백을 발생 ( 보통은 사용하고 있지 않아 생략)   
  request를 보낼 때 "Max-Forwards"라는 헤더 필드에 수치를 포함시켜 서버를 통과할 때마다 그 수치를 줄인다.   
  수치가 0이 된 곳을 끝으로 , request를 마지막로 수신한 곳에서 상태 코드 200 OK response를 돌려준다.   
  클라이언트는 TRACE메소드를 사용하여, request를 보낸 곳에 어떤 리퀘스트가 가공되어 있는지 알 수 있다.   
  #### 보안 상의 문제가 있어 보통은 사용되지 않는다.😅   

### 💙 CONNECT : 프록시에 터널링 요구

  프록시에 터널 접속 확립을 요구함으로써, TCP 통신을 터널링 시키기 위해 사용      
  주로 SSL, TLS 등의 프로토콜로 암호화 된 것을 터널링 시키기 위해서 사용되고 있다.   
  CONNECT 프록시 서버 : 포트 HTTP버전   
  <p align="center"><img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/%EA%B0%84%EB%8B%A8%ED%95%9C%20%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C%20HTTP/img/4.PNG">
  </p>


## 2.6 메소드는 리소스에 어떤 행동을 원하는지 지시를 내린다.
  - LINK와 UNLINK는 HTTP /1.1에서 폐기되어 제공하지 않는다.   

    | 메소드 | 설명 | HTTP 버전|
    | :---: | :---: | :---: |
    | GET | 리소스 취득| 1.0 1.1|
    | POST | 엔티티 바디 전송 | 1.0 1.1|
    | PUT | 파일 전송 | 1.0 1.1|
    | HEAD| 메시지 헤더 취득 | 1.0 1.1|
    | DELETE| 파일 삭제 |1.0 1.1|
    | OPTIONS| 서포트하고 있는 메소드 문의 | 1.1 |
    | TRACE| 경로 조사 | 1.1 |
    | CONNECT| 프록시에의 터널링 요구 | 1.1 |
    | LINK| 리소스 간에 링크 관계를 확립 |1.0 |
    | UNLINK| 링크 관계 삭제 | 1.0 |

## 2.7 지속 연결로 접속량을 절약 
- HTTP 초기 버전에서는 HTTP 통신을 한 번 할 때마다 TCP에 의해 연결과 종료를 해야했었다.
- 초기 통신에서는 작은 사이즈의 텍스트를 보내는 정도였기 때문에 문제가 없었다. 
- HTTP가 널리 보급되고, 다량의 이미지를 포함하는 문서들이 늘어났다.   
예를 들어서 한개의 HTML 문서에 여러개있는 이미지를 회득하기 위해서 여러번의 리퀘스트를 송신   
매번 TCP연결과 종료를 하게 되는 쓸모없는 일이 발생되어 통신량이 늘어나는 단점이 발생
<p align="center"><img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/%EA%B0%84%EB%8B%A8%ED%95%9C%20%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C%20HTTP/img/5.PNG">
</p>

  ### 2.7.1 지속연결
  - 한 쪽이 연결을 종료하지 않는 이상 TCP연결을 계속 유지   
    
  ### 😃 장점
  - TCP 커넥션의 연결과 종료가 반복되는 오버헤드를 줄여 서버의 부하를 경감
  - 오버헤드를 줄인만큼 웹페이지가 빨라짐   
  - HTTP/1.1에서는 표준이지만 HTTP/1.0은 일부만 지원

  ### 2.7.2 파이프라인화
  - 지속 연결하여 여러 리퀘스트를 보낼 수 있도록 파이프라인화가 가능
  - response를 기다리지 않고 바로 request를 보낼 수 있다.
  - 여러 리퀘스트를 병행해서 보내는 것이 가능
  <p align="center"><img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/%EA%B0%84%EB%8B%A8%ED%95%9C%20%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C%20HTTP/img/6.PNG">
  </p>

## 2.8 쿠키를 사용한 상태 관리
- HTTP는 stateless protocol이다.

  ### 😃 장점
  상태를 유지하지 않아 CPU나 메모리의 리소스 낭비 방지   
  단순 프로토콜이라 다양한 곳에서 이용 가능

  ### 🙄 단점
  인증이 필요한 웹페이지에서 상태관리하기가 어렵다.   
  로그인 상태 확인을 위해 페이지를 이동할때마다 로그인 정보나 매개 변수를 통해 로그인 상태를 관리해야한다.

### 🍪 Cookie 도입 
- request와 response에 Cookie 정보를 추가해서 클라이언트의 상태 파악 및 관리
- 서버에서 보내는 response에서 Set-Cookie라는 헤드 필드에 Cookie를 저장하여 보낸다.
- 그 후 클라이언트가 보내는 request에 자동으로 Cookie 값을 넣어서 보낸다.

  ### 1️⃣ Cookie 없는 Request
  1. 클라이언트가 request 보내기
  2. 서버는 상태관리를 위한 Cookie 생성
  3. 서버가 response + Cookie 로 응답  

  ### 2️⃣ 쿠키를 가지고 있는 Request
  1. request + Cookie
  2. 서버는 Cookie로 상태를 확인 후 response

  ### 💚예제
  1. request
  ```
  GET /medicine/ HTTP /1.1
  Host: www.mond.com
  ```
  2. response + Cookie
  ```
  HTTP /1.1 200 OK
  Date: Thu, 19 Dec 2022 22:22:15 GMT
  Server : Nginx
  <Set-Cookie: sid=7845687452684: path=/:expires=Wed, => 31 Dec 2023 01:20:15 GMT>
  Content-Type: text/plain: charset=UTF-8
  ```
  3. request + Cookie
  ```
  GET /medicine/ HTTP /1.1
  Host: www.mond.com
  Cookie: sid=7845687452684
  ```

  
  



  
  
 

