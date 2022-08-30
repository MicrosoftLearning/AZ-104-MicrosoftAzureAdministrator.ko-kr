---
lab:
  title: 03a - Azure Portal을 사용하여 Azure 리소스 관리
  module: Module 03 - Azure Administration
---

# <a name="lab-03a---manage-azure-resources-by-using-the-azure-portal"></a>랩 03a - Azure Portal을 사용하여 Azure 리소스 관리
# <a name="student-lab-manual"></a>학생용 랩 매뉴얼

## <a name="lab-scenario"></a>랩 시나리오

You need to explore the basic Azure administration capabilities associated with provisioning resources and organizing them based on resource groups, including moving resources between resource groups. You also want to explore options for protecting disk resources from being accidentally deleted, while still allowing for modifying their performance characteristics and size.

## <a name="objectives"></a>목표

이 랩에서는 다음 작업을 수행합니다.

+ 작업 1: 리소스 그룹을 만들고 리소스 그룹에 리소스 배포
+ 작업 2: 리소스 그룹 간 리소스 이동
+ 작업 3: 리소스 잠금 구현 및 테스트

## <a name="estimated-timing-20-minutes"></a>예상 소요 시간: 20분

## <a name="architecture-diagram"></a>아키텍처 다이어그램

![이미지](../media/lab03a.png)

## <a name="instructions"></a>지침

### <a name="exercise-1"></a>연습 1

#### <a name="task-1-create-resource-groups-and-deploy-resources-to-resource-groups"></a>작업 1: 리소스 그룹을 만들고 리소스 그룹에 리소스 배포

이 작업에서는 Azure Portal을 사용하여 리소스 그룹을 만들고 리소스 그룹에 디스크를 만듭니다.

1. [**Azure Portal**](http://portal.azure.com)에 로그인합니다.

1. Azure Portal에서 **디스크**를 검색하여 선택하고 **+ 만들기**를 클릭한 후 다음 설정을 지정합니다.

    |설정|값|
    |---|---|
    |Subscription| 리소스 그룹을 만든 Azure 구독의 이름 |
    |리소스 그룹| 새 리소스 그룹 **az104-03a-rg1**의 이름 |
    |디스크 이름| **az104-03a-disk1** |
    |지역| **(미국) 미국 동부** |
    |가용성 영역| **없음** |
    |소스 형식| **없음** |

    >**참고**: 리소스를 만들 때 새 리소스 그룹을 만들거나 기존 리소스 그룹을 사용할 수 있습니다.

1. 디스크 유형과 크기를 각각 **표준 HDD** 및 **32GiB**로 변경합니다.

1. **검토 + 만들기**를 클릭한 다음, **만들기**를 클릭합니다.

    ><bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: Wait until the disk is created. This should take less than a minute.

#### <a name="task-2-move-resources-between-resource-groups"></a>작업 2: 리소스 그룹 간 리소스 이동 

본 작업에서는 이전 작업에서 만든 디스크 리소스를 새 리소스 그룹으로 이동합니다. 

1. **리소스 그룹**을 검색하여 선택합니다. 

1. **리소스 그룹** 블레이드에서 이전 작업에서 만든 **az104-03a-rg1** 리소스 그룹을 나타내는 항목을 클릭합니다.

1. 리소스 그룹의 **개요** 블레이드에서 리소스 그룹 목록에서 새로 만든 디스크를 나타내는 항목을 선택합니다. 도구 모음에서 **이동**을 클릭하고 드롭다운 목록에서 **다른 리소스 그룹으로 이동**을 선택합니다.

    >**참고**: 이 방법으로 동시에 여러 리소스를 이동할 수 있습니다. 

1. Below the <bpt id="p1">**</bpt>Resource group<ept id="p1">**</ept> text box, click <bpt id="p2">**</bpt>Create new<ept id="p2">**</ept> then type <bpt id="p3">**</bpt>az104-03a-rg2<ept id="p3">**</ept> in the text box. On the Review tab, select the checkbox <bpt id="p1">**</bpt>I understand that tools and scripts associated with moved resources will not work until I update them to use new resource IDs<ept id="p1">**</ept>, and click <bpt id="p2">**</bpt>Move<ept id="p2">**</ept>.

    ><bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: Do not wait for the move to complete but instead proceed to the next task. The move might take about 10 minutes. You can determine that the operation was completed by monitoring activity log entries of the source or target resource group. Revisit this step once you complete the next task.

#### <a name="task-3-implement-resource-locks"></a>작업 3: 리소스 잠금 구현

이 작업에서는 디스크 리소스를 포함하는 Azure 리소스 그룹에 리소스 잠금을 적용합니다.

1. Azure Portal에서 **디스크**를 검색하여 선택하고 **+ 만들기**를 클릭한 후 다음 설정을 지정합니다.

    |설정|값|
    |---|---|
    |Subscription| 이 랩에서 사용 중인 구독 이름 |
    |리소스 그룹| 리소스 그룹 **새로 만들기**를 클릭하고 이름을 **az104-03a-rg3**로 지정합니다. |
    |디스크 이름| **az104-03a-disk2** |
    |지역| 이 랩에서 다른 리소스 그룹을 만든 Azure 지역의 이름 |
    |가용성 영역| **없음** |
    |소스 형식| **없음** |

1. 디스크 유형과 크기를 각각 **표준 HDD** 및 **32GiB**로 설정합니다.

1. **검토 + 만들기**를 클릭한 다음, **만들기**를 클릭합니다.

1. **리소스로 이동**을 클릭합니다.

1. 디스크의 개요 페이지에서 리소스 그룹 **az104-03a-rg3**의 이름을 클릭합니다.

1. **az104-03a-rg3** 리소스 그룹 블레이드에서 **잠금**과 **+ 추가**를 차례로 클릭하고 다음 설정을 지정합니다.

    |설정|값|
    |---|---|
    |잠금 이름| **az104-03a-delete-lock** |
    |잠금 유형| **Delete** |
    
1. **확인**을 클릭합니다.    

1. **az104-03a-rg3** 리소스 그룹 블레이드에서 **개요**를 클릭하고 리소스 그룹 리소스 목록에서 이 작업의 전반부에서 만든 디스크를 나타내는 항목을 선택하고 도구 모음에서 **삭제**를 클릭합니다. 

1. **선택한 모든 리소스를 삭제하시겠습니까?** 라는 메시지가 표시되면 **삭제 확인** 텍스트 상자에서 **예**를 입력하고 **삭제**를 클릭합니다.

1. 삭제 작업이 실패했음을 알리는 오류 메시지가 표시됩니다. 

    >**참고**: 오류 메시지에 명시된대로 리소스 그룹 수준에 적용된 잠금 삭제로 인한 것으로 예상됩니다.

1. **az104-03a-rg3** 리소스 그룹의 리소스 목록으로 돌아가 **az104-03a-disk2** 리소스를 나타내는 항목을 클릭합니다. 

1. On the <bpt id="p1">**</bpt>az104-03a-disk2<ept id="p1">**</ept> blade, in the <bpt id="p2">**</bpt>Settings<ept id="p2">**</ept> section, click <bpt id="p3">**</bpt>Size + performance<ept id="p3">**</ept>, set the disk type and size to <bpt id="p4">**</bpt>Premium SSD<ept id="p4">**</ept> and <bpt id="p5">**</bpt>64 GiB<ept id="p5">**</ept>, respectively, and click <bpt id="p6">**</bpt>Resize<ept id="p6">**</ept> to apply the change. Verify that the change was successful.

    >**참고**: 리소스 그룹 수준 잠금은 삭제 작업에만 적용되므로 예상된 결과입니다. 

#### <a name="clean-up-resources"></a>리소스 정리

   >리소스 프로비저닝, 그리고 리소스 그룹 간 리소스 이동 등 리소스 그룹을 기준으로 리소스를 정리하는 것과 관련된 기본 Azure 관리 기능을 살펴봐야 합니다.

1. **az104-03a-rg3** 리소스 그룹 블레이드로 이동하여 **잠금** 블레이드를 표시하고 **삭제** 잠금 항목의 오른쪽에 있는 **삭제** 링크를 클릭하여 **az104-03a-delete-lock** 잠금을 제거합니다.

#### <a name="review"></a>검토

이 랩에서는 다음을 수행합니다.

- 리소스 그룹 만들기 및 리소스 그룹에 리소스 배포
- 리소스 그룹 간 리소스 이동
- 리소스 잠금 구현 및 테스트
