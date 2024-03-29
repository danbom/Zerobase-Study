# 제 4장. 결과를 전달하는 HTTP 상태 코드

> 📑 HTTP 상태 코드 </br>
📌 2XX 성공 (Success) </br>
📌 3XX 리다이렉트 (Redirection) </br>
📌 4XX 클라이언트 에러 (Client Error) </br>
📌 5XX 서버 에러 (Server Error)

</br>

# 4.1 상태 코드는 서버로부터 리퀘스트 결과를 전달한다

상태 코드의 역할: 클라이언트가 서버를 향해 리퀘스트를 보낼 때 서버에서 그 결과가 어떻게 되었는지 알려주는 것. (서버가 리퀘스트를 정상적으로 처리했는지, 에러였는지의 여부를 알 수 있다)

상태코드는 200 OK와 같이 3자리 숫자와 설명으로 나타낸다. 첫 번쨰 숫자는 response 클래스를 나타내고, 나머지 두 자리는 분류가 없다.

✨ 상태 코드 클래스

|     | 클래스        | 설명                                     |
| --- | ------------- | ---------------------------------------- |
| 1XX | Informational | Request를 받아서 처리중                  |
| 2XX | Success       | Request를 정상적으로 처리했음            |
| 3XX | Redirection   | Request를 완료하기 위해 추가 동작이 필요 |
| 4XX | Client Error  | 서버가 Request 이해 불가능               |
| 5XX | Server Error  | 서버가 Request 처리 실패                 |

대표적인 14개의 상태 코드

</br>

# 4.2 2XX 성공 (Success)

## 1) 200 OK

- Request 가 정상 처리되었을 때 서버가 200OK를 보낸다.
- Response 에서 상태 코드와 함께 오는 정보는 메소드에 따라 다르다.

## 2) 204 No Content

- 서버가 Request를 처리하는 건 성공했지만, 리스폰스에 엔티티 바디를 포함하지 않는다.
- 어떠한 엔티티 바디를 되돌려 보내도 안된다.
- ex) 브라우저에서 Request를 보낸 후 204 Reponse를 수신해도 표시된 화면이 변하지 않는다.
- 클라이언트 → 서버로 정보 보내는 것으로 족하고, 클라에 대해 새로운 정보를 보낼 필요가 없는 경우에 사용된다.

## 3) 206 Partial Content

- Range로 범위가 지정된 Request에 의해 서버가 부분적인 GET Request를 받을 때 나타난다.
- Response에는 Content-Range로 지정된 범위의 엔티티가 포함된다.

</br>

# 4.3 3XX 리다이렉트 (Redirection)

3XX response는 Request가 정상적으로 처리를 종료하기 위해 브라우저 측에서 특별한 처리를 수행해야 할 때 나타난다.

## 1) 301 Moved Permanently

- Request된 리소스에 새로운 URI가 부여되어 있어, 이후로는 그 리소스를 참조하는 URI를 사용해야 할 때 나타난다.
- 북마크하고 있는 경우, Location 헤더 필드에서 가리키고 있는 URI에 북마크를 다시 하는 게 좋다는 것을 나타낸다.
- ex) 디렉토리를 지정했을 때 마지막 부분에 슬래시(/) 붙이는 것을 잊은 경우 등

## 2) 302 Found

- Request된 리소스에는 새로운 URI가 할당되어 있기 때문에, 그 URI를 참조해 달라는 의미를 나타낸다.
- 301과 비슷하지만, 302는 영구적인 이동이 아닌, 일시적인 것이다. → 이동하는 곳의 URI는 앞으로 이동될 가능성이 있다.

## 3) 303 See Other

- Request 에 대한 리소스는 다른 URI에 있기 때문에 GET 메소드를 사용해서 얻어야 할 때 나타난다.
- 302 와 같은 기능이지만, 차이점은 303은 리다이렉트 장소를 GET 메소드로 얻어야 한다고 명확하게 제시한다는 점이다.

## 4) 304 Not Modified

- 클라이언트가 조건부 Request를 했을 때 리소스에 대한 액세스는 허락하지만, 조건이 충족되지 않음을 나타낸다.
- Response 바디에 어떤 것도 포함되지 않는다.
- 3XX에 분류돼 있지만, 리다이렉트와는 관계가 없다.

## 5) 307 Temporary Redirect

- 302와 같은 의미를 지니지만, 302는 POST로부터 GET치환이 금지되어 있는데도 불구하고 구현상 그와 같이 되어 있지 않는다. 뭔소리?
- 307은 브라우저 사양에 따라 POST에서 GET으로 치환을 하지 않는다.

</br>

# 4.4 4XX 클라이언트 에러 (Client Error)

클라이언트의 원인으로 에러 발생 시 나타난다.

## 1) 400 Bad Request

- Request구문이 잘못되었음을 나타낸다.
- Request 내용을 검토하고 재송신해야 한다.

## 2) 401 Unauthorized

- 송신한 Request에 HTTP인증 (BASIC인증, DIGEST 인증)정보가 필요하다는 것을 나타낸다.
- 한 번 Request가 이뤄진 경우에는 유저 인증 실패했음을 나타낸다.

## 3) 403 Forbidden

- Request된 리소스의 액세스가 거부되었음을 나타낸다.
- 서버 측은 거부의 이유를 명확하게 하는 경우에 엔티티 바디에 기재하여 유저 측에 표시한다.
- ex) 파일 시스템의 허가가 부여되지 않은 경우와, 액세스 권한 문제가 있을 때 발생한다.

## 4) 404 Not Found

- Request한 리소스가 서버상에 없을 때 나타난다.
- 혹은 서버 측에 해당 Request를 거부하고 싶은 이유를 분명히 하고 싶지 않은 경우 이용할 수 있다.

</br>

# 4.5 5XX 서버 에러 (Server Error)

서버 원인으로 에러 발생할 때 나타난다.

## 1) 500 Internal Server Error

- 서버에서 Request를 처리하는 도중에 에러가 발생함을 나타낸다.

## 2) 503 Service Unavaliable

- 일시적으로 서버가 과부하 상태이거나 점검중이기 때문에 현재 Request를 처리할 수 없음을 나타낸다.
- 이 상태가 해결되기까지 시간이 걸리는 경우에는 Retry-After 헤더 필드에 따라 클라이언트에 전달하는 것이 바람직하다.
