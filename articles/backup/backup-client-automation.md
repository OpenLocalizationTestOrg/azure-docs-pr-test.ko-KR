---
title: Windows Server tooAzure aaaUse PowerShell tooback | Microsoft Docs
description: "자세한 내용은 방법 toodeploy 및 PowerShell을 사용 하 여 Azure 백업 관리"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 65218095-2996-44d9-917b-8c84fc9ac415
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;jimpark;nkolli;trinadhk
ms.openlocfilehash: f13224f53abd6fbd132fee4347b0b99e8f5e2678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a>배포 하 고 PowerShell을 사용 하 여 Windows Server/Windows 클라이언트에 대 한 백업 tooAzure 관리
> [!div class="op_single_selector"]
> * [ARM](backup-client-automation.md)
> * [클래식](backup-client-automation-classic.md)
>
>

이 문서에서는 Windows Server 또는 Windows 클라이언트에서 Azure 백업 설정 및 백업 및 복구 관리 하기 위한 PowerShell toouse 합니다.

## <a name="install-azure-powershell"></a>Azure Powershell 설치
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

이 문서는 Azure 리소스 관리자 (ARM) hello 및 hello toouse 리소스 그룹에 복구 서비스 자격 증명 모음을 사용할 수 있는 MS 온라인 백업 PowerShell cmdlet 중점적으로 수행 합니다.

Azure PowerShell 1.0이 2015년 10월에 출시되었습니다. 이 릴리스에서 hello 0.9.8 릴리스 성공 못하고 hello hello cmdlet의 이름 지정 패턴의 특히 몇 가지 주요 변경 사항에 대 한 합니다. 1.0 cmdlet에 따라 hello 명명 패턴 {동사}-{명사}; AzureRm 반면 hello 0.9.8 이름 포함 되지 않습니다 **Rm** (예를 들어 새로 만들기-AzureRmResourceGroup 새로 AzureResourceGroup 대신). Hello를 실행 하 여 hello Resource Manager 모드를 먼저 활성화 해야 Azure PowerShell 0.9.8을 사용할 경우 **Switch-azuremode AzureResourceManager** 명령입니다. 이 명령은 1.0 이상에서는 필요하지 않습니다.

Toouse hello 1.0 또는 이상 환경에서 hello 0.9.8 환경 용으로 작성 된 스크립트를 원하는 경우 신중 하 게 업데이트 하 고 테스트 해야 hello 스크립트 사전 프로덕션 환경에서 프로덕션 tooavoid에 사용 하기 전에 예기치 않은 영향입니다.

[Hello 최신 PowerShell 릴리스의 다운로드](https://github.com/Azure/azure-powershell/releases) (필요한 최소 버전은: 1.0.0)

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a>복구 서비스 자격 증명 모음 만들기
단계를 수행 하는 hello 복구 서비스 자격 증명 모음을 만드는 과정을 안내 합니다. 복구 서비스 자격 증명 모음은 백업 자격 증명 모음과 다릅니다.

1. 을 사용 중인 Azure 백업 hello에 대 한 처음으로 hello를 사용 해야 **레지스터 AzureRMResourceProvider** cmdlet tooregister hello Azure 복구 서비스 공급자를 구독 합니다.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. hello 복구 서비스 자격 증명 모음이 ARM 리소스를 tooplace 있으므로 리소스 그룹 내에서. 기존 리소스 그룹을 사용하거나 리소스 그룹을 새로 만들 수 있습니다. 새 리소스 그룹을 만들 때 hello 이름과 hello 리소스 그룹에 대 한 위치를 지정 합니다.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. 사용 하 여 hello **새로 AzureRmRecoveryServicesVault** cmdlet toocreate hello 새 자격 증명 모음입니다. Hello 리소스 그룹에 대해 사용한 것과 toospecify hello hello 자격 증명 모음에 대해 동일한 위치 해야 합니다.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. Hello 유형의 저장소 중복성 toouse;를 지정 합니다. 사용할 수 있습니다 [로컬 중복 저장소 (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) 또는 [지역 중복 저장소 (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage)합니다. hello 다음 예제에서는 testVault에 대 한 hello-BackupStorageRedundancy 옵션 tooGeoRedundant 설정

   > [!TIP]
   > 많은 Azure 백업 cmdlet을 입력으로 hello 복구 서비스 자격 증명 모음 개체를 필요로합니다. 이러한 이유로 변수의 편리한 toostore hello 백업 복구 서비스 자격 증명 모음 개체입니다.
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a>구독에서 보기 hello 자격 증명 모음
사용 하 여 **Get AzureRmRecoveryServicesVault** tooview hello 목록이 hello 현재 구독에서 모든 자격 증명 모음입니다. 새 자격 증명 모음 만들어진을이 명령 toocheck 또는 toosee 사용할 수 있는 자격 증명 모음 hello 구독에서 사용할 수 있는 합니다.

Hello 명령을 실행 **Get AzureRmRecoveryServicesVault**, hello 구독에서 모든 자격 증명 모음에 나열 됩니다.

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="installing-hello-azure-backup-agent"></a>Hello Azure 백업 에이전트를 설치
Hello Azure 백업 에이전트를 설치 하기 전에 다운로드 하 여 Windows 서버 hello에 toohave hello installer가 필요 합니다. Hello에서 hello hello installer의 최신 버전을 얻을 수 있습니다 [Microsoft 다운로드 센터](http://aka.ms/azurebackup_agent) 또는 hello 복구 서비스 자격 증명 모음의 대시보드 페이지에서. Hello 설치 관리자와 같은 tooan 쉽게 액세스할 수 있는 위치를 저장 * C:\Downloads\*합니다.

또는, PowerShell tooget hello 다운로더를 사용 합니다.
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

다음 명령을 관리자 권한 PowerShell 콘솔 hello 실행 tooinstall hello 에이전트:

```
PS C:\> MARSAgentInstaller.exe /q
```

이 모든 hello 기본 옵션으로 hello 에이전트를 설치합니다. hello 설치 hello 백그라운드에서 몇 분이 걸립니다. Hello를 지정 하지 않으면 */nu* 옵션 다음 hello **Windows Update** 모든 업데이트에 대 한 hello 설치 toocheck hello 끝나기 전에 창이 열립니다. 설치 되 면 hello 에이전트 hello 설치 된 프로그램 목록에 표시 됩니다.

설치 된 프로그램 toosee hello 목록이, 너무 이동**제어판** > **프로그램** > **프로그램 및 기능**합니다.

![에이전트 설치됨](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a>설치 옵션
통해 사용할 수 있는 옵션을 hello 모든 toosee 명령줄 hello, hello 다음 명령을 사용 하 여:

```
PS C:\> MARSAgentInstaller.exe /?
```

hello 사용할 수 있는 옵션은 다음과 같습니다.

| 옵션 | 세부 정보 | 기본값 |
| --- | --- | --- |
| /q |자동 설치 |- |
| /p:"위치" |Hello Azure 백업 에이전트에 대 한 toohello 설치 폴더 경로입니다. |C:\Program Files\Microsoft Azure Recovery Services Agent |
| /s:"위치" |Hello Azure 백업 에이전트에 대 한 toohello 캐시 폴더 경로입니다. |C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch |
| /m |옵트인 tooMicrosoft 업데이트 |- |
| /nu |설치가 완료된 후 업데이트에 대한 검사 안 함 |- |
| /d |Microsoft Azure Recovery Services 에이전트를 제거합니다. |- |
| /ph |프록시 호스트 주소 |- |
| /po |프록시 호스트 포트 번호 |- |
| /pu |프록시 호스트 사용자 이름 |- |
| /pw |프록시 암호 |- |

## <a name="registering-windows-server-or-windows-client-machine-tooa-recovery-services-vault"></a>Windows Server 또는 Windows 클라이언트 컴퓨터 tooa 복구 서비스 자격 증명 모음 등록
Hello 복구 서비스 자격 증명 모음을 만든 후 hello 최신 에이전트 및 hello 자격 증명 모음 자격 증명을 다운로드 하 고 C:\Downloads 같은 편리한 위치에 저장 합니다.

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

Hello Windows Server 또는 Windows 클라이언트 컴퓨터에서 실행 hello [Start-obregistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) hello 자격 증명 모음 cmdlet tooregister hello 컴퓨터.
이 및 백업에 사용 되는 다른 cmdlet은 hello MSONLINE 모듈에서 Mars AgentInstaller hello 설치 프로세스의 일부로 추가 하는 hello입니다. 

hello Agent installer $Env hello를 업데이트 하지 않습니다: PSModulePath 변수에 합니다. 즉, 모듈 자동 로드에 실패합니다. tooresolve 할 수 있는이 hello 다음:

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

또는 수동으로 로드할 수 있습니다 hello 모듈 스크립트에서 다음과 같이 합니다.

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

Hello 온라인 백업 cmdlet을 로드 하면 hello 자격 증명 모음 등록 합니다.


```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :WestUS
Machine registration succeeded.
```

> [!IMPORTANT]
> 상대 경로 toospecify hello 자격 증명 모음 자격 증명 파일을 사용 하지 마십시오. 입력된 toohello cmdlet으로는 절대 경로 제공 해야 합니다.
>
>

## <a name="networking-settings"></a>네트워킹 서비스
Hello의 hello 연결 Windows 컴퓨터 인터넷 프록시 서버를 통해은 toohello을 때 hello 프록시 설정은 제공할 수도 있습니다 toohello 에이전트입니다. 이 예제에서는 프록시 서버가 없으므로 프록시와 관련된 모든 정보를 명시적으로 지웁니다.

Hello 옵션의 대역폭 사용량을 제어할 수도 있습니다 ```work hour bandwidth``` 및 ```non-work hour bandwidth``` hello 주 중 일의 특정된 집합에 대 한 합니다.

Hello 프록시 및 대역폭 세부 정보를 설정 이루어진다는 hello를 사용 하 여 [Set-obmachinesetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a>암호화 설정
hello 전송 되는 백업 데이터 tooAzure 백업 hello 데이터의 암호화 된 tooprotect hello 기밀입니다. hello 암호화의 암호는 복원의 hello 시 hello "password" toodecrypt hello 데이터입니다.

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> 설정 되 면 hello 암호 정보를 안전 하 게 유지 합니다. 이 암호 없이 Azure에서 수 toorestore 데이터를 수는 없습니다.
>
>

## <a name="back-up-files-and-folders"></a>파일 및 폴더 백업
Windows 서버 및 클라이언트 tooAzure 백업에서에서 모든 백업 정책에 의해 제어 됩니다. hello 정책에는 세 부분으로 구성 됩니다.

1. A **백업 일정** 백업을 toobe 가져오고 hello 서비스와 동기화 해야 하는 경우를 지정 하는 합니다.
2. A **보존 일정** Azure tooretain hello 복구 지점 기간을 지정 하는 합니다.
3. 백업해야 할 항목을 지정하는 **파일 포함/제외 사양** .

이 문서에서는 백업을 자동화하기 때문에 아무것도 구성되지 않은 것으로 가정합니다. 사용 하 여 hello를 사용 하 여 새 백업 정책을 만드는 [New-obpolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.

```
PS C:\> $newpolicy = New-OBPolicy
```

이 시간 hello에서 정책 비어 있고 다른 cmdlet은 필요한 toodefine 포함 되거나 제외 될 항목, 백업이 저장 될 때 백업을 실행 하 고 여기서 hello 됩니다.

### <a name="configuring-hello-backup-schedule"></a>Hello 백업 일정 구성
먼저 hello hello 정책 3 부분이 hello를 사용 하 여 생성 된 백업 일정을 hello [새로 OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet. 백업 일정 hello 백업을 toobe 수행 해야 하는 경우를 정의 합니다. 일정을 만들 때 2 toospecify 입력된 매개 변수가 필요 합니다.

* **Hello 주 중 일** 해당 hello 백업을 실행 해야 합니다. Hello만 1 일에서 백업 작업 또는 hello 주 매일 또는 조합을 사이 실행할 수 있습니다.
* **Hello 하루 중 시간** hello 백업 실행 시기입니다. Too3 시간 hello hello 백업 트리거될 수는 때를 정의할 수 있습니다.

예를 들어, 토요일과 일요일마다 오후 4시에 실행되는 백업 정책을 구성할 수 있습니다.

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

hello 백업 일정을 정책에 연결 된 toobe 되어야 하며 hello를 사용 하 여 이렇게 할 [Set-obschedule](https://technet.microsoft.com/library/hh770407) cmdlet.

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a>보존 정책 구성
hello 보존 정책은 백업 작업에서 생성 된 지점을 유지 되는 시간 복구를 정의 합니다. Hello를 사용 하 여 새 보존 정책을 만들 때 [새로 OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet hello 일 수를 백업 복구 지점을 hello 필요 toobe를 Azure 백업 보존을 지정할 수 있습니다. 다음 예제에서는 hello 보존 정책을 7 일로 설정합니다.

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

hello 보존 정책을 연결 해야 hello cmdlet을 사용 하는 hello 주 정책과 [집합 OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-toobe-backed-up"></a>포함 및 제외 toobe 파일 백업
```OBFileSpec``` hello 파일 toobe 포함 되거나 백업에서 제외 개체를 정의 합니다. Hello 아웃 범위는 컴퓨터의 파일 및 폴더 보호 하는 규칙의 집합입니다. 필요에 따라 원하는 만큼 파일을 포함 또는 제외시키고 정책과 연결할 수 있습니다. 새 OBFileSpec 개체를 만드는 경우 다음 작업을 수행할 수 있습니다.

* 포함 된 hello 파일 및 폴더 toobe 지정
* Hello 파일 및 폴더 toobe 제외를 지정 합니다.
* 재귀 백업 데이터 폴더 (또는) hello 최상위에 있는 파일만 hello 지정 된 폴더를 백업 해야 하는지 여부를 지정 합니다.

후자의 hello hello New-obfilespec 명령 hello-비재귀 플래그를 사용 하 여 이루어집니다.

Hello 아래의 예제에서는 c: 및 d: 볼륨을 백업 알아보고 hello OS 바이너리 hello Windows 폴더 및 임시 폴더에 제외 하겠습니다. hello를 사용 하 여 두 파일 사양 만들겠습니다 하므로 toodo [New-obfilespec](https://technet.microsoft.com/library/hh770408) cmdlet-포함 및 제외 하나에 대 한 합니다. Hello를 사용 하 여 hello 정책과 연결 된 자신이 hello 파일 지정을 만든 후 [Add-obfilespec](https://technet.microsoft.com/library/hh770424) cmdlet.

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-hello-policy"></a>Hello 정책 적용
이제 hello 정책 개체가 완료 되 고 연결된 된 백업 일정, 보존 정책 및은 파일 포함/제외 목록. 이 정책은 이제 toouse Azure 백업에 대 한 커밋할 수 있습니다. 새로 만든 hello를 적용 하기 전에 정책을 확인 hello를 사용 하 여 hello 서버와 관련 된 기존 백업 정책이 없으면 [제거 OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet. Hello 정책 제거 하는 확인 메시지를 표시 합니다. tooskip hello 확인 hello를 사용 하 여 ```-Confirm:$false``` hello cmdlet과 플래그입니다.

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

커밋 hello 정책 개체 이루어집니다 hello를 사용 하 여 [Set-obpolicy](https://technet.microsoft.com/library/hh770421) cmdlet. 이 작업에서도 확인 메시지가 표시됩니다. tooskip hello 확인 hello를 사용 하 여 ```-Confirm:$false``` hello cmdlet과 플래그입니다.

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

Hello hello를 사용 하 여 hello 기존 백업 정책 세부 정보를 볼 수 있습니다 [Get-obpolicy](https://technet.microsoft.com/library/hh770406) cmdlet. 있습니다 수 드릴 다운 hello를 사용 하 여 자세히 [Get OBSchedule](https://technet.microsoft.com/library/hh770423) hello 백업 일정 및 hello에 대 한 cmdlet [Get OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) hello 보존 정책에 대 한 cmdlet

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a>임시 백업 수행
백업 정책을 설정 되 면 hello 백업을 hello 일정에 따라 발생 합니다. 임시 백업을 트리거하는 hello를 사용 하 여 가능한도 [시작 OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing hello metadata VHD...
Data transfer is in progress. It might take longer since it is hello first backup and all data needs toobe transferred...
Data transfer completed and all backed up data is in hello cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a>Azure 백업에서 데이터 복원
이 섹션에서는 Azure 백업에서 데이터의 복구 자동화에 대 한 hello 단계를 안내 합니다. 이렇게 하면 hello를 단계를 수행 하므로 구성 되어 있습니다.

1. Hello 원본 볼륨 선택
2. 백업 지점 toorestore 선택
3. 항목 toorestore 선택
4. 트리거 hello 복원 프로세스

### <a name="picking-hello-source-volume"></a>Hello 원본 볼륨을 선택합니다.
순서 toorestore Azure 백업에서 항목에에서는 먼저 hello 항목의 tooidentify hello 원본이 필요 합니다. Windows Server 또는 Windows 클라이언트의 hello 컨텍스트에서 hello 명령을 실행 하는 것, 이후 hello 컴퓨터는 이미 식별 됩니다. hello 소스를 식별 hello 다음 단계에는 포함 하는 tooidentify hello 볼륨입니다. Hello를 실행 하 여 검색할 수 있습니다이 컴퓨터에서 백업 중인 볼륨 또는 원본 목록 [Get-obrecoverablesource](https://technet.microsoft.com/library/hh770410) cmdlet. 이 명령은이 서버/클라이언트에서 백업 하는 모든 hello 원본의 배열을 반환 합니다.

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-from-which-toorestore"></a>어떤 toorestore에서 백업 지점 선택
Hello를 실행 하 여 백업 지점 목록 검색 [Get-obrecoverableitem](https://technet.microsoft.com/library/hh770399.aspx) 적절 한 매개 변수를 사용 하 여 cmdlet. 예에서 hello hello 원본 볼륨에 대 한 최신 백업 지점을 선택 합니다 *d:* toorecover 특정 파일을 사용 합니다.

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
hello 개체 ```$rps``` 배열 백업 지점입니다. 첫 번째 요소가 hello hello 최신 시점 고 hello n 번째 요소는 hello 가장 오래 된 지점입니다. toochoose hello 최신 지점을 사용 하 여 ```$rps[0]```합니다.

### <a name="choosing-an-item-toorestore"></a>항목 toorestore 선택
재귀적으로 hello를 사용 하 여 tooidentify hello 정확한 파일 또는 폴더 toorestore [Get-obrecoverableitem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet. 전적으로 hello를 사용 하 여 해당 방식으로 hello 폴더 계층 구조를 찾아볼 수 ```Get-OBRecoverableItem```합니다.

이 예제에서는 toorestore hello 파일 원하는 *finances.xls* 사용 하는 것을 참조할 수 있습니다 hello 개체 ```$filesFolders[1]```합니다.

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

항목 toorestore hello를 사용 하 여 검색할 수 있습니다 ```Get-OBRecoverableItem``` cmdlet. 예제에 대 한 toosearch *finances.xls* 이 명령을 실행 하 여 hello 파일에 대 한 핸들 신속:

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a>트리거 hello 복원 프로세스
tootrigger hello 복원 프로세스를 먼저 필요 toospecify hello 복구 옵션입니다. Hello를 사용 하 여이 작업을 수행할 수 있습니다 [새로 OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet. 이 예에서는 가정 한다고 toorestore hello 파일 너무*C:\temp*합니다. 또한 가정해 hello 대상 폴더에 이미 있는 tooskip 파일 한다고 *C:\temp*. toocreate 같은 복구 옵션을 사용 하 여 다음 명령을 hello:

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

이제 hello를 사용 하 여 hello 복원 프로세스를 트리거할 [Start-obrecovery](https://technet.microsoft.com/library/hh770402.aspx) hello 선택한 명령을 ```$item``` hello의 hello 출력에서 ```Get-OBRecoverableItem``` cmdlet:

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a>Hello Azure 백업 에이전트를 제거합니다.
다음 명령을 hello를 사용 하 여 hello Azure 백업 에이전트 제거를 수행할 수 있습니다.

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

Hello 컴퓨터에서 제거 하는 hello 에이전트 이진 파일에 일부 결과 tooconsider가 있습니다.

* Hello 컴퓨터에서 hello 파일 필터를 제거 하 고 변경 내용 추적 중지 됩니다.
* Hello 컴퓨터에서 정책 정보를 모두 없어지지만 hello 정책 정보가 hello 서비스에 저장 된 toobe 계속 있습니다.
* 모든 백업 일정이 제거되고 더 이상 백업이 수행되지 않습니다.

그러나 hello 데이터는 Azure 유지에 저장 하 고 hello 보존 정책 설정에 따라 사용자가 유지 됩니다. 이전 지점은 시간이 경과하면 자동으로 삭제됩니다.

## <a name="remote-management"></a>원격 관리
Hello Azure 백업 에이전트, 정책 및 데이터 원본 주위의 모든 hello 관리는 PowerShell을 통해 원격으로 수행할 수 있습니다. 원격으로 관리 되는 hello 컴퓨터에 제대로 준비 toobe가 필요 합니다.

기본적으로 hello WinRM 서비스를 수동으로 시작 구성 됩니다. hello 시작 유형을 너무 설정 해야*자동* hello service를 시작 해야 합니다. WinRM 서비스가 hello tooverify 실행 되 고, hello hello Status 속성 값 있어야 *실행*합니다.

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

PowerShell을 원격 작업용으로 구성해야 합니다.

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

hello 컴퓨터 수 이제 원격으로 관리할 수-hello 설치 된 hello 에이전트를에서 시작 합니다. 예를 들어 다음 스크립트는 hello hello 에이전트 toohello 원격 컴퓨터를 복사 설치 합니다.

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a>다음 단계
Windows Server/Client용 Azure 백업에 대한 자세한 정보는 다음을 참조하세요.

* [소개 tooAzure 백업](backup-introduction-to-azure-backup.md)
* [Windows 서버 백업](backup-configure-vault.md)
