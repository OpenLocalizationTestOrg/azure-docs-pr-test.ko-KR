---
title: "aaaManage PowerShell 사용한 Azure 미디어 서비스 계정"
description: "PowerShell cmdlet과 toomanage Azure 미디어 서비스 계정 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="a8563-103">PowerShell을 사용하여 Azure 미디어 서비스 계정 관리</span><span class="sxs-lookup"><span data-stu-id="a8563-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a8563-104">포털</span><span class="sxs-lookup"><span data-stu-id="a8563-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="a8563-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8563-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="a8563-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="a8563-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="a8563-107">toobe 수 toocreate Azure 미디어 서비스 계정, Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-107">toobe able toocreate an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="a8563-108">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a8563-109">자세한 내용은 <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure 무료 평가판</a>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8563-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="a8563-110">개요</span><span class="sxs-lookup"><span data-stu-id="a8563-110">Overview</span></span>
<span data-ttu-id="a8563-111">이 문서 hello Azure 리소스 관리자 framework에서 hello Azure PowerShell cmdlet에 대 한 Azure 미디어 서비스 AMS ()를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-111">This article lists hello Azure PowerShell cmdlets for Azure Media Services (AMS) in hello Azure Resource Manager framework.</span></span> <span data-ttu-id="a8563-112">hello에 hello cmdlet 존재 **Microsoft.Azure.Commands.Media** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-112">hello cmdlets exist in hello **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="a8563-113">버전</span><span class="sxs-lookup"><span data-stu-id="a8563-113">Versions</span></span>
<span data-ttu-id="a8563-114">**ApiVersion**: "2015-10-01"</span><span class="sxs-lookup"><span data-stu-id="a8563-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="a8563-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="a8563-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="a8563-116">미디어 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="a8563-117">구문</span><span class="sxs-lookup"><span data-stu-id="a8563-117">Syntax</span></span>
<span data-ttu-id="a8563-118">매개 변수 집합: StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="a8563-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="a8563-119">매개 변수 집합: StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="a8563-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="a8563-120">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a8563-120">Parameters</span></span>
<span data-ttu-id="a8563-121">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="a8563-122">이 미디어 서비스 속한 hello 리소스 그룹 toowhich hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-122">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="a8563-123">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-123">Aliases</span></span> | <span data-ttu-id="a8563-124">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-125">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-125">Required?</span></span> |<span data-ttu-id="a8563-126">true</span><span class="sxs-lookup"><span data-stu-id="a8563-126">true</span></span> |
| <span data-ttu-id="a8563-127">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-127">Position?</span></span> |<span data-ttu-id="a8563-128">0</span><span class="sxs-lookup"><span data-stu-id="a8563-128">0</span></span> |
| <span data-ttu-id="a8563-129">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-129">Default value</span></span> |<span data-ttu-id="a8563-130">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-130">none</span></span> |
| <span data-ttu-id="a8563-131">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-131">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-132">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-133">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-133">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-134">false</span><span class="sxs-lookup"><span data-stu-id="a8563-134">false</span></span> |

<span data-ttu-id="a8563-135">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="a8563-136">Hello hello 미디어 서비스 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-136">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="a8563-137">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-137">Aliases</span></span> | <span data-ttu-id="a8563-138">Name</span><span class="sxs-lookup"><span data-stu-id="a8563-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-139">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-139">Required?</span></span> |<span data-ttu-id="a8563-140">true</span><span class="sxs-lookup"><span data-stu-id="a8563-140">true</span></span> |
| <span data-ttu-id="a8563-141">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-141">Position?</span></span> |<span data-ttu-id="a8563-142">1</span><span class="sxs-lookup"><span data-stu-id="a8563-142">1</span></span> |
| <span data-ttu-id="a8563-143">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-143">Default value</span></span> |<span data-ttu-id="a8563-144">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-144">none</span></span> |
| <span data-ttu-id="a8563-145">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-145">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-146">false</span><span class="sxs-lookup"><span data-stu-id="a8563-146">false</span></span> |
| <span data-ttu-id="a8563-147">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-147">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-148">false</span><span class="sxs-lookup"><span data-stu-id="a8563-148">false</span></span> |

<span data-ttu-id="a8563-149">**-Location &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="a8563-150">Hello 미디어 서비스의 hello 리소스 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-150">Specifies hello resource location of hello media service.</span></span>

| <span data-ttu-id="a8563-151">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-151">Aliases</span></span> | <span data-ttu-id="a8563-152">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-153">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-153">Required?</span></span> |<span data-ttu-id="a8563-154">true</span><span class="sxs-lookup"><span data-stu-id="a8563-154">true</span></span> |
| <span data-ttu-id="a8563-155">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-155">Position?</span></span> |<span data-ttu-id="a8563-156">2</span><span class="sxs-lookup"><span data-stu-id="a8563-156">2</span></span> |
| <span data-ttu-id="a8563-157">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-157">Default value</span></span> |<span data-ttu-id="a8563-158">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-158">none</span></span> |
| <span data-ttu-id="a8563-159">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-159">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-160">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-161">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-161">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-162">false</span><span class="sxs-lookup"><span data-stu-id="a8563-162">false</span></span> |

<span data-ttu-id="a8563-163">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="a8563-164">Hello 미디어 서비스와 연결 된 기본 저장소 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-164">Specifies a primary storage account that associated with hello media service.</span></span>

* <span data-ttu-id="a8563-165">새 저장소 계정 (hello 리소스 관리자 API를 사용 하 여 만든)만 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-165">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="a8563-166">hello 저장소 계정이 있어야 하며가 hello hello 미디어 서비스와 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-166">hello storage account must exist and has hello same location with hello media service.</span></span>

| <span data-ttu-id="a8563-167">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-167">Aliases</span></span> | <span data-ttu-id="a8563-168">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-169">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-169">Required?</span></span> |<span data-ttu-id="a8563-170">true</span><span class="sxs-lookup"><span data-stu-id="a8563-170">true</span></span> |
| <span data-ttu-id="a8563-171">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-171">Position?</span></span> |<span data-ttu-id="a8563-172">3</span><span class="sxs-lookup"><span data-stu-id="a8563-172">3</span></span> |
| <span data-ttu-id="a8563-173">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-173">Default value</span></span> |<span data-ttu-id="a8563-174">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-174">none</span></span> |
| <span data-ttu-id="a8563-175">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-175">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-176">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-177">매개 변수 집합 이름</span><span class="sxs-lookup"><span data-stu-id="a8563-177">Parameter set name</span></span> |<span data-ttu-id="a8563-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="a8563-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="a8563-179">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-179">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-180">false</span><span class="sxs-lookup"><span data-stu-id="a8563-180">false</span></span> |

<span data-ttu-id="a8563-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="a8563-182">Hello 미디어 서비스와 연결 된 저장소 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-182">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="a8563-183">새 저장소 계정 (hello 리소스 관리자 API를 사용 하 여 만든)만 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-183">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="a8563-184">hello 저장소 계정이 있어야 하며가 hello hello 미디어 서비스와 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-184">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="a8563-185">단 하나의 저장소 계정 만을 기본으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="a8563-186">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-186">Aliases</span></span> | <span data-ttu-id="a8563-187">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-188">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-188">Required?</span></span> |<span data-ttu-id="a8563-189">true</span><span class="sxs-lookup"><span data-stu-id="a8563-189">true</span></span> |
| <span data-ttu-id="a8563-190">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-190">Position?</span></span> |<span data-ttu-id="a8563-191">3</span><span class="sxs-lookup"><span data-stu-id="a8563-191">3</span></span> |
| <span data-ttu-id="a8563-192">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-192">Default value</span></span> |<span data-ttu-id="a8563-193">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-193">none</span></span> |
| <span data-ttu-id="a8563-194">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-194">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-195">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-196">매개 변수 집합 이름</span><span class="sxs-lookup"><span data-stu-id="a8563-196">Parameter set name</span></span> |<span data-ttu-id="a8563-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="a8563-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="a8563-198">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-198">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-199">false</span><span class="sxs-lookup"><span data-stu-id="a8563-199">false</span></span> |

<span data-ttu-id="a8563-200">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="a8563-201">Hello 미디어 서비스와 관련 된 hello 태그의 해시 테이블을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-201">Specifies a hash table of hello tags that are associated with hello media service.</span></span>

* <span data-ttu-id="a8563-202">예: @{"tag1"="value1";" tag2 "=: value2"을 (를)</span><span class="sxs-lookup"><span data-stu-id="a8563-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="a8563-203">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-203">Aliases</span></span> | <span data-ttu-id="a8563-204">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-205">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-205">Required?</span></span> |<span data-ttu-id="a8563-206">false</span><span class="sxs-lookup"><span data-stu-id="a8563-206">false</span></span> |
| <span data-ttu-id="a8563-207">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-207">Position?</span></span> |<span data-ttu-id="a8563-208">named</span><span class="sxs-lookup"><span data-stu-id="a8563-208">named</span></span> |
| <span data-ttu-id="a8563-209">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-209">Default value</span></span> |<span data-ttu-id="a8563-210">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-210">none</span></span> |
| <span data-ttu-id="a8563-211">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-211">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-212">false</span><span class="sxs-lookup"><span data-stu-id="a8563-212">false</span></span> |
| <span data-ttu-id="a8563-213">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-213">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-214">false</span><span class="sxs-lookup"><span data-stu-id="a8563-214">false</span></span> |

<span data-ttu-id="a8563-215">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="a8563-216">이 cmdlet은 공통 매개 변수 hello:-디버그,-ErrorAction,-ErrorVariable,-InformationAction,-InformationVariable,-OutVariable,-OutBuffer,-PipelineVariable,-Verbose,-WarningAction 및-warningvariable을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-216">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="a8563-217">입력</span><span class="sxs-lookup"><span data-stu-id="a8563-217">Inputs</span></span>
<span data-ttu-id="a8563-218">hello 입력된 형식은 toohello cmdlet에 파이프할 수 있음을 hello hello 유형의 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-218">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="a8563-219">outputs</span><span class="sxs-lookup"><span data-stu-id="a8563-219">Outputs</span></span>
<span data-ttu-id="a8563-220">hello 출력 유형은 cmdlet hello hello 개체 유형의 hello를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-220">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="a8563-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="a8563-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="a8563-222">미디어 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="a8563-223">구문</span><span class="sxs-lookup"><span data-stu-id="a8563-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="a8563-224">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a8563-224">Parameters</span></span>
<span data-ttu-id="a8563-225">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="a8563-226">이 미디어 서비스 속한 hello 리소스 그룹 toowhich hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-226">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="a8563-227">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-227">Aliases</span></span> | <span data-ttu-id="a8563-228">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-229">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-229">Required?</span></span> |<span data-ttu-id="a8563-230">true</span><span class="sxs-lookup"><span data-stu-id="a8563-230">true</span></span> |
| <span data-ttu-id="a8563-231">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-231">Position?</span></span> |<span data-ttu-id="a8563-232">0</span><span class="sxs-lookup"><span data-stu-id="a8563-232">0</span></span> |
| <span data-ttu-id="a8563-233">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-233">Default Value</span></span> |<span data-ttu-id="a8563-234">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-234">none</span></span> |
| <span data-ttu-id="a8563-235">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="a8563-236">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-237">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-237">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-238">false</span><span class="sxs-lookup"><span data-stu-id="a8563-238">false</span></span> |

<span data-ttu-id="a8563-239">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="a8563-240">Hello hello 미디어 서비스 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-240">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="a8563-241">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-241">Aliases</span></span> | <span data-ttu-id="a8563-242">Name</span><span class="sxs-lookup"><span data-stu-id="a8563-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-243">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-243">Required?</span></span> |<span data-ttu-id="a8563-244">true</span><span class="sxs-lookup"><span data-stu-id="a8563-244">True</span></span> |
| <span data-ttu-id="a8563-245">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-245">Position?</span></span> |<span data-ttu-id="a8563-246">1</span><span class="sxs-lookup"><span data-stu-id="a8563-246">1</span></span> |
| <span data-ttu-id="a8563-247">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-247">Default value</span></span> |<span data-ttu-id="a8563-248">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-248">None</span></span> |
| <span data-ttu-id="a8563-249">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-249">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-250">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-251">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-251">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-252">False</span><span class="sxs-lookup"><span data-stu-id="a8563-252">False</span></span> |

<span data-ttu-id="a8563-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="a8563-254">Hello 미디어 서비스와 연결 된 저장소 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-254">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="a8563-255">새 저장소 계정 (hello 리소스 관리자 API를 사용 하 여 만든)만 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-255">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="a8563-256">hello 저장소 계정이 있어야 하며가 hello hello 미디어 서비스와 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-256">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="a8563-257">단 하나의 저장소 계정 만을 기본으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="a8563-258">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-258">Aliases</span></span> | <span data-ttu-id="a8563-259">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-260">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-260">Required?</span></span> |<span data-ttu-id="a8563-261">false</span><span class="sxs-lookup"><span data-stu-id="a8563-261">false</span></span> |
| <span data-ttu-id="a8563-262">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-262">Position?</span></span> |<span data-ttu-id="a8563-263">named</span><span class="sxs-lookup"><span data-stu-id="a8563-263">Named</span></span> |
| <span data-ttu-id="a8563-264">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-264">Default value</span></span> |<span data-ttu-id="a8563-265">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-265">none</span></span> |
| <span data-ttu-id="a8563-266">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-266">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-267">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-268">매개 변수 집합 이름</span><span class="sxs-lookup"><span data-stu-id="a8563-268">Parameter set name</span></span> |<span data-ttu-id="a8563-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="a8563-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="a8563-270">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-270">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-271">false</span><span class="sxs-lookup"><span data-stu-id="a8563-271">false</span></span> |

<span data-ttu-id="a8563-272">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="a8563-273">이 미디어 서비스와 관련 된 hello 태그의 해시 테이블을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-273">Specifies a hash table of hello tags that are associated with this media service.</span></span>

* <span data-ttu-id="a8563-274">hello 미디어 서비스와 관련 된 hello 태그 hello 고객이 지정 된 값으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-274">hello tags that are associated with hello media service are replaced with value specified by hello customer.</span></span>

| <span data-ttu-id="a8563-275">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-275">Aliases</span></span> | <span data-ttu-id="a8563-276">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-277">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-277">Required?</span></span> |<span data-ttu-id="a8563-278">false</span><span class="sxs-lookup"><span data-stu-id="a8563-278">False</span></span> |
| <span data-ttu-id="a8563-279">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-279">Position?</span></span> |<span data-ttu-id="a8563-280">named</span><span class="sxs-lookup"><span data-stu-id="a8563-280">Named</span></span> |
| <span data-ttu-id="a8563-281">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-281">Default value</span></span> |<span data-ttu-id="a8563-282">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-282">None</span></span> |
| <span data-ttu-id="a8563-283">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-283">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-284">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-285">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-285">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-286">false</span><span class="sxs-lookup"><span data-stu-id="a8563-286">false</span></span> |

<span data-ttu-id="a8563-287">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="a8563-288">이 cmdlet은 공통 매개 변수 hello:-디버그,-ErrorAction,-ErrorVariable,-InformationAction,-InformationVariable,-OutVariable,-OutBuffer,-PipelineVariable,-Verbose,-WarningAction 및-warningvariable을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-288">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="a8563-289">입력</span><span class="sxs-lookup"><span data-stu-id="a8563-289">Inputs</span></span>
<span data-ttu-id="a8563-290">hello 입력된 형식은 toohello cmdlet에 파이프할 수 있음을 hello hello 유형의 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-290">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="a8563-291">outputs</span><span class="sxs-lookup"><span data-stu-id="a8563-291">Outputs</span></span>
<span data-ttu-id="a8563-292">hello 출력 유형은 cmdlet hello hello 개체 유형의 hello를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-292">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="a8563-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="a8563-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="a8563-294">미디어 서비스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="a8563-295">구문</span><span class="sxs-lookup"><span data-stu-id="a8563-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="a8563-296">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a8563-296">Parameters</span></span>
<span data-ttu-id="a8563-297">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="a8563-298">이 미디어 서비스 속한 hello 리소스 그룹 toowhich hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-298">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="a8563-299">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-299">Aliases</span></span> | <span data-ttu-id="a8563-300">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-301">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-301">Required?</span></span> |<span data-ttu-id="a8563-302">true</span><span class="sxs-lookup"><span data-stu-id="a8563-302">true</span></span> |
| <span data-ttu-id="a8563-303">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-303">Position?</span></span> |<span data-ttu-id="a8563-304">0</span><span class="sxs-lookup"><span data-stu-id="a8563-304">0</span></span> |
| <span data-ttu-id="a8563-305">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-305">Default value</span></span> |<span data-ttu-id="a8563-306">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-306">none</span></span> |
| <span data-ttu-id="a8563-307">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-307">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-308">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-309">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-309">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-310">false</span><span class="sxs-lookup"><span data-stu-id="a8563-310">false</span></span> |

<span data-ttu-id="a8563-311">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="a8563-312">Hello hello 미디어 서비스 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-312">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="a8563-313">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-313">Aliases</span></span> | <span data-ttu-id="a8563-314">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-315">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-315">Required?</span></span> |<span data-ttu-id="a8563-316">true</span><span class="sxs-lookup"><span data-stu-id="a8563-316">true</span></span> |
| <span data-ttu-id="a8563-317">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-317">Position?</span></span> |<span data-ttu-id="a8563-318">2</span><span class="sxs-lookup"><span data-stu-id="a8563-318">2</span></span> |
| <span data-ttu-id="a8563-319">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-319">Default value</span></span> |<span data-ttu-id="a8563-320">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-320">None</span></span> |
| <span data-ttu-id="a8563-321">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-321">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-322">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-323">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-323">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-324">False</span><span class="sxs-lookup"><span data-stu-id="a8563-324">False</span></span> |

<span data-ttu-id="a8563-325">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="a8563-326">이 cmdlet은 공통 매개 변수 hello:-디버그,-ErrorAction,-ErrorVariable,-InformationAction,-InformationVariable,-OutVariable,-OutBuffer,-PipelineVariable,-Verbose,-WarningAction 및-warningvariable을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-326">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="a8563-327">입력</span><span class="sxs-lookup"><span data-stu-id="a8563-327">Inputs</span></span>
<span data-ttu-id="a8563-328">hello 입력된 형식은 toohello cmdlet에 파이프할 수 있음을 hello hello 유형의 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-328">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="a8563-329">outputs</span><span class="sxs-lookup"><span data-stu-id="a8563-329">Outputs</span></span>
<span data-ttu-id="a8563-330">hello 출력 유형은 cmdlet hello hello 개체 유형의 hello를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-330">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="a8563-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="a8563-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="a8563-332">지정된 이름으로 리소스 그룹 또는 미디어 서비스에 있는 모든 미디어 서비스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="a8563-333">구문</span><span class="sxs-lookup"><span data-stu-id="a8563-333">Syntax</span></span>
<span data-ttu-id="a8563-334">ParameterSet: ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="a8563-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="a8563-335">ParameterSet: AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="a8563-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="a8563-336">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a8563-336">Parameters</span></span>
<span data-ttu-id="a8563-337">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="a8563-338">이 미디어 서비스 속한 hello 리소스 그룹 toowhich hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-338">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="a8563-339">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-339">Aliases</span></span> | <span data-ttu-id="a8563-340">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-341">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-341">Required?</span></span> |<span data-ttu-id="a8563-342">true</span><span class="sxs-lookup"><span data-stu-id="a8563-342">true</span></span> |
| <span data-ttu-id="a8563-343">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-343">Position?</span></span> |<span data-ttu-id="a8563-344">0</span><span class="sxs-lookup"><span data-stu-id="a8563-344">0</span></span> |
| <span data-ttu-id="a8563-345">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-345">Default value</span></span> |<span data-ttu-id="a8563-346">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-346">none</span></span> |
| <span data-ttu-id="a8563-347">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-347">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-348">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-349">매개 변수 집합 이름</span><span class="sxs-lookup"><span data-stu-id="a8563-349">Parameter set name</span></span> |<span data-ttu-id="a8563-350">ResourceGroupParameterSet, AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="a8563-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="a8563-351">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-351">Accept wildcard characters?</span></span>   <span data-ttu-id="a8563-352">false</span><span class="sxs-lookup"><span data-stu-id="a8563-352">false</span></span>

<span data-ttu-id="a8563-353">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="a8563-354">Hello hello 미디어 서비스 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-354">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="a8563-355">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-355">Aliases</span></span> | <span data-ttu-id="a8563-356">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-357">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-357">Required?</span></span> |<span data-ttu-id="a8563-358">true</span><span class="sxs-lookup"><span data-stu-id="a8563-358">true</span></span> |
| <span data-ttu-id="a8563-359">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-359">Position?</span></span> |<span data-ttu-id="a8563-360">1</span><span class="sxs-lookup"><span data-stu-id="a8563-360">1</span></span> |
| <span data-ttu-id="a8563-361">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-361">Default value</span></span> |<span data-ttu-id="a8563-362">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-362">none</span></span> |
| <span data-ttu-id="a8563-363">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-363">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-364">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-365">매개 변수 집합 이름</span><span class="sxs-lookup"><span data-stu-id="a8563-365">Parameter set name</span></span> |<span data-ttu-id="a8563-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="a8563-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="a8563-367">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-367">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-368">false</span><span class="sxs-lookup"><span data-stu-id="a8563-368">false</span></span> |

<span data-ttu-id="a8563-369">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="a8563-370">이 cmdlet은 공통 매개 변수 hello:-디버그,-ErrorAction,-ErrorVariable,-InformationAction,-InformationVariable,-OutVariable,-OutBuffer,-PipelineVariable,-Verbose,-WarningAction 및-warningvariable을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-370">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="a8563-371">입력</span><span class="sxs-lookup"><span data-stu-id="a8563-371">Inputs</span></span>
<span data-ttu-id="a8563-372">hello 입력된 형식은 toohello cmdlet에 파이프할 수 있음을 hello hello 유형의 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-372">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="a8563-373">outputs</span><span class="sxs-lookup"><span data-stu-id="a8563-373">Outputs</span></span>
<span data-ttu-id="a8563-374">hello 출력 유형은 cmdlet hello hello 개체 유형의 hello를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-374">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="a8563-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="a8563-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="a8563-376">미디어 서비스의 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="a8563-377">구문</span><span class="sxs-lookup"><span data-stu-id="a8563-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="a8563-378">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a8563-378">Parameters</span></span>
<span data-ttu-id="a8563-379">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="a8563-380">이 미디어 서비스 속한 hello 리소스 그룹 toowhich hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-380">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="a8563-381">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-381">Aliases</span></span> | <span data-ttu-id="a8563-382">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-383">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-383">Required?</span></span> |<span data-ttu-id="a8563-384">true</span><span class="sxs-lookup"><span data-stu-id="a8563-384">true</span></span> |
| <span data-ttu-id="a8563-385">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-385">Position?</span></span> |<span data-ttu-id="a8563-386">0</span><span class="sxs-lookup"><span data-stu-id="a8563-386">0</span></span> |
| <span data-ttu-id="a8563-387">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-387">Default value</span></span> |<span data-ttu-id="a8563-388">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-388">none</span></span> |
| <span data-ttu-id="a8563-389">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-389">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-390">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-391">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-391">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-392">false</span><span class="sxs-lookup"><span data-stu-id="a8563-392">false</span></span> |

<span data-ttu-id="a8563-393">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="a8563-394">Hello hello 미디어 서비스 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-394">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="a8563-395">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-395">Aliases</span></span> | <span data-ttu-id="a8563-396">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-397">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-397">Required?</span></span> |<span data-ttu-id="a8563-398">true</span><span class="sxs-lookup"><span data-stu-id="a8563-398">true</span></span> |
| <span data-ttu-id="a8563-399">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-399">Position?</span></span> |<span data-ttu-id="a8563-400">1</span><span class="sxs-lookup"><span data-stu-id="a8563-400">1</span></span> |
| <span data-ttu-id="a8563-401">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-401">Default value</span></span> |<span data-ttu-id="a8563-402">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-402">none</span></span> |
| <span data-ttu-id="a8563-403">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-403">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-404">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-405">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-405">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-406">false</span><span class="sxs-lookup"><span data-stu-id="a8563-406">false</span></span> |

<span data-ttu-id="a8563-407">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="a8563-408">이 cmdlet은 공통 매개 변수 hello:-디버그,-ErrorAction,-ErrorVariable,-InformationAction,-InformationVariable,-OutVariable,-OutBuffer,-PipelineVariable,-Verbose,-WarningAction 및-warningvariable을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-408">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="a8563-409">입력</span><span class="sxs-lookup"><span data-stu-id="a8563-409">Inputs</span></span>
<span data-ttu-id="a8563-410">hello 입력된 형식은 toohello cmdlet에 파이프할 수 있음을 hello hello 유형의 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-410">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="a8563-411">outputs</span><span class="sxs-lookup"><span data-stu-id="a8563-411">Outputs</span></span>
<span data-ttu-id="a8563-412">hello 출력 유형은 cmdlet hello hello 개체 유형의 hello를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-412">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="a8563-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="a8563-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="a8563-414">미디어 서비스의 기본 또는 보조 키를 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="a8563-415">구문</span><span class="sxs-lookup"><span data-stu-id="a8563-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="a8563-416">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a8563-416">Parameters</span></span>
<span data-ttu-id="a8563-417">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="a8563-418">이 미디어 서비스 속한 hello 리소스 그룹 toowhich hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-418">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="a8563-419">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-419">Aliases</span></span> | <span data-ttu-id="a8563-420">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-421">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-421">Required?</span></span> |<span data-ttu-id="a8563-422">true</span><span class="sxs-lookup"><span data-stu-id="a8563-422">true</span></span> |
| <span data-ttu-id="a8563-423">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-423">Position?</span></span> |<span data-ttu-id="a8563-424">0</span><span class="sxs-lookup"><span data-stu-id="a8563-424">0</span></span> |
| <span data-ttu-id="a8563-425">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-425">Default value</span></span> |<span data-ttu-id="a8563-426">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-426">none</span></span> |
| <span data-ttu-id="a8563-427">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-427">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-428">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-429">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-429">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-430">false</span><span class="sxs-lookup"><span data-stu-id="a8563-430">false</span></span> |

<span data-ttu-id="a8563-431">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="a8563-432">Hello hello 미디어 서비스 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-432">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="a8563-433">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-433">Aliases</span></span> | <span data-ttu-id="a8563-434">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-435">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-435">Required?</span></span> |<span data-ttu-id="a8563-436">true</span><span class="sxs-lookup"><span data-stu-id="a8563-436">true</span></span> |
| <span data-ttu-id="a8563-437">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-437">Position?</span></span> |<span data-ttu-id="a8563-438">1</span><span class="sxs-lookup"><span data-stu-id="a8563-438">1</span></span> |
| <span data-ttu-id="a8563-439">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-439">Default value</span></span> |<span data-ttu-id="a8563-440">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-440">none</span></span> |
| <span data-ttu-id="a8563-441">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-441">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-442">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-443">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-443">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-444">false</span><span class="sxs-lookup"><span data-stu-id="a8563-444">false</span></span> |

<span data-ttu-id="a8563-445">**-KeyType &lt;KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="a8563-446">Hello hello 미디어 서비스 키 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-446">Specifies hello key type of hello media service.</span></span>

* <span data-ttu-id="a8563-447">기본 또는 보조</span><span class="sxs-lookup"><span data-stu-id="a8563-447">Primary or Secondary</span></span>

| <span data-ttu-id="a8563-448">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-448">Aliases</span></span> | <span data-ttu-id="a8563-449">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-450">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-450">Required?</span></span> |<span data-ttu-id="a8563-451">true</span><span class="sxs-lookup"><span data-stu-id="a8563-451">true</span></span> |
| <span data-ttu-id="a8563-452">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-452">Position?</span></span> |<span data-ttu-id="a8563-453">2</span><span class="sxs-lookup"><span data-stu-id="a8563-453">2</span></span> |
| <span data-ttu-id="a8563-454">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-454">Default value</span></span> |<span data-ttu-id="a8563-455">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-455">none</span></span> |
| <span data-ttu-id="a8563-456">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-456">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-457">false</span><span class="sxs-lookup"><span data-stu-id="a8563-457">false</span></span> |
| <span data-ttu-id="a8563-458">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-458">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-459">false</span><span class="sxs-lookup"><span data-stu-id="a8563-459">false</span></span> |

<span data-ttu-id="a8563-460">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="a8563-461">이 cmdlet은 공통 매개 변수 hello:-디버그,-ErrorAction,-ErrorVariable,-InformationAction,-InformationVariable,-OutVariable,-OutBuffer,-PipelineVariable,-Verbose,-WarningAction 및-warningvariable을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-461">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="a8563-462">입력</span><span class="sxs-lookup"><span data-stu-id="a8563-462">Inputs</span></span>
<span data-ttu-id="a8563-463">hello 입력된 형식은 toothe cmdlet에 파이프할 수 있음을 hello hello 유형의 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-463">hello input type is hello type of hello objects that you can pipe toothe cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="a8563-464">outputs</span><span class="sxs-lookup"><span data-stu-id="a8563-464">Outputs</span></span>
<span data-ttu-id="a8563-465">hello 출력 유형은 cmdlet hello hello 개체 유형의 hello를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-465">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="a8563-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="a8563-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="a8563-467">Hello 미디어 서비스와 연결 된 저장소 계정에 대 한 저장소 계정 키를 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-467">Synchronizes storage account keys for a storage account associated with hello media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="a8563-468">구문</span><span class="sxs-lookup"><span data-stu-id="a8563-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="a8563-469">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a8563-469">Parameters</span></span>
<span data-ttu-id="a8563-470">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="a8563-471">이 미디어 서비스 속한 hello 리소스 그룹 toowhich hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-471">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="a8563-472">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-472">Aliases</span></span> | <span data-ttu-id="a8563-473">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-474">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-474">Required?</span></span> |<span data-ttu-id="a8563-475">true</span><span class="sxs-lookup"><span data-stu-id="a8563-475">true</span></span> |
| <span data-ttu-id="a8563-476">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-476">Position?</span></span> |<span data-ttu-id="a8563-477">0</span><span class="sxs-lookup"><span data-stu-id="a8563-477">0</span></span> |
| <span data-ttu-id="a8563-478">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-478">Default value</span></span> |<span data-ttu-id="a8563-479">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-479">none</span></span> |
| <span data-ttu-id="a8563-480">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-480">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-481">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-482">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-482">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-483">false</span><span class="sxs-lookup"><span data-stu-id="a8563-483">false</span></span> |

<span data-ttu-id="a8563-484">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="a8563-485">Hello hello 미디어 서비스 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-485">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="a8563-486">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-486">Aliases</span></span> | <span data-ttu-id="a8563-487">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-488">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-488">Required?</span></span> |<span data-ttu-id="a8563-489">true</span><span class="sxs-lookup"><span data-stu-id="a8563-489">true</span></span> |
| <span data-ttu-id="a8563-490">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-490">Position?</span></span> |<span data-ttu-id="a8563-491">1</span><span class="sxs-lookup"><span data-stu-id="a8563-491">1</span></span> |
| <span data-ttu-id="a8563-492">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-492">Default value</span></span> |<span data-ttu-id="a8563-493">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-493">none</span></span> |
| <span data-ttu-id="a8563-494">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-494">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-495">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-496">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-496">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-497">false</span><span class="sxs-lookup"><span data-stu-id="a8563-497">false</span></span> |

<span data-ttu-id="a8563-498">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="a8563-499">Hello 미디어 서비스와 관련 된 hello 저장소 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-499">Specifies hello storage account associated with hello media service.</span></span>

| <span data-ttu-id="a8563-500">Aliases</span><span class="sxs-lookup"><span data-stu-id="a8563-500">Aliases</span></span> | <span data-ttu-id="a8563-501">Id</span><span class="sxs-lookup"><span data-stu-id="a8563-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="a8563-502">Required?</span><span class="sxs-lookup"><span data-stu-id="a8563-502">Required?</span></span> |<span data-ttu-id="a8563-503">true</span><span class="sxs-lookup"><span data-stu-id="a8563-503">true</span></span> |
| <span data-ttu-id="a8563-504">Position?</span><span class="sxs-lookup"><span data-stu-id="a8563-504">Position?</span></span> |<span data-ttu-id="a8563-505">2</span><span class="sxs-lookup"><span data-stu-id="a8563-505">2</span></span> |
| <span data-ttu-id="a8563-506">기본값</span><span class="sxs-lookup"><span data-stu-id="a8563-506">Default value</span></span> |<span data-ttu-id="a8563-507">없음</span><span class="sxs-lookup"><span data-stu-id="a8563-507">none</span></span> |
| <span data-ttu-id="a8563-508">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="a8563-508">Accept pipeline input?</span></span> |<span data-ttu-id="a8563-509">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="a8563-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="a8563-510">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="a8563-510">Accept wildcard characters?</span></span> |<span data-ttu-id="a8563-511">false</span><span class="sxs-lookup"><span data-stu-id="a8563-511">false</span></span> |

<span data-ttu-id="a8563-512">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="a8563-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="a8563-513">이 cmdlet은 공통 매개 변수 hello:-디버그,-ErrorAction,-ErrorVariable,-InformationAction,-InformationVariable,-OutVariable,-OutBuffer,-PipelineVariable,-Verbose,-WarningAction 및-warningvariable을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-513">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="a8563-514">입력</span><span class="sxs-lookup"><span data-stu-id="a8563-514">Inputs</span></span>
<span data-ttu-id="a8563-515">hello 입력된 형식은 toohello cmdlet에 파이프할 수 있음을 hello hello 유형의 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-515">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="a8563-516">outputs</span><span class="sxs-lookup"><span data-stu-id="a8563-516">Outputs</span></span>
<span data-ttu-id="a8563-517">hello 출력 유형은 cmdlet hello hello 개체 유형의 hello를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a8563-517">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="a8563-518">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a8563-518">Next step</span></span>
<span data-ttu-id="a8563-519">미디어 서비스 학습 경로를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="a8563-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a8563-520">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="a8563-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

