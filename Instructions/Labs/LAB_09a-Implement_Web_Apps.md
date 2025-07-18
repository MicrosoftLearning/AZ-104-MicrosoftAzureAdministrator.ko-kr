---
lab:
  title: '랩 09a: Web Apps 구현'
  module: Administer PaaS Compute Options
---

# 랩 09a - 웹앱 구현


## 랩 소개

이 랩에서는 Azure 웹앱에 대해 알아봅니다. 외부 GitHub 리포지토리에 Hello World 애플리케이션을 표시하도록 웹앱을 구성하는 방법을 알아봅니다. 스테이징 슬롯을 만들고 프로덕션 슬롯으로 교환하는 방법을 알아봅니다. 수요 변화를 수용하기 위한 자동 크기 조정에 대해서도 알아봅니다.

이 랩을 수행하려면 Azure 구독이 필요합니다. 구독 유형은 이 랩의 기능 가용성에 영향을 미칠 수 있습니다. 지역을 변경할 수 있지만 단계는 미국 동부를 사용하여 작성됩니다.

## 예상 소요 시간: 20분

## 랩 시나리오

사용자의 조직은 회사 웹 사이트를 호스팅하기 위해 Azure 웹앱에 관심이 있습니다. 웹 사이트는 현재 온-프레미스 데이터 센터에서 호스팅됩니다. 웹 사이트는 PHP 런타임 스택을 사용하여 Windows 서버에서 실행되고 있습니다. 하드웨어의 수명이 거의 끝나서 곧 바꿔야 합니다. 조직에서는 Azure를 사용하여 웹 사이트를 호스팅함으로써 새로운 하드웨어 비용을 피하려고 합니다. 

## 대화형 랩 시뮬레이션

>**참고**: 이전에 제공되었던 랩 시뮬레이션은 사용 중지되었습니다.

## 아키텍처 다이어그램

![작업 다이어그램.](../media/az104-lab09a-architecture.png)

## 작업 기술

+ 작업 1: Azure 웹앱을 만들고 구성합니다.
+ 작업 2: 배포 슬롯을 만들고 구성합니다.
+ 작업 3: 웹앱 배포 설정을 구성합니다.
+ 작업 4: 배포 슬롯 전환
+ 작업 5: Azure 웹앱의 자동 크기 조정 구성 및 테스트.

## 작업 1: Azure 웹앱 만들기 및 구성

이 작업에서는 Azure 웹앱을 만듭니다. Azure App Services는 웹, 모바일 및 기타 웹 기반 애플리케이션을 위한 PAAS(Platform As a Service) 솔루션입니다. Azure 웹앱은 PHP, Java, .NET 등 대부분의 런타임 환경을 호스팅하는 Azure App Services의 일부입니다. 선택한 App Service 요금제에 따라 웹앱 컴퓨팅, 스토리지 및 기능이 결정됩니다. 

1. **Azure Portal** - `https://portal.azure.com`에 로그인합니다.

1. `App services`을 검색하고 선택합니다.

1. 드롭다운 메뉴 **웹앱**에서 **+ 만들기**를 선택합니다. 다른 선택 사항을 확인합니다. 

1. **웹앱 만들기** 블레이드의 **기본** 탭에서 다음 설정을 지정합니다(다른 설정은 기본값으로 유지).

    | 설정 | 값 |
    | --- | ---|
    | Subscription | Azure 구독 |
    | Resource group | `az104-rg9`(필요한 경우 **새로 만들기** 선택) |
    | 웹앱 이름 | 전역으로 고유한 이름 |
    | 게시 | **코드** |
    | 런타임 스택 | **PHP 8.2** |
    | 운영 체제 | **Linux** |
    | 지역 | **미국 동부** |
    | 가격 책정 계획 | **프리미엄 V3 P1V3** |
    | 영역 중복 | 기본값을 그대로 적용 |

 1. **검토 + 만들기**를 클릭하고 **만들기**를 클릭합니다.

    >**참고**: 웹앱이 만들어질 때까지 기다린 후 다음 작업으로 진행합니다. 약 1분 정도 소요됩니다.
    
    >**참고**: 배포가 실패하면 다른 지역으로 변경하고 다시 시도합니다. 이는 다른 지역의 할당량 때문입니다.  

1. 배포 후 **리소스로 이동**을 선택합니다.

## 작업 2: 배포 슬롯 만들기 및 구성

이 작업에서는 스테이징 배포 슬롯을 만듭니다. 배포 슬롯을 사용하면 앱을 대중(또는 최종 사용자)에게 제공하기 전에 테스트를 수행할 수 있습니다. 테스트를 수행한 후 슬롯을 개발 또는 준비에서 프로덕션으로 전환할 수 있습니다. 많은 조직에서는 슬롯을 사용하여 사전 프로덕션 테스트를 수행합니다. 또한 많은 조직에서는 모든 애플리케이션(예: 개발, QA, 테스트 및 프로덕션)에 대해 여러 슬롯을 실행합니다.

1. 새로 배포된 웹앱의 블레이드에서 **기본 도메인** 링크를 클릭하여 새 브라우저 탭에 기본 웹 페이지를 표시합니다.

1. 새 브라우저 탭을 닫고 Azure Portal로 돌아가 웹앱 블레이드의 **배포** 섹션에서 **배포 슬롯**을 클릭합니다.

1. **슬롯 추가**를 클릭하고 다음 설정으로 새 슬롯을 추가합니다.

    | 설정 | 값 |
    | --- | ---|
    | 속성 | `staging` |
    | 설정 복제 위치 | **설정을 복제하지 않음**|

1. **추가**를 선택하여 슬롯을 만듭니다.

1. 페이지를 새로 고쳐 프로덕션 및 스테이징 슬롯을 봅니다. 

1. 새로 만든 스테이징 슬롯을 나타내는 항목을 선택합니다.

    >**참고**: 이렇게 하면 스테이징 슬롯의 특성이 표시되는 블레이드가 열립니다.

1. 스테이징 슬롯 블레이드를 검토하고 URL이 프로덕션 슬롯에 할당된 URL과 다르다는 것에 유의합니다.

## 작업 3: 웹앱 배포 설정 구성

이 작업에서는 웹앱 배포 설정을 구성합니다. 배포 설정을 사용하면 지속적인 배포가 가능합니다. 이렇게 하면 앱 서비스에 최신 버전의 애플리케이션이 포함됩니다.

1. 스테이징 슬롯에서 **배포 센터**를 선택한 다음 **설정**을 선택합니다.

    >**참고:** 프로덕션 슬롯이 아닌 스테이징 슬롯 블레이드에 있어야 합니다.
    
1. **소스** 드롭다운 목록에서 **외부 Git**을 선택합니다. 다른 선택 사항을 확인합니다. 

1. 리포지토리 필드에 `https://github.com/Azure-Samples/php-docs-hello-world`를 입력합니다.

1. 분기 필드에 `master`를 입력합니다.

1. **저장**을 선택합니다.

1. 스테이징 슬롯에서 **개요**를 선택합니다.

1. **기본 도메인** 링크를 선택하고 새 탭에서 URL을 엽니다. 

1. 스테이징 슬롯에 **Hello World**가 표시되는지 확인합니다. 

>**참고:** 배포는 몇 분 정도가 걸릴 수 있습니다. 애플리케이션 페이지를 **새로 고침**합니다.

## 작업 4: 배포 슬롯 교환

이 작업에서는 스테이징 슬롯을 프로덕션 슬롯으로 전환합니다. 슬롯을 교환하면 스테이징 슬롯에서 테스트한 코드를 사용하고 이를 프로덕션으로 이동할 수 있습니다. Azure Portal에서는 슬롯에 대해 사용자 지정한 다른 애플리케이션 설정을 이동해야 하는 경우에도 메시지를 표시합니다. 슬롯 교환은 애플리케이션 팀과 애플리케이션 지원 팀, 특히 일상적인 앱 업데이트와 버그 수정을 배포하는 팀의 일반적인 작업입니다.

1. 다시 **배포 슬롯** 블레이드로 이동한 다음 **교환**를 선택합니다.

1. 기본 설정을 검토하고 **교환 시작**을 클릭합니다. 스왑이 완료되었다는 알림을 기다립니다.

1. 포털 홈 페이지로 돌아갑니다. 프로덕션 웹앱과 스테이징 슬롯이 모두 있어야 합니다.

1. `App Services`을(를) 검색하고 App Service 웹앱을 선택합니다. 그러면 프로덕션 배포 슬롯으로 돌아갑니다.

1. App Service 웹앱을 선택하고 웹앱의 **개요** 블레이드에서 **기본 도메인** 링크를 선택하면 웹사이트 홈 페이지가 표시됩니다.

1. 프로덕션 웹 페이지에 **Hello World!** 가 표시되는지 확인합니다. 페이지에서 사용할 수 있는 바로 가기 키를 보여 줍니다.

    >**참고:** 다음 작업의 부하 테스트에 필요한 기본 도메인 **URL**을 복사합니다. 

## 작업 5: Azure 웹앱의 자동 크기 조정 구성 및 테스트

이 작업에서는 Azure Web App의 자동 크기 조정을 구성합니다. 자동 크기 조정을 사용하면 웹앱에 대한 트래픽이 증가할 때 웹앱에 대한 최적의 성능을 유지할 수 있습니다. 앱이 크기 조정되어야 하는 시기를 결정하려면 CPU 사용량, 메모리 또는 대역폭과 같은 메트릭을 모니터링하면 됩니다.

1. **설정** 섹션에서 **스케일 아웃(App Service 요금제)** 을 선택합니다.

    >**참고:** 스테이징 슬롯이 아닌 프로덕션 슬롯에서 작업하고 있는지 확인합니다.  

1. **크기 조정** 섹션에서 **자동**을 선택합니다. **규칙 기반** 옵션을 확인합니다. 다양한 앱 메트릭에 대해 규칙 기반 조정을 구성할 수 있습니다. 

1. **최대 버스트** 필드에서 **2**를 선택합니다.

    ![자동 크기 조정 페이지의 스크린샷](../media/az104-lab09a-autoscale.png)

1. **저장**을 선택합니다.

1. **문제 진단 및 해결**을 선택합니다.(왼쪽 메뉴)

1. **앱 부하 테스트** 상자에서 **부하 테스트 만들기**를 선택합니다.

    + **+ 만들기**를 선택하고 부하 테스트에 **이름**을 지정합니다.  이름은 고유해야 합니다.
    + **검토 + 만들기**를 선택한 다음, **만들기**를 선택합니다.

1. 부하 테스트가 만들어질 때까지 기다린 다음 **리소스로 이동**을 선택합니다.

1. **개요** | **HTTP 요청을 추가하여 만들기**에서 **만들기**를 선택합니다.

1. **테스트 계획** 탭에서 **요청 추가**를 클릭합니다. **URL 필드**에 **기본 도메인** URL을 붙여넣으세요. 형식이 올바른지, **https://** 로 시작하는지 확인합니다. **추가**를 선택하여 변경 내용을 저장합니다. 

1. **검토 + 만들기** 및 **만들기**를 선택합니다.

    >**참고:** 테스트를 만드는 데 몇 분 정도 걸릴 수 있습니다. 알림 보기.

1. 테스트로 이동합니다(홈페이지에 나열됨). 

1. **가상 사용자**, **응답 시간** 및 **요청/초**를 포함한 라이브 메트릭을 새로 고침하고 검토합니다.

1. **중지**를 선택하여 테스트 실행을 완료합니다. 테스트가 완료될 때까지 기다릴 필요가 없습니다. 

## 리소스 정리

**고유의 구독**으로 작업하는 경우 랩 리소스를 삭제해 보세요. 이렇게 하면 리소스가 확보되고 비용이 최소화됩니다. 랩 리소스를 삭제하려면 랩 리소스 그룹을 삭제하는 것이 가장 쉽습니다. 

+ Azure Portal에서 리소스 그룹을 선택하고 **리소스 그룹 삭제**, **리소스 그룹 이름 입력**을 선택한 다음 **삭제**를 클릭합니다.
+ Azure PowerShell 사용, `Remove-AzResourceGroup -Name resourceGroupName`.
+ CLI 사용, `az group delete --name resourceGroupName`.

## Copilot을 사용하여 학습 확장
Copilot은 Azure 스크립팅 도구를 사용하는 방법을 익히는 데 도움을 줍니다. 또한 Copilot은 랩에서 다루지 않는 영역이나 추가 정보가 필요한 영역을 지원할 수 있습니다. Edge 브라우저를 열고 Copilot(오른쪽 위)을 선택하거나 *copilot.microsoft.com*으로 이동하세요. 몇 분 정도 시간을 내어 이러한 프롬프트를 사용해 보세요.

+ Azure 웹앱을 만들고 구성하는 단계를 요약합니다.
+ Azure 웹앱의 크기를 조정할 수 있는 방법은 무엇인가요?

## 자기 주도적 학습을 통해 자세히 알아보기

+ [App Service 배포 슬롯을 사용하여 테스트 및 롤백하기 위해 웹앱 배포 스테이징](https://learn.microsoft.com/training/modules/stage-deploy-app-service-deployment-slots/). Azure App Service에서 배포 슬롯을 사용하여 배포를 간소화하고 웹앱을 롤백합니다.
+ [App Service 강화 및 규모 확장을 통해 App Service 웹앱의 크기를 조정하여 효율적으로 요구 사항 충족](https://learn.microsoft.com/training/modules/app-service-scale-up-scale-out/) 사용 가능한 리소스를 점차적으로 늘린 다음, 작업이 감소하면 비용을 줄이기 위해 이러한 리소스를 줄여 작업이 증가하는 기간에 대응합니다.

## 핵심 내용

축하합니다. 랩을 완료했습니다. 이 랩의 주요 내용은 다음과 같습니다. 

+ Azure App Services를 사용하면 웹앱을 빠르게 빌드, 배포 및 크기 조정할 수 있습니다.
+ App Service에는 ASP.NET, Java, PHP 및 Python을 포함한 다양한 개발자 환경에 대한 지원이 포함되어 있습니다.
+ 배포 슬롯을 사용하면 웹앱을 배포하고 테스트하기 위한 별도의 환경을 만들 수 있습니다.
+ 추가 수요를 처리하기 위해 웹앱의 크기를 수동 또는 자동으로 조정할 수 있습니다.
+ 다양한 진단 및 테스트 도구를 사용할 수 있습니다. 
