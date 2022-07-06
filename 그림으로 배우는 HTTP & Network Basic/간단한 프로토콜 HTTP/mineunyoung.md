# CHAPTER2
## _간단한 프로토콜 HTTP_
![image](https://user-images.githubusercontent.com/52441697/177045299-01365fb4-7961-43c8-b6d8-490b85f2e586.png)

- 💡 [Request/Response 메세지](#-requestresponse-메세지)
- ✨ [HTTP 메소드](#-http11-메소드)
- 🍪 [Cookie 활용 상태 관리](#-쿠키를-사용한-상태-관리)
<br>

## 📑 Request/Response 메세지

HTTP 프로토콜에서는 반드시 한 쪽은 리소스를 요청하는 클라이언트, 다른 한 쪽은 리소스를 제공하는 서버의 역할을 담당하며 반드시 클라이언트 측에서 `Request`를 보내고 서버 측에서 `Response`가 되돌아 온다.
> 항상 클라이언트 측으로부터 통신이 시작된다.

<br>

### 📌 Request 메세지 구성
```
POST /form/entry HTTP /1.1
Host: hackr.jp
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Content-Length: 16

name=ueno&age=37
```
| ex | name | desc |
| - | - | - |
|`POST`|메소드|서버에 요구하는 종류|
|`/form/entry`|Request URI|요구 대상(리소스) 식별|
|`HTTP /1.1`|프로토콜 버전|HTTP 버전 번호, 클라이언트 기능 식별|
|`Host: ... 16`|Request 헤더 필드| |
|`name= ... 37`|엔티티| |

<br>HTTP는 Request URI로 리소스를 식별해 인터넷 상 리소스를 지정한다. 리소스 지정 방법에는 두 가지가 있다.

<br>☝ 모든 URI를 Request URI에 포함하는 방법
```
GET http//hackr.jp/index/htm HTTP/1.1
```
✌ Host 헤더 필드에 네트워크 로케이션을 포함하는 방법
```
GET /index.html HTTP/1.1
Host: hackr.jp
```

<br>

### 📌 Response 메세지 구성
```
HTTP /1.1 200 OK
Date: Tue, 10 Jul 2012 06:50:15 GMT
Content-Length: 362
Content-Type: text/html

<html>
...
```
| ex | name | desc |
| - | - | - |
|`HTTP /1.1`|프로토콜 버전|서버의 HTTP 버전|
|`200 OK`|상태 코드 및 프레이즈|리퀘스트 처리 결과 상태 코드 및 설명|
|`Date ... text/html`|Response 헤더 필드| |
|`<html> ...`|바디|리소스 본체|

<br>

### 📌 Persistent Connections(지속 연결)
초기 HTTP 통신은 아래와 같은 개별 연결 방식이었다.

![image](https://user-images.githubusercontent.com/52441697/177045739-63aa1b2a-4858-4b64-9a12-96f9a601ca86.png)

많은 리소스가 필요한 페이지가 증가하면서 각 리소스를 요청할 때마다 개별 연결 통신이 발생하는 문제가 생겼다.

![image](https://user-images.githubusercontent.com/52441697/177045954-ff979046-0b23-4b2e-903a-77227da2acaf.png)

이를 해결하기 위해 한 쪽이 명시적으로 연결을 종료하지 않는 이상 TCP 연결을 계속 유지시키는 **지속 연결**이 고안되었다.

![image](https://user-images.githubusercontent.com/52441697/177046043-fb2f2071-e193-47df-9a69-80f382b9d708.png)

이러한 **지속 연결**이 TCP 연결+종료의 반복되는 오버헤드를 감소시켜 서버 부하를 경감시키고 HTTP 통신 속도를 개선했다. 또한 지속 연결은 Request를 병렬적으로 나열하는 `파이프라인화`가 가능해 전체 Request 완료 시간을 훨씬 줄일 수 있다.

![image](https://user-images.githubusercontent.com/52441697/177046161-dbde829d-ccd4-4b10-af0f-a7979b3db269.png)


<br><br>

## 📑 HTTP/1.1 메소드
| 메소드 | 설명 | Request Body | Response Body | Idempotent | 비고 |
| - | - | - | - | - | - |
|`GET`|Request URI로 식별된 리소스를 요구|❌|✔|✔| |
|`HEAD`|`GET`과 같은 기능, 메세지 헤더 취득|❌|❌|✔|URI 유효성과 리소스 갱신 시간 확인하는 목적으로 사용된다.|
|`POST`|Body를 통해 데이터 전달 및 처리|✔|✔|❌|주로 신규 리소스 등록, 프로세스 처리 등에 사용한다. 또 다른 메소드로 처리하기 애매한 경우에도 사용된다.|
|`PUT`|파일 전송|✔|✔|✔|자체 인증 기능이 없어 보안 상의 문제 발생 가능성이 있어 일반 웹 사이트에선 사용하지 않는다.|
|`DELETE`|리퀘스트 URI로 지정된 리소스 파일 삭제|❌|✔|✔|PUT과 마찬가지로 자체 인증 기능이 없다.|
|`OPTIONS`|리퀘스트 URI로 지정한 리소스가 제공하고 있는 메소드 문의|optional|✔|✔|서버가 허용하는 메소드를 알려준다. e.g. Request: `OPTIONS * HTTP /1.1 Host: www.hackr.jp`<br>Response: `HTTP /1.1 200 OK Allow: GET, POST. HEAD, OPTIONS`|
|`TRACE`|대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행|❌|✔|✔|거의 사용되지 않는다.|
|`CONNECT`|프록시에 터널링 요구|✔|✔|❌|프록시에 터널 접속 확림을 요함으로써 TCP 통신을 터널링 시키기 위해 사용한다. 주로 SSL, TLS 등 프로토콜로 암호화된 것을 터널링 시키기 위해 사용한다.|
|`LINK`|리소스 간 링크 관계 확립|-|-|-|HTTP /1.1에서 폐기되었다.|
|`UNLINK`|링크 관계 삭제|-|-|-|HTTP /1.1에서 폐기되었다.|

**Idempotent**란 동일한 요청을 여러 번 보내도 한 번 보내는 것과 같은 결과를 갖는 지 여부를 의미한다. 외부 요인으로 중간에 리소스가 변경되는 것을 고려하지 않고 해당 요청을 기준으로 고려한다.
```
DELETE /members/100 → 200
DELETE /members/100 → 404
```
`DELETE`를 여러 번 호출하면 응답 코드는 달라질 수 있지만, 100번 member가 삭제된 것은 동일하다.

<br>마지막으로, 보안상의 이유로 대부분의 웹 서버가 `GET`,`POST` 2개 또는 `OPTIONS` 포함 3개만을 허용한다.

<br>`OPTIONS`는 백엔드에서 직접 구현하는 메소드가 아닌 서버 자체가 허용하고 있는 메소드들을 알려주는 방식으로 동작한다(커스텀 가능).

<br><br>

## 📑 쿠키를 사용한 상태 관리
HTTP는 상태를 유지하지 않는 stateless 프로토콜이기 때문에 이전 Request, Response에 대한 정보를 가지고 있지 않다. 이렇게 설계한 이유는 많은 데이터를 빠르고 확실하게 처리하는 범위성을 확보하기 위함이며 이렇게 설계함으로써 서버의 CPU나 메모리 같은 리소스 소비를 억제할 수 있는 장점을 가지고 있다. 

하지만 과거 상태를 근거로 현재 Request를 처리해야하는 로그인, 인증 상태 관리 등 stateless로 처리하기 어려운 일이 증가했다. 이를 해결하기 위해 `쿠키(Cookie) 시스템`이 도입되었다. `쿠키 시스템`을 통해 HTTP 통신도 상태 지속 관리가 가능해진 것이다.

`쿠키 시스템`이란 Request와 Response에 특정 정보를 추가해 클라이언트의 상태를 파악하기 위한 시스템으로 쿠키는 Response로 보내진 `Set-Cookie`라는 헤더 필드에 의해 클라이언트에 보존된다. 보존된 쿠키는 클라이언트가 같은 서버로 Request를 보낼 때 자동으로 함께 송신되어 서버가 이를 확인해 어느 클라이언트가 접속했는지 체크하고 이에 대한 기록을 확인해 상태를 파악할 수 있게 해준다.

<br>

1️⃣ **Request** 
```
GET /reader/ HTTP /1.1
Host: www.youngjin.com
* 헤더 필드에 쿠키는 없다
```
쿠키를 가지고 있지 않은 상태

<br>

2️⃣ **Response** 
```
HTTP /1.1 200 OK
Date: Thu, 12 Jul 2012 07:12:20 GMT
Server: Apache
<Set-Cookie: sid=1342077140226724; path=/;expires=Wed, => 10-Oct-12 07:12:20 GMT>
Content-Type: text/plain; charset=UFT-8
```
서버가 쿠키를 발행

<br>

3️⃣ **Request**
```
GET /image/ HTTP /1.1
Host: www.youngjin.com
Cookie: sid=1342077140226724
```
보관하고 있던 쿠키를 자동 송신

<br><br>

<hr>
참조 : 
https://kyun2da.dev/CS/http-%EB%A9%94%EC%86%8C%EB%93%9C%EC%99%80-%EC%83%81%ED%83%9C%EC%BD%94%EB%93%9C/
https://girawhale.tistory.com/66
