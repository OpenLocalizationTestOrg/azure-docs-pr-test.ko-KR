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
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="936a2-103">종단 간 키 회전 및 감사를 사용하여 Azure Key Vault 설정</span><span class="sxs-lookup"><span data-stu-id="936a2-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="936a2-104">소개</span><span class="sxs-lookup"><span data-stu-id="936a2-104">Introduction</span></span>
<span data-ttu-id="936a2-105">주요 자격 증명 모음을 만든 후 해당 자격 증명 모음 toostore 키와 암호를 사용 하 여 수 toostart 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-105">After creating your key vault, you will be able toostart using that vault toostore your keys and secrets.</span></span> <span data-ttu-id="936a2-106">응용 프로그램 키 또는 암호를 toopersist 더 이상 필요는 없지만 대신 요청으로 hello 키 자격 증명 모음에서 필요에 따라.</span><span class="sxs-lookup"><span data-stu-id="936a2-106">Your applications no longer need toopersist your keys or secrets, but rather will request them from hello key vault as needed.</span></span> <span data-ttu-id="936a2-107">이렇게 하면 있습니다 tooupdate 키와 암호 hello 응용 프로그램의 동작을 다양 한 키와 비밀 관리 가능성을 열 수 있는 영향을 주지 않고.</span><span class="sxs-lookup"><span data-stu-id="936a2-107">This allows you tooupdate keys and secrets without affecting hello behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="936a2-108">이 경우 응용 프로그램에 의해 액세스 되는 Azure 저장소 계정 키의 암호를 toostore Azure 키 자격 증명 모음을 사용 하는 예제를 통해이 문서에서는 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-108">This article walks through an example of using Azure Key Vault toostore a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="936a2-109">또한 해당 저장소 계정 키의 예약된 회전 구현에 대해서도 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="936a2-110">마지막으로, toomonitor 주요 자격 증명 모음 감사 로그 hello 하 고 예기치 않은 요청을 만들 때 경고를 발생 하는 방법의 데모를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-110">Finally, it walks through a demonstration of how toomonitor hello key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="936a2-111">이 자습서에에서 없는 경우 의도 한 tooexplain 주요 자격 증명 모음의 세부 hello 초기 설치</span><span class="sxs-lookup"><span data-stu-id="936a2-111">This tutorial is not intended tooexplain in detail hello initial setup of your key vault.</span></span> <span data-ttu-id="936a2-112">자세한 내용은 [Azure 키 자격 증명 모음 시작](key-vault-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="936a2-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="936a2-113">플랫폼 간 명령줄 인터페이스 지침은 [CLI를 사용하여 Key Vault 관리](key-vault-manage-with-cli2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="936a2-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli2.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="936a2-114">주요 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="936a2-114">Set up Key Vault</span></span>
<span data-ttu-id="936a2-115">응용 프로그램 tooretrieve 비밀 tooenable 주요 자격 증명에서 먼저 hello 암호를 만들고 해야 tooyour 자격 증명 모음에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-115">tooenable an application tooretrieve a secret from Key Vault, you must first create hello secret and upload it tooyour vault.</span></span> <span data-ttu-id="936a2-116">Azure PowerShell 세션을 시작 하 고 로그인 tooyour Azure 계정 hello 다음 명령을 사용 하 여이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-116">This can be accomplished by starting an Azure PowerShell session and signing in tooyour Azure account with hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="936a2-117">Hello 팝업 브라우저 창에서 Azure 계정 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-117">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="936a2-118">PowerShell이이 계정과 연결 된 모든 hello 구독을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-118">PowerShell will get all hello subscriptions that are associated with this account.</span></span> <span data-ttu-id="936a2-119">PowerShell 사용 하 여 hello 기본적으로 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-119">PowerShell uses hello first one by default.</span></span>

<span data-ttu-id="936a2-120">여러 구독이 있는 하는 경우에 주요 자격 증명 모음을 사용 하는 toocreate 인 hello toospecify를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-120">If you have multiple subscriptions, you might have toospecify hello one that was used toocreate your key vault.</span></span> <span data-ttu-id="936a2-121">Hello toosee hello 구독 계정에 대해 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-121">Enter hello following toosee hello subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="936a2-122">toospecify hello 연결 된 구독으로 로그인 수는 경우, hello 키 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-122">toospecify hello subscription that's associated with hello key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="936a2-123">이 문서에서는 저장소 계정 키를 비밀로 저장하는 방법을 설명하므로 해당 저장소 계정 키를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="936a2-124">본인에 (이 경우 저장소 계정 키)를 검색 한 후 해당 tooa 보안 문자열을 변환한 다음 해당 값을 가진 주요 자격 증명 모음에서 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-124">After retrieving your secret (in this case, your storage account key), you must convert that tooa secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="936a2-125">다음으로 만든 hello 암호에 대 한 hello를 URI를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-125">Next, get hello URI for hello secret you created.</span></span> <span data-ttu-id="936a2-126">Hello 주요 자격 증명 모음 tooretrieve 본인을 호출 하는 경우이 이후 단계에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-126">This is used in a later step when you call hello key vault tooretrieve your secret.</span></span> <span data-ttu-id="936a2-127">Hello 다음 PowerShell 명령을 실행 하 고 hello 암호로 URI hello ID 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-127">Run hello following PowerShell command and make note of hello ID value, which is hello secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a><span data-ttu-id="936a2-128">Hello 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="936a2-128">Set up hello application</span></span>
<span data-ttu-id="936a2-129">저장 되는 암호를가지고 코드 tooretrieve를 사용할 수 있으며 사용.</span><span class="sxs-lookup"><span data-stu-id="936a2-129">Now that you have a secret stored, you can use code tooretrieve and use it.</span></span> <span data-ttu-id="936a2-130">가지가 몇 가지 단계 필요한 tooachieve이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-130">There are a few steps required tooachieve this.</span></span> <span data-ttu-id="936a2-131">hello 첫 번째 이자 가장 중요 한 단계는 응용 프로그램을 Azure Active Directory 등록 이며 다음 응용 프로그램에서 요청을 허용할 수 있도록 응용 프로그램 정보 자격 증명 모음 키를 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-131">hello first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="936a2-132">응용 프로그램에 만들어야 hello 동일한 주요 자격 증명 모음으로 Azure Active Directory 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-132">Your application must be created on hello same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="936a2-133">Azure Active Directory의 hello 응용 프로그램 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-133">Open hello applications tab of Azure Active Directory.</span></span>

![Azure Active Directory에서 응용 프로그램 열기](./media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="936a2-135">선택 **추가** tooadd 응용 프로그램 tooyour Azure Active Directory 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-135">Choose **ADD** tooadd an application tooyour Azure Active Directory.</span></span>

![[추가] 선택](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="936a2-137">Hello 응용 프로그램 유형으로 둡니다 **웹 응용 프로그램 및/또는 웹 API** 하 고 응용 프로그램 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-137">Leave hello application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![이름 hello 응용 프로그램](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="936a2-139">응용 프로그램에 **로그온 URL** 및 **앱 ID URI**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="936a2-140">이 데모에서는 사용자가 원하는 어떤 것이라도 가능하며 필요한 경우 나중에 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![필요한 URI 제공](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="936a2-142">Hello 응용 프로그램 tooAzure Active Directory를 추가한 후 hello 응용 프로그램 페이지로 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-142">After hello application is added tooAzure Active Directory, you will be brought into hello application page.</span></span> <span data-ttu-id="936a2-143">Hello 클릭 **구성** 탭 하 고 다음 찾아서 복사할 hello **클라이언트 ID** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-143">Click hello **Configure** tab and then find and copy hello **Client ID** value.</span></span> <span data-ttu-id="936a2-144">이후 단계에 대 한 hello 클라이언트 ID를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-144">Make note of hello client ID for later steps.</span></span>

<span data-ttu-id="936a2-145">다음으로, Azure Active Directory와 상호 작용할 수 있도록 응용 프로그램에 대한 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="936a2-146">Hello에서 만들 수 있습니다 **키** hello 섹션인 **구성** 탭 합니다. 이후 단계에서 새로 생성 하는 hello Azure Active Directory 응용 프로그램에서 사용할 수 있도록 키를 메모를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-146">You can create this under hello **Keys** section in hello **Configuration** tab. Make note of hello newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Azure Active Directory 앱 키](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="936a2-148">Hello 주요 자격 증명 모음에 응용 프로그램에서 모든 호출을 설정 하기 전에 응용 프로그램 및 해당 사용 권한을 대 한 hello 주요 자격 증명 모음을 알려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-148">Before establishing any calls from your application into hello key vault, you must tell hello key vault about your application and its permissions.</span></span> <span data-ttu-id="936a2-149">hello 다음 명령에서는 hello 자격 증명 모음 이름 및 Azure Active Directory 응용 프로그램 및 부여에서 클라이언트 ID hello **가져오기** 액세스 tooyour 주요 자격 증명 모음 hello 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-149">hello following command takes hello vault name and hello client ID from your Azure Active Directory app and grants **Get** access tooyour key vault for hello application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="936a2-150">이 시점에서 응용 프로그램이 호출 작성 준비 toostart 됩니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-150">At this point, you are ready toostart building your application calls.</span></span> <span data-ttu-id="936a2-151">응용 프로그램에서 Azure 키 자격 증명 모음 및 Azure Active Directory와 hello NuGet 패키지가 필요한 toointeract를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-151">In your application, you must install hello NuGet packages required toointeract with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="936a2-152">Hello Visual Studio 패키지 관리자 콘솔에서 다음 명령을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-152">From hello Visual Studio Package Manager console, enter hello following commands.</span></span> <span data-ttu-id="936a2-153">이 문서의 hello 문서 작성 당시 hello hello Azure Active Directory 패키지의 최신 버전 이므로 3.10.305231913, tooconfirm hello에 대 한 최신 정보를 원하는 고에 따라 업데이트 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-153">At hello writing of this article, hello current version of hello Azure Active Directory package is 3.10.305231913, so you might want tooconfirm hello latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="936a2-154">응용 프로그램 코드에서 Azure Active Directory 인증에 대 한 클래스 toohold hello 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-154">In your application code, create a class toohold hello method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="936a2-155">이 예제에서 이 클래스는 **Utils**입니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-155">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="936a2-156">Hello 다음 추가 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="936a2-156">Add hello following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="936a2-157">다음으로 hello 메서드 tooretrieve hello JWT 토큰을 Azure Active Directory에서 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-157">Next, add hello following method tooretrieve hello JWT token from Azure Active Directory.</span></span> <span data-ttu-id="936a2-158">유지 관리의 편의성 웹 또는 응용 프로그램 구성에 toomove hello 하드 코드 된 문자열 값 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-158">For maintainability, you may want toomove hello hard-coded string values into your web or application configuration.</span></span>

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

<span data-ttu-id="936a2-159">Hello 필요한 코드 toocall 주요 자격 증명 모음을 추가 하 고 사용자가 본인 확인 값을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-159">Add hello necessary code toocall Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="936a2-160">먼저 추가한 다음 hello 다음 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="936a2-160">First you must add hello following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="936a2-161">Hello 메서드 호출 tooinvoke 주요 자격 증명 모음을 추가 하 고 본인을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-161">Add hello method calls tooinvoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="936a2-162">이 방법에서는 hello 암호는 이전 단계에서 저장 하는 URI를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-162">In this method, you provide hello secret URI that you saved in a previous step.</span></span> <span data-ttu-id="936a2-163">Hello hello 사용 **GetToken** hello 메서드에서 **유틸리티** 이전에 만든 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-163">Note hello use of hello **GetToken** method from hello **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="936a2-164">응용 프로그램을 실행 하면 있습니다 해야 이제 인증을 받게 tooAzure Active Directory 및 Azure 키 자격 증명 모음에서 다음 프로그램 비밀 값을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-164">When you run your application, you should now be authenticating tooAzure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="936a2-165">Azure Automation을 사용하여 키 회전</span><span class="sxs-lookup"><span data-stu-id="936a2-165">Key rotation using Azure Automation</span></span>
<span data-ttu-id="936a2-166">Azure 주요 자격 증명 모음 암호 정보로 저장하는 값을 위한 회전 전략을 구현하는 다양한 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-166">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="936a2-167">수동 프로세스의 일부로 비밀을 회전할 수 있으며 API 호출을 활용하여 프로그래밍 방식으로 회전하거나 Automation 스크립트 방식으로 회전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-167">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="936a2-168">이 문서의 hello 위해 됩니다 Azure PowerShell을 사용 하 여 함께 Azure 자동화 toochange Azure 저장소 계정 액세스 키입니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-168">For hello purposes of this article, you will be using Azure PowerShell combined with Azure Automation toochange an Azure Storage Account access key.</span></span> <span data-ttu-id="936a2-169">그런 다음 해당 새 키를 사용하여 Key Vault 비밀을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-169">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="936a2-170">tooallow Azure 자동화 tooset 비밀 값 주요 자격 증명 모음에서 Azure 자동화 인스턴스를 설정할 때 생성 된 AzureRunAsConnection 라는 hello 연결에 대 한 hello 클라이언트 ID를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-170">tooallow Azure Automation tooset secret values in your key vault, you must get hello client ID for hello connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="936a2-171">Azure Automation 인스턴스에서 **자산**을 선택하여 이 ID를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-171">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="936a2-172">여기에서 선택 **연결** 선택한 후 hello **AzureRunAsConnection** 원칙 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-172">From there, you choose **Connections** and then select hello **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="936a2-173">Hello를 메모해 **응용 프로그램 ID**합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-173">Take note of hello **Application ID**.</span></span>

![Azure Automation 클라이언트 ID](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="936a2-175">**자산**에서 **모듈**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-175">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="936a2-176">**모듈**선택, **갤러리**, 한 다음 검색 하 고 **가져오기** 각각 hello 다음 모듈의 업데이트 된 버전:</span><span class="sxs-lookup"><span data-stu-id="936a2-176">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of hello following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="936a2-177">이 문서의 hello 문서 작성 당시만 hello 필요한 이전에 메모 모듈 toobe 업데이트 스크립트를 다음 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-177">At hello writing of this article, only hello previously noted modules needed toobe updated for hello following script.</span></span> <span data-ttu-id="936a2-178">자동화 작업이 실패하는 것으로 확인되면 필요한 모든 모듈과 해당 종속성을 가져왔는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-178">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="936a2-179">Azure 자동화 연결에 대 한 hello 응용 프로그램 ID를 검색 한 후 알려야 주요 자격 증명 모음 자격 증명 모음에서이 응용 프로그램 액세스 tooupdate 비밀 정보에는 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-179">After you have retrieved hello application ID for your Azure Automation connection, you must tell your key vault that this application has access tooupdate secrets in your vault.</span></span> <span data-ttu-id="936a2-180">다음 PowerShell 명령을 hello로이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-180">This can be accomplished with hello following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="936a2-181">다음으로 Azure Automation 인스턴스 아래에서 **Runbooks**을 선택하고 **Runbook 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-181">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="936a2-182">**빠른 생성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-182">Select **Quick Create**.</span></span> <span data-ttu-id="936a2-183">Runbook 이름을 지정 하 고 선택 **PowerShell** hello runbook 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-183">Name your runbook and select **PowerShell** as hello runbook type.</span></span> <span data-ttu-id="936a2-184">Hello 옵션 tooadd 설명을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-184">You have hello option tooadd a description.</span></span> <span data-ttu-id="936a2-185">마지막으로 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-185">Finally, click **Create**.</span></span>

![runbook 만들기](./media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="936a2-187">새 runbook에 대 한 hello 편집기 창에서 PowerShell 스크립트 뒤 hello를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-187">Paste hello following PowerShell script in hello editor pane for your new runbook:</span></span>

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

<span data-ttu-id="936a2-188">Hello 편집기 창에서 선택 **테스트 창** tootest 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-188">From hello editor pane, choose **Test pane** tootest your script.</span></span> <span data-ttu-id="936a2-189">Hello 스크립트가 오류 없이 실행 되 고, 선택할 수 있습니다 **게시**, 다음 hello runbook 구성 창에서 다시 hello runbook에 대 한 일정을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-189">Once hello script is running without error, you can select **Publish**, and then you can apply a schedule for hello runbook back in hello runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="936a2-190">Key Vault 감사 파이프라인</span><span class="sxs-lookup"><span data-stu-id="936a2-190">Key Vault auditing pipeline</span></span>
<span data-ttu-id="936a2-191">주요 자격 증명 모음을 설정할 때 감사 액세스 요청이 toohello 주요 자격 증명 모음에 toocollect 로그 켤 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-191">When you set up a key vault, you can turn on auditing toocollect logs on access requests made toohello key vault.</span></span> <span data-ttu-id="936a2-192">이러한 로그는 지정된 Azure Storage 계정에 저장되며 끌어내기, 모니터링 및 분석이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-192">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="936a2-193">hello 다음과 같은 시나리오 사용 Azure 함수, Azure 논리 앱 및 주요 자격 증명 모음 감사 로그 toocreate 파이프라인 toosend 전자 메일이 hello 웹 앱의 hello 응용 프로그램 ID와 일치 하는 응용 프로그램 hello 자격 증명 모음에서 암호를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-193">hello following scenario uses Azure functions, Azure logic apps, and key vault audit logs toocreate a pipeline toosend an email when an app that does match hello app ID of hello web app retrieves secrets from hello vault.</span></span>

<span data-ttu-id="936a2-194">먼저 Key Vault에서 로깅을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-194">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="936a2-195">Hello 다음 PowerShell 명령을 통해이 작업을 수행할 수 있습니다 (전체 세부 정보에서 볼 수 있습니다 [키 자격 증명 모음 로깅](key-vault-logging.md)):</span><span class="sxs-lookup"><span data-stu-id="936a2-195">This can be done via hello following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="936a2-196">이 활성화 된 후 감사 저장소 계정을 지정 하는 hello에 수집 시작을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-196">After this is enabled, audit logs start collecting into hello designated storage account.</span></span> <span data-ttu-id="936a2-197">이러한 로그에는 Key Vault를 어떻게, 언제, 누가 액세스하는지에 대한 이벤트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-197">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="936a2-198">10 분 후 hello 키 자격 증명 모음 작업 로깅 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-198">You can access your logging information 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="936a2-199">이 시간은 일반적으로 10분보다 짧습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-199">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="936a2-200">hello 다음 단계는 너무[Azure 서비스 버스 큐 만들기](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-200">hello next step is too[create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="936a2-201">여기에 Key Vault 감사 로그가 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-201">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="936a2-202">Hello 감사 로그 메시지 hello 큐에 있는 경우 hello 논리 앱은을 선택 하 고에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-202">When hello audit log messages are in hello queue, hello logic app picks them up and acts on them.</span></span> <span data-ttu-id="936a2-203">단계를 수행 하는 hello로 서비스 버스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-203">Create a service bus with hello following steps:</span></span>

1. <span data-ttu-id="936a2-204">서비스 버스 네임 스페이스 만들기 (이미 있는 경우 원하는 toouse이를 건너뜁니다 tooStep 2).</span><span class="sxs-lookup"><span data-stu-id="936a2-204">Create a Service Bus namespace (if you already have one that you want toouse for this, skip tooStep 2).</span></span>
2. <span data-ttu-id="936a2-205">Azure 포털 hello 및 선택 hello 네임 스페이스 toocreate hello 큐에서 원하는 toohello 서비스 버스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-205">Browse toohello service bus in hello Azure portal and select hello namespace you want toocreate hello queue in.</span></span>
3. <span data-ttu-id="936a2-206">선택 **새로** 선택 **서비스 버스 > 큐** hello 필요한 세부 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-206">Select **New** and choose **Service Bus > Queue** and enter hello required details.</span></span>
4. <span data-ttu-id="936a2-207">Hello 네임 스페이스를 선택 하 고 클릭 하 여 hello 서비스 버스 연결 정보를 선택 **연결 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-207">Select hello Service Bus connection information by choosing hello namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="936a2-208">Hello 다음 섹션에이 정보가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-208">You will need this information for hello next section.</span></span>

<span data-ttu-id="936a2-209">그런 다음, [Azure 함수를 만들](../azure-functions/functions-create-first-azure-function.md) toopoll 주요 자격 증명 모음 로그 내 저장소 계정을 hello 및 새 이벤트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-209">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) toopoll key vault logs within hello storage account and pick up new events.</span></span> <span data-ttu-id="936a2-210">그러면 일정에 따라 트리거되는 함수가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-210">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="936a2-211">toocreate Azure에서 함수를 선택 **새로 만들기 > 함수 앱** hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="936a2-211">toocreate an Azure function, choose **New > Function App** in hello Azure portal.</span></span> <span data-ttu-id="936a2-212">만들기 중에 기존 호스팅 계획을 사용하거나 새 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-212">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="936a2-213">동적 호스팅을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-213">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="936a2-214">호스팅 옵션 함수에 대 한 자세한 내용은에서 확인할 수 있습니다 [어떻게 tooscale Azure 함수](../azure-functions/functions-scale.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-214">More details on Function hosting options can be found at [How tooscale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="936a2-215">Hello Azure 함수를 만들면 tooit를 탐색 하 고 함수와 C 타이머를 선택할\#합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-215">When hello Azure function is created, navigate tooit and choose a timer function and C\#.</span></span> <span data-ttu-id="936a2-216">그런 다음 **이 함수 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-216">Then click **Create this function**.</span></span>

![Azure Functions 시작 블레이드](./media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="936a2-218">Hello에 **개발** 탭, hello run.csx 코드 hello 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-218">On hello **Develop** tab, replace hello run.csx code with hello following:</span></span>

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
> <span data-ttu-id="936a2-219">Hello 앞 코드 toopoint tooyour 저장소 계정 키 자격 증명 모음 로그 hello 기록 되므로, 이전에 만든 hello 서비스 버스에에서 있는지 tooreplace hello 변수를 확인 하 고 특정 경로 toohello 주요 자격 증명 모음 저장소 로그 hello 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-219">Make sure tooreplace hello variables in hello preceding code toopoint tooyour storage account where hello key vault logs are written, hello service bus you created earlier, and hello specific path toohello key vault storage logs.</span></span>
>
>

<span data-ttu-id="936a2-220">hello 함수 hello 최신 로그 hello 저장소 계정에서 여기서 hello 주요 자격 증명 모음 로그 기록 된 파일, grabs의 hello 최신 이벤트를 해당 파일을 선택 하 고 tooa 서비스 버스 큐를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-220">hello function picks up hello latest log file from hello storage account where hello key vault logs are written, grabs hello latest events from that file, and pushes them tooa Service Bus queue.</span></span> <span data-ttu-id="936a2-221">단일 파일에는 여러 이벤트가 있을 수 있습니다, 때문 sync.txt 파일 hello 함수를 받았음을 hello 마지막 이벤트의 toodetermine hello 타임 스탬프도 확인을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-221">Since a single file could have multiple events, you should create a sync.txt file that hello function also looks at toodetermine hello time stamp of hello last event that was picked up.</span></span> <span data-ttu-id="936a2-222">이렇게 하면 푸시 하지 않는 같은 이벤트가 여러 번 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-222">This ensures that you don't push hello same event multiple times.</span></span> <span data-ttu-id="936a2-223">이 sync.txt 파일 hello 마지막 발생 한 이벤트에 대 한 타임 스탬프를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-223">This sync.txt file contains a timestamp for hello last encountered event.</span></span> <span data-ttu-id="936a2-224">hello 로그, 로드 되 면가 정렬 toobe 기반으로 hello 타임 스탬프 tooensure 바르게 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-224">hello logs, when loaded, have toobe sorted based on hello timestamp tooensure they are ordered correctly.</span></span>

<span data-ttu-id="936a2-225">이 함수에 대 한 몇 가지 Azure 함수에서 hello 상자를 사용할 수 없는 추가 라이브러리 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-225">For this function, we reference a couple of additional libraries that are not available out of hello box in Azure Functions.</span></span> <span data-ttu-id="936a2-226">tooinclude 이러한 Azure 함수 toopull 필요한 NuGet을 사용 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-226">tooinclude these, we need Azure Functions toopull them using NuGet.</span></span> <span data-ttu-id="936a2-227">Hello 선택 **파일 보기** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-227">Choose hello **View Files** option.</span></span>

![보기 파일 옵션](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="936a2-229">project.json이라는 파일에 다음 콘텐츠를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-229">And add a file called project.json with following content:</span></span>

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
<span data-ttu-id="936a2-230">시 **저장**, Azure 함수 hello 필요한 이진 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-230">Upon **Save**, Azure Functions will download hello required binaries.</span></span>

<span data-ttu-id="936a2-231">Toohello 전환 **통합** 탭 및 hello 함수 내에서 의미 있는 이름을 toouse hello 타이머 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-231">Switch toohello **Integrate** tab and give hello timer parameter a meaningful name toouse within hello function.</span></span> <span data-ttu-id="936a2-232">호출 하는 hello 타이머 toobe 것 예상 hello 코드 앞에, *myTimer*합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-232">In hello preceding code, it expects hello timer toobe called *myTimer*.</span></span> <span data-ttu-id="936a2-233">지정 된 [CRON 식](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) 다음과 같이: 0 \* \* \* \* \* hello 함수 toorun 1 분 마다 발생 시키는 hello 타이머에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-233">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for hello timer that will cause hello function toorun once a minute.</span></span>

<span data-ttu-id="936a2-234">에 동일한 hello **통합** 탭에서 추가 hello 형식의 입력 **Azure Blob 저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-234">On hello same **Integrate** tab, add an input of hello type **Azure Blob Storage**.</span></span> <span data-ttu-id="936a2-235">이 hello 마지막 이벤트를 감시 한 hello 함수 hello 타임 스탬프를 포함 하는 toohello sync.txt 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-235">This will point toohello sync.txt file that contains hello timestamp of hello last event looked at by hello function.</span></span> <span data-ttu-id="936a2-236">이 hello 매개 변수 이름 사용 하 여 hello 기능 내에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-236">This will be available within hello function by hello parameter name.</span></span> <span data-ttu-id="936a2-237">Hello 코드 앞에에서 hello Azure Blob 저장소 입력 매개 변수 이름 toobe hello를 16 *inputBlob*합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-237">In hello preceding code, hello Azure Blob Storage input expects hello parameter name toobe *inputBlob*.</span></span> <span data-ttu-id="936a2-238">Hello sync.txt 파일 상주할 hello 저장소 계정을 선택 (수도 hello 같거나 다른 저장소 계정).</span><span class="sxs-lookup"><span data-stu-id="936a2-238">Choose hello storage account where hello sync.txt file will reside (it could be hello same or a different storage account).</span></span> <span data-ttu-id="936a2-239">Hello 경로 필드에서 hello 파일 hello 형식 {container-name}/path/to/sync.txt 거주 하는 hello 경로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-239">In hello path field, provide hello path where hello file lives in hello format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="936a2-240">Hello 형식의 출력 추가 *Azure Blob 저장소* 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-240">Add an output of hello type *Azure Blob Storage* output.</span></span> <span data-ttu-id="936a2-241">이 hello 입력에 정의 된 toohello sync.txt 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-241">This will point toohello sync.txt file you defined in hello input.</span></span> <span data-ttu-id="936a2-242">이 hello 함수 toowrite hello 이벤트의 타임 스탬프 hello 마지막에 검토 하 여 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-242">This is used by hello function toowrite hello timestamp of hello last event looked at.</span></span> <span data-ttu-id="936a2-243">hello 앞의 코드에서는이 매개 변수 toobe 호출 *outputBlob*합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-243">hello preceding code expects this parameter toobe called *outputBlob*.</span></span>

<span data-ttu-id="936a2-244">이 시점에서 hello 함수는 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-244">At this point, hello function is ready.</span></span> <span data-ttu-id="936a2-245">있는지 tooswitch 백 toohello 확인 **개발** 탭 및 hello 코드를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-245">Make sure tooswitch back toohello **Develop** tab and save hello code.</span></span> <span data-ttu-id="936a2-246">컴파일 오류에 대 한 hello 출력 창을 확인 및 해결 하는 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-246">Check hello output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="936a2-247">Hello 코드가 컴파일 hello 코드는 이제 수 로그를 확인 hello 주요 자격 증명 모음 1 분 마다 서비스 버스 큐를 정의 된 hello에 새 이벤트를 밀어 그리고 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-247">If hello code compiles, then hello code should now be checking hello key vault logs every minute and pushing any new events onto hello defined Service Bus queue.</span></span> <span data-ttu-id="936a2-248">Hello 함수 트리거될 때마다 toohello 로그 창을 작성 하는 로깅 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-248">You should see logging information write out toohello log window every time hello function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="936a2-249">Azure 논리 앱</span><span class="sxs-lookup"><span data-stu-id="936a2-249">Azure logic app</span></span>
<span data-ttu-id="936a2-250">그런 다음 하 hello 함수 toohello 서비스 버스 큐에 푸시합니다, hello 콘텐츠를 구문 분석 하 고 보냅니다 하 게 일치 하는 조건에 따라 전자 메일 hello 이벤트를 선택 하는 Azure 논리 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-250">Next you must create an Azure logic app that picks up hello events that hello function is pushing toohello Service Bus queue, parses hello content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="936a2-251">[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md) 너무 이동 하 여**새로 만들기 > 논리 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-251">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going too**New > Logic App**.</span></span>

<span data-ttu-id="936a2-252">Hello 논리 앱을 만든 후 tooit를 탐색 하 고 선택할 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-252">Once hello logic app is created, navigate tooit and choose **edit**.</span></span> <span data-ttu-id="936a2-253">Hello 논리가 응용 프로그램 편집기 내에서 선택 **서비스 버스 큐** 서비스 버스 자격 증명 tooconnect 입력 것 toohello 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-253">Within hello logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials tooconnect it toohello queue.</span></span>

![Azure 논리 앱 서비스 버스](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="936a2-255">다음으로 **조건 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-255">Next choose **Add a condition**.</span></span> <span data-ttu-id="936a2-256">Hello 조건 toohello 고급 편집기를 전환 하 고 코드 다음, hello로 APP_ID 대체 hello 입력 웹 응용 프로그램의 실제 APP_ID:</span><span class="sxs-lookup"><span data-stu-id="936a2-256">In hello condition, switch toohello advanced editor and enter hello following code, replacing APP_ID with hello actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="936a2-257">이 식은 기본적으로 반환 **false** 경우 hello *appid* (즉, hello hello 서비스 버스 메시지 본문) 들어오는 이벤트 hello 하지는 hello *appid* hello의 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-257">This expression essentially returns **false** if hello *appid* from hello incoming event (which is hello body of hello Service Bus message) is not hello *appid* of hello app.</span></span>

<span data-ttu-id="936a2-258">이제 **아니요인 경우, 아무 작업도 수행하지 않습니다** 옵션 아래에서 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-258">Now, create an action under **If no, do nothing**.</span></span>

![Azure 논리 앱 선택 작업](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="936a2-260">Hello 동작에 대 한 선택 **Office 365-전자 메일 보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-260">For hello action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="936a2-261">Hello 필드 toocreate 메일 toosend 때 채워야 hello 정의 조건 반환 **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-261">Fill out hello fields toocreate an email toosend when hello defined condition returns **false**.</span></span> <span data-ttu-id="936a2-262">Office 365가 없는 경우에 대안 살펴볼 수 있습니다 tooachieve hello 동일한 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-262">If you do not have Office 365, you could look at alternatives tooachieve hello same results.</span></span>

<span data-ttu-id="936a2-263">이 시점에서 1 분 마다 새 주요 자격 증명 모음 감사 로그를 검색 하는 최종 tooend 파이프라인을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-263">At this point, you have an end tooend pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="936a2-264">Tooa 서비스 버스 큐를 찾으면 새 로그를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-264">It pushes new logs it finds tooa service bus queue.</span></span> <span data-ttu-id="936a2-265">hello 논리 앱은 hello 큐에 새 메시지가 삽입 하는 경우에 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-265">hello logic app is triggered when a new message lands in hello queue.</span></span> <span data-ttu-id="936a2-266">경우 hello *appid* hello 내에서 이벤트의 응용 프로그램을 호출 하는 hello hello 앱 ID 일치 하지 않습니다, 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="936a2-266">If hello *appid* within hello event does not match hello app ID of hello calling application, it sends an email.</span></span>
