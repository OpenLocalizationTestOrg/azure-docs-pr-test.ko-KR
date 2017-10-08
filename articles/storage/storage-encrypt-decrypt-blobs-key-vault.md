---
title: "자습서: Azure Key Vault를 사용하여 Azure Storage에서 Blob 암호화 및 해독 | Microsoft Docs"
description: "어떻게 tooencrypt 및 클라이언트 쪽 암호화를 사용 하 여 Azure 키 자격 증명 모음과 Microsoft Azure 저장소에 대 한 blob을 암호 해독 합니다."
services: storage
documentationcenter: 
author: adhurwit
manager: jasonsav
editor: tysonn
ms.assetid: 027e8631-c1bf-48c1-9d9b-f6843e88b583
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 01/23/2017
ms.author: adhurwit
ms.openlocfilehash: 3eb64f104f378dd09ef295c94e03167655883391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="19e05-103">자습서: Microsoft Azure 저장소에서 Azure 키 자격 증명 모음을 사용하여 Blob 암호화 및 해독</span><span class="sxs-lookup"><span data-stu-id="19e05-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="19e05-104">소개</span><span class="sxs-lookup"><span data-stu-id="19e05-104">Introduction</span></span>
<span data-ttu-id="19e05-105">이 자습서에서는 toomake 클라이언트 쪽 저장소 암호화 Azure 키 자격 증명을 사용 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-105">This tutorial covers how toomake use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="19e05-106">방법 안내 합니다 tooencrypt 및 이러한 기술을 사용 하 여 콘솔 응용 프로그램에 blob를 암호 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-106">It walks you through how tooencrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="19e05-107">**예상 시간 toocomplete:** 20 분</span><span class="sxs-lookup"><span data-stu-id="19e05-107">**Estimated time toocomplete:** 20 minutes</span></span>

<span data-ttu-id="19e05-108">Azure Key Vault에 대한 개요는 [Azure Key Vault란?](../key-vault/key-vault-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19e05-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="19e05-109">Azure Storage에 대한 클라이언트 쪽 암호화의 개요 정보는 [Microsoft Azure Storage에 대한 클라이언트 쪽 암호화 및 Azure Key Vault](storage-client-side-encryption.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19e05-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19e05-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="19e05-110">Prerequisites</span></span>
<span data-ttu-id="19e05-111">toocomplete이이 자습서에서는 다음 hello 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-111">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="19e05-112">Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="19e05-112">An Azure Storage account</span></span>
* <span data-ttu-id="19e05-113">Visual Studio 2013 이상</span><span class="sxs-lookup"><span data-stu-id="19e05-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="19e05-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="19e05-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="19e05-115">클라이언트 쪽 암호화 개요</span><span class="sxs-lookup"><span data-stu-id="19e05-115">Overview of client-side encryption</span></span>
<span data-ttu-id="19e05-116">Azure Storage에 대한 클라이언트 쪽 암호화의 개요는 [Microsoft Storage에 대한 클라이언트 쪽 암호화 및 Azure Key Vault](storage-client-side-encryption.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19e05-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md)</span></span>

<span data-ttu-id="19e05-117">클라이언트 쪽 암호화의 작동 원리에 대한 간단한 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="19e05-118">hello Azure 저장소 클라이언트 SDK는 한 번 사용 대칭 키는 콘텐츠 암호화 키 (CEK)를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-118">hello Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="19e05-119">고객 데이터는 이 CEK를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="19e05-120">hello CEK 다음 래핑된 hello 키 암호화 키 KEK ()를 사용 하 여 (암호화) 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-120">hello CEK is then wrapped (encrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="19e05-121">hello KEK 키 식별자로 식별 되 하거나 수 있습니다는 비대칭 키 쌍 또는 대칭 키 및 수 수 로컬로 관리 Azure 키 자격 증명 모음에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-121">hello KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="19e05-122">hello 저장소 클라이언트 자체에 대 한 액세스 toohello KEK에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-122">hello Storage client itself never has access toohello KEK.</span></span> <span data-ttu-id="19e05-123">방금 주요 자격 증명 모음에서 제공 하는 hello 키 래핑 알고리즘을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-123">It just invokes hello key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="19e05-124">고객은 toouse 래핑/래핑 해제 하려는 경우 키에 대 한 사용자 지정 공급자를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-124">Customers can choose toouse custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="19e05-125">hello 암호화 된 데이터는 다음 toohello Azure 저장소 서비스에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-125">hello encrypted data is then uploaded toohello Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="19e05-126">Azure 키 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="19e05-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="19e05-127">이 자습서와 함께 순서 tooproceed,에서는 toodo hello hello 자습서에 나와 있는 단계를 수행 해야 [Azure 키 자격 증명 모음 시작](../key-vault/key-vault-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="19e05-127">In order tooproceed with this tutorial, you need toodo hello following steps, which are outlined in hello tutorial  [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="19e05-128">키 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-128">Create a key vault.</span></span>
* <span data-ttu-id="19e05-129">키 또는 toohello 비밀 키 자격 증명 모음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-129">Add a key or secret toohello key vault.</span></span>
* <span data-ttu-id="19e05-130">Azure Active Directory에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="19e05-131">Hello 응용 프로그램 toouse hello 키 또는 암호에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-131">Authorize hello application toouse hello key or secret.</span></span>

<span data-ttu-id="19e05-132">기록 hello ClientID 및 ClientSecret Azure Active Directory로 응용 프로그램을 등록할 때 생성 된 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-132">Make note of hello ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="19e05-133">Hello 키 자격 증명 모음에 두 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-133">Create both keys in hello key vault.</span></span> <span data-ttu-id="19e05-134">이름 다음 hello를 사용한 hello 자습서의 나머지 부분 hello에 대 한 가정: ContosoKeyVault 및 TestRSAKey1 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-134">We assume for hello rest of hello tutorial that you have used hello following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="19e05-135">패키지 및 AppSettings를 사용하여 콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="19e05-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="19e05-136">Visual Studio에서 새 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="19e05-137">Hello 패키지 관리자 콘솔에서에서 필요한 nuget 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-137">Add necessary nuget packages in hello Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="19e05-138">AppSettings toohello App.Config를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-138">Add AppSettings toohello App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="19e05-139">Hello 다음 추가 `using` 문과 있는지 tooadd 참조 tooSystem.Configuration toohello 프로젝트를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="19e05-139">Add hello following `using` statements and make sure tooadd a reference tooSystem.Configuration toohello project.</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Configuration;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.Azure.KeyVault;
using System.Threading;        
using System.IO;
```

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a><span data-ttu-id="19e05-140">메서드 tooget 토큰 tooyour 콘솔 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="19e05-140">Add a method tooget a token tooyour console application</span></span>
<span data-ttu-id="19e05-141">hello 다음 메서드 클래스에서 사용 됩니다 주요 자격 증명 모음 tooauthenticate 액세스 tooyour 주요 자격 증명 모음에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-141">hello following method is used by Key Vault classes that need tooauthenticate for access tooyour key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="19e05-142">사용자의 프로그램에서 저장소 및 키 자격 증명 모음 액세스</span><span class="sxs-lookup"><span data-stu-id="19e05-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="19e05-143">Main 함수 hello hello 코드 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-143">In hello Main function, add hello following code.</span></span>

```csharp
// This is standard code toointeract with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// hello Resolver object is used toointeract with Key Vault for Azure Storage.
// This is where hello GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="19e05-144">키 자격 증명 모음 개체 모델</span><span class="sxs-lookup"><span data-stu-id="19e05-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="19e05-145">이 두 개의 주요 자격 증명 모음 개체에 실제로 있는지 toounderstand 모델링 toobe 인식 중요: hello REST API (KeyVault 네임 스페이스)에 따라 하나 이며 기타 hello 클라이언트 쪽 암호화에 대 한 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-145">It is important toounderstand that there are actually two Key Vault object models toobe aware of: one is based on hello REST API (KeyVault namespace) and hello other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="19e05-146">키 자격 증명 모음 클라이언트 hello hello REST API와 상호 작용 하 고 JSON 웹 키와 비밀 hello 두 가지 주요 자격 증명 모음에 포함 하는 것에 대 한 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-146">hello Key Vault Client interacts with hello REST API and understands JSON Web Keys and secrets for hello two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="19e05-147">hello 키 자격 증명 모음 확장은 Azure 저장소의 클라이언트 쪽 암호화를 위해 특별히 생성 된 것 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-147">hello Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="19e05-148">키 (IKey)와 키 해결 프로그램의 hello 개념을 기반으로 클래스에 대 한 인터페이스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-148">They contain an interface for keys (IKey) and classes based on hello concept of a Key Resolver.</span></span> <span data-ttu-id="19e05-149">IKey tooknow 해야 하는 두 가지 구현이 없는: RSAKey 및 SymmetricKey입니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-149">There are two implementations of IKey that you need tooknow: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="19e05-150">이제 주요 자격 증명 모음에 포함 된 hello 가지 toocoincide 발생 고 있지만 시점에서 독립적인 (하므로 hello 키 및 비밀 키 자격 증명 모음 클라이언트 hello 검색 IKey를 구현 하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="19e05-150">Now they happen toocoincide with hello things that are contained in a Key Vault, but at this point they are independent classes (so hello Key and Secret retrieved by hello Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="19e05-151">Blob 암호화 및 업로드</span><span class="sxs-lookup"><span data-stu-id="19e05-151">Encrypt blob and upload</span></span>
<span data-ttu-id="19e05-152">Hello 다음 tooencrypt blob를 코드로 바꾸고 tooyour Azure 저장소 계정에 업로드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-152">Add hello following code tooencrypt a blob and upload it tooyour Azure storage account.</span></span> <span data-ttu-id="19e05-153">hello **ResolveKeyAsync** 사용 되는 메서드는 IKey를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-153">hello **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve hello key that you created previously.
// hello IKey that is returned here is an RsaKey.
// Remember that we used hello names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use hello RSA key tooencrypt by setting it in hello BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using hello UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="19e05-154">다음은 hello의 스크린 샷을 [Azure 클래식 포털](https://manage.windowsazure.com) 주요 자격 증명 모음에 저장 된 키가 있는 클라이언트 쪽 암호화를 사용 하 여 암호화 된 blob에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-154">Following is a screenshot from hello [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="19e05-155">hello **KeyId** 속성은 hello 키 KEK hello으로 사용 되는 주요 자격 증명 모음에 대 한 hello URI입니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-155">hello **KeyId** property is hello URI for hello key in Key Vault that acts as hello KEK.</span></span> <span data-ttu-id="19e05-156">hello **EncryptedKey** 속성 hello 암호화 된 버전의 hello CEK 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-156">hello **EncryptedKey** property contains hello encrypted version of hello CEK.</span></span>

![암호화 메타 데이터를 포함하고 있는 Blob 메타데이터를 보여 주는 스크린샷](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="19e05-158">Hello BlobEncryptionPolicy 생성자를 보면 키 및/또는 확인 자가 사용할 수 있는 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-158">If you look at hello BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="19e05-159">현재 해결 프로그램은 기본 키를 지원하지 않기 때문에 암호화에 사용할 수 없다는 데 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="19e05-160">Blob 암호 해독 및 다운로드</span><span class="sxs-lookup"><span data-stu-id="19e05-160">Decrypt blob and download</span></span>
<span data-ttu-id="19e05-161">암호 해독은 실제로 경우 확인자를 사용 하 여 hello 클래스 맞지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-161">Decryption is really when using hello Resolver classes make sense.</span></span> <span data-ttu-id="19e05-162">암호화에 사용 되는 hello 키 hello ID 해당 메타 데이터에 hello blob와 연결 되므로 tooretrieve hello 키에 대 한 이유가 없습니다 및 키와 blob 간의 hello 연결 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-162">hello ID of hello key used for encryption is associated with hello blob in its metadata, so there is no reason for you tooretrieve hello key and remember hello association between key and blob.</span></span> <span data-ttu-id="19e05-163">키 자격 증명 모음에 그 hello 키 유지 되는지 toomake를 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-163">You just have toomake sure that hello key remains in Key Vault.</span></span>   

<span data-ttu-id="19e05-164">주요 자격 증명에는 RSA 키 남아의 개인 키 hello 하므로 암호 해독 toooccur에 대 한 hello 암호화 키 CEK 전송 암호 해독을 위한 자격 증명 모음 tooKey hello를 포함 하는 hello blob 메타 데이터에서.</span><span class="sxs-lookup"><span data-stu-id="19e05-164">hello private key of an RSA Key remains in Key Vault, so for decryption toooccur, hello Encrypted Key from hello blob metadata that contains hello CEK is sent tooKey Vault for decryption.</span></span>

<span data-ttu-id="19e05-165">방금 업로드 toodecrypt hello blob 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-165">Add hello following toodecrypt hello blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="19e05-166">비롯 하 여 다른 종류의 해결 프로그램 toomake 키 관리에 대 한 몇 가지: AggregateKeyResolver 및 CachingKeyResolver 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-166">There are a couple of other kinds of resolvers toomake key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="19e05-167">키 자격 증명 모음 암호 사용</span><span class="sxs-lookup"><span data-stu-id="19e05-167">Use Key Vault secrets</span></span>
<span data-ttu-id="19e05-168">암호는 기본적으로 대칭 키 때문에 hello SymmetricKey 클래스를 통해 hello 방식으로 toouse 클라이언트 쪽 암호화 된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-168">hello way toouse a secret with client-side encryption is via hello SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="19e05-169">하지만 키 자격 증명 모음의 암호 tooa SymmetricKey 정확 하 게 위에서 언급 한 대로 매핑하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-169">But, as noted above, a secret in Key Vault does not map exactly tooa SymmetricKey.</span></span> <span data-ttu-id="19e05-170">몇 가지 toounderstand 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-170">There are a few things toounderstand:</span></span>

* <span data-ttu-id="19e05-171">SymmetricKey의 hello 키의 toobe 고정된 길이: 128, 192 256, 384 및 512 비트입니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-171">hello key in a SymmetricKey has toobe a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="19e05-172">SymmetricKey의 hello 키 Base64 인코딩 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-172">hello key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="19e05-173">SymmetricKey로 사용 될 키 자격 증명 모음 암호 toohave "응용 프로그램/옥텟 스트림" 키 자격 증명 모음의 내용 유형이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-173">A Key Vault secret that will be used as a SymmetricKey needs toohave a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="19e05-174">다음은 SymmetricKey로 사용할 수 있는 키 자격 증명 모음의 암호를 만드는 Powershell의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="19e05-175">Hello 하드 코드 된 값, $key, 데모 용도로 임을 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="19e05-175">Please note that hello hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="19e05-176">사용자 코드에서 싶을 것 toogenerate이이 키입니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-176">In your own code you'll want toogenerate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     hello characters are in hello ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute hello VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="19e05-177">콘솔 응용 프로그램에서 동일한 호출 tooretrieve 하기 전에 암호는 SymmetricKey로 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-177">In your console application, you can use hello same call as before tooretrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="19e05-178">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-178">That's it.</span></span> <span data-ttu-id="19e05-179">마음껏 즐기세요!</span><span class="sxs-lookup"><span data-stu-id="19e05-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="19e05-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="19e05-180">Next steps</span></span>
<span data-ttu-id="19e05-181">C#에서 Microsoft Azure Storage 사용에 대한 자세한 내용은 [.NET용 Microsoft Azure Storage Client Library](https://msdn.microsoft.com/library/azure/dn261237.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19e05-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="19e05-182">Hello Blob REST API에 대 한 자세한 내용은 참조 [Blob 서비스 REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-182">For more information about hello Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="19e05-183">Microsoft Azure 저장소에 대 한 최신 정보 hello, toohello 이동 [Microsoft Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/)합니다.</span><span class="sxs-lookup"><span data-stu-id="19e05-183">For hello latest information on Microsoft Azure Storage, go toohello [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
