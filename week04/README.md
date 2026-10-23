# Week 04: Docker Compose 및 멀티 컨테이너 오케스트레이션

## 1. 학습 목표
- 다중 컨테이너 애플리케이션 아키텍처 이해
- docker-compose.yml을 활용한 복수 서비스(Web, DB 등) 일괄 관리
- 네트워크 및 볼륨(Volume)을 통한 데이터 영속성 유지

## 2. 주요 실습 내용
- Docker Compose 구성:
  - YAML 기반 구성 파일 작성(services, ports, volumes, environment)
  - docker compose up -d를 이용한 멀티 컨테이너 동시 실행
  - docker compose down을 활용한 리소스 깔끔하게 정리
- 데이터 영속성 및 서비스 연결:
  - 컨테이너가 재시작되어도 데이터가 유지되도록 호스트 볼륨 매핑

## 3. 트러블슈팅 및 배운 점
- 여러 명령어를 일일이 칠 필요 없이 파일 하나로 전체 인프라를 코드(IaC)로 관리하는 편의성을 체감함.
