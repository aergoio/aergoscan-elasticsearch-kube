# 1. elasticsearch helm 설치 및 업그레이드
  ```shell
  helm upgrade --atomic --install aergoscan-es ./elasticsearch
  ```

# 2. 데이터 초기화[local 제외]
* 데이터 초기화만 진행하는 차트로 완료 후 배포된 릴리즈는 제거 한다.
  * 내부에서 `Job` 만 실행됨
* local의 경우 `k3s` 의 기본 `pvc` 정책으로 인해 `pvc` 삭제 시 `pv` 볼륨도 같이 삭제되어 초기화를 할 필요가 없다.
  * `aws` 의 쿠버네티스 구현체의 `pvc` 정책은 `pvc` 삭제해도 `pv` 는 보존되어 별도로 초기화를 사용할 수 있다.

```
    # 볼륨 초기화 
    helm install --atomic aergoscan-es-init-data ./elasticsearch-init-data
    # 릴리즈 제거
    helm uninstall aergoscan-es-init-data
```
