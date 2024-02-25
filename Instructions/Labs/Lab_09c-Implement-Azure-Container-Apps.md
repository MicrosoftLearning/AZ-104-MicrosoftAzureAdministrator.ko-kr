---
lab:
  title: '랩 09c: Azure Container Apps 구현'
  module: Administer PaaS Compute Options
---

# 랩 09c - Azure Container Apps 구현

## 랩 소개

이 랩에서는 Azure Container Apps를 구현하고 배포하는 방법을 알아봅니다.

이 랩에는 Azure 구독이 필요합니다. 구독 유형은 이 랩의 기능 가용성에 영향을 줄 수 있습니다. 지역을 변경할 수 있지만 단계는 미국** 동부를 사용하여 **작성됩니다.

## 예상 소요 시간: 15분

## 랩 시나리오

조직에는 온-프레미스 데이터 센터의 가상 머신에서 실행되는 웹 애플리케이션이 있습니다. 조직은 모든 애플리케이션을 클라우드로 이동하려고 하지만 관리할 서버가 많이 없도록 하고 싶지는 않습니다. Azure Container Apps를 평가하기로 결정합니다.

## 대화형 랩 시뮬레이션

이 항목에 대한 대화형 랩 시뮬레이션은 없습니다. 

## 작업 기술

- 작업 1: Azure Container App 및 환경을 만들고 구성합니다.
- 작업 2: Azure Container App의 배포를 테스트하고 확인합니다.

## 아키텍처 다이어그램

![작업의 다이어그램.](../media/az104-lab09b-aca-architecture.png)

## 작업 1: Azure Container App 및 환경 만들기 및 구성

Azure Container Apps는 관리되는 Kubernetes 클러스터의 개념을 한 단계 더 발전시키고 클러스터 환경을 관리하고 클러스터 위에 다른 관리형 서비스를 제공합니다. 클러스터를 계속 관리해야 하는 Azure Kubernetes 클러스터와 달리 Azure Container Apps 인스턴스는 Kubernetes 클러스터를 설정하는 복잡성을 제거합니다.

1. Azure Portal에서 검색하여 선택합니다 `Container Apps`.

1. Container Apps**에서 **만들기**를 선택합니다**.

1. 다음 정보를 사용하여 기본 사항 탭의 **세부 정보를 입력합니다** .*.

    | 설정 | 작업 |
    |---|---|
    | 구독 | Azure 구독 선택 |
    | Resource group | `az104-rg9` |
    | 컨테이너 앱 이름 |  `my-app` |
    | 지역    | **미국** 동부(또는 가까운 지역) |
    | Container Apps 환경 | 기본값 유지 |

1. 컨테이너 탭에서 **빠른 시작 이미지 사용을 사용하도록 설정하고 빠른 시작 이미지가** Simple hello world 컨테이너**로 **설정되어 있는지 확인**합니다.**

1. 검토를 선택하고 만든** 다음 **만들기를 **선택합니다**.

    >**참고:** 컨테이너 앱이 배포되기를 기다립니다. 이 작업에 몇 분 정도가 소요됩니다. 
 
## 작업 2: Azure Container App 배포 테스트 및 확인

기본적으로 만드는 Azure 컨테이너 앱은 샘플 헬로 월드 애플리케이션을 사용하여 포트 80의 트래픽을 허용합니다. Azure Container Apps는 애플리케이션에 대한 DNS 이름을 제공합니다. 이 URL을 복사하고 이동하여 애플리케이션이 실행 중인지 확인합니다.

1. **리소스로 이동**을 선택하여 새 컨테이너 앱을 봅니다.

1. *애플리케이션 URL* 옆에 있는 링크를 선택하여 애플리케이션을 봅니다.

    ![포털의 ACA 개요 페이지 스크린샷.](../media/az104-lab09b-aca-overview.png)

1. Azure Container Apps 앱이 **라이브** 메시지인지 확인합니다.
   
## 리소스 정리

고유한 구독**으로 **작업하는 경우 랩 리소스를 삭제하는 데 1분이 소요됩니다. 이렇게 하면 리소스가 해제되고 비용이 최소화됩니다. 랩 리소스를 삭제하는 가장 쉬운 방법은 랩 리소스 그룹을 삭제하는 것입니다. 

+ Azure Portal에서 리소스 그룹을 선택하고, 리소스 그룹 삭제를 선택하고 **, **리소스 그룹** 이름을** 입력한 다음, 삭제**를 클릭합니다**.
+ Azure PowerShell 사용. `Remove-AzResourceGroup -Name resourceGroupName` 
+ CLI `az group delete --name resourceGroupName`를 사용하여 .



## 핵심 내용

랩을 완료한 것을 축하합니다. 다음은 이 랩에 대한 기본 설명입니다. 

+ ACA(Azure Container Apps)는 컨테이너화된 애플리케이션을 실행하는 동안 인프라를 기본 절감하고 비용을 절감할 수 있는 서버리스 플랫폼입니다.
+ Container Apps는 서버 구성, 컨테이너 오케스트레이션 및 배포 세부 정보를 제공합니다. 
+ ACA의 워크로드는 일반적으로 웹앱과 같은 장기 실행 프로세스입니다.

## 자기 주도적 학습을 통해 자세히 알아보기

+ [Azure Container Apps에서 컨테이너 앱을 구성합니다](https://learn.microsoft.com/training/modules/configure-container-app-azure-container-apps/). Azure Container Apps의 기능과 기능을 검사한 다음, Azure Container Apps를 사용하여 컨테이너 앱을 만들고, 구성하고, 크기를 조정하고, 관리하는 방법에 중점을 둡니다.
     
