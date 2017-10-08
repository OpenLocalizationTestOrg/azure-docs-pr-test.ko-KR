---
title: "Azure 키 자격 증명 모음을 종단 간 키 회전 및 감사 aaaSet | Microsoft Docs"
description: "키 회전 및 모니터링 주요 자격 증명 모음 로그 설정 가져오기 방법 tootoohelp이를 사용 합니다."
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: e0c393873077e3b91adc9fa7f39128bc1b6abe26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a>종단 간 키 회전 및 감사를 사용하여 Azure Key Vault 설정
## <a name="introduction"></a>소개
주요 자격 증명 모음을 만든 후 해당 자격 증명 모음 toostore 키와 암호를 사용 하 여 수 toostart 수 있습니다. 응용 프로그램 키 또는 암호를 toopersist 더 이상 필요는 없지만 대신 요청으로 hello 키 자격 증명 모음에서 필요에 따라. 이렇게 하면 있습니다 tooupdate 키와 암호 hello 응용 프로그램의 동작을 다양 한 키와 비밀 관리 가능성을 열 수 있는 영향을 주지 않고.

이 경우 응용 프로그램에 의해 액세스 되는 Azure 저장소 계정 키의 암호를 toostore Azure 키 자격 증명 모음을 사용 하는 예제를 통해이 문서에서는 안내 합니다. 또한 해당 저장소 계정 키의 예약된 회전 구현에 대해서도 살펴봅니다. 마지막으로, toomonitor 주요 자격 증명 모음 감사 로그 hello 하 고 예기치 않은 요청을 만들 때 경고를 발생 하는 방법의 데모를 안내 합니다.

> [!NOTE]
> 이 자습서에에서 없는 경우 의도 한 tooexplain 주요 자격 증명 모음의 세부 hello 초기 설치 자세한 내용은 [Azure 키 자격 증명 모음 시작](key-vault-get-started.md)을 참조하세요. 플랫폼 간 명령줄 인터페이스 지침은 [CLI를 사용하여 Key Vault 관리](key-vault-manage-with-cli2.md)를 참조하세요.
>
>

## <a name="set-up-key-vault"></a>주요 자격 증명 모음 설정
응용 프로그램 tooretrieve 비밀 tooenable 주요 자격 증명에서 먼저 hello 암호를 만들고 해야 tooyour 자격 증명 모음에 업로드 합니다. Azure PowerShell 세션을 시작 하 고 로그인 tooyour Azure 계정 hello 다음 명령을 사용 하 여이 수행할 수 있습니다.

```powershell
Login-AzureRmAccount
```

Hello 팝업 브라우저 창에서 Azure 계정 사용자 이름 및 암호를 입력 합니다. PowerShell이이 계정과 연결 된 모든 hello 구독을 받습니다. PowerShell 사용 하 여 hello 기본적으로 첫 번째입니다.

여러 구독이 있는 하는 경우에 주요 자격 증명 모음을 사용 하는 toocreate 인 hello toospecify를 할 수 있습니다. Hello toosee hello 구독 계정에 대해 다음을 입력 합니다.

```powershell
Get-AzureRmSubscription
```

toospecify hello 연결 된 구독으로 로그인 수는 경우, hello 키 자격 증명을 입력 합니다.

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

이 문서에서는 저장소 계정 키를 비밀로 저장하는 방법을 설명하므로 해당 저장소 계정 키를 가져와야 합니다.

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

본인에 (이 경우 저장소 계정 키)를 검색 한 후 해당 tooa 보안 문자열을 변환한 다음 해당 값을 가진 주요 자격 증명 모음에서 암호를 만듭니다.

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
다음으로 만든 hello 암호에 대 한 hello를 URI를 가져옵니다. Hello 주요 자격 증명 모음 tooretrieve 본인을 호출 하는 경우이 이후 단계에서 사용 됩니다. Hello 다음 PowerShell 명령을 실행 하 고 hello 암호로 URI hello ID 값을 기록해 둡니다.

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a>Hello 응용 프로그램 설정
저장 되는 암호를가지고 코드 tooretrieve를 사용할 수 있으며 사용. 가지가 몇 가지 단계 필요한 tooachieve이 있습니다. hello 첫 번째 이자 가장 중요 한 단계는 응용 프로그램을 Azure Active Directory 등록 이며 다음 응용 프로그램에서 요청을 허용할 수 있도록 응용 프로그램 정보 자격 증명 모음 키를 지시 합니다.

> [!NOTE]
> 응용 프로그램에 만들어야 hello 동일한 주요 자격 증명 모음으로 Azure Active Directory 테 넌 트입니다.
>
>

Azure Active Directory의 hello 응용 프로그램 탭을 엽니다.

![Azure Active Directory에서 응용 프로그램 열기](./media/keyvault-keyrotation/AzureAD_Header.png)

선택 **추가** tooadd 응용 프로그램 tooyour Azure Active Directory 합니다.

![[추가] 선택](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

Hello 응용 프로그램 유형으로 둡니다 **웹 응용 프로그램 및/또는 웹 API** 하 고 응용 프로그램 이름을 지정 합니다.

![이름 hello 응용 프로그램](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

응용 프로그램에 **로그온 URL** 및 **앱 ID URI**를 제공합니다. 이 데모에서는 사용자가 원하는 어떤 것이라도 가능하며 필요한 경우 나중에 변경할 수 있습니다.

![필요한 URI 제공](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

Hello 응용 프로그램 tooAzure Active Directory를 추가한 후 hello 응용 프로그램 페이지로 이동 됩니다. Hello 클릭 **구성** 탭 하 고 다음 찾아서 복사할 hello **클라이언트 ID** 값입니다. 이후 단계에 대 한 hello 클라이언트 ID를 기록해 둡니다.

다음으로, Azure Active Directory와 상호 작용할 수 있도록 응용 프로그램에 대한 키를 생성합니다. Hello에서 만들 수 있습니다 **키** hello 섹션인 **구성** 탭 합니다. 이후 단계에서 새로 생성 하는 hello Azure Active Directory 응용 프로그램에서 사용할 수 있도록 키를 메모를 확인 합니다.

![Azure Active Directory 앱 키](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

Hello 주요 자격 증명 모음에 응용 프로그램에서 모든 호출을 설정 하기 전에 응용 프로그램 및 해당 사용 권한을 대 한 hello 주요 자격 증명 모음을 알려야 합니다. hello 다음 명령에서는 hello 자격 증명 모음 이름 및 Azure Active Directory 응용 프로그램 및 부여에서 클라이언트 ID hello **가져오기** 액세스 tooyour 주요 자격 증명 모음 hello 응용 프로그램에 대 한 합니다.

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

이 시점에서 응용 프로그램이 호출 작성 준비 toostart 됩니다. 응용 프로그램에서 Azure 키 자격 증명 모음 및 Azure Active Directory와 hello NuGet 패키지가 필요한 toointeract를 설치 해야 합니다. Hello Visual Studio 패키지 관리자 콘솔에서 다음 명령을 hello를 입력 합니다. 이 문서의 hello 문서 작성 당시 hello hello Azure Active Directory 패키지의 최신 버전 이므로 3.10.305231913, tooconfirm hello에 대 한 최신 정보를 원하는 고에 따라 업데이트 될 수 있습니다.

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

응용 프로그램 코드에서 Azure Active Directory 인증에 대 한 클래스 toohold hello 메서드를 만듭니다. 이 예제에서 이 클래스는 **Utils**입니다. Hello 다음 추가 문을 사용 하 여:

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

다음으로 hello 메서드 tooretrieve hello JWT 토큰을 Azure Active Directory에서 다음을 추가 합니다. 유지 관리의 편의성 웹 또는 응용 프로그램 구성에 toomove hello 하드 코드 된 문자열 값 수도 있습니다.

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

Hello 필요한 코드 toocall 주요 자격 증명 모음을 추가 하 고 사용자가 본인 확인 값을 검색 합니다. 먼저 추가한 다음 hello 다음 문을 사용 하 여:

```csharp
using Microsoft.Azure.KeyVault;
```

Hello 메서드 호출 tooinvoke 주요 자격 증명 모음을 추가 하 고 본인을 검색 합니다. 이 방법에서는 hello 암호는 이전 단계에서 저장 하는 URI를 제공 합니다. Hello hello 사용 **GetToken** hello 메서드에서 **유틸리티** 이전에 만든 클래스입니다.

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

응용 프로그램을 실행 하면 있습니다 해야 이제 인증을 받게 tooAzure Active Directory 및 Azure 키 자격 증명 모음에서 다음 프로그램 비밀 값을 검색 합니다.

## <a name="key-rotation-using-azure-automation"></a>Azure Automation을 사용하여 키 회전
Azure 주요 자격 증명 모음 암호 정보로 저장하는 값을 위한 회전 전략을 구현하는 다양한 옵션이 있습니다. 수동 프로세스의 일부로 비밀을 회전할 수 있으며 API 호출을 활용하여 프로그래밍 방식으로 회전하거나 Automation 스크립트 방식으로 회전할 수 있습니다. 이 문서의 hello 위해 됩니다 Azure PowerShell을 사용 하 여 함께 Azure 자동화 toochange Azure 저장소 계정 액세스 키입니다. 그런 다음 해당 새 키를 사용하여 Key Vault 비밀을 업데이트합니다.

tooallow Azure 자동화 tooset 비밀 값 주요 자격 증명 모음에서 Azure 자동화 인스턴스를 설정할 때 생성 된 AzureRunAsConnection 라는 hello 연결에 대 한 hello 클라이언트 ID를 발생 합니다. Azure Automation 인스턴스에서 **자산**을 선택하여 이 ID를 가져올 수 있습니다. 여기에서 선택 **연결** 선택한 후 hello **AzureRunAsConnection** 원칙 서비스입니다. Hello를 메모해 **응용 프로그램 ID**합니다.

![Azure Automation 클라이언트 ID](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

**자산**에서 **모듈**을 선택합니다. **모듈**선택, **갤러리**, 한 다음 검색 하 고 **가져오기** 각각 hello 다음 모듈의 업데이트 된 버전:

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> 이 문서의 hello 문서 작성 당시만 hello 필요한 이전에 메모 모듈 toobe 업데이트 스크립트를 다음 hello에 대 한 합니다. 자동화 작업이 실패하는 것으로 확인되면 필요한 모든 모듈과 해당 종속성을 가져왔는지 확인해야 합니다.
>
>

Azure 자동화 연결에 대 한 hello 응용 프로그램 ID를 검색 한 후 알려야 주요 자격 증명 모음 자격 증명 모음에서이 응용 프로그램 액세스 tooupdate 비밀 정보에는 합니다. 다음 PowerShell 명령을 hello로이 수행할 수 있습니다.

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

다음으로 Azure Automation 인스턴스 아래에서 **Runbooks**을 선택하고 **Runbook 추가**를 선택합니다. **빠른 생성**을 선택합니다. Runbook 이름을 지정 하 고 선택 **PowerShell** hello runbook 형식입니다. Hello 옵션 tooadd 설명을 해야합니다. 마지막으로 **만들기**를 클릭합니다.

![runbook 만들기](./media/keyvault-keyrotation/Create_Runbook.png)

새 runbook에 대 한 hello 편집기 창에서 PowerShell 스크립트 뒤 hello를 붙여 넣습니다.

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get hello connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in tooAzure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set hello following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for hello storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

Hello 편집기 창에서 선택 **테스트 창** tootest 스크립트입니다. Hello 스크립트가 오류 없이 실행 되 고, 선택할 수 있습니다 **게시**, 다음 hello runbook 구성 창에서 다시 hello runbook에 대 한 일정을 적용할 수 있습니다.

## <a name="key-vault-auditing-pipeline"></a>Key Vault 감사 파이프라인
주요 자격 증명 모음을 설정할 때 감사 액세스 요청이 toohello 주요 자격 증명 모음에 toocollect 로그 켤 수 있습니다. 이러한 로그는 지정된 Azure Storage 계정에 저장되며 끌어내기, 모니터링 및 분석이 가능합니다. hello 다음과 같은 시나리오 사용 Azure 함수, Azure 논리 앱 및 주요 자격 증명 모음 감사 로그 toocreate 파이프라인 toosend 전자 메일이 hello 웹 앱의 hello 응용 프로그램 ID와 일치 하는 응용 프로그램 hello 자격 증명 모음에서 암호를 검색 합니다.

먼저 Key Vault에서 로깅을 사용하도록 설정해야 합니다. Hello 다음 PowerShell 명령을 통해이 작업을 수행할 수 있습니다 (전체 세부 정보에서 볼 수 있습니다 [키 자격 증명 모음 로깅](key-vault-logging.md)):

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

이 활성화 된 후 감사 저장소 계정을 지정 하는 hello에 수집 시작을 기록 합니다. 이러한 로그에는 Key Vault를 어떻게, 언제, 누가 액세스하는지에 대한 이벤트가 포함됩니다.

> [!NOTE]
> 10 분 후 hello 키 자격 증명 모음 작업 로깅 정보에 액세스할 수 있습니다. 이 시간은 일반적으로 10분보다 짧습니다.
>
>

hello 다음 단계는 너무[Azure 서비스 버스 큐 만들기](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)합니다. 여기에 Key Vault 감사 로그가 푸시됩니다. Hello 감사 로그 메시지 hello 큐에 있는 경우 hello 논리 앱은을 선택 하 고에 작동 합니다. 단계를 수행 하는 hello로 서비스 버스를 만듭니다.

1. 서비스 버스 네임 스페이스 만들기 (이미 있는 경우 원하는 toouse이를 건너뜁니다 tooStep 2).
2. Azure 포털 hello 및 선택 hello 네임 스페이스 toocreate hello 큐에서 원하는 toohello 서비스 버스를 찾습니다.
3. 선택 **새로** 선택 **서비스 버스 > 큐** hello 필요한 세부 정보를 입력 합니다.
4. Hello 네임 스페이스를 선택 하 고 클릭 하 여 hello 서비스 버스 연결 정보를 선택 **연결 정보**합니다. Hello 다음 섹션에이 정보가 필요 합니다.

그런 다음, [Azure 함수를 만들](../azure-functions/functions-create-first-azure-function.md) toopoll 주요 자격 증명 모음 로그 내 저장소 계정을 hello 및 새 이벤트를 선택 합니다. 그러면 일정에 따라 트리거되는 함수가 됩니다.

toocreate Azure에서 함수를 선택 **새로 만들기 > 함수 앱** hello Azure 포털의에서. 만들기 중에 기존 호스팅 계획을 사용하거나 새 계획을 만들 수 있습니다. 동적 호스팅을 선택할 수도 있습니다. 호스팅 옵션 함수에 대 한 자세한 내용은에서 확인할 수 있습니다 [어떻게 tooscale Azure 함수](../azure-functions/functions-scale.md)합니다.

Hello Azure 함수를 만들면 tooit를 탐색 하 고 함수와 C 타이머를 선택할\#합니다. 그런 다음 **이 함수 만들기**를 클릭합니다.

![Azure Functions 시작 블레이드](./media/keyvault-keyrotation/Azure_Functions_Start.png)

Hello에 **개발** 탭, hello run.csx 코드 hello 다음 코드로 바꿉니다.

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting toonow.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required tooorder by time as they may not be in hello file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending tooServiceBus, use hello payloadStream and set keeporiginal tootrue
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> Hello 앞 코드 toopoint tooyour 저장소 계정 키 자격 증명 모음 로그 hello 기록 되므로, 이전에 만든 hello 서비스 버스에에서 있는지 tooreplace hello 변수를 확인 하 고 특정 경로 toohello 주요 자격 증명 모음 저장소 로그 hello 키를 누릅니다.
>
>

hello 함수 hello 최신 로그 hello 저장소 계정에서 여기서 hello 주요 자격 증명 모음 로그 기록 된 파일, grabs의 hello 최신 이벤트를 해당 파일을 선택 하 고 tooa 서비스 버스 큐를 푸시합니다. 단일 파일에는 여러 이벤트가 있을 수 있습니다, 때문 sync.txt 파일 hello 함수를 받았음을 hello 마지막 이벤트의 toodetermine hello 타임 스탬프도 확인을 만들어야 합니다. 이렇게 하면 푸시 하지 않는 같은 이벤트가 여러 번 hello 합니다. 이 sync.txt 파일 hello 마지막 발생 한 이벤트에 대 한 타임 스탬프를 포함 합니다. hello 로그, 로드 되 면가 정렬 toobe 기반으로 hello 타임 스탬프 tooensure 바르게 정렬 됩니다.

이 함수에 대 한 몇 가지 Azure 함수에서 hello 상자를 사용할 수 없는 추가 라이브러리 참조할 수 있습니다. tooinclude 이러한 Azure 함수 toopull 필요한 NuGet을 사용 하 게 합니다. Hello 선택 **파일 보기** 옵션입니다.

![보기 파일 옵션](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

project.json이라는 파일에 다음 콘텐츠를 추가합니다.

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
시 **저장**, Azure 함수 hello 필요한 이진 파일을 다운로드 합니다.

Toohello 전환 **통합** 탭 및 hello 함수 내에서 의미 있는 이름을 toouse hello 타이머 매개 변수를 제공 합니다. 호출 하는 hello 타이머 toobe 것 예상 hello 코드 앞에, *myTimer*합니다. 지정 된 [CRON 식](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) 다음과 같이: 0 \* \* \* \* \* hello 함수 toorun 1 분 마다 발생 시키는 hello 타이머에 대 한 합니다.

에 동일한 hello **통합** 탭에서 추가 hello 형식의 입력 **Azure Blob 저장소**합니다. 이 hello 마지막 이벤트를 감시 한 hello 함수 hello 타임 스탬프를 포함 하는 toohello sync.txt 파일을 가리킵니다. 이 hello 매개 변수 이름 사용 하 여 hello 기능 내에서 사용할 수 있습니다. Hello 코드 앞에에서 hello Azure Blob 저장소 입력 매개 변수 이름 toobe hello를 16 *inputBlob*합니다. Hello sync.txt 파일 상주할 hello 저장소 계정을 선택 (수도 hello 같거나 다른 저장소 계정). Hello 경로 필드에서 hello 파일 hello 형식 {container-name}/path/to/sync.txt 거주 하는 hello 경로 제공 합니다.

Hello 형식의 출력 추가 *Azure Blob 저장소* 출력 합니다. 이 hello 입력에 정의 된 toohello sync.txt 파일을 가리킵니다. 이 hello 함수 toowrite hello 이벤트의 타임 스탬프 hello 마지막에 검토 하 여 사용 됩니다. hello 앞의 코드에서는이 매개 변수 toobe 호출 *outputBlob*합니다.

이 시점에서 hello 함수는 준비 합니다. 있는지 tooswitch 백 toohello 확인 **개발** 탭 및 hello 코드를 저장 합니다. 컴파일 오류에 대 한 hello 출력 창을 확인 및 해결 하는 적절 하 게 합니다. Hello 코드가 컴파일 hello 코드는 이제 수 로그를 확인 hello 주요 자격 증명 모음 1 분 마다 서비스 버스 큐를 정의 된 hello에 새 이벤트를 밀어 그리고 합니다. Hello 함수 트리거될 때마다 toohello 로그 창을 작성 하는 로깅 정보를 볼 수 있습니다.

### <a name="azure-logic-app"></a>Azure 논리 앱
그런 다음 하 hello 함수 toohello 서비스 버스 큐에 푸시합니다, hello 콘텐츠를 구문 분석 하 고 보냅니다 하 게 일치 하는 조건에 따라 전자 메일 hello 이벤트를 선택 하는 Azure 논리 앱을 만들어야 합니다.

[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md) 너무 이동 하 여**새로 만들기 > 논리 앱**합니다.

Hello 논리 앱을 만든 후 tooit를 탐색 하 고 선택할 **편집**합니다. Hello 논리가 응용 프로그램 편집기 내에서 선택 **서비스 버스 큐** 서비스 버스 자격 증명 tooconnect 입력 것 toohello 큐입니다.

![Azure 논리 앱 서비스 버스](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

다음으로 **조건 추가**를 선택합니다. Hello 조건 toohello 고급 편집기를 전환 하 고 코드 다음, hello로 APP_ID 대체 hello 입력 웹 응용 프로그램의 실제 APP_ID:

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

이 식은 기본적으로 반환 **false** 경우 hello *appid* (즉, hello hello 서비스 버스 메시지 본문) 들어오는 이벤트 hello 하지는 hello *appid* hello의 응용 프로그램입니다.

이제 **아니요인 경우, 아무 작업도 수행하지 않습니다** 옵션 아래에서 작업을 만듭니다.

![Azure 논리 앱 선택 작업](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

Hello 동작에 대 한 선택 **Office 365-전자 메일 보내기**합니다. Hello 필드 toocreate 메일 toosend 때 채워야 hello 정의 조건 반환 **false**합니다. Office 365가 없는 경우에 대안 살펴볼 수 있습니다 tooachieve hello 동일한 결과입니다.

이 시점에서 1 분 마다 새 주요 자격 증명 모음 감사 로그를 검색 하는 최종 tooend 파이프라인을 해야 합니다. Tooa 서비스 버스 큐를 찾으면 새 로그를 푸시합니다. hello 논리 앱은 hello 큐에 새 메시지가 삽입 하는 경우에 트리거됩니다. 경우 hello *appid* hello 내에서 이벤트의 응용 프로그램을 호출 하는 hello hello 앱 ID 일치 하지 않습니다, 전자 메일을 보냅니다.
