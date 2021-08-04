# 12 7계층 HTTP

## HTTP 프로토콜

- HyperText Transfer Protocol 
- www에서 쓰이는 핵심 프로토콜, 문서의 전송을 위해 쓰이며 요즘에는 거의 모든 웹 애플리케이션에서 사용되고 있다.
- Request/Response 동작에 기반하여 서비스를 제공한다.



## HTTP 역사

- HTTP 1.0

  - 연결 수립, 동작, 연결 해제 -> 단순함이 특징이다.

  - 하나의 url은 하나의 TCP 연결 

  - HTML 문서를 전송 받은 뒤 연결을 끊고 다시 연결하여 데이터를 전송한다.

    -> 단순 동작(연결 수립, 동작, 연결 해제) 이 반복되어서 통신 부하 문제가 발생

    ![http 1.0](img/http/http%201.0.png)

- HTTP 1.1

![http 1.0-2](img/http/http%201.0-2.png)





### HTTP  요청 프로토콜

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
  - HTTP 버전:

- Headers

- Body

