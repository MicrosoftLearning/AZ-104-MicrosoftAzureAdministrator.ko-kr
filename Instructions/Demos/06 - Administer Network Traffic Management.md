---
demo:
  title: '데모 06: 네트워크 트래픽 관리'
  module: Administer Network Traffic Management
---


# 06 - 네트워크 트래픽 관리 관리

## Azure Load Balancer 구성

이 데모에서는 공용 부하 분산 장치를 만드는 방법을 알아봅니다. 

**참고:** 이 데모에서는 서브넷이 하나 이상 있는 가상 네트워크가 필요합니다. 

**참조**: [빠른 시작: Azure Portal 사용하여 VM 부하를 분산하는 공용 부하 분산 장치 만들기](https://learn.microsoft.com/azure/load-balancer/quickstart-load-balancer-standard-public-portal)

**포털의 기능 선택 도움말 표시**

1. Azure Portal에 액세스합니다.

1. 부하 분산을 검색하여 선택합니다. **선택하세요**.

1. 마법사를 사용하여 다양한 시나리오를 연습합니다.
   
**부하 분산 장치 만들기**

1. Azure Portal 계속합니다.

1. **부하 분산** 장치를 검색하여 선택합니다. 부하 분산 장치를 **만듭니**다. 

1. **기본 사항** 탭에서 **SKU**, **유형** 및 계층에 대해 설명**합니다**.

1. **프런트 엔드 IP 구성** 탭에서 공용 IP 주소 사용에 대해 설명합니다.

1. **백 엔드 풀** 탭에서 IP 주소 범위가 있는 가상 네트워크를 선택합니다.

1. **인바운드 규칙 탭에서** 부하 분산 규칙을 만듭니다. **프로토콜**, **포트**, **상태 프로브** 및 **세션 지속성과** 같은 매개 변수에 대해 설명합니다. 


## Azure Application Gateway 구성

이 데모에서는 Azure Application Gateway 만드는 방법을 알아봅니다. 

**참고**: 간단하게 유지하려면 구성을 진행할 때 새 가상 네트워크 및 서브넷을 만듭니다. 

**참조**: [빠른 시작: Azure Application Gateway 사용하여 직접 웹 트래픽 - Azure Portal](https://learn.microsoft.com/azure/application-gateway/quick-create-portal)

**Azure Application Gateway 만들기**

1. Azure Portal에 액세스합니다.

1. **Azure Application Gateway** 검색하여 선택합니다.

1. 새 게이트웨이를 **만듭니**다.

1. **기본 사항** 탭에서 **계층**, **자동 크기 조정** 및 **인스턴스 수에** 대해 설명합니다.

1. **프런트 엔드** 탭에서 IP 주소 유형에 대해 설명합니다.

1. **백 엔드** 탭에서 빈 백 엔드 풀을 사용하는 시기를 설명합니다.

1. **구성** 탭에서 라우팅 규칙에 대해 설명합니다. 부하 분산 장치 규칙과 비교합니다.

1. 게이트웨이를 만든 후 백 엔드 대상을 추가하고 테스트할 것이라고 설명합니다. 
