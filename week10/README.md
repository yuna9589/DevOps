# 10주차 과제: Deployment와 Service

## 1. Replicas 5개 스케일링 결과 (`kubectl get pods`)
Deployment의 replicas 수를 5로 변경한 후 실행 결과

'''bash
$kubectl scale deployment guestbook --replicas=5$ kubectl get pods
NAME                        READY   STATUS    RESTARTS   AGE
guestbook-d579db6c5-2x8lp   1/1     Running   0          10s
guestbook-d579db6c5-5l8pt   1/1     Running   0          5m
guestbook-d579db6c5-9q2mr   1/1     Running   0          10s
guestbook-d579db6c5-k4z7t   1/1     Running   0          10s
guestbook-d579db6c5-rdzbn   1/1     Running   0          5m
