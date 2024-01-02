---
lab:
  title: '랩 01: Microsoft Entra ID ID 관리'
  module: Administer Identity
---

# 랩 01 - Microsoft Entra ID ID 관리

## 랩 소개

이는 Azure 관리istrators에 대한 일련의 랩 중 첫 번째입니다. 이 랩에서는 사용자 및 그룹에 대해 알아봅니다. 사용자 및 그룹은 ID 솔루션의 기본 구성 요소입니다. 기본 관리자 도구에 대해서도 잘 알고 있습니다. 

이 랩에는 Azure 구독이 필요합니다. 구독 유형은 이 랩의 기능 가용성에 영향을 줄 수 있습니다. 지역을 변경할 수 있지만 단계는 미국 동부에 표시됩니다.

## 예상 소요 시간: 40분

## 랩 시나리오

조직에서 앱 및 서비스의 사전 프로덕션 테스트를 위한 새로운 랩 환경을 구축하고 있습니다.  가상 머신을 포함하여 랩 환경을 관리하기 위해 몇 명의 엔지니어가 고용되고 있습니다. 엔지니어가 Microsoft Entra ID를 사용하여 인증할 수 있도록 사용자 및 그룹 계정을 프로비전해야 합니다. 관리 오버헤드를 최소화하려면 직위를 기준으로 그룹의 멤버 자격을 자동으로 업데이트해야 합니다. 또한 엔지니어가 조직을 떠난 후 액세스를 방지하기 위해 사용자를 삭제하는 방법도 알아야 합니다.

## 대화형 랩 시뮬레이션

이 항목에 유용할 수 있는 대화형 랩 시뮬레이션이 있습니다. 시뮬레이션을 사용하면 비슷한 시나리오를 원하는 속도로 클릭할 수 있습니다. 대화형 시뮬레이션과 이 랩 사이에는 차이점이 있지만, 대부분의 핵심 개념은 동일합니다. Azure 구독은 필요하지 않습니다. 

+ [Entra ID ID를 관리합니다](https://mslabs.cloudguides.com/guides/AZ-104%20Exam%20Guide%20-%20Microsoft%20Azure%20Administrator%20Exercise%201). 사용자를 만들고 구성하고 그룹에 할당합니다. Azure 테넌트를 만들고 게스트 계정을 관리합니다. 

## 아키텍처 다이어그램
![랩 01 아키텍처의 다이어그램.](../media/az104-lab01-user-and-groups2.png)

## 작업

+ 작업 1: 리소스 그룹을 만듭니다.
+ 작업 2: 사용자 계정을 만들고 구성합니다.
+ 작업 3: 그룹을 만들고 구성원을 추가합니다.
+ 작업 4: Cloud Shell을 숙지합니다.
+ 작업 5: Azure PowerShell을 사용하여 연습합니다.
+ 작업 6: Bash 셸을 사용하여 연습합니다.

## 작업 1: 리소스 그룹 만들기

이 작업에서는 리소스 그룹을 만듭니다. 리소스 그룹은 관련 리소스의 그룹화입니다. 예를 들어 프로젝트, 부서 또는 애플리케이션에 대한 모든 리소스입니다. 

>**참고:** 이 과정의 각 랩에 대해 새 리소스 그룹을 만듭니다. 이렇게 하면 랩 리소스를 빠르게 찾고 관리할 수 있습니다. 

1. **Azure Portal** - `https://portal.azure.com`에 로그인합니다.

    >**참고:** Azure Portal은 모든 랩에서 사용됩니다. Azure를 새로 사용하는 경우 맨 위 검색 상자에 입력 `Quickstart Center` 합니다. 그런 다음 몇 분 후에 Azure Portal** 비디오에서 시작하기를 시청**합니다. 이전에 포털을 사용한 적이 있더라도 내부 탐색 및 사용자 지정에 대한 몇 가지 팁과 요령을 찾을 수 있습니다. 
   
1. Azure Portal에서 검색하여 선택합니다 `Resource groups`.
   
1. 리소스 그룹** 블레이드에서 **+ 만들기**를 클릭하고 **필요한 정보를 제공합니다. 

    | 설정 | 값 |
    | --- | --- |
    | 구독 이름 | 구독 |
    | 리소스 그룹 이름 | `az104-rg1` |
    | 위치 | **미국 동부** |

    >**참고:** 모든 랩은 미국** 동부를 사용합니다**. **빠른 시작 센터에서** 최상의 지역 선택 비디오를 **시청하여 지역을** 선택할 때 고려해야 할 사항을 알아봅니다.  
    
1. **검토 + 만들기**를 클릭한 다음, **만들기**를 클릭합니다.

    >**참고**: 리소스 그룹이 배포될 때까지 기다립니다. **알림** 아이콘(오른쪽 위)을 사용하여 배포 진행률을 추적합니다.

1. 리소스**로 이동을 선택하고 **페이지를 새로 고치고 리소스 그룹 목록에 새 리소스 그룹이 표시되는지 확인합니다.

    ![리소스 그룹 목록의 스크린샷](../media/az104-lab01-create-resource-group.png)

## 작업 2: 사용자 계정 만들기 및 구성

이 작업에서는 사용자 계정을 만들고 구성합니다. 사용자 계정은 이름, 부서, 위치 및 연락처 정보와 같은 사용자 데이터를 저장합니다.

1. Azure Portal에서 계속합니다. 

1. `Microsoft Entra ID`을 검색하고 선택합니다.

1. Microsoft Entra ID 블레이드에서 관리** 섹션까지 아래로 스크롤하여 **사용자 설정을** 클릭하고 **사용 가능한 구성 옵션을 검토합니다.

1. **사용자 - 모든 사용자** 블레이드로 다시 이동한 다음 **+ 새 사용자**를 선택하세요.

1. 다음 설정을 사용하여 새 사용자를 만듭니다(다른 사용자는 기본값을 그대로 둡니다). 사용자 계정에 포함할 수 있는 다양한 유형의 데이터를 확인합니다. 

    | 설정 | 값 |
    | --- | --- |
    | 사용자 계정 이름 | `az104-user1` |
    | 표시 이름 | `az104-user1` |
    | 암호 자동 생성 | 선택 해제 |
    | 초기 암호 | **보안 암호 제공** |
    | 직호(속성 탭) | `Cloud Administrator` |
    | 부서(속성 탭) | `IT` |
    | 사용 위치(속성 탭) | **미국** |

### 작업 4: 그룹 만들기 및 구성원 추가

이 작업에서는 그룹을 만듭니다. 그룹은 사용자 계정 또는 디바이스에 사용됩니다. 일부 그룹에는 정적으로 할당된 멤버가 있습니다. 일부 그룹에는 동적으로 할당된 멤버가 있습니다. 동적 그룹은 사용자 계정 또는 디바이스의 속성에 따라 자동으로 업데이트됩니다. 정적 그룹에는 더 많은 관리 오버헤드가 필요합니다(관리자는 구성원을 수동으로 추가 및 제거해야 합니다).

1. Azure Portal에서 검색하여 선택합니다 `Groups`.

1. 멤버 자격 유형, **원본 및 형식**과 **같은 **그룹 정보를 확인합니다****. 또한 그룹의 멤버 수도 확인합니다. 

1. + 새 그룹을** 선택하고 **새 그룹을 만듭니다. 

    | 설정 | 값 |
    | --- | --- |
    | 그룹 형식 | **보안** |
    | 그룹 이름 | `IT Lab Administrators` (이 이름을 사용할 수 없는 경우 이름을 조정합니다.) |
    | 그룹 설명 | `Administrators that manage the IT lab` |
    | 멤버 자격 유형 | **할당됨** |

    >**참고**: **멤버 자격 유형** 드롭다운 목록이 회색으로 표시될 수 있습니다. 여기서 할당된 그룹에서 동적 그룹으로 전환할 수 있습니다. 이렇게 하려면 Entra ID Premium P1 또는 P2 라이선스가 필요합니다.

    ![할당된 그룹 만들기 스크린샷](../media/az104-lab01-create-assigned-group.png)

1. **선택한 구성원 없음**을 클릭합니다.

1. **멤버** 추가 블레이드에서 az104-user1**을 검색하여 선택하고 **그룹에 추가합니다. 

1. 만들기**를 클릭하여 **그룹 만들기를 완료합니다. 

## 작업 5: Cloud Shell을 숙지합니다.

이 작업에서는 Azure Cloud Shell을 사용합니다. Azure Cloud Shell은 Azure 리소스를 관리하기 위한 대화형 인증 브라우저 액세스 터미널입니다. Bash나 PowerShell 작업 방식에 가장 적합한 셸 환경을 유연하게 선택할 수 있습니다. 

1. Azure Portal의 **오른쪽 위에 있는 Cloud Shell** 아이콘을 선택합니다. 또는 .으로 직접 이동할 `https://shell.azure.com`수 있습니다.

1. Bash** 또는 PowerShell**을 **선택하라는 메시지가 표시되면 PowerShell**을 선택합니다****. Bash는 다음 작업에서 사용됩니다.

    >**알고 계셨나요?**  Linux 시스템을 주로 사용하는 경우 Azure CLI는 더 자연스러운 느낌을 줍니다. Windows 시스템을 주로 사용하는 경우 Azure PowerShell은 더 자연스러운 느낌을 줍니다. 

1. **탑재된** 스토리지가 없는 경우 화면에서 고급 설정** 표시를 선택하고 **필요한 정보를 제공합니다. 완료되면 스토리지** 만들기를 선택합니다**. 

    | 설정 | 값 |
    |  -- | -- |
    | 리소스 그룹 | **새 리소스 그룹 만들기** |
    | 스토리지 계정(전역적으로 고유한 이름을 사용하는 새 계정 만들기(예: cloudshellstoragemystorage)) | **cloudshellxxxxxxx** |
    | 파일 공유(새로 만들기) | **shellstorage** |

    >**참고:** 호스트된 랩 환경에서 작업하는 경우 새 랩 환경을 만들 때마다 클라우드 셸 스토리지를 구성해야 합니다.

    >**참고:** 작업 6을 사용하면 Azure PowerShell을 연습할 수 있습니다. 작업 7을 사용하면 CLI를 연습할 수 있습니다. 두 작업 또는 가장 관심 있는 작업만 수행할 수 있습니다. 

## 작업 6: Azure PowerShell 연습

이 작업에서는 Cloud Shell 내에서 Azure PowerShell 세션을 사용하여 리소스 그룹 및 Azure AD 그룹을 만듭니다.

    >**Note:** Use the arrow keys to move through the command history. Use the tab key to autocomplete commands and parameters.

1. Cloud Shell에서 작업을 계속합니다. 언제든지 cls를** 사용하여 **명령 창을 지웁니다.

1. Azure PowerShell은 cmdlet에 *동사**-명사* 형식을 사용합니다. 예를 들어 새 리소스 그룹을 만드는 cmdlet은 New-AzResourceGroup입니다****. cmdlet을 사용하는 방법을 보려면 Get-Help 명령을 실행합니다.

   ```powershell
   Get-Help New-AzResourceGroup -detailed
   ```
1. Cloud Shell 내의 PowerShell 세션에서 리소스 그룹을 만들려면 다음 명령을 실행합니다. 달러 기호($)로 시작하는 명령은 이후 명령에서 사용할 수 있는 변수를 만듭니다. 성공한 메시지가 표시되는지 확인합니다. 

   ```powershell
   $location = 'eastus'
   $rgName = 'az104-rg-ps'
   New-AzResourceGroup -Name $rgName -Location $location
   ```

1. 새로 만든 리소스 그룹의 속성을 검색하려면 다음 명령을 실행합니다.

   ```powershell
   Get-AzResourceGroup -Name $rgName
   ```

1. 이제 새 Azure 그룹을 만들어 보겠습니다.

   ```powershell
   Get-Help New-AzureADGroup -detailed
   ```

1. 도움말의 예제를 사용하여 다음 명령을 사용해 보세요. 먼저 Azure AD에 연결해야 합니다.

   ```powershell
   Connect-AzureAD 
   New-AzureADGroup -DisplayName "MyPSgroup" -MailEnabled $false -SecurityEnabled $true -MailNickName "MyPSgroup"
   ```

1. Azure Portal로 돌아갑니다. 새 리소스 그룹과 새 Azure 그룹이 있는지 확인합니다. 페이지를 새로 고쳐야 할 수도 있습니다. 

## 작업 7: Bash 셸 연습

이 작업에서는 Cloud Shell 내에서 Azure CLI 세션을 사용하여 리소스 그룹 및 Azure 그룹을 만듭니다.

1. Cloud Shell에서 계속 진행합니다. 드롭다운을 사용하여 Bash**로 전환합니다**.

    >**참고:** 화살표 키를 사용하여 명령 기록을 이동합니다. 탭 키를 사용하여 명령 및 매개 변수를 자동으로 완성합니다. 

1. Azure CLI는 읽기 쉬운 구문을 사용합니다. 예를 들어 리소스 그룹과 상호 작용하기 위해 명령은 az group**입니다**.  

   ```sh
   az group --help
   ```

1. **만들기** 옵션은 유망한 것으로 보입니다. 대문자로 된 이름은 후속 명령에서 참조할 수 있는 변수를 만듭니다. 

   ```sh
   RGNAME='az104-rg1-cli'
   LOCATION='eastus'
   az group create --name $RGNAME --location $LOCATION
   ```
   
1. 새로 만든 리소스 그룹에 대한 속성을 확인하고 검색하려면 show** 명령을 사용해 보세요**. 

   ```sh
   az group show --name $RGNAME
   ```
1. 이제 도움말을 사용하여 Azure 그룹을 만드는 방법에 대해 자세히 알아보겠습니다.

    ```sh
    az ad group --help
    ```

1. **그룹을 **만들고** 확인할 그룹을 나열**합니다.

   ```sh
   az ad group create --display-name MyCLIgroup --mail-nickname MyCLIgroup
   az ad group list
   ```

1. Azure Portal로 돌아갑니다. 새 리소스 그룹과 새 Azure 그룹이 있는지 확인합니다. 페이지를 새로 고쳐야 할 수도 있습니다.   
    
## 랩의 기본 지점 검토

랩을 완료한 것을 축하합니다. 다음은 이 랩에 대한 몇 가지 기본 진행입니다.

+ Azure Portal은 Azure 리소스 만들기 및 관리를 시작하는 좋은 방법입니다. 관리 관리자는 포털을 사용자 지정하고 대시보드를 공유할 수 있습니다.
+ 리소스 그룹은 관련 리소스를 그룹화할 수 있는 방법입니다. 프로젝트, 부서 또는 애플리케이션에 리소스 그룹을 사용할 수 있습니다. 이렇게 하면 관련 리소스 그룹을 쉽게 관리하고 모니터링할 수 있습니다. 
+ Microsoft Entra ID에는 다양한 형식의 사용자 계정이 있습니다. 각 사용자 계정 유형에는 예상 작업 범위와 관련된 액세스 수준이 있습니다. 
+ 관련 사용자 또는 디바이스를 그룹화합니다. 그룹 멤버 자격은 정적 또는 동적으로 할당할 수 있습니다. 
+ Cloud Shell은 Azure 리소스를 관리하기 위한 인증된 대화형 터미널입니다. Cloud Shell은 Bash 또는 Azure PowerShell에 대한 액세스를 제공합니다.
+ Azure PowerShell 및 Bash는 리소스를 만드는 스크립싱된 방법을 제공합니다. 

## 리소스 정리

고유한 구독으로 작업하는 경우 랩 리소스를 삭제하는 데 1분이 소요됩니다. 이렇게 하면 리소스가 해제되고 비용이 최소화됩니다. 랩 리소스를 삭제하는 가장 쉬운 방법은 랩 리소스 그룹을 삭제하는 것입니다. 

+ Azure Portal에서 리소스 그룹을 선택하고, 리소스 그룹 삭제를 선택하고 **, **리소스 그룹** 이름을** 입력한 다음, 삭제**를 클릭합니다**.

+ Azure PowerShell 사용. `Remove-AzResourceGroup -Name resourceGroupName` 

+ CLI `az group delete --name resourceGroupName`를 사용하여 .

