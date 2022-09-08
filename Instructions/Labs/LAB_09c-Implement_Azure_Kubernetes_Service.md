---
lab:
  title: 09c - Azure Kubernetes Service 구현
  module: Administer Serverless Computing
---

# <a name="lab-09c---implement-azure-kubernetes-service"></a>랩 09c - Azure Kubernetes Service 구현
# <a name="student-lab-manual"></a>학생용 랩 매뉴얼

## <a name="lab-scenario"></a>랩 시나리오

Contoso has a number of multi-tier applications that are not suitable to run by using Azure Container Instances. In order to determine whether they can be run as containerized workloads, you want to evaluate using Kubernetes as the container orchestrator. To further minimize management overhead, you want to test Azure Kubernetes Service, including its simplified deployment experience and scaling capabilities.

대화형 가이드 형식으로 이 랩을 미리 보려면 **[여기를 클릭하세요](https://mslabs.cloudguides.com/en-us/guides/AZ-104%20Exam%20Guide%20-%20Microsoft%20Azure%20Administrator%20Exercise%2015)** .

## <a name="objectives"></a>목표

이 랩에서는 다음을 수행합니다.

+ 작업 1: Microsoft.Kubernetes 및 Microsoft.KubernetesConfiguration 리소스 공급자를 등록합니다.
+ 작업 2: Azure Kubernetes Service 클러스터 배포
+ 작업 3: Azure Kubernetes Service 클러스터에 Pod 배포
+ 작업 4: Azure Kubernetes Service 클러스터에서 컨테이너화된 워크로드 크기 조정

## <a name="estimated-timing-40-minutes"></a>예상 소요 시간: 40분

## <a name="architecture-diagram"></a>아키텍처 다이어그램

![이미지](../media/lab09c.png)

## <a name="instructions"></a>Instructions

### <a name="exercise-1"></a>연습 1

#### <a name="task-1-register-the-microsoftkubernetes-and-microsoftkubernetesconfiguration-resource-providers"></a>작업 1: Microsoft.Kubernetes 및 Microsoft.KubernetesConfiguration 리소스 공급자를 등록합니다.

이 작업에서는 Azure Kubernetes Service 클러스터를 배포하는 데 필요한 리소스 공급자를 등록합니다.

1. [Azure Portal](https://portal.azure.com)에 로그인합니다.

1. Azure Portal에서 오른쪽 상단의 아이콘을 클릭하여 **Azure Cloud Shell**을 엽니다.

1. **Bash**와 **PowerShell** 중에서 선택하라는 메시지가 표시되면 **PowerShell**을 선택합니다.

    >**참고**: **Cloud Shell**을 처음 시작했는데 **탑재된 스토리지 없음**이라는 메시지가 표시되면 이 랩에서 사용하는 구독을 선택하고 **스토리지 만들기**를 클릭합니다.

1. Cloud Shell 창에서 다음 명령을 실행하여 Microsoft.Kubernetes와 Microsoft.KubernetesConfiguration 리소스 공급자를 등록합니다.

   ```powershell
   Register-AzResourceProvider -ProviderNamespace Microsoft.Kubernetes

   Register-AzResourceProvider -ProviderNamespace Microsoft.KubernetesConfiguration
   ```

1. Cloud Shell 창을 닫습니다.

#### <a name="task-2-deploy-an-azure-kubernetes-service-cluster"></a>작업 2: Azure Kubernetes Service 클러스터 배포

이 작업에서는 Azure Portal을 사용하여 Azure Kubernetes 서비스 클러스터를 배포합니다.

1. Azure Portal에서 **Kubernetes 서비스**를 검색하여 찾고 **Kubernetes 서비스** 블레이드에서 **+ 만들기**, **+ Kubernetes 클러스터 만들기**를 차례로 클릭합니다.

1. **Kubernetes 클러스터 만들기** 블레이드의 **기본** 탭에서 다음 설정을 지정합니다(다른 설정은 기본값으로 남겨둡니다).

    | 설정 | 값 |
    | ---- | ---- |
    | Subscription | 이 랩에서 사용 중인 Azure 구독의 이름 |
    | Resource group | 새 리소스 그룹 **az104-09c-rg1**의 이름 |
    | 클러스터 사전 설정 구성 | **Dev/Test ($)** |
    | Kubernetes 클러스터 이름 | **az104-9c-aks1** |
    | 지역 | Kubernetes 클러스터를 프로비전할 수 있는 지역의 이름 |
    | 가용성 영역 | **없음**(모든 상자 선택 취소) |
    | Kubernetes 버전 | 기본값 수락 |
    | API 서버 가용성 | 기본값 수락 |
    | 노드 크기 | 기본값 수락 |
    | 스케일링 방법 | **수동** |
    | 노드 수 | **1** |

1. **다음: 노드 풀 >** 을 클릭하고, **Kubernetes 클러스터 만들기** 블레이드의 **노드 풀** 탭에서 다음 설정을 지정합니다(다른 설정은 기본값으로 둡니다).

    | 설정 | 값 |
    | ---- | ---- |
    | 가상 노드 사용 | **사용 안 함**(기본값) |

1. **다음: 액세스 >** 를 클릭하고, **Kubernetes 클러스터 만들기** 블레이드의 **액세스** 탭에서 다음 설정을 지정합니다(다른 설정은 기본값으로 유지).

    | 설정 | 값 |
    | ---- | ---- |
    | 인증 방법 | **시스템 할당 관리 ID**(기본값 - 변경 없음) | 
    | RBAC(역할 기반 액세스 제어) | **Enabled** |

1. **다음: 네트워킹 >** 을 클릭하고, **Kubernetes 클러스터 만들기** 블레이드의 **네트워킹** 탭에서 다음 설정을 지정합니다(다른 설정은 기본값으로 유지).

    | 설정 | 값 |
    | ---- | ---- |
    | 네트워크 구성 | **kubenet** |
    | DNS 이름 접두사 | 유효하고 전역적으로 고유한 DNS 접두사|

1. **다음: 통합 >** 을 클릭하고, **Kubernetes 클러스터 만들기** 블레이드의 **통합** 탭에서 **컨테이너 모니터링**을 **사용 안 함**으로 설정하고, **검토 + 만들기**를 클릭하고, 유효성 검사를 통과했는지 확인하고, **만들기**를 클릭합니다.

    ><bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: In production scenarios, you would want to enable monitoring. Monitoring is disabled in this case since it is not covered in the lab.

    ><bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: Wait for the deployment to complete. This should take about 10 minutes.

#### <a name="task-3-deploy-pods-into-the-azure-kubernetes-service-cluster"></a>작업 3: Azure Kubernetes Service 클러스터에 Pod 배포

이 작업에서는 Azure Kubernetes Service 클러스터에 Pod를 배포합니다.

1. 배포 블레이드에서 **리소스로 이동** 링크를 클릭합니다.

1. **설정 ** 섹션의 **az104-9c-aks1** Kubernetes 서비스 블레이드에서 **노드 풀을 클릭합니다**.

1. **az104-9c-aks1 - 노드 풀** 블레이드에서 클러스터가 하나의 노드가 있는 단일 풀로 구성되어 있는지 확인합니다.

1. Azure Portal에서 오른쪽 상단의 아이콘을 클릭하여 **Azure Cloud Shell**을 엽니다.

1. **Azure Cloud Shell**을 **Bash**(검은색 배경)로 전환합니다.

1. Cloud Shell 창에서 다음 명령을 실행하여 AKS 클러스터에 액세스할 때 필요한 자격 증명을 검색하세요.

    ```sh
    RESOURCE_GROUP='az104-09c-rg1'

    AKS_CLUSTER='az104-9c-aks1'

    az aks get-credentials --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER
    ```

1. **Cloud Shell** 창에서 다음 명령을 실행하여 AKS 클러스터에 연결되었는지 확인하세요.

    ```sh
    kubectl get nodes
    ```

1. **Cloud Shell** 창에서 출력을 검토하고 이 시점에 클러스터를 구성하고 있는 하나의 노드가 **준비** 상태를 보고하고 있는지 확인합니다.

1. **Cloud Shell** 창에서 다음 명령을 실행하여 Docker Hub에서 **nginx** 이미지를 배포합니다.

    ```sh
    kubectl create deployment nginx-deployment --image=nginx
    ```

    > **참고**: 배포 이름(nginx-deployment)을 입력할 때 소문자를 사용해야 합니다.

1. **Cloud Shell** 창에서 다음 명령을 실행하여 Kubernetes Pod가 제대로 만들어졌는지 확인합니다.

    ```sh
    kubectl get pods
    ```

1. **Cloud Shell** 창에서 다음 명령을 실행하여 배포 상태를 확인합니다.

    ```sh
    kubectl get deployment
    ```

1. **Cloud Shell** 창에서 다음 명령을 실행하여 Pod를 인터넷에서 사용할 수 있게 만듭니다.

    ```sh
    kubectl expose deployment nginx-deployment --port=80 --type=LoadBalancer
    ```

1. **Cloud Shell** 창에서 다음 명령을 실행하여 공용 IP 주소가 프로비전되었는지 확인합니다.

    ```sh
    kubectl get service
    ```

1. Re-run the command until the value in the <bpt id="p1">**</bpt>EXTERNAL-IP<ept id="p1">**</ept> column for the <bpt id="p2">**</bpt>nginx-deployment<ept id="p2">**</ept> entry changes from <bpt id="p3">**</bpt><ph id="ph1">\&lt;pending\&gt;</ph><ept id="p3">**</ept> to a public IP address. Note the public IP address in the <bpt id="p1">**</bpt>EXTERNAL-IP<ept id="p1">**</ept> column for <bpt id="p2">**</bpt>nginx-deployment<ept id="p2">**</ept>.

1. Open a browser window and navigate to the IP address you obtained in the previous step. Verify that the browser page displays the <bpt id="p1">**</bpt>Welcome to nginx!<ept id="p1">**</ept> message.

#### <a name="task-4-scale-containerized-workloads-in-the-azure-kubernetes-service-cluster"></a>작업 4: Azure Kubernetes Service 클러스터에서 컨테이너화된 워크로드 크기 조정

이 작업에서는 Pod 갯수와 클러스터 노드 갯수를 가로로 조정합니다.

1. **Cloud Shell** 창에서 다음 명령을 실행하여 Pod 수를 2로 늘려 배포를 스케일링합니다.

    ```sh
    kubectl scale --replicas=2 deployment/nginx-deployment
    ```

1. **Cloud Shell** 창에서 다음 명령을 실행하여 배포 크기가 잘 조정되었는지 확인합니다.

    ```sh
    kubectl get pods
    ```

    > **참고**: 명령의 출력을 검토하여 Pod 수가 2로 증가했는지 확인합니다.

1. **Cloud Shell** 창에서 노드 수를 2로 늘려 클러스터를 스케일 아웃하려면 다음을 실행합니다.

    ```sh
    RESOURCE_GROUP='az104-09c-rg1'

    AKS_CLUSTER='az104-9c-aks1'

    az aks scale --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER --node-count 2
    ```

    > Contoso에는 Azure Container Instances를 사용하여 실행하기에는 적합하지 않은 많은 다중 계층 애플리케이션이 있습니다.

1. **Cloud Shell** 창에서 다음 명령을 실행하여 클러스터 스케일링이 잘 수행되었는지 확인합니다.

    ```sh
    kubectl get nodes
    ```

    > **참고**: 명령의 출력을 검토하여 노드 수가 2로 증가했는지 확인합니다.

1. **Cloud Shell** 창에서 다음 명령을 실행하여 배포 크기를 조정합니다.

    ```sh
    kubectl scale --replicas=10 deployment/nginx-deployment
    ```

1. **Cloud Shell** 창에서 다음 명령을 실행하여 배포 크기가 잘 조정되었는지 확인합니다.

    ```sh
    kubectl get pods
    ```

    > **참고**: 명령의 출력을 검토하여 Pod 수가 10으로 증가했는지 확인합니다.

1. **Cloud Shell** 창에서 다음을 실행하여 클러스터 노드 전반의 Pod 분포를 검토합니다.

    ```sh
    kubectl get pod -o=custom-columns=NODE:.spec.nodeName,POD:.metadata.name
    ```

    > **참고**: 명령의 출력을 검토하여 두 노드에 Pod가 분산되어 있는지 확인합니다.

1. **Cloud Shell** 창에서 다음 명령을 실행하여 배포를 삭제합니다.

    ```sh
    kubectl delete deployment nginx-deployment
    ```

1. **Cloud Shell** 창을 닫습니다.

#### <a name="clean-up-resources"></a>리소스 정리

>컨테이너화된 워크로드로 실행할 수 있는지 여부를 확인하기 위해 Kubernetes를 컨테이너 오케스트레이터로 사용하여 평가하려고 합니다.

>관리 오버헤드를 더욱 최소화하기 위해 간소화된 배포 환경 및 스케일링 기능을 포함하여 Azure Kubernetes Service를 테스트하려고 합니다. 

1. Azure Portal의 **Cloud Shell** 창에서 **Bash** 세션을 시작합니다.

1. 다음 명령을 실행하여 이 모듈의 전체 랩에서 생성된 모든 리소스 그룹을 나열합니다.

   ```sh
   az group list --query "[?starts_with(name,'az104-09c')].name" --output tsv
   ```

1. 다음 명령을 실행하여 이 모듈의 랩 전체에서 만든 모든 리소스 그룹을 삭제합니다.

   ```sh
   az group list --query "[?starts_with(name,'az104-09c')].[name]" --output tsv | xargs -L1 bash -c 'az group delete --name $0 --no-wait --yes'
   ```

    >**참고**: 명령은 비동기적으로 실행되므로(--nowait 매개 변수에 의해 결정됨) 동일한 Bash 세션 내에서 즉시 다른 Azure CLI 명령을 실행할 수 있지만 리소스 그룹이 실제로 제거되기까지 몇 분 정도 걸립니다.

#### <a name="review"></a>검토

이 랩에서는 다음을 수행합니다.

+ Azure Kubernetes Service 클러스터 배포
+ Pod를 Azure Kubernetes Service 클러스터에 배포
+ Azure Kubernetes Service 클러스터에서 컨테이너화된 워크로드를 스케일링
