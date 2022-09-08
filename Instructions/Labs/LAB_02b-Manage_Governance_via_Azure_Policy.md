---
lab:
  title: 02b - Azure Policy를 통한 거버넌스 관리
  module: Administer Governance and Compliance
---

# <a name="lab-02b---manage-governance-via-azure-policy"></a>랩 02b - Azure Policy를 통한 거버넌스 관리
# <a name="student-lab-manual"></a>학생용 랩 매뉴얼

## <a name="lab-scenario"></a>랩 시나리오

Contoso에서 Azure 리소스 관리를 개선하기 위해 다음 기능을 구현하는 작업을 맡았습니다.

- 인프라 리소스(예: Cloud Shell 스토리지 계정)만 포함하는 리소스 그룹을 태그 지정합니다.

- 적절하게 태그가 지정된 인프라 리소스만 인프라 리소스 그룹에 추가할 수 있도록 합니다.

- 모든 비준수 리소스를 수정합니다.

대화형 가이드 형식으로 이 랩을 미리 보려면 **[여기를 클릭하세요](https://mslabs.cloudguides.com/en-us/guides/AZ-104%20Exam%20Guide%20-%20Microsoft%20Azure%20Administrator%20Exercise%203)** .

## <a name="objectives"></a>목표

이 랩에서는 다음 작업을 수행합니다.

+ 작업 1: Azure Portal을 통한 태그 만들기 및 할당
+ 작업 2: Azure Policy를 통한 강제 태그 지정
+ 작업 3: Azure Policy를 통한 태그 지정 적용

## <a name="estimated-timing-30-minutes"></a>예상 소요 시간: 30분

## <a name="architecture-diagram"></a>아키텍처 다이어그램

![이미지](../media/lab02b.png)

## <a name="instructions"></a>Instructions

### <a name="exercise-1"></a>연습 1

#### <a name="task-1-assign-tags-via-the-azure-portal"></a>작업 1: Azure Portal을 통한 태그 할당

이 작업에서는 Azure Portal을 통해 Azure 리소스 그룹에 태그를 만들고 할당합니다.

1. Azure Portal에서 **Cloud Shell**내의 **PowerShell** 세션을 시작합니다.

    >**참고**: **Cloud Shell**을 처음 시작했는데 **탑재된 스토리지 없음**이라는 메시지가 표시되면 이 랩에서 사용하는 구독을 선택하고 **스토리지 만들기**를 클릭합니다. 

1. Cloud Shell 창에서 다음을 실행하여 Cloud Shell에서 사용하는 스토리지 계정의 이름을 식별합니다.

   ```powershell
   df
   ```

1. 명령의 출력에 Cloud Shell 홈 드라이브 탑재를 지정하는 정규화된 경로의 첫 번째 부분을 기록해 둡니다(여기서는 `xxxxxxxxxxxxxx`로 표시됨).

   ```
   //xxxxxxxxxxxxxx.file.core.windows.net/cloudshell   (..)  /usr/csuser/clouddrive
   ```

1. Azure Portal에서 **스토리지 계정**을 검색하여 선택하고 스토리지 계정 목록에서 이전 단계에서 식별한 스토리지 계정을 나타내는 항목을 클릭합니다.

1. 스토리지 계정 블레이드에서 스토리지 계정을 포함하는 리소스 그룹의 이름을 나타내는 링크를 클릭합니다.

    **참고**: 스토리지 계정이 어떤 리소스 그룹에 있는지 메모해 두세요. 나중에 랩에서 필요합니다.

1. 리소스 그룹 블레이드에서 **태그** 옆에 있는 **편집**을 클릭하여 새 태그를 만듭니다.

1. 다음 설정을 사용하여 태그를 만들고 변경 내용을 적용합니다.

    | 설정 | 값 |
    | --- | --- |
    | Name | **역할** |
    | 값 | **인프라** |

1. Navigate back to the storage account blade. Review the <bpt id="p1">**</bpt>Overview<ept id="p1">**</ept> information and note that the new tag was not automatically assigned to the storage account. 

#### <a name="task-2-enforce-tagging-via-an-azure-policy"></a>작업 2: Azure Policy를 통한 강제 태그 지정

본 작업에서는 *리스스에 대한 태그 및 값 필요* 기본 제공 정책을 리소스 그룹에 할당하고 결과를 평가합니다. 

1. Azure Portal에서 **정책**을 찾아서 선택합니다. 

1. In the <bpt id="p1">**</bpt>Authoring<ept id="p1">**</ept> section, click <bpt id="p2">**</bpt>Definitions<ept id="p2">**</ept>. Take a moment to browse through the list of built-in policy definitions that are available for you to use. List all built-in policies that involve the use of tags by selecting the <bpt id="p1">**</bpt>Tags<ept id="p1">**</ept> entry (and de-selecting all other entries) in the <bpt id="p2">**</bpt>Category<ept id="p2">**</ept> drop-down list. 

1. **리소스에 대한 태그 및 값 필요** 기본 제공 정책을 나타내는 항목을 클릭하고 해당 정의를 검토합니다.

1. **리소스에 대한 태그 및 값 필요** 기본 제공 정책 정의 블레이드에서 **할당**을 클릭합니다.

1. 줄임표 단추를 클릭하고 다음 값을 선택하여 **범위**를 지정합니다.

    | 설정 | 값 |
    | --- | --- |
    | Subscription | 이 랩에서 사용 중인 Azure 구독의 이름 |
    | 리소스 그룹 | 이전 작업에서 식별한 Cloud Shell 계정을 포함하는 리소스 그룹의 이름 |

    ><bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: A scope determines the resources or resource groups where the policy assignment takes effect. You could assign policies on the management group, subscription, or resource group level. You also have the option of specifying exclusions, such as individual subscriptions, resource groups, or resources (depending on the assignment scope). 

1. 다음 설정을 지정하여 할당의 **기본** 속성을 구성합니다(다른 설정은 기본값으로 유지).

    | 설정 | 값 |
    | --- | --- |
    | 할당 이름 | **인프라 값이 있는 역할 태그 필요**|
    | Description | **Cloud Shell 리소스 그룹의 모든 리소스에 대해 인프라 값이 있는 역할 태그 필요**|
    | 정책 적용 | 사용 |

    ><bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: The <bpt id="p2">**</bpt>Assignment name<ept id="p2">**</ept> is automatically populated with the policy name you selected, but you can change it. You can also add an optional <bpt id="p1">**</bpt>Description<ept id="p1">**</ept>. <bpt id="p1">**</bpt>Assigned by<ept id="p1">**</ept> is automatically populated based on the user name creating the assignment. 

1. **다음**을 클릭하고 **매개 변수**를 다음 값으로 설정합니다.

    | 설정 | 값 |
    | --- | --- |
    | 태그 이름 | **역할** |
    | 태그 값 | **인프라** |

1. **다음**을 클릭하여 **수정** 탭을 검토합니다. **관리 ID 만들기** 체크박스는 선택하지 않은 상태로 유지합니다. 

    >**참고**: 본 설정은 정책 또는 이니셔티브에 **deployIfNotExists** 또는 **수정** 효과가 포함될 때 사용할 수 있습니다.

1. **검토 + 만들기**를 클릭한 다음, **만들기**를 클릭합니다.

    >**참고**: 이제 필요한 태그를 명시적으로 추가하지 않고 리소스 그룹에 다른 Azure Storage 계정을 만들어 새 정책 할당이 적용되었는지 확인합니다. 
    
    >**참고**: 정책이 적용되기까지 5~15분 정도 걸릴 수 있습니다.

1. 이전 작업에서 식별한 Cloud Shell 홈 드라이브에 사용된 스토리지 계정을 호스트하는 리소스 그룹의 블레이드로 돌아갑니다.

1. 리소스 그룹 블레이드에서 **+ 만들기**를 클릭한 다음, **스토리지 계정**을 검색하고, **+ 만들기**를 클릭합니다. 

1. **스토리지 계정 만들기** 블레이드의 **기본** 탭에서 정책이 적용된 리소스 그룹을 사용하고 있는지 확인한 후 다음 설정을 지정하고(다른 설정은 기본값으로 유지) **검토 + 만들기**를 클릭한 후에 **만들기**를 클릭합니다.

    | 설정 | 값 |
    | --- | --- |
    | 스토리지 계정 이름 | 문자로 시작하며 3~24개의 소문자와 숫자로 이루어진 전역적으로 고유한 조합 |

1. Once you create the deployment, you should see the <bpt id="p1">**</bpt>Deployment failed<ept id="p1">**</ept> message in the <bpt id="p2">**</bpt>Notifications<ept id="p2">**</ept> list of the portal. From the <bpt id="p1">**</bpt>Notifications<ept id="p1">**</ept> list, navigate to the deployment overview and click the <bpt id="p2">**</bpt>Deployment failed. Click here for details<ept id="p2">**</ept> message to identify the reason for the failure. 

    >**참고**: 오류 메시지에서 리소스 배포가 정책상 허용되지 않는 것인지를 확인합니다. 

    ><bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: By clicking the <bpt id="p2">**</bpt>Raw Error<ept id="p2">**</ept> tab, you can find more details about the error, including the name of the role definition <bpt id="p3">**</bpt>Require Role tag with Infra value<ept id="p3">**</ept>. The deployment failed because the storage account you attempted to create did not have a tag named <bpt id="p1">**</bpt>Role<ept id="p1">**</ept> with its value set to <bpt id="p2">**</bpt>Infra<ept id="p2">**</ept>.

#### <a name="task-3-apply-tagging-via-an-azure-policy"></a>작업 3: Azure Policy를 통한 태그 지정 적용

이 작업에서는 다른 정책 정의를 사용하여 비준수 리소스를 수정합니다. 

1. Azure Portal에서 **정책**을 찾아서 선택합니다. 

1. **작성** 섹션에서 **할당**을 클릭합니다. 

1. 할당 목록에서 **인프라 값이 있는 역할 태그 필요** 정책을 나타내는 행의 줄임표 아이콘을 클릭하고 **할당 삭제** 메뉴 항목을 사용하여 할당을 삭제합니다.

1. **정책 할당**을 클릭한 다음 줄임표 단추를 클릭하고 다음 값을 선택하여 **범위**를 지정합니다.

    | 설정 | 값 |
    | --- | --- |
    | Subscription | 이 랩에서 사용 중인 Azure 구독의 이름 |
    | 리소스 그룹 | 첫 번째 작업에서 식별한 Cloud Shell 계정이 포함된 리소스 그룹의 이름 |

1. **정책 정의**를 지정하려면 줄임표 단추를 클릭한 다음 **누락된 경우 리소스 그룹에서 태그 상속**을 검색하고 선택합니다.

1. 다음 설정을 지정(다른 설정은 기본값으로 유지)하여 할당의 나머지 **기본** 속성을 구성합니다.

    | 설정 | 값 |
    | --- | --- |
    | 할당 이름 | **누락된 경우 Cloud Shell 리소스 그룹에서 역할 태그 및 해당 인프라 값 상속**|
    | 설명 | **누락된 경우 Cloud Shell 리소스 그룹에서 역할 태그 및 해당 인프라 값 상속**|
    | 정책 적용 | 사용 |

1. **다음**을 클릭하고 **매개 변수**를 다음 값으로 설정합니다.

    | 설정 | 값 |
    | --- | --- |
    | 태그 이름 | **역할** |

1. **다음**을 클릭하고 **수정** 탭에서 다음 설정을 구성합니다(다른 설정은 기본값으로 유지).

    | 설정 | 값 |
    | --- | --- |
    | 수정 작업 만들기 | 사용 |
    | 수정해야 하는 정책 | **누락된 경우 구독에서 태그 상속** |

    >**참고**: 이 정책 정의에는 **수정** 효과가 포함됩니다.

1. **검토 + 만들기**를 클릭한 다음, **만들기**를 클릭합니다.

    >**참고**: 새 정책 할당이 적용되는지 확인하려면 필요한 태그를 명시적으로 추가하지 않고 동일한 리소스 그룹에 다른 Azure Storage 계정을 만듭니다. 
    
    >**참고**: 정책이 적용되기까지 5~15분 정도 걸릴 수 있습니다.

1. 첫 번째 작업에서 식별한 Cloud Shell 홈 드라이브에 사용된 스토리지 계정을 호스트하는 리소스 그룹의 블레이드로 돌아갑니다.

1. 리소스 그룹 블레이드에서 **+ 만들기**를 클릭한 다음, **스토리지 계정**을 검색하고, **+ 만들기**를 클릭합니다. 

1. **스토리지 계정 만들기** 블레이드의 **기본** 탭에서 정책이 적용된 리소스 그룹을 사용하고 있는지 확인한 후 다음 설정을 지정하고(다른 설정은 기본값으로 유지) **검토 + 만들기**를 클릭합니다.

    | 설정 | 값 |
    | --- | --- |
    | 스토리지 계정 이름 | 문자로 시작하며 3~24개의 소문자와 숫자로 이루어진 전역적으로 고유한 조합 |

1. 유효성 검사를 통과했는지 확인하고 **만들기**를 클릭합니다.

1. 새 스토리지 계정이 프로비전되면 **리소스로 이동** 단추를 클릭하고 새로 만든 스토리지 계정의 **개요** 블레이드에서 **인프라** 값이 있는 **역할** 태그가 리소스에 자동으로 할당된 것을 확인합니다.

#### <a name="task-4-clean-up-resources"></a>작업 4: 리소스 정리

   ><bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: Remember to remove any newly created Azure resources that you no longer use. Removing unused resources ensures you will not see unexpected charges, although keep in mind that Azure policies do not incur extra cost.
   
   ><bpt id="p1">**</bpt>Note<ept id="p1">**</ept>:  Don't worry if the lab resources cannot be immediately removed. Sometimes resources have dependencies and take a longer time to delete. It is a common Administrator task to monitor resource usage, so just periodically review your resources in the Portal to see how the cleanup is going. 

1. 포털에서 **정책**을 검색하여 선택합니다.

1. **작성** 섹션에서 **할당**을 클릭하고 이전 작업에서 만든 할당의 오른쪽에 있는 줄임표 아이콘을 클릭한 다음 **할당 삭제**를 클릭합니다. 

1. 포털에서 **스토리지 계정**을 검색하여 선택합니다.

1. In the list of storage accounts, select the resource group corresponding to the storage account you created in the last task of this lab. Select <bpt id="p1">**</bpt>Tags<ept id="p1">**</ept> and click <bpt id="p2">**</bpt>Delete<ept id="p2">**</ept> (Trash can to the right) to the <bpt id="p3">**</bpt>Role:Infra<ept id="p3">**</ept> tag and press <bpt id="p4">**</bpt>Apply<ept id="p4">**</ept>. 

1. Click <bpt id="p1">**</bpt>Overview<ept id="p1">**</ept> and click <bpt id="p2">**</bpt>Delete<ept id="p2">**</ept> on the top of the storage account blade. When prompted for the confirmation, in the <bpt id="p1">**</bpt>Delete storage account<ept id="p1">**</ept> blade, type the name of the storage account to confirm and click <bpt id="p2">**</bpt>Delete<ept id="p2">**</ept>. 

#### <a name="review"></a>검토

이 랩에서는 다음을 수행합니다.

- Azure Portal을 통한 태그 만들기 및 할당
- Azure Policy를 통한 강제 태그 지정
- Azure Policy를 통한 태그 지정 적용
