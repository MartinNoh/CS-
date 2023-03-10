## RESTful API

> Representational State Transfer API

네트워크 아키텍처에서 사용되는 웹 API 디자인 스타일 중하나입니다.

RESTful API는 클라이언트와 서버 간의 통신을 위한 인터페이스로, HTTP 메서드(GET, POST, PUT, DELETE 등)를 사용하여 데이터를 요청하고 응답합니다. 이 API는 리소스를 표현하고, URI(Uniform Resource Identifier)를 통해 각 리소스에 접근하며, 리소스의 상태(상태 전이)를 변경하는 데 사용됩니다.

RESTful API는 HTTP를 기반으로 하므로, 인터넷에서 가장 보편적으로 사용되는 프로토콜 중 하나입니다. 이 API는 간단하게 확장성이 높으며, 다양한 플랫폼과 언어에서 지원됩니다. 따라서 RESTful API는 다양한 애플리케이션, 서비스, 시스템 간의 상호 운용성을 가능하게 합니다.

### REST 6가지 원칙
- Uniform Interface
- Stateless
- Caching
- Client-Server
- Hierarchical system
- Code on demand

### REST하게 API를 디자인한다는 것은 무엇을 의미하는가?
1. 리소스와 행위를 명시적이고 직관적으로 분리한다.
- 리소스는 URI로 표현되는데 리소스가 가리키는 것은 명사로 표현되어야 한다.
- 행위는 HTTP Method로 표현하고, GET(조회), POST(생성), PUT(기존 entity 전체 수정), PATCH(기존 entity 일부 수정), DELETE(삭제)을 분명한 목적으로 사용한다.

2. Message는 Header와 Body를 명확하게 분리해서 사용한다.
- Entity에 대한 내용은 body에 담는다.
- 애플리케이션 서버가 행동할 판단의 근거가 되는 컨트롤 정보인 API 버전 정보, 응답 받고자 하는 MIME 타입 등은 hedader에 담는다.
- header와 body는 http header와 http body로 나눌 수도 있고, http body에 들어가는 json 구조로 분리할 수도 있다.

3. API 버전을 관리한다.
- 환경은 항상 변하기 때문에 API의 signature가 변경될 수도 있음에 유의하자.
- 특정 API를 변경할 때는 반드시 하위 호환성을 보장해야 한다.

4. 서버와 클라이언트가 같은 방식을 사용해서 요청하도록 한다.
- 브라우저는 form-data 형식의 submit으로 보내고 서버에서는 json 형태로 보내는 식의 분리보다는 json으로 보내든, 둘 다 form-data 형식으로 보내든 하나로 통일한다.
- 다른 말로 표현하자면 URI가 플랫폼 중립적이어야 한다.

### RESTful API의 장점
1. Open API를 제공하기 쉽다.
2. 멀티플랫폼 지원 및 연동이 용이하다.
3. 원하는 타입으로 데이터를 주고 받을 수 있다.
4. 기존 웹 인프라(HTTP)를 그대로 사용할 수 있다.

### RESTful API의 단점
1. 사용할 수 있는 메소드가 한정적이다.
2. 분산 환경에는 부적합하자.
3. HTTP 통신 모델에 대해서만 지원한다.