> [스프링 부트 - 핵심 원리와 활용](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-%ED%95%B5%EC%8B%AC%EC%9B%90%EB%A6%AC-%ED%99%9C%EC%9A%A9/dashboard)을 정리한 내용입니다.

스프링 부트 - 핵심 원리와 활용
==============================
## 스프링 부트 소개

* Boot, 부팅
  - 최소한의 인간 개입으로 시작학소 완전히 작동하는 것을 의미
  - 어떤 일을 시작하기 위해 필요한 모든 준비를 마친다는 의미
* 시작을 위한 복잡한 설정 과정은 스프링 부트가 해결
  - 개발자는 새로운 스프링 애플리케이션을 쉽고 빠르게 시작할 수 있음
* 스프링을 편리하게 사용할 수 있도록 지원, 최근에는 스프링 부트를 시본으로 사용
* 단독으로 실행할 수 있는 스프링 애플리케이션을 쉽게 생성
* 관례에 의한 간결한 설정(복잡한 설정을 간결하게 줄일 수 있음)
  - 최근에는 스프링 프레임워크 단독으로만 사용하지 않음

### 스프링 부트 - 핵심 기능 5가지
* WAS : Tomcat같은 웹 서버를 내장해서 별도의 웹 서버를 설치하지 않아도 됨
* 라이브러리 관리 
  - 손쉬운 빌드 구성을 위한 스타터 종속성 제공(ex. JPA 스타터)
  - 스프링과 외부 라이브러리의 버전을 자동으로 관리
    + 스프링 부트에 맞는 스프링 버전과 그에 맞는 기타(제이슨 라이브러리 등)의 호환 가능한 버전을 자동으로 맞춰줌
  - 자동 구성 : 프로젝트 시작에 필요한 스프링과 외부 라이브러리의 빈을 자동 등록
    + 자동 구성(auto configuration)
  - 외부 설정 : 환경에 따라 달라져야하는 외부 설정 공통화
  - 프로덕션 준비 : 모니터링을 위한 메트릭, 상태 확인 기능 제공
 
### 스프링 프레임워크와 스프링 부트
* 스프링 부트는 스프링 프레임 워크를 쉽게 사용할 수 있게 도와주는 도구일 뿐
* 본질은 스프링 프레임워크
* 하지만 스프링 부트가 제공하는 편의 기능이 너무 막강해서 스프링 부트 사용 필수

### 스프링?
스프링이라는 단어는 문맥에 따라 다르게 사용됨
* 스프링 DI 컨테이너 기술
* 스프링 프레임워크
* 스프링 부트, 스프링 프레임워크 등을 모두 포함한 스프링 생태계

## 웹 서버와 서블릿 컨테이너
### 외장 서버 vs 내장서버
* 전통적인 방식
  - 과거에 자바로 웹 어플리케이션을 개발할 때, 먼저 서버에 톰캣같은 WAS(웹 애플리케이션 서버)를 설치했음
  - WAS에서 동작하도록 서블릿 스펙에 맞춰 코드를 작성하고 WAR형식으로 빌드해서 war파일을 만들었음
  - 이렇게 만들어진 war파일을 WAS에 전달해서 배포하는 방식으로 전체 개발 주기가 동작함
  - 이런 방식은 WAS 기반위에서 개발하고 실행해야 함. IDE같은 개발 환경에서도 WAS와 연동해서 실행되도록 복잡한 추가 설정이 필요했음

* 최근 방식
  - 스프링 부트가 내장 톰캣을 포함하고 있음(애플리케이션 코드 안에 톰캣같은 WAS가 라이브러리로 내장되어있음)
  - 개발자는 코드를 작성하고 JAR로 빌드(자바 기본 빌드)한 다음에 해당 JAR를 원하는 위치에서 실행하기만 하면 WAS도 함께 실행됨
  - 즉, main 메소드만 실행하면 되고, WAS설치나 IDE같은 개발 환ㄱ령에서 WAS와 연동하는 복잡한 일은 수행하지 않아도 됨
 
* 톰캣 설치
  - https://tomcat.apache.org/download-10.cgi
  - ref) https://www.snugarchive.com/blog/apache-tomcat-setup/
  - window cmd(/bin) 에서
    + 실행 : startup.bat
    + 종료 : shutdown.bat
    + 연결되면 주소 : http://localhost:8080
      + 이미 포트에 연결되어있는 경우 : cmd에 netstat -ano | findstr :8080
      + taskkill /f /pid 254188(프로세스 번호)
      + ![image](https://github.com/yongbyn/TIL/assets/44955172/ba186bae-34a8-44be-b21f-be2427126213)

* build.gradle 설정
```
plugins {
    id 'java'
    id 'war'
}

group = 'hello'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = '17'

repositories {
    mavenCentral()
}

dependencies {
    //서블릿
    implementation 'jakarta.servlet:jakarta.servlet-api:6.0.0'
}

tasks.named('test') {
    useJUnitPlatform()
}
```
※ 여기서 useJUnitPlatform가 에러날 경우 task.name('test')를 test로 바꿔주면 됨
  - ref) https://www.inflearn.com/questions/1071921/tasks-named-x27-test-x27-%EC%99%80-%EA%B7%B8%EB%83%A5-test
  - ref) https://velog.io/@hye9807/%EC%98%88%EC%A0%9C1-%EB%B9%84%EC%A6%88%EB%8B%88%EC%8A%A4-%EC%9A%94%EA%B5%AC%EC%82%AC%ED%95%AD%EA%B3%BC-%EC%84%A4%EA%B3%84
* gradlew build
  - terminal에서 ./gradlew build 안되면 gradlew build
