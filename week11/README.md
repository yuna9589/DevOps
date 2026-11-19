# 11주차: 쿠버네티스 설정과 상태 점검

## 1. Secret 보안 한계
- Secret은 암호화가 아닌 Base64 인코딩이므로 `base64 -d`로 누구나 원본 값을 확인할 수 있어 단독 보안 수단으로 안전하지 않음.

## 2. ConfigMap 설정 변경
- 이미지 재빌드 없이 ConfigMap 수정 후 `kubectl rollout restart deployment guestbook`으로 새 Pod에 설정 반영 완료.

## 3. Probe 실패 실험
- **Readiness 실패**: Redis 종료 시 `Running` 상태지만 `READY 0/1`로 전환되며 트래픽 차단 (재시작 안 함).
- **Liveness 실패**: 잘못된 경로(`/devops`) 설정 시 컨테이너가 반복 재시작되며 `RESTARTS` 증가.

## 4. 트러블슈팅 3단 루틴
1. `kubectl get pods` : Pod 상태(STATUS, READY, RESTARTS) 확인
2. `kubectl describe pod <이름>` : 하단 Events에서 원인 확인
3. `kubectl logs <이름>` : 컨테이너 내부 에러 로그 확인 (재시작 시 `--previous`)
