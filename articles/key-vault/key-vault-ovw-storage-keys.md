---
ms.assetid: 
title: "aaaAzure 키 자격 증명 모음 저장소 계정 키"
description: "저장소 계정 키 Azure 키 자격 증명 모음 키 기반된 액세스 tooAzure 저장소 계정 사이의 곧바로 통합 기능을 제공 합니다."
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: becdf97798a08164c48d3a7a14aea6ca54085c9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-storage-account-keys"></a>Azure Key Vault Storage 계정 키

Azure 키 자격 증명 모음 저장소 계정 키를 하기 전에 개발자 toomanage 자체 Azure 저장소 계정 (ASA) 키가와 수동으로 또는 외부 자동화를 통해 회전 합니다. 이제 Key Vault Storage 계정 키가 Azure Storage 계정에 인증하기 위한 [Key Vault 암호](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets)로 구현됩니다. 

hello ASA 핵심 기능은 비밀 회전을 관리 하 고 공유 액세스 서명 (SAS) 메서드로 제공 하 여 ASA 키로 직접 연락처에 대 한 hello 요구를 제거 합니다. 

Azure Storage 계정에 대한 일반적인 내용은 [Azure storage 계정 정보](https://docs.microsoft.com/azure/storage/storage-create-storage-account)를 참조하세요.

## <a name="supporting-interfaces"></a>인터페이스 지원

hello Azure 저장소 계정 키 기능 초기에.NET hello REST 통해 C# 및 PowerShell 인터페이스 /입니다. 자세한 내용은 [Key Vault 참조](https://docs.microsoft.com/azure/key-vault/)를 참조하세요.


## <a name="storage-account-keys-behavior"></a>저장소 계정 키 동작

### <a name="what-key-vault-manages"></a>Key Vault에서 관리하는 사항

저장소 계정 키를 사용할 경우 Key Vault에서 사용자 대신 여러 가지 내부 관리 기능을 수행합니다.

1. Azure Key Vault는 ASA(Azure Storage Account)의 키를 관리합니다. 
    - 내부적으로 Azure Key Vault는 키와 Azure Storage 계정을 나열(동기화)할 수 있습니다.  
    - Azure 주요 자격 증명을 다시 생성 (회전) hello 정기적으로 키입니다. 
    - 키 값 toocaller 응답에서에서 반환 되지 않습니다. 
    - Azure Key Vault는 저장소 계정과 클래식 저장소 계정 둘 다의 키를 관리합니다. 
2. Azure 키 자격 증명 모음에는 사용자, 자격 증명 모음/개체 소유자 hello, toocreate SAS (계정 또는 서비스 SAS) 정의 수 있습니다. 
    - hello SAS 값 SAS 정의 사용 하 여 만든 hello REST URI 경로 통해 암호도 반환 됩니다. 자세한 내용은 [Azure Key Vault 저장소 계정 작업](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations)을 참조하세요.

### <a name="naming-guidance"></a>명명 지침

저장소 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 포함할 수 있습니다.  
 
SAS 정의 이름은 1-102자로, 0-9, a-z, A-Z만 포함해야 합니다.

## <a name="developer-experience"></a>개발자 환경 

### <a name="before-azure-key-vault-storage-keys"></a>Azure Key Vault Storage 키 이전 

개발자는 저장소 계정 키 tooget 액세스 tooAzure 저장소와 사례 tooneed toodo hello를 사용 합니다. 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a>Azure Key Vault Storage 키 이후 

```
//Please make sure tooset storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command tooget Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using hello SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and hello Blob storage endpoint toocreate a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about tooexpire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a>개발자 모범 사례 

- ASA 키 자격 증명 모음 키 toomanage 허용 합니다. Toomanage 마십시오으로 키 자격 증명 모음의 프로세스와 충돌할 됩니다, 직접 합니다. 
- ASA 키 toobe 둘 이상의 키 자격 증명 모음 개체에 의해 관리 되는 허용 하지 않습니다. 
- 필요한 경우 toomanually ASA 키 다시 생성, 키 자격 증명 모음을 통해 재생성 하는 것이 좋습니다. 

## <a name="getting-started"></a>시작

### <a name="setup-for-role-based-access-control-rbac-permissions"></a>RBAC(역할 기반 액세스 제어) 권한 설정

주요 자격 증명 모음 필요한 권한이 너무*목록* 및 *다시 생성* 저장소 계정에 대 한 키입니다. 단계를 수행 하는 hello를 사용 하 여 이러한 권한을 설정 합니다.

- Key Vault의 ObjectId를 가져옵니다. 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- 저장소 키 연산자 역할 tooAzure 키 자격 증명 모음 Identity를 지정 합니다. 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > 클래식 계정 유형에 대 한 hello 역할 매개 변수를 너무 설정*"클래식 저장소 계정 키 연산자 서비스 역할"*합니다.

### <a name="storage-account-onboarding"></a>저장소 계정 등록 

예:으로 저장소를 추가한 키 자격 증명 모음의 개체 소유자 계정을 개체 tooyour Azure 키 자격 증명 모음 tooonboard 저장소 계정입니다.

등록 하는 동안 키 자격 증명 모음 필요한 hello 온 보 딩 계정의 hello id에 대 한 권한이 너무 tooverify*목록* 및 너무*다시 생성* 저장소 키입니다. 주문 tooverify 이러한 사용 권한, 주요 자격 증명 모음 토큰을 가져옵니다는 OBO (On를 대신 하 여의) hello 인증 서비스에서 대상 그룹 tooAzure 리소스 관리자를 설정 하 고 만듭니다는 *목록* 키 toohello Azure 저장소 서비스를 호출 합니다. 경우 hello *목록* 호출이 실패, 개체 생성의 HTTP 상태 코드와 함께 실패 키 자격 증명 모음 hello *사용할 수 없음*합니다. 이러한 방식으로 나열 된 hello 키 엔터티 저장 장치를 키 자격 증명 모음과 함께 캐시 됩니다. 

주요 자격 증명 모음 hello id가가지고 있는지 확인 해야 *다시 생성* 사용 권한을 다시 생성 하 여 키의 소유권을 만들 수 있습니다. OBO 토큰을 통해 id hello 수 있을 뿐 아니라 첫 번째 파티 id를 키 자격 증명 모음 hello 있는 tooverify에 이러한 권한이 있습니다.

- 주요 자격 증명 모음에는 RBAC hello 저장소 계정 리소스에 대 한 권한을 나열합니다.
- 주요 자격 증명 모음 작업 및 비 작업의 정규식 일치를 통해 hello 응답의 유효성을 검사 합니다. 

[Key Vault - Managed Storage 계정 키 샘플](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167)에서 지원하는 몇 가지 예제를 찾습니다.

Hello identity에 없는 경우 *다시 생성* 사용 권한 또는 없는 첫 번째 파티 id를 키 자격 증명 모음의 경우 *목록* 또는 *다시 생성* 권한, 다음 hello 온 보 딩 요청이 실패는 적절 한 오류 코드와 메시지를 반환 합니다. 

hello OBO 토큰 첫 번째 파티, PowerShell 또는 CLI의 네이티브 클라이언트 응용 프로그램을 사용 하는 경우에 작동 합니다.

## <a name="other-applications"></a>다른 응용 프로그램

- 키 자격 증명 모음 저장소 계정 키를 사용 하 여 생성 되는 SAS 토큰에 더 많은 액세스 제어 tooan Azure 저장소 계정 제공 합니다. 자세한 내용은 [공유 액세스 서명 사용](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)을 참조하세요.

## <a name="see-also"></a>참고 항목

- [키, 비밀 및 인증서에 대한 정보](https://docs.microsoft.com/rest/api/keyvault/)
- [Key Vault 팀 블로그](https://blogs.technet.microsoft.com/kv/)
