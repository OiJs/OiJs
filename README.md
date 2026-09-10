### 이준서 — Backend Developer

## About Me

대용량 트래픽 처리와 분산 환경(MSA)에서 성능 최적화를 통해 서비스를 개선하는 백엔드 개발자입니다.

정해진 구현에 안주하기보다, 병목 지점을 직접 측정하고 구조적으로 해결하는 데 집중합니다. Redis 기반 동시성 제어부터 가상 스레드 기반 배치 병렬화까지, 트래픽과 지연 문제를 아키텍처 레벨에서 풀어내는 개발자가 되고자 합니다.

- 조선대학교 전자공학부(지능형 IoT전공) 학사 졸업
- NHN Academy — JavaBackend 12기 수료 · AIOT 웹서비스 개발자(Java AIOT 03기) 과정 수료
- oijs9663@gmail.com

## Tech Stack

**Language & Framework**

![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![Spring Data JPA](https://img.shields.io/badge/Spring%20Data%20JPA-6DB33F?style=flat-square&logo=spring&logoColor=white)
![Spring Batch](https://img.shields.io/badge/Spring%20Batch-6DB33F?style=flat-square&logo=spring&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring%20Security-6DB33F?style=flat-square&logo=springsecurity&logoColor=white)
![Spring AI](https://img.shields.io/badge/Spring%20AI-6DB33F?style=flat-square&logo=spring&logoColor=white)

**Data & Messaging**

![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=flat-square&logo=rabbitmq&logoColor=white)
![InfluxDB](https://img.shields.io/badge/InfluxDB-22ADF6?style=flat-square&logo=influxdb&logoColor=white)

**Infra & DevOps**

![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![SonarQube](https://img.shields.io/badge/SonarQube-4E9BCD?style=flat-square&logo=sonarqube&logoColor=white)

## Featured Projects

### Book2OnAndOn — Coupon Service | MSA 기반 도서 이커머스 플랫폼

대규모 트래픽을 고려한 도서 이커머스 플랫폼의 쿠폰·배치 서비스 · 2025.11 ~ 2025.12 · 7주 · 7인 협업
역할: Coupon Service 리드 개발 · User Service Batch 설계 (137 commits · 기여도 93%)

Tech · Java 21 · Spring Boot 3.x · Spring Data JPA · PostgreSQL · Redis · RabbitMQ · ShedLock

대규모 트래픽 환경에서 발견한 4가지 핵심 문제를 구조적으로 해결했습니다.

**1. Redis + RabbitMQ 기반 선착순 쿠폰 발급 동시성 제어**
- 문제 · 비관적 락(@Lock) 적용으로 트랜잭션 대기 중 DB 커넥션 풀 고갈
- 해결 · Redis 인메모리 연산(중복/재고 검증)과 RabbitMQ 메시지 큐잉으로 DB 접근을 비동기 분리
- 결과 · 타임아웃 장애 0%, 응답 시간 99% 단축, TPS 77% 향상

**2. 이벤트 기반 비동기 통신으로 서비스 결합도 완화**
- 문제 · 동기 호출 구조로 쿠폰 서비스 장애가 회원가입 실패로 직결되는 강결합
- 해결 · RabbitMQ 비동기 이벤트 발행 + DLQ 라우팅으로 장애 격리
- 결과 · 타 서비스 장애 상황에서도 메인 API 가용성 100% 보장

**3. 분산 스케줄링 제어 및 대용량 배치 최적화**
- 문제 · Scale-out 환경에서 스케줄러 중복 실행에 따른 데이터 오염 위험, 인덱스 부재로 배치 성능 저하
- 해결 · ShedLock 분산 락으로 단일 인스턴스 실행 보장 + 복합 인덱스 추가 + JDBC Bulk 방식으로 리팩토링
- 결과 · 데이터 오염 100% 차단, 배치 처리 시간 45분 → 15분(66% 단축)

**4. N+1 쿼리 제거로 조회 성능 개선**
- 문제 · MemberCoupon 조회 시 지연 로딩으로 1 + 2N회 쿼리 발생
- 해결 · JPQL JOIN FETCH + @BatchSize(100) IN절 배치 처리
- 결과 · 쿼리 11회 → 1회(90.9% 감소)

[GitHub](https://github.com/nhnacademy-be12-Book2OnAndOn/Book2OnAndOn-coupon-service) · [Live Demo](https://book2onandon.shop)

---

### InsightOn — 스마트 오피스 IoT 관제 플랫폼

IoT 센서 데이터 기반 실시간 위험 감지 및 AI 리포트 생성 플랫폼 · 2026.07 ~ 2026.09 · 11주 · 8인 협업
역할: InsightOn-ai(AI 서비스) 리드 개발 · InsightOn-core(게이트웨이) 일부 (171 commits · 기여도 96%+)

Tech · Spring Boot 3.x · Spring AI(Google Gemini) · Spring Data JPA · PostgreSQL · InfluxDB · Redis · RabbitMQ · ShedLock

**1. 다중 인스턴스 MQTT 연결 소유권 분산**
- 문제 · 코디네이터 없는 다중 인스턴스 환경에서 같은 게이트웨이에 여러 인스턴스가 동시 접속해 clientId 충돌(연결 뺏기) 위험
- 해결 · 해시 기반 선호 소유자 샤딩 + Redis SETNX 분산 락으로 소유권을 결정론적으로 배타 관리, tick마다 캐시-DB 자가 치유
- 결과 · Testcontainers 검증(인스턴스 2개, 100틱 동시 실행) 결과 소유권 중복 0건 달성

**2. Graceful Shutdown 중 분산 락 반납 실패 버그 해결**
- 문제 · 락 반납 로직이 @PreDestroy에 있었으나 SmartLifecycle.stop()이 먼저 실행돼 Redis 연결이 끊긴 뒤라 매번 반납 실패
- 해결 · ContextClosedEvent가 SmartLifecycle 정지보다 먼저 발행됨을 확인, @EventListener(ContextClosedEvent)로 교체
- 결과 · 락 반납 성공률 0% → 100% 개선

**3. 가상 스레드로 리포트 배치 병렬화**
- 문제 · location마다 DB 조회·Feign·LLM 호출을 순차 처리해 location 수만큼 지연 누적
- 해결 · Executors.newVirtualThreadPerTaskExecutor() + Semaphore(10)로 location별 가상 스레드 병렬 처리
- 결과 · 배치 처리 시간 3,163ms → 325ms(약 9.2배 단축)

**4. LLM 호출 배치화로 토큰 사용량 최적화**
- 문제 · 패턴마다 LLM을 개별 호출해 지연·입력 토큰이 패턴 수에 비례해 증가
- 해결 · 모든 패턴을 하나의 프롬프트로 묶어 LLM 호출 1회로 구조화된 결정 리스트 일괄 수신
- 결과 · 패턴 3개 동시 발생 케이스에서도 LLM 호출 1회 고정 검증

[GitHub](https://github.com/nhnacademy-aiot3-insighton/InsightOn-ai) · [Live Demo](https://insighton.store)

## GitHub Activity

![OiJs's contribution graph](https://ghchart.rshah.org/OiJs)

## Certifications

| 자격 | 발급 기관 | 취득일 |
|---|---|---|
| 정보처리기사 | 한국산업인력공단 | 2025.09 |
| SQL 개발자(SQLD) | 한국데이터산업진흥원(Kdata) | 2024.09 |
