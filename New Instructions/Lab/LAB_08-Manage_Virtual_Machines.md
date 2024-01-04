---
lab:
  title: '랩 08: Virtual Machines 관리'
  module: Administer Virtual Machines
---

# 랩 08 - 가상 머신 관리

## 랩 소개

이 랩에서는 가상 머신의 수동 크기 조정과 가상 머신의 자동 크기 조정을 비교합니다. 단일 가상 머신을 구성하고 크기를 조정하는 방법을 알아봅니다. 가상 머신 확장 집합을 만들고 자동 크기 조정을 구성하는 방법을 알아봅니다.

이 랩에는 Azure 구독이 필요합니다. 구독 유형은 이 랩의 기능 가용성에 영향을 줄 수 있습니다. 지역을 변경할 수 있지만 단계는 미국 동부를 사용하여 작성됩니다.

## 예상 소요 시간: 50분

## 랩 시나리오

조직에서 Azure 가상 머신 배포 및 구성을 탐색하려고 합니다. 먼저 Azure 가상 머신을 사용할 경우 구현할 수 있는 다양한 컴퓨팅 및 스토리지 복원력과 확장성 옵션을 결정해야 합니다. 다음으로 Azure 가상 머신 확장 집합을 사용할 경우 사용할 수 있는 컴퓨팅 및 스토리지 복원력과 확장성 옵션을 조사해야 합니다.

## 대화형 랩 시뮬레이션

이 항목에 유용할 수 있는 대화형 랩 시뮬레이션이 있습니다. 시뮬레이션을 사용하면 비슷한 시나리오를 원하는 속도로 클릭할 수 있습니다. 대화형 시뮬레이션과 이 랩 사이에는 차이점이 있지만, 대부분의 핵심 개념은 동일합니다. Azure 구독은 필요하지 않습니다.

+ [포털](https://mslearn.cloudguides.com/en-us/guides/AZ-900%20Exam%20Guide%20-%20Azure%20Fundamentals%20Exercise%201)에서 가상 머신을 만듭니다. 가상 머신을 만들고, 연결하고, 웹 서버 역할을 설치합니다. 
+ [템플릿](https://mslearn.cloudguides.com/en-us/guides/AZ-900%20Exam%20Guide%20-%20Azure%20Fundamentals%20Exercise%209)을 사용하여 가상 머신을 배포합니다. 빠른 시작 갤러리를 탐색하고 가상 머신 템플릿을 찾습니다. 템플릿을 배포하고 배포를 확인합니다.
+ [PowerShell](https://mslearn.cloudguides.com/en-us/guides/AZ-900%20Exam%20Guide%20-%20Azure%20Fundamentals%20Exercise%2010)을 사용하여 가상 머신을 만듭니다. Azure PowerShell을 사용하여 가상 머신을 배포합니다. Azure Advisor 권장 사항을 검토합니다. 
+ [CLI](https://mslearn.cloudguides.com/en-us/guides/AZ-900%20Exam%20Guide%20-%20Azure%20Fundamentals%20Exercise%2011)를 사용하여 가상 머신을 만듭니다. CLI를 사용하여 가상 머신을 배포합니다. Azure Advisor 권장 사항을 검토합니다. 

## 작업

+ 작업 1: Azure Portal을 사용하여 영역 복원력 있는 Azure 가상 머신 배포
+ 작업 2: 가상 머신에 대한 컴퓨팅 및 스토리지 크기 조정 관리
+ 작업 3: Azure Virtual Machine Scale Sets 구현
+ 작업 4: Azure Virtual Machine Scale Sets 크기 조정
+ 작업 5: Azure PowerShell을 사용하여 가상 머신 만들기(옵션 1)
+ 작업 6: CLI를 사용하여 가상 머신 만들기(옵션 2) 




## 작업 1 및 2: Azure Virtual Machines 아키텍처 다이어그램

![아키텍처 작업의 다이어그램.](../media/az104-lab08a-architecture-diagram.png)

## 작업 1: Azure Portal을 사용하여 영역 복원력 있는 Azure 가상 머신 배포

이 작업에서는 Azure Portal을 사용하여 두 개의 Azure 가상 머신을 다른 가용성 영역에 배포합니다. 가용성 영역은 99.99%의 가상 머신에 대해 가장 높은 수준의 작동 시간 SLA를 제공합니다. 이 SLA를 달성하려면 서로 다른 가용성 영역에 두 개 이상의 가상 머신을 배포해야 합니다.

1. Azure Portal에 로그인 - `https://portal.azure.com`.

1. 가상 머신** 블레이드에서 **+ 만들기**를 검색**하여 선택한 `Virtual machines` 다음 드롭다운 **+ Azure 가상 머신**에서 선택합니다.

1. **가상 머신** 만들기 블레이드의 **기본 사항** 탭에 있는 **가용성 영역** 드롭다운 메뉴에서 영역 2** 옆에 검사 표시를 **배치합니다. 영역 1**과 **영역 2**를 모두 **선택해야 합니다.

    >**참고**: 선택한 지역에 각각 하나씩 두 개의 가상 머신을 배포합니다. 두 개 이상의 영역에 둘 이상의 VM이 분산되어 있으므로 99.99% 작동 시간 SLA를 달성합니다. VM이 하나만 필요할 수 있는 시나리오에서는 디스크와 해당 리소스가 동일한 영역에 있는지 확인하기 위해 VM을 영역에 계속 배포하는 것이 가장 좋습니다.

1. 기본 사항 탭에서 다음 설정을 사용하여 필드를 완료합니다(다른 사용자는 기본값으로 유지).

    | 설정 | 값 |
    | --- | --- |
    | 구독 | Azure 구독의 이름 |
    | Resource group |  **az104-rg8**(필요한 경우 새로** 만들기 클릭**) |
    | 가상 머신 이름 | `az104-vm1`및 `az104-vm2` (두 가용성 영역을 모두 선택한 후 VM 이름 필드 아래에서 이름** 편집을 선택합니다**.) |
    | 지역 | **미국 동부** |
    | 가용성 옵션 | **가용성 영역** |
    | 가용성 영역 | **영역 1, 2** (가상 머신 확장 집합 사용에 대한 참고 사항 읽기) |
    | 보안 유형 | **Standard** |
    | 이미지 | **Ubuntu Server 20.04 LTS - x64 Gen2** |
    | Azure Spot 인스턴스 | **unchecked** |
    | 크기 | **표준 D2s v3** |
    | 인증 유형 | **암호** |
    | 사용자 이름 | `localadmin` |
    | 암호 | **보안 암호 제공** |
    | 공용 인바운드 포트 | **없음** |
    | 기존 Windows Server 라이선스를 사용하시겠습니까? | **선택 취소** |

    ![vm 만들기 페이지의 스크린샷.](../media/az104-lab08-create-vm.png)

1. **다음: 디스크 >** 를 클릭하고 **가상 머신 만들기** 블레이드의 **디스크** 탭에서 다음 설정을 지정합니다(다른 설정은 기본값으로 유지).

    | 설정 | 값 |
    | --- | --- |
    | OS 디스크 유형 | **프리미엄 SSD** |
    | Ultra Disk 호환성 사용 | **선택 취소** |

1. 다음을 클릭합니다 **. 네트워킹 >** 기본값을 사용하지만 부하 분산 장치를 제공하지 않습니다. 
   
    | 부하 분산 옵션 | **없음** |
    
1. **다음: 관리 >** 를 클릭하고 **가상 머신 만들기** 블레이드의 **관리** 탭에서 다음 설정을 지정합니다(다른 설정은 기본값으로 유지).

    | 설정 | 값 |
    | --- | --- |
    | 패치 오케스트레이션 옵션 | **Azure 오케스트레이션됨** |  

1. **다음: 모니터링 >** 을 클릭하고, **가상 머신 만들기** 블레이드의 **모니터링** 탭에서 다음 설정을 지정합니다(다른 설정은 기본값으로 유지).

    | 설정 | 값 |
    | --- | --- |
    | 부트 진단 | 사용 안 함 |

1. **다음: 고급 >** 을 클릭하고, **가상 머신 만들기** 블레이드의 **고급** 탭에서 아무것도 수정하지 말고 사용 가능한 설정을 검토하고, **검토 + 만들기**를 클릭합니다.

1. **검토 + 만들기** 블레이드에서 **만들기**를 클릭합니다.

    >**참고:** 알림** 메시지를 모니터링하고 **배포가 완료되기를 기다립니다. 

## 작업 2: 가상 머신에 대한 컴퓨팅 및 스토리지 크기 조정 관리

이 작업에서는 가상 머신의 크기를 다른 SKU로 조정하여 가상 머신의 컴퓨팅 크기를 조정합니다. Azure는 할당된 더 많은(또는 더 적은) 컴퓨팅 및 메모리가 필요한 경우 일정 기간 동안 VM을 조정할 수 있도록 VM 크기 선택에서 유연성을 제공합니다. 이 개념은 디스크로 확장되어 디스크의 성능을 수정하거나 할당된 용량을 늘릴 수 있습니다.

1. Azure Portal에서 az104-vm1**을 검색하여 선택합니다**.

1. **az104-vm1** 가상 머신 블레이드에서 크기를** 클릭하고 **가상 머신 크기를 **DS1_v2** 설정하고 크기 조정을 클릭합니다 **.**

    >**참고**: **표준 DS1_v2**를 사용할 수 없는 경우 다른 크기를 선택합니다.

    ![가상 머신의 크기 조정 스크린샷.](../media/az104-lab08-resize-vm.png)

1. **az104-vm1** 가상 머신 블레이드에서 디스크**를 클릭하고 **데이터 디스크**에서 **+ 만들기를 클릭하고 **새 디스크**를 연결합니다.

1. 다음 설정을 사용하여 관리 디스크를 만듭니다(다른 설정은 기본값으로 유지).

    | 설정 | 값 |
    | --- | --- |
    | 디스크 이름 | `vm1-disk1` |
    | 스토리지 유형 | **표준 HDD** |
    | 크기(GiB) | `32` |

1. **적용**을 클릭합니다.

1. 디스크를 만든 후 분리를 클릭한 **다음 적용**을 클릭합니다**.**
    
    >**참고**: 분리* 아이콘을 보려면 *오른쪽으로 스크롤해야 할 수 있습니다.

1. Azure Portal에서 검색하여 선택합니다 `Disks`.

1. 디스크 목록에서 vm1-disk1** 개체를 **선택합니다.

1. vm1-disk1에서 크기 + 성능을** 선택합니다**.

1. 크기 + 성능에서 스토리지 유형을 표준 SSD로 **설정한 다음 저장**을 클릭합니다**.**

    >**참고**: 디스크가 연결된 동안 또는 VM이 실행되는 동안에는 디스크의 스토리지 유형을 변경할 수 없습니다. 

1. az104-vm1 가상 머신으로 다시 **이동하여 디스크를** 선택합니다**.**

1. 이제 **디스크가 표준 HDD**인지 확인합니다.

## 작업 3 및 4: Azure Virtual Machine Scale Sets 아키텍처 다이어그램

![아키텍처 작업의 다이어그램.](../media/az104-lab08b-architecture-diagram.png)

## 작업 3: Azure Virtual Machine Scale Sets 구현

이 작업에서는 가용성 영역에 Azure 가상 머신 확장 집합을 배포합니다. 개별 VM을 사용하면 애플리케이션에 추가 컴퓨팅이 필요한 경우 추가 VM을 배포하고 구성하기 위해 다른 자동화가 필요합니다. VM Scale Sets는 확장 집합이 집합의 VM 수를 자동으로 확장하거나 축소할 수 있도록 하는 메트릭 또는 조건을 구성할 수 있도록 하여 자동화의 관리 오버헤드를 줄입니다.

1. Azure Portal에서 가상 머신 확장 집합** 블레이드를 검색하여 **선택하고 `Virtual machine scale sets` + 만들기**를 클릭합니다**.

1. **가상 머신 확장 집합** 만들기 블레이드의 **기본 사항** 탭에서 다음 설정을 지정하고(다른 설정을 기본값으로 유지) 다음: 스폿 >** 클릭합니다**.

    | 설정 | 값 |
    | --- | --- |
    | 구독 | Azure 구독의 이름  |
    | Resource group | **az104-rg8**  |
    | 가상 머신 확장 집합 이름 | `vmss1` |
    | 지역 | **미국** 동부(또는 가까운 지역) |
    | 가용성 영역 | **영역 1, 2, 3** |
    | 오케스트레이션 모드 | **Uniform** |
    | 보안 유형 | **Standard** | 
    | 이미지 | **Windows Server 2019 Datacenter - x64 Gen2** |
    | Azure Spot 할인으로 실행 | **선택 취소** |
    | 크기 | **표준 D2s_v3** |
    | 사용자 이름 | `localadmin` |
    | 암호 | **보안 암호 제공**  |
    | 이미 Windows Server 라이선스가 있나요? | **선택 취소** |

    >**참고**: Windows Virtual Machines를 가용성 영역에 배포하는 것을 지원하는 Azure 영역 목록은 [Azure의 가용성 영역이란 무엇인가요?](https://docs.microsoft.com/en-us/azure/availability-zones/az-overview)를 참조하세요.

    ![vmss 만들기 페이지의 스크린샷 ](../media/az104-lab08-create-vmss.png)

1. 스폿** 탭에서 **기본값을 적용하고 다음: 디스크 >** 선택합니다**.

1. 디스크** 탭에서 **기본값을 적용하고 다음 : 네트워킹 >** 클릭합니다**.

1. 네트워킹 탭에서 **가상** 네트워크 텍스트 상자 아래의 **** 가상 네트워크** 만들기 링크를 클릭하고 다음 설정을 사용하여 새 가상 네트워크를 만듭니다(다른 사용자는 기본값을 그대로 둡니다).**  완료되면 확인을** 선택합니다**. 

    | 설정 | 값 |
    | --- | --- |
    | 속성 | `vmss-vnet` |
    | 주소 범위 | `10.82.0.0/20` |
    | 서브넷 이름 | `subnet0` |
    | 서브넷 범위 | `10.82.0.0/24` |

1. 네트워킹 탭에서 **네트워크 인터페이스 항목 오른쪽에 있는 네트워크 인터페이스** 편집 아이콘을 클릭합니다**.**

1. **NIC 네트워크 보안 그룹** 섹션의 **네트워크 인터페이스 편집** 블레이드에서 **고급**을 클릭하고 **네트워크 보안 그룹 구성** 드롭다운 목록에서 **새로 만들기**를 클릭합니다.

1. **네트워크 보안 그룹 만들기** 블레이드에서 다음 설정을 지정합니다(다른 설정은 기본값으로 유지).

    | 설정 | 값 |
    | --- | --- |
    | 속성 | **vmss1-nsg** |

1. **인바운드 규칙 추가**를 클릭하고 다음 설정으로 인바운드 보안 규칙을 추가합니다(나머지는 기본값으로 유지).

    | 설정 | 값 |
    | --- | --- |
    | 원본 | **임의** |
    | 원본 포트 범위 | * |
    | 대상 | **임의** |
    | 서비스 | **HTTP** |
    | 작업 | **허용** |
    | 우선 순위 | **1010** |
    | 이름 | `allow-http` |

1. **추가**를 클릭하고 **네트워크 보안 그룹 만들기** 블레이드로 돌아와서 **확인**을 클릭합니다.

1. 네트워크 인터페이스 편집 블레이드의 ****공용 IP 주소** 섹션에서 [사용 **]을 클릭하고 **[확인]**을 클릭합니다**.**

1. 네트워킹** 탭**의 **부하 분산** 섹션에서 다음을 지정합니다(다른 사용자는 기본값을 그대로 둡니다).

    | 설정 | 값 |
    | --- | --- |
    | 부하 분산 옵션 | **Azure Load Balancer** |
    | 부하 분산 장치 선택 | **부하 분산 장치 만들기** |
    
1.  **부하 분산 장치 만들기** 페이지에서 부하 분산 장치 이름을 지정하고 기본값을 사용합니다. 완료되면 **만들기**를 클릭한 후, **다음 : 스케일링 >** 을 클릭합니다.
    
    | 설정 | 값 |
    | --- | --- |
    | 부하 분산 장치 이름 | `vmss-lb` |

1. 크기 조정 탭에서 **다음 설정을 지정하고(다른 설정을 기본값으로 유지) 다음을 클릭합니다 **. 관리 >**.**

    | 설정 | 값 |
    | --- | --- |
    | 초기 인스턴스 수 | `2` |
    | 크기 조정 정책 | **수동** |

1. 관리** 탭에서 **다음 설정을 지정합니다(다른 설정은 기본값으로 유지).

    | 설정 | 값 |
    | --- | --- |
    | 부트 진단 | 사용 안 함 |
    
1. **다음: 상태 >** 를 클릭합니다.

1. 상태** 탭에서 **변경하지 않고 기본 설정을 검토하고 다음 : 고급 >** 클릭합니다**.

1. 고급 탭에서 **검토 + 만들기**를 클릭합니다**.**

1. 검토 + 만들기 탭에서 **유효성 검사가 통과되었는지 확인하고 만들기**를 클릭합니다**.**

    >**참고**: 가상 머신 확장 집합 배포가 완료될 때까지 기다립니다. 이 작업은 약 5분 정도 걸립니다.


## 작업 4: Azure Virtual Machine Scale Sets 크기 조정

이 작업에서는 사용자 지정 크기 조정 규칙을 사용하여 가상 머신 확장 집합의 크기를 조정합니다.

1. **리소스**로 이동 또는 검색을 선택하고 vmss1** 확장 집합을 선택합니다**.

1. 확장 집합 창의 왼쪽 메뉴에서 크기 조정**을 선택합니다**.

1. 크기 조정 모드는 **메트릭**에 따라 크기 조정 또는 **특정 인스턴스 수**로 크기 조정이 될 **수** 있습니다. VM 인스턴스 수가 적은 확장 집합에서는 인스턴스 수를 늘리거나 줄이는 것이 가장 좋습니다. VM 인스턴스 수가 많은 확장 집합에서는 메트릭을 기반으로 크기를 조정하는 것이 더 적합할 수 있습니다.

1. 사용자 지정 자동 크기 조정**에 대한 **단추를 선택합니다. 그런 다음 **규칙 추가**를 선택합니다. 

### 규모 확장 규칙

1. VM 인스턴스 수를 자동으로 늘리는 스케일 아웃 규칙을 만들어 보겠습니다. 이 규칙은 평균 CPU 로드가 10분 동안 70% 이상일 때 확장됩니다. 규칙이 트리거되면 VM 인스턴스 수가 20% 증가합니다. 선택한 후 추가**를 클릭합니다**. 

    | 설정 | 값 |
    | --- | --- |
    | 메트릭 원본 | **현재 리소스(vmss1)** |
    | 메트릭 네임스페이스 | **가상 머신 호스트** |
    | 메트릭 이름 | **CPU** 백분율(다른 선택 항목 검토) |
    | 연산자 | **보다 큼** |
    | 크기 조정 작업을 트리거하는 메트릭 임계값 | **70** |
    | 기간(분) | **10** |
    | 시간 조직 통계 | **평균** |
    | 연산 | **백분율 증가** (다른 선택 사항 검토) |
    | 정지 시간(분) | **5** |
    | 백분율 | **20** |
    
    ![크기 조정 규칙 추가 페이지의 스크린샷.](../media/az104-lab08-scale-rule.png)

### 규칙 크기 조정

1. 저녁이나 주말에는 수요가 감소할 수 있으므로 규칙의 규모를 만드는 것이 중요합니다.

1. 확장 집합의 VM 인스턴스 수를 줄이는 규칙을 만들어 보겠습니다. 평균 CPU 부하가 10분 동안 30% 미만으로 떨어지면 인스턴스 수가 감소해야 합니다. 규칙이 트리거되면 VM 인스턴스 수가 20% 감소합니다. 설정을 조정한 다음 추가**를 선택합니다**.

    | 설정 | 값 |
    | --- | --- |
    | 연산자 | **보다 작음** |
    | 임계값 | **30** |
    | 연산 | **백분율** 감소 기준(다른 선택 사항 검토) |
    | 인스턴트 수 | **20** |

### 인스턴스 제한 설정

1. 자동 크기 조정 규칙이 적용되면 인스턴스 제한은 최대 인스턴스 수를 초과하여 확장하거나 최소 인스턴스 수를 초과하여 스케일 인하지 않도록 합니다.

1. **인스턴스 제한은** 규칙 뒤의 **크기 조정** 페이지에 표시됩니다. 

    | 설정 | 값 |
    | --- | --- |
    | 최소 | **2** |
    | 최대 | **10** |
    | 기본값 | **2** |

1. 변경 내용을 저장**해야 **합니다.

1. **vmss1** 페이지에서 인스턴스를** 선택합니다**. 가상 머신 인스턴스 수를 모니터링하는 위치입니다. 

## 작업 5: Azure PowerShell을 사용하여 가상 머신 만들기(옵션 1)

1. Azure Portal에 로그인 - `https://portal.azure.com`.

1. 메뉴를 사용하여 Cloud Shell** 세션을 시작**합니다. 또는 .`https://shell.azure.com`

1. 필요한 경우 Cloud Shell을 구성합니다. PowerShell**을 선택**해야 합니다.

1. 다음 명령을 실행하여 가상 머신을 만듭니다. 메시지가 표시되면 VM에 대한 사용자 이름과 암호를 제공합니다. 대기하는 동안 가상 머신 만들기와 관련된 모든 매개 변수에 대해 New-AzVM[ 명령 참조를 검사](https://learn.microsoft.com/powershell/module/az.compute/new-azvm?view=azps-11.1.0).

    ```powershell
    New-AzVm `
    -ResourceGroupName 'az104-rg8' `
    -Name 'myPSVM' `
    -Location 'East US' `
    -Image 'Win2019Datacenter' `
    -Zone '1' `
    -Size 'Standard_D2s_v3' 
    -Credential '(Get-Credential)' `

1. Once the command completes, use **Get-AzVM** to list the virtual machines in your resource group. 

    ```powershell
    Get-AzVM `
    -ResourceGroupName 'az104-rg8'
    -Status

1. Verify your new virtual machine is listed and the **Status** is **Running**.

1. Use **Stop-AzVM** to deallocate your virtual machine. Type **Yes** to confirm. 

    ```
    Stop-AzVM `
    -ResourceGroupName 'az104-rg8'
    -Name 'myPSVM' `

1. -Status** 매개 변수와 함께 **Get-AzVM**을 사용하여 **컴퓨터**의 할당이 취소되었는지 확인합니다**.

    >**알고 계셨나요?** Azure를 사용하여 가상 머신을 중지하면 상태 *할당이 취소됩니다*. 즉, 비정적 공용 IP가 해제되고 VM의 컴퓨팅 비용 지불이 중지됩니다.

## 작업 6: CLI를 사용하여 가상 머신 만들기(옵션 2)

1. Azure Portal에 로그인 - `https://portal.azure.com`.

1. 메뉴를 사용하여 Cloud Shell** 세션을 시작**합니다. 또는 .`https://shell.azure.com`

1. 필요한 경우 Cloud Shell을 구성합니다. Bash**를 선택**해야 합니다.

1. 다음 명령을 실행하여 가상 머신을 만듭니다. 메시지가 표시되면 VM에 대한 사용자 이름과 암호를 제공합니다. 대기하는 동안 검사 [가상 머신 만들기와 관련된 모든 매개 변수에 대한 az vm create 명령 참조를 만듭니](https://learn.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-create)다.


    ```sh
    az vm create --name myCLIVM --resource-group az104-rg8 --image Ubuntu2204 --admin-username localadmin --generate-ssh-keys 
    
1. Once the command completes, use **az vm show** to verify your machine was created.

    ```sh
    az vm show --name  myCLIVM --resource-group az104-rg8 --show-details

1. Verify the **powerState** is **VM Running**.

1. Use **az vm deallocate** to deallocate your virtual machine. Type **Yes** to confirm. 

    ```sh
    az vm deallocate --resource-group az104-rg8 --name myCLIVM

1. Use **az vm show** to ensure the **powerState** is **VM deallocated**.

    >**Did you know?** When you use Azure to stop your virtual machine, the status is *deallocated*. This means that any non-static public IPs are released, and you stop paying for the VM’s compute costs.

## Key takeaways

Congratulations on completing the lab. Here are the main takeaways for this lab. 

+ Azure virtual machines are on-demand, scalable computing resources.
+ Configuring Azure virtual machines includes choosing an operating system, size, storage and networking settings. 
+ Azure Virtual Machine Scale Sets let you create and manage a group of load balanced VMs.
+ The virtual machines in a Virtual Machine Scale Set are created from the same image and configuration. 
+ In a Virtual Machine Scale Set the number of VM instances can automatically increase or decrease in response to demand or a defined schedule.

## Cleanup your resources

If you are working with your own subscription take a minute to delete the lab resources. This will ensure resources are freed up and cost is minimized. The easiest way to delete the lab resources is to delete the lab resource group. 

+ In the Azure portal, select the resource group, select **Delete the resource group**, **Enter resource group name**, and then click **Delete**.

+ Using Azure PowerShell, `Remove-AzResourceGroup -Name resourceGroupName`.

+ Using the CLI, `az group delete --name resourceGroupName`.


