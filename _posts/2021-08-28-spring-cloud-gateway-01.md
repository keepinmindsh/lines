---
title: "Spring Cloud Gateway"
excerpt: ""

categories:
  - Spring
tags:
  - Spring 
classes: wide
---

> 남이 나를 알아주지 않음을 걱정하지말고, 자신의 능하지 못함을 걱정해야 한다. 

### Get Started With Cloud Gateway 

- 기본 pom.xml 설정 

```xml 

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.5.4</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.example</groupId>
    <artifactId>spring-cloud-gateway</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>spring-cloud-gateway</name>
    <description>spring-cloud-gateway</description>
    <properties>
        <java.version>11</java.version>
        <spring-cloud.version>2020.0.3</spring-cloud.version>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-webflux</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-gateway</artifactId>
        </dependency>

        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>io.projectreactor</groupId>
            <artifactId>reactor-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${spring-cloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <excludes>
                        <exclude>
                            <groupId>org.projectlombok</groupId>
                            <artifactId>lombok</artifactId>
                        </exclude>
                    </excludes>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>

```

- 기본 routes 예제 

```java

public static void main(String[] args) {
    SpringApplication.run(SpringCloudGatewayApplication.class, args);
}

@Bean
RouteLocator gateway ( RouteLocatorBuilder rlb ) {
    return rlb
            .routes()
            .route( routeSpec ->
                    routeSpec.path("/hello").and().host("*.spring.io")
                            .filters(gatewayFilterSpec ->
                                    gatewayFilterSpec.setPath("/guides"))
                            .uri("https://spring.io/")
                    )
            .route("twitter", routeSpec ->
                routeSpec.path("/twitter/**")
                        .filters( fs -> fs.rewritePath("/twitter/(?<handle>.*)",
                                "/${handle}"
                                )
                        ).uri("http://twitter.com/@"))

            .build();
}

```

### Spring Cloud Gateway 시작하기 

Spring Cloud Gateway는 Spring Boot 2.X, Spring WebFlux, 그리고 Project Reactor를 기반으로 구성되어 있다. 

- 기본 용어 
  - Route
  - Predicate
  - Filter 

###### Spring Cloud Gateway 설정시 참고 사항 

Spring Cloud Gateway는 Netty Runtime, Spring WebFlux 기반한에 동작한다. 기존의 전통적인 서블릿 컨테이너나 WAR로 빌드 되는 방식에서는 동작하지 않는다. 왜냐하면 Spring Cloud Gateway의 경우 Spring Boot 2.X, Spring WebFlux, 그리고 Project Reactor를 바탕으로 개발되었기 때문이다. 


### 어떻게 동작하는가?

![](https://keepinmindsh.github.io/lines/assets/img/spring_cloud_gateway_diagram.png){: .align-center} 

Client는 Spring Cloud Gateway로 요청을 전달하면, Gateway Handler가 만약 설정된 route 정보에 해당 하는 요청일 경우, Gateway Web Handler로 요청을 전달한다. 그리고 이 핸들러는 요청에 특화된 Filter Chain을 통해서 요청을 동작시킨다. 
필터가 점선에 의해서 구분되는 것은 전/후의 로직에 대해서 Filter를 통해서 처리할 수 있다. 모든 "pre" 필터 로직은 실행될 것이다. 
그리고 해당 우회 요청이 생기고, 그 우회 요청이 생깅 후에 "post" 필터의 로직이 동작할 것이다. 

### 간단 예제

- yaml 

```

spring:
  cloud:
    gateway:
      routes:
      - id: after_route
        uri: https://example.org
        predicates:
        - Cookie=mycookie,mycookievalue

```

> https://docs.spring.io/spring-cloud-gateway/docs/current/reference/html/#gateway-starter [2021-08-29]

### Predicates 

Predicates의 경우, 다양한 옵션에 의해서 URL로의 접근을 제어할 수 있다. Predicates로 설정된 조건이 맞을 경우, uri에 설정된 값을 가져올 수 있다.  
Predicates에 설정된 조건에 부합할 경우 설정된 URL로 Match되며 값이 전달 된다. 

 - Cookies를 활용한 경우 

```

spring:
  cloud:
    gateway:
      routes:
      - id: after_route
        uri: https://example.org
        predicates:
        - name: Cookie
          args:
            name: mycookie
            regexp: mycookievalue

```

 - After, Before, Between 에 의한 URL 허용 제한 

```

spring:
  cloud:
    gateway:
      routes:
      - id: after_route
        uri: https://example.org
        predicates:
        - After=2017-01-20T17:42:47.789-07:00[America/Denver]

```

```

spring:
  cloud:
    gateway:
      routes:
      - id: before_route
        uri: https://example.org
        predicates:
        - Before=2017-01-20T17:42:47.789-07:00[America/Denver]

```

```

spring:
  cloud:
    gateway:
      routes:
      - id: between_route
        uri: https://example.org
        predicates:
        - Between=2017-01-20T17:42:47.789-07:00[America/Denver], 2017-01-21T17:42:47.789-07:00[America/Denver]

```

 - Header, Host, Method, etc 에 의한 허용 방식 

```

spring:
  cloud:
    gateway:
      routes:
      - id: header_route
        uri: https://example.org
        predicates:
        - Header=X-Request-Id, \d+

```

```

spring:
  cloud:
    gateway:
      routes:
      - id: host_route
        uri: https://example.org
        predicates:
        - Host=**.somehost.org,**.anotherhost.org

```

```

spring:
  cloud:
    gateway:
      routes:
      - id: method_route
        uri: https://example.org
        predicates:
        - Method=GET,POST

```

 - Path 에 의한 허용 방식 

```

spring:
  cloud:
    gateway:
      routes:
      - id: path_route
        uri: https://example.org
        predicates:
        - Path=/red/{segment},/blue/{segment}

```

 - Query 에 의한 허용 방식 

```

spring:
  cloud:
    gateway:
      routes:
      - id: query_route
        uri: https://example.org
        predicates:
        - Query=green

```

- Weight에 의한 분배 방식 

설정한 그룹에 요청이 들어올 때 호출되는 비율을 지정한다. 아래는 8:2의 비율로 URL이 호출된다. 

```

spring:
  cloud:
    gateway:
      routes:
      - id: weight_high
        uri: https://weighthigh.org
        predicates:
        - Weight=group1, 8
      - id: weight_low
        uri: https://weightlow.org
        predicates:
        - Weight=group1, 2

```