# Todo In-Memory API

Spring Boot를 활용하여 구현한 인메모리 기반 Todo REST API 프로젝트입니다.

데이터베이스를 사용하지 않고 Java의 `Map` 자료구조에 Todo 데이터를 저장하며,
Controller → Service → Repository 계층 구조와 REST API의 기본적인 CRUD 동작을 학습하기 위해 구현했습니다.

## 개발 환경

- Java 21
- Spring Boot 4.1.0
- Gradle
- Spring MVC
- Lombok
- Springdoc OpenAPI (Swagger)
- JUnit 5
- AssertJ
- Mockito

## 프로젝트 구조

```text
com.asdf.todo
├── config
│   └── ApiDocumentationConfig
├── controller
│   └── TodoController
├── model
│   └── Todo
├── repository
│   └── TodoInMemoryRepository
├── service
│   └── TodoService
└── TodoInMemoryApplication
```

### 계층 구조

```text
REST Client
     ↓
Controller
     ↓
Service
     ↓
Repository
     ↓
In-Memory Map
```

- **Controller**: HTTP 요청 및 응답 처리
- **Service**: Todo 관련 비즈니스 로직 처리
- **Repository**: Todo 데이터 저장 및 조회
- **Model**: Todo 데이터 구조 정의

## 주요 기능

| HTTP Method | Endpoint | 기능 |
|---|---|---|
| GET | `/api/todos/v1` | 전체 Todo 조회 |
| GET | `/api/todos/v1/{id}` | 특정 Todo 조회 |
| POST | `/api/todos/v1` | Todo 생성 |
| PUT | `/api/todos/v1/{id}` | Todo 수정 |
| DELETE | `/api/todos/v1/{id}` | Todo 삭제 |

## 데이터 저장 방식

데이터베이스 대신 `Map<Long, Todo>`를 사용하여 Todo 데이터를 메모리에 저장합니다.

Todo의 ID는 `AtomicLong`을 이용하여 자동으로 생성합니다.

인메모리 방식이므로 **애플리케이션을 종료하면 저장된 데이터는 모두 사라집니다.**

## 실행 방법

### 1. 프로젝트 빌드

프로젝트 루트 디렉토리에서 다음 명령어를 실행합니다.

```bash
./gradlew clean build
```

### 2. 애플리케이션 실행

```bash
./gradlew bootRun
```

애플리케이션이 정상적으로 실행되면 기본적으로 다음 주소에서 서버가 실행됩니다.

```text
http://localhost:8080
```

## Swagger UI

애플리케이션 실행 후 다음 주소에서 API 문서를 확인하고 직접 API를 테스트할 수 있습니다.

```text
http://localhost:8080/swagger-ui/index.html
```

OpenAPI 문서는 다음 엔드포인트에서 확인할 수 있습니다.

```text
http://localhost:8080/v3/api-docs
```

## 테스트

전체 테스트를 실행합니다.

```bash
./gradlew test
```

### Controller 테스트

`TodoControllerTests`

- `@WebMvcTest`를 이용하여 Controller 관련 빈만 로드
- `MockMvc`를 이용하여 HTTP 요청과 응답을 테스트
- Mockito를 이용하여 Service 계층을 Mock 객체로 대체
- HTTP 상태 코드 및 JSON 응답 검증

### Service 테스트

`TodoServiceTests`

- Todo 저장
- 전체 Todo 조회
- ID를 이용한 Todo 조회
- Todo 수정
- Todo 삭제

## 학습 내용

이 프로젝트를 통해 다음 내용을 학습했습니다.

- Spring Boot 프로젝트 구성
- Controller → Service → Repository 계층 구조
- Spring Bean과 의존성 주입
- REST API CRUD 구현
- `Map`을 이용한 인메모리 Repository 구현
- HTTP Method와 HTTP 상태 코드
- Swagger/OpenAPI를 이용한 API 문서화
- JUnit 5를 이용한 테스트
- MockMvc와 Mockito를 이용한 Controller 테스트

## 참고

이 프로젝트는 『스프링 부트 개발자 온보딩 가이드』의 예제를 참고하여 학습 목적으로 구현했습니다.

교재의 예제를 기반으로 하되, 현재 학습 환경에 맞게 다음 사항을 변경하여 진행했습니다.

- Spring Boot 3 → Spring Boot 4.1.0
- Spring Boot 버전 변경에 따른 일부 의존성 및 코드 수정