# 6장 HTTP 헤더 
## 6.1 HTTP 메시지 헤더
- HTTP 프로토콜의 리퀘스트와 리스폰스는 반드시 메시지 헤더가 포함되어 있다. 
- 메시지 헤더 : 클라이언트와 서버 처리에 필요한 주요 정보 
- 메시지 바디 : 사용자와 리소스를 필요로하는 정보

## 6.2 HTTP 헤더 필드
### 6.2.1 HTTP 헤더 필드는 중요한 정보를 전달한다. 
- HTTP 헤더필드는 리퀘스트, 리스폰스에도 사용되고 있고, 중요한 정보를 전달하는 역할을 담당
- 메시지 `바디의 크기`나 사용하고 있는 `언어`, `인증 정보` 등을 브라우저나 서버에 제공하기 위해 사용
- 헤더 필드는 `부가적인 정보`를 다루는 일이 많다.</br></br>

### 6.2.2 HTTP 헤더 필드의 구조</br></br> 
콜론 ":"으로 나뉘어져 있다.    

    헤더 필드 명 : 필드 값
  
💚예시      

    Content-Type:text/html 

HTTP 헤더필드는 여러 개의 필드 값을 가질 수 있다.    

    Keep-Alive:timeout=15, max=100

### 6.2.3 4종류의 HTTP헤더 필드

- 일반적 헤더 필드(General Header Fields)
    - 리퀘스트와 리스폰스 메시지 둘다 사용 
- 리퀘스트 헤더 필드(Request Header Fields)
    - 클라이언트 -> 서버 리퀘스트의 부가적 정보, 클라이언트 정보, 리스폰스 콘텐츠에 관한 우선 순위 부가
- 리스폰스 헤더필드(Response Header Fields)
    - 서버 -> 클라이언트 리스폰스 정보, 서버 정보, 클라이언트의 추가 정보 요구 부가
- 엔티티 헤더 필드(Entity Header Fields)
    - 엔티티에 사용되는 헤더로 콘텐츠 갱신 시간, 엔티티에 관한 정보 부가

### 6.2.4 HTTP/1.1 헤더 필드 일람
표를 추가해야할지 사진을 추가할지 고민,,, 굳이 넣어야하나

### 6.2.5 HTTP/1.1 이외의 헤더 필드
- Set-Cookie, Content-Disposition 같이, RFC에 정의되어 폭 넓게 사용되고 있다.
- 비표준 헤더 필드는 RFC4229 HTTP Header Field Registrations에 정리

### 6.2.6 End-to-end 헤더와 Hop-by-hop 헤더 
- End-to-end 헤더
    - 리퀘스트나 리스폰스의 최종 수진자에게 전송
    - 캐시에서 구축된 리스폰스가 보존되어야 하고, 다시 전송되지 않으면 안되도록 되어 있다. 
- Hop-by-hop 헤더
    - 한 번 전송에 대해서만 유효하고 캐시와 프록시에 의해서 전송되지 않는 것도 있다.
    - HTTP/1.1과 그 이후에서 사용되는 Hop-by-hop 헤더는 Connection헤더 필드에 열거해야 한다.
- End-to-end 헤더 종류
    - Connection
    - Keep-Alive
    - Proxy-Authenticate
    - Proxy-Authorization
    - Trailer
    - TE
    - Transfer-Encoding
    - Upgrade
    
## 6.3 HTTP/1.1 일반 헤더 필드 
- 일반 헤더 필드 : 리퀘스트 메시지와 리스폰스 메시지 양쪽에서 사용되는 헤더

### 6.3.1 Cache-Control
- 디렉티브로 불리는 명령을 사용하여 캐싱 동작을 지정
- 지정한 디렉티브에는 파라미터가 있는 것과 없는 것도 있으며 여러 개의 디렉티브를 지정하는 경우 콤마 ","로 구분한다.
- Cache-Control헤더 필드의 디렉티브는 리퀘스트 및 리스폰스 할 때 사용할 수 있다. 

💚예시 

        Cache-Control: private, max-age=0, no-cache

- Cache-Control 디렉티브 알람
    - 사용 가능한 디렉티브를 리퀘스와 리스폰스로 나눠서 다음과 같이 나타낸다. 
    
    💚캐시 리퀘스트 디렉티브    </br></br>

    | 디렉티브 | 파라미터 | 설명 |
    | :----: | :---: | :------- |
    | no-cache | 없음 | 오리진 서버에 강제적인 재검증 |
    | no-store | 없음 | 캐시는 리퀘스트, 리스폰스의 일부분을 보존해서는 안됨 |
    | max-age=[초] | 필수 | 리스폰스의 최대 age값|
    | max-state=[초] | 생략 가능 | 기한이 지난 리스폰스를 수신 |
    | min-fresh=[초] | 필수 | 지정한 시간 이후에 변경된 리스폰스를 보냄 |
    | no-transform | 없음 | 프록시는 미디어 타입을 변환해서는 안됨 |
    | only-if-cahced | 없음 | 캐시에서 리소스를 취득 |
    | cache-extension | - | 새로운 디렉티브를 위해서 토큰 | 

    💚캐시 리스폰스 디렉티브    
    | 디렉티브 | 파라미터 | 설명 |
    | :----: | :---: | :------- |
    | public | 없음 | 어딘가에 리스폰스 캐시가 있음 |
    | private | 생략 가능 | 특정 유저에 대해서만 리스폰스 |
    | no-cache | 생략 가능 | 유효성의 재확인 없이는 캐시는 사용해서는 안됨 |
    | no-store | 없음 | 캐시는 리퀘슽, 리스폰스의 일부분을 보존해서는 안됨 |
    | no-transtorm | 없음 | 프로시는 미디어 타입을 변경해서는 안됨 |
    | must-revaildate | 없음 | 캐시 가능하지만 오리진 서버에 리소스의 재확인을 요구 |
    | proxy-revaildate | 없음 | 중간 캐시 서버에 대해서 캐시했던 리스폰스의 유효성의 재확인을 요구 |
    | max-age=[초] | 필수 | 리스폰스의 최대 age값 |
    | s-maxage=[초] | 필수 | 공유 캐시 서버의 리스폰스 최대 age값 |
    | cache-extension | - | 새로운 디렉티브를 위한 토큰 |

    1. public 디렉티브 : `다른 유저`에게도 돌려 줄 수 있는 캐시를 해도 좋다는 것을 명시적으로 나타냄    
    💚예시 

            Cache-Control: public

    2. private 디렉티브 : `특정 유저만`을 대상으로하고 있다는 것을 나타냄, 캐시서버는 특정 유저를 위해서 리소스를 캐시할 수 있지만, 다른 유저로부터 같은 리퀘스트가 온다고 하더라도 그 캐시를 반환해서는 안된다.   
    💚예시   

            Cache-Control: private

    3. no-cache 디렉티브 : 캐시로부터 오래된 리소스가 반환되는 것을 막기 위해 사용, 중간 캐시 서버가 오리진 서버까지 리퀘스트를 전송해야한다.    
    💚예시

            Cache-Control: no-cache
    
    4. no-store 디렉티브 : 리퀘스트, 리스폰스에 기밀 정보가 포함되어 있음을 나타냄, 캐시는 로컬에 저장해서는 안된다는 지정   
    💚예시

            Cache-Control: no-store

    5. s-maxage 디렉티브 : 여러 유저가 이용할 수 있는 공유 캐시 서버에만 적용된다. Expires 헤더 필드와 max-age 디렉티브는 무시된다.   
    💚예시

            Cache-Control: s-maxage=604800 (단위 : 초)
    
    6. max-age 디렉티브
        - 클라이언트 리퀘스트 : 지정되었던 값보다 새로운 경우에는 캐시되었던 리소스를 받아들일 수 있다. 지정된 값이 0이면 캐시 서버는 리퀘스트를 항상 오리진 서버에 넘길 필요가 있다. 

        - 서버 리스폰스 : 캐시 서버가 유효성의 재확인을 하지 않고 리소스를 캐시에 보존해 두는 최대 시간

        - HTTP/1.1 캐시 서버 : 동시에 Expire 헤더 필드가 사용된 경우, max-age를 우선으로 지정하고 Expire 헤더필드를 무시한다. 

        - HTTP/1.0 캐시 서버 : max-age < Expire 헤더필드(우선)

    7. min-fresh 디렉티브 : 캐시된 리소스가 적어도 지정된 시간은 최신 상태의 것을 반환하도록 캐시 서버에 요구한다.  아래의 예시처럼 60초로 지정되어 있는 경우 60초 지난 리소스를 리스폰스로 반환해서는 안된다.    
    💚예시

            Cache-Control: min-fresh=60 (단위 : 초) 

    8. max-state 디렉티브 : 캐시된 리소스의 유효 기간이 끝났더라도 받아들일 수 있음을 나타냄 유효기간이 지난 후로부터 지정 시간 내라면 받아 들인다는 뜻을 서버에 전달 

    9. only-if-cached 디렉티브 : 캐시 서버에서 리스폰스의 리로드 유효성을 재확인하지 않도록 요구. 캐시 서버가 로컬 캐시로부터 응답할 수 없는 경우 "504 Gateway Timeout" 상태를 반환한다. 

    10. must-revalidate 디렉티브 : 리스폰스의 캐시가 현재도 유효한지 아닌지의 여부를 오리진 서버에 조회를 요구한다. 프록시가 오리진 서버에 도달할 수 없고, 리소스를 다시 요구할 수 없는 경우에는 캐시는 클라이언트에 504를 반환한다. 리퀘스트에서 max-state 디렉티브를 사용하고 있더라도 무시한다. 

    11. Proxy-revalidate 디렉티브 : 모든 캐시 서버에 대해서 이후의 리퀘스트로 해당 리스폰스를 반환할 때는 반드시 유효성 재확인을 하도록 요구   

    12. no-transform 디렉티브 : 리퀘스트와 리스폰스의 캐시가 엔티티 바디의 미디어 타입을 변경할 수 없다. 캐시 서버에 의해서 이미지가 압축되는 것을 방지할 수 있다. 

    13. cache-extension 토큰 : extension 토큰을 사용하여 디렉티브를 확장할 수 있다. 아래 예시와 같이 community 디렉티브는 cache-control 헤더 필드에는 없지만 extension 토큰에 의해 추가할 수 있다. 만약 추가한 디렉티브를 서버가 이해하지 못할 경우 무시된다.   
    💚예시

            Cache-Control: private, community="UCI"


### 6.3.2 Connection
- 프록시에 더 이상 전송하지 않는 헤더 필드를 지정   
💚예시   
-> 더 이상 전송하지 않는 헤더 필드 명 지정
<p align="center"><img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/HTTP%20%ED%97%A4%EB%8D%94/part6img/1.PNG"></p>

- 지속적 접속 관리    
HTTP/1.1에서는 지속적 접속이 기본이다. 서버 측에서 명시적으로 접속을 끊고 싶을 경우에 Connection 헤더 필드에 Close라고 지정 


### 6.3.3 Date
- HTTP 메시지를 생성한 날짜, RFC850 포맷과 C라이브러리에 포함되어 있는 asctime() 출력 포맷이 있다. 

### 6.3.4 Pragma
- HTTP/1.0의 후방 호환성만을 위해서 정의되어 있는 헤더 필드, 클라이언트는 캐시된 리소스의 리스폰스를 원하지 않음을 중간서버에 알리기 위해 사용, 현실적으로 거의 사용하지 않는다.   

        Pragma: no-cache 

### 6.3.5 Trailer
- 메시지 바디 뒤에 기술되어 있는 헤더 필드를 미리 전달
- HTTP/1.1에 구현, 청크 전송 인코딩을 사용하고 있는 경우에 사용 가능

        HTTP/1.1 200 OK
        Date: Tue, Jul 2012 04:40:56 GMT
        ...
        Transfer-Encoding: chunked
        Trailer: Expire

        ....메시지 바디...
        Expires: Tue, 28 Sep 2004 23:59:59 GMT

### 6.3.6 Transfer-Encoding
- 메시지 바디의 전송 코딩 형식을 지정하는 경우, 청크 전송만 정의되어 있다. 

### 6.3.7 Upgrade
- HTTP및 다른 프로토콜의 새로운 버전이 통신에 이용되는 경우 사용
- 지정하는 대상이 전혀 다른 통신 프로토콜이여도 상관없다. 


### 6.3.8 Via
- 클라이언트와 서버 간의 리퀘스트 혹인 리스폰스 메시지의 경로를 알기 위해 사용
- Via 헤더 필드는 전송된 메시지의 추적과 리퀘스트 루프의 회피 등에 사용되기 때문에 프록시를 경유하는 경우 반드시 부가해야한다. 
<p align="center"><img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/HTTP%20%ED%97%A4%EB%8D%94/part6img/2.PNG"></p>

### 6.3.9 Warning
- HTTP/1.0 리스폰스 헤더(Retry-After)가 HTTP/1.1에서 변경된 것으로, 리스폰스에 대한 추가 정보를 전달   

| 코드 | 경고문 | 설명 |
| :---: | :---: | :-------- |
| 110 | Response is state | 프록시가 유효기한이 지난 리소스를 반환했다. |
| 111 | Revalidation failed | 프록시가 리소스의 유효성 재확인에 실패했다.</br>(서버에 도달할 수 없는 등)|
| 112 | Disconnection operation | 프록시가 네트워크로부터 고의로 끊겨 있다. |
| 113 | Heuristic expiration | 리스폰스가 24시간이상 경과하고 있는 경우</br>캐시의 유효기간을 24시간 이상으로 설정하고 있는 경우 |
| 199 | Miscellaneous warning | 임의의 경고문 |
| 214 | Transformation appiled | 프록시가 인코딩과 미디어 타입 등에 대응해서 무언가의 처리를 한 경우 |
| 299 | Miscellaneous persistent warning | 임의의 경고문 |

💚예시

        Warning: 133 gw.hackr.ip:8000 "Heuristic expiration"Tue, 03 Jul => 2012 05:09:44 GMT

        Warging: [경고 코드][경고한 호스트:포트 번호]"[경고문]" ([날짜])
