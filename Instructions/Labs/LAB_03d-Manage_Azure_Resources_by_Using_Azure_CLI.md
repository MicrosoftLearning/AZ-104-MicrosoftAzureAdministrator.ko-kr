---
lab:
  title: 03d - Azure CLI를 사용하여 Azure 리소스 관리
  module: Administer Azure Resources
---

# <a name="lab-03d---manage-azure-resources-by-using-azure-cli"></a>랩 03d - Azure CLI를 사용하여 Azure 리소스 관리
# <a name="student-lab-manual"></a>학생용 랩 매뉴얼

## <a name="lab-scenario"></a>랩 시나리오

Now that you explored the basic Azure administration capabilities associated with provisioning resources and organizing them based on resource groups by using the Azure portal, Azure Resource Manager templates, and Azure PowerShell, you need to carry out the equivalent task by using Azure CLI. To avoid installing Azure CLI, you will leverage Bash environment available in Azure Cloud Shell.

대화형 가이드 형식으로 이 랩을 미리 보려면 **[여기를 클릭하세요](https://mslabs.cloudguides.com/en-us/guides/AZ-104%20Exam%20Guide%20-%20Microsoft%20Azure%20Administrator%20Exercise%207)** .

## <a name="objectives"></a>목표

이 랩에서는 다음을 수행합니다.

+ 작업 1: Azure Cloud Shell에서 Bash 세션을 시작합니다.
+ 작업 2: Azure CLI를 사용하여 리소스 그룹 및 Azure 관리 디스크 만들기
+ 작업 3: Azure CLI를 사용하여 관리 디스크 구성

## <a name="estimated-timing-20-minutes"></a>예상 소요 시간: 20분

## <a name="instructions"></a>Instructions

### <a name="exercise-1"></a>연습 1

#### <a name="task-1-start-a-bash-session-in-azure-cloud-shell"></a>작업 1: Azure Cloud Shell에서 Bash 세션을 시작합니다.

이 작업에서는 Cloud Shell에서 Bash 세션을 엽니다. 

1. 포털에서 오른쪽 상단의 아이콘을 클릭하여 **Azure Cloud Shell**을 엽니다.

1. **Bash**와 **PowerShell** 중 선택하라는 메시지가 표시되면 **Bash**를 선택합니다. 

    >**참고**: **Cloud Shell**을 처음 시작했는데 **탑재된 스토리지 없음**이라는 메시지가 표시되면 이 랩에서 사용하는 구독을 선택하고 **스토리지 만들기**를 클릭합니다. 

1. 메시지가 표시되면 **스토리지 만들기**를 클릭하고 Azure Cloud Shell 창이 표시될 때까지 기다립니다. 

1. Cloud Shell 창의 왼쪽 상단 모서리에 있는 드롭다운 메뉴에 **Bash**가 나타나는지 확인합니다.

#### <a name="task-2-create-a-resource-group-and-an-azure-managed-disk-by-using-azure-cli"></a>작업 2: Azure CLI를 사용하여 리소스 그룹 및 Azure 관리 디스크 만들기

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

#### <a name="task-3-configure-the-managed-disk-by-using-azure-cli"></a>작업 3: Azure CLI를 사용하여 관리 디스크 구성

이 작업에서는 Cloud Shell 내에 있는 Azure CLI 세션을 사용하여 Azure 관리 디스크의 구성을 관리합니다. 

1. Cloud Shell 내의 Bash 세션에서 Azure 관리 디스크의 크기를 **64GB**로 늘리려면 다음 명령을 실행합니다.

   ```sh
   az disk update --resource-group $RGNAME --name $DISKNAME --size-gb 64
   ```

1. 변경이 적용되었는지 확인하려면 다음 명령을 실행합니다.

   ```sh
   az disk show --resource-group $RGNAME --name $DISKNAME --query diskSizeGb
   ```

1. Cloud Shell 내의 Bash 세션에서 디스크 성능 SKU를 **Premium_LRS**로 변경하려면 다음 명령을 실행합니다.

   ```sh
   az disk update --resource-group $RGNAME --name $DISKNAME --sku 'Premium_LRS'
   ```

1. 변경이 적용되었는지 확인하려면 다음 명령을 실행합니다.

   ```sh
   az disk show --resource-group $RGNAME --name $DISKNAME --query sku
   ```

#### <a name="clean-up-resources"></a>리소스 정리

 > <bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: Remember to remove any newly created Azure resources that you no longer use. Removing unused resources ensures you will not see unexpected charges.

 > <bpt id="p1">**</bpt>Note<ept id="p1">**</ept>:  Don't worry if the lab resources cannot be immediately removed. Sometimes resources have dependencies and take a long time to delete. It is a common Administrator task to monitor resource usage, so just periodically review your resources in the Portal to see how the cleanup is going. 

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

#### <a name="review"></a>검토

이 랩에서는 다음을 수행합니다.

- Azure Cloud Shell에서 Bash 세션 시작
- Azure CLI를 사용하여 리소스 그룹 및 Azure 관리 디스크 만들기
- Azure CLI를 사용하여 관리 디스크 구성
