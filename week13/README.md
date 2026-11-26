# 방명록 (DevOps)

Kubernetes(Minikube) 환경에서 GitHub Actions, Argo CD, Prometheus/Grafana를 연동해 배포 및 모니터링을 구축한 방명록 프로젝트입니다.

## 1. 아키텍처

```text
코드 ──git push──▶ GitHub (yuna9589/DevOps)
                      │ PR + Branch Protection
                      ▼
               GitHub Actions ──테스트 & 빌드──▶ ghcr.io/yuna9589/guestbook:<해시>
                                                      │ 이미지 태그 PR (Argo CD 동기화)
                                                      ▼
┌──────────────────────── Kubernetes (minikube) ────────────────────────┐
│  [Service: guestbook (NodePort 30080)]                                │
│         │                                                             │
│  [Deployment: guestbook (replicas 2)] ── Pod ── Pod ◀── ConfigMap/Secret│
│         │                                                             │
│  [Service: redis (ClusterIP)] ── [Deployment: redis] ── Pod           │
└───────────────────────────────────────────────────────────────────────┘
          ▲
사용자 ──브라우저──┘
```

## 2. 기술 스택

- **App / DB:** Python (Flask), Redis
- **Infra / CI·CD:** Docker, GitHub Actions, GHCR, Kubernetes (Minikube), Argo CD
- **Monitoring:** Metrics Server, Prometheus, Grafana

## 3. 실행 방법

1. `minikube start --driver=docker`
2. `gh repo clone yuna9589/DevOps && cd DevOps/guestbook`
3. `kubectl apply -f k8s`
4. `kubectl get pods` (확인: `guestbook` Pod 2개, `redis` Pod 1개)
5. `minikube service guestbook`

## 4. 배포 절차

1. 작업 브랜치에서 코드 수정 후 PR 생성 및 `main` 머지
2. GitHub Actions 빌드 통과 후 `ghcr.io`에 새 이미지 푸시
3. `k8s/deployment.yaml` 이미지 태그를 최신 커밋 해시로 변경(PR) 후 Argo CD 자동 배포

## 5. 설정

- **ConfigMap (`guestbook-config`):** `APP_TITLE`, `THEME_COLOR`, `REDIS_HOST`, `REDIS_PORT`
- **Secret (`ghcr-secret`):** GHCR 이미지 풀 인증 정보

## 6. 트러블슈팅 기록

- **`CrashLoopBackOff` 반복 종료**
  - **증상/확인:** 파드 기동 직후 즉시 종료 (`kubectl logs` 에러 없음)
  - **원인/조치:** `app.py`에 `app.run(host="0.0.0.0", port=5000)` 누락 → 구문 추가 후 재배포
  - **결과:** `guestbook` 파드 `1/1 Running` 정상 유지
- **제목 `CI/CD` 중복 출력**
  - **증상/확인:** 화면 제목이 `방명록 (k8s) CI/CD CI/CD`로 중복 표시됨
  - **원인/조치:** `configmap.yaml`과 `index.html` 양쪽에 `CI/CD` 포함 → `APP_TITLE`을 `"방명록 (k8s)"`로 수정 후 파드 재시작
  - **결과:** `방명록 (k8s) CI/CD`로 정상 출력