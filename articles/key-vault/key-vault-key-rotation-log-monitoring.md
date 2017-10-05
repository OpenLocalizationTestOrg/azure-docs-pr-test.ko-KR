---
title: "종단 간 키 회전 및 감사를 사용하여 Azure Key Vault 설정 | Microsoft Docs"
description: "키 회전 및 Key Vault 로그의 모니터링을 통해 설정을 가져오는 데 이 방법을 사용합니다."
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
ms.openlocfilehash: 38c342802ed687985ac6f84f5a590a1a0dcc6c6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="0b779-103">종단 간 키 회전 및 감사를 사용하여 Azure Key Vault 설정</span><span class="sxs-lookup"><span data-stu-id="0b779-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="0b779-104">소개</span><span class="sxs-lookup"><span data-stu-id="0b779-104">Introduction</span></span>
<span data-ttu-id="0b779-105">Key Vault를 만든 후에는 키와 비밀을 저장하는 데 Key Vault를 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-105">After creating your key vault, you will be able to start using that vault to store your keys and secrets.</span></span> <span data-ttu-id="0b779-106">사용자 응용 프로그램에서는 키 또는 암호 정보를 더 이상 유지할 필요가 없으며 대신, 필요에 따라 주요 자격 증명 모음에서 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-106">Your applications no longer need to persist your keys or secrets, but rather will request them from the key vault as needed.</span></span> <span data-ttu-id="0b779-107">이렇게 하면 응용 프로그램의 동작에 영향을 주지 않고 키 및 비밀을 업데이트할 수 있으며 키 및 비밀 관리 동작에 대한 다양한 가능성이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-107">This allows you to update keys and secrets without affecting the behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="0b779-108">이 문서에서는 Azure Key Vault를 사용하여 비밀(이 예에서는 응용 프로그램에서 액세스하는 Azure Storage 계정 키)을 저장하는 예제를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-108">This article walks through an example of using Azure Key Vault to store a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="0b779-109">또한 해당 저장소 계정 키의 예약된 회전 구현에 대해서도 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="0b779-110">마지막으로, 예기치 않은 요청이 있을 때 Key Vault 감사 로그를 모니터하고 경고를 생성하는 방법도 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-110">Finally, it walks through a demonstration of how to monitor the key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="0b779-111">이 자습서는 Key Vault의 초기 설정에 대해서는 자세히 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-111">This tutorial is not intended to explain in detail the initial setup of your key vault.</span></span> <span data-ttu-id="0b779-112">자세한 내용은 [Azure 키 자격 증명 모음 시작](key-vault-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b779-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="0b779-113">플랫폼 간 명령줄 인터페이스 지침은 [CLI를 사용하여 Key Vault 관리](key-vault-manage-with-cli2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b779-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli2.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="0b779-114">주요 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="0b779-114">Set up Key Vault</span></span>
<span data-ttu-id="0b779-115">응용 프로그램을 통해 Azure Key Vault에서 비밀을 검색하려면 먼저 비밀을 만들어 Key Vault에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-115">To enable an application to retrieve a secret from Key Vault, you must first create the secret and upload it to your vault.</span></span> <span data-ttu-id="0b779-116">이렇게 하려면 Azure PowerShell 세션을 시작하고 다음 명령 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-116">This can be accomplished by starting an Azure PowerShell session and signing in to your Azure account with the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="0b779-117">팝업 브라우저 창에 Azure 계정 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-117">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="0b779-118">PowerShell이 이 계정과 연결된 모든 구독을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-118">PowerShell will get all the subscriptions that are associated with this account.</span></span> <span data-ttu-id="0b779-119">PowerShell은 기본적으로 첫 번째 구독을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-119">PowerShell uses the first one by default.</span></span>

<span data-ttu-id="0b779-120">구독이 여러 개인 경우 Key Vault을 만드는 데 사용된 구독을 지정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-120">If you have multiple subscriptions, you might have to specify the one that was used to create your key vault.</span></span> <span data-ttu-id="0b779-121">계정에 대한 구독을 보려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-121">Enter the following to see the subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="0b779-122">로깅하려는 Key Vault와 연결된 구독을 지정하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-122">To specify the subscription that's associated with the key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="0b779-123">이 문서에서는 저장소 계정 키를 비밀로 저장하는 방법을 설명하므로 해당 저장소 계정 키를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="0b779-124">비밀(이 예에서는 저장소 계정 키)을 검색한 후에는 보안 문자열로 변환한 후 해당 값을 사용하여 Key Vault에 비밀을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-124">After retrieving your secret (in this case, your storage account key), you must convert that to a secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="0b779-125">그런 다음, 만든 비밀의 URI를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-125">Next, get the URI for the secret you created.</span></span> <span data-ttu-id="0b779-126">이 URI는 이후에 비밀을 검색하기 위해 Key Vault를 호출하는 단계에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-126">This is used in a later step when you call the key vault to retrieve your secret.</span></span> <span data-ttu-id="0b779-127">다음 PowerShell 명령을 실행하고 비밀 URI인 ID 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-127">Run the following PowerShell command and make note of the ID value, which is the secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-the-application"></a><span data-ttu-id="0b779-128">응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="0b779-128">Set up the application</span></span>
<span data-ttu-id="0b779-129">비밀이 저장되었으니 이제 코드를 사용하여 비밀을 검색하고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-129">Now that you have a secret stored, you can use code to retrieve and use it.</span></span> <span data-ttu-id="0b779-130">이 작업을 수행하려면 몇 가지 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-130">There are a few steps required to achieve this.</span></span> <span data-ttu-id="0b779-131">가장 중요한 첫 번째 단계는 응용 프로그램을 Azure Active Directory에 등록한 후 응용 프로그램의 요청을 허용하도록 Key Vault에 응용 프로그램을 알리는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-131">The first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="0b779-132">응용 프로그램은 Key Vault와 동일한 Azure Active Directory에서 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-132">Your application must be created on the same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="0b779-133">Azure Active Directory의 응용 프로그램 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-133">Open the applications tab of Azure Active Directory.</span></span>

![Azure Active Directory에서 응용 프로그램 열기](./media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="0b779-135">**추가**를 선택하여 응용 프로그램을 Azure Active Directory에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-135">Choose **ADD** to add an application to your Azure Active Directory.</span></span>

![[추가] 선택](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="0b779-137">응용 프로그램 유형을 **웹 응용 프로그램 및/또는 웹 API**로 두고 응용 프로그램 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-137">Leave the application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![응용 프로그램 이름 지정](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="0b779-139">응용 프로그램에 **로그온 URL** 및 **앱 ID URI**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="0b779-140">이 데모에서는 사용자가 원하는 어떤 것이라도 가능하며 필요한 경우 나중에 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![필요한 URI 제공](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="0b779-142">응용 프로그램이 Azure Active Directory에 추가되면 응용 프로그램 페이지로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-142">After the application is added to Azure Active Directory, you will be brought into the application page.</span></span> <span data-ttu-id="0b779-143">**구성** 탭을 클릭한 후 **클라이언트 ID** 값을 찾아 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-143">Click the **Configure** tab and then find and copy the **Client ID** value.</span></span> <span data-ttu-id="0b779-144">이후 단계에서 클라이언트 ID를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-144">Make note of the client ID for later steps.</span></span>

<span data-ttu-id="0b779-145">다음으로, Azure Active Directory와 상호 작용할 수 있도록 응용 프로그램에 대한 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="0b779-146">**구성** 탭의 **키** 섹션 아래에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-146">You can create this under the **Keys** section in the **Configuration** tab.</span></span> <span data-ttu-id="0b779-147">이후 단계에서 사용할 수 있도록 Azure Active Directory 응용 프로그램에서 새로 생성된 키를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-147">Make note of the newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Azure Active Directory 앱 키](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="0b779-149">응용 프로그램에서 Key Vault로 모든 호출을 설정하기 전에 Key Vault에 응용 프로그램 및 해당 권한에 대한 정보를 알려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-149">Before establishing any calls from your application into the key vault, you must tell the key vault about your application and its permissions.</span></span> <span data-ttu-id="0b779-150">다음 명령은 Azure Active Directory 앱에서 Key Vault 이름 및 클라이언트 ID를 가져와 Key Vault에 응용 프로그램에 대한 **Get** 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-150">The following command takes the vault name and the client ID from your Azure Active Directory app and grants **Get** access to your key vault for the application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="0b779-151">이제 응용 프로그램 호출의 빌드를 시작할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-151">At this point, you are ready to start building your application calls.</span></span> <span data-ttu-id="0b779-152">응용 프로그램에서 Azure Key Vault 및 Azure Active Directory와 상호 작용하는 데 필요한 NuGet 패키지를 먼저 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-152">In your application, you must install the NuGet packages required to interact with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="0b779-153">Visual Studio 패키지 관리자 콘솔에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-153">From the Visual Studio Package Manager console, enter the following commands.</span></span> <span data-ttu-id="0b779-154">이 문서를 작성할 당시 Azure Active Directory 패키지의 최신 버전은 3.10.305231913이므로 최신 버전을 확인하고 그에 따라 업데이트해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-154">At the writing of this article, the current version of the Azure Active Directory package is 3.10.305231913, so you might want to confirm the latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="0b779-155">응용 프로그램 코드에서 Azure Active Directory 인증에 대한 메서드를 보유할 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-155">In your application code, create a class to hold the method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="0b779-156">이 예제에서 이 클래스는 **Utils**입니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-156">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="0b779-157">다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-157">Add the following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="0b779-158">다음으로, Azure Active Directory에서 JWT 토큰을 검색하는 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-158">Next, add the following method to retrieve the JWT token from Azure Active Directory.</span></span> <span data-ttu-id="0b779-159">유지 관리를 위해 하드 코딩된 문자열 값을 웹 또는 응용 프로그램 구성으로 이동하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-159">For maintainability, you may want to move the hard-coded string values into your web or application configuration.</span></span>

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed to obtain the JWT token");

    return result.AccessToken;
}
```

<span data-ttu-id="0b779-160">Key Vault를 호출하고 비밀 값을 검색하는 데 필요한 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-160">Add the necessary code to call Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="0b779-161">먼저 다음 using 문을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-161">First you must add the following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="0b779-162">Key Vault를 호출하고 비밀을 검색하는 메서드 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-162">Add the method calls to invoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="0b779-163">이 메서드에 이전 단계에서 저장한 비밀 URI를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-163">In this method, you provide the secret URI that you saved in a previous step.</span></span> <span data-ttu-id="0b779-164">앞에서 만든 **Utils** 클래스의 **GetToken** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-164">Note the use of the **GetToken** method from the **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="0b779-165">응용 프로그램을 실행하면 Azure Active Directory에 인증된 후 Azure Key Vault에서 비밀 값을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-165">When you run your application, you should now be authenticating to Azure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="0b779-166">Azure Automation을 사용하여 키 회전</span><span class="sxs-lookup"><span data-stu-id="0b779-166">Key rotation using Azure Automation</span></span>
<span data-ttu-id="0b779-167">Azure 주요 자격 증명 모음 암호 정보로 저장하는 값을 위한 회전 전략을 구현하는 다양한 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-167">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="0b779-168">수동 프로세스의 일부로 비밀을 회전할 수 있으며 API 호출을 활용하여 프로그래밍 방식으로 회전하거나 Automation 스크립트 방식으로 회전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-168">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="0b779-169">이 문서의 목적에 따라 Azure Automation과 결합된 Azure PowerShell을 사용하여 Azure Storage 계정 액세스 키를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-169">For the purposes of this article, you will be using Azure PowerShell combined with Azure Automation to change an Azure Storage Account access key.</span></span> <span data-ttu-id="0b779-170">그런 다음 해당 새 키를 사용하여 Key Vault 비밀을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-170">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="0b779-171">Azure Automation이 Key Vault의 비밀 값을 설정할 수 있도록 허용하려면 Azure Automation 인스턴스를 설정할 때 AzureRunAsConnection이라는 이름으로 생성된 연결에 대한 클라이언트 ID를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-171">To allow Azure Automation to set secret values in your key vault, you must get the client ID for the connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="0b779-172">Azure Automation 인스턴스에서 **자산**을 선택하여 이 ID를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-172">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="0b779-173">여기에서 **연결**을 선택한 후 **AzureRunAsConnection** 서비스 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-173">From there, you choose **Connections** and then select the **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="0b779-174">**응용 프로그램 ID**를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-174">Take note of the **Application ID**.</span></span>

![Azure Automation 클라이언트 ID](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="0b779-176">**자산**에서 **모듈**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-176">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="0b779-177">**모듈**에서 **갤러리**를 선택한 후 다음 각 모듈의 업데이트된 버전을 검색하여 **가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-177">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of the following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="0b779-178">이 문서를 작성할 당시 위에 명시된 모듈만 다음 스크립트에 대해 업데이트되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-178">At the writing of this article, only the previously noted modules needed to be updated for the following script.</span></span> <span data-ttu-id="0b779-179">자동화 작업이 실패하는 것으로 확인되면 필요한 모든 모듈과 해당 종속성을 가져왔는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-179">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="0b779-180">Azure Automation 연결에 대한 응용 프로그램 ID를 검색한 후에는 이 응용 프로그램에서 Key Vault의 비밀을 업데이트할 권한이 있음을 Key Vault에 알려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-180">After you have retrieved the application ID for your Azure Automation connection, you must tell your key vault that this application has access to update secrets in your vault.</span></span> <span data-ttu-id="0b779-181">다음 PowerShell 명령을 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-181">This can be accomplished with the following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="0b779-182">다음으로 Azure Automation 인스턴스 아래에서 **Runbooks**을 선택하고 **Runbook 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-182">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="0b779-183">**빠른 생성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-183">Select **Quick Create**.</span></span> <span data-ttu-id="0b779-184">runbook의 이름을 지정하고 runbook 유형으로 **PowerShell**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-184">Name your runbook and select **PowerShell** as the runbook type.</span></span> <span data-ttu-id="0b779-185">설명을 추가하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-185">You have the option to add a description.</span></span> <span data-ttu-id="0b779-186">마지막으로 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-186">Finally, click **Create**.</span></span>

![runbook 만들기](./media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="0b779-188">새 runbook의 편집기 창에 다음 PowerShell 스크립트를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-188">Paste the following PowerShell script in the editor pane for your new runbook:</span></span>

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get the connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in to Azure..."
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

#Optionally you may set the following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for the storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

<span data-ttu-id="0b779-189">편집기 창에서 **테스트 창**을 선택하여 스크립트를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-189">From the editor pane, choose **Test pane** to test your script.</span></span> <span data-ttu-id="0b779-190">스크립트가 오류 없이 실행되면 **게시**를 선택한 후 runbook 구성 창에서 runbook에 대한 일정을 다시 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-190">Once the script is running without error, you can select **Publish**, and then you can apply a schedule for the runbook back in the runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="0b779-191">Key Vault 감사 파이프라인</span><span class="sxs-lookup"><span data-stu-id="0b779-191">Key Vault auditing pipeline</span></span>
<span data-ttu-id="0b779-192">Key Vault를 설정할 때 감사를 켜서 Key Vault에 대해 발생하는 액세스 요청에 대한 로그를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-192">When you set up a key vault, you can turn on auditing to collect logs on access requests made to the key vault.</span></span> <span data-ttu-id="0b779-193">이러한 로그는 지정된 Azure Storage 계정에 저장되며 끌어내기, 모니터링 및 분석이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-193">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="0b779-194">다음 시나리오에서는 웹앱의 앱 ID가 일치하는 앱이 Key Vault에서 검색하는 경우 Azure Functions, Azure Logic Apps 및 Key Vault를 사용하여 전자 메일을 보내는 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-194">The following scenario uses Azure functions, Azure logic apps, and key vault audit logs to create a pipeline to send an email when an app that does match the app ID of the web app retrieves secrets from the vault.</span></span>

<span data-ttu-id="0b779-195">먼저 Key Vault에서 로깅을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-195">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="0b779-196">이 작업은 다음 PowerShell 명령을 통해 수행할 수 있습니다(전체 설명은 [key-vault-로깅](key-vault-logging.md)에서 확인할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="0b779-196">This can be done via the following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="0b779-197">로깅이 활성화되면 감사 로그가 지정된 저장소 계정으로 수집하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-197">After this is enabled, audit logs start collecting into the designated storage account.</span></span> <span data-ttu-id="0b779-198">이러한 로그에는 Key Vault를 어떻게, 언제, 누가 액세스하는지에 대한 이벤트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-198">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="0b779-199">Key Vault 작업 후 10분 내에 로깅 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-199">You can access your logging information 10 minutes after the key vault operation.</span></span> <span data-ttu-id="0b779-200">이 시간은 일반적으로 10분보다 짧습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-200">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="0b779-201">다음은 [Azure Service Bus 큐를 만드는](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)단계입니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-201">The next step is to [create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="0b779-202">여기에 Key Vault 감사 로그가 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-202">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="0b779-203">감사 로그 메시지가 큐에 있으면 논리 앱이 감사 로그 메시지를 선택하여 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-203">When the audit log messages are in the queue, the logic app picks them up and acts on them.</span></span> <span data-ttu-id="0b779-204">다음 단계를 수행하여 Service Bus를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-204">Create a service bus with the following steps:</span></span>

1. <span data-ttu-id="0b779-205">Service Bus 네임스페이스를 만듭니다(사용할 네임스페이스가 이미 있는 경우 2단계로 건너뜀).</span><span class="sxs-lookup"><span data-stu-id="0b779-205">Create a Service Bus namespace (if you already have one that you want to use for this, skip to Step 2).</span></span>
2. <span data-ttu-id="0b779-206">Azure Portal에서 Service Bus를 찾아 안에 큐를 만들 네임스페이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-206">Browse to the service bus in the Azure portal and select the namespace you want to create the queue in.</span></span>
3. <span data-ttu-id="0b779-207">**새로 만들기**를 선택하고 **Service Bus -> 큐**를 선택한 다음 필요한 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-207">Select **New** and choose **Service Bus > Queue** and enter the required details.</span></span>
4. <span data-ttu-id="0b779-208">네임스페이스를 선택하고 **연결 정보**를 클릭하여 Service Bus 연결 정보를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-208">Select the Service Bus connection information by choosing the namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="0b779-209">다음 섹션에서 이 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-209">You will need this information for the next section.</span></span>

<span data-ttu-id="0b779-210">다음으로, [Azure 함수를 만들어](../azure-functions/functions-create-first-azure-function.md) 저장소 계정 내에서 Key Vault 로그를 폴링하고 새 이벤트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-210">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) to poll key vault logs within the storage account and pick up new events.</span></span> <span data-ttu-id="0b779-211">그러면 일정에 따라 트리거되는 함수가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-211">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="0b779-212">Azure 함수를 만들려면 Azure Portal에서 **새로 만들기 -> 함수 앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-212">To create an Azure function, choose **New > Function App** in the Azure portal.</span></span> <span data-ttu-id="0b779-213">만들기 중에 기존 호스팅 계획을 사용하거나 새 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-213">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="0b779-214">동적 호스팅을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-214">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="0b779-215">함수 호스팅 옵션에 대한 자세한 내용은 [Azure Functions 크기 조정 방법](../azure-functions/functions-scale.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-215">More details on Function hosting options can be found at [How to scale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="0b779-216">Azure 함수를 만들었으면 해당 함수로 이동하여 타이머 함수 및 C\#을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-216">When the Azure function is created, navigate to it and choose a timer function and C\#.</span></span> <span data-ttu-id="0b779-217">그런 다음 **이 함수 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-217">Then click **Create this function**.</span></span>

![Azure Functions 시작 블레이드](./media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="0b779-219">**개발** 탭에서 run.csx 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-219">On the **Develop** tab, replace the run.csx code with the following:</span></span>

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
            log.Verbose($"Sync point file didnt have a date. Setting to now.");
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

            //required to order by time as they may not be in the file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending to ServiceBus, use the payloadStream and set keeporiginal to true
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

    //Generate the shared access signature on the container, setting the constraints directly on the signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> <span data-ttu-id="0b779-220">위의 코드에 있는 변수를 Key Vault 로그가 기록된 저장소 계정, 이전에 생성한 Service Bus 및 Key Vault 저장소 로그의 경로를 가리키도록 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-220">Make sure to replace the variables in the preceding code to point to your storage account where the key vault logs are written, the service bus you created earlier, and the specific path to the key vault storage logs.</span></span>
>
>

<span data-ttu-id="0b779-221">이 함수는 Key Vault 로그가 기록된 저장소 계정에서 최신 로그 파일을 선택하고 해당 파일에서 최신 이벤트를 가져와 Service Bus 큐에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-221">The function picks up the latest log file from the storage account where the key vault logs are written, grabs the latest events from that file, and pushes them to a Service Bus queue.</span></span> <span data-ttu-id="0b779-222">단일 파일에 여러 이벤트가 포함될 수 있으므로 함수가 선택된 최신 이벤트의 타임스탬프를 결정하기 위해 확인하는 sync.txt 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-222">Since a single file could have multiple events, you should create a sync.txt file that the function also looks at to determine the time stamp of the last event that was picked up.</span></span> <span data-ttu-id="0b779-223">그러면 동일한 이벤트를 여러 번 푸시하지 않게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-223">This ensures that you don't push the same event multiple times.</span></span> <span data-ttu-id="0b779-224">이 sync.txt 파일은 최근에 발생한 이벤트에 대한 타임스탬프를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-224">This sync.txt file contains a timestamp for the last encountered event.</span></span> <span data-ttu-id="0b779-225">로그(로드된 경우)는 바르게 정렬되도록 타임스탬프를 기반으로 정렬해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-225">The logs, when loaded, have to be sorted based on the timestamp to ensure they are ordered correctly.</span></span>

<span data-ttu-id="0b779-226">이 함수에서는 Azure Functions에서 바로 사용할 수 없는 몇 가지 추가 라이브러리를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-226">For this function, we reference a couple of additional libraries that are not available out of the box in Azure Functions.</span></span> <span data-ttu-id="0b779-227">이를 포함하려면 NuGet을 사용하여 끌어오기 위해 Azure Functions가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-227">To include these, we need Azure Functions to pull them using NuGet.</span></span> <span data-ttu-id="0b779-228">**보기 파일** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-228">Choose the **View Files** option.</span></span>

![보기 파일 옵션](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="0b779-230">project.json이라는 파일에 다음 콘텐츠를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-230">And add a file called project.json with following content:</span></span>

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
<span data-ttu-id="0b779-231">**저장** 시 Azure Functions가 필요한 이진 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-231">Upon **Save**, Azure Functions will download the required binaries.</span></span>

<span data-ttu-id="0b779-232">**통합** 탭으로 전환하고 타이머 매개 변수에 함수 내에서 사용할 의미 있는 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-232">Switch to the **Integrate** tab and give the timer parameter a meaningful name to use within the function.</span></span> <span data-ttu-id="0b779-233">위의 코드는 타이머가 *myTimer*로 호출될 것으로 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-233">In the preceding code, it expects the timer to be called *myTimer*.</span></span> <span data-ttu-id="0b779-234">타이머에 대한 [CRON 식](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON)을 0 \* \* \* \* \*로 지정하면 함수가 1분에 한 번 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-234">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for the timer that will cause the function to run once a minute.</span></span>

<span data-ttu-id="0b779-235">동일한 **통합** 탭에서 **Azure Blob Storage** 형식의 입력을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-235">On the same **Integrate** tab, add an input of the type **Azure Blob Storage**.</span></span> <span data-ttu-id="0b779-236">이렇게 하면 함수에서 확인하는 최신 이벤트의 타임스탬프를 포함하는 sync.txt 파일을 가리키게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-236">This will point to the sync.txt file that contains the timestamp of the last event looked at by the function.</span></span> <span data-ttu-id="0b779-237">그러면 함수 내에서 매개 변수 이름으로 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-237">This will be available within the function by the parameter name.</span></span> <span data-ttu-id="0b779-238">위의 코드에서 Azure Blob Storage 입력에 대한 매개 변수 이름은 *inputBlob*으로 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-238">In the preceding code, the Azure Blob Storage input expects the parameter name to be *inputBlob*.</span></span> <span data-ttu-id="0b779-239">sync.txt 파일이 상주할 저장소 계정을 선택합니다(같은 저장소 계정일 수도 있고 다른 저장소 계정일 수도 있음).</span><span class="sxs-lookup"><span data-stu-id="0b779-239">Choose the storage account where the sync.txt file will reside (it could be the same or a different storage account).</span></span> <span data-ttu-id="0b779-240">경로 필드에는 파일이 {container-name}/path/to/sync.txt 형식으로 상주하는 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-240">In the path field, provide the path where the file lives in the format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="0b779-241">*Azure Blob Storage* 형식의 출력을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-241">Add an output of the type *Azure Blob Storage* output.</span></span> <span data-ttu-id="0b779-242">이렇게 하면 입력에서 방금 정의한 sync.txt 파일을 가리키게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-242">This will point to the sync.txt file you defined in the input.</span></span> <span data-ttu-id="0b779-243">이 파일은 함수에서 확인하는 최신 이벤트의 타임스탬프를 작성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-243">This is used by the function to write the timestamp of the last event looked at.</span></span> <span data-ttu-id="0b779-244">위의 코드에서는 이 매개 변수를 *outputBlob*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-244">The preceding code expects this parameter to be called *outputBlob*.</span></span>

<span data-ttu-id="0b779-245">이제 함수가 준비되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-245">At this point, the function is ready.</span></span> <span data-ttu-id="0b779-246">다시 **개발** 탭으로 전환하고 코드를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-246">Make sure to switch back to the **Develop** tab and save the code.</span></span> <span data-ttu-id="0b779-247">출력 창에서 컴파일 오류를 확인하고 적절히 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-247">Check the output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="0b779-248">코드가 컴파일되면 해당 코드는 이제 1분마다 Key Vault 로그를 확인하고 모든 새 이벤트를 정의된 Service Bus 큐에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-248">If the code compiles, then the code should now be checking the key vault logs every minute and pushing any new events onto the defined Service Bus queue.</span></span> <span data-ttu-id="0b779-249">함수가 트리거될 때마다 로깅 정보가 로그 창에 기록되는 것이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-249">You should see logging information write out to the log window every time the function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="0b779-250">Azure 논리 앱</span><span class="sxs-lookup"><span data-stu-id="0b779-250">Azure logic app</span></span>
<span data-ttu-id="0b779-251">다음으로 함수가 Service Bus 큐에 푸시하는 이벤트를 선택하고 콘텐츠를 구문 분석한 후 일치하는 조건에 따라 전자 메일을 보내는 Azure 논리 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-251">Next you must create an Azure logic app that picks up the events that the function is pushing to the Service Bus queue, parses the content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="0b779-252">**새로 만들기 -> 논리 앱**으로 이동하여 [논리 앱을 만듭니다](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0b779-252">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going to **New > Logic App**.</span></span>

<span data-ttu-id="0b779-253">논리 앱을 만들었으면 해당 논리 앱으로 이동하여 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-253">Once the logic app is created, navigate to it and choose **edit**.</span></span> <span data-ttu-id="0b779-254">논리 앱 편집기 내에서 **Service Bus 큐**를 선택하고 큐에 연결하기 위한 Service Bus 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-254">Within the logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials to connect it to the queue.</span></span>

![Azure 논리 앱 서비스 버스](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="0b779-256">다음으로 **조건 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-256">Next choose **Add a condition**.</span></span> <span data-ttu-id="0b779-257">조건에서 고급 편집기로 전환한 후 다음 코드를 입력합니다. 이때 APP_ID를 웹앱의 실제 APP_ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-257">In the condition, switch to the advanced editor and enter the following code, replacing APP_ID with the actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="0b779-258">이 식은 기본적으로 들어오는 이벤트(Service Bus 메시지의 본문)의 *appid*가 앱의 *appid*가 아닌 경우 **false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-258">This expression essentially returns **false** if the *appid* from the incoming event (which is the body of the Service Bus message) is not the *appid* of the app.</span></span>

<span data-ttu-id="0b779-259">이제 **아니요인 경우, 아무 작업도 수행하지 않습니다** 옵션 아래에서 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-259">Now, create an action under **If no, do nothing**.</span></span>

![Azure 논리 앱 선택 작업](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="0b779-261">작업의 경우 **Office 365 - 전자 메일 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-261">For the action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="0b779-262">정의된 조건에서 **false**를 반환하는 경우 보낼 전자 메일을 작성하도록 필드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-262">Fill out the fields to create an email to send when the defined condition returns **false**.</span></span> <span data-ttu-id="0b779-263">Office 365가 없는 경우 같은 결과를 얻을 수 있는 대안을 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-263">If you do not have Office 365, you could look at alternatives to achieve the same results.</span></span>

<span data-ttu-id="0b779-264">현재는 1분마다 새로운 Key Vault 감사 로그를 확인하는 종단 간 파이프라인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-264">At this point, you have an end to end pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="0b779-265">이 파이프라인은 새 로그가 발견되면 Service Bus 큐에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-265">It pushes new logs it finds to a service bus queue.</span></span> <span data-ttu-id="0b779-266">새 메시지가 큐에 도착하면 논리 앱이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-266">The logic app is triggered when a new message lands in the queue.</span></span> <span data-ttu-id="0b779-267">이벤트 내의 *appid*가 호출 응용 프로그램의 앱 ID와 일치하지 않으면 전자 메일이 발송됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b779-267">If the *appid* within the event does not match the app ID of the calling application, it sends an email.</span></span>
