## ✅ 백엔드 포트폴리오 단위 평가

### �� 주제: **사용자 인증 및 게시글 API 구현**

### �� 개요

간단한 커뮤니티 시스템을 개발합니다. 사용자 회원가입 및 로그인, 인증 기반의 게시글 CRUD API를 구현하세요.

---

## �� 요구 기능

### 1. **회원(User) 기능**

* 사용자 회원가입
* 로그인 (JWT 발급)
* 사용자 정보 조회 (인증 필요)

### 2. **게시글(Post) 기능**

* 게시글 목록 조회 (페이징)
* 게시글 단건 조회
* 게시글 작성 (로그인 필요)
* 게시글 수정/삭제 (작성자 본인만 가능)

---

## �� 기술 요구사항

| 영역          | 내용                                                 |
| ----------- | -------------------------------------------------- |
| Spring Boot | 3.x 이상 권장                                          |
| ORM         | Spring Data JPA + H2 또는 MySQL 사용                   |
| 인증/보안       | Spring Security + JWT 기반 인증                        |
| REST API    | RESTful 원칙에 따라 URL/Method 설계                       |
| 예외 처리       | GlobalExceptionHandler 사용하여 응답 통일화                 |
| 유효성 검사      | `@Valid`와 `@Validated` 사용                          |
| 테스트 (선택)    | Postman collection 또는 간단한 Controller Test 포함 시 가산점 |

---

## �� 상세 테이블 설계

### �� User

| 필드명      | 타입          | 설명             |
| -------- | ----------- | -------------- |
| id       | Long (PK)   | 사용자 고유 ID      |
| username | String      | 로그인 ID (중복X)   |
| password | String      | 비밀번호 (암호화)     |
| nickname | String      | 사용자 닉네임        |
| role     | Enum/String | 권한 (e.g. USER) |

---

### �� Post

| 필드명       | 타입            | 설명        |
| --------- | ------------- | --------- |
| id        | Long (PK)     | 게시글 고유 ID |
| title     | String        | 게시글 제목    |
| content   | String        | 게시글 내용    |
| author    | User (FK)     | 작성자 참조    |
| createdAt | LocalDateTime | 작성일시      |

---

## �� 구현 예시

### �� 인증 API

```
POST /api/auth/signup      → 회원가입
POST /api/auth/login       → 로그인 후 JWT 반환
GET  /api/users/me         → 현재 로그인한 사용자 정보
```

### �� 게시글 API

```
GET    /api/posts               → 게시글 목록 (페이징)
GET    /api/posts/{id}          → 게시글 상세 조회
POST   /api/posts               → 게시글 작성 (인증 필요)
PUT    /api/posts/{id}          → 게시글 수정 (본인만)
DELETE /api/posts/{id}          → 게시글 삭제 (본인만)
```

---

## ✅ JWT 요구 조건

* 로그인 성공 시 JWT 발급 (AccessToken)
* Authorization 헤더: `Bearer <token>` 방식 사용
* JWT를 통해 사용자 인증 및 권한 검사

---

## ⚠️ 주의 사항

* 비밀번호는 **암호화(BCrypt)** 해서 저장해야 합니다.
* 게시글 수정/삭제는 **작성자만 가능**해야 합니다.
* JPA Lazy 로딩 시 예외 방지를 위한 DTO 사용 권장
* API 응답은 통일된 JSON 형식으로 작성

```json
{
  "status": "OK",
  "message": "성공적으로 처리되었습니다.",
  "data": { ... }
}
```

---

## �� 제출 방식

* 압축 파일 제출
* 디렉토리 구조는 다음과 같이 구성해주세요:

```
src/
 └─ main/
     ├─ java/com/example/demo/
     │    ├─ controller
     │    ├─ domain
     │    ├─ dto
     │    ├─ repository
     │    ├─ security
     │    ├─ service
     │    └─ config
     └─ resources/
         └─ application.yml
