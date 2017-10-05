---
title: "Azure Key Vault 로깅 | Microsoft Docs"
description: "이 자습서를 사용하여 Azure 키 자격 증명 모음 로깅을 시작할 수 있습니다."
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
ms.openlocfilehash: e9a4f16f048833dab49f7db79892fe47a5aeff37
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-key-vault-logging"></a><span data-ttu-id="77519-103">Azure 키 자격 증명 모음 로깅</span><span class="sxs-lookup"><span data-stu-id="77519-103">Azure Key Vault Logging</span></span>
<span data-ttu-id="77519-104">Azure 키 자격 증명 모음은 대부분 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77519-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="77519-105">자세한 내용은 [키 자격 증명 모음 가격 책정 페이지](https://azure.microsoft.com/pricing/details/key-vault/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77519-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="77519-106">소개</span><span class="sxs-lookup"><span data-stu-id="77519-106">Introduction</span></span>
<span data-ttu-id="77519-107">하나 이상의 키 자격 증명 모음을 만든 후 키 자격 증명 모음이 액세스되는 방법, 시기 및 사용자를 모니터링하려는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77519-107">After you have created one or more key vaults, you will likely want to monitor how and when your key vaults are accessed, and by whom.</span></span> <span data-ttu-id="77519-108">Azure 저장소 계정에 제공하는 정보를 저장하는 키 자격 증명 모음에 대한 로깅을 사용하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77519-108">You can do this by enabling logging for Key Vault, which saves information in an Azure storage account that you provide.</span></span> <span data-ttu-id="77519-109">**insights-logs-auditevent** 라는 새 컨테이너가 지정된 저장소 계정에 대해 자동으로 만들어지고 여러 키 자격 증명 모음에 대한 로그를 수집하기 위해 이 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77519-109">A new container named **insights-logs-auditevent** is automatically created for your specified storage account, and you can use this same storage account for collecting logs for multiple key vaults.</span></span>

<span data-ttu-id="77519-110">키 자격 증명 모음 작업 후 최대 10분 후에 로깅 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77519-110">You can access your logging information at most, 10 minutes after the key vault operation.</span></span> <span data-ttu-id="77519-111">대부분의 경우 이것보다 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="77519-111">In most cases, it will be quicker than this.</span></span>  <span data-ttu-id="77519-112">저장소 계정의 로그 관리에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="77519-112">It's up to you to manage your logs in your storage account:</span></span>

* <span data-ttu-id="77519-113">표준 Azure 액세스 제어 메서드를 사용하여 액세스할 수 있는 사용자를 제한하여 로그를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-113">Use standard Azure access control methods to secure your logs by restricting who can access them.</span></span>
* <span data-ttu-id="77519-114">더 이상 저장소 계정에 유지하지 않으려는 로그를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-114">Delete logs that you no longer want to keep in your storage account.</span></span>

<span data-ttu-id="77519-115">이 자습서를 사용하면 저장소 계정을 만들고 로깅을 활성화하고 수집되는 로깅 정보를 해석하는 Azure 키 자격 증명 모음을 시작하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77519-115">Use this tutorial to help you get started with Azure Key Vault logging, to create your storage account, enable logging, and interpret the logging information collected.</span></span>  

> [!NOTE]
> <span data-ttu-id="77519-116">이 자습서는 키 자격 증명 모음, 키 또는 암호를 만드는 방법에 대한 지침을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77519-116">This tutorial does not include instructions for how to create key vaults, keys, or secrets.</span></span> <span data-ttu-id="77519-117">자세한 내용은 [Azure 키 자격 증명 모음 시작](key-vault-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77519-117">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="77519-118">또는 플랫폼 간 명령줄 인터페이스 지침에 대한 참조는 [이 해당 자습서](key-vault-manage-with-cli2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77519-118">Or, for Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>
>
> <span data-ttu-id="77519-119">현재는 Azure 포털에서 Azure 키 자격 증명 모음을 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="77519-119">Currently, you cannot configure Azure Key Vault in the Azure portal.</span></span> <span data-ttu-id="77519-120">대신, 이 Azure PowerShell 지침을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-120">Instead, use these Azure PowerShell instructions.</span></span>
>
>

<span data-ttu-id="77519-121">Azure 키 자격 증명 모음에 대한 개요는 [Azure 키 자격 증명 모음이란?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="77519-121">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77519-122">필수 조건</span><span class="sxs-lookup"><span data-stu-id="77519-122">Prerequisites</span></span>
<span data-ttu-id="77519-123">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-123">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="77519-124">사용하고 있는 기존 키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="77519-124">An existing key vault that you have been using.</span></span>  
* <span data-ttu-id="77519-125">Azure PowerShell, **최소 버전 1.0.1**.</span><span class="sxs-lookup"><span data-stu-id="77519-125">Azure PowerShell, **minimum version of 1.0.1**.</span></span> <span data-ttu-id="77519-126">Azure PowerShell을 설치하고 Azure 구독에 연결하려면 [Azure PowerShell 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77519-126">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="77519-127">이미 Azure PowerShell가 설치되어 있고 버전을 알 수 없는 경우, Azure PowerShell 콘솔에서 `(Get-Module azure -ListAvailable).Version`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-127">If you have already installed Azure PowerShell and do not know the version, from the Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span>  
* <span data-ttu-id="77519-128">키 자격 증명 모음 로그에 대한 Azure의 충분한 저장소.</span><span class="sxs-lookup"><span data-stu-id="77519-128">Sufficient storage on Azure for your Key Vault logs.</span></span>

## <span data-ttu-id="77519-129"><a id="connect"></a>구독에 연결</span><span class="sxs-lookup"><span data-stu-id="77519-129"><a id="connect"></a>Connect to your subscriptions</span></span>
<span data-ttu-id="77519-130">Azure PowerShell 세션을 시작하고 다음 명령 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-130">Start an Azure PowerShell session and sign in to your Azure account with the following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="77519-131">팝업 브라우저 창에 Azure 계정 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-131">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="77519-132">Azure PowerShell은 이 계정과 연관된 모든 구독을 받고 기본적으로 첫 번째 구독을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-132">Azure PowerShell will get all the subscriptions that are associated with this account and by default, uses the first one.</span></span>

<span data-ttu-id="77519-133">구독이 여러 개인 경우 Azure Key Vault을 만드는 데 사용된 특정된 하나를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-133">If you have multiple subscriptions, you might have to specify a specific one that was used to create your Azure Key Vault.</span></span> <span data-ttu-id="77519-134">계정에 대한 구독을 보려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-134">Type the following to see the subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="77519-135">그런 다음 로깅하려는 키 자격 증명 모음과 연결된 구독을 지정하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-135">Then, to specify the subscription that's associated with your key vault you will be logging, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> <span data-ttu-id="77519-136">이 과정은 중요한 단계이며 사용자 계정에 여러 구독이 연결된 경우 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-136">This is an important step and especially helpful if you have multiple subscriptions associated with your account.</span></span> <span data-ttu-id="77519-137">이 단계를 건너뛰면 Microsoft.Insights를 등록하는 데 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77519-137">You may receive an error to register Microsoft.Insights if this step is skipped.</span></span>
>   
>

<span data-ttu-id="77519-138">Azure PowerShell 구성에 관한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77519-138">For more information about configuring Azure PowerShell, see  [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="77519-139"><a id="storage"></a>로그에 대한 새 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="77519-139"><a id="storage"></a>Create a new storage account for your logs</span></span>
<span data-ttu-id="77519-140">로그에 대해 기존 저장소 계정을 사용할 수 있지만 키 자격 증명 모음 로그 전용 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77519-140">Although you can use an existing storage account for your logs, we'll create a new storage account that will be dedicated to Key Vault logs.</span></span> <span data-ttu-id="77519-141">나중에 이를 지정해야 하는 경우 편의를 위해 **sa**라는 변수로 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-141">For convenience for when we have to specify this later, we'll store the details into a variable named **sa**.</span></span>

<span data-ttu-id="77519-142">추가적인 관리 편이성을 위해 키 자격 증명 모음을 포함하는 것과 동일한 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-142">For additional ease of management, we'll also use the same resource group as the one that contains our key vault.</span></span> <span data-ttu-id="77519-143">[시작 자습서](key-vault-get-started.md)에서 이 리소스 그룹은 **ContosoResourceGroup** 이며 동아시아 위치를 계속해서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-143">From the [getting started tutorial](key-vault-get-started.md), this resource group is named **ContosoResourceGroup** and we'll continue to use the East Asia location.</span></span> <span data-ttu-id="77519-144">이 값을 적절하게 사용자 고유 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-144">Substitute these values for your own, as applicable:</span></span>

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> <span data-ttu-id="77519-145">기존 저장소 계정을 사용하려는 경우 사용자 키 자격 증명 모음과 동일한 구독을 사용하고 클래식 배포 모델보다는 Resource Manager 배포 모델을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-145">If you decide to use an existing storage account, it must use the same subscription as your key vault and it must use the Resource Manager deployment model, rather than the Classic deployment model.</span></span>
>
>

## <span data-ttu-id="77519-146"><a id="identify"></a>로그에 대한 주요 자격 증명 모음 식별</span><span class="sxs-lookup"><span data-stu-id="77519-146"><a id="identify"></a>Identify the key vault for your logs</span></span>
<span data-ttu-id="77519-147">시작 자습서에서 주요 자격 증명 모음 이름은 **ContosoKeyVault**이었으므로 해당 이름을 계속해서 사용하고 **kv**라는 변수에 세부 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-147">In our getting started tutorial, our key vault name was **ContosoKeyVault**, so we'll continue to use that name and store the details into a variable named **kv**:</span></span>

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <span data-ttu-id="77519-148"><a id="enable"></a>로깅 사용</span><span class="sxs-lookup"><span data-stu-id="77519-148"><a id="enable"></a>Enable logging</span></span>
<span data-ttu-id="77519-149">키 자격 증명 모음에 대한 로깅을 사용하려면 새 저장소 계정 및 키 자격 증명 모음용으로 만든 변수와 함께 Set-AzureRmDiagnosticSetting cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-149">To enable logging for Key Vault, we'll use the Set-AzureRmDiagnosticSetting cmdlet, together with the variables we created for our new storage account and our key vault.</span></span> <span data-ttu-id="77519-150">**-Enabled** 플래그를 **$true**로 설정하고 범주를 AuditEvent(Key Vault 로깅에 대한 유일한 범주)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-150">We'll also set the **-Enabled** flag to **$true** and set the category to AuditEvent (the only category for Key Vault logging), :</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

<span data-ttu-id="77519-151">이에 대한 출력에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="77519-151">The output for this includes:</span></span>

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


<span data-ttu-id="77519-152">저장소 계정에 정보를 저장하는 사용자 키 자격 증명 모음에 로깅을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-152">This confirms that logging is now enabled for your key vault, saving information to your storage account.</span></span>

<span data-ttu-id="77519-153">선택적으로 오래된 로그를 자동으로 삭제하는 로그에 대한 보존 정책을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77519-153">Optionally you can also set retention policy for your logs such that older logs will be automatically deleted.</span></span> <span data-ttu-id="77519-154">예를 들어 **-RetentionEnabled** 플래그를 사용하여 보존 정책을 **$true**로 설정하고 **-RetentionInDays** 매개 변수를 **90**으로 설정하므로 90일보다 오래된 로그는 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="77519-154">For example, set retention policy using **-RetentionEnabled** flag to **$true** and set **-RetentionInDays** parameter to **90** so that logs older than 90 days will be automatically deleted.</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

<span data-ttu-id="77519-155">다음이 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="77519-155">What's logged:</span></span>

* <span data-ttu-id="77519-156">액세스 권한, 시스템 오류 또는 잘못된 요청으로 인해 실패한 요청을 포함하는 모든 인증된 REST API 요청이 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="77519-156">All authenticated REST API requests are logged, which includes failed requests as a result of access permissions, system errors or bad requests.</span></span>
* <span data-ttu-id="77519-157">키 자격 증명 모음 액세스 정책 만들기, 삭제, 설정 및 태그와 같은 키 자격 증명 모음 특성 업데이트를 포함하는 키 자격 증명 모음 자체에 대한 작업.</span><span class="sxs-lookup"><span data-stu-id="77519-157">Operations on the key vault itself, which includes creation, deletion, setting key vault access policies, and updating key vault attributes such as tags.</span></span>
* <span data-ttu-id="77519-158">이러한 키 또는 암호 만들기, 수정 또는 삭제를 포함하는 키 자격 증명 모음의 키 및 암호에 대한 작업, 키 서명, 확인, 암호화, 해독, 래핑 및 래핑 해제, 암호 가져오기, 키, 암호 및 버전 나열과 같은 작업.</span><span class="sxs-lookup"><span data-stu-id="77519-158">Operations on keys and secrets in the key vault, which includes creating, modifying, or deleting these keys or secrets; operations such as sign, verify, encrypt, decrypt, wrap and unwrap keys, get secrets, list keys and secrets and their versions.</span></span>
* <span data-ttu-id="77519-159">401 응답이 발생하는 인증되지 않은 요청.</span><span class="sxs-lookup"><span data-stu-id="77519-159">Unauthenticated requests that result in a 401 response.</span></span> <span data-ttu-id="77519-160">예를 들어 전달자 토큰이 없거나 형식이 잘못되거나 만료되거나 토큰이 잘못된 요청이 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-160">For example, requests that do not have a bearer token, or are malformed or expired, or have an invalid token.</span></span>  

## <span data-ttu-id="77519-161"><a id="access"></a>로그에 액세스</span><span class="sxs-lookup"><span data-stu-id="77519-161"><a id="access"></a>Access your logs</span></span>
<span data-ttu-id="77519-162">주요 자격 증명 모음 로그는 사용자가 제공한 저장소 계정의 **insights-logs-auditevent** 컨테이너에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="77519-162">Key vault logs are stored in the **insights-logs-auditevent** container in the storage account you provided.</span></span> <span data-ttu-id="77519-163">이 컨테이너에 있는 모든 Blob을 나열하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-163">To list all the blobs in this container, type:</span></span>

<span data-ttu-id="77519-164">먼저, 컨테이너 이름에 대한 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77519-164">First, create a variable for the container name.</span></span> <span data-ttu-id="77519-165">이 이름은 연습의 나머지 전체에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="77519-165">This will be used throughout the rest of the walk through.</span></span>

    $container = 'insights-logs-auditevent'

<span data-ttu-id="77519-166">이 컨테이너에 있는 모든 Blob을 나열하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-166">To list all the blobs in this container, type:</span></span>

    Get-AzureStorageBlob -Container $container -Context $sa.Context
<span data-ttu-id="77519-167">출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-167">The output will look something similar to this:</span></span>

<span data-ttu-id="77519-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span><span class="sxs-lookup"><span data-stu-id="77519-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span></span>

<span data-ttu-id="77519-169">**Name**</span><span class="sxs-lookup"><span data-stu-id="77519-169">**Name**</span></span>

- - -
<span data-ttu-id="77519-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="77519-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span></span>

<span data-ttu-id="77519-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="77519-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span></span>

<span data-ttu-id="77519-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span><span class="sxs-lookup"><span data-stu-id="77519-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span></span>

<span data-ttu-id="77519-173">이 출력에서 확인할 수 있듯이 Blob은 명명 규칙 **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="77519-173">As you can see from this output, the blobs follow a naming convention: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span></span>

<span data-ttu-id="77519-174">날짜 및 시간 값은 UTC를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-174">The date and time values use UTC.</span></span>

<span data-ttu-id="77519-175">여러 리소스에 대한 로그를 수집하는 데 동일한 저장소 계정을 사용할 수 있으므로 Blob 이름에 있는 전체 리소스 ID는 필요한 Blob에 액세스하거나 다운로드하는 데 매우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-175">Because the same storage account can be used to collect logs for multiple resources, the full resource ID in the blob name is very useful to access or download just the blobs that you need.</span></span> <span data-ttu-id="77519-176">하지만 그 전에 먼저 모든 Blob을 다운로드하는 방법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="77519-176">But before we do that, we'll first cover how to download all the blobs.</span></span>

<span data-ttu-id="77519-177">먼저 Blob을 다운로드할 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77519-177">First, create a folder to download the blobs.</span></span> <span data-ttu-id="77519-178">예:</span><span class="sxs-lookup"><span data-stu-id="77519-178">For example:</span></span>

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

<span data-ttu-id="77519-179">그런 다음 모든 Blob 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="77519-179">Then get a list of all blobs:</span></span>  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

<span data-ttu-id="77519-180">'Get-AzureStorageBlobContent'를 통해 이 목록을 파이프하여 Blob을 대상 폴더로 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-180">Pipe this list through 'Get-AzureStorageBlobContent' to download the blobs into our destination folder:</span></span>

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

<span data-ttu-id="77519-181">이 두 번째 명령을 실행할 때 Blob 이름의 **/** 구분 기호는 대상 폴더 아래에 전체 폴더 구조를 만들고 이 구조는 Blob을 파일로 다운로드하고 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="77519-181">When you run this second command, the **/** delimiter in the blob names create a full folder structure under the destination folder, and this structure will be used to download and store the blobs as files.</span></span>

<span data-ttu-id="77519-182">선택적으로 Blob을 다운로드하려면 와일드카드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-182">To selectively download blobs, use wildcards.</span></span> <span data-ttu-id="77519-183">예:</span><span class="sxs-lookup"><span data-stu-id="77519-183">For example:</span></span>

* <span data-ttu-id="77519-184">여러 키 자격 증명 모음이 있고 CONTOSOKEYVAULT3이라는 하나의 키 자격 증명 모음에 대한 로그를 다운로드하려는 경우:</span><span class="sxs-lookup"><span data-stu-id="77519-184">If you have multiple key vaults and want to download logs for just one key vault, named CONTOSOKEYVAULT3:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* <span data-ttu-id="77519-185">리소스 그룹이 여러 개이고 하나의 리소스 그룹에 대한 로그를 다운로드하려는 경우 `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`을(를) 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-185">If you have multiple resource groups and want to download logs for just one resource group, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* <span data-ttu-id="77519-186">2016년 1월의 모든 로그를 다운로드하려는 경우 `-Blob '*/year=2016/m=01/*'`을(를) 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-186">If you want to download all the logs for the month of January 2016, use `-Blob '*/year=2016/m=01/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

<span data-ttu-id="77519-187">이제 로그에 있는 것을 확인할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="77519-187">You're now ready to start looking at what's in the logs.</span></span> <span data-ttu-id="77519-188">진행하기 전에 알아야 할 Get-AzureRmDiagnosticSetting에 대한 두 개 이상의 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="77519-188">But before moving onto that, two more parameters for Get-AzureRmDiagnosticSetting that you might need to know:</span></span>

* <span data-ttu-id="77519-189">주요 자격 증명 모음 리소스의 진단 설정 상태를 쿼리하려면: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span><span class="sxs-lookup"><span data-stu-id="77519-189">To query the  status of diagnostic settings for your key vault resource: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span></span>
* <span data-ttu-id="77519-190">주요 자격 증명 모음 리소스의 로깅을 사용하지 않으려면: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span><span class="sxs-lookup"><span data-stu-id="77519-190">To disable logging for your key vault resource: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span></span>

## <span data-ttu-id="77519-191"><a id="interpret"></a>Key Vault 로그 해석</span><span class="sxs-lookup"><span data-stu-id="77519-191"><a id="interpret"></a>Interpret your Key Vault logs</span></span>
<span data-ttu-id="77519-192">개별 Blob은 JSON Blob 형식으로 텍스트로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="77519-192">Individual blobs are stored as text, formatted as a JSON blob.</span></span> <span data-ttu-id="77519-193">다음은 `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`을 실행하는 예제 로그 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="77519-193">This is an example log entry from running `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span></span>

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


<span data-ttu-id="77519-194">다음 표는 필드 이름 및 설명을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-194">The following table lists the field names and descriptions.</span></span>

| <span data-ttu-id="77519-195">필드 이름</span><span class="sxs-lookup"><span data-stu-id="77519-195">Field name</span></span> | <span data-ttu-id="77519-196">설명</span><span class="sxs-lookup"><span data-stu-id="77519-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="77519-197">실시간</span><span class="sxs-lookup"><span data-stu-id="77519-197">time</span></span> |<span data-ttu-id="77519-198">날짜 및 시간(UTC)</span><span class="sxs-lookup"><span data-stu-id="77519-198">Date and time (UTC).</span></span> |
| <span data-ttu-id="77519-199">resourceId</span><span class="sxs-lookup"><span data-stu-id="77519-199">resourceId</span></span> |<span data-ttu-id="77519-200">Azure 리소스 관리자 리소스 ID.</span><span class="sxs-lookup"><span data-stu-id="77519-200">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="77519-201">Key Vault 로그의 경우 이는 항상 Key Vault 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="77519-201">For Key Vault logs, this is always the  Key Vault resource ID.</span></span> |
| <span data-ttu-id="77519-202">operationName</span><span class="sxs-lookup"><span data-stu-id="77519-202">operationName</span></span> |<span data-ttu-id="77519-203">다음 표에 설명된 대로 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="77519-203">Name of the operation, as documented in the next table.</span></span> |
| <span data-ttu-id="77519-204">operationVersion</span><span class="sxs-lookup"><span data-stu-id="77519-204">operationVersion</span></span> |<span data-ttu-id="77519-205">클라이언트에서 요청한 REST API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="77519-205">This is the REST API version requested by the client.</span></span> |
| <span data-ttu-id="77519-206">카테고리</span><span class="sxs-lookup"><span data-stu-id="77519-206">category</span></span> |<span data-ttu-id="77519-207">키 자격 증명 모음 로그의 경우 AuditEvent는 단일의 사용 가능한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="77519-207">For Key Vault logs, AuditEvent is the single, available value.</span></span> |
| <span data-ttu-id="77519-208">resultType</span><span class="sxs-lookup"><span data-stu-id="77519-208">resultType</span></span> |<span data-ttu-id="77519-209">REST API 요청 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="77519-209">Result of REST API request.</span></span> |
| <span data-ttu-id="77519-210">resultSignature</span><span class="sxs-lookup"><span data-stu-id="77519-210">resultSignature</span></span> |<span data-ttu-id="77519-211">HTTP 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="77519-211">HTTP status.</span></span> |
| <span data-ttu-id="77519-212">resultDescription</span><span class="sxs-lookup"><span data-stu-id="77519-212">resultDescription</span></span> |<span data-ttu-id="77519-213">사용 가능한 경우 결과에 대한 추가 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="77519-213">Additional description about the result, when available.</span></span> |
| <span data-ttu-id="77519-214">durationMS</span><span class="sxs-lookup"><span data-stu-id="77519-214">durationMs</span></span> |<span data-ttu-id="77519-215">밀리초 단위로 REST API 요청을 처리하는 데 걸린 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="77519-215">Time it took to service the REST API request, in milliseconds.</span></span> <span data-ttu-id="77519-216">네트워크 대기 시간을 포함하지 않으므로 클라이언트 쪽에서 측정한 시간은 이 시간과 일치하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77519-216">This does not include the network latency, so the time you measure on the client side might not match this time.</span></span> |
| <span data-ttu-id="77519-217">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="77519-217">callerIpAddress</span></span> |<span data-ttu-id="77519-218">요청한 클라이언트의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="77519-218">IP address of the client who made the request.</span></span> |
| <span data-ttu-id="77519-219">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="77519-219">correlationId</span></span> |<span data-ttu-id="77519-220">클라이언트가 서비스 쪽(키 자격 증명 모음) 로그를 사용하여 클라이언트 쪽 로그 상관 관계를 지정하도록 전달할 수 있는 선택적 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="77519-220">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="77519-221">ID</span><span class="sxs-lookup"><span data-stu-id="77519-221">identity</span></span> |<span data-ttu-id="77519-222">REST API 요청을 수행할 때 제공된 토큰의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="77519-222">Identity from the token that was presented when making the REST API request.</span></span> <span data-ttu-id="77519-223">Azure PowerShell cmdlet에서 발생하는 요청의 경우처럼 이는 보통 "사용자", "서비스 주체" 또는 "사용자+appId"의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="77519-223">This is usually a "user", a "service principal" or a combination "user+appId" as in case of a request resulting from a Azure PowerShell cmdlet.</span></span> |
| <span data-ttu-id="77519-224">properties</span><span class="sxs-lookup"><span data-stu-id="77519-224">properties</span></span> |<span data-ttu-id="77519-225">이 필드는 작업(작업 이름)에 따라 다른 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="77519-225">This field will contain different information based on the operation (operationName).</span></span> <span data-ttu-id="77519-226">대부분의 경우 클라이언트 정보(클라이언트에서 전달한 useragent 문자열), 정확한 REST API 요청 URI 및 HTTP 상태 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-226">In most cases, contains client information (the useragent string passed by the client), the exact REST API request URI, and HTTP status code.</span></span> <span data-ttu-id="77519-227">또한 개체가 요청의 결과로 반환되면(예: KeyCreate 또는 VaultGet) 키 URI(“ID”로), 자격 증명 모음 URI 또는 암호 URI도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-227">In addition, when an object is returned as a result of a request (for example, KeyCreate or VaultGet) it will also contain the Key URI (as "id"), Vault URI, or Secret URI.</span></span> |

<span data-ttu-id="77519-228">**operationName** 필드 값은 ObjectVerb 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="77519-228">The **operationName** field values are in ObjectVerb format.</span></span> <span data-ttu-id="77519-229">예:</span><span class="sxs-lookup"><span data-stu-id="77519-229">For example:</span></span>

* <span data-ttu-id="77519-230">모든 주요 자격 증명 모음 작업은 `VaultGet`, `VaultCreate` 등의 'Vault`<action>`' 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="77519-230">All key vault operations have the 'Vault`<action>`' format, such as `VaultGet` and `VaultCreate`.</span></span>
* <span data-ttu-id="77519-231">모든 주요 작업은 `KeySign`, `KeyList` 등의 'Key`<action>`' 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="77519-231">All  key operations have the 'Key`<action>`' format, such as `KeySign` and `KeyList`.</span></span>
* <span data-ttu-id="77519-232">모든 암호 작업은 `SecretGet`, `SecretListVersions` 등의 'Secret`<action>`' 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="77519-232">All secret operations have the 'Secret`<action>`' format, such as `SecretGet` and `SecretListVersions`.</span></span>

<span data-ttu-id="77519-233">다음 표는 operationName 및 해당 REST API 명령을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-233">The following table lists the operationName and corresponding REST API command.</span></span>

| <span data-ttu-id="77519-234">operationName</span><span class="sxs-lookup"><span data-stu-id="77519-234">operationName</span></span> | <span data-ttu-id="77519-235">REST API 명령</span><span class="sxs-lookup"><span data-stu-id="77519-235">REST API Command</span></span> |
| --- | --- |
| <span data-ttu-id="77519-236">인증</span><span class="sxs-lookup"><span data-stu-id="77519-236">Authentication</span></span> |<span data-ttu-id="77519-237">Azure Active Directory 끝점을 통해</span><span class="sxs-lookup"><span data-stu-id="77519-237">Via Azure Active Directory endpoint</span></span> |
| <span data-ttu-id="77519-238">VaultGet</span><span class="sxs-lookup"><span data-stu-id="77519-238">VaultGet</span></span> |[<span data-ttu-id="77519-239">키 자격 증명 모음에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="77519-239">Get information about a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| <span data-ttu-id="77519-240">VaultPut</span><span class="sxs-lookup"><span data-stu-id="77519-240">VaultPut</span></span> |[<span data-ttu-id="77519-241">키 자격 증명 모음 만들기 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="77519-241">Create or update a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| <span data-ttu-id="77519-242">VaultDelete</span><span class="sxs-lookup"><span data-stu-id="77519-242">VaultDelete</span></span> |[<span data-ttu-id="77519-243">키 자격 증명 모음 삭제</span><span class="sxs-lookup"><span data-stu-id="77519-243">Delete a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| <span data-ttu-id="77519-244">VaultPatch</span><span class="sxs-lookup"><span data-stu-id="77519-244">VaultPatch</span></span> |[<span data-ttu-id="77519-245">키 자격 증명 모음 업데이트</span><span class="sxs-lookup"><span data-stu-id="77519-245">Update a key vault</span></span>](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| <span data-ttu-id="77519-246">VaultList</span><span class="sxs-lookup"><span data-stu-id="77519-246">VaultList</span></span> |[<span data-ttu-id="77519-247">리소스 그룹의 모든 키 자격 증명 모음 목록</span><span class="sxs-lookup"><span data-stu-id="77519-247">List all key vaults in a resource group</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| <span data-ttu-id="77519-248">KeyCreate</span><span class="sxs-lookup"><span data-stu-id="77519-248">KeyCreate</span></span> |[<span data-ttu-id="77519-249">키 만들기</span><span class="sxs-lookup"><span data-stu-id="77519-249">Create a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| <span data-ttu-id="77519-250">KeyGet</span><span class="sxs-lookup"><span data-stu-id="77519-250">KeyGet</span></span> |[<span data-ttu-id="77519-251">키에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="77519-251">Get information about a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| <span data-ttu-id="77519-252">KeyImport</span><span class="sxs-lookup"><span data-stu-id="77519-252">KeyImport</span></span> |[<span data-ttu-id="77519-253">자격 증명 모음으로 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="77519-253">Import a key into a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| <span data-ttu-id="77519-254">KeyBackup</span><span class="sxs-lookup"><span data-stu-id="77519-254">KeyBackup</span></span> |<span data-ttu-id="77519-255">[키 백업](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span><span class="sxs-lookup"><span data-stu-id="77519-255">[Backup a key](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span></span> |
| <span data-ttu-id="77519-256">KeyDelete</span><span class="sxs-lookup"><span data-stu-id="77519-256">KeyDelete</span></span> |[<span data-ttu-id="77519-257">키 삭제</span><span class="sxs-lookup"><span data-stu-id="77519-257">Delete a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| <span data-ttu-id="77519-258">KeyRestore</span><span class="sxs-lookup"><span data-stu-id="77519-258">KeyRestore</span></span> |[<span data-ttu-id="77519-259">키 복원</span><span class="sxs-lookup"><span data-stu-id="77519-259">Restore a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| <span data-ttu-id="77519-260">KeySign</span><span class="sxs-lookup"><span data-stu-id="77519-260">KeySign</span></span> |[<span data-ttu-id="77519-261">키로 서명</span><span class="sxs-lookup"><span data-stu-id="77519-261">Sign with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| <span data-ttu-id="77519-262">KeyVerify</span><span class="sxs-lookup"><span data-stu-id="77519-262">KeyVerify</span></span> |[<span data-ttu-id="77519-263">키로 확인</span><span class="sxs-lookup"><span data-stu-id="77519-263">Verify with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| <span data-ttu-id="77519-264">KeyWrap</span><span class="sxs-lookup"><span data-stu-id="77519-264">KeyWrap</span></span> |[<span data-ttu-id="77519-265">키 래핑</span><span class="sxs-lookup"><span data-stu-id="77519-265">Wrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| <span data-ttu-id="77519-266">KeyUnwrap</span><span class="sxs-lookup"><span data-stu-id="77519-266">KeyUnwrap</span></span> |[<span data-ttu-id="77519-267">키 래핑 취소</span><span class="sxs-lookup"><span data-stu-id="77519-267">Unwrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| <span data-ttu-id="77519-268">KeyEncrypt</span><span class="sxs-lookup"><span data-stu-id="77519-268">KeyEncrypt</span></span> |[<span data-ttu-id="77519-269">키로 암호화</span><span class="sxs-lookup"><span data-stu-id="77519-269">Encrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| <span data-ttu-id="77519-270">KeyDecrypt</span><span class="sxs-lookup"><span data-stu-id="77519-270">KeyDecrypt</span></span> |[<span data-ttu-id="77519-271">키로 암호 해독</span><span class="sxs-lookup"><span data-stu-id="77519-271">Decrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| <span data-ttu-id="77519-272">KeyUpdate</span><span class="sxs-lookup"><span data-stu-id="77519-272">KeyUpdate</span></span> |[<span data-ttu-id="77519-273">키 업데이트</span><span class="sxs-lookup"><span data-stu-id="77519-273">Update a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| <span data-ttu-id="77519-274">KeyList</span><span class="sxs-lookup"><span data-stu-id="77519-274">KeyList</span></span> |[<span data-ttu-id="77519-275">자격 증명 모음에 키 나열</span><span class="sxs-lookup"><span data-stu-id="77519-275">List the keys in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| <span data-ttu-id="77519-276">KeyListVersions</span><span class="sxs-lookup"><span data-stu-id="77519-276">KeyListVersions</span></span> |[<span data-ttu-id="77519-277">키 버전 나열</span><span class="sxs-lookup"><span data-stu-id="77519-277">List the versions of a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| <span data-ttu-id="77519-278">SecretSet</span><span class="sxs-lookup"><span data-stu-id="77519-278">SecretSet</span></span> |[<span data-ttu-id="77519-279">암호 만들기</span><span class="sxs-lookup"><span data-stu-id="77519-279">Create a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| <span data-ttu-id="77519-280">SecretGet</span><span class="sxs-lookup"><span data-stu-id="77519-280">SecretGet</span></span> |[<span data-ttu-id="77519-281">암호 가져오기</span><span class="sxs-lookup"><span data-stu-id="77519-281">Get secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| <span data-ttu-id="77519-282">SecretUpdate</span><span class="sxs-lookup"><span data-stu-id="77519-282">SecretUpdate</span></span> |[<span data-ttu-id="77519-283">암호 업데이트</span><span class="sxs-lookup"><span data-stu-id="77519-283">Update a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| <span data-ttu-id="77519-284">SecretDelete</span><span class="sxs-lookup"><span data-stu-id="77519-284">SecretDelete</span></span> |[<span data-ttu-id="77519-285">암호 삭제</span><span class="sxs-lookup"><span data-stu-id="77519-285">Delete a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| <span data-ttu-id="77519-286">SecretList</span><span class="sxs-lookup"><span data-stu-id="77519-286">SecretList</span></span> |[<span data-ttu-id="77519-287">자격 증명 모음에 암호 나열</span><span class="sxs-lookup"><span data-stu-id="77519-287">List secrets in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| <span data-ttu-id="77519-288">SecretListVersions</span><span class="sxs-lookup"><span data-stu-id="77519-288">SecretListVersions</span></span> |[<span data-ttu-id="77519-289">암호 버전 나열</span><span class="sxs-lookup"><span data-stu-id="77519-289">List versions of a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <span data-ttu-id="77519-290"><a id="loganalytics"></a>Log Analytics 사용</span><span class="sxs-lookup"><span data-stu-id="77519-290"><a id="loganalytics"></a>Use Log Analytics</span></span>

<span data-ttu-id="77519-291">Log Analytics에서 Azure Key Vault 솔루션을 사용하여 Azure Key Vault AuditEvent 로그를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77519-291">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span></span> <span data-ttu-id="77519-292">설정 방법을 비롯한 자세한 내용은 [Log Analytics의 Azure Key Vault 솔루션](../log-analytics/log-analytics-azure-key-vault.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77519-292">For more information, including how to set this up, see [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span></span> <span data-ttu-id="77519-293">또한 이 문서는 먼저 Azure Storage 계정으로 로그를 라우팅하고 해당 위치에서 읽도록 Log Analytics를 구성한 Log Analytics 미리 보기 중 제공된 이전 Key Vault 솔루션에서 마이그레이션해야 할 경우 지침을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="77519-293">This article also contains instructions if you need to migrate from the old Key Vault solution that was offered during the Log Analytics preview, where you first routed your logs to an Azure Storage account and configured Log Analytics to read from there.</span></span>

## <span data-ttu-id="77519-294"><a id="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="77519-294"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="77519-295">웹 응용 프로그램에서 Azure Key Vault를 사용하는 자습서는 [웹 응용 프로그램에서 Azure Key Vault 사용](key-vault-use-from-web-application.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77519-295">For a tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="77519-296">프로그래밍 참조는 [Azure 주요 자격 증명 모음 개발자 가이드](key-vault-developers-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77519-296">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

<span data-ttu-id="77519-297">Azure Key Vault의 Azure PowerShell 1.0 cmdlet 목록은 [Azure Key Vault Cmdlet](/powershell/module/azurerm.keyvault/#key_vault)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77519-297">For a list of Azure PowerShell 1.0 cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>

<span data-ttu-id="77519-298">Azure Key Vault을 사용하는 키 회전 및 로그 감사에 대한 자습서는 [종단 간 키 회전 및 감사를 사용하여 Key Vault를 설정하는 방법](key-vault-key-rotation-log-monitoring.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77519-298">For a tutorial on key rotation and log auditing with Azure Key Vault, see [How to setup Key Vault with end to end key rotation and auditing](key-vault-key-rotation-log-monitoring.md).</span></span>
