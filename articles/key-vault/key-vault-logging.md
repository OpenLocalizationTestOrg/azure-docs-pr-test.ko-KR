---
title: "키 자격 증명 모음 로깅 aaaAzure | Microsoft Docs"
description: "Azure 키 자격 증명 모음 시작 하기 자습서 toohelp이를 사용 하 여 로그인 합니다."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a>Azure 키 자격 증명 모음 로깅
Azure 키 자격 증명 모음은 대부분 지역에서 사용할 수 있습니다. 자세한 내용은 참조 hello [키 자격 증명 모음 가격 책정 페이지](https://azure.microsoft.com/pricing/details/key-vault/)합니다.

## <a name="introduction"></a>소개
하나 이상의 키 자격 증명 모음을 만든 후 toomonitor, 액세스 및 업데이트 수행자는 키 자격 증명 모음 시기와 방법을 설정할 수 있습니다. Azure 저장소 계정에 제공하는 정보를 저장하는 키 자격 증명 모음에 대한 로깅을 사용하여 이를 수행할 수 있습니다. **insights-logs-auditevent** 라는 새 컨테이너가 지정된 저장소 계정에 대해 자동으로 만들어지고 여러 키 자격 증명 모음에 대한 로그를 수집하기 위해 이 저장소 계정을 사용할 수 있습니다.

최대 로깅 정보에 액세스할 수 있습니다, 자격 증명 모음 작업에 hello 키 후 10 분입니다. 대부분의 경우 이것보다 빠릅니다.  저장소 계정에 로그를 tooyou toomanage를입니다.

* 액세스할 수 있는 사용자를 제한 하 여 표준 Azure 액세스 제어 메서드 toosecure 로그를 사용 합니다.
* 저장소 계정에 tookeep 없게 하려면 로그를 삭제 합니다.

Azure 키 자격 증명 로깅, toocreate 시작 하기 자습서 toohelp이를 사용 하 여 저장소 계정의 로깅을 활성화 하 고 수집 된 hello 로깅 정보를 해석 합니다.  

> [!NOTE]
> 이 자습서는 toocreate 자격 증명 모음, 키 또는 암호를 입력 하는 방법에 대 한 지침을 다루지 않습니다. 자세한 내용은 [Azure 키 자격 증명 모음 시작](key-vault-get-started.md)을 참조하세요. 또는 플랫폼 간 명령줄 인터페이스 지침에 대한 참조는 [이 해당 자습서](key-vault-manage-with-cli2.md)를 참조하세요.
>
> 현재 hello Azure 포털에서에서 Azure 키 자격 증명 모음을 구성할 수 없습니다. 대신, 이 Azure PowerShell 지침을 사용합니다.
>
>

Azure 키 자격 증명 모음에 대한 개요는 [Azure 키 자격 증명 모음이란?](key-vault-whatis.md)

## <a name="prerequisites"></a>필수 조건
toocomplete이이 자습서에서는 다음 hello 있어야 합니다.

* 사용하고 있는 기존 키 자격 증명 모음  
* Azure PowerShell, **최소 버전 1.0.1**. Azure PowerShell tooinstall Azure 구독과 연결을 참조 하세요 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다. Azure PowerShell을 이미 설치 되어 있는 hello Azure PowerShell 콘솔에서 hello 버전 알지 못할 경우 입력 `(Get-Module azure -ListAvailable).Version`합니다.  
* 키 자격 증명 모음 로그에 대한 Azure의 충분한 저장소.

## <a id="connect"></a>Tooyour 구독 연결
Azure PowerShell 세션을 시작 하 고 다음 명령을 hello로 tooyour Azure 계정에에서 로그인 합니다.  

    Login-AzureRmAccount

Hello 팝업 브라우저 창에서 Azure 계정 사용자 이름 및 암호를 입력 합니다. Azure PowerShell에는 기본적으로이 계정은 관련 된 모든 hello 등록이 가져오며, 사용 하 여 첫 번째 hello 합니다.

다중 구독인 경우 해야할 toospecify 하나를 사용 하는 toocreate Azure 키 자격 증명 모음입니다. Hello toosee hello 구독 계정에 대해 다음을 입력 합니다.

    Get-AzureRmSubscription

그런 다음 toospecify hello 연결 된 구독으로 키 자격 증명 모음이 있습니다 로깅 됩니다, 유형:

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> 이 과정은 중요한 단계이며 사용자 계정에 여러 구독이 연결된 경우 특히 유용합니다. 이 단계를 건너뜁니다 오류 tooregister Microsoft.Insights 표시 될 수 있습니다.
>   
>

Azure PowerShell을 구성 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

## <a id="storage"></a>로그에 대한 새 저장소 계정 만들기
로그에 대 한 기존 저장소 계정을 사용 하 여 있지만 전용된 tooKey 자격 증명 모음 로그 수 있는 새 저장소 계정을 만들겠습니다. 편의 위해 때 했으므로 toospecify이에 대 한 hello 세부 정보 라는 변수를 저장할 것 이라면 **sa**합니다.

추가 관리 용이성도 사용 hello 우리의 주요 자격 증명 모음을 포함 하는 대로 동일한 리소스 그룹을 hello 합니다. Hello에서 [시작 자습서](key-vault-get-started.md),이 리소스 그룹 이름은 **ContosoResourceGroup** 및 toouse hello 동아시아 위치를 계속 실행 됩니다. 이 값을 적절하게 사용자 고유 값으로 대체합니다.

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> 사용 해야 toouse 기존 저장소 계정을 결정 한 경우 hello 클래식 배포 모델 보다는 hello 리소스 관리자 배포 모델을 사용 해야 하며 주요 자격 증명 모음으로 동일한 구독 hello 합니다.
>
>

## <a id="identify"></a>식별 하면 로그에 대 한 hello에 키 자격 증명 모음.
이 시작된 자습서 통해 주요 자격 증명 모음 이름 되었습니다 **ContosoKeyVault**이므로 이름을 지정 하 고 명명 된 변수로 hello 세부 정보를 저장 하는 toouse 노력할 것 **kv**:

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <a id="enable"></a>로깅 사용
tooenable hello 집합 AzureRmDiagnosticSetting cmdlet를 사용 합니다, hello 변수 함께 우리의 새 저장소 계정 및 우리의 주요 자격 증명 모음에 대해 만든 키 자격 증명 모음에 대 한 로깅, 합니다. Hello 바로잡을 수 또한 **-활성화** 너무 플래그**$true** hello 범주 tooAuditEvent (hello만 범주 키 자격 증명 모음 로깅에 대 한), 설정 및:

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

이 대 한 hello 출력에는 다음이 포함 됩니다.

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


로깅 주요 자격 증명 모음을 저장 하는 정보 tooyour 저장소 계정에 대 한 기능이 이제 확인 합니다.

선택적으로 오래된 로그를 자동으로 삭제하는 로그에 대한 보존 정책을 설정할 수도 있습니다. 예를 들어, 사용 하 여 보존 정책을 설정 **-RetentionEnabled** 너무 플래그**$true** 설정 **-RetentionInDays** 매개 변수가 너무**90** 하므로 90 일 보다 오래 된 로그가 자동으로 삭제 됩니다.

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

다음이 로깅됩니다.

* 액세스 권한, 시스템 오류 또는 잘못된 요청으로 인해 실패한 요청을 포함하는 모든 인증된 REST API 요청이 로깅됩니다.
* Hello 키에 대 한 작업 생성, 삭제, 주요 자격 증명 모음 액세스 정책 설정를 포함 하는 자체 자격 증명 모음 및 태그와 같은 주요 자격 증명 모음 특성을 업데이트 합니다.
* 키와 hello 키 자격 증명 모음에, 만들기, 수정 또는 삭제 이러한 키 또는 암호; 포함 하는 암호에 대 한 작업 기호 등의 작업 확인, 암호화, 암호를 해독, 줄 바꿈 및 unwrap 키, 암호, 키 나열 및 기밀 정보 및 해당 버전을 가져옵니다.
* 401 응답이 발생하는 인증되지 않은 요청. 예를 들어 전달자 토큰이 없거나 형식이 잘못되거나 만료되거나 토큰이 잘못된 요청이 해당합니다.  

## <a id="access"></a>로그에 액세스
주요 자격 증명 모음 로그 hello에 저장 됩니다 **insights-로그-auditevent** 제공한 hello 저장소 계정의 컨테이너입니다. toolist이이 컨테이너의 모든 hello blob를 입력 합니다.

먼저 hello 컨테이너 이름에 대 한 변수를 만듭니다. Hello 나머지 hello 연습을 전체에서 사용 됩니다.

    $container = 'insights-logs-auditevent'

toolist이이 컨테이너의 모든 hello blob를 입력 합니다.

    Get-AzureStorageBlob -Container $container -Context $sa.Context
hello 출력에는 다음과 유사한 toothis 표시 됩니다.

**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**

**Name**

- - -
**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****

이 출력을 알 수 있듯이 hello blob 명명 규칙을 지키는: **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>h / =<hour>/m =<minute>/filename.json**

UTC를 사용 하는 hello 날짜 및 시간 값입니다.

Hello 동일한 저장소 계정을 일 수 있으므로 여러 리소스에 대 한 로그를 사용 하는 toocollect hello 전체 리소스 ID hello blob 이름에는 매우 유용한 tooaccess 또는 필요한 정당한 hello blob를 다운로드 합니다. 그 전에 먼저 다룰 것 이지만 어떻게 toodownload blob hello 모든 합니다.

먼저 폴더 toodownload hello를 blob 만듭니다. 예:

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

그런 다음 모든 Blob 목록을 가져옵니다.  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

이 대상 폴더에 ' Get AzureStorageBlobContent' toodownload hello blob 통해이 목록을 파이프할:

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

이 두 번째 명령은 실행 하면 hello  **/**  hello blob 이름에 구분 기호가 hello 대상 폴더에서 전체 폴더 구조를 만들고이 구조체 파일로 toodownload 및 저장소 hello blob 사용된 됩니다.

tooselectively는 blob 다운로드 전용, 와일드 카드를 사용 합니다. 예:

* 여러 키 자격 증명 모음 있고 하나의 키 자격 증명 모음에 대해 toodownload 로그를 원하는 경우 CONTOSOKEYVAULT3 이라는 입력 합니다.

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* 리소스 그룹이 여러 개 있는 하나의 리소스 그룹에 대 한 toodownload 로그를 사용할 경우 사용 하 여 `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* 사용 하 여 2016 년 1 월의 hello 월에 대 한 모든 hello 로그 toodownload 않으려면 `-Blob '*/year=2016/m=01/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

Hello에 무엇이 살펴보면 준비 toostart 로그 이제 것입니다. 으로 하는 Get AzureRmDiagnosticSetting tooknow이 필요할 수 있습니다에 대 한 매개 변수 두 개를 더 진행 하기 전에:

* 주요 자격 증명 모음 리소스에 대 한 진단 설정의 tooquery hello 상태:`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`
* 주요 자격 증명 모음 리소스에 대 한 toodisable 로깅:`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`

## <a id="interpret"></a>Key Vault 로그 해석
개별 Blob은 JSON Blob 형식으로 텍스트로 저장됩니다. 다음은 `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`을 실행하는 예제 로그 항목입니다.

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


hello 다음 표에 나열 hello 필드 이름 및 설명 합니다.

| 필드 이름 | 설명 |
| --- | --- |
| 실시간 |날짜 및 시간(UTC) |
| resourceId |Azure 리소스 관리자 리소스 ID. 주요 자격 증명 모음 로그의 경우이 항상 hello 키 자격 증명 모음 리소스 id입니다. |
| operationName |Hello 다음 표에 설명 된 대로 hello 작업의 이름입니다. |
| operationVersion |Hello 클라이언트에서 요청한 hello REST API 버전입니다. |
| 카테고리 |주요 자격 증명 모음 로그 AuditEvent hello를 사용할 수 있는 단일 값입니다. |
| resultType |REST API 요청 결과입니다. |
| resultSignature |HTTP 상태입니다. |
| resultDescription |사용 가능한 경우 hello 결과 대 한 자세한 설명입니다. |
| durationMS |밀리초 단위로 tooservice hello REST API 요청에 소요 된 시간입니다. Hello 클라이언트 쪽에서 측정 hello 시간이 이번 일치 하지 않을 수 있으므로 hello 네트워크 대기 시간, 포함 되지 않습니다. |
| callerIpAddress |Hello 요청을 수행한 hello 클라이언트의 IP 주소입니다. |
| CorrelationId |클라이언트 hello 선택적 GUID가 toocorrelate 서비스 측 (키 자격 증명 모음) 로그를 사용 하 여 클라이언트 쪽 로그를 전달할 수 있습니다. |
| ID |Hello REST API 요청을 만드는 경우에 발표 hello 토큰에서 id입니다. Azure PowerShell cmdlet에서 발생하는 요청의 경우처럼 이는 보통 "사용자", "서비스 주체" 또는 "사용자+appId"의 조합입니다. |
| properties |이 필드는 hello 작업 (작업 이름)에 따라 다른 정보가 포함 됩니다. 대부분의 경우에는 클라이언트 정보가 (hello useragent에서 전달 된 문자열 hello 클라이언트), 들어 hello 정확한 REST API 요청 URI 및 HTTP 상태 코드입니다. 또한 개체 (예를 들어 KeyCreate 또는 VaultGet) 요청의 결과로 반환 될 때 키 URI ("id")로, 자격 증명 모음 URI 또는 URI 비밀 hello를 포함 됩니다. |

hello **operationName** 필드 값은 ObjectVerb 형식입니다. 예:

* 모든 주요 자격 증명 모음 작업 체계가 hello ' 자격 증명 모음`<action>`' 형식으로 `VaultGet` 및 `VaultCreate`합니다.
* 모든 주요 작업 체계가 hello ' 키`<action>`' 형식으로 `KeySign` 및 `KeyList`합니다.
* 모든 보안 작업 체계가 hello ' 비밀`<action>`' 형식으로 `SecretGet` 및 `SecretListVersions`합니다.

다음 표에서 hello hello operationName 및 해당 하는 REST API 명령을 나열 합니다.

| operationName | REST API 명령 |
| --- | --- |
| 인증 |Azure Active Directory 끝점을 통해 |
| VaultGet |[키 자격 증명 모음에 대한 정보 가져오기](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| VaultPut |[키 자격 증명 모음 만들기 또는 업데이트](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| VaultDelete |[키 자격 증명 모음 삭제](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| VaultPatch |[키 자격 증명 모음 업데이트](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| VaultList |[리소스 그룹의 모든 키 자격 증명 모음 목록](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| KeyCreate |[키 만들기](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| KeyGet |[키에 대한 정보 가져오기](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| KeyImport |[자격 증명 모음으로 키 가져오기](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| KeyBackup |[키 백업](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx). |
| KeyDelete |[키 삭제](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| KeyRestore |[키 복원](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| KeySign |[키로 서명](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| KeyVerify |[키로 확인](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| KeyWrap |[키 래핑](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| KeyUnwrap |[키 래핑 취소](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| KeyEncrypt |[키로 암호화](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| KeyDecrypt |[키로 암호 해독](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| KeyUpdate |[키 업데이트](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| KeyList |[자격 증명 모음의 hello 키 나열](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| KeyListVersions |[키의 hello 버전 나열](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| SecretSet |[암호 만들기](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| SecretGet |[암호 가져오기](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| SecretUpdate |[암호 업데이트](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| SecretDelete |[암호 삭제](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| SecretList |[자격 증명 모음에 암호 나열](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| SecretListVersions |[암호 버전 나열](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <a id="loganalytics"></a>Log Analytics 사용

로그 분석 tooreview Azure 키 자격 증명 모음 AuditEvent 로그에서 hello Azure 키 자격 증명 모음 솔루션을 사용할 수 있습니다. 를 비롯 한 자세한 내용은 tooset,이 확인 하려면 어떻게 [로그 분석에서 Azure 키 자격 증명 모음 솔루션](../log-analytics/log-analytics-azure-key-vault.md)합니다. 또한이 문서 toomigrate hello 로그 분석 미리 보기, 먼저 Azure 저장소 계정에 로그 tooan 라우팅된 하 고 있는 로그 분석 tooread 여기에서 구성 하는 동안 제공 된 hello 이전 하는 주요 자격 증명 모음 솔루션에서 해야 할 경우 지침을 포함 합니다.

## <a id="next"></a>다음 단계
웹 응용 프로그램에서 Azure Key Vault를 사용하는 자습서는 [웹 응용 프로그램에서 Azure Key Vault 사용](key-vault-use-from-web-application.md)을 참조하세요.

프로그래밍 참조에 대 한 참조 [Azure 키 자격 증명 모음 개발자 가이드 hello](key-vault-developers-guide.md)합니다.

Azure Key Vault의 Azure PowerShell 1.0 cmdlet 목록은 [Azure Key Vault Cmdlet](/powershell/module/azurerm.keyvault/#key_vault)을 참조하세요.

키 회전 및 Azure 키 자격 증명 감사 로그에 대 한 자습서를 참조 하십시오. [끝 tooend와 toosetup 키 자격 증명 모음 키 회전 및 감사 어떻게](key-vault-key-rotation-log-monitoring.md)합니다.
