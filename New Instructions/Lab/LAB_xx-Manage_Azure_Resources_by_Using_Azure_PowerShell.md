---
lab:
  title: '랩 03c: Azure PowerShell을 사용하여 Azure 리소스 관리(선택 사항)'
  module: Administer Azure Resources
---

# 랩 03c - Azure PowerShell을 사용하여 Azure 리소스 관리
# 학생용 랩 매뉴얼

## 랩 시나리오

사용자와 팀은 리소스를 프로비전하고 리소스 그룹을 기반으로 구성하는 등 Azure Portal의 기본 Azure 관리 기능을 살펴보했습니다. 또한 Azure Resource Manager 템플릿을 살펴보기도 했습니다. 다음으로, Azure PowerShell을 사용하여 동등한 작업을 시도하려고 합니다. 이 랩에서는 Azure Cloud Shell에서 사용할 수 있는 PowerShell 환경을 활용합니다.

**참고:** **[대화형 랩 시뮬레이션](https://mslabs.cloudguides.com/guides/AZ-104%20Exam%20Guide%20-%20Microsoft%20Azure%20Administrator%20Exercise%206)** 을 사용하여 이 랩을 원하는 속도로 클릭할 수 있습니다. 대화형 시뮬레이션과 호스트된 랩 간에 약간의 차이가 있을 수 있지만 보여주는 핵심 개념과 아이디어는 동일합니다. 

## 목표

이 랩에서는 다음을 수행합니다.

+ 작업 1: Azure Cloud Shell에서 PowerShell 세션 시작하기
+ 작업 2: Azure PowerShell을 사용하여 리소스 그룹 및 Azure 관리 디스크 만들기
+ 작업 3: Azure PowerShell을 사용하여 관리 디스크 구성

## 예상 소요 시간: 20분

## 아키텍처 다이어그램

![아키텍처 다이어그램.](../media/az104-lab03c-architecture-diagram.png)

### 지침

## 연습 1

## 작업 1: Azure Cloud Shell에서 PowerShell 세션 시작하기

이 작업에서는 Cloud Shell에서 PowerShell 세션을 엽니다. Cloud Shell은 Azure Portal에 기본 제공되므로 아무 것도 설치할 필요 없이 포털에서 직접 PowerShell 또는 Azure CLI 명령을 실행할 수 있습니다. 스토리지 계정은 명령 기록을 유지하고 스크립트를 저장하기 위한 위치를 제공합니다.

1. 포털에서 Azure Portal 오른쪽 상단에 있는 아이콘을 클릭하여 **Azure Cloud Shell**을 엽니다. 또는 .`https://shell.azure.com`

1. **Bash**와 **PowerShell** 중에서 선택하라는 메시지가 표시되면 **PowerShell**을 선택합니다. 

    >**참고**: **Cloud Shell**을 처음 시작했는데 **탑재된 스토리지 없음**이라는 메시지가 표시되면 이 랩에서 사용하는 구독을 선택하고 **스토리지 만들기**를 클릭합니다. 

1. 메시지가 표시되면 **스토리지 만들기**를 클릭하고 Azure Cloud Shell 창이 표시될 때까지 기다립니다. 

1. Cloud Shell 창의 왼쪽 상단 모서리에 있는 드롭다운 메뉴에 **PowerShell**이 나타나는지 확인합니다.

## 작업 2: Azure PowerShell을 사용하여 리소스 그룹 및 Azure 관리 디스크 만들기

이 작업에서는 Cloud Shell 내에서 Azure PowerShell 세션을 사용하여 리소스 그룹 및 Azure 관리 디스크를 만듭니다. 이 작업은 Cloud Shell 및 Azure PowerShell을 사용하여 일반적인 작업을 스크립싱하는 방법을 보여 줍니다. 그런 다음 Azure Automation, Logic Apps 또는 기타 자동화 도구를 사용하여 스크립트를 트리거할 수 있습니다.

1. PowerShell은 cmdlet에 *동사**-명사* 형식을 사용합니다. 예를 들어 새 리소스 그룹을 만드는 cmdlet은 New-AzResourceGroup입니다****. cmdlet을 사용하는 방법을 보려면 다음 명령을 실행합니다.

   ```powershell
   Get-Help New-AzResourceGroup
   ```


1. Cloud Shell 내의 PowerShell 세션에서 리소스 그룹을 만들려면 다음 명령을 실행합니다. 달러 기호($)로 시작하는 명령은 이후 명령에서 사용할 수 있는 변수를 만듭니다.

   ```powershell
   $location = 'eastus'

   $rgName = 'az104-rg1'

   New-AzResourceGroup -Name $rgName -Location $location
   ```
   >**참고**: az104-rg1**이 이미 있는 경우 **$rgName** 매개 변수에 **다른 이름을 사용합니다. 

   ![리소스 그룹 만들기의 스크린샷 ](../media/az104-lab03c-createrg.png)

1. 새로 만든 리소스 그룹의 속성을 검색하려면 다음 명령을 실행합니다.

   ```powershell
   Get-AzResourceGroup -Name $rgName
   ```

1. 새 리소스 그룹을 만드는 것과 마찬가지로 새 디스크를 만들려면 New-AzDisk** cmdlet을 **사용합니다. cmdlet을 사용하는 방법을 보려면 다음 명령을 실행합니다.

   ```powershell
   Get-Help New-AzDisk
   ```

1. az104-disk1**이라는 **새 관리 디스크를 만들려면 다음 명령을 실행합니다.

   ```powershell
   $diskConfig = New-AzDiskConfig `
    -Location $location `
    -CreateOption Empty `
    -DiskSizeGB 32 `
    -SkuName Standard_LRS

   $diskName = 'az104-disk1'

   New-AzDisk `
    -ResourceGroupName $rgName `
    -DiskName $diskName `
    -Disk $diskConfig
   ```

   ![디스크 만들기 스크린샷 ](../media/az104-lab03c-createdisk.png)

1. 새로 만든 디스크의 속성을 검색하려면 다음 명령을 실행합니다.

   ```powershell
   Get-AzDisk -ResourceGroupName $rgName -Name $diskName
   ```

## 작업 3: Azure PowerShell을 사용하여 관리 디스크 구성

이 작업에서는 Cloud Shell 내에서 Azure PowerShell 세션을 사용하여 Azure 관리 디스크를 구성합니다. 이 작업은 Cloud Shell 및 Azure PowerShell을 사용하여 일반적인 작업을 스크립싱하는 방법을 보여 줍니다.

>**알고 계셨나요?**  Azure Automation, Logic Apps 또는 기타 자동화 도구를 사용하여 스크립트를 실행할 수도 있습니다.

1. Cloud Shell 내의 PowerShell 세션에서 Azure 관리 디스크의 크기를 **64 GB**로 늘리려면 다음 명령을 실행합니다.

   ```powershell
   New-AzDiskUpdateConfig -DiskSizeGB 64 | Update-AzDisk -ResourceGroupName $rgName -DiskName $diskName
   ```

1. 변경 내용이 적용되었는지 확인하려면 다음 명령을 실행합니다.

   ```powershell
   Get-AzDisk -ResourceGroupName $rgName -Name $diskName
   ```

1. 현재 SKU **를 Standard_LRS** 확인하려면 다음 명령을 실행합니다.

   ```powershell
   (Get-AzDisk -ResourceGroupName $rgName -Name $diskName).Sku
   ```

   ![업데이트 sku의 스크린샷.](../media/az104-lab03c-updatesku.png)

1. 디스크 성능 SKU를 **Premium_LRS** 변경하려면 Cloud Shell 내의 PowerShell 세션에서 다음 명령을 실행합니다.

   ```powershell
   New-AzDiskUpdateConfig -SkuName Premium_LRS | Update-AzDisk -ResourceGroupName $rgName -DiskName $diskName
   ```

1. 변경 내용이 적용되었는지 확인하려면 다음 명령을 실행합니다.

   ```powershell
   (Get-AzDisk -ResourceGroupName $rgName -Name $diskName).Sku
   ```

   ![업데이트 sku 최종 스크린샷](../media/az104-lab03c-updatesku2.png)

>**눈치채셨나요?** PowerShell cmdlet은 Get **, **New** 및 Update**와 **같은 **일반적인 동사를 사용합니다. Get**부터 **시작하는 Cmdlet은 일반적으로 구성에 대한 정보를 검색합니다. New**로 **시작하는 Cmdlet은 일반적으로 새 리소스를 만듭니다. 업데이트**로 시작하는 **Cmdlet은 일반적으로 기존 리소스를 구성합니다.

## 검토

축하합니다! Azure Cloud Shell 세션을 성공적으로 시작하고, PowerShell을 사용하여 리소스 그룹을 만들고, PowerShell을 사용하여 관리 디스크를 만들고, PowerShell을 사용하여 관리 디스크를 구성했습니다.
