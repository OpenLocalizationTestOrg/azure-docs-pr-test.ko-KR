---
title: "Azure PowerShell을 사용하여 Azure Redis Cache 관리 | Microsoft Docs"
description: "Azure PowerShell을 사용하여 Azure Redis Cache에 대한 관리 작업을 수행하는 방법을 알아봅니다."
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
ms.openlocfilehash: 0a5c95eab3fd01f611fc049e80c5c506857e0b81
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a><span data-ttu-id="8e79e-103">Azure PowerShell을 사용하여 Azure Redis Cache 관리</span><span class="sxs-lookup"><span data-stu-id="8e79e-103">Manage Azure Redis Cache with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8e79e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e79e-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="8e79e-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8e79e-105">Azure CLI</span></span>](cache-manage-cli.md)
> 
> 

<span data-ttu-id="8e79e-106">이 항목에서는 Azure Redis Cache 인스턴스 만들기, 업데이트 및 크기 조정과 같은 일반적인 작업을 수행하고 액세스 키를 다시 생성하며 캐시에 대한 정보를 보는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-106">This topic shows you how to perform common tasks such as create, update, and scale your Azure Redis Cache instances, how to regenerate access keys, and how to view information about your caches.</span></span> <span data-ttu-id="8e79e-107">Azure Redis Cache PowerShell cmdlet의 전체 목록은 [Azure Redis Cache cmdlet](https://msdn.microsoft.com/library/azure/mt634513.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e79e-107">For a complete list of Azure Redis Cache PowerShell cmdlets, see [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="8e79e-108">두 배포 모델에 대한 자세한 내용은 [Azure Resource Manager 및 클래식 배포: 배포 모델 및 리소스 상태 이해](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e79e-108">For more information about the classic deployment model, see [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e79e-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8e79e-109">Prerequisites</span></span>
<span data-ttu-id="8e79e-110">Azure PowerShell을 이미 설치한 경우 Azure PowerShell 버전 1.0.0 이상이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-110">If you have already installed Azure PowerShell, you must have Azure PowerShell version 1.0.0 or later.</span></span> <span data-ttu-id="8e79e-111">Azure PowerShell 명령 프롬프트에서 다음 명령을 사용하여 설치한 Azure PowerShell의 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-111">You can check the version of Azure PowerShell that you have installed with this command at the Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version


<span data-ttu-id="8e79e-112">먼저 다음 명령을 사용하여 Azure에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-112">First, you must log in to Azure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="8e79e-113">Microsoft Azure 로그인 대화 상자에서 Azure 계정의 전자 메일 주소 및 해당 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-113">Specify the email address of your Azure account and its password in the Microsoft Azure sign-in dialog.</span></span>

<span data-ttu-id="8e79e-114">다음으로, 여러 Azure 구독이 있는 경우 Azure 구독을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-114">Next, if you have multiple Azure subscriptions, you need to set your Azure subscription.</span></span> <span data-ttu-id="8e79e-115">현재 구독 목록을 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-115">To see a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="8e79e-116">구독을 지정하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-116">To specify the subscription, run the following command.</span></span> <span data-ttu-id="8e79e-117">다음 예제에서 구독 이름은 `ContosoSubscription`입니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-117">In the following example, the subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

<span data-ttu-id="8e79e-118">Azure 리소스 관리자에서 Windows PowerShell을 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-118">Before you can use Windows PowerShell with Azure Resource Manager, you need the following:</span></span>

* <span data-ttu-id="8e79e-119">Windows PowerShell, 버전 3.0 또는 4.0.</span><span class="sxs-lookup"><span data-stu-id="8e79e-119">Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="8e79e-120">Windows PowerShell 버전을 확인하려면 `$PSVersionTable`을 입력하고 `PSVersion` 값이 3.0 또는 4.0인지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-120">To find the version of Windows PowerShell, type:`$PSVersionTable` and verify the value of `PSVersion` is 3.0 or 4.0.</span></span> <span data-ttu-id="8e79e-121">호환 버전을 설치하려면 [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) 또는 [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e79e-121">To install a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="8e79e-122">이 자습서에 나오는 cmdlet에 대한 자세한 도움말을 보려면 Get-Help cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-122">To get detailed help for any cmdlet you see in this tutorial, use the Get-Help cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="8e79e-123">예를 들어 `New-AzureRmRedisCache` cmdlet에 대한 도움말을 보려면 다음과 같이 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-123">For example, to get help for the `New-AzureRmRedisCache` cmdlet, type:</span></span>

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-to-connect-to-other-clouds"></a><span data-ttu-id="8e79e-124">다른 클라우드에 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="8e79e-124">How to connect to other clouds</span></span>
<span data-ttu-id="8e79e-125">기본적으로 Azure 환경은 글로벌 Azure 클라우드 인스턴스를 나타내는 `AzureCloud`입니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-125">By default the Azure environment is `AzureCloud`, which represents the global Azure cloud instance.</span></span> <span data-ttu-id="8e79e-126">다른 인스턴스에 연결하려면 원하는 환경 또는 환경 이름을 사용하여 `-Environment` 또는 -`EnvironmentName` 명령줄 스위치와 함께 `Add-AzureRmAccount` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-126">To connect to a different instance, use the `Add-AzureRmAccount` command with the `-Environment` or -`EnvironmentName` command line switch with the desired environment or environment name.</span></span>

<span data-ttu-id="8e79e-127">사용 가능한 환경 목록을 보려면 `Get-AzureRmEnvironment` cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-127">To see the list of available environments, run the `Get-AzureRmEnvironment` cmdlet.</span></span>

### <a name="to-connect-to-the-azure-government-cloud"></a><span data-ttu-id="8e79e-128">Azure Government 클라우드를 연결하려면</span><span class="sxs-lookup"><span data-stu-id="8e79e-128">To connect to the Azure Government Cloud</span></span>
<span data-ttu-id="8e79e-129">Azure Government 클라우드를 연결하려면 다음 명령 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-129">To connect to the Azure Government Cloud, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

<span data-ttu-id="8e79e-130">또는</span><span class="sxs-lookup"><span data-stu-id="8e79e-130">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

<span data-ttu-id="8e79e-131">Azure Government 클라우드 내에 캐시를 만들려면 다음 위치 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-131">To create a cache in the Azure Government Cloud, use one of the following locations.</span></span>

* <span data-ttu-id="8e79e-132">USGov 버지니아</span><span class="sxs-lookup"><span data-stu-id="8e79e-132">USGov Virginia</span></span>
* <span data-ttu-id="8e79e-133">미국 정부 아이오와</span><span class="sxs-lookup"><span data-stu-id="8e79e-133">USGov Iowa</span></span>

<span data-ttu-id="8e79e-134">Azure Government 클라우드에 대한 자세한 내용은 [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) 및 [Microsoft Azure Government 개발자 가이드](../azure-government-developer-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e79e-134">For more information about the Azure Government Cloud, see [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) and [Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>

### <a name="to-connect-to-the-azure-china-cloud"></a><span data-ttu-id="8e79e-135">Azure 중국 클라우드에 연결하려면</span><span class="sxs-lookup"><span data-stu-id="8e79e-135">To connect to the Azure China Cloud</span></span>
<span data-ttu-id="8e79e-136">Azure 중국 클라우드에 연결하려면 다음 명령 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-136">To connect to the Azure China Cloud, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

<span data-ttu-id="8e79e-137">또는</span><span class="sxs-lookup"><span data-stu-id="8e79e-137">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

<span data-ttu-id="8e79e-138">Azure 중국 클라우드에서 캐시를 만들려면 다음 위치 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-138">To create a cache in the Azure China Cloud, use one of the following locations.</span></span>

* <span data-ttu-id="8e79e-139">중국 동부</span><span class="sxs-lookup"><span data-stu-id="8e79e-139">China East</span></span>
* <span data-ttu-id="8e79e-140">중국 북부</span><span class="sxs-lookup"><span data-stu-id="8e79e-140">China North</span></span>

<span data-ttu-id="8e79e-141">Azure 중국 클라우드에 대한 자세한 내용은 [중국 21Vianet에서 운영하는 Azure용 AzureChinaCloud](http://www.windowsazure.cn/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e79e-141">For more information about the Azure China Cloud, see [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span>

### <a name="to-connect-to-microsoft-azure-germany"></a><span data-ttu-id="8e79e-142">Microsoft Azure Germany에 연결하려면</span><span class="sxs-lookup"><span data-stu-id="8e79e-142">To connect to Microsoft Azure Germany</span></span>
<span data-ttu-id="8e79e-143">Microsoft Azure Germany에 연결하려면 다음 명령 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-143">To connect to Microsoft Azure Germany, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


<span data-ttu-id="8e79e-144">또는</span><span class="sxs-lookup"><span data-stu-id="8e79e-144">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

<span data-ttu-id="8e79e-145">Microsoft Azure Germany에서 캐시를 만들려면 다음 위치 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-145">To create a cache in Microsoft Azure Germany, use one of the following locations.</span></span>

* <span data-ttu-id="8e79e-146">독일 중부</span><span class="sxs-lookup"><span data-stu-id="8e79e-146">Germany Central</span></span>
* <span data-ttu-id="8e79e-147">독일 북동부</span><span class="sxs-lookup"><span data-stu-id="8e79e-147">Germany Northeast</span></span>

<span data-ttu-id="8e79e-148">Microsoft Azure Germany에 대한 자세한 내용은 [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e79e-148">For more information about Microsoft Azure Germany, see [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span></span>

### <a name="properties-used-for-azure-redis-cache-powershell"></a><span data-ttu-id="8e79e-149">Azure Redis Cache PowerShell에 사용되는 속성</span><span class="sxs-lookup"><span data-stu-id="8e79e-149">Properties used for Azure Redis Cache PowerShell</span></span>
<span data-ttu-id="8e79e-150">다음 표에서는 Azure PowerShell을 사용하여 Azure Redis Cache 인스턴스를 만들고 관리할 때 자주 사용되는 매개 변수에 대한 속성 및 설명을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-150">The following table contains properties and descriptions for commonly used parameters when creating and managing your Azure Redis Cache instances using Azure PowerShell.</span></span>

| <span data-ttu-id="8e79e-151">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8e79e-151">Parameter</span></span> | <span data-ttu-id="8e79e-152">설명</span><span class="sxs-lookup"><span data-stu-id="8e79e-152">Description</span></span> | <span data-ttu-id="8e79e-153">기본값</span><span class="sxs-lookup"><span data-stu-id="8e79e-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8e79e-154">Name</span><span class="sxs-lookup"><span data-stu-id="8e79e-154">Name</span></span> |<span data-ttu-id="8e79e-155">캐시의 이름</span><span class="sxs-lookup"><span data-stu-id="8e79e-155">Name of the cache</span></span> | |
| <span data-ttu-id="8e79e-156">위치</span><span class="sxs-lookup"><span data-stu-id="8e79e-156">Location</span></span> |<span data-ttu-id="8e79e-157">캐시의 위치</span><span class="sxs-lookup"><span data-stu-id="8e79e-157">Location of the cache</span></span> | |
| <span data-ttu-id="8e79e-158">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="8e79e-158">ResourceGroupName</span></span> |<span data-ttu-id="8e79e-159">캐시를 만들 리소스 그룹 이름</span><span class="sxs-lookup"><span data-stu-id="8e79e-159">Resource group name in which to create the cache</span></span> | |
| <span data-ttu-id="8e79e-160">크기</span><span class="sxs-lookup"><span data-stu-id="8e79e-160">Size</span></span> |<span data-ttu-id="8e79e-161">캐시의 크기.</span><span class="sxs-lookup"><span data-stu-id="8e79e-161">The size of the cache.</span></span> <span data-ttu-id="8e79e-162">유효한 값: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span><span class="sxs-lookup"><span data-stu-id="8e79e-162">Valid values are: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span></span> |<span data-ttu-id="8e79e-163">1GB</span><span class="sxs-lookup"><span data-stu-id="8e79e-163">1GB</span></span> |
| <span data-ttu-id="8e79e-164">ShardCount</span><span class="sxs-lookup"><span data-stu-id="8e79e-164">ShardCount</span></span> |<span data-ttu-id="8e79e-165">클러스터링을 사용하는 프리미엄 캐시를 만들 때 만들 분할된 데이터베이스 수.</span><span class="sxs-lookup"><span data-stu-id="8e79e-165">The number of shards to create when creating a premium cache with clustering enabled.</span></span> <span data-ttu-id="8e79e-166">유효한 값: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span><span class="sxs-lookup"><span data-stu-id="8e79e-166">Valid values are: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></span> | |
| <span data-ttu-id="8e79e-167">SKU</span><span class="sxs-lookup"><span data-stu-id="8e79e-167">SKU</span></span> |<span data-ttu-id="8e79e-168">캐시의 SKU를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-168">Specifies the SKU of the cache.</span></span> <span data-ttu-id="8e79e-169">유효한 값: 기본, 표준, 프리미엄</span><span class="sxs-lookup"><span data-stu-id="8e79e-169">Valid values are: Basic, Standard, Premium</span></span> |<span data-ttu-id="8e79e-170">표준</span><span class="sxs-lookup"><span data-stu-id="8e79e-170">Standard</span></span> |
| <span data-ttu-id="8e79e-171">RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="8e79e-171">RedisConfiguration</span></span> |<span data-ttu-id="8e79e-172">Redis 구성 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-172">Specifies Redis configuration settings.</span></span> <span data-ttu-id="8e79e-173">각 설정에 대한 자세한 내용은 다음 [RedisConfiguration 속성](#redisconfiguration-properties) 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e79e-173">For details on each setting, see the following [RedisConfiguration properties](#redisconfiguration-properties) table.</span></span> | |
| <span data-ttu-id="8e79e-174">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="8e79e-174">EnableNonSslPort</span></span> |<span data-ttu-id="8e79e-175">비 SSL 포트를 사용하는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-175">Indicates whether the non-SSL port is enabled.</span></span> |<span data-ttu-id="8e79e-176">False</span><span class="sxs-lookup"><span data-stu-id="8e79e-176">False</span></span> |
| <span data-ttu-id="8e79e-177">MaxMemoryPolicy</span><span class="sxs-lookup"><span data-stu-id="8e79e-177">MaxMemoryPolicy</span></span> |<span data-ttu-id="8e79e-178">이 매개 변수는 더 이상 사용되지 않으며 대신 RedisConfiguration을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-178">This parameter has been deprecated - use RedisConfiguration instead.</span></span> | |
| <span data-ttu-id="8e79e-179">StaticIP</span><span class="sxs-lookup"><span data-stu-id="8e79e-179">StaticIP</span></span> |<span data-ttu-id="8e79e-180">VNET에서 캐시를 호스팅하는 경우 서브넷에서 캐시에 대한 고유 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-180">When hosting your cache in a VNET, specifies a unique IP address in the subnet for the cache.</span></span> <span data-ttu-id="8e79e-181">제공되지 않으면 하나의 IP 주소가 서브넷에서 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-181">If not provided, one is chosen for you from the subnet.</span></span> | |
| <span data-ttu-id="8e79e-182">서브넷</span><span class="sxs-lookup"><span data-stu-id="8e79e-182">Subnet</span></span> |<span data-ttu-id="8e79e-183">VNET에서 캐시를 호스팅하는 경우에 캐시를 배포할 서브넷의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-183">When hosting your cache in a VNET, specifies the name of the subnet in which to deploy the cache.</span></span> | |
| <span data-ttu-id="8e79e-184">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="8e79e-184">VirtualNetwork</span></span> |<span data-ttu-id="8e79e-185">VNET에서 캐시를 호스팅하는 경우에 캐시를 배포할 VNET의 리소스 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-185">When hosting your cache in a VNET, specifies the resource ID of the VNET in which to deploy the cache.</span></span> | |
| <span data-ttu-id="8e79e-186">KeyType</span><span class="sxs-lookup"><span data-stu-id="8e79e-186">KeyType</span></span> |<span data-ttu-id="8e79e-187">액세스 키를 갱신할 때 다시 생성할 액세스 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-187">Specifies which access key to regenerate when renewing access keys.</span></span> <span data-ttu-id="8e79e-188">유효한 값: 주, 보조</span><span class="sxs-lookup"><span data-stu-id="8e79e-188">Valid values are: Primary, Secondary</span></span> | |

### <a name="redisconfiguration-properties"></a><span data-ttu-id="8e79e-189">RedisConfiguration 속성</span><span class="sxs-lookup"><span data-stu-id="8e79e-189">RedisConfiguration properties</span></span>
| <span data-ttu-id="8e79e-190">속성</span><span class="sxs-lookup"><span data-stu-id="8e79e-190">Property</span></span> | <span data-ttu-id="8e79e-191">설명</span><span class="sxs-lookup"><span data-stu-id="8e79e-191">Description</span></span> | <span data-ttu-id="8e79e-192">가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="8e79e-192">Pricing tiers</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8e79e-193">rdb-backup-enabled</span><span class="sxs-lookup"><span data-stu-id="8e79e-193">rdb-backup-enabled</span></span> |<span data-ttu-id="8e79e-194">[Redis 데이터 지속성](cache-how-to-premium-persistence.md) 사용 여부</span><span class="sxs-lookup"><span data-stu-id="8e79e-194">Whether [Redis data persistence](cache-how-to-premium-persistence.md) is enabled</span></span> |<span data-ttu-id="8e79e-195">프리미엄 전용</span><span class="sxs-lookup"><span data-stu-id="8e79e-195">Premium only</span></span> |
| <span data-ttu-id="8e79e-196">rdb-storage-connection-string</span><span class="sxs-lookup"><span data-stu-id="8e79e-196">rdb-storage-connection-string</span></span> |<span data-ttu-id="8e79e-197">[Redis 데이터 지속성](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="8e79e-197">The connection string to the storage account for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="8e79e-198">프리미엄 전용</span><span class="sxs-lookup"><span data-stu-id="8e79e-198">Premium only</span></span> |
| <span data-ttu-id="8e79e-199">rdb-backup-frequency</span><span class="sxs-lookup"><span data-stu-id="8e79e-199">rdb-backup-frequency</span></span> |<span data-ttu-id="8e79e-200">[Redis 데이터 지속성](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="8e79e-200">The backup frequency for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="8e79e-201">프리미엄 전용</span><span class="sxs-lookup"><span data-stu-id="8e79e-201">Premium only</span></span> |
| <span data-ttu-id="8e79e-202">maxmemory-reserved</span><span class="sxs-lookup"><span data-stu-id="8e79e-202">maxmemory-reserved</span></span> |<span data-ttu-id="8e79e-203">비 캐시 프로세스를 위해 [예약되는 메모리](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) 를 구성합니다</span><span class="sxs-lookup"><span data-stu-id="8e79e-203">Configures the [memory reserved](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for non-cache processes</span></span> |<span data-ttu-id="8e79e-204">표준 및 프리미엄</span><span class="sxs-lookup"><span data-stu-id="8e79e-204">Standard and Premium</span></span> |
| <span data-ttu-id="8e79e-205">maxmemory-policy</span><span class="sxs-lookup"><span data-stu-id="8e79e-205">maxmemory-policy</span></span> |<span data-ttu-id="8e79e-206">캐시에 대한 [제거 정책](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) 을 구성합니다</span><span class="sxs-lookup"><span data-stu-id="8e79e-206">Configures the [eviction policy](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for the cache</span></span> |<span data-ttu-id="8e79e-207">모든 가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="8e79e-207">All pricing tiers</span></span> |
| <span data-ttu-id="8e79e-208">notify-keyspace-events</span><span class="sxs-lookup"><span data-stu-id="8e79e-208">notify-keyspace-events</span></span> |<span data-ttu-id="8e79e-209">[Keyspace 알림](cache-configure.md#keyspace-notifications-advanced-settings)</span><span class="sxs-lookup"><span data-stu-id="8e79e-209">Configures [keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings)</span></span> |<span data-ttu-id="8e79e-210">표준 및 프리미엄</span><span class="sxs-lookup"><span data-stu-id="8e79e-210">Standard and Premium</span></span> |
| <span data-ttu-id="8e79e-211">hash-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="8e79e-211">hash-max-ziplist-entries</span></span> |<span data-ttu-id="8e79e-212">작은 집계 데이터 형식에 대한 [메모리 최적화](http://redis.io/topics/memory-optimization) 구성</span><span class="sxs-lookup"><span data-stu-id="8e79e-212">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="8e79e-213">표준 및 프리미엄</span><span class="sxs-lookup"><span data-stu-id="8e79e-213">Standard and Premium</span></span> |
| <span data-ttu-id="8e79e-214">hash-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="8e79e-214">hash-max-ziplist-value</span></span> |<span data-ttu-id="8e79e-215">작은 집계 데이터 형식에 대한 [메모리 최적화](http://redis.io/topics/memory-optimization) 구성</span><span class="sxs-lookup"><span data-stu-id="8e79e-215">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="8e79e-216">표준 및 프리미엄</span><span class="sxs-lookup"><span data-stu-id="8e79e-216">Standard and Premium</span></span> |
| <span data-ttu-id="8e79e-217">set-max-intset-entries</span><span class="sxs-lookup"><span data-stu-id="8e79e-217">set-max-intset-entries</span></span> |<span data-ttu-id="8e79e-218">작은 집계 데이터 형식에 대한 [메모리 최적화](http://redis.io/topics/memory-optimization) 구성</span><span class="sxs-lookup"><span data-stu-id="8e79e-218">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="8e79e-219">표준 및 프리미엄</span><span class="sxs-lookup"><span data-stu-id="8e79e-219">Standard and Premium</span></span> |
| <span data-ttu-id="8e79e-220">zset-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="8e79e-220">zset-max-ziplist-entries</span></span> |<span data-ttu-id="8e79e-221">작은 집계 데이터 형식에 대한 [메모리 최적화](http://redis.io/topics/memory-optimization) 구성</span><span class="sxs-lookup"><span data-stu-id="8e79e-221">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="8e79e-222">표준 및 프리미엄</span><span class="sxs-lookup"><span data-stu-id="8e79e-222">Standard and Premium</span></span> |
| <span data-ttu-id="8e79e-223">zset-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="8e79e-223">zset-max-ziplist-value</span></span> |<span data-ttu-id="8e79e-224">작은 집계 데이터 형식에 대한 [메모리 최적화](http://redis.io/topics/memory-optimization) 구성</span><span class="sxs-lookup"><span data-stu-id="8e79e-224">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="8e79e-225">표준 및 프리미엄</span><span class="sxs-lookup"><span data-stu-id="8e79e-225">Standard and Premium</span></span> |
| <span data-ttu-id="8e79e-226">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="8e79e-226">databases</span></span> |<span data-ttu-id="8e79e-227">데이터베이스 수를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-227">Configures the number of databases.</span></span> <span data-ttu-id="8e79e-228">이 속성은 캐시 만들기에서만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-228">This property can be configured only at cache creation.</span></span> |<span data-ttu-id="8e79e-229">표준 및 프리미엄</span><span class="sxs-lookup"><span data-stu-id="8e79e-229">Standard and Premium</span></span> |

## <a name="to-create-a-redis-cache"></a><span data-ttu-id="8e79e-230">Redis Cache를 만들려면</span><span class="sxs-lookup"><span data-stu-id="8e79e-230">To create a Redis Cache</span></span>
<span data-ttu-id="8e79e-231">[New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet을 사용하여 새 Azure Redis Cache 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-231">New Azure Redis Cache instances are created using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e79e-232">Azure 포털을 사용하여 구독에 처음으로 Redis 캐시를 만들 때 포털은 해당 구독에 대해 `Microsoft.Cache` 네임스페이스를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-232">The first time you create a Redis cache in a subscription using the Azure portal, the portal registers the `Microsoft.Cache` namespace for that subscription.</span></span> <span data-ttu-id="8e79e-233">PowerShell을 사용하여 구독에서 첫 번째 Redis 캐시를 만드는 경우, 먼저 다음 명령을 사용하여 해당 네임스페이스를 등록해야 하며 그렇지 않은 경우 `New-AzureRmRedisCache` 및 `Get-AzureRmRedisCache`의 cmdlet이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-233">If you attempt to create the first Redis cache in a subscription using PowerShell, you must first register that namespace using the following command; otherwise cmdlets such as `New-AzureRmRedisCache` and `Get-AzureRmRedisCache` fail.</span></span>
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

<span data-ttu-id="8e79e-234">`New-AzureRmRedisCache`에 대해 사용 가능한 매개 변수 및 해당 설명에 대한 목록을 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-234">To see a list of available parameters and their descriptions for `New-AzureRmRedisCache`, run the following command.</span></span>

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
        The New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of the redis cache to create.

        -ResourceGroupName <String>
            Name of resource group in which to create the redis cache.

        -Location <String>
            Location in which to create the redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of the redis cache. The default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. The default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            The 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting to set
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, the default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            The number of shards to create on a Premium Cluster Cache.

        -VirtualNetwork <String>
            The exact ARM resource ID of the virtual network to deploy the redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="8e79e-235">기본 매개 변수로 캐시를 만들려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-235">To create a cache with default parameters, run the following command.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

<span data-ttu-id="8e79e-236">`ResourceGroupName`, `Name` 및 `Location`은 필수 매개 변수이지만 나머지는 선택 사항이며 기본값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-236">`ResourceGroupName`, `Name`, and `Location` are required parameters, but the rest are optional and have default values.</span></span> <span data-ttu-id="8e79e-237">이전 명령을 실행하면 지정된 이름, 위치 및 리소스 그룹으로 크기 1GB의 표준 SKU Azure Redis Cache 인스턴스가 비 SSL 포트가 비활성화된 상태로 만들어집니다. </span><span class="sxs-lookup"><span data-stu-id="8e79e-237">Running the previous command creates a Standard SKU Azure Redis Cache instance with the specified name, location, and resource group, that is 1 GB in size with the non-SSL port disabled.</span></span>

<span data-ttu-id="8e79e-238">프리미엄 캐시를 만들려면 P1(6GB - 60GB), P2(13GB - 130GB), P3(26GB - 260GB) 또는 P4(53GB - 530GB) 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-238">To create a premium cache, specify a size of P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), or P4 (53 GB - 530 GB).</span></span> <span data-ttu-id="8e79e-239">클러스터링을 사용하려면 `ShardCount` 매개 변수를 사용하여 분할된 데이터베이스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-239">To enable clustering, specify a shard count using the `ShardCount` parameter.</span></span> <span data-ttu-id="8e79e-240">다음 예제에서는 3개의 분할된 데이터베이스가 있는 P1 프리미엄 캐시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-240">The following example creates a P1 premium cache with 3 shards.</span></span> <span data-ttu-id="8e79e-241">P1 프리미엄 캐시는 6GB 크기이고 3개의 분할된 데이터베이스를 지정했으므로 총 크기는 18GB(3 x 6GB)입니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-241">A P1 premium cache is 6 GB in size, and since we specified three shards the total size is 18 GB (3 x 6 GB).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

<span data-ttu-id="8e79e-242">`RedisConfiguration` 매개 변수에 대한 값을 지정하려면 `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`처럼 키/값 쌍으로 값을 `{}`로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-242">To specify values for the `RedisConfiguration` parameter, enclose the values inside `{}` as key/value pairs like `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span></span> <span data-ttu-id="8e79e-243">다음 예제에서는 `allkeys-random` 최대 정책을 사용하고 `KEA`의 keyspace 알림이 구성된 표준 1GB 캐시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-243">The following example creates a standard 1 GB cache with `allkeys-random` maxmemory policy and keyspace notifications configured with `KEA`.</span></span> <span data-ttu-id="8e79e-244">자세한 내용은 [Keyspace 알림(고급 설정)](cache-configure.md#keyspace-notifications-advanced-settings) 및 [메모리 정책](cache-configure.md#memory-policies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e79e-244">For more information, see [Keyspace notifications (advanced settings)](cache-configure.md#keyspace-notifications-advanced-settings) and [Memory policies](cache-configure.md#memory-policies).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="to-configure-the-databases-setting-during-cache-creation"></a><span data-ttu-id="8e79e-245">캐시를 만드는 동안 데이터베이스 설정을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="8e79e-245">To configure the databases setting during cache creation</span></span>
<span data-ttu-id="8e79e-246">`databases` 설정은 캐시를 만드는 동안에만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-246">The `databases` setting can be configured only during cache creation.</span></span> <span data-ttu-id="8e79e-247">다음 예제에서는 [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet를 사용하여 48 데이터베이스로 프리미엄 P3 (26 GB) 캐시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-247">The following example creates a premium P3 (26 GB) cache with 48 databases using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

<span data-ttu-id="8e79e-248">`databases` 속성에 대한 자세한 내용은 [기본 Azure Redis Cache 서버 구성](cache-configure.md#default-redis-server-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e79e-248">For more information on the `databases` property, see [Default Azure Redis Cache server configuration](cache-configure.md#default-redis-server-configuration).</span></span> <span data-ttu-id="8e79e-249">[New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet를 사용하여 캐시를 만드는 방법에 대한 자세한 내용은 이전의 [Redis 캐시 만들려면](#to-create-a-redis-cache) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e79e-249">For more information on creating a cache using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, see the previous [To create a Redis Cache](#to-create-a-redis-cache) section.</span></span>

## <a name="to-update-a-redis-cache"></a><span data-ttu-id="8e79e-250">Redis Cache를 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="8e79e-250">To update a Redis cache</span></span>
<span data-ttu-id="8e79e-251">[Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet을 사용하여 Azure Redis Cache 인스턴스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-251">Azure Redis Cache instances are updated using the [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span></span>

<span data-ttu-id="8e79e-252">`Set-AzureRmRedisCache`에 대해 사용 가능한 매개 변수 및 해당 설명에 대한 목록을 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-252">To see a list of available parameters and their descriptions for `Set-AzureRmRedisCache`, run the following command.</span></span>

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
        The Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of the redis cache to update.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        -Size <String>
            Size of the redis cache. The default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. The default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            The 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting to set
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. The default value is null and no change will be made to the
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            The number of shards to create on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="8e79e-253">`Size`, `Sku`, `EnableNonSslPort`의 속성과 `RedisConfiguration` 값을 업데이트하는 데 `Set-AzureRmRedisCache` cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-253">The `Set-AzureRmRedisCache` cmdlet can be used to update properties such as `Size`, `Sku`, `EnableNonSslPort`, and the `RedisConfiguration` values.</span></span> 

<span data-ttu-id="8e79e-254">다음 명령은 myCache라는 Redis Cache에 대한 maxmemory-policy를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-254">The following command updates the maxmemory-policy for the Redis Cache named myCache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="to-scale-a-redis-cache"></a><span data-ttu-id="8e79e-255">Redis Cache의 크기를 조정하려면</span><span class="sxs-lookup"><span data-stu-id="8e79e-255">To scale a Redis cache</span></span>
<span data-ttu-id="8e79e-256">`Size`, `Sku` 또는 `ShardCount` 속성이 수정될 때 Azure Redis Cache 인스턴스 크기를 조정하는 데 `Set-AzureRmRedisCache`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-256">`Set-AzureRmRedisCache` can be used to scale an Azure Redis cache instance when the `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> 

> [!NOTE]
> <span data-ttu-id="8e79e-257">PowerShell을 사용하여 캐시 크기를 조정할 경우 Azure 포털에서 캐시 크기를 조정할 때와 동일한 한도 및 지침이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-257">Scaling a cache using PowerShell is subject to the same limits and guidelines as scaling a cache from the Azure portal.</span></span> <span data-ttu-id="8e79e-258">다른 가격 책정 계층으로 크기를 조정할 수 있지만 다음과 같은 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-258">You can scale to a different pricing tier with the following restrictions.</span></span>
> 
> * <span data-ttu-id="8e79e-259">높은 가격 책정 계층에서 낮은 가격 책정 계층으로 크기를 조정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-259">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
> * <span data-ttu-id="8e79e-260">**프리미엄** 캐시에서 **표준** 또는 **기본** 캐시로 축소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-260">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
> * <span data-ttu-id="8e79e-261">**표준** 캐시에서 **기본** 캐시로 축소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-261">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
> * <span data-ttu-id="8e79e-262">**기본** 캐시에서 **표준** 캐시로 크기를 조정할 수 있지만 동시에 크기를 변경할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-262">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="8e79e-263">다른 크기가 필요한 경우 후속 크기 조정 작업을 통해 원하는 크기로 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-263">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
> * <span data-ttu-id="8e79e-264">**기본** 캐시에서 바로 **프리미엄** 캐시로 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-264">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="8e79e-265">크기 조정 작업을 통해 **기본**에서 **표준**으로 확장한 다음, 후속 크기 조정 작업을 통해 **표준**에서 **프리미엄**으로 확장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-265">You must scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
> * <span data-ttu-id="8e79e-266">더 큰 크기에서 **C0(250MB)** 크기로 축소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-266">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>
> 
> <span data-ttu-id="8e79e-267">자세한 내용은 [Azure Redis Cache 크기를 조정하는 방법](cache-how-to-scale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e79e-267">For more information, see [How to Scale Azure Redis Cache](cache-how-to-scale.md).</span></span>
> 
> 

<span data-ttu-id="8e79e-268">다음 예제에서는 `myCache` 라는 캐시를 2.5GB 캐시로 크기를 조정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-268">The following example shows how to scale a cache named `myCache` to a 2.5 GB cache.</span></span> <span data-ttu-id="8e79e-269">이 명령은 기본 또는 표준 캐시 둘 다에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-269">Note that this command works for both a Basic or a Standard cache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="8e79e-270">이 명령을 실행하면 캐시 상태가 반환됩니다( `Get-AzureRmRedisCache`호출과 유사).</span><span class="sxs-lookup"><span data-stu-id="8e79e-270">After this command is issued, the status of the cache is returned (similar to calling `Get-AzureRmRedisCache`).</span></span> <span data-ttu-id="8e79e-271">여기서 `ProvisioningState`는 `Scaling`입니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-271">Note that the `ProvisioningState` is `Scaling`.</span></span>

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

<span data-ttu-id="8e79e-272">크기 조정 작업이 완료되면 `ProvisioningState`는 `Succeeded`로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-272">When the scaling operation is complete, the `ProvisioningState` changes to `Succeeded`.</span></span> <span data-ttu-id="8e79e-273">기본에서 표준으로 변경 후 크기 변경과 같은 후속 크기 조정 작업을 수행해야 하는 경우 이전 작업이 완료될 때까지 대기해야 하며 그렇지 않은 경우 다음과 같은 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-273">If you need to make a subsequent scaling operation, such as changing from Basic to Standard and then changing the size, you must wait until the previous operation is complete or you receive an error similar to the following.</span></span>

    Set-AzureRmRedisCache : Conflict: The resource '...' is not in a stable state, and is currently unable to accept the update request.

## <a name="to-get-information-about-a-redis-cache"></a><span data-ttu-id="8e79e-274">Redis Cache에 대한 정보를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="8e79e-274">To get information about a Redis cache</span></span>
<span data-ttu-id="8e79e-275">[Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet을 사용하여 캐시에 대한 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-275">You can retrieve information about a cache using the [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span></span>

<span data-ttu-id="8e79e-276">`Get-AzureRmRedisCache`에 대해 사용 가능한 매개 변수 및 해당 설명에 대한 목록을 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-276">To see a list of available parameters and their descriptions for `Get-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in the specified resource group or all caches in the current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        The Get-AzureRmRedisCache cmdlet gets the details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in the specified resource group.

        If no parameters are given than it will return details about all caches the current subscription.

    PARAMETERS
        -Name <String>
            The name of the cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns the details for the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns the details of the cache specified by Name. If only the ResourceGroup
            parameter is provided, then details for all caches in the resource group are returned.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="8e79e-277">현재 구독의 모든 캐시에 대한 정보를 반환하려면 매개 변수 없이 `Get-AzureRmRedisCache`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-277">To return information about all caches in the current subscription, run `Get-AzureRmRedisCache` without any parameters.</span></span>

    Get-AzureRmRedisCache

<span data-ttu-id="8e79e-278">특정 리소스 그룹의 모든 캐시에 대한 정보를 반환하려면 `ResourceGroupName` 매개 변수와 함께 `Get-AzureRmRedisCache`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-278">To return information about all caches in a specific resource group, run `Get-AzureRmRedisCache` with the `ResourceGroupName` parameter.</span></span>

    Get-AzureRmRedisCache -ResourceGroupName myGroup

<span data-ttu-id="8e79e-279">특정 캐시에 대한 정보를 반환하려면 캐시 이름을 포함하는 `Name` 매개 변수와 해당 캐시를 포함하는 리소스 그룹이 있는 `ResourceGroupName` 매개 변수와 함께 `Get-AzureRmRedisCache`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-279">To return information about a specific cache, run `Get-AzureRmRedisCache` with the `Name` parameter containing the name of the cache, and the `ResourceGroupName` parameter with the resource group containing that cache.</span></span>

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

## <a name="to-retrieve-the-access-keys-for-a-redis-cache"></a><span data-ttu-id="8e79e-280">Redis Cache에 대한 액세스 키를 검색하려면</span><span class="sxs-lookup"><span data-stu-id="8e79e-280">To retrieve the access keys for a Redis cache</span></span>
<span data-ttu-id="8e79e-281">캐시에 대한 액세스 키를 검색하려면 [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-281">To retrieve the access keys for your cache, you can use the [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span></span>

<span data-ttu-id="8e79e-282">`Get-AzureRmRedisCacheKey`에 대해 사용 가능한 매개 변수 및 해당 설명에 대한 목록을 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-282">To see a list of available parameters and their descriptions for `Get-AzureRmRedisCacheKey`, run the following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets the accesskeys for the specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        The Get-AzureRmRedisCacheKey cmdlet gets the access keys for the specified cache.

    PARAMETERS
        -Name <String>
            Name of the redis cache.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="8e79e-283">캐시에 대한 키를 검색하려면 `Get-AzureRmRedisCacheKey` cmdlet을 호출하고 캐시 이름과 해당 캐시를 포함하는 리소스 그룹 이름을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-283">To retrieve the keys for your cache, call the `Get-AzureRmRedisCacheKey` cmdlet and pass in the name of your cache the name of the resource group that contains the cache.</span></span>

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="to-regenerate-access-keys-for-your-redis-cache"></a><span data-ttu-id="8e79e-284">Redis Cache에 대한 액세스 키를 다시 생성하려면</span><span class="sxs-lookup"><span data-stu-id="8e79e-284">To regenerate access keys for your Redis cache</span></span>
<span data-ttu-id="8e79e-285">캐시에 대한 액세스 키를 다시 생성하려면 [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-285">To regenerate the access keys for your cache, you can use the [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span></span>

<span data-ttu-id="8e79e-286">`New-AzureRmRedisCacheKey`에 대해 사용 가능한 매개 변수 및 해당 설명에 대한 목록을 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-286">To see a list of available parameters and their descriptions for `New-AzureRmRedisCacheKey`, run the following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates the access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        The New-AzureRmRedisCacheKey cmdlet regenerate the access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of the redis cache.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        -KeyType <String>
            Specifies whether to regenerate the primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When the Force parameter is provided, the specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="8e79e-287">캐시에 대한 주 및 보조 키를 다시 생성하려면 `New-AzureRmRedisCacheKey` cmdlet을 호출하고 이름, 리소스 그룹을 전달하고 `KeyType` 매개 변수에 대해 `Primary` 또는 `Secondary`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-287">To regenerate the primary or secondary key for your cache, call the `New-AzureRmRedisCacheKey` cmdlet and pass in the name, resource group, and specify either `Primary` or `Secondary` for the `KeyType` parameter.</span></span> <span data-ttu-id="8e79e-288">다음 예제에서는 캐시에 대한 보조 액세스 키가 다시 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-288">In the following example, the secondary access key for a cache is regenerated.</span></span>

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want to regenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="to-delete-a-redis-cache"></a><span data-ttu-id="8e79e-289">Redis Cache를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="8e79e-289">To delete a Redis cache</span></span>
<span data-ttu-id="8e79e-290">Redis Cache를 삭제하려면 [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-290">To delete a Redis cache, use the [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span></span>

<span data-ttu-id="8e79e-291">`Remove-AzureRmRedisCache`에 대해 사용 가능한 매개 변수 및 해당 설명에 대한 목록을 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-291">To see a list of available parameters and their descriptions for `Remove-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        The Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of the redis cache to remove.

        -ResourceGroupName <String>
            Name of the resource group of the cache to remove.

        -Force
            When the Force parameter is provided, the cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes the cache and does not return any value. If the PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating the success of the operatio

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="8e79e-292">다음 예제에서는 캐시 이름 `myCache` 가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-292">In the following example, the cache named `myCache` is removed.</span></span>

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want to remove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="to-import-a-redis-cache"></a><span data-ttu-id="8e79e-293">Redis Cache를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="8e79e-293">To import a Redis cache</span></span>
<span data-ttu-id="8e79e-294">`Import-AzureRmRedisCache` cmdlet을 사용하여 Azure Redis Cache 인스턴스에 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-294">You can import data into an Azure Redis Cache instance using the `Import-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e79e-295">가져오기/내보내기는 [프리미엄 계층](cache-premium-tier-intro.md) 캐시에만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-295">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="8e79e-296">가져오기/내보내기에 대한 자세한 내용은 [Azure Redis Cache에서 데이터 가져오기 및 내보내기](cache-how-to-import-export-data.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e79e-296">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="8e79e-297">`Import-AzureRmRedisCache`에 대해 사용 가능한 매개 변수 및 해당 설명에 대한 목록을 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-297">To see a list of available parameters and their descriptions for `Import-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs to Azure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Import-AzureRmRedisCache cmdlet imports data from the specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into the cache.

        -Format <String>
            Format for the blob.  Currently "rdb" is the only supported, with other formats expected in the future.

        -Force
            When the Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If the PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating the success of the
            operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="8e79e-298">다음 명령은 SAS URI가 지정한 Blob에서 Azure Redis Cache에 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-298">The following command imports data from the blob specified by the SAS uri into Azure Redis Cache.</span></span>

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="to-export-a-redis-cache"></a><span data-ttu-id="8e79e-299">Redis Cache를 내보내려면</span><span class="sxs-lookup"><span data-stu-id="8e79e-299">To export a Redis cache</span></span>
<span data-ttu-id="8e79e-300">`Export-AzureRmRedisCache` cmdlet을 사용하여 Azure Redis Cache 인스턴스에서 데이터를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-300">You can export data from an Azure Redis Cache instance using the `Export-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e79e-301">가져오기/내보내기는 [프리미엄 계층](cache-premium-tier-intro.md) 캐시에만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-301">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="8e79e-302">가져오기/내보내기에 대한 자세한 내용은 [Azure Redis Cache에서 데이터 가져오기 및 내보내기](cache-how-to-import-export-data.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e79e-302">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="8e79e-303">`Export-AzureRmRedisCache`에 대해 사용 가능한 매개 변수 및 해당 설명에 대한 목록을 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-303">To see a list of available parameters and their descriptions for `Export-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache to a specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache to a specified container.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -Prefix <String>
            Prefix to use for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for the blob.  Currently "rdb" is the only supported, with other formats expected in the future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If the PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating the success of the operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="8e79e-304">다음 명령은 Azure Redis Cache 인스턴스에서 SAS uri가 지정한 컨테이너로 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-304">The following command exports data from an Azure Redis Cache instance into the container specified by the SAS uri.</span></span>

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="to-reboot-a-redis-cache"></a><span data-ttu-id="8e79e-305">Redis Cache를 재부팅하려면</span><span class="sxs-lookup"><span data-stu-id="8e79e-305">To reboot a Redis cache</span></span>
<span data-ttu-id="8e79e-306">`Reset-AzureRmRedisCache` cmdlet을 사용하여 Azure Redis Cache 인스턴스를 재부팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-306">You can reboot your Azure Redis Cache instance using the `Reset-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e79e-307">재부팅은 [프리미엄 계층](cache-premium-tier-intro.md) 캐시에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-307">Reboot is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="8e79e-308">캐시를 재부팅하는 방법에 대한 자세한 내용은 [캐시 관리 - 재부팅](cache-administration.md#reboot)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e79e-308">For more information about rebooting your cache, see [Cache administration - reboot](cache-administration.md#reboot).</span></span>
> 
> 

<span data-ttu-id="8e79e-309">`Reset-AzureRmRedisCache`에 대해 사용 가능한 매개 변수 및 해당 설명에 대한 목록을 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-309">To see a list of available parameters and their descriptions for `Reset-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Reset-AzureRmRedisCache cmdlet reboots the specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -RebootType <String>
            Which node to reboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard to reboot when rebooting a premium cache with clustering enabled.

        -Force
            When the Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If the PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating the success of the operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="8e79e-310">다음 명령은 지정된 캐시의 두 노드를 모두 재부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-310">The following command reboots both nodes of the specified cache.</span></span>

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a><span data-ttu-id="8e79e-311">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8e79e-311">Next steps</span></span>
<span data-ttu-id="8e79e-312">Azure에서 Windows PowerShell 사용에 대한 자세한 내용은 다음 리소스를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="8e79e-312">To learn more about using Windows PowerShell with Azure, see the following resources:</span></span>

* [<span data-ttu-id="8e79e-313">MSDN에 있는 Azure Redis Cache cmdlet 설명서</span><span class="sxs-lookup"><span data-stu-id="8e79e-313">Azure Redis Cache cmdlet documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* <span data-ttu-id="8e79e-314">[Azure Resource Manager Cmdlet](http://go.microsoft.com/fwlink/?LinkID=394765): Azure Resource Manager 모듈에서 cmdlet을 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): Learn to use the cmdlets in the Azure Resource Manager module.</span></span>
* <span data-ttu-id="8e79e-315">[리소스 그룹을 사용하여 Azure 리소스 관리](../azure-resource-manager/resource-group-template-deploy-portal.md): Azure 포털에서 리소스 그룹을 만들고 관리하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-315">[Using Resource groups to manage your Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md): Learn how to create and manage resource groups in the Azure portal.</span></span>
* <span data-ttu-id="8e79e-316">[Azure 블로그](http://blogs.msdn.com/windowsazure): Azure의 새로운 기능에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-316">[Azure blog](http://blogs.msdn.com/windowsazure): Learn about new features in Azure.</span></span>
* <span data-ttu-id="8e79e-317">[Windows PowerShell 블로그](http://blogs.msdn.com/powershell): Windows PowerShell의 새로운 기능에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-317">[Windows PowerShell blog](http://blogs.msdn.com/powershell): Learn about new features in Windows PowerShell.</span></span>
* <span data-ttu-id="8e79e-318">["Hey, Scripting Guy!" 블로그](http://blogs.technet.com/b/heyscriptingguy/): Windows PowerShell 커뮤니티에서 실제 팁과 요령을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8e79e-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Get real-world tips and tricks from the Windows PowerShell community.</span></span>

