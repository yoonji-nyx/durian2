# cicd-platform-gitops

ArgoCD가 감시하는 배포 설정 저장소입니다. 앱 코드는 `cicd-platform` 저장소에 있습니다.

```
apps/sample-app/
├── base/                    # 공통 매니페스트 (Deployment, Service)
└── overlays/
    ├── staging/             # staging 환경 (자동 동기화)
    └── prod/                # prod 환경 (수동 동기화, replicas 2)
```

## 이미지 태그 변경

각 overlay의 `kustomization.yaml` 안 `images[].newTag` 값이 배포될 버전입니다.
태그 변경은 반드시 커밋/PR로 하고, 클러스터에 직접 `kubectl apply` 하지 않습니다.

## 롤백

이전 커밋으로 `git revert` 후 push 하면 ArgoCD가 이전 상태로 되돌립니다.
