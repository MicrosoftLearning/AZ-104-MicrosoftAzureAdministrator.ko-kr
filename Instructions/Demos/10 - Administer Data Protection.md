---
demo:
  title: '데모 10: 관리데이터 보호 등록'
  module: Administer Data Protection
---

# 10 - 데이터 보호 관리

## Azure 파일 공유 백업

이 데모에서는 Azure Portal에서 파일 공유 백업을 살펴봅니다.

> **참고:** 이 데모에서는 파일 공유가 있는 스토리지 계정이 필요합니다. 

**참조**: [Azure Portal에서 Azure 파일 공유 백업](https://docs.microsoft.com/azure/backup/backup-afs)

**Recovery Services 자격 증명 모음 만들기**

1. Azure Portal 사용

1. 선택한 **Recovery Services 자격 증명 모음을 검색합니다**.

1. **Recovery Services 자격 증명 모음을 만듭니다**. 자격 증명 모음이 파일 공유와 동일한 지역에 있어야 한다는 요구 사항을 검토합니다. 

1. 자격 증명 모음이 만들어질 때까지 기다립니다. 

**Azure 파일 백업 구성**

1. Backup 센터로** 이동하여 **새 **Backup** 인스턴스를 만듭니다.

1. 데이터 원본 유형** 드롭다운에서 **선택 항목을 검토하고 논의합니다. Azure 파일(Azure Storage)**을 선택합니다**. 

1. 자격 증명 모음**을 **선택합니다.

1. **백업 구성을 계속** 합니다. 백업하려는 특정 스토리지 계정 및 파일 공유를 선택합니다.  

1. **정책 세부 정보**에서 이 정책** 편집을 클릭합니다**. 백업 정책의 용도에 대해 설명합니다. **백업 일정** 및 **보존 범위를 검토합니다**.  

1. **백업** 을 사용하여 변경 내용을 저장합니다. 

1. 시간이 지남에 따라 Backup 인스턴스**를 복원 **** 하는 **방법을 검토합니다. 또한 백업 작업을** 모니터링**하는 방법도 있습니다. 

## Azure Virtual Machines 백업

이 데모에서는 Recovery Services 자격 증명 모음에 가상 머신의 일일 백업을 예약합니다.

> **참고:** 이 데모에는 가상 머신 및 Recovery Services 자격 증명 모음이 필요합니다.

**참조**: [자습서 - 여러 Azure 가상 머신 백업](https://docs.microsoft.com/azure/backup/tutorial-backup-vm-at-scale)

1. Azure Portal 사용

1. Backup 센터로** 이동하여 **새 **Backup** 인스턴스를 만듭니다.

1. **Azure Virtual Machines**를 **데이터 원본 유형**으로 선택하고 자격 증명 모음을 선택합니다.

1. DefaultPolicy를 **검토합니다**. 기본 정책은 하루에 한 번 가상 머신을 백업합니다. 매일 백업은 30일 동안 보존됩니다. 즉시 복구 스냅샷 2일 동안 유지됩니다.

1. 백업**을 사용하도록 **설정하여 구성을 저장합니다.

1. 시간이 지남에 따라 지금** 백업하는 **방법을 검토합니다. 또한 백업 작업을** 검토**하는 방법도 있습니다.  

