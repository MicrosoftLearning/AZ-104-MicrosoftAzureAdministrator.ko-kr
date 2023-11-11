---
demo:
  title: '데모 09: 관리aS 컴퓨팅 옵션 등록'
  module: Administer PaaS Compute Options
---

# 09 - 관리aS 컴퓨팅 옵션 등록

## Azure App Service 계획 구성

이 데모에서는 Azure 앱 Service 계획을 만들고 작업합니다.

**참조**: [App Service 계획 관리 - Azure 앱 Service](https://docs.microsoft.com/azure/app-service/app-service-plan-manage)

**참조**: [Azure 앱 Service에서 앱 강화](https://learn.microsoft.com/azure/app-service/manage-scale-up)

**참조**: [Azure 앱 Service에서 자동 크기 조정](https://learn.microsoft.com/azure/app-service/manage-automatic-scaling?tabs=azure-portal)

1. Azure Portal 사용 

1. App Service 계획을 ** 검색하고 선택합니다**.

1. 간단한 App Service 계획을 만듭니다. Windows 또는 Linux를 선택해야 하는 필요성에 대해 설명합니다. 지금 또는 다음 단계에서 가격 책정 계획을 논의합니다. 

1. 새 App Service 계획을 배포합니다. 

1. **강화(App Service 계획)** 블레이드를 검토합니다. 개발/테스트** 계획과 **프로덕션** 계획의 차이점**에 대해 설명합니다. 기능 목록을 검토합니다. 

1. **규모 확장(App Service 계획)** 블레이드를 검토합니다. 수동** 및 **규칙 기반**의 **차이점을 검토합니다. 

## Azure App Services 구성

이 데모에서는 Docker 컨테이너를 실행하는 새 웹앱을 만듭니다. 컨테이너에 시작 메시지가 표시됩니다.

**참조**: [웹앱 만들기](https://learn.microsoft.com/training/modules/host-a-web-app-with-azure-app-service/3-exercise-create-a-web-app-in-the-azure-portal?pivots=csharp)

이 작업에서는 Azure 앱 Service Web App을 만듭니다.

1. Azure Portal 사용 

1. App Services **를 검색하고 선택합니다**.

1. ****웹앱을 만듭니**다**.

    - 게시: **코드**. 다른 선택 항목을 검토합니다.
    - 런타임 스택: **.Net**. 다른 선택 항목을 검토합니다.
    - 운영 체제: **Linux**

1. **무료 F1** 서비스 계획을 선택합니다.

1. **검토 + 웹앱 만들기** 리소스가 배포될 때까지 기다립니다.

1. **개요** 페이지에서 상태가** 실행 중**인지 **확인**합니다.

1. URL**을 **선택하고 기본 자리 표시자 페이지가 로드되는지 확인합니다.

1. 시간이 지남에 따라 배포 슬롯 옵션을 탐색 **합니다** .
   
## Azure Container Instances 구성

이 데모에서는 Azure Portal에서 ACI(Azure Container Instances)를 사용하여 컨테이너를 만들고 구성하고 배포합니다. ACI 애플리케이션은 공용 Microsoft 헬로 월드 이미지가 있는 정적 HTML 페이지를 표시합니다. 

**참조**: [빠른 시작 - 컨테이너 인스턴스에 Docker 컨테이너 배포](https://learn.microsoft.com/en-us/azure/container-instances/container-instances-quickstart-portal)

1. Azure Portal 사용

1. 컨테이너 인스턴스 **를 검색하고 선택합니다**.

1. **새 컨테이너 인스턴스를 만듭니** 다. 

1. **리소스 그룹** 및 **컨테이너 이름을** 입력합니다. 

1. 이미지 원본** 옵션에 대해 **설명합니다. 빠른 시작 이미지를** 사용합니다**.

1. 컨테이너 이미지의 경우 **mcr.microsoft.com/azuredocs/aci-helloworld:latest(Linux)**를 사용합니다**.** 이 샘플 Linux 이미지는 고정 HTML 페이지를 제공하는 Node.js로 작성된 작은 웹앱을 패키지합니다.

1. **네트워킹** 페이지에서 컨테이너의 **DNS 이름 레이블**을 지정합니다. 

1. 다른 모든 설정은 기본값으로 두고 **검토 + 만들기**를 선택합니다.

1. 리소스가 배포될 때까지 기다립니다.

1. 리소스에 **대한 개요** 페이지에서 상태가** 실행 중**인지 **확인**합니다.

1. 컨테이너 인스턴스에 **대한 FQDN** 으로 이동하여 시작 페이지가 표시되는지 확인합니다. 

**참고**: 추가 비용을 방지하려면 리소스를 삭제합니다. 

## Azure Container Apps 구성

이 데모에서는 Azure Container Apps를 만들고 사용합니다. 

**참조**: [빠른 시작: Azure Portal을 사용하여 첫 번째 컨테이너 앱 배포](https://learn.microsoft.com/azure/container-apps/quickstart-portal)

1. Container Apps**를 검색하여 선택합니다**.

1. **프로젝트 세부 정보를** 완료하고 컨테이너 앱 **환경을 만듭니다**.

1. **컨테이너 앱을 검토하고 만듭니** 다.

1. **애플리케이션 URL** 링크를 사용하여 애플리케이션을 봅니다.

1. 브라우저에 Azure Container Apps** 시작 메시지가 표시되는**지 확인합니다. 






