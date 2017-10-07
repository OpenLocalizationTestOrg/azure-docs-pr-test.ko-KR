---
title: "백업-DPM 작업 백업 PowerShell 사용 하 여 tooback aaaAzure | Microsoft Docs"
description: "자세한 내용은 방법 toodeploy 및 Azure 백업에 대 한 Data Protection Manager (DPM) PowerShell을 사용 하 여 관리"
services: backup
documentationcenter: 
author: NKolli1
manager: shreeshd
editor: 
ms.assetid: e9bd223c-2398-4eb1-9bf3-50e08970fea7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: adigan;anuragm;trinadhk;markgal
ms.openlocfilehash: 27d2b4b3127b68c9da564697eb61dc3ccbc34b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a>배포 하 고 PowerShell을 사용 하 여 Data Protection Manager (DPM) 서버에 대 한 백업 tooAzure 관리
> [!div class="op_single_selector"]
> * [ARM](backup-dpm-automation.md)
> * [클래식](backup-dpm-automation-classic.md)
>
>

이 문서에서는 어떻게 toouse PowerShell toosetup를 Azure 백업에서 DPM 서버 및 toomanage 백업 및 복구 합니다.

## <a name="setting-up-hello-powershell-environment"></a>Hello PowerShell 환경 설정
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Data Protection Manager tooAzure toomanage 백업을 PowerShell을 사용 하려면 먼저 toohave hello 오른쪽 환경 powershell에서이 필요 합니다. Hello PowerShell 세션을 hello 시작 시 hello 다음 명령 tooimport hello 오른쪽 모듈을 실행 하 고 toocorrectly 참조 hello DPM cmdlet을 사용 하면 확인 합니다.

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a>설정 및 등록
toobegin:

1. [최신 PowerShell을 다운로드](https://github.com/Azure/azure-powershell/releases) 합니다(필요한 최소 버전: 1.0.0).
2. 너무 전환 하 여 hello Azure 백업 commandlet을 사용 하도록 설정*AzureResourceManager* hello를 사용 하 여 모드 **Switch-azuremode** commandlet:

```
PS C:\> Switch-AzureMode AzureResourceManager
```

hello 다음과 같은 설치 및 등록 작업을 자동화 하는 PowerShell로:

* 복구 서비스 자격 증명 모음 만들기
* Hello Azure 백업 에이전트를 설치
* Hello Azure 백업 서비스 등록
* 네트워킹 서비스
* 암호화 설정

## <a name="create-a-recovery-services-vault"></a>복구 서비스 자격 증명 모음 만들기
단계를 수행 하는 hello 복구 서비스 자격 증명 모음을 만드는 과정을 안내 합니다. 복구 서비스 자격 증명 모음은 백업 자격 증명 모음과 다릅니다.

1. 을 사용 중인 Azure 백업 hello에 대 한 처음으로 hello를 사용 해야 **레지스터 AzureRMResourceProvider** cmdlet tooregister hello Azure 복구 서비스 공급자를 구독 합니다.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. hello 복구 서비스 자격 증명 모음이 ARM 리소스를 tooplace 있으므로 리소스 그룹 내에서. 기존 리소스 그룹을 사용하거나 리소스 그룹을 새로 만들 수 있습니다. 새 리소스 그룹을 만들 때 hello 이름과 hello 리소스 그룹에 대 한 위치를 지정 합니다.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. 사용 하 여 hello **새로 AzureRmRecoveryServicesVault** cmdlet toocreate 새 자격 증명 모음입니다. Hello 리소스 그룹에 대해 사용한 것과 toospecify hello hello 자격 증명 모음에 대해 동일한 위치 해야 합니다.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
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

Get-AzureRmRecoveryServicesVault hello 명령을 실행 하 고 hello 구독에서 모든 자격 증명 모음 나열 됩니다.

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


## <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a>DPM 서버에서 hello Azure 백업 에이전트를 설치합니다.
Hello Azure 백업 에이전트를 설치 하기 전에 다운로드 하 여 Windows 서버 hello에 toohave hello installer가 필요 합니다. Hello에서 hello hello installer의 최신 버전을 얻을 수 있습니다 [Microsoft 다운로드 센터](http://aka.ms/azurebackup_agent) 또는 hello 복구 서비스 자격 증명 모음의 대시보드 페이지에서. Hello 설치 관리자와 같은 tooan 쉽게 액세스할 수 있는 위치를 저장 * C:\Downloads\*합니다.

다음 명령을 관리자 권한 PowerShell 콘솔 hello 실행 tooinstall hello 에이전트 **hello DPM 서버의**:

```
PS C:\> MARSAgentInstaller.exe /q
```

이 모든 hello 기본 옵션으로 hello 에이전트를 설치합니다. hello 설치 hello 백그라운드에서 몇 분이 걸립니다. Hello를 지정 하지 않으면 */nu* 옵션 hello **Windows Update** 모든 업데이트에 대 한 hello 설치 toocheck hello 끝나기 전에 창이 열립니다.

hello 에이전트 hello 설치 된 프로그램 목록에 나타납니다. 설치 된 프로그램 toosee hello 목록이, 너무 이동**제어판** > **프로그램** > **프로그램 및 기능**합니다.

![에이전트 설치됨](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a>설치 옵션
toosee hello commandline에 따라 사용 하 여 hello 통해 사용할 수 있는 모든 hello 옵션 명령 수 있습니다.

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

## <a name="registering-dpm-tooa-recovery-services-vault"></a>DPM tooa 복구 서비스 자격 증명 모음 등록
Hello 복구 서비스 자격 증명 모음을 만든 후 hello 최신 에이전트 및 hello 자격 증명 모음 자격 증명을 다운로드 하 고 C:\Downloads 같은 편리한 위치에 저장 합니다.

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

Hello DPM 서버에서 실행 hello [Start-obregistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) hello 자격 증명 모음 cmdlet tooregister hello 컴퓨터.

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a>초기 구성 설정
DPM 서버 hello hello로 등록 되 면 복구 서비스 자격 증명 모음, 기본 구독 설정으로 시작 합니다. 이러한 구독 설정 네트워킹, 암호화 및 hello 준비 영역에 포함 됩니다. toofirst 필요한 toochange 구독 설정을 hello hello를 사용 하는 기존 (기본값) 설정에는 핸들을 가져올 [Get DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

모든 수정이 로컬 PowerShell 개체를 만들어 놓은 toothis ```$setting``` 하 고 hello 전체 개체 커밋된 tooDPM 및 Azure 백업 toosave hello를 통해 [집합 DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet. Toouse hello 필요한 ```–Commit``` 변경 hello 플래그 tooensure 유지 됩니다. hello 설정 되지 적용 되며 커밋된 하지 않는 한 Azure 백업에 사용 합니다.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a>네트워킹
이면 hello 연결 hello DPM 컴퓨터 toohello hello에 Azure 백업 서비스의 인터넷 프록시 서버를 통해 성공적인 백업에 대 한 hello 프록시 서버 설정 제공 되어야 합니다. Hello를 사용 하 여 이렇게 ```-ProxyServer```및 ```-ProxyPort```, ```-ProxyUsername``` 및 hello ```ProxyPassword``` hello로 매개 변수 [집합 DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet. 이 예제에서는 프록시 서버가 없으므로 프록시와 관련된 모든 정보를 명시적으로 지웁니다.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

옵션의 대역폭 사용량을 제어할 수도 있습니다 ```-WorkHourBandwidth``` 및 ```-NonWorkHourBandwidth``` hello 주 중 일의 특정된 집합에 대 한 합니다. 이 예제에서는 제한을 설정하지 않습니다.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-hello-staging-area"></a>Hello 준비 영역 구성
hello DPM 서버에서 실행 되는 hello Azure 백업 에이전트 hello 클라우드 (로컬 준비 영역)에서 복원 된 데이터에 대 한 임시 저장소가 필요 합니다. Hello를 사용 하 여 hello 준비 영역 구성 [집합 DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet 및 hello ```-StagingAreaPath``` 매개 변수입니다.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

위의 hello 예제 hello 준비 영역을 설정할 너무*C:\StagingArea* hello PowerShell 개체의 ```$setting```합니다. 하도록는 hello 지정한 폴더가 이미 hello 최종 커밋 hello 구독 설정에 실패 합니다.

### <a name="encryption-settings"></a>암호화 설정
hello 전송 되는 백업 데이터 tooAzure 백업 hello 데이터의 암호화 된 tooprotect hello 기밀입니다. hello 암호화의 암호는 복원의 hello 시 hello "password" toodecrypt hello 데이터입니다. 중요 한 tookeep 정보 안전이 사용 되며 설정 되 면 보안을 설정 합니다.

Hello 아래 예제에서는 첫 번째 명령은 hello hello 문자열 변환 ```passphrase123456789``` tooa 보안 문자열 및 할당 hello 보안 toohello 이라는 문자열 변수 ```$Passphrase```합니다. 보안 문자열 hello를 설정 하는 hello 두 번째 명령은 ```$Passphrase``` 백업을 암호화 하기 위해 hello 암호와 합니다.

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> 설정 되 면 hello 암호 정보를 안전 하 게 유지 합니다. 이 암호 없이 Azure에서 수 toorestore 데이터 되지 않습니다.
>
>

이 시점에서 하였습니다 모든 hello 필요한 변경 내용을 toohello ```$setting``` 개체입니다. Toocommit hello 변경 해야 합니다.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a>데이터 tooAzure 백업 보호
이 섹션에서는 프로덕션 서버 tooDPM를 추가 하 고 hello 데이터 toolocal DPM 저장소 및 tooAzure 백업을 보호 합니다. Hello 예제에서 보여 드리겠습니다 방법을 tooback 파일 및 폴더를 합니다. hello 논리 쉽게 수는 DPM에서 지 원하는 데이터 원본 확장된 toobackup 일 합니다. 모든 DPM 백업은 4개 부분으로 구성된 보호 그룹(PG)에 의해 제어됩니다.

1. **멤버를 그룹화** 은 모든 hello 보호 가능한 개체의 목록 (라고도 *Datasources* DPM에서) hello에 tooprotect 되도록 동일한 보호 그룹입니다. 예를 들어 좋습니다 tooprotect 프로덕션 Vm 한 개의 보호 그룹 및 다른 보호 그룹에서 SQL Server 데이터베이스에 따라 서로 다른 백업 요구 사항이 있을 수 있습니다. 프로덕션 서버에는 데이터 원본을 백업할 수 전에 DPM 에이전트가 hello 서버에 설치 된 DPM에서 관리 되 고 있는지 hello toomake 해야 합니다. 에 대 한 hello 단계에 따라 [DPM 에이전트를 hello 설치](https://technet.microsoft.com/library/bb870935.aspx) toohello 연결 하는 DPM 서버에 적절 합니다.
2. **데이터 보호 방법** hello 대상 백업 위치-테이프, 디스크 및 클라우드를 지정 합니다. 예제에서 데이터 toohello 로컬 디스크 및 toohello 클라우드를 보호 합니다.
3. A **백업 일정** 백업을 toobe 수행 해야 하는 경우와 얼마나 자주 hello 데이터를 동기화 해야 hello DPM 서버와 프로덕션 서버 hello 지정 하는 합니다.
4. A **보존 일정** Azure tooretain hello 복구 지점 기간을 지정 하는 합니다.

### <a name="creating-a-protection-group"></a>보호 그룹 만들기
Hello를 사용 하 여 새 보호 그룹을 만들어 시작 [새로 DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

위의 cmdlet hello 라는 보호 그룹을 만들고 됩니다 *ProtectGroup01*합니다. 기존 보호 그룹 이후 tooadd 백업 toohello Azure 클라우드 수정할 수도 있습니다. 그러나 toomake 변경 내용을 tooget 핸들에 필요-기존의 또는 새 보호 그룹-toohello는 *수정 가능한* hello를 사용 하 여 개체 [Get DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a>그룹 구성원 toohello 보호 그룹 추가
각 DPM 에이전트에 설치 되어 있는 hello 서버에서 데이터 원본 목록이 hello를 알고 있습니다. datasource toohello 보호 그룹 tooadd hello 요구 toofirst DPM 에이전트 hello datasources 백 toohello DPM 서버의 목록을 보냅니다. 하나 이상의 데이터 원본 toohello 보호 그룹을 추가 하 고 선택 됩니다. hello PowerShell 단계가 tooachieve이 필요 합니다.

1. DPM에서 DPM 에이전트 hello를 통해 관리 되는 모든 서버 목록이 인출 합니다.
2. 특정 서버를 선택합니다.
3. Hello 서버에서 모든 데이터 원본 목록이 인출 합니다.
4. 하나 이상의 데이터 원본 선택 하 고 toohello 보호 그룹에 추가

서버는 hello DPM 에이전트가 설치 되 고 hello DPM 서버에서 관리 하는 hello 목록 hello로 획득 [Get DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet. 이 예제에서는 백업에 대해 이름이 *productionserver01* 인 PS만 필터링하여 구성합니다.

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

이제 hello 목록 데이터 원본에 가져올 ```$server``` hello를 사용 하 여 [Get DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet. 이 예에서 hello 볼륨에 대 한 필터링 * d:\* 백업용 tooconfigure 한다고 합니다. 그런 다음이 데이터는 toohello 보호 그룹 추가 hello를 사용 하 여 [추가 DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet. Toouse hello 기억 *수정 가능한* 보호 그룹 개체 ```$MPG``` toomake hello 추가 합니다.

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

Datasources toohello 보호 그룹을 선택 하는 모든 hello 추가 필요에 따라 횟수 만큼이 단계를 반복 합니다. 하나의 데이터 원본 및 hello 보호 그룹을 만들기 위한 전체 hello 워크플로로 시작 하 고 나중에 더 많은 데이터 원본을 toohello 보호 그룹을 추가 수도 있습니다.

### <a name="selecting-hello-data-protection-method"></a>Hello 데이터 보호 방법 선택
Hello 다음 단계는 toospecify hello 보호 방법 hello를 사용 하 여 hello datasources toohello 보호 그룹 추가 된, 일단 [집합 DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet. 이 예제에서는 보호 그룹 hello를 사용 하면 로컬 디스크와 클라우드 백업에 대 한 설치가.입니다. 또한 toospecify hello tooprotect toocloud hello를 사용 하 여 원하는 데이터 소스를 해야 [추가 DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet을-온라인 플래그입니다.

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a>Hello 보존 범위를 설정합니다.
Hello를 사용 하 여 hello 백업 지점에 대 한 hello 보존 설정 [집합 DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet. Hello 백업 일정 정의 전에, hello를 사용 하 여 홀수 tooset hello 보존 처럼 보이기는 하지만 ```Set-DPMPolicyObjective``` cmdlet 자동으로 설정 하는 기본 백업 일정을 수정할 수 있습니다. 항상 가능한 tooset hello에 대 한 백업 일정 먼저 사용 되며 이후 보존 정책 hello 합니다.

Hello 아래 예제에서는 hello cmdlet 디스크 백업에 대 한 hello 보존 기간을 설정합니다. 이 유지 백업은 10 일 및 동기화 데이터에 대 한 hello 프로덕션 서버와 DPM 서버 hello 6 시간 마다 합니다. hello ```SynchronizationFrequencyMinutes``` 빈도 백업 지점이 생성 된 경우 어떻게 하지만 정의 되지 않은 자주 데이터는 복사 toohello DPM 서버입니다.  이 설정은 백업이 너무 커지지 않도록 방지합니다.

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

(DPM toothem 온라인 백업을 지칭) tooAzure 라인으로 전환 하는 백업에 대 한 hello 보존 범위에 대해 구성할 있습니다 [장기간 보존 Son-ब ा प ज-구성표 (GFS)를 사용 하 여](backup-azure-backup-cloud-as-tape.md)합니다. 즉, 매일, 매주, 매월 및 매년 보존 정책이 포함된 통합 보존 정책을 정의할 수 있습니다. 이 예제에서는 우리가 원하는 hello 복잡 한 보존 규칙을 나타내는 배열을 만들고 hello를 사용 하 여 hello 보존 범위를 구성 합니다 [집합 DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a>Hello 백업 일정 설정
DPM 설정 기본 백업 일정을 자동으로 hello를 사용 하 여 hello 보호 목표를 지정 하는 경우 ```Set-DPMPolicyObjective``` cmdlet. toochange hello 기본 일정을 사용 하 여 hello [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet 뒤 hello [집합 DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

위 예제를 hello에 ```$onlineSch``` hello hello GFS 구성표에 hello 보호 그룹에 대 한 기존 온라인 보호 일정을 포함 하는 네 요소 배열:

1. ```$onlineSch[0]```hello 일별 일정을 포함합니다.
2. ```$onlineSch[1]```hello 주간 일정을 포함합니다.
3. ```$onlineSch[2]```hello 월별 일정을 포함합니다.
4. ```$onlineSch[3]```hello 연간 일정이 포함

Toorefer toohello 필요 toomodify hello 주간 일정 해야 할 경우 ```$onlineSch[1]```합니다.

### <a name="initial-backup"></a>초기 백업
처음으로 DPM 요구 hello에 대 한 데이터를 백업 생성할 때 초기 복제 하는 DPM 복제본 볼륨에서 보호 되는 hello datasource toobe의 전체 복사본을 만듭니다. 이 활동 특정 시간 동안 예약 수 또는 수동으로 트리거할 수, hello를 사용 하 여 [집합 DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) hello 매개 변수를 사용 하 여 cmdlet ```-NOW```합니다.

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a>DPM 복제 및 복구 지점 볼륨의 hello 크기를 변경
DPM 복제본 볼륨 및 사용 하 여 섀도 복사본 볼륨의 hello 크기를 변경할 수도 있습니다 [집합 DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) hello 다음 예제와 같이 cmdlet: Get-datasourcediskallocation-Datasource $DS Set-datasourcediskallocation-Datasource $DS-ProtectionGroup $MPG-수동 ReplicaArea (2gb)-ShadowCopyArea (2gb)

### <a name="committing-hello-changes-toohello-protection-group"></a>보호 그룹 toohello 변경 hello 커밋
마지막으로, hello 변경 toobe 커밋된 DPM 새 보호 그룹 구성 hello 당 hello 백업을 만들 수 있어야 합니다. Hello를 사용 하 여 수행할 수 있습니다 [집합 DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a>보기 hello 백업 지점
Hello를 사용할 수 있습니다 [Get DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget 데이터 원본에 대 한 모든 복구 지점 목록이 있습니다. 이 예제에서는 다음을 수행합니다.

* fetch는 PGs hello DPM 서버의 hello 모든와 배열에 저장```$PG```
* hello datasources 해당 toohello 가져오기```$PG[0]```
* 데이터 원본에 대 한 모든 hello 복구 지점을 가져옵니다.

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a>Azure에 보호된 데이터 복원
데이터 복원은 ```RecoverableItem``` 개체와 ```RecoveryOption``` 개체의 조합입니다. Hello 이전 섹션에서 데이터 원본에 대 한 hello 백업 지점 목록을 가져왔습니다.

Hello 아래의 예제에서는 hello로 백업 지점 결합 하 여 Azure 백업에서 toorestore는 Hyper-v 가상 컴퓨터 복구에 대 한 대상 하는 방법을 보여 줍니다. 이 예제에는 다음이 포함됩니다.

* Hello를 사용 하 여 복구 옵션을 만들 [새로 DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.
* Hello를 사용 하 여 백업 지점 반입 hello 배열 ```Get-DPMRecoveryPoint``` cmdlet.
* 백업 지점 toorestore를 선택 합니다.

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

hello 명령은 모든 데이터 원본 유형에 대해 쉽게 확장할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* DPM에 대 한 자세한 내용은 백업 tooAzure 참조 [소개 tooDPM 백업](backup-azure-dpm-introduction.md)
