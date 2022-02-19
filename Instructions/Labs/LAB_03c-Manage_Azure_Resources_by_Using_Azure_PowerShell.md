---
lab:
    title: '03c - Azure PowerShell을 사용하여 Azure 리소스 관리'
    module: '모듈 03 - Azure 관리'
---

# 랩 03c - Azure PowerShell을 사용하여 Azure 리소스 관리
# 학생 랩 매뉴얼

## 랩 시나리오

이제 Azure Portal 및 Azure Resource Manager 템플릿을 사용하여 리소스 프로비전 및 리소스 그룹에 기반한 리소스 구성과 관련된 기본 Azure 관리 기능을 살펴보았으므로 Azure PowerShell을 사용하여 동등한 작업을 수행해야 합니다. Azure PowerShell 모듈을 설치하지 않으려면 Azure Cloud Shell에서 사용할 수 있는 PowerShell 환경을 활용합니다.

## 목표

이 랩에서는 다음 작업을 수행합니다.

+ 작업 1: Azure Cloud Shell에서 PowerShell 세션 시작하기
+ 작업 2: Azure PowerShell을 사용하여 리소스 그룹 및 Azure 관리 디스크 만들기
+ 작업 3: Azure PowerShell을 사용하여 관리 디스크 구성

## 예상 시간: 20분

## 아키텍처 다이어그램

![이미지](../media/lab03c.png)

## 지침

### 연습 1:

#### 작업 1: Azure Cloud Shell에서 PowerShell 세션 시작하기

이 작업에서는 Cloud Shell에서 PowerShell 세션을 엽니다. 

1. 포털에서 Azure Portal 오른쪽 상단에 있는 아이콘을 클릭하여 **Azure Cloud Shell**을 엽니다.

1. **Bash** 또는 **PowerShell**을 선택하라는 메시지가 표시되면 **PowerShell**을 선택합니다. 

    >**참고**: 처음으로 **Cloud Shell**을 시작하고 **탑재된 스토리지가 없음** 메시지가 표시되면, 이 랩에서 사용하는 구독을 선택하고 **스토리지 만들기**를 클릭합니다. 

1. 메시지가 표시되면 **스토리지 만들기**를 클릭하고 Azure Cloud Shell 창이 표시될 때까지 기다립니다. 

1. Cloud Shell 창의 왼쪽 상단 모서리에 있는 드롭다운 메뉴에 **PowerShell**이 나타나는지 확인합니다.

#### 작업 2: Azure PowerShell을 사용하여 리소스 그룹 및 Azure 관리 디스크 만들기

이 작업에서는 Cloud Shell 내에 있는 Azure PowerShell 세션을 사용하여 리소스 그룹 및 Azure 관리 디스크를 만듭니다.

1. Cloud Shell 내의 PowerShell 세션에서 이전 랩에서 만든 **az104-03b-rg1** 리소스 그룹과 동일한 Azure 지역에 있는 리소스 그룹을 만들려면 다음 명령을 실행합니다.

   ```powershell
   $location = (Get-AzResourceGroup -Name az104-03b-rg1).Location

   $rgName = 'az104-03c-rg1'

   New-AzResourceGroup -Name $rgName -Location $location
   ```
1. 새로 만든 리소스 그룹의 속성을 검색하려면 다음 명령을 실행합니다.

   ```powershell
   Get-AzResourceGroup -Name $rgName
   ```
1. 본 모듈의 이전 랩에서 만든 것과 동일한 특성을 가진 새 관리 디스크를 만들려면 다음 명령을 실행합니다.

   ```powershell
   $diskConfig = New-AzDiskConfig `
    -Location $location `
    -CreateOption Empty `
    -DiskSizeGB 32 `
    -Sku Standard_LRS

   $diskName = 'az104-03c-disk1'

   New-AzDisk `
    -ResourceGroupName $rgName `
    -DiskName $diskName `
    -Disk $diskConfig
   ```

1. 새로 만든 디스크의 속성을 검색하려면 다음 명령을 실행합니다.

   ```powershell
   Get-AzDisk -ResourceGroupName $rgName -Name $diskName
   ```

#### 작업 3: Azure PowerShell을 사용하여 관리 디스크 구성

이 작업에서는 Cloud Shell 내에서 Azure PowerShell 세션을 사용하여 Azure 관리 디스크의 구성을 관리합니다. 

1. Cloud Shell 내의 PowerShell 세션에서 Azure 관리 디스크의 크기를 **64 GB**로 늘리려면 다음 명령을 실행합니다.

   ```powershell
   New-AzDiskUpdateConfig -DiskSizeGB 64 | Update-AzDisk -ResourceGroupName $rgName -DiskName $diskName
   ```

1. 변경이 적용되었는지 확인하려면 다음 명령을 실행합니다.

   ```powershell
   Get-AzDisk -ResourceGroupName $rgName -Name $diskName
   ```

1. 현재 SKU(**Standard_LRS**)를 확인하려면 다음 명령을 실행합니다.

   ```powershell
   (Get-AzDisk -ResourceGroupName $rgName -Name $diskName).Sku
   ```

1. Cloud Shell 내의 PowerShell 세션에서 디스크 성능 SKU를 **Premium_LRS** 로 변경하려면 다음 명령을 실행합니다.

   ```powershell
   New-AzDiskUpdateConfig -Sku Premium_LRS | Update-AzDisk -ResourceGroupName $rgName -DiskName $diskName
   ```

1. 변경이 적용되었는지 확인하려면 다음 명령을 실행합니다.

   ```powershell
   (Get-AzDisk -ResourceGroupName $rgName -Name $diskName).Sku
   ```

#### 리소스 정리

   >**참고**: 이 랩에서 배포한 리소스는 삭제하지 마세요. 이 모듈의 다음 랩에서 참조해야 합니다.

#### 복습

이 랩에서는 다음을 수행했습니다.

- Azure Cloud Shell에서 PowerShell 세션을 시작하기
- Azure PowerShell을 사용하여 리소스 그룹 및 Azure 관리 디스크 만들기
- Azure PowerShell을 사용하여 관리 디스크 구성하기
