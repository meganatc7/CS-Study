# 12 7계층 HTTP

## 🤗 HTTP 프로토콜

- HyperText Transfer Protocol 
- www에서 쓰이는 핵심 프로토콜, 문서의 전송을 위해 쓰이며 요즘에는 거의 모든 웹 애플리케이션에서 사용되고 있다.
- Request/Response 동작에 기반하여 서비스를 제공한다.



## 🤗 HTTP 역사

- HTTP 1.0

  - 연결 수립, 동작, 연결 해제 -> 단순함이 특징이다.

  - 하나의 url은 하나의 TCP 연결 

  - HTML 문서를 전송 받은 뒤 연결을 끊고 다시 연결하여 데이터를 전송한다.

    -> 단순 동작(연결 수립, 동작, 연결 해제) 이 반복되어서 통신 부하 문제가 발생

    ![http 1.0](img/http/http%201.0.png)

- HTTP 1.1

![http 1.0-2](img/http/http%201.0-2.png)





### 😏 HTTP  요청 프로토콜

![http구조](img/http/http%EA%B5%AC%EC%A1%B0.PNG)



- Request Line

  ![request line](img/http/request%20line.png)

  - 요청 타입: GET, POST, PUT, DELETE
    - GET: 데이터를 서버로 보낼 때 uri부분에 데이터를 포함 시켜서 보낸다. -> 중요하지 않은 데이터를 보낼 때 사용
    - POST: uri에 따로 보이지 않는다. -> 중요한 데이터를 보낼 때 사용
  - URI: 인터넷 상에서 특정 자원(파일)을 나타내는 유일한 주소
    - `scheme ://host[:port][/path][?query]`
      - scheme: 7계층 프로토콜
      - host: IP주소
  - HTTP 버전

- Headers

- Body





### 😏 HTTP 응답 프로토콜

- 구조

  ![http 응답](img/http/http%20%EC%9D%91%EB%8B%B5.PNG)

  ![http응답 2](img/http/http%EC%9D%91%EB%8B%B5%202.png)

  - Status Line: `HTTP/1.1 200 OK`
    - HTTP 버전 + 공백 + **상태 코드** + 공백 + 상태 문구
    - 상태 코드
      - 100~199: 단순 정보
      - **200~299**: Client 요청 **성공**
      - 300~399: Client 요청이 수행되지 않아 다른 URL로 재지정
      - **400~499**: **Client**의 요청이 불완전하여 다른 정보가 필요
      - **500~599**: **Server**의 오류 or Client 요청 수행 불가
    - 상태코드 set
      - (403,Forbidden): 권한이 없는 페이지 요청
      - (404, Not Found): 서버에 없는 페이지 요청
      - (500, Internal Server Error): 서버의 일부가 멈췄거나 설정 오류 발생
      - (503, Service Unavailable): 최대 Session 수 초과
  - Body: 사용자가 요청한 데이터

  



### 😏 HTTP 헤더

##### 🥕 일반 헤더

- **Content-Length**: 메시지 바디 길이
- **Content-Type**: 메시지 바디에 들어있는 컨텐츠 종류 (HTML: text/html)



##### 🥕 요청 헤더

- **Cookie**: 서버로부터 받은 쿠키를 다시 서버에게 보내주는 역할
- **Host**: 요청된 URL에 나타난 호스트명을 상세하게 표시(HTTP 1.1버전에서는 필수값)
- **User-Agent**: Client Program에 대한 식별 기능 정보 제공(이걸로 핸드폰으로 접속했는지, pc로 접속했는지 알 수 있음)



##### 🥕 응답 헤더

- Server: 사용하고 있는 웹 서버의 소프트웨어에 대한 정보를 포함
- Set-Cookie: 쿠키를 생성하고 브라우저에 보낼 때 사용, 해당 쿠키 값을 브라우저가 서버에게 다시 보낼 때 사용한다.







