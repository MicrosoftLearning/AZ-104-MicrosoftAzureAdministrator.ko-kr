---
demo:
  title: '데모 04: 가상 네트워킹 관리'
  module: Administer Virtual Networking
---

# 04 - 가상 네트워킹 관리

## Virtual Networks 구성

본 데모에서는 가상 네트워크를 만듭니다.

**참조**: [빠른 시작: 가상 네트워크 만들기 - Azure Portalk](https://docs.microsoft.com/azure/virtual-network/quick-create-portal)

## 포털에서 가상 네트워크 만들기

1.  Azure Portal 로그인하고 **Virtual Network**를 검색합니다.

1.  진행 중인 기본 설정을 설명하는 가상 네트워크를 만듭니다. 하나 이상의 서브넷이 생성되었는지 확인합니다. 

1.  가상 네트워크가 생성되었는지 확인합니다.

## 네트워크 보안 그룹 구성

이 데모에서는 NSG 및 서비스 엔드포인트를 살펴봅니다.

**참조**: [PaaS 리소스에 대한 액세스 제한 - 자습서 - Azure Portal](https://docs.microsoft.com/azure/virtual-network/tutorial-restrict-network-access-to-resources)

**네트워크 보안 그룹 만들기**

1. Azure Portal에 액세스합니다.

1.  **네트워크 보안 그룹을** 검색하여 선택합니다.

1. 이동하는 동안 설정을 설명하는 NSG를 만듭니다. 
 
1. 새 NSG가 배포될 때까지 기다립니다.

**인바운드 및 아웃바운드 규칙 살펴보기**

1. 새 NSG를 선택합니다.

1. NSG를 서브넷 또는 네트워크 인터페이스와 연결할 수 있는 방법을 설명합니다.

1. 인바운드 및 아웃바운드 규칙의 목적에 대해 설명합니다.  

1. 기본 인바운드 및 아웃바운드 규칙을 검토합니다. 

1. 진행 중인 설정을 설명하는 새 규칙을 만듭니다. 특히 서비스 선택(예: HTTPS) 및 우선 순위 설정에 대해 설명합니다. 

## Azure DNS 구성

본 데모에서는 Azure DNS에 대해 살펴봅니다.

**참조**: [자습서: 도메인 및 하위 도메인 호스트 - Azure DNS](https://docs.microsoft.com/azure/dns/dns-delegate-domain-azure-dns)


**DNS 영역 만들기**

1. Azure Portal에 액세스합니다.

1.  **DNS 영역**서비스를 검색합니다 .

1. **DNS 영역을 만들고 영역**의 용도를 설명합니다. 이름의 경우 contoso.internal.com 사용할 수 있습니다.

1.  DNS 영역이 만들어질 때까지 기다립니다. 페이지를 **새로 고쳐** 야 할 수도 있습니다.

**DNS 레코드 집합 추가**

**참조**: [자습서: 영역 리소스 레코드를 참조하는 별칭 레코드 만들기](https://learn.microsoft.com/azure/dns/tutorial-alias-rr)

1. 영역이 만들어지면 **+레코드 집합을** 선택합니다.

1.  **형식** 드롭다운을 사용하여 다양한 유형의 레코드를 볼 수 있습니다. 다양한 레코드 형식을 사용하는 방법을 검토합니다. 다른 레코드 유형을 선택하면 레코드 정보가 어떻게 변경되는지 확인합니다.

1. **A** 레코드를 예로 만듭니다. 

