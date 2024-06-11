---
lab:
  title: '랩 03: Azure Resource Manager 템플릿을 사용하여 Azure 리소스 관리'
  module: Administer Azure Resources
---

# 랩 03 - Azure Resource Manager 템플릿을 사용하여 Azure 리소스 관리

## 랩 소개

이 랩에서는 리소스 배포를 자동화하는 방법을 알아봅니다. Azure Resource Manager 템플릿 및 Bicep 템플릿에 대해 알아봅니다. 템플릿을 배포하는 다양한 방법에 대해 알아봅니다. 

이 랩을 수행하려면 Azure 구독이 필요합니다. 구독 유형은 이 랩의 기능 가용성에 영향을 미칠 수 있습니다. 지역을 변경할 수 있지만 단계는 **미국 동부**를 사용하여 작성됩니다. 

## 예상 소요 시간: 50분

## 대화형 랩 시뮬레이션

이 항목에 유용할 수 있는 대화형 랩 시뮬레이션이 있습니다. 시뮬레이션을 통해 고유의 속도에 맞춰 유사한 시나리오를 클릭할 수 있습니다. 대화형 시뮬레이션과 이 랩에는 차이점이 있지만 핵심 개념은 대부분 동일합니다. Azure 구독은 필요하지 않습니다. 

+ [Azure Resource Manager 템플릿을 사용하여 Azure 리소스를 관리합니다](https://mslabs.cloudguides.com/guides/AZ-104%20Exam%20Guide%20-%20Microsoft%20Azure%20Administrator%20Exercise%205). 템플릿을 사용하여 관리 디스크를 검토하고, 만들고, 배포합니다.
  
+ [템플릿을 사용하여 가상 머신을 만듭니다](https://mslearn.cloudguides.com/en-us/guides/AZ-900%20Exam%20Guide%20-%20Azure%20Fundamentals%20Exercise%209). QuickStart 템플릿을 사용하여 가상 머신을 배포합니다.
  
## 랩 시나리오

팀에서 리소스 배포를 자동화하고 간소화하는 방법을 찾으려고 합니다. 조직에서 관리 오버헤드와 사용자 오류를 줄이고 일관성을 높일 수 있는 방법을 찾고 있습니다.  

## 아키텍처 다이어그램

![작업 다이어그램.](../media/az104-lab03-architecture.png)

## 작업 기술

+ 작업 1: Azure Resource Manager 템플릿을 만듭니다.
+ 작업 2: Azure Resource Manager 템플릿을 편집하고 템플릿을 다시 배포합니다.
+ 작업 3: Cloud Shell을 구성하고 Azure PowerShell을 사용하여 템플릿을 배포합니다.
+ 작업 4: CLI를 사용하여 템플릿을 배포합니다. 
+ 작업 5: Azure Bicep을 사용하여 리소스를 배포합니다.

## 작업 1: Azure Resource Manager 템플릿 만들기

이 작업에서는 Azure Portal에서 관리 디스크를 만듭니다. 관리 디스크는 가상 머신과 함께 사용하도록 설계된 스토리지입니다. 디스크가 배포되면 다른 배포에 사용할 수 있는 템플릿을 내보냅니다.

1. **Azure Portal** - `https://portal.azure.com`에 로그인합니다.

1. `Disks`을 검색하고 선택합니다.

1. 디스크 페이지에서 **만들기**를 선택합니다.

1. **관리 디스크 만들기** 페이지에서 디스크를 구성한 다음 **확인**을 선택합니다. 
    
    | 설정 | 값 |
    | --- | --- |
    | 구독 | *구독* | 
    | 리소스 그룹 | `az104-rg3`(필요한 경우 **새로 만들기**를 선택합니다.)
    | 디스크 이름 | `az104-disk1` | 
    | 지역 | **미국 동부** |
    | 가용성 영역 | **인프라 중복 필요 없음** | 
    | 소스 형식 | **없음** |
    | 성능 | **표준 HDD**(크기 변경) |
    | 크기 | **32Gib** | 

    >**참고:** 템플릿을 사용해 실습할 수 있도록 간단한 관리 디스크를 만들고 있습니다. Azure 관리 디스크는 Azure에서 관리하는 블록 수준 스토리지 볼륨입니다.

1. **검토 + 만들기**를 클릭한 다음 **만들기**를 선택합니다.

1. 알림(오른쪽 상단)을 모니터링하고 배포 후 **리소스로 이동**을 선택합니다. 

1. **자동화** 블레이드에서 **템플릿 내보내기**를 선택합니다. 

1. **템플릿** 및 **매개 변수** 파일을 검토해 보세요.

1. **다운로드**를 클릭하고 템플릿을 로컬 드라이브에 저장합니다. 이렇게 하면 압축된 zip 파일이 만들어집니다. 

1. 파일 탐색기를 사용하여 다운로드한 파일의 콘텐츠를 컴퓨터의 **다운로드** 폴더에 추출합니다. 두 개의 JSON 파일(템플릿 및 매개 변수)이 있습니다. 

   >**유용한 정보**  전체 리소스 그룹을 내보낼 수도 있고 해당 리소스 그룹 내의 특정 리소스만 내보낼 수도 있습니다.

## 작업 2: Azure Resource Manager 템플릿을 편집한 후 템플릿을 다시 배포합니다.

이 작업에서는 다운로드한 템플릿을 사용하여 새 관리 디스크를 배포합니다. 이 작업에서는 배포를 빠르고 쉽게 반복하는 방법을 간략하게 설명합니다. 

1. Azure Portal에서 `Deploy a custom template`을 검색하여 선택합니다.

1. **사용자 지정 배포** 블레이드에는 **빠른 시작 템플릿**을 사용할 수 있는 기능이 있습니다. 드롭다운 메뉴에 표시된 것처럼 많은 기본 제공 템플릿이 있습니다. 

1. 빠른 시작을 사용하지 말고 **편집기에서 사용자 고유의 템플릿 만들기**를 선택합니다.

1. **템플릿 편집** 블레이드에서 **파일 로드**를 클릭하고 다운로드한 **template.json** 파일을 로컬 디스크에 업로드합니다.

1. 편집기 창에서 다음과 같이 변경합니다.

    + **disks_az104_disk1_name**을 `disk_name`으로 변경합니다(2개 위치 변경).
    + **az104-disk1**을 `az104-disk2`로 변경합니다(1개 위치 변경).

1. 이는 **표준** 디스크입니다. 위치는 **동부**입니다. 디스크 크기는 **32GB**입니다.

1. 변경 내용을 **저장**합니다.

1. 다음은 매개 변수 파일의 경우입니다. **매개 변수 편집**을 선택하고 **파일 로드**를 클릭한 후 **parameters.json**을 업로드합니다. 

1. 템플릿 파일과 일치하도록 변경합니다.

    **disks_az104_disk1_name**을 **disk_name**로 변경합니다(1개 위치 변경).

1. 변경 내용을 **저장**합니다. 

1. 사용자 지정 배포 설정을 완료합니다.

    | 설정 | 값 |
    | --- |--- |
    | 구독 | *구독* |
    | 리소스 그룹 | `az104-rg3` |
    | 지역 | **((미국) 미국 동부)** |
    | Disk_name | `az104-disk2` |

1. **검토 + 생성**를 선택한 다음, **생성**를 선택합니다.

1. **리소스로 이동**을 선택합니다. **az104-disk2**가 만들어졌는지 확인합니다.

1. **개요** 블레이드에서 리소스 그룹 **az104-rg3**을 선택합니다. 이제 두 개의 디스크가 있어야 합니다.
   
1. **설정** 섹션에서 **배포**를 클릭합니다.

    >**참고:** 모든 배포 세부 정보는 리소스 그룹에 문서화되어 있습니다. 대규모 작업에 템플릿을 사용하기 전에 성공을 보장하기 위해 처음 몇 가지 템플릿 기반 배포를 검토하는 것이 좋습니다.

1. 배포를 선택하고 **입력** 및 **템플릿** 블레이드의 콘텐츠를 검토합니다.

## 작업 3: Cloud Shell을 구성하고 Azure PowerShell을 사용하여 템플릿 배포

이 작업에서는 Azure Cloud Shell 및 Azure PowerShell을 사용하여 작업합니다. Azure Cloud Shell은 Azure 리소스를 관리하기 위해 브라우저에서 액세스할 수 있는 인증된 대화형 터미널입니다. Bash나 PowerShell 작업 방식에 가장 적합한 셸 환경을 유연하게 선택할 수 있습니다. 이 작업에서는 PowerShell을 사용하여 템플릿을 배포합니다. 

1. Azure Portal 오른쪽 상단에 있는 **Cloud Shell** 아이콘을 선택합니다. 또는 `https://shell.azure.com`으로 직접 이동할 수도 있습니다.

   ![Cloud Shell 아이콘의 스크린샷](../media/az104-lab03-cloudshell-icon.png)

1. **Bash** 또는 **PowerShell**을 선택하라는 메시지가 표시되면 **PowerShell**을 선택합니다. 

    >**유용한 정보**  주로 Linux 시스템을 사용하는 경우 Bash(CLI)에 더 익숙합니다. 주로 Windows 시스템을 사용하는 경우 Azure PowerShell에 더 익숙합니다. 

1. **시작** 화면에서 **스토리지 계정 탑재**와 **스토리지 계정을 만들고 싶음**을 차례로 선택합니다.  

    >**참고:** 이 랩의 경우 스토리지 계정이 필요합니다. 필요한 정보를 입력합니다. 
    
    | 설정 | 값 |
    |  -- | -- |
    | 구독 | *구독 선택* |
    | 리소스 그룹 | **az104-rg3** |
    | 지역 | *지역 선택* | 
    | 스토리지 계정(새로 만들기) | *전역적으로 고유해야 하고 길이는 3~24자여야 하며 숫자와 소문자만 사용해야 함* |
    | 파일 공유(새로 만들기) | `fs-cloudshell` |

1. 완료되면 **다음**을 선택합니다. 이 작업은 Cloud Shell을 처음 사용할 때만 수행하면 됩니다. 스토리지를 프로비전하는 데 몇 분 정도 걸립니다.

1. **파일 업로드/다운로드** 아이콘을 사용하여 다운로드 디렉터리에서 템플릿과 매개 변수 파일을 업로드합니다. 각 파일을 별도로 업로드해야 합니다.

   >**참고:** 언제든지 **클래식 클라우드 셸로 전환**하라는 메시지가 표시되면 이 작업을 수행합니다. 

1. Cloud Shell 스토리지에서 파일을 사용할 수 있는지 확인합니다. 

    ```powershell
    dir
    ```
    >**참고**: 필요한 경우 **cls**를 사용하여 명령 창을 지울 수 있습니다. 화살표 키를 사용하여 명령 기록을 이동할 수 있습니다.
   
1. **편집기**(중괄호) 아이콘을 선택하고 템플릿 JSON 파일로 이동합니다.

1. 변경합니다. 예를 들어, 디스크 이름을 **az104-disk3**으로 변경합니다. 변경 내용을 저장하려면 **Ctrl +S**를 사용합니다. 

    >**참고**: 템플릿 배포 대상을 리소스 그룹, 구독, 관리 그룹 또는 테넌트로 지정할 수 있습니다. 배포의 범위에 따라 다른 명령을 사용합니다.

1. 리소스 그룹에 배포하려면 **New-AzResourceGroupDeployment**를 사용합니다.

    ```powershell
    New-AzResourceGroupDeployment -ResourceGroupName az104-rg3 -TemplateFile template.json -TemplateParameterFile parameters.json
    ```
1. 명령이 완료되고 ProvisioningState가 **성공**인지 확인합니다.

1. 디스크가 만들어졌는지 확인합니다.

   ```powershell
   Get-AzDisk
   ```
   
## 작업 4: CLI를 사용하여 템플릿 배포 

1. 계속해서 **Cloud Shell**에서 **Bash**를 선택합니다. 선택 내용을 **확인**합니다.

1. Cloud Shell 스토리지에서 파일을 사용할 수 있는지 확인합니다. 이전 작업을 완료했다면 템플릿 파일을 사용할 수 있습니다. 

    ```sh
    ls
    ```

1. **편집기**(중괄호) 아이콘을 선택하고 템플릿 JSON 파일로 이동합니다.

1. 변경합니다. 예를 들어, 디스크 이름을 **az104-disk4**로 변경합니다. 변경 내용을 저장하려면 **Ctrl +S**를 사용합니다. 

    >**참고**: 템플릿 배포 대상을 리소스 그룹, 구독, 관리 그룹 또는 테넌트로 지정할 수 있습니다. 배포의 범위에 따라 다른 명령을 사용합니다.

1. 리소스 그룹에 배포하려면 **az deployment group create**를 사용합니다.

    ```sh
    az deployment group create --resource-group az104-rg3 --template-file template.json --parameters parameters.json
    ```
    
1. 명령이 완료되고 ProvisioningState가 **성공**인지 확인합니다.

1. 디스크가 만들어졌는지 확인합니다.

     ```sh
     az disk list --output table
     ```
   
## 작업 5: Azure Bicep을 사용하여 리소스 배포

이 작업에서는 Bicep 파일을 사용하여 관리 디스크를 배포합니다. Bicep은 ARM 템플릿을 기반으로 빌드된 선언적 자동화 도구입니다.

1. **Bash** 세션의 **Cloud Shell**에서 계속 작업합니다.

1. **\Allfiles\Lab03\azuredeploydisk.bicep** 파일을 찾아 다운로드합니다.

1. bicep 파일을 Cloud Shell에 **업로드**합니다. 

1. **편집기**(중괄호) 아이콘을 선택하고 파일을 탐색합니다.

1. bicep 템플릿 파일을 읽어 보세요. 디스크 리소스가 어떻게 정의되는지 확인합니다. 
   
1. 다음과 같이 변경합니다.

    + **managedDiskName** 값을 `Disk4`로 변경합니다.
    + **sku 이름** 값을 `StandardSSD_LRS`로 변경합니다.
    + **diskSizeinGiB** 값을 `32`로 변경합니다.

1. 변경 내용을 저장하려면 **Ctrl +S**를 사용합니다.

1. 이제 템플릿을 배포합니다.

    ```
    az deployment group create --resource-group az104-rg3 --template-file azuredeploydisk.bicep
    ```

1. 디스크가 만들어졌는지 확인합니다.

    ```sh
    az disk list --output table
    ```

    >**참고:** 각각 다른 방식으로 5개의 관리 디스크를 성공적으로 배포했습니다. 잘하셨습니다!

## 리소스 정리

**고유의 구독**으로 작업하는 경우 랩 리소스를 삭제해 보세요. 이렇게 하면 리소스가 확보되고 비용이 최소화됩니다. 랩 리소스를 삭제하려면 랩 리소스 그룹을 삭제하는 것이 가장 쉽습니다. 

+ Azure Portal에서 리소스 그룹을 선택하고 **리소스 그룹 삭제**, **리소스 그룹 이름 입력**을 선택한 다음 **삭제**를 클릭합니다.
+ Azure PowerShell 사용, `Remove-AzResourceGroup -Name resourceGroupName`.
+ CLI 사용, `az group delete --name resourceGroupName`.

## Copilot을 사용하여 학습 확장

Copilot은 Azure 스크립팅 도구를 사용하는 방법을 익히는 데 도움을 줍니다. 또한 Copilot은 랩에서 다루지 않는 영역이나 추가 정보가 필요한 영역을 지원할 수 있습니다. Edge 브라우저를 열고 Copilot(오른쪽 위)을 선택하거나 *copilot.microsoft.com*으로 이동하세요. 몇 분 정도 시간을 내어 이러한 프롬프트를 사용해 보세요.

+ Azure Resource Manager 템플릿 파일의 형식은 무엇인가요? 예를 들어, 각 구성 요소를 설명합니다. 
+ 기존 Azure Resource Manager 템플릿을 어떻게 사용하나요?
+ Azure Resource Manager 템플릿과 Azure Bicep 템플릿을 비교하고 대조해 보세요. 


## 자기 주도적 학습을 통해 자세히 알아보기

+ [JSON ARM 템플릿을 사용하여 Azure 인프라를 배포합니다](https://learn.microsoft.com/training/modules/create-azure-resource-manager-template-vs-code/). Visual Studio Code를 사용하여 일관되게 안정적으로 인프라를 Azure에 배포하는 ARM(Azure Resource Manager) 템플릿을 작성합니다.
+ [Azure Cloud Shell의 기능 및 도구를 검토합니다](https://learn.microsoft.com/training/modules/review-features-tools-for-azure-cloud-shell/). Cloud Shell 기능 및 도구 
+ [Windows PowerShell을 사용하여 Azure 리소스를 관리합니다](https://learn.microsoft.com/training/modules/manage-azure-resources-windows-powershell/). 이 모듈에서는 클라우드 서비스 관리에 필요한 모듈을 설치하고 PowerShell 명령을 사용하여 Azure 가상 머신, Azure 구독 및 Azure Storage 계정과 같은 클라우드 리소스에서 간단한 관리 작업을 수행하는 방법을 설명합니다.
+ [Bash를 소개합니다](https://learn.microsoft.com/training/modules/bash-introduction/). Bash를 사용하여 IT 인프라를 관리합니다.
+ [첫 번째 Bicep 템플릿 빌드](https://learn.microsoft.com/training/modules/build-first-bicep-template/). Bicep 템플릿 내에서 Azure 리소스를 정의합니다. 배포의 일관성과 안정성을 개선하고 필요한 수동 작업을 줄이며 환경 간에 배포를 확장합니다. 템플릿은 매개 변수, 변수, 식 및 모듈을 사용하여 유연하고 재사용이 가능합니다.

## 핵심 내용

축하합니다. 랩을 완료했습니다. 이 랩의 주요 내용은 다음과 같습니다. 

+ Azure Resource Manager 템플릿을 사용하면 솔루션의 모든 리소스를 개별적으로 처리하는 대신 그룹으로 배포, 관리 및 모니터링할 수 있습니다.
+ Azure Resource Manager 템플릿은 스크립트가 아닌 선언적으로 인프라를 관리할 수 있는 JSON(JavaScript Object Notation) 파일입니다.
+ 템플릿에서 매개 변수를 인라인 값으로 전달하는 대신 매개 변수 값이 포함된 별도의 JSON 파일을 사용할 수 있습니다.
+ Azure Resource Manager 템플릿은 Azure Portal, Azure PowerShell 및 CLI를 비롯한 다양한 방법으로 배포할 수 있습니다.
+ Bicep은 Azure Resource Manager 템플릿의 대안입니다. Bicep은 선언적 구문을 사용하여 Azure 리소스를 배포합니다.
+ Bicep는 간결한 구문, 신뢰할 수 있는 형식 안전성 및 코드 다시 사용에 대한 지원을 제공합니다. Bicep은 Azure에서 코드형 인프라 솔루션에 대한 최고의 제작 환경을 제공합니다.


