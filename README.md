# interview1. 스프링 시큐리티에 대하여 설명하시오.
· 스프링 기반의 어플리케이션의 보안(인증과 권한)을 담당하는 하나의 프레임워크이다.



2. 스트링시큐리티를 적용하기 위한 기본 설정 및 세팅을 설명하시오.



1)pox.xml 4개의 라이브러리 설정 (spring보다 낮은 버전을 사용해야하며, 버전은 메이븐 레포지토리에서 확인 가능)

1
2https://blog.kakaocdn.net/dn/bLZYme/btqXu5q2Fwf/NLeZdjt0dh0zbGTzmUPmW1/img.png
3
4
5
6
7
8
9
10
11


12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
    <properties>
        <java-version>1.8</java-version>
        <org.springframework-version>5.0.7.RELEASE</org.springframework-version>
        <org.aspectj-version>1.6.10</org.aspectj-version>
        <org.slf4j-version>1.6.6</org.slf4j-version>
        <org.security-version>5.0.6.RELEASE</org.security-version>
    </properties>

    <!-- Spring Security -->
    <dependency>
        <groupId>org.springframework.security</groupId>
        <artifactId>spring-security-core</artifactId>
        <version>${org.security-version}</version>
    </dependency>

    <dependency>
        <groupId>org.springframework.security</groupId>
        <artifactId>spring-security-web</artifactId>
        <version>${org.security-version}</version>
    </dependency>

    <dependency>
        <groupId>org.springframework.security</groupId>
        <artifactId>spring-security-config</artifactId>
        <version>${org.security-version}</version>
    </dependency>

    <dependency>
        <groupId>org.springframework.security</groupId>
        <artifactId>spring-security-taglibs</artifactId>
        <version>${org.security-version}</version>
    </dependency>
 </dependencies>
Colored by Color Scripter
cs


2)web.xml 필터 설정(한글 처리 밑에 첨부)

1
2
3
4
5
6
7
8
9
10
   <!-- Spring Security Filter -->
    <filter>
        <filter-name>springSecurityFilterChain</filter-name>
        <filter-class>org.springframework.web.filter.DelegatingFilterProxy</filter-class>
    </filter>

    <filter-mapping>
          <filter-name>springSecurityFilterChain</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
Colored by Color Scripter
cs


3)security-context.xml 설정

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
 <?xml version="1.0" encoding="UTF-8"?>
 <beans:beans xmlns="http://www.springframework.org/schema/security"
    xmlns:beans="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/security http://www.springframework.org/schema/security/spring-security.xsd
      http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    
   <http> 
      <form-login />
   </http> 
   
   <!-- provider --> 
   <authentication-manager>
   </authentication-manager>   
    
 </beans:beans>
Colored by Color Scripter
cs


※/login으로 유입했을 때, 컨트롤러에서 맵핑 처리를 하지 않았지만 아래와 같이 페이지를 출력하는 이유?

   스프링 시큐리티의 url 처리를 통해 페이지를 출력하기 때문!!


3. 인증과 권한에 대하여 설명하시오.
· 인증은 자신을 증명하는 과정으로, 애플리케이션의 작업을 수행할 수 있는 주체임을 증명한다.
  아이디와 비밀번호를 통한 로그인이 인증의 대표적인 예로 볼 수 있다. 
· 권한은 접근 할 수 없도록 제한되어 있는 리소스에 권한에 따라 접근 여부가 달라진다.
· ex) 사원증을 통한 회사 출근을 인증이라 하며, 회사 내의 해당부서에 출입가능한 자격을 권한이라 한다.  



4. XSS와 CSRF에 대하여 설명하시오. 
※XSS란?

· 다른 웹사이트와 정보를 교환하는 식으로 작동하여 사이트 간 스크립팅이라 명칭하며, 웹 상에서 가장 기초적인 취약점 공격

  방법의 일종으로, 악의적인 사용자가 공격하려는 사이트에 스크립트를 넣는 기법을 일컫는다.
· 이 취약점은 웹 애플리케이션이 사용자로부터 입력 받은 값을 제대로 검사하지 않고 사용할 경우에 나타나며,
  해커가 사용자의 정보(쿠키, 세션)을 탈취하거나, 자동으로 비정상적인 기능을 수행하게 할 수 있다.  
※CSRF란?

· 웹 사이트 취약점 공격의 하나로 사이트 간 요청 위조라 명칭하며, 사용자가 자신의 의지와는 무관하게 공격자가 의도한

  행위(수정, 삭제, 등록 등)를 특정 웹사이트에 요청하게 하는 공격을 말한다.
※XSS와 CSRF의 차이는? 

· XSS는 사용자가 특정 웹사이트를 신용하는 점을 노린 것이고, CSRF는 특정 웹사이트가 사용자의 엡 브라우저를 신용하는

 상태를 노린 것이다.



