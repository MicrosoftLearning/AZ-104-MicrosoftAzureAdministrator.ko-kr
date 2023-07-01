---
demo:
  title: '데모 08: Azure Virtual Machines 관리'
  module: Administer Azure Virtual Machines
---


# 08 - Azure Virtual Machines 관리

## 데모 -- 포털에서 Virtual Machines 만들기

이 데모에서는 포털에서 Azure 가상 머신을 만들고 액세스합니다.

**참조**

[빠른 시작 - Azure Portal에서 Windows VM 만들기](https://docs.microsoft.com/azure/virtual-machines/windows/quick-create-portal)

[빠른 시작 - Azure Portal에서 Linux VM 만들기](https://docs.microsoft.com/azure/virtual-machines/linux/quick-create-portal)

[Bastion을 사용하여 가상 머신에 연결](https://learn.microsoft.com/azure/bastion/tutorial-create-host-portal#connect)

**가상 머신 만들기**

**참고:** 이러한 단계에서는 몇 가지 가상 머신 매개 변수만 다룹니다. 다른 영역도 살펴보고 다룹니다.  대상 그룹에 따라 Windows 또는 Linux 가상 머신을 만들 수 있습니다.

1. Azure 포털을 사용합니다.

1. **가상 머신**을 검색합니다. 

1. 기본 가상 머신을 만듭니다. 가용성 옵션, 이미지 및 인바운드 규칙을 검토합니다.

1. 보안 관리자 계정을 만드는 것의 중요성에 대해 설명합니다.

1. 가상 머신을 만들고 리소스가 배포되기를 기다립니다.  

**가상 머신에 연결**

1. 가상 머신에 **연결하는** 방법에는 여러 가지가 있습니다. 

1. Windows 서버의 경우 자습서와 같이 **RDP**를 사용할 수 있습니다. 웹 서버를 설치하고 IIS 시작 페이지를 확인하여 한 단계 더 나아갈 수 있습니다. 

1. Linux 서버의 경우 자습서와 같이 **SSH**를 수행할 수 있습니다. 웹 서버를 설치하고 작동 중인 웹 서버를 확인하여 한 단계 더 나아갈 수 있습니다.

1. 두 서버 모두 **Bastion** 서비스(자습서)에 연결할 수 있습니다. Bastion이 RDP 또는 SSH에 선호되는 이유를 검토합니다. 

## 가상 머신 가용성 구성

이 데모에서는 가상 머신 크기 조정 옵션에 대해 살펴보겠습니다.

**참조**

[Azure Portal을 사용하여 확장 집합에서 가상 머신 만들기](https://learn.microsoft.com/azure/virtual-machine-scale-sets/flexible-virtual-machine-scale-sets-portal)

1. Azure Portal을 사용합니다.

1. **Virtual Machine Scale Sets** 검색하여 선택합니다. 

1. **Virtual Machine Scale Sets** 만듭니다. 가상 머신 확장 집합의 용도를 검토합니다. **균일** 및 **유연한** 오케스트레이션 모드의 차이점을 검토합니다. 선택한 항목이 크기 조정 옵션에 영향을 줄 수 있다고 설명합니다. 

1.  **크기 조정** 탭으로 이동합니다. 

1.  **수동 크기 조정** 및 **스케일 인 정책이** 사용되는 방법을 검토합니다. 

1. **사용자 지정** 크기 조정 정책으로 변경합니다. 

1. 가상 머신 인스턴스에서 **CPU 임계값(%)** 을 사용하여 스케일 아웃하고 스케일링하는 방법을 검토합니다. 

