---
demo:
  title: '데모 07: 관리 Azure Storage 등록'
  module: Administer Azure Storage
---


# 07 - Azure Storage 관리 등록

## 스토리지 계정 구성

이 데모에서는 스토리지 계정을 만듭니다.

**참조**: [스토리지 계정 만들기](https://docs.microsoft.com/azure/storage/common/storage-account-create?tabs=azure-portal)

1. Azure Portal 사용

1. 스토리지 계정의 용도를 검토합니다. 
   
1. 스토리지 계정을** 검색하고 선택합니다**. 
 
1. 기본 스토리지 계정을 만듭니다. 

    - 스토리지 계정 이름 지정에 대한 요구 사항과 Azure에서 고유한 이름을 지정해야 하는 필요성에 대해 설명합니다. 

    - 다양한 스토리지 종류를 검토합니다. 예를 들어 범용 v2입니다. 

    - 액세스 계층 선택을 검토합니다. 예를 들어 쿨 계층과 핫 계층이 있습니다. 

    - 다른 탭 및 설정은 다른 데모에서 다룹니다. 

1. 스토리지 계정을 만들고 리소스가 배포되기를 기다립니다. 


## Blob Storage 구성

이 데모에서는 Blob Storage를 살펴봅니다.

**참고:** 이러한 단계에는 스토리지 계정이 필요합니다.

**참조**: [빠른 시작: Blob 업로드, 다운로드 및 나열](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal)

1. Azure Portal에서 스토리지 계정으로 이동합니다.

1. Blob Storage의 용도를 검토합니다. 

1. Blob 컨테이너를 만듭니다. 컨테이너에 대한 액세스 수준을 검토합니다. 예를 들어 private(익명 액세스 없음)입니다. 

1. 컨테이너에 Blob을 업로드합니다. 시간이 지남에 따라 고급 설정을 검토합니다. 예를 들어 Blob 형식 및 Blob 크기입니다. 

## 스토리지 보안 구성

이 데모에서는 공유 액세스 서명을 만듭니다.

**참고:** 이 데모에는 Blob 컨테이너 및 업로드된 파일이 있는 스토리지 계정이 필요합니다.

**참조**: [스토리지 컨테이너에 대한 SAS 토큰 만들기](https://learn.microsoft.com/azure/applied-ai-services/form-recognizer/create-sas-tokens?source=recommendations&view=form-recog-3.0.0)

1. 보호하려는 Blob 또는 파일을 선택합니다. 

1. SAS(공유 액세스 서명)를 생성합니다. 사용 권한, 시작 및 만료 시간 및 허용되는 프로토콜을 검토합니다.

1. SAS URL을 사용하여 리소스가 표시되는지 확인합니다. 


## Azure Files 구성 

이 데모에서는 파일 공유 및 스냅샷 작업합니다.

**참고:** 이러한 단계에는 스토리지 계정이 필요합니다.

**참조**: [Azure 파일 공유를 관리하기 위한 빠른 시작](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-portal?tabs=azure-portal)

1. 파일 공유의 용도를 검토합니다. 

1. 스토리지 계정에 액세스하고 파일을 ** 클릭합니다**.

1. 파일 공유 만들기. 할당량을 검토하고, 파일을 업로드하고, 디렉터리를 추가하여 정보를 구성합니다. 

1. 파일 공유 스냅샷 만듭니다. 스냅샷 사용하는 시기와 백업과 다른 방법을 검토합니다. 시간이 지남에 따라 파일을 업로드하고, 스냅샷 수행하고, 파일을 삭제하고, 스냅샷 복원합니다.


## 스토리지 도구(선택 사항)

이 데모에서는 몇 가지 일반적인 Azure 스토리지 도구를 검토합니다. 

**참조**: [Storage Explorer 시작](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer?tabs=windows)

1. Storage Explorer를 설치하거나 스토리지 브라우저를 사용합니다.

1. 스토리지 리소스를 찾아보고 만드는 방법을 검토합니다. 예를 들어 Blob 컨테이너를 추가합니다. 

**참조**: [AzCopy v10을 사용하여 Azure Storage로 데이터 복사 또는 이동](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy-v10?toc=/azure/storage/files/toc.json)

1. AzCopy를 사용하는 시기를 설명합니다. 도움말, **azcopy /?** 를 확인합니다.

1. 샘플 ** 섹션을**아래로 스크롤합니다. 시간이 지남에 따라 예제를 시도해 보세요. 
    



