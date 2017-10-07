---
title: "Azure PowerShell을 사용한 Azure Redis Cache aaaManage | Microsoft Docs"
description: "자세한 내용은 방법 tooperform Azure PowerShell을 사용 하 여 Azure Redis 캐시에 대 한 관리 작업입니다."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a><span data-ttu-id="0f16b-103">Azure PowerShell을 사용하여 Azure Redis Cache 관리</span><span class="sxs-lookup"><span data-stu-id="0f16b-103">Manage Azure Redis Cache with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0f16b-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f16b-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="0f16b-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0f16b-105">Azure CLI</span></span>](cache-manage-cli.md)
> 
> 

<span data-ttu-id="0f16b-106">이 항목에서는 방식과 tooperform 공통 작업 만들기와 같은, 업데이트 및 사용자의 Azure Redis Cache 인스턴스가 어떻게 확장 tooregenerate 선택 키와 방법을 캐시에 대 한 tooview 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-106">This topic shows you how tooperform common tasks such as create, update, and scale your Azure Redis Cache instances, how tooregenerate access keys, and how tooview information about your caches.</span></span> <span data-ttu-id="0f16b-107">Azure Redis Cache PowerShell cmdlet의 전체 목록은 [Azure Redis Cache cmdlet](https://msdn.microsoft.com/library/azure/mt634513.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f16b-107">For a complete list of Azure Redis Cache PowerShell cmdlets, see [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="0f16b-108">Hello 클래식 배포 모델에 대 한 자세한 내용은 참조 [Azure 리소스 관리자 및 클래식 배포: 배포 모델을 이해 하 고 리소스 상태를 hello](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-108">For more information about hello classic deployment model, see [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f16b-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0f16b-109">Prerequisites</span></span>
<span data-ttu-id="0f16b-110">Azure PowerShell을 이미 설치한 경우 Azure PowerShell 버전 1.0.0 이상이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-110">If you have already installed Azure PowerShell, you must have Azure PowerShell version 1.0.0 or later.</span></span> <span data-ttu-id="0f16b-111">Hello hello Azure PowerShell 명령 프롬프트에서이 명령을 사용 하 여 설치 된 Azure PowerShell 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-111">You can check hello version of Azure PowerShell that you have installed with this command at hello Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version


<span data-ttu-id="0f16b-112">첫째, tooAzure이이 명령 사용 하 여 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-112">First, you must log in tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="0f16b-113">Microsoft Azure 로그인 hello 대화 상자에서 Azure 계정 및 암호의 hello 전자 메일 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-113">Specify hello email address of your Azure account and its password in hello Microsoft Azure sign-in dialog.</span></span>

<span data-ttu-id="0f16b-114">다음으로, 여러 Azure 구독이 있는 경우 해야 tooset Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="0f16b-114">Next, if you have multiple Azure subscriptions, you need tooset your Azure subscription.</span></span> <span data-ttu-id="0f16b-115">현재 구독 목록이 toosee이이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-115">toosee a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="0f16b-116">toospecify hello 구독을 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-116">toospecify hello subscription, run hello following command.</span></span> <span data-ttu-id="0f16b-117">다음 예제는 hello, hello 구독 이름은 `ContosoSubscription`합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-117">In hello following example, hello subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

<span data-ttu-id="0f16b-118">Azure 리소스 관리자와 Windows PowerShell을 사용할 수 있습니다, 전에 hello 다음을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-118">Before you can use Windows PowerShell with Azure Resource Manager, you need hello following:</span></span>

* <span data-ttu-id="0f16b-119">Windows PowerShell, 버전 3.0 또는 4.0.</span><span class="sxs-lookup"><span data-stu-id="0f16b-119">Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="0f16b-120">toofind hello 버전의 Windows PowerShell, 유형:`$PSVersionTable` 의 hello 값을 확인 하 고 `PSVersion` 3.0 또는 4.0가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-120">toofind hello version of Windows PowerShell, type:`$PSVersionTable` and verify hello value of `PSVersion` is 3.0 or 4.0.</span></span> <span data-ttu-id="0f16b-121">호환 되는 버전 tooinstall 참조 [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) 또는 [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-121">tooinstall a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="0f16b-122">tooget은 hello Get-help cmdlet 사용 하 여가이 자습서에 나와 있는 모든 cmdlet에 대 한 도움말을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-122">tooget detailed help for any cmdlet you see in this tutorial, use hello Get-Help cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="0f16b-123">예를 들어 hello에 대 한 도움말을 tooget `New-AzureRmRedisCache` cmdlet, 유형:</span><span class="sxs-lookup"><span data-stu-id="0f16b-123">For example, tooget help for hello `New-AzureRmRedisCache` cmdlet, type:</span></span>

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a><span data-ttu-id="0f16b-124">어떻게 tooconnect tooother 클라우드</span><span class="sxs-lookup"><span data-stu-id="0f16b-124">How tooconnect tooother clouds</span></span>
<span data-ttu-id="0f16b-125">환경에는 기본 hello Azure로 `AzureCloud`이며 나타냅니다 hello 글로벌 Azure 클라우드 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="0f16b-125">By default hello Azure environment is `AzureCloud`, which represents hello global Azure cloud instance.</span></span> <span data-ttu-id="0f16b-126">tooconnect tooa 다른 인스턴스를 사용 하 여 hello `Add-AzureRmAccount` hello로 명령을 `-Environment` 또는-`EnvironmentName` hello 원하는 환경 또는 환경 이름이 명령줄 스위치입니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-126">tooconnect tooa different instance, use hello `Add-AzureRmAccount` command with hello `-Environment` or -`EnvironmentName` command line switch with hello desired environment or environment name.</span></span>

<span data-ttu-id="0f16b-127">toosee hello 목록이 hello를 실행 하는 사용 가능한 환경 `Get-AzureRmEnvironment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0f16b-127">toosee hello list of available environments, run hello `Get-AzureRmEnvironment` cmdlet.</span></span>

### <a name="tooconnect-toohello-azure-government-cloud"></a><span data-ttu-id="0f16b-128">tooconnect toohello Azure Government 클라우드</span><span class="sxs-lookup"><span data-stu-id="0f16b-128">tooconnect toohello Azure Government Cloud</span></span>
<span data-ttu-id="0f16b-129">tooconnect toohello Azure Government 클라우드 hello 다음 명령 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-129">tooconnect toohello Azure Government Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

<span data-ttu-id="0f16b-130">또는</span><span class="sxs-lookup"><span data-stu-id="0f16b-130">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

<span data-ttu-id="0f16b-131">hello Azure Government 클라우드에서에서 캐시 toocreate hello 다음 위치 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-131">toocreate a cache in hello Azure Government Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="0f16b-132">USGov 버지니아</span><span class="sxs-lookup"><span data-stu-id="0f16b-132">USGov Virginia</span></span>
* <span data-ttu-id="0f16b-133">미국 정부 아이오와</span><span class="sxs-lookup"><span data-stu-id="0f16b-133">USGov Iowa</span></span>

<span data-ttu-id="0f16b-134">Hello Azure Government 클라우드에 대 한 자세한 내용은 참조 하십시오. [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) 및 [Microsoft Azure Government 개발자 가이드](../azure-government-developer-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-134">For more information about hello Azure Government Cloud, see [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) and [Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>

### <a name="tooconnect-toohello-azure-china-cloud"></a><span data-ttu-id="0f16b-135">tooconnect toohello Azure 중국 클라우드</span><span class="sxs-lookup"><span data-stu-id="0f16b-135">tooconnect toohello Azure China Cloud</span></span>
<span data-ttu-id="0f16b-136">tooconnect toohello Azure 중국 클라우드 hello 다음 명령 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-136">tooconnect toohello Azure China Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

<span data-ttu-id="0f16b-137">또는</span><span class="sxs-lookup"><span data-stu-id="0f16b-137">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

<span data-ttu-id="0f16b-138">hello Azure 중국 클라우드에서에서 캐시 toocreate hello 다음 위치 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-138">toocreate a cache in hello Azure China Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="0f16b-139">중국 동부</span><span class="sxs-lookup"><span data-stu-id="0f16b-139">China East</span></span>
* <span data-ttu-id="0f16b-140">중국 북부</span><span class="sxs-lookup"><span data-stu-id="0f16b-140">China North</span></span>

<span data-ttu-id="0f16b-141">Hello Azure 중국 클라우드에 대 한 자세한 내용은 참조 하십시오. [중국의 21Vianet에서에서 운영 되는 Azure에 대 한 AzureChinaCloud](http://www.windowsazure.cn/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-141">For more information about hello Azure China Cloud, see [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span>

### <a name="tooconnect-toomicrosoft-azure-germany"></a><span data-ttu-id="0f16b-142">tooconnect tooMicrosoft Azure 독일</span><span class="sxs-lookup"><span data-stu-id="0f16b-142">tooconnect tooMicrosoft Azure Germany</span></span>
<span data-ttu-id="0f16b-143">tooconnect tooMicrosoft Azure 독일 hello 다음 명령 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-143">tooconnect tooMicrosoft Azure Germany, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


<span data-ttu-id="0f16b-144">또는</span><span class="sxs-lookup"><span data-stu-id="0f16b-144">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

<span data-ttu-id="0f16b-145">Microsoft Azure 독일의 캐시 toocreate hello 다음 위치 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-145">toocreate a cache in Microsoft Azure Germany, use one of hello following locations.</span></span>

* <span data-ttu-id="0f16b-146">독일 중부</span><span class="sxs-lookup"><span data-stu-id="0f16b-146">Germany Central</span></span>
* <span data-ttu-id="0f16b-147">독일 북동부</span><span class="sxs-lookup"><span data-stu-id="0f16b-147">Germany Northeast</span></span>

<span data-ttu-id="0f16b-148">Microsoft Azure Germany에 대한 자세한 내용은 [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f16b-148">For more information about Microsoft Azure Germany, see [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span></span>

### <a name="properties-used-for-azure-redis-cache-powershell"></a><span data-ttu-id="0f16b-149">Azure Redis Cache PowerShell에 사용되는 속성</span><span class="sxs-lookup"><span data-stu-id="0f16b-149">Properties used for Azure Redis Cache PowerShell</span></span>
<span data-ttu-id="0f16b-150">다음 표에 hello 속성과 자주 사용 되는 매개 변수를 만들고 Azure PowerShell을 사용 하 여 Azure Redis 캐시 인스턴스를 관리 하는 경우에 대 한 설명을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-150">hello following table contains properties and descriptions for commonly used parameters when creating and managing your Azure Redis Cache instances using Azure PowerShell.</span></span>

| <span data-ttu-id="0f16b-151">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0f16b-151">Parameter</span></span> | <span data-ttu-id="0f16b-152">설명</span><span class="sxs-lookup"><span data-stu-id="0f16b-152">Description</span></span> | <span data-ttu-id="0f16b-153">기본값</span><span class="sxs-lookup"><span data-stu-id="0f16b-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f16b-154">이름</span><span class="sxs-lookup"><span data-stu-id="0f16b-154">Name</span></span> |<span data-ttu-id="0f16b-155">Hello 캐시의 이름</span><span class="sxs-lookup"><span data-stu-id="0f16b-155">Name of hello cache</span></span> | |
| <span data-ttu-id="0f16b-156">위치</span><span class="sxs-lookup"><span data-stu-id="0f16b-156">Location</span></span> |<span data-ttu-id="0f16b-157">Hello 캐시의 위치</span><span class="sxs-lookup"><span data-stu-id="0f16b-157">Location of hello cache</span></span> | |
| <span data-ttu-id="0f16b-158">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="0f16b-158">ResourceGroupName</span></span> |<span data-ttu-id="0f16b-159">어떤 toocreate hello 캐시에 리소스 그룹 이름</span><span class="sxs-lookup"><span data-stu-id="0f16b-159">Resource group name in which toocreate hello cache</span></span> | |
| <span data-ttu-id="0f16b-160">크기</span><span class="sxs-lookup"><span data-stu-id="0f16b-160">Size</span></span> |<span data-ttu-id="0f16b-161">hello hello 캐시 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-161">hello size of hello cache.</span></span> <span data-ttu-id="0f16b-162">유효한 값: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span><span class="sxs-lookup"><span data-stu-id="0f16b-162">Valid values are: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span></span> |<span data-ttu-id="0f16b-163">1GB</span><span class="sxs-lookup"><span data-stu-id="0f16b-163">1GB</span></span> |
| <span data-ttu-id="0f16b-164">ShardCount</span><span class="sxs-lookup"><span data-stu-id="0f16b-164">ShardCount</span></span> |<span data-ttu-id="0f16b-165">클러스터링을 사용 프리미엄 캐시를 만들 때 분할 영역 toocreate hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-165">hello number of shards toocreate when creating a premium cache with clustering enabled.</span></span> <span data-ttu-id="0f16b-166">유효한 값: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span><span class="sxs-lookup"><span data-stu-id="0f16b-166">Valid values are: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></span> | |
| <span data-ttu-id="0f16b-167">SKU</span><span class="sxs-lookup"><span data-stu-id="0f16b-167">SKU</span></span> |<span data-ttu-id="0f16b-168">Hello hello 캐시의 SKU를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-168">Specifies hello SKU of hello cache.</span></span> <span data-ttu-id="0f16b-169">유효한 값: 기본, 표준, 프리미엄</span><span class="sxs-lookup"><span data-stu-id="0f16b-169">Valid values are: Basic, Standard, Premium</span></span> |<span data-ttu-id="0f16b-170">표준</span><span class="sxs-lookup"><span data-stu-id="0f16b-170">Standard</span></span> |
| <span data-ttu-id="0f16b-171">RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="0f16b-171">RedisConfiguration</span></span> |<span data-ttu-id="0f16b-172">Redis 구성 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-172">Specifies Redis configuration settings.</span></span> <span data-ttu-id="0f16b-173">각 설정에 대 한 자세한 내용은 hello 다음을 참조 하십시오. [RedisConfiguration 속성](#redisconfiguration-properties) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-173">For details on each setting, see hello following [RedisConfiguration properties](#redisconfiguration-properties) table.</span></span> | |
| <span data-ttu-id="0f16b-174">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="0f16b-174">EnableNonSslPort</span></span> |<span data-ttu-id="0f16b-175">Hello 비 SSL 포트를 사용 하는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-175">Indicates whether hello non-SSL port is enabled.</span></span> |<span data-ttu-id="0f16b-176">False</span><span class="sxs-lookup"><span data-stu-id="0f16b-176">False</span></span> |
| <span data-ttu-id="0f16b-177">MaxMemoryPolicy</span><span class="sxs-lookup"><span data-stu-id="0f16b-177">MaxMemoryPolicy</span></span> |<span data-ttu-id="0f16b-178">이 매개 변수는 더 이상 사용되지 않으며 대신 RedisConfiguration을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-178">This parameter has been deprecated - use RedisConfiguration instead.</span></span> | |
| <span data-ttu-id="0f16b-179">StaticIP</span><span class="sxs-lookup"><span data-stu-id="0f16b-179">StaticIP</span></span> |<span data-ttu-id="0f16b-180">VNET에서 캐시를 호스팅하는 경우 hello 캐시에 대 한 hello 서브넷에 고유한 IP 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-180">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="0f16b-181">을 지정 하지 않으면 하나는 선택 됩니다 hello 서브넷에서.</span><span class="sxs-lookup"><span data-stu-id="0f16b-181">If not provided, one is chosen for you from hello subnet.</span></span> | |
| <span data-ttu-id="0f16b-182">서브넷</span><span class="sxs-lookup"><span data-stu-id="0f16b-182">Subnet</span></span> |<span data-ttu-id="0f16b-183">VNET에서 캐시를 호스팅하는 경우 어떤 toodeploy hello 캐시 hello hello 서브넷 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-183">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="0f16b-184">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="0f16b-184">VirtualNetwork</span></span> |<span data-ttu-id="0f16b-185">hello 리소스 ID를 지정 하는 VNET에서 캐시를 호스팅하는 경우에 어떤 toodeploy hello 캐시에는 VNET hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-185">When hosting your cache in a VNET, specifies hello resource ID of hello VNET in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="0f16b-186">KeyType</span><span class="sxs-lookup"><span data-stu-id="0f16b-186">KeyType</span></span> |<span data-ttu-id="0f16b-187">액세스 키를 지정 합니다. 액세스 키를 갱신할 때 tooregenerate 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-187">Specifies which access key tooregenerate when renewing access keys.</span></span> <span data-ttu-id="0f16b-188">유효한 값: 주, 보조</span><span class="sxs-lookup"><span data-stu-id="0f16b-188">Valid values are: Primary, Secondary</span></span> | |

### <a name="redisconfiguration-properties"></a><span data-ttu-id="0f16b-189">RedisConfiguration 속성</span><span class="sxs-lookup"><span data-stu-id="0f16b-189">RedisConfiguration properties</span></span>
| <span data-ttu-id="0f16b-190">속성</span><span class="sxs-lookup"><span data-stu-id="0f16b-190">Property</span></span> | <span data-ttu-id="0f16b-191">설명</span><span class="sxs-lookup"><span data-stu-id="0f16b-191">Description</span></span> | <span data-ttu-id="0f16b-192">가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="0f16b-192">Pricing tiers</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f16b-193">rdb-backup-enabled</span><span class="sxs-lookup"><span data-stu-id="0f16b-193">rdb-backup-enabled</span></span> |<span data-ttu-id="0f16b-194">[Redis 데이터 지속성](cache-how-to-premium-persistence.md) 사용 여부</span><span class="sxs-lookup"><span data-stu-id="0f16b-194">Whether [Redis data persistence](cache-how-to-premium-persistence.md) is enabled</span></span> |<span data-ttu-id="0f16b-195">프리미엄 전용</span><span class="sxs-lookup"><span data-stu-id="0f16b-195">Premium only</span></span> |
| <span data-ttu-id="0f16b-196">rdb-storage-connection-string</span><span class="sxs-lookup"><span data-stu-id="0f16b-196">rdb-storage-connection-string</span></span> |<span data-ttu-id="0f16b-197">연결 문자열 toohello 저장소 계정에 대 한 hello [Redis 데이터 지 속성](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="0f16b-197">hello connection string toohello storage account for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="0f16b-198">프리미엄 전용</span><span class="sxs-lookup"><span data-stu-id="0f16b-198">Premium only</span></span> |
| <span data-ttu-id="0f16b-199">rdb-backup-frequency</span><span class="sxs-lookup"><span data-stu-id="0f16b-199">rdb-backup-frequency</span></span> |<span data-ttu-id="0f16b-200">백업 빈도 대 한 hello [Redis 데이터 지 속성](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="0f16b-200">hello backup frequency for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="0f16b-201">프리미엄 전용</span><span class="sxs-lookup"><span data-stu-id="0f16b-201">Premium only</span></span> |
| <span data-ttu-id="0f16b-202">maxmemory-reserved</span><span class="sxs-lookup"><span data-stu-id="0f16b-202">maxmemory-reserved</span></span> |<span data-ttu-id="0f16b-203">Hello 구성 [예약 되는 메모리](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) 캐시 되지 않은 프로세스에 대 한</span><span class="sxs-lookup"><span data-stu-id="0f16b-203">Configures hello [memory reserved](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for non-cache processes</span></span> |<span data-ttu-id="0f16b-204">표준 및 프리미엄</span><span class="sxs-lookup"><span data-stu-id="0f16b-204">Standard and Premium</span></span> |
| <span data-ttu-id="0f16b-205">maxmemory-policy</span><span class="sxs-lookup"><span data-stu-id="0f16b-205">maxmemory-policy</span></span> |<span data-ttu-id="0f16b-206">Hello 구성 [의 제거 정책](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) hello 캐시에 대 한</span><span class="sxs-lookup"><span data-stu-id="0f16b-206">Configures hello [eviction policy](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for hello cache</span></span> |<span data-ttu-id="0f16b-207">모든 가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="0f16b-207">All pricing tiers</span></span> |
| <span data-ttu-id="0f16b-208">notify-keyspace-events</span><span class="sxs-lookup"><span data-stu-id="0f16b-208">notify-keyspace-events</span></span> |<span data-ttu-id="0f16b-209">[Keyspace 알림](cache-configure.md#keyspace-notifications-advanced-settings)</span><span class="sxs-lookup"><span data-stu-id="0f16b-209">Configures [keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings)</span></span> |<span data-ttu-id="0f16b-210">표준 및 프리미엄</span><span class="sxs-lookup"><span data-stu-id="0f16b-210">Standard and Premium</span></span> |
| <span data-ttu-id="0f16b-211">hash-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="0f16b-211">hash-max-ziplist-entries</span></span> |<span data-ttu-id="0f16b-212">작은 집계 데이터 형식에 대한 [메모리 최적화](http://redis.io/topics/memory-optimization) 구성</span><span class="sxs-lookup"><span data-stu-id="0f16b-212">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="0f16b-213">표준 및 프리미엄</span><span class="sxs-lookup"><span data-stu-id="0f16b-213">Standard and Premium</span></span> |
| <span data-ttu-id="0f16b-214">hash-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="0f16b-214">hash-max-ziplist-value</span></span> |<span data-ttu-id="0f16b-215">작은 집계 데이터 형식에 대한 [메모리 최적화](http://redis.io/topics/memory-optimization) 구성</span><span class="sxs-lookup"><span data-stu-id="0f16b-215">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="0f16b-216">표준 및 프리미엄</span><span class="sxs-lookup"><span data-stu-id="0f16b-216">Standard and Premium</span></span> |
| <span data-ttu-id="0f16b-217">set-max-intset-entries</span><span class="sxs-lookup"><span data-stu-id="0f16b-217">set-max-intset-entries</span></span> |<span data-ttu-id="0f16b-218">작은 집계 데이터 형식에 대한 [메모리 최적화](http://redis.io/topics/memory-optimization) 구성</span><span class="sxs-lookup"><span data-stu-id="0f16b-218">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="0f16b-219">표준 및 프리미엄</span><span class="sxs-lookup"><span data-stu-id="0f16b-219">Standard and Premium</span></span> |
| <span data-ttu-id="0f16b-220">zset-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="0f16b-220">zset-max-ziplist-entries</span></span> |<span data-ttu-id="0f16b-221">작은 집계 데이터 형식에 대한 [메모리 최적화](http://redis.io/topics/memory-optimization) 구성</span><span class="sxs-lookup"><span data-stu-id="0f16b-221">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="0f16b-222">표준 및 프리미엄</span><span class="sxs-lookup"><span data-stu-id="0f16b-222">Standard and Premium</span></span> |
| <span data-ttu-id="0f16b-223">zset-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="0f16b-223">zset-max-ziplist-value</span></span> |<span data-ttu-id="0f16b-224">작은 집계 데이터 형식에 대한 [메모리 최적화](http://redis.io/topics/memory-optimization) 구성</span><span class="sxs-lookup"><span data-stu-id="0f16b-224">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="0f16b-225">표준 및 프리미엄</span><span class="sxs-lookup"><span data-stu-id="0f16b-225">Standard and Premium</span></span> |
| <span data-ttu-id="0f16b-226">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="0f16b-226">databases</span></span> |<span data-ttu-id="0f16b-227">Hello 데이터베이스 수를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-227">Configures hello number of databases.</span></span> <span data-ttu-id="0f16b-228">이 속성은 캐시 만들기에서만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-228">This property can be configured only at cache creation.</span></span> |<span data-ttu-id="0f16b-229">표준 및 프리미엄</span><span class="sxs-lookup"><span data-stu-id="0f16b-229">Standard and Premium</span></span> |

## <a name="toocreate-a-redis-cache"></a><span data-ttu-id="0f16b-230">toocreate Redis 캐시</span><span class="sxs-lookup"><span data-stu-id="0f16b-230">toocreate a Redis Cache</span></span>
<span data-ttu-id="0f16b-231">Hello를 사용 하 여 새 Azure Redis Cache 인스턴스가 만들어지지 [새로 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0f16b-231">New Azure Redis Cache instances are created using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f16b-232">hello 처음 hello Azure 포털을 사용 하 여 구독에서 Redis cache를 만들 때 hello 포털 등록 hello `Microsoft.Cache` 해당 구독에 대 한 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-232">hello first time you create a Redis cache in a subscription using hello Azure portal, hello portal registers hello `Microsoft.Cache` namespace for that subscription.</span></span> <span data-ttu-id="0f16b-233">사용 하려는 경우 toocreate hello PowerShell을 사용 하 여 구독에서 캐시를 먼저 Redis, 다음 명령을; hello를 사용 하 여 해당 네임 스페이스를 먼저 등록 해야 합니다. 그렇지 않으면 cmdlet과 같은 `New-AzureRmRedisCache` 및 `Get-AzureRmRedisCache` 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-233">If you attempt toocreate hello first Redis cache in a subscription using PowerShell, you must first register that namespace using hello following command; otherwise cmdlets such as `New-AzureRmRedisCache` and `Get-AzureRmRedisCache` fail.</span></span>
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

<span data-ttu-id="0f16b-234">사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `New-AzureRmRedisCache`실행 hello 다음 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-234">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="0f16b-235">toocreate hello 다음 명령을 실행 합니다. 기본 매개 변수가 있는 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-235">toocreate a cache with default parameters, run hello following command.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

<span data-ttu-id="0f16b-236">`ResourceGroupName``Name`, 및 `Location` 필수 매개 변수가 있지만 hello 나머지는 선택 사항이 며 기본값이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-236">`ResourceGroupName`, `Name`, and `Location` are required parameters, but hello rest are optional and have default values.</span></span> <span data-ttu-id="0f16b-237">Hello 지정 된 이름, 위치 및 크기와 사용 하지 않도록 설정 하는 hello 비 SSL 포트에에서 1GB 있는 리소스 그룹으로 표준 SKU Azure Redis 캐시 인스턴스를 만듭니다 hello 이전 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-237">Running hello previous command creates a Standard SKU Azure Redis Cache instance with hello specified name, location, and resource group, that is 1 GB in size with hello non-SSL port disabled.</span></span>

<span data-ttu-id="0f16b-238">P1 (6GB-60GB), P2 (13 GB-130 기가바이트)의 크기를 지정 하는 프리미엄 캐시 toocreate P3 (26GB-260 기가바이트) 또는 P4 (53GB 530 10GB).</span><span class="sxs-lookup"><span data-stu-id="0f16b-238">toocreate a premium cache, specify a size of P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), or P4 (53 GB - 530 GB).</span></span> <span data-ttu-id="0f16b-239">hello를 사용 하 여 분할 영역 수를 지정 하는 클러스터링, tooenable `ShardCount` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-239">tooenable clustering, specify a shard count using hello `ShardCount` parameter.</span></span> <span data-ttu-id="0f16b-240">hello 다음 만드는 예제 P1 프리미엄 캐시 3 분할 된 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-240">hello following example creates a P1 premium cache with 3 shards.</span></span> <span data-ttu-id="0f16b-241">P1 프리미엄 캐시의 크기를 6GB는 하며 세 가지 분할 영역 hello 전체 크기를 지정 했기 때문 18 GB (3 x 6 GB)</span><span class="sxs-lookup"><span data-stu-id="0f16b-241">A P1 premium cache is 6 GB in size, and since we specified three shards hello total size is 18 GB (3 x 6 GB).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

<span data-ttu-id="0f16b-242">hello에 대 한 toospecify 값 `RedisConfiguration` 매개 변수를 내부 hello 값 묶습니다 `{}` 으로 키/값 쌍 같은 `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-242">toospecify values for hello `RedisConfiguration` parameter, enclose hello values inside `{}` as key/value pairs like `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span></span> <span data-ttu-id="0f16b-243">hello 다음 예제에서는 캐시를 만든 표준 1GB와 `allkeys-random` 구성 된 최대 메모리 정책 및 키 스페이스 알림 `KEA`합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-243">hello following example creates a standard 1 GB cache with `allkeys-random` maxmemory policy and keyspace notifications configured with `KEA`.</span></span> <span data-ttu-id="0f16b-244">자세한 내용은 [Keyspace 알림(고급 설정)](cache-configure.md#keyspace-notifications-advanced-settings) 및 [메모리 정책](cache-configure.md#memory-policies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f16b-244">For more information, see [Keyspace notifications (advanced settings)](cache-configure.md#keyspace-notifications-advanced-settings) and [Memory policies](cache-configure.md#memory-policies).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a><span data-ttu-id="0f16b-245">캐시 만들기 중에 설정 tooconfigure hello 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="0f16b-245">tooconfigure hello databases setting during cache creation</span></span>
<span data-ttu-id="0f16b-246">hello `databases` 캐시 만들기 중에 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-246">hello `databases` setting can be configured only during cache creation.</span></span> <span data-ttu-id="0f16b-247">hello 다음 예제에서는 프리미엄 P3 hello를 사용 하 여 48 데이터베이스와 함께 (26GB) 캐시 [새로 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0f16b-247">hello following example creates a premium P3 (26 GB) cache with 48 databases using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

<span data-ttu-id="0f16b-248">Hello에 대 한 자세한 내용은 `databases` 속성 참조 [기본 Azure Redis Cache 서버 구성](cache-configure.md#default-redis-server-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-248">For more information on hello `databases` property, see [Default Azure Redis Cache server configuration](cache-configure.md#default-redis-server-configuration).</span></span> <span data-ttu-id="0f16b-249">Hello를 사용 하 여 캐시를 만드는 방법에 대 한 자세한 내용은 [새로 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet hello 이전 참조 [toocreate Redis Cache](#to-create-a-redis-cache) 섹션.</span><span class="sxs-lookup"><span data-stu-id="0f16b-249">For more information on creating a cache using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, see hello previous [toocreate a Redis Cache](#to-create-a-redis-cache) section.</span></span>

## <a name="tooupdate-a-redis-cache"></a><span data-ttu-id="0f16b-250">tooupdate Redis 캐시</span><span class="sxs-lookup"><span data-stu-id="0f16b-250">tooupdate a Redis cache</span></span>
<span data-ttu-id="0f16b-251">Azure Redis 캐시 인스턴스가 hello를 사용 하 여 업데이트 됩니다 [집합 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0f16b-251">Azure Redis Cache instances are updated using hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span></span>

<span data-ttu-id="0f16b-252">사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `Set-AzureRmRedisCache`실행 hello 다음 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-252">toosee a list of available parameters and their descriptions for `Set-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="0f16b-253">hello `Set-AzureRmRedisCache` cmdlet과 같은 사용된 tooupdate 속성 수 `Size`, `Sku`, `EnableNonSslPort`, 및 hello `RedisConfiguration` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-253">hello `Set-AzureRmRedisCache` cmdlet can be used tooupdate properties such as `Size`, `Sku`, `EnableNonSslPort`, and hello `RedisConfiguration` values.</span></span> 

<span data-ttu-id="0f16b-254">hello 업데이트 hello에 대 한 hello Redis 캐시 maxmemory 정책 다음 명령은 이름이 myCache입니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-254">hello following command updates hello maxmemory-policy for hello Redis Cache named myCache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a><span data-ttu-id="0f16b-255">tooscale Redis 캐시</span><span class="sxs-lookup"><span data-stu-id="0f16b-255">tooscale a Redis cache</span></span>
<span data-ttu-id="0f16b-256">`Set-AzureRmRedisCache`사용 되는 tooscale 때 hello Azure Redis 캐시 인스턴스 수 `Size`, `Sku`, 또는 `ShardCount` 속성이 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-256">`Set-AzureRmRedisCache` can be used tooscale an Azure Redis cache instance when hello `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> 

> [!NOTE]
> <span data-ttu-id="0f16b-257">PowerShell을 사용 하 여 캐시 크기 조정 주체 toohello 동일한 제한을 이며 캐시에서 크기 조정 지침 hello Azure 포털.</span><span class="sxs-lookup"><span data-stu-id="0f16b-257">Scaling a cache using PowerShell is subject toohello same limits and guidelines as scaling a cache from hello Azure portal.</span></span> <span data-ttu-id="0f16b-258">Tooa 다른 제한 사항에 따라 hello로 가격 책정 계층을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-258">You can scale tooa different pricing tier with hello following restrictions.</span></span>
> 
> * <span data-ttu-id="0f16b-259">더 높은 가격 책정 계층 tooa 더 낮은 가격 책정 계층에서에서 확장할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-259">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
> * <span data-ttu-id="0f16b-260">업그레이드할 수 없는 **프리미엄** tooa 아래로 캐시 **표준** 또는 **기본** 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-260">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
> * <span data-ttu-id="0f16b-261">업그레이드할 수 없는 **표준** tooa 아래로 캐시 **기본** 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-261">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
> * <span data-ttu-id="0f16b-262">확장할 수는 **기본** tooa 캐시 **표준** 캐시 있지만 hello hello 크기를 변경할 수 없습니다 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-262">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="0f16b-263">크기를 다르게 해야 할 경우에 크기 조정 작업의 후속 toohello 원하는 크기를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-263">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
> * <span data-ttu-id="0f16b-264">업그레이드할 수 없는 **기본** 캐시 직접 tooa **프리미엄** 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-264">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="0f16b-265">확장 해야 **기본** 너무**표준** 한 크기 조정 작업에서 **표준** 너무**프리미엄** 후속 배율 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-265">You must scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
> * <span data-ttu-id="0f16b-266">toohello 아래로 더 큰 크기를 확장할 수 없으며 **C0 (250MB)** 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-266">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>
> 
> <span data-ttu-id="0f16b-267">자세한 내용은 참조 [어떻게 tooScale Azure Redis 캐시](cache-how-to-scale.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-267">For more information, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>
> 
> 

<span data-ttu-id="0f16b-268">hello 다음 예제에서는 어떻게 tooscale 캐시 라는 `myCache` tooa 2.5 g B 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-268">hello following example shows how tooscale a cache named `myCache` tooa 2.5 GB cache.</span></span> <span data-ttu-id="0f16b-269">이 명령은 기본 또는 표준 캐시 둘 다에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-269">Note that this command works for both a Basic or a Standard cache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="0f16b-270">이 명령이 실행 된 후에 hello 캐시의 hello 상태가 반환 됩니다 (유사한 toocalling `Get-AzureRmRedisCache`).</span><span class="sxs-lookup"><span data-stu-id="0f16b-270">After this command is issued, hello status of hello cache is returned (similar toocalling `Get-AzureRmRedisCache`).</span></span> <span data-ttu-id="0f16b-271">해당 hello 참고 `ProvisioningState` 은 `Scaling`합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-271">Note that hello `ProvisioningState` is `Scaling`.</span></span>

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

<span data-ttu-id="0f16b-272">Hello 크기 조정 작업이 완료 되 면 hello `ProvisioningState` 쪽 변경`Succeeded`합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-272">When hello scaling operation is complete, hello `ProvisioningState` changes too`Succeeded`.</span></span> <span data-ttu-id="0f16b-273">Toomake 후속 있는 크기 조정 작업에서 기본 tooStandard 변경 등 다음 hello 크기를 변경 해야 할 경우 hello 이전 작업이 완료 되거나 오류 유사한 toohello 다음 수신 될 때까지 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-273">If you need toomake a subsequent scaling operation, such as changing from Basic tooStandard and then changing hello size, you must wait until hello previous operation is complete or you receive an error similar toohello following.</span></span>

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a><span data-ttu-id="0f16b-274">Redis 캐시에 대 한 tooget 정보</span><span class="sxs-lookup"><span data-stu-id="0f16b-274">tooget information about a Redis cache</span></span>
<span data-ttu-id="0f16b-275">Hello를 사용 하 여 캐시에 대 한 정보를 검색할 수 [Get AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0f16b-275">You can retrieve information about a cache using hello [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span></span>

<span data-ttu-id="0f16b-276">사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `Get-AzureRmRedisCache`실행 hello 다음 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-276">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="0f16b-277">hello 현재 구독에서 모든 캐시에 대 한 정보 tooreturn 실행 `Get-AzureRmRedisCache` 매개 변수 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-277">tooreturn information about all caches in hello current subscription, run `Get-AzureRmRedisCache` without any parameters.</span></span>

    Get-AzureRmRedisCache

<span data-ttu-id="0f16b-278">특정 리소스 그룹의 모든 캐시에 대 한 정보 tooreturn 실행 `Get-AzureRmRedisCache` hello로 `ResourceGroupName` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-278">tooreturn information about all caches in a specific resource group, run `Get-AzureRmRedisCache` with hello `ResourceGroupName` parameter.</span></span>

    Get-AzureRmRedisCache -ResourceGroupName myGroup

<span data-ttu-id="0f16b-279">특정 캐시에 대 한 정보 tooreturn 실행 `Get-AzureRmRedisCache` hello로 `Name` hello 캐시 및 hello의 hello 이름을 포함 하는 매개 변수 `ResourceGroupName` 해당 캐시를 포함 하는 hello 리소스 그룹과 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-279">tooreturn information about a specific cache, run `Get-AzureRmRedisCache` with hello `Name` parameter containing hello name of hello cache, and hello `ResourceGroupName` parameter with hello resource group containing that cache.</span></span>

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a><span data-ttu-id="0f16b-280">Redis cache에 대해 tooretrieve hello 선택 키</span><span class="sxs-lookup"><span data-stu-id="0f16b-280">tooretrieve hello access keys for a Redis cache</span></span>
<span data-ttu-id="0f16b-281">캐시에 대 한 hello 선택 키 tooretrieve hello를 사용할 수 있습니다 [Get AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0f16b-281">tooretrieve hello access keys for your cache, you can use hello [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span></span>

<span data-ttu-id="0f16b-282">사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `Get-AzureRmRedisCacheKey`실행 hello 다음 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-282">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="0f16b-283">캐시에 호출 hello에 대 한 키 tooretrieve hello `Get-AzureRmRedisCacheKey` cmdlet 및 캐시의 hello 이름에는 통과 hello hello 캐시를 포함 하는 hello 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-283">tooretrieve hello keys for your cache, call hello `Get-AzureRmRedisCacheKey` cmdlet and pass in hello name of your cache hello name of hello resource group that contains hello cache.</span></span>

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a><span data-ttu-id="0f16b-284">Redis 캐시에 대 한 tooregenerate 선택 키</span><span class="sxs-lookup"><span data-stu-id="0f16b-284">tooregenerate access keys for your Redis cache</span></span>
<span data-ttu-id="0f16b-285">캐시에 대 한 hello 선택 키 tooregenerate hello를 사용할 수 있습니다 [새로 AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0f16b-285">tooregenerate hello access keys for your cache, you can use hello [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span></span>

<span data-ttu-id="0f16b-286">사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `New-AzureRmRedisCacheKey`실행 hello 다음 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-286">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="0f16b-287">캐시에서 호출 hello tooregenerate hello 기본 또는 보조 키 `New-AzureRmRedisCacheKey` cmdlet 및 hello 전달 리소스 그룹 이름을 지정 하 고 지정 `Primary` 또는 `Secondary` hello에 대 한 `KeyType` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-287">tooregenerate hello primary or secondary key for your cache, call hello `New-AzureRmRedisCacheKey` cmdlet and pass in hello name, resource group, and specify either `Primary` or `Secondary` for hello `KeyType` parameter.</span></span> <span data-ttu-id="0f16b-288">다음 예제는 hello에 캐시에 대 한 hello 보조 액세스 키 다시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-288">In hello following example, hello secondary access key for a cache is regenerated.</span></span>

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a><span data-ttu-id="0f16b-289">toodelete Redis 캐시</span><span class="sxs-lookup"><span data-stu-id="0f16b-289">toodelete a Redis cache</span></span>
<span data-ttu-id="0f16b-290">Redis cache toodelete hello를 사용 하 여 [제거 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0f16b-290">toodelete a Redis cache, use hello [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span></span>

<span data-ttu-id="0f16b-291">사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `Remove-AzureRmRedisCache`실행 hello 다음 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-291">toosee a list of available parameters and their descriptions for `Remove-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="0f16b-292">다음 예제는 hello에서 명명 된 캐시 hello `myCache` 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-292">In hello following example, hello cache named `myCache` is removed.</span></span>

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a><span data-ttu-id="0f16b-293">tooimport Redis 캐시</span><span class="sxs-lookup"><span data-stu-id="0f16b-293">tooimport a Redis cache</span></span>
<span data-ttu-id="0f16b-294">Hello를 사용 하 여 Azure Redis Cache 인스턴스로 데이터를 가져올 수 있습니다 `Import-AzureRmRedisCache` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0f16b-294">You can import data into an Azure Redis Cache instance using hello `Import-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f16b-295">가져오기/내보내기는 [프리미엄 계층](cache-premium-tier-intro.md) 캐시에만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-295">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="0f16b-296">가져오기/내보내기에 대한 자세한 내용은 [Azure Redis Cache에서 데이터 가져오기 및 내보내기](cache-how-to-import-export-data.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f16b-296">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="0f16b-297">사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `Import-AzureRmRedisCache`실행 hello 다음 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-297">toosee a list of available parameters and their descriptions for `Import-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="0f16b-298">hello 다음 명령에서에서 데이터를 가져옵니다 Azure Redis 캐시로 hello SAS uri로 지정 된 hello blob입니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-298">hello following command imports data from hello blob specified by hello SAS uri into Azure Redis Cache.</span></span>

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a><span data-ttu-id="0f16b-299">tooexport Redis 캐시</span><span class="sxs-lookup"><span data-stu-id="0f16b-299">tooexport a Redis cache</span></span>
<span data-ttu-id="0f16b-300">Azure Redis Cache 인스턴스에서 hello를 사용 하 여 데이터를 내보낼 수 `Export-AzureRmRedisCache` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0f16b-300">You can export data from an Azure Redis Cache instance using hello `Export-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f16b-301">가져오기/내보내기는 [프리미엄 계층](cache-premium-tier-intro.md) 캐시에만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-301">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="0f16b-302">가져오기/내보내기에 대한 자세한 내용은 [Azure Redis Cache에서 데이터 가져오기 및 내보내기](cache-how-to-import-export-data.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f16b-302">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="0f16b-303">사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `Export-AzureRmRedisCache`실행 hello 다음 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-303">toosee a list of available parameters and their descriptions for `Export-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="0f16b-304">hello 다음 명령은 데이터에서에서 내보냅니다 hello SAS uri로 지정 된 hello 컨테이너로 Azure Redis Cache 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="0f16b-304">hello following command exports data from an Azure Redis Cache instance into hello container specified by hello SAS uri.</span></span>

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a><span data-ttu-id="0f16b-305">tooreboot Redis 캐시</span><span class="sxs-lookup"><span data-stu-id="0f16b-305">tooreboot a Redis cache</span></span>
<span data-ttu-id="0f16b-306">Azure Redis 캐시 인스턴스의 hello를 사용 하 여 다시 부팅할 수 `Reset-AzureRmRedisCache` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0f16b-306">You can reboot your Azure Redis Cache instance using hello `Reset-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f16b-307">재부팅은 [프리미엄 계층](cache-premium-tier-intro.md) 캐시에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-307">Reboot is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="0f16b-308">캐시를 재부팅하는 방법에 대한 자세한 내용은 [캐시 관리 - 재부팅](cache-administration.md#reboot)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f16b-308">For more information about rebooting your cache, see [Cache administration - reboot](cache-administration.md#reboot).</span></span>
> 
> 

<span data-ttu-id="0f16b-309">사용 가능한 매개 변수 목록과 해당 설명을 보려면에 대 한 toosee `Reset-AzureRmRedisCache`실행 hello 다음 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-309">toosee a list of available parameters and their descriptions for `Reset-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="0f16b-310">hello 다음 명령을 다시 부팅 지정 hello의 두 노드 모두 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-310">hello following command reboots both nodes of hello specified cache.</span></span>

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a><span data-ttu-id="0f16b-311">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f16b-311">Next steps</span></span>
<span data-ttu-id="0f16b-312">Azure를 통해 Windows PowerShell 사용에 대 한 더 toolearn hello 다음 리소스를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0f16b-312">toolearn more about using Windows PowerShell with Azure, see hello following resources:</span></span>

* [<span data-ttu-id="0f16b-313">MSDN에 있는 Azure Redis Cache cmdlet 설명서</span><span class="sxs-lookup"><span data-stu-id="0f16b-313">Azure Redis Cache cmdlet documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* <span data-ttu-id="0f16b-314">[Azure 리소스 관리자 Cmdlet](http://go.microsoft.com/fwlink/?LinkID=394765): hello Azure 리소스 관리자 모듈의 toouse hello cmdlet에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): Learn toouse hello cmdlets in hello Azure Resource Manager module.</span></span>
* <span data-ttu-id="0f16b-315">[Toomanage Azure 리소스 그룹 리소스를 사용 하 여](../azure-resource-manager/resource-group-template-deploy-portal.md): 자세한 방법을 toocreate hello Azure 포털에서에서 리소스 그룹 및 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-315">[Using Resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md): Learn how toocreate and manage resource groups in hello Azure portal.</span></span>
* <span data-ttu-id="0f16b-316">[Azure 블로그](http://blogs.msdn.com/windowsazure): Azure의 새로운 기능에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-316">[Azure blog](http://blogs.msdn.com/windowsazure): Learn about new features in Azure.</span></span>
* <span data-ttu-id="0f16b-317">[Windows PowerShell 블로그](http://blogs.msdn.com/powershell): Windows PowerShell의 새로운 기능에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-317">[Windows PowerShell blog](http://blogs.msdn.com/powershell): Learn about new features in Windows PowerShell.</span></span>
* <span data-ttu-id="0f16b-318">["Hey, Scripting Guy!" 블로그](http://blogs.technet.com/b/heyscriptingguy/): hello Windows PowerShell 커뮤니티에서에서 실제 팁과 요령을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0f16b-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Get real-world tips and tricks from hello Windows PowerShell community.</span></span>

