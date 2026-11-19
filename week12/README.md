# 12주차: GitHub Actions를 활용한 CI 구축

## 1. 실습 요약
- **CI 자동화**: `.github/workflows/build.yml`을 작성해 코드 푸시 및 PR 시 **린트(`ruff`) → 단위 테스트(`unittest`) → Docker 이미지 빌드 및 GHCR 게시** 파이프라인 구축[cite: 33, 37, 40].
- **오류 검증 (`빨간 X → 초록 ✓`)**: 문법 오류, 변수 오타(`APP_TITL`), 기능 오류(`/healthz` 500 반환)를 의도적으로 주입해 CI 단계에서 빌드 중단 및 차단 확인[cite: 52, 55, 57].
- **브랜치 보호**: `main` 브랜치에 Ruleset(`main-protector`)을 적용해 PR 및 `build` 체크 통과 없이 머지되지 않도록 설정[cite: 63, 64].

## 2. 트러블슈팅
- **워크플로 미인식**: `build.yml`을 저장소 최상단 `.github/workflows/` 경로로 이동하여 해결[cite: 50].
- **워크플로 푸시 거절**: `gh auth refresh -h github.com -s workflow`로 토큰에 `workflow` 권한을 추가해 해결.
- **Minikube 이미지 Pull 오류**: `deployment.yaml`의 이미지 주소를 `ghcr.io/yuna9589/guestbook`으로 수정하여 해결[cite: 1].
