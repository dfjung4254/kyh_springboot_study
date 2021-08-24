### Spring boot 강의

- 스프링 부트 라이브러리
  1. spring-boot-starter-tomcat : 톰캣(웹서버 내장형 - 임베디드)
  2. spring-webmvc : 스프링 웹 MVC
  3. spring-boot-starter-thymeleaf : 타임리프 템플릿 엔진(view)
  4. spring-boot-starter(공통) : 코어 + 로깅
     1. spring-core
     2. logback + slf4j(interface)

- 테스트 라이브러리
  1. spring-boot-starter-test
     1. junit : 테스트 프레임워크
     2. mockito : 목 라이브러리
     3. assertj : 테스트코드 편하게 작성하도록 도와주는 라이브러리
     4. spring-test : 스프링 통합 테스트 지원
     

### 스프링 웹 개발 기초
- 정적 컨텐츠
- MVC와 템플릿 엔진
- API -> MVVM (json) / 서버to서버 간 통신

1. 정적 컨텐츠
   - 스프링부트는 자동지원 : /resources/static
   - 요청들어왔을 때
     1. 내장톰켓에서 스프링 controller 먼저 탐색
     2. 없을 시 resource 하위의 정적 컨텐츠 탐색
     3. 해당 경로에 요청 리소스 존재 시 리턴

2. MVC : Model, View, Controller
   - View 는 화면을 그리는데 집중해야 한다.
   - Model, Controller 는 비즈니스로직에 집중해야 한다.
   - 요청들어왔을 때
     1. 내장톰켓에서 스프링 controller 탐색
     2. controller 에서는 요청 parameter를 받아 비즈니스로직 구현
     3. model 에 필요한 값을 담아 view와 함께 return
     4. viewResolver 를 통해 템플릿엔진은 model의 값을 참조하여 동적으로 html 생성
     5. 변환된 html을 클라이언트에 리턴

3. API
   - @ResponseBody 로 리턴 - json 구조로 응답.
   - 요청들어왔을 때 (@ResponseBody 원리)
     1. 내장톰켓에서 스프링 controller 탐색
     2. controller 에서는 요청 parameter를 받아 비즈니스로직 구현
     3. 이때 controller에 @ResponseBody 어노테이션이 붙어 있으면 return 값이 Html Resposne Body 값이 됨.
     4. constoller에서 리턴된 값이 Object 타입이라면 HttpMessageConverter에 의해 json 등 값으로 변경되어 응답body 값 세팅.
   - viewResolver 대신 HttpMessageConverter 가 동작하는 것.
   - return 값이 String 타입이면 StringHttpMessageConverter
   - return 값이 Object 타입이면 MappingJackson2HttpMessageConverter
     - Jackson library
     - Gson library
   - byte 처리 등 HttpMessageConverter가 기본으로 등록되어 있음.
   
- 참고 : 클라이언트의 Http Accept 헤더와 서버의 컨트롤러 반환 타입정보를 조합해서 HttpMessageConverter가 선택됨.














