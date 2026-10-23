# Week 02: 실습 환경 구축과 버전 관리 기초

## 1. 학습 목표
- 가상화(Bare-metal, Hypervisor, Container)의 개념 및 차이점 이해
- WSL2 및 Ubuntu를 활용한 리눅스 개발 환경 구축
- Linux 기본 명령어(파일, 디렉터리, 권한) 및 Git/GitHub 버전 관리 숙달

## 2. 주요 실습 내용
- WSL2 환경 구성: Windows 환경에서 Ubuntu 배포판을 활성화하여 리눅스 터미널 환경 구축
- Linux 기본 명령어: cd, ls, mkdir, echo 등을 활용한 파일/디렉터리 조작
- Git/GitHub 실습:
  - git init을 통한 버전 관리 시작
  - git add 및 git commit을 활용한 파일 변화 스냅샷 기록
  - GitHub 저장소 생성(gh repo create) 및 원격 저장소 푸시

## 3. 트러블슈팅 및 배운 점
- 메인 브랜치 보호 정책(Protected Branch)으로 인해 direct push가 차단되었을 때, git switch -c를 이용해 작업 브랜치를 새로 생성하고 우회하여 푸시하는 깃 워크플로우를 실습함.
