---
title: "PowerShell을 사용하여 Azure 미디어 서비스 계정 관리"
description: "PowerShell cmdlet를 사용하여 Azure 미디어 서비스 계정을 관리하는 방법에 대해 알아봅니다."
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: 3d999d9e27844bc0164cc3572522b9ec022118a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="366c7-103">PowerShell을 사용하여 Azure 미디어 서비스 계정 관리</span><span class="sxs-lookup"><span data-stu-id="366c7-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="366c7-104">포털</span><span class="sxs-lookup"><span data-stu-id="366c7-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="366c7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="366c7-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="366c7-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="366c7-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="366c7-107">Azure 미디어 서비스 계정을 만들려면 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-107">To be able to create an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="366c7-108">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="366c7-109">자세한 내용은 <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure 무료 평가판</a>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366c7-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="366c7-110">개요</span><span class="sxs-lookup"><span data-stu-id="366c7-110">Overview</span></span>
<span data-ttu-id="366c7-111">이 문서는 Azure Resource Manager 프레임워크의 AMS(Azure 미디어 서비스)에 대한 Azure PowerShell cmdlet을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-111">This article lists the Azure PowerShell cmdlets for Azure Media Services (AMS) in the Azure Resource Manager framework.</span></span> <span data-ttu-id="366c7-112">Cmdlet는 **Microsoft.Azure.Commands.Media** 네임스페이스에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-112">The cmdlets exist in the **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="366c7-113">버전</span><span class="sxs-lookup"><span data-stu-id="366c7-113">Versions</span></span>
<span data-ttu-id="366c7-114">**ApiVersion**: "2015-10-01"</span><span class="sxs-lookup"><span data-stu-id="366c7-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="366c7-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="366c7-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="366c7-116">미디어 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="366c7-117">구문</span><span class="sxs-lookup"><span data-stu-id="366c7-117">Syntax</span></span>
<span data-ttu-id="366c7-118">매개 변수 집합: StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="366c7-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="366c7-119">매개 변수 집합: StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="366c7-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="366c7-120">매개 변수</span><span class="sxs-lookup"><span data-stu-id="366c7-120">Parameters</span></span>
<span data-ttu-id="366c7-121">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="366c7-122">이 미디어 서비스가 속하는 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-122">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="366c7-123">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-123">Aliases</span></span> | <span data-ttu-id="366c7-124">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-125">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-125">Required?</span></span> |<span data-ttu-id="366c7-126">true</span><span class="sxs-lookup"><span data-stu-id="366c7-126">true</span></span> |
| <span data-ttu-id="366c7-127">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-127">Position?</span></span> |<span data-ttu-id="366c7-128">0</span><span class="sxs-lookup"><span data-stu-id="366c7-128">0</span></span> |
| <span data-ttu-id="366c7-129">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-129">Default value</span></span> |<span data-ttu-id="366c7-130">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-130">none</span></span> |
| <span data-ttu-id="366c7-131">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-131">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-132">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-133">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-133">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-134">false</span><span class="sxs-lookup"><span data-stu-id="366c7-134">false</span></span> |

<span data-ttu-id="366c7-135">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="366c7-136">미디어 서비스의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-136">Specifies the name of the media service.</span></span>

| <span data-ttu-id="366c7-137">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-137">Aliases</span></span> | <span data-ttu-id="366c7-138">Name</span><span class="sxs-lookup"><span data-stu-id="366c7-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-139">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-139">Required?</span></span> |<span data-ttu-id="366c7-140">true</span><span class="sxs-lookup"><span data-stu-id="366c7-140">true</span></span> |
| <span data-ttu-id="366c7-141">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-141">Position?</span></span> |<span data-ttu-id="366c7-142">1</span><span class="sxs-lookup"><span data-stu-id="366c7-142">1</span></span> |
| <span data-ttu-id="366c7-143">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-143">Default value</span></span> |<span data-ttu-id="366c7-144">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-144">none</span></span> |
| <span data-ttu-id="366c7-145">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-145">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-146">false</span><span class="sxs-lookup"><span data-stu-id="366c7-146">false</span></span> |
| <span data-ttu-id="366c7-147">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-147">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-148">false</span><span class="sxs-lookup"><span data-stu-id="366c7-148">false</span></span> |

<span data-ttu-id="366c7-149">**-Location &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="366c7-150">미디어 서비스의 리소스 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-150">Specifies the resource location of the media service.</span></span>

| <span data-ttu-id="366c7-151">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-151">Aliases</span></span> | <span data-ttu-id="366c7-152">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-153">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-153">Required?</span></span> |<span data-ttu-id="366c7-154">true</span><span class="sxs-lookup"><span data-stu-id="366c7-154">true</span></span> |
| <span data-ttu-id="366c7-155">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-155">Position?</span></span> |<span data-ttu-id="366c7-156">2</span><span class="sxs-lookup"><span data-stu-id="366c7-156">2</span></span> |
| <span data-ttu-id="366c7-157">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-157">Default value</span></span> |<span data-ttu-id="366c7-158">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-158">none</span></span> |
| <span data-ttu-id="366c7-159">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-159">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-160">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-161">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-161">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-162">false</span><span class="sxs-lookup"><span data-stu-id="366c7-162">false</span></span> |

<span data-ttu-id="366c7-163">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="366c7-164">미디어 서비스와 연결된 기본 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-164">Specifies a primary storage account that associated with the media service.</span></span>

* <span data-ttu-id="366c7-165">(리소스 관리자 API로 만든) 새 저장소 계정 만 지원함.</span><span class="sxs-lookup"><span data-stu-id="366c7-165">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="366c7-166">저장소 계정이 존재하며 미디어 서비스와 동일한 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-166">The storage account must exist and has the same location with the media service.</span></span>

| <span data-ttu-id="366c7-167">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-167">Aliases</span></span> | <span data-ttu-id="366c7-168">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-169">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-169">Required?</span></span> |<span data-ttu-id="366c7-170">true</span><span class="sxs-lookup"><span data-stu-id="366c7-170">true</span></span> |
| <span data-ttu-id="366c7-171">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-171">Position?</span></span> |<span data-ttu-id="366c7-172">3</span><span class="sxs-lookup"><span data-stu-id="366c7-172">3</span></span> |
| <span data-ttu-id="366c7-173">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-173">Default value</span></span> |<span data-ttu-id="366c7-174">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-174">none</span></span> |
| <span data-ttu-id="366c7-175">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-175">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-176">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-177">매개 변수 집합 이름</span><span class="sxs-lookup"><span data-stu-id="366c7-177">Parameter set name</span></span> |<span data-ttu-id="366c7-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="366c7-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="366c7-179">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-179">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-180">false</span><span class="sxs-lookup"><span data-stu-id="366c7-180">false</span></span> |

<span data-ttu-id="366c7-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="366c7-182">미디어 서비스와 연결된 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-182">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="366c7-183">(리소스 관리자 API로 만든) 새 저장소 계정 만 지원함.</span><span class="sxs-lookup"><span data-stu-id="366c7-183">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="366c7-184">저장소 계정이 존재하며 미디어 서비스와 동일한 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-184">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="366c7-185">단 하나의 저장소 계정 만을 기본으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="366c7-186">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-186">Aliases</span></span> | <span data-ttu-id="366c7-187">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-188">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-188">Required?</span></span> |<span data-ttu-id="366c7-189">true</span><span class="sxs-lookup"><span data-stu-id="366c7-189">true</span></span> |
| <span data-ttu-id="366c7-190">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-190">Position?</span></span> |<span data-ttu-id="366c7-191">3</span><span class="sxs-lookup"><span data-stu-id="366c7-191">3</span></span> |
| <span data-ttu-id="366c7-192">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-192">Default value</span></span> |<span data-ttu-id="366c7-193">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-193">none</span></span> |
| <span data-ttu-id="366c7-194">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-194">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-195">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-196">매개 변수 집합 이름</span><span class="sxs-lookup"><span data-stu-id="366c7-196">Parameter set name</span></span> |<span data-ttu-id="366c7-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="366c7-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="366c7-198">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-198">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-199">false</span><span class="sxs-lookup"><span data-stu-id="366c7-199">false</span></span> |

<span data-ttu-id="366c7-200">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="366c7-201">미디어 서비스와 연결된 태그의 해시 테이블을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-201">Specifies a hash table of the tags that are associated with the media service.</span></span>

* <span data-ttu-id="366c7-202">예: @{"tag1"="value1";" tag2 "=: value2"을 (를)</span><span class="sxs-lookup"><span data-stu-id="366c7-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="366c7-203">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-203">Aliases</span></span> | <span data-ttu-id="366c7-204">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-205">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-205">Required?</span></span> |<span data-ttu-id="366c7-206">false</span><span class="sxs-lookup"><span data-stu-id="366c7-206">false</span></span> |
| <span data-ttu-id="366c7-207">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-207">Position?</span></span> |<span data-ttu-id="366c7-208">named</span><span class="sxs-lookup"><span data-stu-id="366c7-208">named</span></span> |
| <span data-ttu-id="366c7-209">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-209">Default value</span></span> |<span data-ttu-id="366c7-210">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-210">none</span></span> |
| <span data-ttu-id="366c7-211">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-211">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-212">false</span><span class="sxs-lookup"><span data-stu-id="366c7-212">false</span></span> |
| <span data-ttu-id="366c7-213">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-213">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-214">false</span><span class="sxs-lookup"><span data-stu-id="366c7-214">false</span></span> |

<span data-ttu-id="366c7-215">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="366c7-216">이 cmdlet 일반 매개 변수를 지원합니다. -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction 및 -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="366c7-216">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="366c7-217">입력</span><span class="sxs-lookup"><span data-stu-id="366c7-217">Inputs</span></span>
<span data-ttu-id="366c7-218">입력 형식은 cmdlet으로 파이프할 수 있는 개체의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-218">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="366c7-219">출력</span><span class="sxs-lookup"><span data-stu-id="366c7-219">Outputs</span></span>
<span data-ttu-id="366c7-220">출력 형식은 cmdlet이 내보내는 개체의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-220">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="366c7-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="366c7-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="366c7-222">미디어 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="366c7-223">구문</span><span class="sxs-lookup"><span data-stu-id="366c7-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="366c7-224">매개 변수</span><span class="sxs-lookup"><span data-stu-id="366c7-224">Parameters</span></span>
<span data-ttu-id="366c7-225">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="366c7-226">이 미디어 서비스가 속하는 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-226">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="366c7-227">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-227">Aliases</span></span> | <span data-ttu-id="366c7-228">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-229">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-229">Required?</span></span> |<span data-ttu-id="366c7-230">true</span><span class="sxs-lookup"><span data-stu-id="366c7-230">true</span></span> |
| <span data-ttu-id="366c7-231">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-231">Position?</span></span> |<span data-ttu-id="366c7-232">0</span><span class="sxs-lookup"><span data-stu-id="366c7-232">0</span></span> |
| <span data-ttu-id="366c7-233">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-233">Default Value</span></span> |<span data-ttu-id="366c7-234">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-234">none</span></span> |
| <span data-ttu-id="366c7-235">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="366c7-236">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-237">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-237">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-238">false</span><span class="sxs-lookup"><span data-stu-id="366c7-238">false</span></span> |

<span data-ttu-id="366c7-239">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="366c7-240">미디어 서비스의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-240">Specifies the name of the media service.</span></span>

| <span data-ttu-id="366c7-241">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-241">Aliases</span></span> | <span data-ttu-id="366c7-242">Name</span><span class="sxs-lookup"><span data-stu-id="366c7-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-243">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-243">Required?</span></span> |<span data-ttu-id="366c7-244">true</span><span class="sxs-lookup"><span data-stu-id="366c7-244">True</span></span> |
| <span data-ttu-id="366c7-245">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-245">Position?</span></span> |<span data-ttu-id="366c7-246">1</span><span class="sxs-lookup"><span data-stu-id="366c7-246">1</span></span> |
| <span data-ttu-id="366c7-247">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-247">Default value</span></span> |<span data-ttu-id="366c7-248">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-248">None</span></span> |
| <span data-ttu-id="366c7-249">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-249">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-250">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-251">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-251">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-252">False</span><span class="sxs-lookup"><span data-stu-id="366c7-252">False</span></span> |

<span data-ttu-id="366c7-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="366c7-254">미디어 서비스와 연결된 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-254">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="366c7-255">(리소스 관리자 API로 만든) 새 저장소 계정 만 지원함.</span><span class="sxs-lookup"><span data-stu-id="366c7-255">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="366c7-256">저장소 계정이 존재하며 미디어 서비스와 동일한 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-256">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="366c7-257">단 하나의 저장소 계정 만을 기본으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="366c7-258">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-258">Aliases</span></span> | <span data-ttu-id="366c7-259">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-260">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-260">Required?</span></span> |<span data-ttu-id="366c7-261">false</span><span class="sxs-lookup"><span data-stu-id="366c7-261">false</span></span> |
| <span data-ttu-id="366c7-262">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-262">Position?</span></span> |<span data-ttu-id="366c7-263">named</span><span class="sxs-lookup"><span data-stu-id="366c7-263">Named</span></span> |
| <span data-ttu-id="366c7-264">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-264">Default value</span></span> |<span data-ttu-id="366c7-265">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-265">none</span></span> |
| <span data-ttu-id="366c7-266">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-266">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-267">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-268">매개 변수 집합 이름</span><span class="sxs-lookup"><span data-stu-id="366c7-268">Parameter set name</span></span> |<span data-ttu-id="366c7-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="366c7-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="366c7-270">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-270">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-271">false</span><span class="sxs-lookup"><span data-stu-id="366c7-271">false</span></span> |

<span data-ttu-id="366c7-272">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="366c7-273">이 미디어 서비스와 연결된 태그의 해시 테이블을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-273">Specifies a hash table of the tags that are associated with this media service.</span></span>

* <span data-ttu-id="366c7-274">미디어 서비스와 연결된 태그가 고객이 지정한 값으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-274">The tags that are associated with the media service are replaced with value specified by the customer.</span></span>

| <span data-ttu-id="366c7-275">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-275">Aliases</span></span> | <span data-ttu-id="366c7-276">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-277">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-277">Required?</span></span> |<span data-ttu-id="366c7-278">false</span><span class="sxs-lookup"><span data-stu-id="366c7-278">False</span></span> |
| <span data-ttu-id="366c7-279">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-279">Position?</span></span> |<span data-ttu-id="366c7-280">named</span><span class="sxs-lookup"><span data-stu-id="366c7-280">Named</span></span> |
| <span data-ttu-id="366c7-281">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-281">Default value</span></span> |<span data-ttu-id="366c7-282">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-282">None</span></span> |
| <span data-ttu-id="366c7-283">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-283">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-284">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-285">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-285">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-286">false</span><span class="sxs-lookup"><span data-stu-id="366c7-286">false</span></span> |

<span data-ttu-id="366c7-287">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="366c7-288">이 cmdlet 일반 매개 변수를 지원합니다. -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction 및 -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="366c7-288">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="366c7-289">입력</span><span class="sxs-lookup"><span data-stu-id="366c7-289">Inputs</span></span>
<span data-ttu-id="366c7-290">입력 형식은 cmdlet으로 파이프할 수 있는 개체의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-290">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="366c7-291">출력</span><span class="sxs-lookup"><span data-stu-id="366c7-291">Outputs</span></span>
<span data-ttu-id="366c7-292">출력 형식은 cmdlet이 내보내는 개체의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-292">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="366c7-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="366c7-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="366c7-294">미디어 서비스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="366c7-295">구문</span><span class="sxs-lookup"><span data-stu-id="366c7-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="366c7-296">매개 변수</span><span class="sxs-lookup"><span data-stu-id="366c7-296">Parameters</span></span>
<span data-ttu-id="366c7-297">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="366c7-298">이 미디어 서비스가 속하는 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-298">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="366c7-299">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-299">Aliases</span></span> | <span data-ttu-id="366c7-300">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-301">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-301">Required?</span></span> |<span data-ttu-id="366c7-302">true</span><span class="sxs-lookup"><span data-stu-id="366c7-302">true</span></span> |
| <span data-ttu-id="366c7-303">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-303">Position?</span></span> |<span data-ttu-id="366c7-304">0</span><span class="sxs-lookup"><span data-stu-id="366c7-304">0</span></span> |
| <span data-ttu-id="366c7-305">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-305">Default value</span></span> |<span data-ttu-id="366c7-306">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-306">none</span></span> |
| <span data-ttu-id="366c7-307">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-307">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-308">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-309">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-309">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-310">false</span><span class="sxs-lookup"><span data-stu-id="366c7-310">false</span></span> |

<span data-ttu-id="366c7-311">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="366c7-312">미디어 서비스의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-312">Specifies the name of the media service.</span></span>

| <span data-ttu-id="366c7-313">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-313">Aliases</span></span> | <span data-ttu-id="366c7-314">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-315">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-315">Required?</span></span> |<span data-ttu-id="366c7-316">true</span><span class="sxs-lookup"><span data-stu-id="366c7-316">true</span></span> |
| <span data-ttu-id="366c7-317">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-317">Position?</span></span> |<span data-ttu-id="366c7-318">2</span><span class="sxs-lookup"><span data-stu-id="366c7-318">2</span></span> |
| <span data-ttu-id="366c7-319">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-319">Default value</span></span> |<span data-ttu-id="366c7-320">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-320">None</span></span> |
| <span data-ttu-id="366c7-321">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-321">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-322">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-323">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-323">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-324">False</span><span class="sxs-lookup"><span data-stu-id="366c7-324">False</span></span> |

<span data-ttu-id="366c7-325">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="366c7-326">이 cmdlet 일반 매개 변수를 지원합니다. -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction 및 -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="366c7-326">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="366c7-327">입력</span><span class="sxs-lookup"><span data-stu-id="366c7-327">Inputs</span></span>
<span data-ttu-id="366c7-328">입력 형식은 cmdlet으로 파이프할 수 있는 개체의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-328">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="366c7-329">출력</span><span class="sxs-lookup"><span data-stu-id="366c7-329">Outputs</span></span>
<span data-ttu-id="366c7-330">출력 형식은 cmdlet이 내보내는 개체의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-330">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="366c7-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="366c7-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="366c7-332">지정된 이름으로 리소스 그룹 또는 미디어 서비스에 있는 모든 미디어 서비스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="366c7-333">구문</span><span class="sxs-lookup"><span data-stu-id="366c7-333">Syntax</span></span>
<span data-ttu-id="366c7-334">ParameterSet: ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="366c7-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="366c7-335">ParameterSet: AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="366c7-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="366c7-336">매개 변수</span><span class="sxs-lookup"><span data-stu-id="366c7-336">Parameters</span></span>
<span data-ttu-id="366c7-337">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="366c7-338">이 미디어 서비스가 속하는 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-338">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="366c7-339">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-339">Aliases</span></span> | <span data-ttu-id="366c7-340">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-341">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-341">Required?</span></span> |<span data-ttu-id="366c7-342">true</span><span class="sxs-lookup"><span data-stu-id="366c7-342">true</span></span> |
| <span data-ttu-id="366c7-343">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-343">Position?</span></span> |<span data-ttu-id="366c7-344">0</span><span class="sxs-lookup"><span data-stu-id="366c7-344">0</span></span> |
| <span data-ttu-id="366c7-345">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-345">Default value</span></span> |<span data-ttu-id="366c7-346">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-346">none</span></span> |
| <span data-ttu-id="366c7-347">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-347">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-348">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-349">매개 변수 집합 이름</span><span class="sxs-lookup"><span data-stu-id="366c7-349">Parameter set name</span></span> |<span data-ttu-id="366c7-350">ResourceGroupParameterSet, AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="366c7-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="366c7-351">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-351">Accept wildcard characters?</span></span>   <span data-ttu-id="366c7-352">false</span><span class="sxs-lookup"><span data-stu-id="366c7-352">false</span></span>

<span data-ttu-id="366c7-353">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="366c7-354">미디어 서비스의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-354">Specifies the name of the media service.</span></span>

| <span data-ttu-id="366c7-355">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-355">Aliases</span></span> | <span data-ttu-id="366c7-356">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-357">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-357">Required?</span></span> |<span data-ttu-id="366c7-358">true</span><span class="sxs-lookup"><span data-stu-id="366c7-358">true</span></span> |
| <span data-ttu-id="366c7-359">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-359">Position?</span></span> |<span data-ttu-id="366c7-360">1</span><span class="sxs-lookup"><span data-stu-id="366c7-360">1</span></span> |
| <span data-ttu-id="366c7-361">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-361">Default value</span></span> |<span data-ttu-id="366c7-362">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-362">none</span></span> |
| <span data-ttu-id="366c7-363">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-363">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-364">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-365">매개 변수 집합 이름</span><span class="sxs-lookup"><span data-stu-id="366c7-365">Parameter set name</span></span> |<span data-ttu-id="366c7-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="366c7-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="366c7-367">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-367">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-368">false</span><span class="sxs-lookup"><span data-stu-id="366c7-368">false</span></span> |

<span data-ttu-id="366c7-369">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="366c7-370">이 cmdlet 일반 매개 변수를 지원합니다. -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction 및 -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="366c7-370">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="366c7-371">입력</span><span class="sxs-lookup"><span data-stu-id="366c7-371">Inputs</span></span>
<span data-ttu-id="366c7-372">입력 형식은 cmdlet으로 파이프할 수 있는 개체의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-372">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="366c7-373">출력</span><span class="sxs-lookup"><span data-stu-id="366c7-373">Outputs</span></span>
<span data-ttu-id="366c7-374">출력 형식은 cmdlet이 내보내는 개체의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-374">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="366c7-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="366c7-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="366c7-376">미디어 서비스의 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="366c7-377">구문</span><span class="sxs-lookup"><span data-stu-id="366c7-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="366c7-378">매개 변수</span><span class="sxs-lookup"><span data-stu-id="366c7-378">Parameters</span></span>
<span data-ttu-id="366c7-379">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="366c7-380">이 미디어 서비스가 속하는 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-380">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="366c7-381">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-381">Aliases</span></span> | <span data-ttu-id="366c7-382">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-383">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-383">Required?</span></span> |<span data-ttu-id="366c7-384">true</span><span class="sxs-lookup"><span data-stu-id="366c7-384">true</span></span> |
| <span data-ttu-id="366c7-385">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-385">Position?</span></span> |<span data-ttu-id="366c7-386">0</span><span class="sxs-lookup"><span data-stu-id="366c7-386">0</span></span> |
| <span data-ttu-id="366c7-387">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-387">Default value</span></span> |<span data-ttu-id="366c7-388">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-388">none</span></span> |
| <span data-ttu-id="366c7-389">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-389">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-390">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-391">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-391">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-392">false</span><span class="sxs-lookup"><span data-stu-id="366c7-392">false</span></span> |

<span data-ttu-id="366c7-393">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="366c7-394">미디어 서비스의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-394">Specifies the name of the media service.</span></span>

| <span data-ttu-id="366c7-395">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-395">Aliases</span></span> | <span data-ttu-id="366c7-396">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-397">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-397">Required?</span></span> |<span data-ttu-id="366c7-398">true</span><span class="sxs-lookup"><span data-stu-id="366c7-398">true</span></span> |
| <span data-ttu-id="366c7-399">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-399">Position?</span></span> |<span data-ttu-id="366c7-400">1</span><span class="sxs-lookup"><span data-stu-id="366c7-400">1</span></span> |
| <span data-ttu-id="366c7-401">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-401">Default value</span></span> |<span data-ttu-id="366c7-402">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-402">none</span></span> |
| <span data-ttu-id="366c7-403">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-403">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-404">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-405">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-405">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-406">false</span><span class="sxs-lookup"><span data-stu-id="366c7-406">false</span></span> |

<span data-ttu-id="366c7-407">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="366c7-408">이 cmdlet 일반 매개 변수를 지원합니다. -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction 및 -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="366c7-408">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="366c7-409">입력</span><span class="sxs-lookup"><span data-stu-id="366c7-409">Inputs</span></span>
<span data-ttu-id="366c7-410">입력 형식은 cmdlet으로 파이프할 수 있는 개체의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-410">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="366c7-411">출력</span><span class="sxs-lookup"><span data-stu-id="366c7-411">Outputs</span></span>
<span data-ttu-id="366c7-412">출력 형식은 cmdlet이 내보내는 개체의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-412">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="366c7-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="366c7-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="366c7-414">미디어 서비스의 기본 또는 보조 키를 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="366c7-415">구문</span><span class="sxs-lookup"><span data-stu-id="366c7-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="366c7-416">매개 변수</span><span class="sxs-lookup"><span data-stu-id="366c7-416">Parameters</span></span>
<span data-ttu-id="366c7-417">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="366c7-418">이 미디어 서비스가 속하는 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-418">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="366c7-419">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-419">Aliases</span></span> | <span data-ttu-id="366c7-420">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-421">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-421">Required?</span></span> |<span data-ttu-id="366c7-422">true</span><span class="sxs-lookup"><span data-stu-id="366c7-422">true</span></span> |
| <span data-ttu-id="366c7-423">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-423">Position?</span></span> |<span data-ttu-id="366c7-424">0</span><span class="sxs-lookup"><span data-stu-id="366c7-424">0</span></span> |
| <span data-ttu-id="366c7-425">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-425">Default value</span></span> |<span data-ttu-id="366c7-426">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-426">none</span></span> |
| <span data-ttu-id="366c7-427">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-427">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-428">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-429">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-429">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-430">false</span><span class="sxs-lookup"><span data-stu-id="366c7-430">false</span></span> |

<span data-ttu-id="366c7-431">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="366c7-432">미디어 서비스의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-432">Specifies the name of the media service.</span></span>

| <span data-ttu-id="366c7-433">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-433">Aliases</span></span> | <span data-ttu-id="366c7-434">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-435">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-435">Required?</span></span> |<span data-ttu-id="366c7-436">true</span><span class="sxs-lookup"><span data-stu-id="366c7-436">true</span></span> |
| <span data-ttu-id="366c7-437">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-437">Position?</span></span> |<span data-ttu-id="366c7-438">1</span><span class="sxs-lookup"><span data-stu-id="366c7-438">1</span></span> |
| <span data-ttu-id="366c7-439">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-439">Default value</span></span> |<span data-ttu-id="366c7-440">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-440">none</span></span> |
| <span data-ttu-id="366c7-441">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-441">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-442">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-443">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-443">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-444">false</span><span class="sxs-lookup"><span data-stu-id="366c7-444">false</span></span> |

<span data-ttu-id="366c7-445">**-KeyType &lt;KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="366c7-446">미디어 서비스의 키 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-446">Specifies the key type of the media service.</span></span>

* <span data-ttu-id="366c7-447">기본 또는 보조</span><span class="sxs-lookup"><span data-stu-id="366c7-447">Primary or Secondary</span></span>

| <span data-ttu-id="366c7-448">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-448">Aliases</span></span> | <span data-ttu-id="366c7-449">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-450">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-450">Required?</span></span> |<span data-ttu-id="366c7-451">true</span><span class="sxs-lookup"><span data-stu-id="366c7-451">true</span></span> |
| <span data-ttu-id="366c7-452">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-452">Position?</span></span> |<span data-ttu-id="366c7-453">2</span><span class="sxs-lookup"><span data-stu-id="366c7-453">2</span></span> |
| <span data-ttu-id="366c7-454">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-454">Default value</span></span> |<span data-ttu-id="366c7-455">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-455">none</span></span> |
| <span data-ttu-id="366c7-456">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-456">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-457">false</span><span class="sxs-lookup"><span data-stu-id="366c7-457">false</span></span> |
| <span data-ttu-id="366c7-458">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-458">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-459">false</span><span class="sxs-lookup"><span data-stu-id="366c7-459">false</span></span> |

<span data-ttu-id="366c7-460">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="366c7-461">이 cmdlet 일반 매개 변수를 지원합니다. -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction 및 -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="366c7-461">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="366c7-462">입력</span><span class="sxs-lookup"><span data-stu-id="366c7-462">Inputs</span></span>
<span data-ttu-id="366c7-463">입력 형식은 cmdlet으로 파이프할 수 있는 개체의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-463">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="366c7-464">출력</span><span class="sxs-lookup"><span data-stu-id="366c7-464">Outputs</span></span>
<span data-ttu-id="366c7-465">출력 형식은 cmdlet이 내보내는 개체의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-465">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="366c7-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="366c7-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="366c7-467">미디어 서비스와 연결된 저장소 계정에 대한 저장소 계정 키를 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-467">Synchronizes storage account keys for a storage account associated with the media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="366c7-468">구문</span><span class="sxs-lookup"><span data-stu-id="366c7-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="366c7-469">매개 변수</span><span class="sxs-lookup"><span data-stu-id="366c7-469">Parameters</span></span>
<span data-ttu-id="366c7-470">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="366c7-471">이 미디어 서비스가 속하는 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-471">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="366c7-472">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-472">Aliases</span></span> | <span data-ttu-id="366c7-473">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-474">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-474">Required?</span></span> |<span data-ttu-id="366c7-475">true</span><span class="sxs-lookup"><span data-stu-id="366c7-475">true</span></span> |
| <span data-ttu-id="366c7-476">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-476">Position?</span></span> |<span data-ttu-id="366c7-477">0</span><span class="sxs-lookup"><span data-stu-id="366c7-477">0</span></span> |
| <span data-ttu-id="366c7-478">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-478">Default value</span></span> |<span data-ttu-id="366c7-479">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-479">none</span></span> |
| <span data-ttu-id="366c7-480">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-480">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-481">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-482">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-482">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-483">false</span><span class="sxs-lookup"><span data-stu-id="366c7-483">false</span></span> |

<span data-ttu-id="366c7-484">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="366c7-485">미디어 서비스의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-485">Specifies the name of the media service.</span></span>

| <span data-ttu-id="366c7-486">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-486">Aliases</span></span> | <span data-ttu-id="366c7-487">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-488">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-488">Required?</span></span> |<span data-ttu-id="366c7-489">true</span><span class="sxs-lookup"><span data-stu-id="366c7-489">true</span></span> |
| <span data-ttu-id="366c7-490">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-490">Position?</span></span> |<span data-ttu-id="366c7-491">1</span><span class="sxs-lookup"><span data-stu-id="366c7-491">1</span></span> |
| <span data-ttu-id="366c7-492">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-492">Default value</span></span> |<span data-ttu-id="366c7-493">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-493">none</span></span> |
| <span data-ttu-id="366c7-494">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-494">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-495">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-496">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-496">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-497">false</span><span class="sxs-lookup"><span data-stu-id="366c7-497">false</span></span> |

<span data-ttu-id="366c7-498">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="366c7-499">미디어 서비스와 연결된 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-499">Specifies the storage account associated with the media service.</span></span>

| <span data-ttu-id="366c7-500">Aliases</span><span class="sxs-lookup"><span data-stu-id="366c7-500">Aliases</span></span> | <span data-ttu-id="366c7-501">Id</span><span class="sxs-lookup"><span data-stu-id="366c7-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="366c7-502">Required?</span><span class="sxs-lookup"><span data-stu-id="366c7-502">Required?</span></span> |<span data-ttu-id="366c7-503">true</span><span class="sxs-lookup"><span data-stu-id="366c7-503">true</span></span> |
| <span data-ttu-id="366c7-504">Position?</span><span class="sxs-lookup"><span data-stu-id="366c7-504">Position?</span></span> |<span data-ttu-id="366c7-505">2</span><span class="sxs-lookup"><span data-stu-id="366c7-505">2</span></span> |
| <span data-ttu-id="366c7-506">기본값</span><span class="sxs-lookup"><span data-stu-id="366c7-506">Default value</span></span> |<span data-ttu-id="366c7-507">없음</span><span class="sxs-lookup"><span data-stu-id="366c7-507">none</span></span> |
| <span data-ttu-id="366c7-508">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="366c7-508">Accept pipeline input?</span></span> |<span data-ttu-id="366c7-509">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="366c7-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="366c7-510">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="366c7-510">Accept wildcard characters?</span></span> |<span data-ttu-id="366c7-511">false</span><span class="sxs-lookup"><span data-stu-id="366c7-511">false</span></span> |

<span data-ttu-id="366c7-512">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="366c7-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="366c7-513">이 cmdlet 일반 매개 변수를 지원합니다. -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction 및 -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="366c7-513">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="366c7-514">입력</span><span class="sxs-lookup"><span data-stu-id="366c7-514">Inputs</span></span>
<span data-ttu-id="366c7-515">입력 형식은 cmdlet으로 파이프할 수 있는 개체의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-515">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="366c7-516">출력</span><span class="sxs-lookup"><span data-stu-id="366c7-516">Outputs</span></span>
<span data-ttu-id="366c7-517">출력 형식은 cmdlet이 내보내는 개체의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="366c7-517">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="366c7-518">다음 단계</span><span class="sxs-lookup"><span data-stu-id="366c7-518">Next step</span></span>
<span data-ttu-id="366c7-519">미디어 서비스 학습 경로를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="366c7-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="366c7-520">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="366c7-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

