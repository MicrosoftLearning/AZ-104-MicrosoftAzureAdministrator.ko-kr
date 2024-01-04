---
lab:
  title: '랩 09b: Azure 컨테이너 구현'
  module: Administer PaaS Compute Options
---

# 랩 09b - Azure 컨테이너 구현

## 랩 소개

이 랩에서는 Azure Container Instances 및 Azure Container Apps를 구현하는 방법을 알아봅니다. azure Container Instance를 배포하여 헬로 월드 앱을 표시하는 방법을 알아봅니다.
기본 Azure Container App을 배포하는 방법을 알아봅니다. 

이 랩에는 Azure 구독이 필요합니다. 구독 유형은 이 랩의 기능 가용성에 영향을 줄 수 있습니다. 지역을 변경할 수 있지만 단계는 미국 동부를 사용하여 작성됩니다.

## 예상 소요 시간: 30분

## 랩 시나리오

조직에는 온-프레미스 데이터 센터의 가상 머신에서 실행되는 웹 애플리케이션이 있습니다. 조직은 모든 애플리케이션을 클라우드로 이동하려고 하지만 관리할 서버가 많이 없도록 하고 싶지는 않습니다. Azure Container Instances 및 Docker를 평가하기로 결정합니다. 또한 Azure 컨테이너 앱을 배포하고 테스트하려고 합니다.

## 대화형 랩 시뮬레이션

이 항목에 유용할 수 있는 대화형 랩 시뮬레이션이 있습니다. 시뮬레이션을 사용하면 비슷한 시나리오를 원하는 속도로 클릭할 수 있습니다. 대화형 시뮬레이션과 이 랩 사이에는 차이점이 있지만, 대부분의 핵심 개념은 동일합니다. Azure 구독은 필요하지 않습니다.

+ [Azure Container Instances를 배포합니다](https://mslearn.cloudguides.com/en-us/guides/AZ-900%20Exam%20Guide%20-%20Azure%20Fundamentals%20Exercise%203). Azure Container Instances를 사용하여 Docker 컨테이너를 만들고 구성하고 배포합니다. 
+ [Azure Container Instances를 구현합니다](https://mslabs.cloudguides.com/guides/AZ-104%20Exam%20Guide%20-%20Microsoft%20Azure%20Administrator%20Exercise%2014).  Azure Container Instances를 사용하여 Docker 이미지를 배포합니다. 

## 작업

- 작업 1: Docker 이미지를 사용하여 Azure Container Instance 배포
- 작업 2: Azure Container Instance의 기능 검토
- 작업 3: Azure Container App 및 환경 만들기
- 작업 4: 컨테이너 앱 배포 및 테스트

## 작업 1 및 2: Azure Container Instances 아키텍처 다이어그램

![작업의 다이어그램.](../media/az104-lab09baci-architecture-diagram.png)

## 작업 1: Docker 이미지를 사용하여 Azure Container Instance 배포

이 작업에서는 웹 애플리케이션에 대한 새 컨테이너 인스턴스를 만듭니다. Docker는 컨테이너라는 격리된 환경에서 애플리케이션을 패키지하고 실행하는 기능을 제공하는 플랫폼입니다. Azure Container Instances는 컨테이너 이미지에 대한 컴퓨팅 환경을 제공합니다.

1. **Azure Portal** - `https://portal.azure.com`에 로그인합니다.

1. Azure Portal에서 검색하여 선택한 `Container instances` 다음 컨테이너 인스턴스** 블레이드에서 **+ 만들기**를 클릭합니다**.

1. **Container Instance 만들기** 블레이드의 **기본** 탭에서 다음 설정을 지정합니다(다른 설정은 기본값으로 남겨둠).

    | 설정 | 값 |
    | ---- | ---- |
    | 구독 | Azure 구독의 이름 |
    | Resource group | `az104-rg9` (필요한 ** 경우새로** 만들기) |
    | 컨테이너 이름 | `az104-c1` |
    | 지역 | **미국** 동부(또는 가까운 지역)|
    | 이미지 원본 | **빠른 시작 이미지** |
    | 이미지 | **mcr.microsoft.com/azuredocs/aci-helloworld:latest(Linux)** |

1. **다음: 네트워킹 >** 및 **컨테이너 인스턴스 만들기** 블레이드의 **네트워킹** 탭에서 다음 설정을 지정합니다(다른 설정은 기본값으로 유지).

    | 설정 | 값 |
    | --- | --- |
    | DNS 이름 레이블 | 유효하고 전역적으로 고유한 DNS 호스트 이름 |

    >**참고**: dns-name-label.region.azurecontainer.io에서 컨테이너에 공개적으로 연결할 수 있습니다. **DNS 이름 레이블을 사용할 수 없음** 오류 메시지가 표시되면, 다른 값을 지정하세요.

1. 다음: 고급 > 클릭하고 **, 변경하지 않고 컨테이너 인스턴스** 만들기 블레이드의 **고급** 탭에서 **설정을 검토**합니다.

 1. 검토 + 만들기를 클릭하고 **유효성 검사가 통과되었는지 확인하고 만들기**를 선택합니다**.**

    >**참고**: 배포가 완료될 때까지 기다립니다. 이 작업은 2-3분 정도 걸립니다.

    >**참고**: 기다리는 동안 [샘플 애플리케이션에 있는 코드](https://github.com/Azure-Samples/aci-helloworld)를 확인할 수 있습니다. 이 코드를 보려면 \\앱 폴더를 찾아보세요.

## 작업 2: Azure Container Instance의 기능 검토

이 작업에서는 컨테이너 인스턴스의 배포를 검토합니다. 기본적으로 Azure Container Instance는 포트 80을 통해 액세스할 수 있습니다. 인스턴스가 배포된 후 이전 작업에서 제공한 DNS 이름을 사용하여 컨테이너로 이동할 수 있습니다.

1. 배포 블레이드에서 **리소스로 이동** 링크를 클릭합니다.

1. 컨테이너 인스턴스의 **개요** 블레이드에서 **상태**가 **실행 중**으로 보고되는지 확인합니다.

1. 컨테이너 인스턴스 **FQDN**의 값을 복사하고 새 브라우저 탭을 열고 해당 URL로 이동합니다.

     ![포털의 ACI 개요 페이지 스크린샷.](../media/az104-lab09b-aci-overview.png)

1. **Azure Container Instance에 오신 것을 환영합니다** 페이지가 표시되는지 확인합니다.

1. 새 브라우저 탭을 닫고 Azure Portal로 돌아가서 컨테이너 인스턴스 블레이드의 **설정** 섹션에서 **컨테이너**를 클릭한 다음 **로그**를 클릭합니다.

1. 브라우저에 애플리케이션을 표시하여 생성된 HTTP GET 요청을 나타내는 로그 항목이 표시되는지 확인합니다.

## 작업 3 및 4: Azure Container Apps 아키텍처 다이어그램

![작업의 다이어그램.](../media/az104-lab09baca-architecture-diagram.png)

## 작업 3: 컨테이너 앱 및 환경 만들기

Azure Container Apps는 관리되는 Kubernetes 클러스터의 개념을 한 단계 더 발전시키고 클러스터 환경을 관리하고 클러스터 위에 다른 관리형 서비스를 제공합니다. 클러스터를 계속 관리해야 하는 Azure Kubernetes 클러스터와 달리 Azure Container Apps 인스턴스는 Kubernetes 클러스터를 설정하는 복잡성을 제거합니다.

1. Azure Portal에서 검색하여 선택합니다 `Container Apps`.

1. Container Apps**에서 **만들기**를 선택합니다**.

1. 다음 정보를 사용하여 기본** 사항 탭에서 **세부 정보를 입력한 다음, 다음: 컨테이너 >** 선택합니다**.

    | 설정 | 작업 |
    |---|---|
    | 구독 | Azure 구독 선택 |
    | Resource group | `az104-rg9` |
    | 컨테이너 앱 이름 |  `my-app` |
    | 지역    | **미국** 동부(또는 가까운 지역) |
    | Container Apps 환경 | 기본값 유지 |

1. **빠른 시작 이미지 사용을 사용하도록 설정하고 빠른 시작 이미지가** Simple hello world 컨테이너**로 **설정되어 있는지 확인합니다.

1. 페이지 아래쪽에서 **검토 및 만들기** 단추를 선택합니다. 

    >**참고**: 오류가 있는 경우 오류가 포함된 탭은 빨간색 점으로 표시됩니다.  해당 탭으로 이동합니다. 오류가 포함된 필드가 빨간색으로 강조 표시되어 있습니다.  모든 오류가 해결되면 **검토 및 만들기**를 다시 선택합니다.

1. **만들기**를 실행합니다.

    >**참고:** 배포가 진행 중*이라는 메시지가 *있는 페이지가 표시됩니다.  배포가 성공적으로 완료되면 *배포가 완료됨*이라는 메시지가 표시됩니다.
 
## 작업 4: 컨테이너 앱 배포 테스트 및 확인

기본적으로 만드는 Azure 컨테이너 앱은 샘플 헬로 월드 애플리케이션을 사용하여 포트 80의 트래픽을 허용합니다. Azure Container Apps는 애플리케이션에 대한 DNS 이름을 제공합니다. 이 URL을 복사하고 이동하여 애플리케이션이 실행 중인지 확인합니다.

1. **리소스로 이동**을 선택하여 새 컨테이너 앱을 봅니다.

1. *애플리케이션 URL* 옆에 있는 링크를 선택하여 애플리케이션을 봅니다.

    ![포털의 ACA 개요 페이지 스크린샷.](../media/az104-lab09b-aca-overview.png)

1. Azure Container Apps 앱이 **라이브** 메시지인지 확인합니다.

## 핵심 내용

랩을 완료한 것을 축하합니다. 다음은 이 랩에 대한 기본 설명입니다. 

+ ACI(Azure Container Instances)는 Microsoft Azure 퍼블릭 클라우드에 컨테이너를 배포할 수 있는 서비스입니다. ACI는 기본 인프라를 프로비전하거나 관리할 필요가 없습니다. 이 서비스는 Linux 컨테이너와 Windows 컨테이너를 모두 지원합니다.
+ ACA(Azure Container Apps)는 컨테이너화된 애플리케이션을 실행하는 동안 인프라를 기본 절감하고 비용을 절감할 수 있는 서버리스 플랫폼입니다. Container Apps는 서버 구성, 컨테이너 오케스트레이션 및 배포 세부 정보를 염려하는 대신 애플리케이션을 안정적이고 안전하게 유지하는 데 필요한 모든 최신 서버 리소스를 제공합니다.
+ ACI의 워크로드는 일반적으로 일종의 프로세스 또는 트리거에 의해 시작 및 중지되며 일반적으로 수명이 짧습니다. ACA의 워크로드는 일반적으로 웹앱과 같은 장기 실행 프로세스입니다.

## 리소스 정리

고유한 구독으로 작업하는 경우 랩 리소스를 삭제하는 데 1분이 소요됩니다. 이렇게 하면 리소스가 해제되고 비용이 최소화됩니다. 랩 리소스를 삭제하는 가장 쉬운 방법은 랩 리소스 그룹을 삭제하는 것입니다. 

+ Azure Portal에서 리소스 그룹을 선택하고, 리소스 그룹 삭제를 선택하고 **, **리소스 그룹** 이름을** 입력한 다음, 삭제**를 클릭합니다**.

+ Azure PowerShell 사용. `Remove-AzResourceGroup -Name resourceGroupName` 

+ CLI `az group delete --name resourceGroupName`를 사용하여 .
