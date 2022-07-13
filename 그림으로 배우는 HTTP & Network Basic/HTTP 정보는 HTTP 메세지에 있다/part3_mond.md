# 제 3장 HTTP정보는 HTTP 메세지에 있다.

## 3.1 HTTP 메시지
- HTTP에서 교환하는 정보 = HTTP 메시지
- Request 메시지 : 요청 정보
- Response 메시지 : 응답 정보 
<p align="center"><img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/HTTP%20%EC%A0%95%EB%B3%B4%EB%8A%94%20HTTP%20%EB%A9%94%EC%84%B8%EC%A7%80%EC%97%90%20%EC%9E%88%EB%8B%A4/part3img/1.PNG">
</p>

## 3.2 Request 메시지와 Response 메시지의 구조

<p align="center"><img  src="https://github.com/mond1219/Zerobase-Study/blob/main/%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C%20%EB%B0%B0%EC%9A%B0%EB%8A%94%20HTTP%20%26%20Network%20Basic/HTTP%20%EC%A0%95%EB%B3%B4%EB%8A%94%20HTTP%20%EB%A9%94%EC%84%B8%EC%A7%80%EC%97%90%20%EC%9E%88%EB%8B%A4/part3img/2.PNG">
</p>  

| Request 메시지 헤더 | 설명 |
|:---:|:-------|
| request 라인 | 메소드, URI, HTTP 버전|
| request 헤더 필드 | request 조건과 속성의 헤더 필드 |
| 일반 헤더 필드 ||
| 엔티티 헤더 필드 ||
| 그 외 | HTTP의 RFC에 없는 헤더 필드(쿠키)가 포함되는 경우가 있다.|

| response 메시지 헤더 | 설명 |
|:---:|:-------|
| 상태 라인 | 결과 상태코드, HTTP버전 |
| response 헤더 필드 | response 조건과 속성의 헤더 필드 |
| 일반 헤더 필드 ||
| 엔티티 헤더 필드 ||
| 그 외 | HTTP의 RFC에 없는 헤더 필드(쿠키)가 포함되는 경우가 있다. |

## 3.3 인코딩으로 전송 효율을 높이다.
- HTTP로 데이터를 인코딩(변환)하면 전송 효율 상승, 다량의 액세스 효율 상승
- 컴퓨터에서 인코딩 처리를 해야해 CPU 등의 리소스는 보다 많이 소비
    
    ### 3.3.1 message Body와 entity Body의 차이

    | message | entity |
    | :---: | :---: |
    |HTTP 통신의 기본 단위로 옥텟 시퀀스(Octet sequence, 8bit)로 구성되고 통신을 통해서 전송|request와 response의 페이로드(payload, 부가물)로 전송되는 정보로 엔티티 헤더 필드와 엔티티 바디로 구성된다.</br> 전송 코딩이 적용된 경우 body의 내용이 변한다.  |
    
    - HTTP message Body는 request와 response에 관한 엔티티 바디를 운반하는 일</br>
    </br>
### 3.3.2 압축해서 보내는 콘텐츠 코딩(Content Codings) 
- 용량을 줄이기 위한 HTTP의 기능 
- entity에 적용하는 인코딩  
- entity정보를 유지한 채로 압축한다. ex) 파일을 zip파일로 압축하듯    
</br>

### 3.3.3 분해해서 보내는 청크 전송 코딩(Chunked transfer Coding)
- 사이즈가 큰 엔티티 바디를 전송할 때 데이터를 분할해서 조금씩 표시
- 엔티티 바디를 청크(덩어리)로 분해
- 청크 사이즈를 16진수로 사용해 단락을 표시
- 엔티티 바디 끝에는 "0(CR+LF)"를 기록
- 수신한 클라이언트 측에서 원래의 엔티티 바디로 디코딩

## 3.4 여러 데이터를 보내는 멀티 파트
| Requeset Line|
| --- |
| HTTP Header |
| Empty Line |
| Message Body | 

- HTTP는 위의 표처럼 4개의 part로 구성
- HTTP Header에 Meesage body의 데이터 타입을  명시해줄 수 있다.
- 명시하는 필드가 Content-type이다. 
- Content-type 필드에 MIME타입을 기술할 수있는데, 여러 타입중 하나가 multipart이다.

- MIME 
    - 텍스트나 영상, 이미지와 같은 여러 다른 데이터를 다루기 위한 기능
    - 이미지 등의 바이너리 데이터를 ASCII 문자열에 인코딩하는 방법과 데이터 종류를 나타내는 방법 등을 규정 
    - Multipart : 다른 종류의 데이터를 수용하는 방법을 사용한다.

// 이부분은 책 보고 안했습니다. 뭐 번역본이라 참,,,험험

### Multipart 란?
- 웹 클라이언트가 request할 때, http 프로토콜의 바디 데이터를 여러 부분으로 나눠서 보낸다. 
- 주로 보통 파일을 전송할 때 사용(ex : 프론트->백엔드 이미지 전송)
- http 프로토콜의 바디 부분에 파일 정보를 담아서 전송하는 데 파일을 한번에 여러개 전송하면 body부분에 파일이 여러개 부분으로 연결되어 전송된다.


## 3.5 일부분만 받는 레인지 리퀘스트
### resume 
- 다운로드 중 커넥션이 끊어지면 다운로드 한 곳에서부터 다운로드를 재개할 수 있는 기능 
- 도입하기 위해 entity의 범위를 지정 

### Range request
- entity의 범위를 지정하여 request한다. 
- 전체 10000byte 정도 크기의 리소스에서 5001~10000byte의 범위(byte range)만을 리퀘스트 할 수 있다.
- range request를 할때 range 헤더 필드를 사용하여 리소스의 byte range를 지정한다. 

- 💚byte range 지정형식
    - 5001~10000 byte
        Range: bytes = 5001-10000
    - 5001 byte 이상
        Range: bytes=5001-
    - 0 ~ 3000byte, 5000~7000byte까지의 복수 범위
        Range: bytes=-3000, 5000-7000
</br></br>
- range request의 response는 상태 코드 206 Partial Content라는 response 메시지가 되돌아온다.
- 복수 범위의 response는 multilpart/byteranges로 response가 돌아온다.
- 서버가 range request를 지원하지 않는 경우 상태 코드 200 OK인 response 메시지로 완전한 엔티티가 되돌아온다.

## 3.6 최적의 콘텐츠를 돌려주는 콘텐츠 네고시에이션
- 같은 content(내용)이지만 여러 개의 페이지를 지닌 웹페이지가 있다.
ex) 내용은 같지만 영어판과 한국어판과 같이 표시되는 언어가 서로 다른 웹페이지

### Content Negotiation
- 클라이언트와 서버가 제공하는 리소스의 내용에 대해서 교섭하는 것   
ex)브라우저가 같은 URI에 엑세스할 때 각각 영어판 웹 페이지와 한국어판 웹 페이지를 표시한다. 

- 제공하는 리소스를 언어와 문자 세트, 인코딩 방식 등 을 기준으로 판단한다
- 판단 기준 : 리퀘스트 메시지에 포함된 다음과 같은 리퀘스트 헤더 필드
    - Accept
    - Accept-Charset
    - Accept-Encoding
    - Accept-Language
    - Content-Language

### Content Negotiation 종류 
</br>

#### 💚Server-driven Negotiation(서버 구동형)   
- 서버 측에서 Negotiation 하는 방식   
- request 헤더 필드의 정보를 참고해서 자동적으로 처리   
- 브라우저가 보내는 정보를 근거로 하기 때문에 **유저에게 정말로 적절한것**이 선택 되었다고 할 수 없다.

#### 💚Agent-driven Negotiation(에이전트 구동형)   
- 클라이언트 측에서 Negotiation하는 방식   
- 선택지 중에서 유저가 수동으로 선택   
- JavaScript 등을 사용해서 웹 페이지에서 자동적으로 정하는 것도 있다.</br>
ex) OS의 종류나 브라우저의 종류 등에 의해서 PC용과 스마트폰용의 웹 페이지를 자동으로 전환하는 것

#### 💚Trnasparent Negotiation
- Server와 agent를 혼합, 서버와 클라이언트가 각각 Negotiation하는 방식 





 


