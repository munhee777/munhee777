# 조문희 | 신입 백엔드 개발자

Java와 Spring Boot로 서비스를 구현하고, 데이터베이스와 트랜잭션까지 살펴 안정적인 백엔드를 만드는 개발자입니다. 기능을 나열하기보다 문제를 어떻게 재현하고 해결했는지, 제가 맡은 부분과 팀 결과를 구분해 기록합니다.

[🌐 포트폴리오](https://munhee777.github.io) · [GitHub 저장소](https://github.com/munhee777?tab=repositories) · [Velog](https://velog.io/@velog_mh)

## 기술 스택

**Backend**
<br><img src="https://img.shields.io/badge/Java-007396?style=flat-square&logo=OpenJDK&logoColor=white"/> <img src="https://img.shields.io/badge/Spring%20Boot-6DB33F?style=flat-square&logo=Spring%20Boot&logoColor=white"/> <img src="https://img.shields.io/badge/Spring%20Security-6DB33F?style=flat-square&logo=Spring%20Security&logoColor=white"/> <img src="https://img.shields.io/badge/Spring%20Data%20JPA-59666C?style=flat-square&logo=Hibernate&logoColor=white"/>

**Data**
<br><img src="https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=databricks&logoColor=white"/> <img src="https://img.shields.io/badge/Oracle-F80000?style=flat-square&logo=Oracle&logoColor=white"/> <img src="https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=MySQL&logoColor=white"/> <img src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=Redis&logoColor=white"/>

**Supporting**
<br><img src="https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=React&logoColor=black"/> <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=Python&logoColor=white"/> <img src="https://img.shields.io/badge/Spring%20AI-6DB33F?style=flat-square&logo=Spring&logoColor=white"/> <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=Docker&logoColor=white"/> <img src="https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=GitHub%20Actions&logoColor=white"/>

## 프로젝트

### [제주 야호 | 숙소 예약 및 관광 큐레이션](https://github.com/munhee777/hotel-booking)

제주 숙소 예약과 주변 관광 정보를 제공하는 팀 프로젝트입니다. Java 21, Spring Boot, Oracle 19c, JPA, QueryDSL, Redis/Redisson을 사용했습니다.

**제가 담당한 백엔드**
- 호스트·예약 도메인의 핵심 REST API
- 카카오 OAuth2/JWT, 이메일 인증 기반 비밀번호 재설정
- Redisson 분산 락을 활용한 예약 동시성 제어
- 숙소 대량 삭제 쿼리 개선, 결제 연동 및 GitHub Actions 배포 설정

**팀에서 함께 구현한 기능**에는 React 기반 화면, 지도·관광 큐레이션, 날씨, 리뷰, AI 챗봇 등이 있습니다. 팀 전체 기능을 개인 기여와 구분해 적었습니다.

[ERD · 제안서 · 발표 자료](https://github.com/munhee777/hotel-booking/tree/develop/docs) · [시연 영상](https://drive.google.com/file/d/1aLvJOjhpbnPIAw_CgQL5NRQCfP8i47C7/view?usp=share_link)

### [CineHub | 영화 커뮤니티](https://github.com/munhee777/cinehub)

게시글 등 CRUD 중심의 백엔드 기능과 REST API를 구현했습니다. JDBC 연결 기반과 DAO에서 SQL CRUD를 다루며 요청과 데이터 처리 흐름을 익혔습니다. 영화 관련 백엔드는 다른 팀원이 담당했습니다.

### Spring AI 학습 프로젝트

Spring AI 기반 서비스 개발 과정에서 생성형 AI 연동과 응답 처리 사례를 학습하고 있습니다. 진행 중인 예제는 [공개 저장소 목록](https://github.com/munhee777?tab=repositories)에서 확인할 수 있습니다.

## 트러블슈팅

### 예약 동시성 | Redisson 분산 락

- **문제:** 남은 객실을 여러 사용자가 동시에 예약하면 초과 예약 위험이 있었습니다.
- **해결:** Redis 기반 Redisson 분산 락으로 예약 자원 접근을 조정했습니다.
- **검증 기록:** 발표 자료에는 잔여 객실 6개, 가상 사용자 100명 동시 요청 시나리오에서 106건 중 6건 성공으로 기록되어 있습니다. 상세 조건과 수치 해석은 [발표 자료](https://github.com/munhee777/hotel-booking/blob/develop/docs/jeju-presentation-draft.pdf)에 공개했습니다.

### 숙소 대량 삭제 | JPA N+1

- **문제:** 숙소에 연결된 재고 데이터가 많을 때 반복 삭제 쿼리로 성능 저하가 발생했습니다.
- **해결:** 외래 키 제약을 고려해 삭제 순서를 설계하고 벌크 연산과 `@Modifying(clearAutomatically = true)`를 적용했습니다.
- **결과:** 반복 엔티티 삭제 경로를 벌크 삭제로 변경했습니다. 자료에 정량 전후 수치가 없어 별도 수치는 주장하지 않습니다.

### 배포 환경 설정 | GitHub Actions Secrets

- **문제:** 배포 과정에서 로컬 설정 파일에 의존할 수 없고 민감 값을 저장소에 포함할 수 없었습니다.
- **해결:** GitHub Secrets와 `deploy.yml`을 연결해 빌드 환경에 필요한 값을 주입했습니다.

### 팀 성능 개선 기록 | Redis 캐시

발표 자료의 측정 기록에서 메인 API 평균 응답 시간은 9.01초에서 226ms로, 처리량은 초당 약 10건에서 약 439건으로 개선되었습니다. **팀 프로젝트 결과로 표시하며 개인 담당 성과로 주장하지 않습니다.** 측정 조건은 [발표 자료](https://github.com/munhee777/hotel-booking/blob/develop/docs/jeju-presentation-draft.pdf)를 참고해 주세요.

## 학력 및 자격

- 한국방송통신대학교 컴퓨터과학과 졸업
- SQLD · 리눅스마스터 2급
- Oracle DBA 과정 수료
- Spring AI 기반 멀티 에이전트 서비스 개발 과정 수강 중
