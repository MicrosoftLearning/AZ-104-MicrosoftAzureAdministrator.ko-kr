---
lab:
  title: 09b - Azure Container Instances 구현
  module: Administer Serverless Computing
---

# <a name="lab-09b---implement-azure-container-instances"></a>랩 09b - Azure Container Instances 구현
# <a name="student-lab-manual"></a>학생용 랩 매뉴얼

## <a name="lab-scenario"></a>랩 시나리오

Contoso wants to find a new platform for its virtualized workloads. You identified a number of container images that can be leveraged to accomplish this objective. Since you want to minimize container management, you plan to evaluate the use of Azure Container Instances for deployment of Docker images.

대화형 가이드 형식으로 이 랩을 미리 보려면 **[여기를 클릭하세요](https://mslabs.cloudguides.com/en-us/guides/AZ-104%20Exam%20Guide%20-%20Microsoft%20Azure%20Administrator%20Exercise%2014)** .

## <a name="objectives"></a>목표

이 랩에서는 다음을 수행합니다.

- 작업 1: Azure Container Instance를 사용하여 Docker 이미지 배포
- 작업 2: Azure Container Instance의 기능 검토

## <a name="estimated-timing-20-minutes"></a>예상 소요 시간: 20분

## <a name="architecture-diagram"></a>아키텍처 다이어그램

![이미지](../media/lab09b.png)

## <a name="instructions"></a>Instructions

### <a name="exercise-1"></a>연습 1

#### <a name="task-1-deploy-a-docker-image-by-using-the-azure-container-instance"></a>작업 1: Azure Container Instance를 사용하여 Docker 이미지 배포

이 작업에서는 웹 애플리케이션에 대한 새 컨테이너 인스턴스를 만듭니다.

1. [Azure Portal](https://portal.azure.com)에 로그인합니다.

1. Azure Portal에서 **컨테이너 인스턴스**를 찾은 다음 **컨테이너 인스턴스** 블레이드에서 **+ 만들기**를 클릭합니다.

1. **Container Instance 만들기** 블레이드의 **기본** 탭에서 다음 설정을 지정합니다(다른 설정은 기본값으로 남겨둠).

    | 설정 | 값 |
    | ---- | ---- |
    | Subscription | 이 랩에서 사용 중인 Azure 구독의 이름 |
    | Resource group | 새 리소스 그룹 **az104-09b-rg1**의 이름 |
    | 컨테이너 이름 | **az104-9b-c1** |
    | 지역 | Azure Container Instances를 프로비전할 수 있는 지역 이름 |
    | 이미지 원본 | **빠른 시작 이미지** |
    | 이미지 | **mcr.microsoft.com/azuredocs/aci-helloworld:latest(Linux)** |

1. **다음: 네트워킹 >** 및 **컨테이너 인스턴스 만들기** 블레이드의 **네트워킹** 탭에서 다음 설정을 지정합니다(다른 설정은 기본값으로 유지).

    | 설정 | 값 |
    | --- | --- |
    | DNS 이름 레이블 | 유효하고 전역적으로 고유한 DNS 호스트 이름 |

    ><bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: Your container will be publicly reachable at dns-name-label.region.azurecontainer.io. If you receive a <bpt id="p1">**</bpt>DNS name label not available<ept id="p1">**</ept> error message, specify a different value.

1. **다음: 고급 >** , 변경하지 않고 **컨테이너 인스턴스 만들기** 블레이드의 **고급** 탭에서 설정을 검토하고 **검토 + 만들기**를 클릭한 다음, 유효성 검사를 통과했는지 확인하고 **만들기**를 클릭합니다.

    ><bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: Wait for the deployment to complete. This should take about 3 minutes.

    ><bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: While you wait, you may be interested in viewing the <bpt id="p2">[</bpt>code behind the sample application<ept id="p2">](https://github.com/Azure-Samples/aci-helloworld)</ept>. To view it, browse the <ph id="ph1">\\</ph>app folder.

#### <a name="task-2-review-the-functionality-of-the-azure-container-instance"></a>작업 2: Azure Container Instance의 기능 검토

이 작업에서는 컨테이너 인스턴스의 배포를 검토합니다.

1. 배포 블레이드에서 **리소스로 이동** 링크를 클릭합니다.

1. 컨테이너 인스턴스의 **개요** 블레이드에서 **상태**가 **실행 중**으로 보고되는지 확인합니다.

1. 컨테이너 인스턴스 **FQDN**의 값을 복사하고 새 브라우저 탭을 열고 해당 URL로 이동합니다.

1. **Azure Container Instance에 오신 것을 환영합니다** 페이지가 표시되는지 확인합니다.

1. 새 브라우저 탭을 닫고 Azure Portal로 돌아가서 컨테이너 인스턴스 블레이드의 **설정** 섹션에서 **컨테이너**를 클릭한 다음 **로그**를 클릭합니다.

1. 브라우저에 애플리케이션을 표시하여 생성된 HTTP GET 요청을 나타내는 로그 항목이 표시되는지 확인합니다.

#### <a name="clean-up-resources"></a>리소스 정리

><bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: Remember to remove any newly created Azure resources that you no longer use. Removing unused resources ensures you will not see unexpected charges.

>Contoso는 가상화된 워크로드에 대한 새로운 플랫폼을 찾고자 합니다. 

1. Azure Portal의 **Cloud Shell** 창에서 **PowerShell** 세션을 엽니다.

1. 다음 명령을 실행하여 이 모듈의 전체 랩에서 생성된 모든 리소스 그룹을 나열합니다.

   ```powershell
   Get-AzResourceGroup -Name 'az104-09b*'
   ```

1. 다음 명령을 실행하여 이 모듈의 랩 전체에서 만든 모든 리소스 그룹을 삭제합니다.

   ```powershell
   Get-AzResourceGroup -Name 'az104-09b*' | Remove-AzResourceGroup -Force -AsJob
   ```

    >**참고**: 이 명령은 -AsJob 매개 변수에 의해 결정되어 비동기로 실행되므로, 동일한 PowerShell 세션 내에서 이 명령을 실행한 직후 다른 PowerShell 명령을 실행할 수 있지만 리소스 그룹이 실제로 제거되기까지는 몇 분 정도 걸립니다.

#### <a name="review"></a>검토

이 랩에서는 다음을 수행합니다.

- Azure Container Instance를 사용하여 Docker 이미지 배포
- Azure Container Instance 기능 검토
