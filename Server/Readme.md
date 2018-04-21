# Server

## 1. JSP(Java Server Page)

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/7/72/JSP_Model_2.svg/220px-JSP_Model_2.svg.png)

* 웹 환경에서 작동하는 웹 애플리케이션
* Java를 이용한 **Server Side Script** 언어
* HTML내에 Java 코드를 삽입하여 웹 서버에서 동적으로 웹 페이지를 생성하여 웹 브라우저에게 돌려주는 언어이다.
* <% ... %> 스크립트 영역이 있다.
* 실행시 javax.servlet.http.HttpServlet 클래스를 상속받은 자바 소스코드로 변환된 다음 컴파일되어 실행된다.
* Servlet Container : JSP 파일을 Servlet 클래스로 변환하고 실행시켜 준다. (Ex **Tomcat**)
* 하나의 JSP 페이지가 하나의 자바 클래스이기 때문에 모든 자바 라이브러리를 끌어다 쓸 수 있다.
* Servlet Container도 Java 프로그램이며, JVM 위에서 실행된다.

  ### 동작 구조

  1. 클라이언트에서 서비스가 요청되면
  2. JSP의 실행을 요구 하고
  3. JSP는 웹 애플리케이션 서버의 서블릿 컨테이너에서 서블릿 원시코드로 변환 된다.
  4. 서블릿 원시코드는 바로 컴파일된 후 실행되어 결과를 HTML 형태로 클라이언트에 돌려 준다.

## 2. Java Servlet

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/4/40/JSPLife.png/400px-JSPLife.png)

* Java를 사용하여 웹 페이지를 동적으로 생성하는 서버측 프로그램, 혹은 그 사양을 말한다. =  **Servlet(서블릿)**
* 웹 서버의 성능을 향상하기 위해 사용되는 자바 클래스의 일종이다.
* JSP와 비슷한 점이 있지만, JSP가 HTML에 Java 코드를 포함하고 있는 반면, 서블릿은 Java코드를 HTML 코드를 포함하고 있다.
* 웹 시스템이 구현되고 있다.
* 비슷한 서비스 : PHP, ASP
* 외부 요청마다 프로세스보다 가벼운 스레드로써 응답하기때문에 CGI 보다 가볍다.
* Java로 구현되기 때문에 다양한 플랫폼에서 동작한다.

## 3. Web Container(Servlet Container)

* 웹 서버의 컴포넌트 중 하나로 Java Servlet과 상호작용한다.
* 웹 컨테이너는 Servlet의 생명주기를 관리하고, URL과 특정 Servlet을 맵핑하여 URL 요청이 올바른 접근 권한을 갖도록 보장한다.
* 웹 컨테이너는 서블릿, JSP 파일, 서버 사이드 코드가 포함된 다른 타입의 파일들에 대한 요청을 다룬다.
* 웹 컨테이너는 서블릿 객체를 생성하고, 서블릿을 로드와 언로드하며, 요청과 응답 객체를 생성하고 관리하고 다른 서블릿 관리 작업을 수행한다.
* 웹 컨포넌트 자바 EE 아키텍처 제약을 구현하고, 보안, 병행성, 생명주기 관리, 트랜잭션, 배포 등 다른 서비스를 포함하는 웹 컴포넌트의 실행 환경을 명세한다.
* 아파치 톰캣은 아피치 소프트웨어 라이센스 하에 사용할 수 있는 오픈 소스 웹 컨테이너다.

## 4. Web Server

## 5. Web Application Server

## 6. Apach Tomcat

## 7. Nginx