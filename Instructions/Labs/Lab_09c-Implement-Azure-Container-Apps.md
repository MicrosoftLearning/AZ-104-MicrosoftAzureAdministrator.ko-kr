---
lab:
  title: '랩 09c: Azure Container Apps 구현'
  module: Administer PaaS Compute Options
---

# 랩 09c: Azure Container Apps 구현
# 학생용 랩 매뉴얼

## 랩 시나리오
Azure Container Apps를 사용하면 서버리스 플랫폼에서 마이크로서비스 및 컨테이너화된 애플리케이션을 실행할 수 있습니다. Container Apps를 사용하면 클라우드 인프라와 복잡한 컨테이너 오케스트레이터를 수동으로 구성해야 하는 걱정을 버리고 컨테이너를 실행하는 이점을 누릴 수 있습니다.

## 목표

이 랩에서는 다음 작업을 수행합니다.
- 작업 1: 컨테이너 앱 및 환경 만들기
- 작업 2: 컨테이너 앱 배포
- 작업 3: 컨테이너 앱의 테스트 및 자세한 배포

먼저 [Azure Portal](https://portal.azure.com)에 로그인합니다.

## 예상 소요 시간: 20분

## 작업 1: 컨테이너 앱 및 환경 만들기

컨테이너 앱을 만들려면 Azure Portal 홈 페이지에서 시작합니다.

1. `Container Apps` 위쪽 검색 창에서 을 검색합니다.
1. 검색 결과에서 **Container Apps**를 선택합니다.
1. **만들기** 단추를 선택합니다.

### 기본 사항 탭

*기본 사항* 탭에서 다음 작업을 수행합니다.

1. *프로젝트 세부 정보* 섹션에서 다음 값을 입력합니다.

    | 설정 | 작업 |
    |---|---|
    | Subscription | Azure 구독을 선택합니다. |
    | Resource group | **새로 만들기**를 선택하고 `az104-09c-rg1`을 입력합니다. |
    | 컨테이너 앱 이름 |  `my-container-app`를 입력합니다. |

#### 환경 만들기

다음으로 컨테이너 앱에 대한 환경을 만듭니다.

1. 적절한 지역을 선택합니다.

    | 설정 | 값 |
    |--|--|
    | 지역 | **당신의 선택**. |

1. *Container Apps 환경 만들기* 필드에서 **새로 만들기** 링크를 선택합니다.
1. *기본 사항* 탭의 *Container Apps 환경 만들기* 페이지에서 다음 값을 입력합니다.

    | 설정 | 값 |
    |--|--|
    | 환경 이름 | `my-environment`를 입력합니다. |
    | 영역 중복 | **사용 안 함**을 선택합니다. |

1. **모니터링** 탭을 선택하여 Log Analytics 작업 영역을 만듭니다.
1. *Log Analytics 작업 영역* 필드에서 **새로 만들기** 링크를 선택하고 다음 값을 입력합니다.

    | 설정 | 값 |
    |--|--|
    | 속성 | `my-container-apps-logs`을 입력합니다. |
  
    *위치* 필드는 사용자의 지역으로 미리 채워져 있습니다.

1. **확인** 및 **만들기**를 차례로 선택합니다. 

1. **다음: 컨테이너**를 클릭합니다.

1. **빠른 시작 이미지 사용 옆의** 확인란을 선택합니다.

1. 페이지 아래쪽에서 **검토 및 만들기** 단추를 선택합니다. 이 단계는 몇 분 정도 걸릴 수 있습니다. 

    컨테이너 앱의 설정이 확인됩니다. 오류가 없으면 *만들기* 단추가 사용하도록 설정됩니다.  

    오류가 있으면 오류가 포함된 탭이 빨간색 점으로 표시됩니다.  해당 탭으로 이동합니다. 오류가 포함된 필드가 빨간색으로 강조 표시되어 있습니다.  모든 오류가 해결되면 **검토 및 만들기**를 다시 선택합니다.

1. **만들기**를 선택합니다.

    *배포 진행 중*이라는 메시지가 있는 페이지가 표시됩니다.  배포가 성공적으로 완료되면 *배포가 완료됨*이라는 메시지가 표시됩니다.
   
## 작업 2: 컨테이너 앱의 테스트 및 자세한 배포

1. **리소스로 이동**을 선택하여 새 컨테이너 앱을 봅니다.

1. *애플리케이션 URL* 옆에 있는 링크를 선택하여 애플리케이션을 봅니다.

1. **Azure Container Apps 앱이 라이브 메시지인지** 확인합니다.

## 리소스 정리

이 애플리케이션을 계속 사용하지 않으려면 리소스 그룹을 제거하여 Azure Container Apps 인스턴스 및 모든 관련 서비스를 삭제할 수 있습니다.

1. *개요* 섹션에서 **my-container-apps** 리소스 그룹을 선택합니다.
1. 리소스 그룹 *개요* 위쪽에서 **리소스 그룹 삭제** 단추를 선택합니다.
1. 리소스 그룹 이름을 입력하고 앱을 삭제할지 확인합니다. 
1. **삭제**를 선택합니다.
1. 리소스 그룹을 삭제하는 프로세스를 완료하는 데 몇 분 정도 걸릴 수 있습니다.