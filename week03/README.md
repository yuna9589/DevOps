# Week 03: Docker 기초와 컨테이너 가상화

## 1. 학습 목표
- 가상머신(VM)과 컨테이너(Container)의 차이점 이해
- Docker 엔진 기본 명령어(Pull, Run, Logs, PS, RM) 실습
- Dockerfile을 활용한 커스텀 컨테이너 이미지 빌드

## 2. 주요 실습 내용
- **도커 기본 명령어**:
  - docker pull: Docker Hub로부터 공식 이미지 다운로드
  - docker run -d -p: 백그라운드 데몬 실행 및 호스트 포트 포워딩
  - docker ps, docker logs: 실행 중인 컨테이너 상태 모니터링
- Dockerfile 작성 및 실행:
  - 베이스 이미지 지정(FROM), 파일 복사(COPY), 환경 변수 설정(ENV) 및 실행 명령어(CMD) 작성

## 3. 트러블슈팅 및 배운 점
- 컨테이너는 독립된 환경을 제공하여 호스트 환경을 오염시키지 않고 애플리케이션을 신속하게 실행할 수 있음을 확인함.
