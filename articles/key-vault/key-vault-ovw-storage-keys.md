---
ms.assetid: 
title: "Azure Key Vault Storage 계정 키"
description: "저장소 계정 키는 Azure Key Vault 간의 원활한 통합과 Azure Storage 계정에 대한 키 기반 액세스를 제공합니다."
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: 3148088c88236c64e089fd25c98eb8ac7cdcbfea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="d2d4d-103">Azure Key Vault Storage 계정 키</span><span class="sxs-lookup"><span data-stu-id="d2d4d-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="d2d4d-104">Azure Key Vault Storage 계정 키 이전에는 개발자가 고유한 ASA(Azure Storage 계정) 키를 관리하고 수동으로 또는 외부 자동화를 통해 회전해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-104">Before Azure Key Vault Storage Account Keys, developers had to manage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="d2d4d-105">이제 Key Vault Storage 계정 키가 Azure Storage 계정에 인증하기 위한 [Key Vault 암호](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets)로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span> 

<span data-ttu-id="d2d4d-106">ASA 키 기능은 자동으로 암호 회전을 관리하고 SAS(공유 액세스 서명)를 방법으로 제공하여 사용자가 ASA 키로 직접 연결할 필요가 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-106">The ASA key feature manages secret rotation for you and removes the need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span> 

<span data-ttu-id="d2d4d-107">Azure Storage 계정에 대한 일반적인 내용은 [Azure storage 계정 정보](https://docs.microsoft.com/azure/storage/storage-create-storage-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-107">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="d2d4d-108">인터페이스 지원</span><span class="sxs-lookup"><span data-stu-id="d2d4d-108">Supporting interfaces</span></span>

<span data-ttu-id="d2d4d-109">Azure Storage 계정 키 기능은 처음에 REST, .NET/C# 및 PowerShell 인터페이스를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-109">The Azure Storage Account keys feature is initially available through the REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="d2d4d-110">자세한 내용은 [Key Vault 참조](https://docs.microsoft.com/azure/key-vault/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-110">For more information, see [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>


## <a name="storage-account-keys-behavior"></a><span data-ttu-id="d2d4d-111">저장소 계정 키 동작</span><span class="sxs-lookup"><span data-stu-id="d2d4d-111">Storage account keys behavior</span></span>

### <a name="what-key-vault-manages"></a><span data-ttu-id="d2d4d-112">Key Vault에서 관리하는 사항</span><span class="sxs-lookup"><span data-stu-id="d2d4d-112">What Key Vault manages</span></span>

<span data-ttu-id="d2d4d-113">저장소 계정 키를 사용할 경우 Key Vault에서 사용자 대신 여러 가지 내부 관리 기능을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-113">Key Vault performs several internal management functions on your behalf when you use Storage Account Keys.</span></span>

1. <span data-ttu-id="d2d4d-114">Azure Key Vault는 ASA(Azure Storage Account)의 키를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-114">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span> 
    - <span data-ttu-id="d2d4d-115">내부적으로 Azure Key Vault는 키와 Azure Storage 계정을 나열(동기화)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-115">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>  
    - <span data-ttu-id="d2d4d-116">Azure Key Vault는 정기적으로 키를 다시 생성(회전)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-116">Azure Key Vault regenerates (rotates) the keys periodically.</span></span> 
    - <span data-ttu-id="d2d4d-117">키 값은 호출자에게 응답으로 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-117">Key values are never returned in response to caller.</span></span> 
    - <span data-ttu-id="d2d4d-118">Azure Key Vault는 저장소 계정과 클래식 저장소 계정 둘 다의 키를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-118">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span> 
2. <span data-ttu-id="d2d4d-119">Azure Key Vault를 사용하면 자격 증명 모음/개체 소유자가 SAS(계정 또는 서비스 SAS) 정의를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-119">Azure Key Vault allows you, the vault/object owner, to create SAS (account or service SAS) definitions.</span></span> 
    - <span data-ttu-id="d2d4d-120">SAS 정의를 사용하여 만든 SAS 값은 REST URI 경로를 통해 암호로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-120">The SAS value, created using SAS definition, is returned as a secret via the REST URI path.</span></span> <span data-ttu-id="d2d4d-121">자세한 내용은 [Azure Key Vault 저장소 계정 작업](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-121">For more information, see [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span></span>

### <a name="naming-guidance"></a><span data-ttu-id="d2d4d-122">명명 지침</span><span class="sxs-lookup"><span data-stu-id="d2d4d-122">Naming guidance</span></span>

<span data-ttu-id="d2d4d-123">저장소 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-123">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>  
 
<span data-ttu-id="d2d4d-124">SAS 정의 이름은 1-102자로, 0-9, a-z, A-Z만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-124">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="d2d4d-125">개발자 환경</span><span class="sxs-lookup"><span data-stu-id="d2d4d-125">Developer experience</span></span> 

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="d2d4d-126">Azure Key Vault Storage 키 이전</span><span class="sxs-lookup"><span data-stu-id="d2d4d-126">Before Azure Key Vault Storage Keys</span></span> 

<span data-ttu-id="d2d4d-127">개발자는 Azure storage에 액세스하기 위해 저장소 계정 키로 다음 작업을 수행해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-127">Developers used to need to do the following practices with a storage account key to get access to Azure storage.</span></span> 
 
 ```
//create storage account using connection string containing account name 
// and the storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="d2d4d-128">Azure Key Vault Storage 키 이후</span><span class="sxs-lookup"><span data-stu-id="d2d4d-128">After Azure Key Vault Storage Keys</span></span> 

```
//Please make sure to set storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command to get Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using the SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and the Blob storage endpoint to create a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about to expire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a><span data-ttu-id="d2d4d-129">개발자 모범 사례</span><span class="sxs-lookup"><span data-stu-id="d2d4d-129">Developer best practices</span></span> 

- <span data-ttu-id="d2d4d-130">Key Vault에서만 ASA 키를 관리하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-130">Only allow Key Vault to manage your ASA keys.</span></span> <span data-ttu-id="d2d4d-131">직접 관리할 경우 Key Vault 프로세스를 방해할 수 있으므로 직접 관리하려고 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-131">Do not attempt to manage them yourself, you will interfere with Key Vault's processes.</span></span> 
- <span data-ttu-id="d2d4d-132">둘 이상의 Key Vault 개체가 ASA 키를 관리하도록 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-132">Do not allow ASA keys to be managed by more than one Key Vault object.</span></span> 
- <span data-ttu-id="d2d4d-133">ASA 키를 수동으로 다시 생성해야 하는 경우 Key Vault를 통해 다시 생성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-133">If you need to manually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="d2d4d-134">시작</span><span class="sxs-lookup"><span data-stu-id="d2d4d-134">Getting started</span></span>

### <a name="setup-for-role-based-access-control-rbac-permissions"></a><span data-ttu-id="d2d4d-135">RBAC(역할 기반 액세스 제어) 권한 설정</span><span class="sxs-lookup"><span data-stu-id="d2d4d-135">Setup for role-based access control (RBAC) permissions</span></span>

<span data-ttu-id="d2d4d-136">Key Vault에 저장소 계정의 키를 *나열*하고 *다시 생성*할 수 있는 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-136">Key Vault needs permissions to *list* and *regenerate* keys for a storage account.</span></span> <span data-ttu-id="d2d4d-137">다음 단계를 따라 이러한 권한을 설정하세요.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-137">Set up these permissions using the following steps:</span></span>

- <span data-ttu-id="d2d4d-138">Key Vault의 ObjectId를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-138">Get ObjectId of Key Vault:</span></span> 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- <span data-ttu-id="d2d4d-139">Azure Key Vault ID에 저장소 키 운영자 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-139">Assign Storage Key Operator role to Azure Key Vault Identity:</span></span> 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > <span data-ttu-id="d2d4d-140">클래식 계정 유형의 경우 역할 매개 변수를 *"클래식 저장소 계정 키 운영자 서비스 역할"*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-140">For a classic account type, set the role parameter to *"Classic Storage Account Key Operator Service Role"*.</span></span>

### <a name="storage-account-onboarding"></a><span data-ttu-id="d2d4d-141">저장소 계정 등록</span><span class="sxs-lookup"><span data-stu-id="d2d4d-141">Storage account onboarding</span></span> 

<span data-ttu-id="d2d4d-142">예제: Key Vault 개체 소유자인 사용자는 Azure Key Vault에 저장소 계정 개체를 추가하여 저장소 계정을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-142">Example: As a Key Vault object owner you add a storage account object to your Azure Key Vault to onboard a storage account.</span></span>

<span data-ttu-id="d2d4d-143">등록하는 동안 Key Vault는 계정을 등록하는 ID에 저장소 키를 *나열* 및 *다시 생성*할 수 있는 사용 권한이 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-143">During onboarding, Key Vault needs to verify that the identity of the onboarding account has permissions to *list* and to *regenerate* storage keys.</span></span> <span data-ttu-id="d2d4d-144">이러한 사용 권한을 확인하기 위해 Key Vault는 인증 서비스에서 OBO(On Behalf Of) 토큰을 가져오고, 대상을 Azure Resource Manager로 설정하고, Azure Storage 서비스에 대한 *나열* 키 호출을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-144">In order to verify these permissions, Key Vault gets an OBO (On Behalf Of) token from the authentication service, audience set to Azure Resource Manager, and makes a *list* key call to the Azure Storage service.</span></span> <span data-ttu-id="d2d4d-145">*list* 호출이 실패할 경우 Key Vault 개체 생성은 *사용할 수 없음*이라는 HTTP 상태 코드로 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-145">If the *list* call fails, the Key Vault object creation fails with a HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="d2d4d-146">이러한 방식으로 나열된 키는 Key Vault 엔터티 저장소로 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-146">The keys listed in this fashion are cached with your key vault entity storage.</span></span> 

<span data-ttu-id="d2d4d-147">Key Vault에서 ID에 *다시 생성* 권한이 있는지 확인해야 키 다시 생성에 대한 소유권을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-147">Key Vault must verify that the identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="d2d4d-148">OBO 토큰을 통한 ID 및 Key Vault의 첫 번째 파티 ID에 이러한 사용 권한이 있는지 확인하기 위해</span><span class="sxs-lookup"><span data-stu-id="d2d4d-148">To verify that the identity, via OBO token, as well as the Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="d2d4d-149">Key Vault는 저장소 계정 리소스에 대한 RBAC 권한을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-149">Key Vault lists RBAC permissions on the storage account resource.</span></span>
- <span data-ttu-id="d2d4d-150">Key Vault는 작업 및 비작업의 정규식 일치를 통해 응답의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-150">Key Vault validates the response via regular expression matching of actions and non-actions.</span></span> 

<span data-ttu-id="d2d4d-151">[Key Vault - Managed Storage 계정 키 샘플](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167)에서 지원하는 몇 가지 예제를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-151">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span></span>

<span data-ttu-id="d2d4d-152">ID에 *다시 생성* 권한이 없거나 Key Vault의 첫 번째 파티 ID에 *나열* 또는 *다시 생성* 권한이 없는 경우 등록 요청이 실패하고 적절한 오류 코드 및 메시지가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-152">If the identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then the onboarding request fails returning an appropriate error code and message.</span></span> 

<span data-ttu-id="d2d4d-153">OBO 토큰은 PowerShell 또는 CLI의 네이티브 클라이언트 응용 프로그램인 첫 번째 파티를 사용하는 경우에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-153">The OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="d2d4d-154">다른 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d2d4d-154">Other applications</span></span>

- <span data-ttu-id="d2d4d-155">Key Vault 저장소 계정 키를 사용하여 생성된 SAS 토큰은 Azure storage 계정에 훨씬 더 제어된 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-155">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access to an Azure storage account.</span></span> <span data-ttu-id="d2d4d-156">자세한 내용은 [공유 액세스 서명 사용](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2d4d-156">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="d2d4d-157">참고 항목</span><span class="sxs-lookup"><span data-stu-id="d2d4d-157">See also</span></span>

- [<span data-ttu-id="d2d4d-158">키, 비밀 및 인증서에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="d2d4d-158">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="d2d4d-159">Key Vault 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="d2d4d-159">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)
