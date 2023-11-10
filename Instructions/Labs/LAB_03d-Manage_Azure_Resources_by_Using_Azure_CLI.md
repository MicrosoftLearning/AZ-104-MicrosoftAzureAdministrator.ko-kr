---
lab:
  title: '랩 03d: Azure CLI를 사용하여 Azure 리소스 관리(선택 사항)'
  module: Administer Azure Resources
---

# 랩 03d - Azure CLI를 사용하여 Azure 리소스 관리
# 학생용 랩 매뉴얼

## 랩 시나리오

Azure Portal, Azure Resource Manager 템플릿 및 Azure PowerShell을 사용하여 리소스 그룹을 기반으로 리소스를 구성하고 프로비전하는 것과 관련된 기본적인 Azure 관리 기능을 살펴보았습니다. 이제 Azure CLI를 사용하여 동일한 작업을 수행해야 합니다. Azure CLI를 설치하지 않으려면 Azure Cloud Shell에서 사용할 수 있는 Bash 환경을 활용합니다.

**참고:** **[대화형 랩 시뮬레이션](https://mslabs.cloudguides.com/guides/AZ-104%20Exam%20Guide%20-%20Microsoft%20Azure%20Administrator%20Exercise%207)** 을 사용하여 이 랩을 원하는 속도로 클릭할 수 있습니다. 대화형 시뮬레이션과 호스트된 랩 간에 약간의 차이가 있을 수 있지만 보여주는 핵심 개념과 아이디어는 동일합니다. 

## 목표

이 랩에서는 다음을 수행합니다.

+ 작업 1: Azure Cloud Shell에서 Bash 세션을 시작합니다.
+ 작업 2: Azure CLI를 사용하여 리소스 그룹 및 Azure 관리 디스크 만들기
+ 작업 3: Azure CLI를 사용하여 관리 디스크 구성

## 예상 소요 시간: 20분

## 아키텍처 다이어그램

![이미지](../media/lab03d.png)

### Instructions

## 연습 1

## 작업 1: Azure Cloud Shell에서 Bash 세션을 시작합니다.

이 작업에서는 Cloud Shell에서 Bash 세션을 엽니다. 

1. 포털에서 오른쪽 상단의 아이콘을 클릭하여 **Azure Cloud Shell**을 엽니다.

1. **Bash**와 **PowerShell** 중 선택하라는 메시지가 표시되면 **Bash**를 선택합니다. 

    >**참고**: **Cloud Shell**을 처음 시작했는데 **탑재된 스토리지 없음**이라는 메시지가 표시되면 이 랩에서 사용하는 구독을 선택하고 **스토리지 만들기**를 클릭합니다. 

1. 메시지가 표시되면 **스토리지 만들기**를 클릭하고 Azure Cloud Shell 창이 표시될 때까지 기다립니다. 

1. Cloud Shell 창의 왼쪽 상단 모서리에 있는 드롭다운 메뉴에 **Bash**가 나타나는지 확인합니다.

## 작업 2: Azure CLI를 사용하여 리소스 그룹 및 Azure 관리 디스크 만들기

이 작업에서는 Cloud Shell 내에 있는 Azure CLI 세션을 사용하여 리소스 그룹 및 Azure 관리 디스크를 만듭니다.

1. 이전 랩에서 만든 **az104-03c-rg1** 리소스 그룹과 동일한 Azure 지역에서 리소스 그룹을 만들려면 Cloud Shell 내의 Bash 세션에서 다음 명령을 실행합니다.

   ```sh
   LOCATION=$(az group show --name 'az104-03c-rg1' --query location --out tsv)

   RGNAME='az104-03d-rg1'

   az group create --name $RGNAME --location $LOCATION
   ```
1. 새로 만든 리소스 그룹의 속성을 검색하려면 다음 명령을 실행합니다.

   ```sh
   az group show --name $RGNAME
   ```
1. 이 모듈의 이전 랩에서 만든 것과 동일한 특성을 가진 새 관리 디스크를 만들려면 Cloud Shell 내의 Bash 세션에서 다음을 실행합니다.

   ```sh
   DISKNAME='az104-03d-disk1'

   az disk create \
   --resource-group $RGNAME \
   --name $DISKNAME \
   --sku 'Standard_LRS' \
   --size-gb 32
   ```
    >**참고**: 여러 줄 구문을 사용하는 경우 각 줄이 후행 공백이 없는 백 슬래시(`\`)로 끝나고 각 줄의 시작 부분에 선행 공백이 없는지 확인합니다.

1. 새로 만든 디스크의 속성을 검색하려면 다음 명령을 실행합니다.

   ```sh
   az disk show --resource-group $RGNAME --name $DISKNAME
   ```

## 작업 3: Azure CLI를 사용하여 관리 디스크 구성

이 작업에서는 Cloud Shell 내에 있는 Azure CLI 세션을 사용하여 Azure 관리 디스크의 구성을 관리합니다. 

1. Cloud Shell 내의 Bash 세션에서 Azure 관리 디스크의 크기를 **64GB**로 늘리려면 다음 명령을 실행합니다.

   ```sh
   az disk update --resource-group $RGNAME --name $DISKNAME --size-gb 64
   ```

1. 변경이 적용되었는지 확인하려면 다음 명령을 실행합니다.

   ```sh
   az disk show --resource-group $RGNAME --name $DISKNAME --query diskSizeGB
   ```

1. Cloud Shell 내의 Bash 세션에서 디스크 성능 SKU를 **Premium_LRS**로 변경하려면 다음 명령을 실행합니다.

   ```sh
   az disk update --resource-group $RGNAME --name $DISKNAME --sku 'Premium_LRS'
   ```

1. 변경이 적용되었는지 확인하려면 다음 명령을 실행합니다.

   ```sh
   az disk show --resource-group $RGNAME --name $DISKNAME --query sku
   ```

## 리소스 정리

 > **참고**: 더 이상 사용하지 않는 새로 만든 Azure 리소스는 모두 제거하세요. 사용되지 않는 리소스를 제거하면 예기치 않은 요금이 발생하지 않습니다.

 > **참고**:  랩 리소스를 즉시 제거할 수 없어도 걱정하지 마세요. 리소스에 종속성이 있고 삭제하는 데 시간이 오래 걸리는 경우가 있습니다. 리소스 사용량을 모니터링하는 것은 일반적인 관리자 작업이므로 포털에서 리소스를 주기적으로 검토하여 정리가 어떻게 진행되고 있는지 확인합니다. 

1. Azure Portal의 **Cloud Shell** 창에서 **Bash** 세션을 시작합니다.

1. 다음 명령을 실행하여 이 모듈의 전체 랩에서 생성된 모든 리소스 그룹을 나열합니다.

   ```sh
   az group list --query "[?starts_with(name,'az104-03')].name" --output tsv
   ```

1. 다음 명령을 실행하여 이 모듈의 랩 전체에서 만든 모든 리소스 그룹을 삭제합니다.

   ```sh
   az group list --query "[?starts_with(name,'az104-03')].[name]" --output tsv | xargs -L1 bash -c 'az group delete --name $0 --no-wait --yes'
   ```

    >**참고**: 명령은 비동기적으로 실행되므로(--nowait 매개 변수에 의해 결정됨) 동일한 Bash 세션 내에서 즉시 다른 Azure CLI 명령을 실행할 수 있지만 리소스 그룹이 실제로 제거되기까지 몇 분 정도 걸립니다.

## 검토

이 랩에서는 다음을 수행합니다.

- Azure Cloud Shell에서 Bash 세션 시작
- Azure CLI를 사용하여 리소스 그룹 및 Azure 관리 디스크 만들기
- Azure CLI를 사용하여 관리 디스크 구성
