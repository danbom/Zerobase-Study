# CHAPTER3
## _HTTP 정보는 HTTP 메세지에 있다_
![image](https://user-images.githubusercontent.com/52441697/178086792-629bb68e-ee03-41da-9558-d223187dec20.png)

- 💡 Message 구조
- ✨ Encoding
- 📣 Multipart
- 🔔 Range Request
- ⭐ Content Negotiation

<br>

## 📑 Message 구조

`HTTP Message`는 복수 행의 데이터로 구성된 텍스트 문자열이며 헤더와 바디는 최초에 나타나는 개행 문자(CR+LF)로 구분된다.
> CR(\r), LF(\n)는 줄바꿈 문자를 의미한다.

![image](https://user-images.githubusercontent.com/52441697/178086920-c3cbedb4-9eab-4766-93ee-c04e8b347c71.png)

![image](https://user-images.githubusercontent.com/52441697/178087090-ca6292ab-5791-4bc5-a6b5-d9d319a520db.png)

### Request Message
"Request HTTP Message"를 의미하며 메소드, Request URI, HTTP 버전을 포함하는 `Request 라인`이 이 `Request Message`의  메세지 헤더에 속한다.

### Response Message
"Response HTTP Message"를 의미하며 Response 결과를 나타내는 상태 코드와 설명, HTTP 버전을 포함하는 `상태 라인`이 이 `Response Message`의  메세지 헤더에 속한다.

Request, Response 메세지에 공통적으로 여러 조건, 속성을 나타내는 각종 헤더 필드가 포함되며 HTTP RFC에 없는 쿠키 등의 헤더 필드가 포함되는 경우도 있다.
> RFC(Request for Comments) 문서는 국제 인터넷 표준화 기구(IETF; Internet Engineering Task Force)에서 관리하는 기술 표준을 의미한다.

<br>

## 📑 Encoding
메세지 : HTTP 통신의 기본 단위, 옥텟 시퀀스(Octet sequence, octet : 8비트)로 구성되고 통신을 통해 전송된다. 메세지 바디의 역할은 리퀘스트/리스폰스에 관한 엔티티 바디를 운반하는 일이다.
엔티티 : 리퀘스트/리스폰스의 페이로드로 전송되는 정보, 엔티티 헤더 필드 + 엔티티 바디로 구성된다.

기본적으로 메세지 바디와 엔티티 바디는 같지만 전송 코딩이 적용된 경우에는 엔티티 바디의 내용이 변하기 때문에 메세지 바디와 달라진다.

HTTP로 데이터를 전송할 때 `Encoding(인코딩)`을 하면 다량의 액세스를 효율 좋게 처리해 전송 효율을 높일 수 있다. 하지만, 컴퓨터에서 인코딩을 처리해야 하기 때문에 CPU 등 리소스를 더 많이 소비한다.

### 콘텐츠 코딩
- 🔑 key: 압축

엔티티에 적용하는 인코딩으로 용량을 줄이기 위해 압축하는 것이다. 이 때, 엔티티의 정보는 유지한 채로 압축한다. `콘텐츠 코딩`된 엔티티는 수신한 클라이언트 측에서 Decoding(디코딩)한다.
주요 콘텐츠 압축 예시엔 gzip(GNU zip), compress(UNIX의 표준 압축), deflate(zlib), identity(인코딩 없음)가 있다.

### 청크 전송 코딩
- 🔑 key: 분해

HTTP 통신에서는 리퀘스트 했던 엔티티 바디의 전송이 완료되지 않으면 브라우저에 표시되지 않는다. 데이터의 사이즈가 큰 경우 엔티티 바디를 작게 분할해 송신하는 기능을 `청크 전송 코딩`이라 부른다. `청크 전송 코딩`은 엔티티 바디를 청크로 분해하고 다음 청크 사이즈를 16진수로 표현해 단락을 표시한다. 엔티티 바디의 끝에는 "0(CR+LF)"를 기록한다.
`청크 전송 코딩`된 엔티티 바디는 수신한 클라이언트 측에서 디코딩한다.

<br>

## 📑 Multipart
메일의 경우 본문과 복수의 첨부 파일을 함께 보낼 수 있다. 이것은 MIME(Multipurpose Interfnet Mail Extensions: 다목적 인터넷 메일 확장 사양)으로 불리는 메일로 여러 다른 데이터를 다루기 위한 기능을 사용하고 있다.
MIME는 이미지 등의 바이너리 데이터를 ASCII 문자열에 인코딩하는 방법과 데이터 종류를 나타내는 방법 등을 규정하고 있다. 이 MIME의 확장 사양에 있는 Multipart(멀티파트)라고 하는 여러 다른 종류의 데이터를 수용하는 방법을 사용하고 있는 것이다.
HTTP도 멀티파트에 대응하고 있어 하나의 메세지 바디 내부에 엔티티를 여러 개 포함시켜 보낼 수 있다. 주로 이미지나 텍스트 파일 등을 업로드할 때 사용되고 있다.

### multipart/form-data
Web 폼으로부터 파일 업로드에 사용된다.
```
Content-Type: multipart/form-data; boundary=AaB03x
--AaB03x
Content-Disposition: form-data; name="field1"
Joe Blow
--AaB03x
Content-Disposition: form-data; name="pics"; filename="file1.txt"
Content-Type: text/plain
... (file1.txt데이터) ...
--AaB03x
```

### multipart/byteranges
상태 코드 206(Partial Content) 리스폰스 메세지가 복수 범위의 내용을 포함할 때 사용된다.
```
HTTP/1.1 206 Partial Content
Date: Fri, 13 Jul 2012 02:45:26 GMT
Last-Modified: Fri, 13 Aug 2007 02:02:20 GMT
Content-Type: multipart/byteranges; boundary=THIS_STRING_SEPARATES

--THIS_STRING_SEPARATES

Content-Type: application/pdf
Content-Range: bytes 500-900/8000

... (지정한 범위의 데이터) ...
--THIS_STRING_SEPARATES

Content-Type: application/pdf
Content-Range: bytes 7000-7999/8000

... (지정한 범위의 데이터) ...
--THIS_STRING_SEPARATES--
```

HTTP 메세지로 멀티파트를 사용할 때에는 Content-Type 헤더 필드르르 사용한다. 멀티파트 각각의 엔티티를 구분하기 위해 "boundary" 문자열을 사용한다. 각 엔티티의 선두에는 "boundary" 문자열 앞에 "--"를 삽입한다. 멀티파트의 마지막에는 그 문자열의 마지막 부분에 "--"를 삽입해서 마무리한다.
멀티파트는 파트마다 헤더 필드가 포함된다. 또한 파트의 중간에 멀티파트를 만드는 것과 같이 파트를 내부에 포함할 수도 있다.

<br>

## 📑 Range Request
요즘처럼 사용자가 광대역의 네트워크를 이용할 수 있기 전에는 대용량의 이미지와 데이터를 다운로드하기가 힘들었다. 왜냐하면 다운로드 중에 커넥션이 끊어지게 되면 처음부터 다시 다운로드를 해야 했기 때문이다. 이러한 문제를 해결하기 위해 일반적인 Resume(리줌)이라는 기능이 필요하게 됐다. 리줌을 통해 이전에 다운로드한 곳에서부터 다운로드를 재개할 수 있었다. 
이 기능을 실현하기 위해 엔티티의 범위를 지정해서 다운로드할 필요가 있다. 이와 같이 범위를 지정해 리퀘스트 하는 것을 `Range Request(레인지 리퀘스트)`라고 부른다.
`레인지 리퀘스트`를 사용하면 전체 10,000 바이트 정도 크기의 리소스에서 5,001~10,000 바이트의 범위(바이트 레인지) 만을 리퀘스트할 수 있다.

![image](https://user-images.githubusercontent.com/52441697/178099329-cefd5a81-41b2-4b94-9dc0-38031d612425.png)

레인지 리퀘스트할 때에는 Range 헤더 필드를 사용해 리소스의 바이트 레인지를 지정한다. 

▪ 5,001 ~ 10,000 바이트
```
Range: bytes = 5001-10000
```

▪ 5,001 바이트 이상
```
Range: bytes = 5001-
```

▪ 처음부터 3,000 바이트까지, 그리고 5,000~7,000 바이트까지의 복수 범위
```
Range: bytes = -3000, 5000-7000
```

레인지 리퀘스트에 대한 리스폰스는 상태 코드 206 Partial Content라는 리스폰스 메세지가 되돌아온다. 또한, 복수 범위의 레인지 리퀘스트에 대한 리스폰스는 multipart/byteranges로 리스폰스가 되돌아온다.
서버가 레인지 리퀘스트에 지원하지 않는 경우에는 상태 코드 200 OK라는 리스폰스 메세지로 완전한 엔티티가 되돌아온다.

<br>

## 📑 Content Negotiation
같은 콘텐츠이지만 여러 개의 페이지를 지닌 웹 페이지가 있다. 예를 들면, 내용은 같지만 영어판/한국어판과 같이 표시되는 언어가 서로 다른 웹 페이지의 경우이다. 
이러한 웹 페이지에서는 영어와 한국어와 같이 서로 다른 언어를 주로 사용하는 브라우저가 같은 URI에 엑세스 할 때에 각각 영어판 웹 페이지와 한국어판 웹 페이지를 표시한다. 이와 같은 구조를 `Content Negotiation(콘텐츠 네고시에이션)`이라고 부른다.

`콘텐츠 네고시에이션`이란 클라이언트와 서버가 제공하는 리소스의 내용에 대해서 교섭하는 것이다. 클라이언트에 더욱 적합한 리소스를 제공하기 위한 구조이다.
`콘텐츠 네고시에이션`은 제공하는 리소스를 언어와 문자 세트, 인코딩 방식을 기준으로 판단하고 있다.
판단 기준은 리퀘스트 메세지에 포함된 다음과 같은 리퀘스트 헤더 필드이다.
- Accept
- Accept-Charset
- Accept-Encoding
- Accept-Language
- Content-Language

### Server-driven Negotiation, 서버 구동형 네고시에이션
서버 측에서 콘텐츠 네고시에이션을 하는 방식이다. 서버 측에서 리퀘스트 헤더 필드의 정보를 참고해 자동적으로 처리한다. 단지, 브라우저가 보내는 정보를 근거로 하기 때문에 유저에게 정말로 적절한 것이 선택되었다고 할 수 없다.

### Agent-driven Negotiation, 에이전트 구동형 네고시에이션
클라이언트 측에서 콘텐츠 네고시에이션을 하는 방식이다. 브라우저에 표시된 선택지 중에서 유저가 수동으로 선택한다. 자바스크립트 등을 사용해 웹 페이지에서 자동적으로 이것을 정하는 것도 있따. 예를 들면, OS의 종류나 브라우저의 종류 등에 의해서 PC용과 스마트폰용의 웹 페이지를 자동으로 전환하는 것이 이에 해당한다.

### Transparent Negotiation, 트랜스페어런트 네고시에이션
서버 구동형과 에이전트 구동형을 혼합한 것으로 서버와 클라이언트가 각각 콘텐츠 네고시에이션을 하는 방식이다.

<hr>
참조 : 
https://velog.io/@koseungbin/HTTP-Message
