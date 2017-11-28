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
# <a name="azure-key-vault-logging"></a><span data-ttu-id="7c9b2-103">Azure 키 자격 증명 모음 로깅</span><span class="sxs-lookup"><span data-stu-id="7c9b2-103">Azure Key Vault Logging</span></span>
<span data-ttu-id="7c9b2-104">Azure 키 자격 증명 모음은 대부분 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="7c9b2-105">자세한 내용은 참조 hello [키 자격 증명 모음 가격 책정 페이지](https://azure.microsoft.com/pricing/details/key-vault/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="7c9b2-106">소개</span><span class="sxs-lookup"><span data-stu-id="7c9b2-106">Introduction</span></span>
<span data-ttu-id="7c9b2-107">하나 이상의 키 자격 증명 모음을 만든 후 toomonitor, 액세스 및 업데이트 수행자는 키 자격 증명 모음 시기와 방법을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-107">After you have created one or more key vaults, you will likely want toomonitor how and when your key vaults are accessed, and by whom.</span></span> <span data-ttu-id="7c9b2-108">Azure 저장소 계정에 제공하는 정보를 저장하는 키 자격 증명 모음에 대한 로깅을 사용하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-108">You can do this by enabling logging for Key Vault, which saves information in an Azure storage account that you provide.</span></span> <span data-ttu-id="7c9b2-109">**insights-logs-auditevent** 라는 새 컨테이너가 지정된 저장소 계정에 대해 자동으로 만들어지고 여러 키 자격 증명 모음에 대한 로그를 수집하기 위해 이 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-109">A new container named **insights-logs-auditevent** is automatically created for your specified storage account, and you can use this same storage account for collecting logs for multiple key vaults.</span></span>

<span data-ttu-id="7c9b2-110">최대 로깅 정보에 액세스할 수 있습니다, 자격 증명 모음 작업에 hello 키 후 10 분입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-110">You can access your logging information at most, 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="7c9b2-111">대부분의 경우 이것보다 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-111">In most cases, it will be quicker than this.</span></span>  <span data-ttu-id="7c9b2-112">저장소 계정에 로그를 tooyou toomanage를입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-112">It's up tooyou toomanage your logs in your storage account:</span></span>

* <span data-ttu-id="7c9b2-113">액세스할 수 있는 사용자를 제한 하 여 표준 Azure 액세스 제어 메서드 toosecure 로그를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-113">Use standard Azure access control methods toosecure your logs by restricting who can access them.</span></span>
* <span data-ttu-id="7c9b2-114">저장소 계정에 tookeep 없게 하려면 로그를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-114">Delete logs that you no longer want tookeep in your storage account.</span></span>

<span data-ttu-id="7c9b2-115">Azure 키 자격 증명 로깅, toocreate 시작 하기 자습서 toohelp이를 사용 하 여 저장소 계정의 로깅을 활성화 하 고 수집 된 hello 로깅 정보를 해석 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-115">Use this tutorial toohelp you get started with Azure Key Vault logging, toocreate your storage account, enable logging, and interpret hello logging information collected.</span></span>  

> [!NOTE]
> <span data-ttu-id="7c9b2-116">이 자습서는 toocreate 자격 증명 모음, 키 또는 암호를 입력 하는 방법에 대 한 지침을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-116">This tutorial does not include instructions for how toocreate key vaults, keys, or secrets.</span></span> <span data-ttu-id="7c9b2-117">자세한 내용은 [Azure 키 자격 증명 모음 시작](key-vault-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-117">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="7c9b2-118">또는 플랫폼 간 명령줄 인터페이스 지침에 대한 참조는 [이 해당 자습서](key-vault-manage-with-cli2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-118">Or, for Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>
>
> <span data-ttu-id="7c9b2-119">현재 hello Azure 포털에서에서 Azure 키 자격 증명 모음을 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-119">Currently, you cannot configure Azure Key Vault in hello Azure portal.</span></span> <span data-ttu-id="7c9b2-120">대신, 이 Azure PowerShell 지침을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-120">Instead, use these Azure PowerShell instructions.</span></span>
>
>

<span data-ttu-id="7c9b2-121">Azure 키 자격 증명 모음에 대한 개요는 [Azure 키 자격 증명 모음이란?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="7c9b2-121">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c9b2-122">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7c9b2-122">Prerequisites</span></span>
<span data-ttu-id="7c9b2-123">toocomplete이이 자습서에서는 다음 hello 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-123">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="7c9b2-124">사용하고 있는 기존 키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="7c9b2-124">An existing key vault that you have been using.</span></span>  
* <span data-ttu-id="7c9b2-125">Azure PowerShell, **최소 버전 1.0.1**.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-125">Azure PowerShell, **minimum version of 1.0.1**.</span></span> <span data-ttu-id="7c9b2-126">Azure PowerShell tooinstall Azure 구독과 연결을 참조 하세요 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-126">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="7c9b2-127">Azure PowerShell을 이미 설치 되어 있는 hello Azure PowerShell 콘솔에서 hello 버전 알지 못할 경우 입력 `(Get-Module azure -ListAvailable).Version`합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-127">If you have already installed Azure PowerShell and do not know hello version, from hello Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span>  
* <span data-ttu-id="7c9b2-128">키 자격 증명 모음 로그에 대한 Azure의 충분한 저장소.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-128">Sufficient storage on Azure for your Key Vault logs.</span></span>

## <span data-ttu-id="7c9b2-129"><a id="connect"></a>Tooyour 구독 연결</span><span class="sxs-lookup"><span data-stu-id="7c9b2-129"><a id="connect"></a>Connect tooyour subscriptions</span></span>
<span data-ttu-id="7c9b2-130">Azure PowerShell 세션을 시작 하 고 다음 명령을 hello로 tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-130">Start an Azure PowerShell session and sign in tooyour Azure account with hello following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="7c9b2-131">Hello 팝업 브라우저 창에서 Azure 계정 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-131">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="7c9b2-132">Azure PowerShell에는 기본적으로이 계정은 관련 된 모든 hello 등록이 가져오며, 사용 하 여 첫 번째 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-132">Azure PowerShell will get all hello subscriptions that are associated with this account and by default, uses hello first one.</span></span>

<span data-ttu-id="7c9b2-133">다중 구독인 경우 해야할 toospecify 하나를 사용 하는 toocreate Azure 키 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-133">If you have multiple subscriptions, you might have toospecify a specific one that was used toocreate your Azure Key Vault.</span></span> <span data-ttu-id="7c9b2-134">Hello toosee hello 구독 계정에 대해 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-134">Type hello following toosee hello subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="7c9b2-135">그런 다음 toospecify hello 연결 된 구독으로 키 자격 증명 모음이 있습니다 로깅 됩니다, 유형:</span><span class="sxs-lookup"><span data-stu-id="7c9b2-135">Then, toospecify hello subscription that's associated with your key vault you will be logging, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> <span data-ttu-id="7c9b2-136">이 과정은 중요한 단계이며 사용자 계정에 여러 구독이 연결된 경우 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-136">This is an important step and especially helpful if you have multiple subscriptions associated with your account.</span></span> <span data-ttu-id="7c9b2-137">이 단계를 건너뜁니다 오류 tooregister Microsoft.Insights 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-137">You may receive an error tooregister Microsoft.Insights if this step is skipped.</span></span>
>   
>

<span data-ttu-id="7c9b2-138">Azure PowerShell을 구성 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-138">For more information about configuring Azure PowerShell, see  [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="7c9b2-139"><a id="storage"></a>로그에 대한 새 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="7c9b2-139"><a id="storage"></a>Create a new storage account for your logs</span></span>
<span data-ttu-id="7c9b2-140">로그에 대 한 기존 저장소 계정을 사용 하 여 있지만 전용된 tooKey 자격 증명 모음 로그 수 있는 새 저장소 계정을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-140">Although you can use an existing storage account for your logs, we'll create a new storage account that will be dedicated tooKey Vault logs.</span></span> <span data-ttu-id="7c9b2-141">편의 위해 때 했으므로 toospecify이에 대 한 hello 세부 정보 라는 변수를 저장할 것 이라면 **sa**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-141">For convenience for when we have toospecify this later, we'll store hello details into a variable named **sa**.</span></span>

<span data-ttu-id="7c9b2-142">추가 관리 용이성도 사용 hello 우리의 주요 자격 증명 모음을 포함 하는 대로 동일한 리소스 그룹을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-142">For additional ease of management, we'll also use hello same resource group as hello one that contains our key vault.</span></span> <span data-ttu-id="7c9b2-143">Hello에서 [시작 자습서](key-vault-get-started.md),이 리소스 그룹 이름은 **ContosoResourceGroup** 및 toouse hello 동아시아 위치를 계속 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-143">From hello [getting started tutorial](key-vault-get-started.md), this resource group is named **ContosoResourceGroup** and we'll continue toouse hello East Asia location.</span></span> <span data-ttu-id="7c9b2-144">이 값을 적절하게 사용자 고유 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-144">Substitute these values for your own, as applicable:</span></span>

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> <span data-ttu-id="7c9b2-145">사용 해야 toouse 기존 저장소 계정을 결정 한 경우 hello 클래식 배포 모델 보다는 hello 리소스 관리자 배포 모델을 사용 해야 하며 주요 자격 증명 모음으로 동일한 구독 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-145">If you decide toouse an existing storage account, it must use hello same subscription as your key vault and it must use hello Resource Manager deployment model, rather than hello Classic deployment model.</span></span>
>
>

## <span data-ttu-id="7c9b2-146"><a id="identify"></a>식별 하면 로그에 대 한 hello에 키 자격 증명 모음.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-146"><a id="identify"></a>Identify hello key vault for your logs</span></span>
<span data-ttu-id="7c9b2-147">이 시작된 자습서 통해 주요 자격 증명 모음 이름 되었습니다 **ContosoKeyVault**이므로 이름을 지정 하 고 명명 된 변수로 hello 세부 정보를 저장 하는 toouse 노력할 것 **kv**:</span><span class="sxs-lookup"><span data-stu-id="7c9b2-147">In our getting started tutorial, our key vault name was **ContosoKeyVault**, so we'll continue toouse that name and store hello details into a variable named **kv**:</span></span>

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <span data-ttu-id="7c9b2-148"><a id="enable"></a>로깅 사용</span><span class="sxs-lookup"><span data-stu-id="7c9b2-148"><a id="enable"></a>Enable logging</span></span>
<span data-ttu-id="7c9b2-149">tooenable hello 집합 AzureRmDiagnosticSetting cmdlet를 사용 합니다, hello 변수 함께 우리의 새 저장소 계정 및 우리의 주요 자격 증명 모음에 대해 만든 키 자격 증명 모음에 대 한 로깅, 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-149">tooenable logging for Key Vault, we'll use hello Set-AzureRmDiagnosticSetting cmdlet, together with hello variables we created for our new storage account and our key vault.</span></span> <span data-ttu-id="7c9b2-150">Hello 바로잡을 수 또한 **-활성화** 너무 플래그**$true** hello 범주 tooAuditEvent (hello만 범주 키 자격 증명 모음 로깅에 대 한), 설정 및:</span><span class="sxs-lookup"><span data-stu-id="7c9b2-150">We'll also set hello **-Enabled** flag too**$true** and set hello category tooAuditEvent (hello only category for Key Vault logging), :</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

<span data-ttu-id="7c9b2-151">이 대 한 hello 출력에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-151">hello output for this includes:</span></span>

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


<span data-ttu-id="7c9b2-152">로깅 주요 자격 증명 모음을 저장 하는 정보 tooyour 저장소 계정에 대 한 기능이 이제 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-152">This confirms that logging is now enabled for your key vault, saving information tooyour storage account.</span></span>

<span data-ttu-id="7c9b2-153">선택적으로 오래된 로그를 자동으로 삭제하는 로그에 대한 보존 정책을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-153">Optionally you can also set retention policy for your logs such that older logs will be automatically deleted.</span></span> <span data-ttu-id="7c9b2-154">예를 들어, 사용 하 여 보존 정책을 설정 **-RetentionEnabled** 너무 플래그**$true** 설정 **-RetentionInDays** 매개 변수가 너무**90** 하므로 90 일 보다 오래 된 로그가 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-154">For example, set retention policy using **-RetentionEnabled** flag too**$true** and set **-RetentionInDays** parameter too**90** so that logs older than 90 days will be automatically deleted.</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

<span data-ttu-id="7c9b2-155">다음이 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-155">What's logged:</span></span>

* <span data-ttu-id="7c9b2-156">액세스 권한, 시스템 오류 또는 잘못된 요청으로 인해 실패한 요청을 포함하는 모든 인증된 REST API 요청이 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-156">All authenticated REST API requests are logged, which includes failed requests as a result of access permissions, system errors or bad requests.</span></span>
* <span data-ttu-id="7c9b2-157">Hello 키에 대 한 작업 생성, 삭제, 주요 자격 증명 모음 액세스 정책 설정를 포함 하는 자체 자격 증명 모음 및 태그와 같은 주요 자격 증명 모음 특성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-157">Operations on hello key vault itself, which includes creation, deletion, setting key vault access policies, and updating key vault attributes such as tags.</span></span>
* <span data-ttu-id="7c9b2-158">키와 hello 키 자격 증명 모음에, 만들기, 수정 또는 삭제 이러한 키 또는 암호; 포함 하는 암호에 대 한 작업 기호 등의 작업 확인, 암호화, 암호를 해독, 줄 바꿈 및 unwrap 키, 암호, 키 나열 및 기밀 정보 및 해당 버전을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-158">Operations on keys and secrets in hello key vault, which includes creating, modifying, or deleting these keys or secrets; operations such as sign, verify, encrypt, decrypt, wrap and unwrap keys, get secrets, list keys and secrets and their versions.</span></span>
* <span data-ttu-id="7c9b2-159">401 응답이 발생하는 인증되지 않은 요청.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-159">Unauthenticated requests that result in a 401 response.</span></span> <span data-ttu-id="7c9b2-160">예를 들어 전달자 토큰이 없거나 형식이 잘못되거나 만료되거나 토큰이 잘못된 요청이 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-160">For example, requests that do not have a bearer token, or are malformed or expired, or have an invalid token.</span></span>  

## <span data-ttu-id="7c9b2-161"><a id="access"></a>로그에 액세스</span><span class="sxs-lookup"><span data-stu-id="7c9b2-161"><a id="access"></a>Access your logs</span></span>
<span data-ttu-id="7c9b2-162">주요 자격 증명 모음 로그 hello에 저장 됩니다 **insights-로그-auditevent** 제공한 hello 저장소 계정의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-162">Key vault logs are stored in hello **insights-logs-auditevent** container in hello storage account you provided.</span></span> <span data-ttu-id="7c9b2-163">toolist이이 컨테이너의 모든 hello blob를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-163">toolist all hello blobs in this container, type:</span></span>

<span data-ttu-id="7c9b2-164">먼저 hello 컨테이너 이름에 대 한 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-164">First, create a variable for hello container name.</span></span> <span data-ttu-id="7c9b2-165">Hello 나머지 hello 연습을 전체에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-165">This will be used throughout hello rest of hello walk through.</span></span>

    $container = 'insights-logs-auditevent'

<span data-ttu-id="7c9b2-166">toolist이이 컨테이너의 모든 hello blob를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-166">toolist all hello blobs in this container, type:</span></span>

    Get-AzureStorageBlob -Container $container -Context $sa.Context
<span data-ttu-id="7c9b2-167">hello 출력에는 다음과 유사한 toothis 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-167">hello output will look something similar toothis:</span></span>

<span data-ttu-id="7c9b2-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span><span class="sxs-lookup"><span data-stu-id="7c9b2-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span></span>

<span data-ttu-id="7c9b2-169">**Name**</span><span class="sxs-lookup"><span data-stu-id="7c9b2-169">**Name**</span></span>

- - -
<span data-ttu-id="7c9b2-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="7c9b2-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span></span>

<span data-ttu-id="7c9b2-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="7c9b2-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span></span>

<span data-ttu-id="7c9b2-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span><span class="sxs-lookup"><span data-stu-id="7c9b2-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span></span>

<span data-ttu-id="7c9b2-173">이 출력을 알 수 있듯이 hello blob 명명 규칙을 지키는: **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>h / =<hour>/m =<minute>/filename.json**</span><span class="sxs-lookup"><span data-stu-id="7c9b2-173">As you can see from this output, hello blobs follow a naming convention: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span></span>

<span data-ttu-id="7c9b2-174">UTC를 사용 하는 hello 날짜 및 시간 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-174">hello date and time values use UTC.</span></span>

<span data-ttu-id="7c9b2-175">Hello 동일한 저장소 계정을 일 수 있으므로 여러 리소스에 대 한 로그를 사용 하는 toocollect hello 전체 리소스 ID hello blob 이름에는 매우 유용한 tooaccess 또는 필요한 정당한 hello blob를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-175">Because hello same storage account can be used toocollect logs for multiple resources, hello full resource ID in hello blob name is very useful tooaccess or download just hello blobs that you need.</span></span> <span data-ttu-id="7c9b2-176">그 전에 먼저 다룰 것 이지만 어떻게 toodownload blob hello 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-176">But before we do that, we'll first cover how toodownload all hello blobs.</span></span>

<span data-ttu-id="7c9b2-177">먼저 폴더 toodownload hello를 blob 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-177">First, create a folder toodownload hello blobs.</span></span> <span data-ttu-id="7c9b2-178">예:</span><span class="sxs-lookup"><span data-stu-id="7c9b2-178">For example:</span></span>

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

<span data-ttu-id="7c9b2-179">그런 다음 모든 Blob 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-179">Then get a list of all blobs:</span></span>  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

<span data-ttu-id="7c9b2-180">이 대상 폴더에 ' Get AzureStorageBlobContent' toodownload hello blob 통해이 목록을 파이프할:</span><span class="sxs-lookup"><span data-stu-id="7c9b2-180">Pipe this list through 'Get-AzureStorageBlobContent' toodownload hello blobs into our destination folder:</span></span>

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

<span data-ttu-id="7c9b2-181">이 두 번째 명령은 실행 하면 hello  **/**  hello blob 이름에 구분 기호가 hello 대상 폴더에서 전체 폴더 구조를 만들고이 구조체 파일로 toodownload 및 저장소 hello blob 사용된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-181">When you run this second command, hello **/** delimiter in hello blob names create a full folder structure under hello destination folder, and this structure will be used toodownload and store hello blobs as files.</span></span>

<span data-ttu-id="7c9b2-182">tooselectively는 blob 다운로드 전용, 와일드 카드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-182">tooselectively download blobs, use wildcards.</span></span> <span data-ttu-id="7c9b2-183">예:</span><span class="sxs-lookup"><span data-stu-id="7c9b2-183">For example:</span></span>

* <span data-ttu-id="7c9b2-184">여러 키 자격 증명 모음 있고 하나의 키 자격 증명 모음에 대해 toodownload 로그를 원하는 경우 CONTOSOKEYVAULT3 이라는 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-184">If you have multiple key vaults and want toodownload logs for just one key vault, named CONTOSOKEYVAULT3:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* <span data-ttu-id="7c9b2-185">리소스 그룹이 여러 개 있는 하나의 리소스 그룹에 대 한 toodownload 로그를 사용할 경우 사용 하 여 `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span><span class="sxs-lookup"><span data-stu-id="7c9b2-185">If you have multiple resource groups and want toodownload logs for just one resource group, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* <span data-ttu-id="7c9b2-186">사용 하 여 2016 년 1 월의 hello 월에 대 한 모든 hello 로그 toodownload 않으려면 `-Blob '*/year=2016/m=01/*'`:</span><span class="sxs-lookup"><span data-stu-id="7c9b2-186">If you want toodownload all hello logs for hello month of January 2016, use `-Blob '*/year=2016/m=01/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

<span data-ttu-id="7c9b2-187">Hello에 무엇이 살펴보면 준비 toostart 로그 이제 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-187">You're now ready toostart looking at what's in hello logs.</span></span> <span data-ttu-id="7c9b2-188">으로 하는 Get AzureRmDiagnosticSetting tooknow이 필요할 수 있습니다에 대 한 매개 변수 두 개를 더 진행 하기 전에:</span><span class="sxs-lookup"><span data-stu-id="7c9b2-188">But before moving onto that, two more parameters for Get-AzureRmDiagnosticSetting that you might need tooknow:</span></span>

* <span data-ttu-id="7c9b2-189">주요 자격 증명 모음 리소스에 대 한 진단 설정의 tooquery hello 상태:`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span><span class="sxs-lookup"><span data-stu-id="7c9b2-189">tooquery hello  status of diagnostic settings for your key vault resource: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span></span>
* <span data-ttu-id="7c9b2-190">주요 자격 증명 모음 리소스에 대 한 toodisable 로깅:`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span><span class="sxs-lookup"><span data-stu-id="7c9b2-190">toodisable logging for your key vault resource: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span></span>

## <span data-ttu-id="7c9b2-191"><a id="interpret"></a>Key Vault 로그 해석</span><span class="sxs-lookup"><span data-stu-id="7c9b2-191"><a id="interpret"></a>Interpret your Key Vault logs</span></span>
<span data-ttu-id="7c9b2-192">개별 Blob은 JSON Blob 형식으로 텍스트로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-192">Individual blobs are stored as text, formatted as a JSON blob.</span></span> <span data-ttu-id="7c9b2-193">다음은 `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`을 실행하는 예제 로그 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-193">This is an example log entry from running `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span></span>

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


<span data-ttu-id="7c9b2-194">hello 다음 표에 나열 hello 필드 이름 및 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-194">hello following table lists hello field names and descriptions.</span></span>

| <span data-ttu-id="7c9b2-195">필드 이름</span><span class="sxs-lookup"><span data-stu-id="7c9b2-195">Field name</span></span> | <span data-ttu-id="7c9b2-196">설명</span><span class="sxs-lookup"><span data-stu-id="7c9b2-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7c9b2-197">실시간</span><span class="sxs-lookup"><span data-stu-id="7c9b2-197">time</span></span> |<span data-ttu-id="7c9b2-198">날짜 및 시간(UTC)</span><span class="sxs-lookup"><span data-stu-id="7c9b2-198">Date and time (UTC).</span></span> |
| <span data-ttu-id="7c9b2-199">resourceId</span><span class="sxs-lookup"><span data-stu-id="7c9b2-199">resourceId</span></span> |<span data-ttu-id="7c9b2-200">Azure 리소스 관리자 리소스 ID.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-200">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="7c9b2-201">주요 자격 증명 모음 로그의 경우이 항상 hello 키 자격 증명 모음 리소스 id입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-201">For Key Vault logs, this is always hello  Key Vault resource ID.</span></span> |
| <span data-ttu-id="7c9b2-202">operationName</span><span class="sxs-lookup"><span data-stu-id="7c9b2-202">operationName</span></span> |<span data-ttu-id="7c9b2-203">Hello 다음 표에 설명 된 대로 hello 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-203">Name of hello operation, as documented in hello next table.</span></span> |
| <span data-ttu-id="7c9b2-204">operationVersion</span><span class="sxs-lookup"><span data-stu-id="7c9b2-204">operationVersion</span></span> |<span data-ttu-id="7c9b2-205">Hello 클라이언트에서 요청한 hello REST API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-205">This is hello REST API version requested by hello client.</span></span> |
| <span data-ttu-id="7c9b2-206">카테고리</span><span class="sxs-lookup"><span data-stu-id="7c9b2-206">category</span></span> |<span data-ttu-id="7c9b2-207">주요 자격 증명 모음 로그 AuditEvent hello를 사용할 수 있는 단일 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-207">For Key Vault logs, AuditEvent is hello single, available value.</span></span> |
| <span data-ttu-id="7c9b2-208">resultType</span><span class="sxs-lookup"><span data-stu-id="7c9b2-208">resultType</span></span> |<span data-ttu-id="7c9b2-209">REST API 요청 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-209">Result of REST API request.</span></span> |
| <span data-ttu-id="7c9b2-210">resultSignature</span><span class="sxs-lookup"><span data-stu-id="7c9b2-210">resultSignature</span></span> |<span data-ttu-id="7c9b2-211">HTTP 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-211">HTTP status.</span></span> |
| <span data-ttu-id="7c9b2-212">resultDescription</span><span class="sxs-lookup"><span data-stu-id="7c9b2-212">resultDescription</span></span> |<span data-ttu-id="7c9b2-213">사용 가능한 경우 hello 결과 대 한 자세한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-213">Additional description about hello result, when available.</span></span> |
| <span data-ttu-id="7c9b2-214">durationMS</span><span class="sxs-lookup"><span data-stu-id="7c9b2-214">durationMs</span></span> |<span data-ttu-id="7c9b2-215">밀리초 단위로 tooservice hello REST API 요청에 소요 된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-215">Time it took tooservice hello REST API request, in milliseconds.</span></span> <span data-ttu-id="7c9b2-216">Hello 클라이언트 쪽에서 측정 hello 시간이 이번 일치 하지 않을 수 있으므로 hello 네트워크 대기 시간, 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-216">This does not include hello network latency, so hello time you measure on hello client side might not match this time.</span></span> |
| <span data-ttu-id="7c9b2-217">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="7c9b2-217">callerIpAddress</span></span> |<span data-ttu-id="7c9b2-218">Hello 요청을 수행한 hello 클라이언트의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-218">IP address of hello client who made hello request.</span></span> |
| <span data-ttu-id="7c9b2-219">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="7c9b2-219">correlationId</span></span> |<span data-ttu-id="7c9b2-220">클라이언트 hello 선택적 GUID가 toocorrelate 서비스 측 (키 자격 증명 모음) 로그를 사용 하 여 클라이언트 쪽 로그를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-220">An optional GUID that hello client can pass toocorrelate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="7c9b2-221">ID</span><span class="sxs-lookup"><span data-stu-id="7c9b2-221">identity</span></span> |<span data-ttu-id="7c9b2-222">Hello REST API 요청을 만드는 경우에 발표 hello 토큰에서 id입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-222">Identity from hello token that was presented when making hello REST API request.</span></span> <span data-ttu-id="7c9b2-223">Azure PowerShell cmdlet에서 발생하는 요청의 경우처럼 이는 보통 "사용자", "서비스 주체" 또는 "사용자+appId"의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-223">This is usually a "user", a "service principal" or a combination "user+appId" as in case of a request resulting from a Azure PowerShell cmdlet.</span></span> |
| <span data-ttu-id="7c9b2-224">properties</span><span class="sxs-lookup"><span data-stu-id="7c9b2-224">properties</span></span> |<span data-ttu-id="7c9b2-225">이 필드는 hello 작업 (작업 이름)에 따라 다른 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-225">This field will contain different information based on hello operation (operationName).</span></span> <span data-ttu-id="7c9b2-226">대부분의 경우에는 클라이언트 정보가 (hello useragent에서 전달 된 문자열 hello 클라이언트), 들어 hello 정확한 REST API 요청 URI 및 HTTP 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-226">In most cases, contains client information (hello useragent string passed by hello client), hello exact REST API request URI, and HTTP status code.</span></span> <span data-ttu-id="7c9b2-227">또한 개체 (예를 들어 KeyCreate 또는 VaultGet) 요청의 결과로 반환 될 때 키 URI ("id")로, 자격 증명 모음 URI 또는 URI 비밀 hello를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-227">In addition, when an object is returned as a result of a request (for example, KeyCreate or VaultGet) it will also contain hello Key URI (as "id"), Vault URI, or Secret URI.</span></span> |

<span data-ttu-id="7c9b2-228">hello **operationName** 필드 값은 ObjectVerb 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-228">hello **operationName** field values are in ObjectVerb format.</span></span> <span data-ttu-id="7c9b2-229">예:</span><span class="sxs-lookup"><span data-stu-id="7c9b2-229">For example:</span></span>

* <span data-ttu-id="7c9b2-230">모든 주요 자격 증명 모음 작업 체계가 hello ' 자격 증명 모음`<action>`' 형식으로 `VaultGet` 및 `VaultCreate`합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-230">All key vault operations have hello 'Vault`<action>`' format, such as `VaultGet` and `VaultCreate`.</span></span>
* <span data-ttu-id="7c9b2-231">모든 주요 작업 체계가 hello ' 키`<action>`' 형식으로 `KeySign` 및 `KeyList`합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-231">All  key operations have hello 'Key`<action>`' format, such as `KeySign` and `KeyList`.</span></span>
* <span data-ttu-id="7c9b2-232">모든 보안 작업 체계가 hello ' 비밀`<action>`' 형식으로 `SecretGet` 및 `SecretListVersions`합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-232">All secret operations have hello 'Secret`<action>`' format, such as `SecretGet` and `SecretListVersions`.</span></span>

<span data-ttu-id="7c9b2-233">다음 표에서 hello hello operationName 및 해당 하는 REST API 명령을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-233">hello following table lists hello operationName and corresponding REST API command.</span></span>

| <span data-ttu-id="7c9b2-234">operationName</span><span class="sxs-lookup"><span data-stu-id="7c9b2-234">operationName</span></span> | <span data-ttu-id="7c9b2-235">REST API 명령</span><span class="sxs-lookup"><span data-stu-id="7c9b2-235">REST API Command</span></span> |
| --- | --- |
| <span data-ttu-id="7c9b2-236">인증</span><span class="sxs-lookup"><span data-stu-id="7c9b2-236">Authentication</span></span> |<span data-ttu-id="7c9b2-237">Azure Active Directory 끝점을 통해</span><span class="sxs-lookup"><span data-stu-id="7c9b2-237">Via Azure Active Directory endpoint</span></span> |
| <span data-ttu-id="7c9b2-238">VaultGet</span><span class="sxs-lookup"><span data-stu-id="7c9b2-238">VaultGet</span></span> |[<span data-ttu-id="7c9b2-239">키 자격 증명 모음에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="7c9b2-239">Get information about a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| <span data-ttu-id="7c9b2-240">VaultPut</span><span class="sxs-lookup"><span data-stu-id="7c9b2-240">VaultPut</span></span> |[<span data-ttu-id="7c9b2-241">키 자격 증명 모음 만들기 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="7c9b2-241">Create or update a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| <span data-ttu-id="7c9b2-242">VaultDelete</span><span class="sxs-lookup"><span data-stu-id="7c9b2-242">VaultDelete</span></span> |[<span data-ttu-id="7c9b2-243">키 자격 증명 모음 삭제</span><span class="sxs-lookup"><span data-stu-id="7c9b2-243">Delete a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| <span data-ttu-id="7c9b2-244">VaultPatch</span><span class="sxs-lookup"><span data-stu-id="7c9b2-244">VaultPatch</span></span> |[<span data-ttu-id="7c9b2-245">키 자격 증명 모음 업데이트</span><span class="sxs-lookup"><span data-stu-id="7c9b2-245">Update a key vault</span></span>](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| <span data-ttu-id="7c9b2-246">VaultList</span><span class="sxs-lookup"><span data-stu-id="7c9b2-246">VaultList</span></span> |[<span data-ttu-id="7c9b2-247">리소스 그룹의 모든 키 자격 증명 모음 목록</span><span class="sxs-lookup"><span data-stu-id="7c9b2-247">List all key vaults in a resource group</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| <span data-ttu-id="7c9b2-248">KeyCreate</span><span class="sxs-lookup"><span data-stu-id="7c9b2-248">KeyCreate</span></span> |[<span data-ttu-id="7c9b2-249">키 만들기</span><span class="sxs-lookup"><span data-stu-id="7c9b2-249">Create a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| <span data-ttu-id="7c9b2-250">KeyGet</span><span class="sxs-lookup"><span data-stu-id="7c9b2-250">KeyGet</span></span> |[<span data-ttu-id="7c9b2-251">키에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="7c9b2-251">Get information about a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| <span data-ttu-id="7c9b2-252">KeyImport</span><span class="sxs-lookup"><span data-stu-id="7c9b2-252">KeyImport</span></span> |[<span data-ttu-id="7c9b2-253">자격 증명 모음으로 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="7c9b2-253">Import a key into a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| <span data-ttu-id="7c9b2-254">KeyBackup</span><span class="sxs-lookup"><span data-stu-id="7c9b2-254">KeyBackup</span></span> |<span data-ttu-id="7c9b2-255">[키 백업](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c9b2-255">[Backup a key](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span></span> |
| <span data-ttu-id="7c9b2-256">KeyDelete</span><span class="sxs-lookup"><span data-stu-id="7c9b2-256">KeyDelete</span></span> |[<span data-ttu-id="7c9b2-257">키 삭제</span><span class="sxs-lookup"><span data-stu-id="7c9b2-257">Delete a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| <span data-ttu-id="7c9b2-258">KeyRestore</span><span class="sxs-lookup"><span data-stu-id="7c9b2-258">KeyRestore</span></span> |[<span data-ttu-id="7c9b2-259">키 복원</span><span class="sxs-lookup"><span data-stu-id="7c9b2-259">Restore a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| <span data-ttu-id="7c9b2-260">KeySign</span><span class="sxs-lookup"><span data-stu-id="7c9b2-260">KeySign</span></span> |[<span data-ttu-id="7c9b2-261">키로 서명</span><span class="sxs-lookup"><span data-stu-id="7c9b2-261">Sign with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| <span data-ttu-id="7c9b2-262">KeyVerify</span><span class="sxs-lookup"><span data-stu-id="7c9b2-262">KeyVerify</span></span> |[<span data-ttu-id="7c9b2-263">키로 확인</span><span class="sxs-lookup"><span data-stu-id="7c9b2-263">Verify with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| <span data-ttu-id="7c9b2-264">KeyWrap</span><span class="sxs-lookup"><span data-stu-id="7c9b2-264">KeyWrap</span></span> |[<span data-ttu-id="7c9b2-265">키 래핑</span><span class="sxs-lookup"><span data-stu-id="7c9b2-265">Wrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| <span data-ttu-id="7c9b2-266">KeyUnwrap</span><span class="sxs-lookup"><span data-stu-id="7c9b2-266">KeyUnwrap</span></span> |[<span data-ttu-id="7c9b2-267">키 래핑 취소</span><span class="sxs-lookup"><span data-stu-id="7c9b2-267">Unwrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| <span data-ttu-id="7c9b2-268">KeyEncrypt</span><span class="sxs-lookup"><span data-stu-id="7c9b2-268">KeyEncrypt</span></span> |[<span data-ttu-id="7c9b2-269">키로 암호화</span><span class="sxs-lookup"><span data-stu-id="7c9b2-269">Encrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| <span data-ttu-id="7c9b2-270">KeyDecrypt</span><span class="sxs-lookup"><span data-stu-id="7c9b2-270">KeyDecrypt</span></span> |[<span data-ttu-id="7c9b2-271">키로 암호 해독</span><span class="sxs-lookup"><span data-stu-id="7c9b2-271">Decrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| <span data-ttu-id="7c9b2-272">KeyUpdate</span><span class="sxs-lookup"><span data-stu-id="7c9b2-272">KeyUpdate</span></span> |[<span data-ttu-id="7c9b2-273">키 업데이트</span><span class="sxs-lookup"><span data-stu-id="7c9b2-273">Update a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| <span data-ttu-id="7c9b2-274">KeyList</span><span class="sxs-lookup"><span data-stu-id="7c9b2-274">KeyList</span></span> |[<span data-ttu-id="7c9b2-275">자격 증명 모음의 hello 키 나열</span><span class="sxs-lookup"><span data-stu-id="7c9b2-275">List hello keys in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| <span data-ttu-id="7c9b2-276">KeyListVersions</span><span class="sxs-lookup"><span data-stu-id="7c9b2-276">KeyListVersions</span></span> |[<span data-ttu-id="7c9b2-277">키의 hello 버전 나열</span><span class="sxs-lookup"><span data-stu-id="7c9b2-277">List hello versions of a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| <span data-ttu-id="7c9b2-278">SecretSet</span><span class="sxs-lookup"><span data-stu-id="7c9b2-278">SecretSet</span></span> |[<span data-ttu-id="7c9b2-279">암호 만들기</span><span class="sxs-lookup"><span data-stu-id="7c9b2-279">Create a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| <span data-ttu-id="7c9b2-280">SecretGet</span><span class="sxs-lookup"><span data-stu-id="7c9b2-280">SecretGet</span></span> |[<span data-ttu-id="7c9b2-281">암호 가져오기</span><span class="sxs-lookup"><span data-stu-id="7c9b2-281">Get secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| <span data-ttu-id="7c9b2-282">SecretUpdate</span><span class="sxs-lookup"><span data-stu-id="7c9b2-282">SecretUpdate</span></span> |[<span data-ttu-id="7c9b2-283">암호 업데이트</span><span class="sxs-lookup"><span data-stu-id="7c9b2-283">Update a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| <span data-ttu-id="7c9b2-284">SecretDelete</span><span class="sxs-lookup"><span data-stu-id="7c9b2-284">SecretDelete</span></span> |[<span data-ttu-id="7c9b2-285">암호 삭제</span><span class="sxs-lookup"><span data-stu-id="7c9b2-285">Delete a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| <span data-ttu-id="7c9b2-286">SecretList</span><span class="sxs-lookup"><span data-stu-id="7c9b2-286">SecretList</span></span> |[<span data-ttu-id="7c9b2-287">자격 증명 모음에 암호 나열</span><span class="sxs-lookup"><span data-stu-id="7c9b2-287">List secrets in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| <span data-ttu-id="7c9b2-288">SecretListVersions</span><span class="sxs-lookup"><span data-stu-id="7c9b2-288">SecretListVersions</span></span> |[<span data-ttu-id="7c9b2-289">암호 버전 나열</span><span class="sxs-lookup"><span data-stu-id="7c9b2-289">List versions of a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <span data-ttu-id="7c9b2-290"><a id="loganalytics"></a>Log Analytics 사용</span><span class="sxs-lookup"><span data-stu-id="7c9b2-290"><a id="loganalytics"></a>Use Log Analytics</span></span>

<span data-ttu-id="7c9b2-291">로그 분석 tooreview Azure 키 자격 증명 모음 AuditEvent 로그에서 hello Azure 키 자격 증명 모음 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-291">You can use hello Azure Key Vault solution in Log Analytics tooreview Azure Key Vault AuditEvent logs.</span></span> <span data-ttu-id="7c9b2-292">를 비롯 한 자세한 내용은 tooset,이 확인 하려면 어떻게 [로그 분석에서 Azure 키 자격 증명 모음 솔루션](../log-analytics/log-analytics-azure-key-vault.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-292">For more information, including how tooset this up, see [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span></span> <span data-ttu-id="7c9b2-293">또한이 문서 toomigrate hello 로그 분석 미리 보기, 먼저 Azure 저장소 계정에 로그 tooan 라우팅된 하 고 있는 로그 분석 tooread 여기에서 구성 하는 동안 제공 된 hello 이전 하는 주요 자격 증명 모음 솔루션에서 해야 할 경우 지침을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-293">This article also contains instructions if you need toomigrate from hello old Key Vault solution that was offered during hello Log Analytics preview, where you first routed your logs tooan Azure Storage account and configured Log Analytics tooread from there.</span></span>

## <span data-ttu-id="7c9b2-294"><a id="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="7c9b2-294"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="7c9b2-295">웹 응용 프로그램에서 Azure Key Vault를 사용하는 자습서는 [웹 응용 프로그램에서 Azure Key Vault 사용](key-vault-use-from-web-application.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-295">For a tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="7c9b2-296">프로그래밍 참조에 대 한 참조 [Azure 키 자격 증명 모음 개발자 가이드 hello](key-vault-developers-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-296">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

<span data-ttu-id="7c9b2-297">Azure Key Vault의 Azure PowerShell 1.0 cmdlet 목록은 [Azure Key Vault Cmdlet](/powershell/module/azurerm.keyvault/#key_vault)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-297">For a list of Azure PowerShell 1.0 cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>

<span data-ttu-id="7c9b2-298">키 회전 및 Azure 키 자격 증명 감사 로그에 대 한 자습서를 참조 하십시오. [끝 tooend와 toosetup 키 자격 증명 모음 키 회전 및 감사 어떻게](key-vault-key-rotation-log-monitoring.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c9b2-298">For a tutorial on key rotation and log auditing with Azure Key Vault, see [How toosetup Key Vault with end tooend key rotation and auditing](key-vault-key-rotation-log-monitoring.md).</span></span>
