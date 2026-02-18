# Habit Tracker Web Service

## 1. Project Overview

본 프로젝트는 사용자의 일상 습관을 기록하고 관리할 수 있는 웹 기반 서비스로, Spring Boot 기반 MVC 구조를 활용하여 구현되었습니다.
회원 인증 기능을 기반으로 사용자별 습관을 생성·관리하고 날짜별 수행 여부를 기록할 수 있도록 설계된 백엔드 중심 웹 서비스입니다.

단순 CRUD 구현을 넘어 실제 서비스 흐름을 고려하여 계층 구조 분리, 인증 처리, 데이터베이스 연동을 포함한 전체 웹 애플리케이션 형태로 구성했습니다.

---

## 2. Tech Stack

### Backend

* Java 17
* Spring Boot
* Spring MVC
* Spring Security
* Spring Data JPA
* Hibernate

### Frontend

* Thymeleaf
* HTML/CSS
* Bootstrap
* JavaScript

### Database

* MySQL

### Tools

* IntelliJ IDEA
* Gradle
* Git / GitHub

---

## 3. Project Structure

```
src
 ├ main
 │   ├ java
 │   │   ├ config
 │   │   ├ member
 │   │   ├ habit
 │   │   ├ habitcheck
 │   │   └ HabitApplication
 │   └ resources
 │       ├ templates
 │       ├ static
 │       └ application.yml
```

Spring Boot MVC 구조를 기반으로 Controller, Service, Repository 계층을 분리하여 유지보수성과 확장성을 고려했습니다.

---

## 4. Core Package Analysis

### 4.1 config

보안 및 애플리케이션 설정을 담당하는 패키지입니다.

#### SecurityConfig

* Spring Security 전반 설정
* 로그인 인증 처리
* URL 접근 권한 설정
* 사용자 인증 흐름 구성

애플리케이션 전반의 인증 및 보안 흐름을 담당하며, 인증된 사용자만 특정 기능에 접근하도록 설정했습니다.

---

### 4.2 member

회원 도메인 관련 기능을 담당합니다.

#### Member Entity

* 사용자 테이블 매핑
* 이메일, 비밀번호, 닉네임 등 사용자 정보 관리
* JPA 기반 엔티티 설계

#### MemberRepository

* Spring Data JPA 기반 데이터 접근
* 사용자 조회 및 저장
* 로그인 인증용 사용자 조회 기능 포함

#### MemberService

* 회원가입 로직 처리
* 사용자 정보 검증
* 서비스 계층 비즈니스 로직 담당

#### MemberController

* 회원가입 요청 처리
* 로그인 페이지 이동
* 사용자 관련 요청 처리

#### MemberSecurityService

* UserDetailsService 구현
* Spring Security 인증 시 사용자 정보 로드
* 로그인 인증 흐름과 DB 사용자 정보 연결

회원 도메인은 인증과 직접 연결되는 핵심 영역으로, Spring Security와 연동되는 구조로 구현했습니다.

---

### 4.3 habit

사용자의 습관 등록 및 관리 기능을 담당합니다.

#### Habit Entity

* 사용자별 습관 데이터 저장
* 습관 이름, 생성일 등 정보 관리
* Member 엔티티와 연관 관계 구성

#### HabitRepository

* 습관 CRUD 처리
* 사용자 기준 습관 조회 기능

#### HabitService

* 습관 생성, 수정, 삭제 로직
* 사용자별 습관 목록 처리
* 비즈니스 로직 담당

#### HabitController

* 습관 등록 요청 처리
* 습관 목록 조회
* 수정 및 삭제 요청 처리
* View 연결

#### HabitDTO

* View와 Entity 간 데이터 전달 객체
* 엔티티 직접 노출 방지
* 데이터 가공 및 전달

습관 도메인은 사용자 중심 서비스의 핵심 기능으로 CRUD 전반을 서비스 계층 중심으로 구현했습니다.

---

### 4.4 habitcheck

사용자의 날짜별 습관 수행 기록 기능을 담당합니다.

#### HabitCheck Entity

* 특정 날짜 습관 수행 여부 저장
* 습관과 사용자 관계 매핑

#### HabitCheckRepository

* 날짜별 수행 기록 조회
* 사용자 및 습관 기준 데이터 조회

#### HabitCheckService

* 습관 수행 체크 로직
* 날짜별 기록 저장
* 사용자 습관 기록 관리

#### HabitCheckController

* 습관 수행 체크 요청 처리
* 수행 기록 화면 출력
* 사용자 요청 처리

습관 기록 기능은 단순 CRUD를 넘어 날짜 기반 서비스 로직을 포함한 기능으로 구성했습니다.

---

## 5. Template Structure

```
templates
 ├ index
 ├ habit
 ├ member
 └ fragments
```

Thymeleaf 기반 서버 사이드 렌더링 구조를 사용했습니다.

* index : 메인 화면
* habit : 습관 등록 및 목록 화면
* member : 회원가입 및 로그인 화면
* fragments : 공통 header 및 layout 구성

Bootstrap을 활용하여 기본 UI를 구성했습니다.

---

## 6. Key Features

### Member

* 회원가입
* 로그인/로그아웃
* Spring Security 기반 인증
* 사용자 세션 관리

### Habit

* 습관 등록
* 습관 수정 및 삭제
* 사용자별 습관 목록 조회
* 습관 상세 조회

### Habit Check

* 날짜별 습관 수행 체크
* 습관 수행 기록 저장
* 사용자 기준 수행 기록 관리

---

## 7. Application Architecture

본 프로젝트는 다음 구조를 기반으로 설계했습니다.

* Controller : 사용자 요청 처리 및 View 연결
* Service : 비즈니스 로직 처리
* Repository : 데이터 접근 계층
* Entity : 데이터베이스 테이블 매핑
* DTO : 데이터 전달 객체 분리
* Security : 인증 및 권한 처리

계층 분리를 통해 유지보수성과 확장성을 고려한 구조로 구현했습니다.

---

## 8. What I Learned

* Spring Boot MVC 구조 설계
* Controller-Service-Repository 계층 분리
* Spring Security 인증 흐름 이해
* JPA 기반 데이터베이스 연동
* 사용자 중심 서비스 로직 설계
* 실제 서비스 구조 기반 백엔드 구현 경험

---

## 9. Future Improvements

* REST API 구조 리팩토링
* Swagger API 문서화
* Global Exception Handler 적용
* 테스트 코드 작성
* AWS 배포
* 통계 기능 및 그래프 추가

---

## 10. Author

백엔드 개발자를 목표로 Spring Boot 기반 웹 서비스 개발과 데이터 처리 역량을 학습하고 있습니다.
실제 서비스 흐름을 이해하고 안정적인 서버를 구현하는 개발자로 성장하는 것을 목표로 합니다.
