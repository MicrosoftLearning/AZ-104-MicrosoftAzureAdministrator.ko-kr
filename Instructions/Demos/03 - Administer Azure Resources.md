---
demo:
  title: '데모 03: Azure 리소스 관리'
  module: Administer Administer Azure Resources
---
# 03 - Azure 리소스 관리

## 데모 -- Azure Portal

이 데모에서는 Azure Portal 살펴보겠습니다.

**참조**: [Azure Portal 설정 및 기본 설정 관리](https://docs.microsoft.com/azure/azure-portal/set-preferences)

**참조**: [Azure Portal dashboard 만들기](https://docs.microsoft.com/azure/azure-portal/azure-portal-dashboards)

**참조**: [Azure 지원 요청을 만드는 방법](https://docs.microsoft.com/azure/azure-portal/supportability/how-to-create-azure-support-request)

1. Azure Portal에 액세스합니다.

1. 위쪽 배너에서 **지원 & 문제 해결 아이콘을** 선택합니다. **지원 리소스** 링크를 검토합니다. 

1. 상단 배너에서 **설정**아이콘을 선택합니다. **모양 + 시작 보기** 설정을 검토합니다. 

1. 왼쪽 메뉴를 사용하고 **대시보드**를 선택합니다. **타일 갤러리**를 사용하여 dashboard **편집**합니다. 사용자 지정 옵션에 대해 설명합니다.

1. 리소스를 검색하고 찾는 방법을 보여 줍니다.

1. 왼쪽 위 메뉴를 사용하여 **모든 서비스를 찾습니다**. 

1. 시간이 지남에 따라 다른 기능을 검토합니다.
   
1. 학생들에게 질문이 있는지 묻습니다.

## 데모 -- Cloud Shell

이 데모에서는 Cloud Shell을 실험해 보겠습니다.

**참조**: [Azure Cloud Shell 대한 빠른 시작](https://learn.microsoft.com/en-us/azure/cloud-shell/quickstart?tabs=azurecli)

**Cloud Shell 구성**

1.   **Azure Portal**에 액세스합니다.

1.  위쪽 배너에서  **Cloud Shell**  아이콘을 클릭합니다.

1.  셸 시작 페이지에서 Bash 또는 PowerShell 선택을 확인합니다.  **PowerShell을** 선택합니다.

1.  Azure Cloud Shell 파일을 유지하기 위해 Azure 파일 공유가 필요한 방법을 설명합니다. 필요한 경우 스토리지 공유를 구성합니다. 

**Azure PowerShell 및 Bash 실험**

1. **PowerShell** 셸이 선택되어 있는지 확인하고 몇 가지 명령을 시도합니다. 예를 들어 **Get-AzSubscription** 및 **Get-AzResourceGroup**입니다.

1. 자동 완성의 작동 방식을 보여 줍니다. 화면을 지우는 방법을 보여 **줍니다. cls.** 

1. **Bash** 셸이 선택되어 있는지 확인하고 몇 가지 명령을 시도합니다. 예를 들어 **az account list** 및 **az resource list**입니다.

1. 학생들에게 PowerShell 또는 Bash 명령 사용에 대한 질문이 있는지 묻습니다. 

**Cloud Shell 편집기를 사용하여 실험(선택 사항)**

1. 클라우드 편집기를 사용하려면 **중괄호 아이콘을** 선택합니다.

1. 왼쪽 탐색 창에서 파일을 선택합니다. 예:  **.profile**.

1. 편집기 상단 배너, 설정 선택(텍스트 크기 및 글꼴) 및 파일 업로드/다운로드를 확인합니다.

1. **저장**, **편집기 닫기** 및 **파일 열기**의 맨 오른쪽에 있는 줄임표(**\...**)를 확인합니다.

1. 시간이 있는 동안 실험한 다음 클라우드 편집기를 **닫습니다** .

1. Cloud Shell 창을 닫습니다.

## 데모 -- 빠른 시작 템플릿

이 데모에서는 빠른 시작 템플릿을 살펴봅니다.

**참조**: [자습서 - & 배포 템플릿 만들기 - Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/template-tutorial-create-first-template?tabs=azure-powershell)

1.  [Azure 빠른 시작 템플릿 갤러리](https://learn.microsoft.com/en-us/samples/browse/?expanded=azure&products=azure-resource-manager)로 이동하여 시작합니다. JSON 및 Bicep 예제가 있습니다. 

1. 학생들에게 관심 있는 특정 템플릿이 있는지 물어봅니다. 그렇지 않은 경우 템플릿을 선택합니다. 예를 들어 [태그가 있는 간단한 Windows VM 배포 템플릿입니다](https://learn.microsoft.com/en-us/samples/azure/azure-quickstart-templates/vm-tags/) .

1. Azure  **에 배포**단추를 사용하여 Azure Portal 통해 템플릿을 직접 배포하는 방법을 설명합니다.

1. JSON 템플릿을 **배포**하고 템플릿 및 매개 변수 파일을 편집하는 방법을 설명합니다. 파일의 용도를 검토합니다. 시간이 지남에 따라 구문을 검토합니다. 

1. 코드 샘플 갤러리로 돌아가서 Bicep 템플릿을 찾습니다. 예를 들어 [표준 스토리지 계정 만들기를 선택합니다](https://learn.microsoft.com/en-us/samples/azure/azure-quickstart-templates/storage-account-create/). 

1. Bicep 템플릿을 **배포**하고 템플릿 및 매개 변수 파일을 편집하는 방법을 설명합니다. 시간이 지남에 따라 구문을 검토합니다. 
