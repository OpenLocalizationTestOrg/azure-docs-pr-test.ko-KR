---
title: "Azure Active Directory 감사 API 참조 | Microsoft Docs"
description: "Azure Active Directory 감사 API를 시작하는 방법"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 573e940c5390e7b990d889681eb37b73c5b253d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="b794c-103">Azure Active Directory 감사 API 참조</span><span class="sxs-lookup"><span data-stu-id="b794c-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="b794c-104">이 항목은 Azure Active Directory Reporting API에 대한 항목 컬렉션의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="b794c-105">Azure AD Reporting은 코드 또는 관련된 도구를 사용하여 감사 데이터에 액세스할 수 있는 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-105">Azure AD reporting provides you with an API that enables you to access audit data using code or related tools.</span></span>
<span data-ttu-id="b794c-106">이 항목은 **감사 API**에 대한 참조 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-106">The scope of this topic is to provide you with reference information about the **audit API**.</span></span>

<span data-ttu-id="b794c-107">다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b794c-107">See:</span></span>

* <span data-ttu-id="b794c-108">자세한 개념 정보는 [감사 로그](active-directory-reporting-azure-portal.md#activity-reports)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b794c-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="b794c-109">[Azure Active Directory Reporting API 시작](active-directory-reporting-api-getting-started.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b794c-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


<span data-ttu-id="b794c-110">관련 작업:</span><span class="sxs-lookup"><span data-stu-id="b794c-110">For:</span></span>

- <span data-ttu-id="b794c-111">질문과 대답(FAQ)은 [FAQ](active-directory-reporting-faq.md)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="b794c-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="b794c-112">문제는 [지원 티켓을 파일로 저장하세요](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="b794c-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-the-data"></a><span data-ttu-id="b794c-113">데이터에 액세스할 수 있는 사용자는 누구인가요?</span><span class="sxs-lookup"><span data-stu-id="b794c-113">Who can access the data?</span></span>
* <span data-ttu-id="b794c-114">보안 관리 또는 보안 판독기 역할의 사용자</span><span class="sxs-lookup"><span data-stu-id="b794c-114">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="b794c-115">전역 관리자</span><span class="sxs-lookup"><span data-stu-id="b794c-115">Global Admins</span></span>
* <span data-ttu-id="b794c-116">API에 액세스하는 인증이 있는 모든 앱(전역 관리자의 사용 권한에 따라 앱 권한 부여를 설정할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="b794c-116">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b794c-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b794c-117">Prerequisites</span></span>
<span data-ttu-id="b794c-118">Reporting API를 통해 이 보고서에 액세스하려면 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-118">In order to access this report through the Reporting API, you must have:</span></span>

* <span data-ttu-id="b794c-119">[Azure Active Directory 무료 이상 버전](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="b794c-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="b794c-120">[Azure AD Reporting API에 액세스하기 위한 필수 구성 요소](active-directory-reporting-api-prerequisites.md)를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-120">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-the-api"></a><span data-ttu-id="b794c-121">API에 액세스</span><span class="sxs-lookup"><span data-stu-id="b794c-121">Accessing the API</span></span>
<span data-ttu-id="b794c-122">예를 들어 [Graph Explorer](https://graphexplorer2.cloudapp.net) 를 통해 또는 프로그래밍 방식으로 PowerShell을 사용하여 이 API에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-122">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="b794c-123">PowerShell이 AAD Graph REST 호출에 사용된 OData 필터 구문을 올바르게 해석하기 위해 '(억음 부호) 기호를 사용하여 $ 기호를 "이스케이프"해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-123">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span></span> <span data-ttu-id="b794c-124">' 기호는 [PowerShell의 이스케이프 문자](https://technet.microsoft.com/library/hh847755.aspx)로 사용되어 PowerShell에서 $ 기호의 리터럴 해석을 수행하고 PowerShell 변수 이름(예: $filter)으로 혼동하지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-124">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="b794c-125">이 항목은 Graph Explorer에 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-125">The focus of this topic is on the Graph Explorer.</span></span> <span data-ttu-id="b794c-126">PowerShell 예제는 이 [PowerShell 스크립트](active-directory-reporting-api-audit-samples.md#powershell-script)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b794c-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="b794c-127">API 끝점</span><span class="sxs-lookup"><span data-stu-id="b794c-127">API Endpoint</span></span>
<span data-ttu-id="b794c-128">다음 URI를 사용하여 이 API에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-128">You can access this API using the following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="b794c-129">Azure AD 감사 API에서 (OData 페이지 매김을 사용하여) 반환되는 레코드의 수가 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-129">There is no limit on the number of records returned by the Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="b794c-130">데이터 보고에서 보존 제한은 [보존 정책 보고](active-directory-reporting-retention.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="b794c-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="b794c-131">이 호출은 배치에서 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-131">This call returns the data in batches.</span></span> <span data-ttu-id="b794c-132">각 배치에는 최대 1000개 레코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="b794c-133">레코드의 다음 배치를 가져오려면 [다음] 링크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-133">To get the next batch of records, use the Next link.</span></span> <span data-ttu-id="b794c-134">첫 번째 반환되는 레코드의 집합에서 skiptoken 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-134">Get the skiptoken information from the first set of returned records.</span></span> <span data-ttu-id="b794c-135">건너뛰기 토큰은 결과 집합의 끝에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-135">The skip token will be at the end of the result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="b794c-136">지원되는 필터</span><span class="sxs-lookup"><span data-stu-id="b794c-136">Supported filters</span></span>
<span data-ttu-id="b794c-137">필터의 형태로 API 호출에서 반환되는 레코드의 수를 좁힐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-137">You can narrow down the number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="b794c-138">로그인 API 관련 데이터의 경우 다음 필터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-138">For sign-in API related data, the following filters are supported:</span></span>

* <span data-ttu-id="b794c-139">**$top=\<반환될 레코드의 수\>** - 반환된 레코드의 수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-139">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span></span> <span data-ttu-id="b794c-140">이 작업은 비용이 많이 드는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-140">This is an expensive operation.</span></span> <span data-ttu-id="b794c-141">수천 개의 개체를 반환하려는 경우 이 필터를 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-141">You should not use this filter if you want to return thousands of objects.</span></span>     
* <span data-ttu-id="b794c-142">**$filter=\<필터 문\>** - 지원되는 필터 필드를 기반으로 원하는 레코드 종류를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-142">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="b794c-143">지원되는 필터 필드 및 연산자</span><span class="sxs-lookup"><span data-stu-id="b794c-143">Supported filter fields and operators</span></span>
<span data-ttu-id="b794c-144">원하는 레코드의 종류를 지정하려면 다음 필터 필드 중 하나 또는 조합을 포함할 수 있는 필터 문을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-144">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span></span>

* <span data-ttu-id="b794c-145">[activityDate](#activitydate) - 날짜 또는 날짜 범위를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="b794c-146">[범주](#category) - 필터링 기준으로 사용할 범주를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-146">[category](#category) - defines the category you want to filter on.</span></span>
* <span data-ttu-id="b794c-147">[activityStatus](#activitystatus) - 활동의 상태를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-147">[activityStatus](#activitystatus) - defines the status of an activity</span></span>
* <span data-ttu-id="b794c-148">[activityType](#activitytype) - 동작의 종류를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-148">[activityType](#activitytype)  - defines the type of an activity</span></span>
* <span data-ttu-id="b794c-149">[활동](#activity) - 활동을 문자열로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-149">[activity](#activity) - defines the activity as string</span></span>  
* <span data-ttu-id="b794c-150">[행위자/이름](#actorname) - 행위자 이름의 형태로 행위자를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-150">[actor/name](#actorname) -   defines the actor in form of the actor's name</span></span>
* <span data-ttu-id="b794c-151">[행위자/objectid](#actorobjectid) - 행위자 ID의 형태로 행위자를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-151">[actor/objectid](#actorobjectid) - defines the actor in form of the actor's ID</span></span>   
* <span data-ttu-id="b794c-152">[행위자/upn](#actorupn) - 행위자 UPN(사용자 계정 이름)의 형태로 행위자를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-152">[actor/upn](#actorupn)  - defines the actor in form of the actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="b794c-153">[대상/이름](#targetname) - 행위자 이름의 형태로 대상을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-153">[target/name](#targetname)  - defines the target in form of the actor's name</span></span>
* <span data-ttu-id="b794c-154">[대상/objectid](#targetobjectid) - 행위자 ID의 형태로 대상을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-154">[target/objectid](#targetobjectid) - defines the target in form of the target's ID</span></span>  
* <span data-ttu-id="b794c-155">[대상/upn](#targetupn) - 행위자 UPN(사용자 계정 이름)의 형태로 행위자를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-155">[target/upn](#targetupn) - defines the actor in form of the actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="b794c-156">activityDate</span><span class="sxs-lookup"><span data-stu-id="b794c-156">activityDate</span></span>
<span data-ttu-id="b794c-157">**지원되는 연산자**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="b794c-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="b794c-158">**예제**:</span><span class="sxs-lookup"><span data-stu-id="b794c-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="b794c-159">**참고**:</span><span class="sxs-lookup"><span data-stu-id="b794c-159">**Notes**:</span></span>

<span data-ttu-id="b794c-160">datetime는 UTC 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="b794c-161">카테고리</span><span class="sxs-lookup"><span data-stu-id="b794c-161">category</span></span>

<span data-ttu-id="b794c-162">**지원되는 값**:</span><span class="sxs-lookup"><span data-stu-id="b794c-162">**Supported values**:</span></span>

| <span data-ttu-id="b794c-163">Category</span><span class="sxs-lookup"><span data-stu-id="b794c-163">Category</span></span>                         | <span data-ttu-id="b794c-164">값</span><span class="sxs-lookup"><span data-stu-id="b794c-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="b794c-165">핵심 디렉터리</span><span class="sxs-lookup"><span data-stu-id="b794c-165">Core Directory</span></span>                   | <span data-ttu-id="b794c-166">디렉터리</span><span class="sxs-lookup"><span data-stu-id="b794c-166">Directory</span></span> |
| <span data-ttu-id="b794c-167">셀프 서비스 암호 관리</span><span class="sxs-lookup"><span data-stu-id="b794c-167">Self-service Password Management</span></span> | <span data-ttu-id="b794c-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="b794c-168">SSPR</span></span>      |
| <span data-ttu-id="b794c-169">셀프 서비스 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="b794c-169">Self-service Group Management</span></span>    | <span data-ttu-id="b794c-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="b794c-170">SSGM</span></span>      |
| <span data-ttu-id="b794c-171">계정 프로비전</span><span class="sxs-lookup"><span data-stu-id="b794c-171">Account Provisioning</span></span>             | <span data-ttu-id="b794c-172">동기화</span><span class="sxs-lookup"><span data-stu-id="b794c-172">Sync</span></span>      |
| <span data-ttu-id="b794c-173">자동화된 암호 롤오버</span><span class="sxs-lookup"><span data-stu-id="b794c-173">Automated Password Rollover</span></span>      | <span data-ttu-id="b794c-174">자동화된 암호 롤오버</span><span class="sxs-lookup"><span data-stu-id="b794c-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="b794c-175">ID 보호</span><span class="sxs-lookup"><span data-stu-id="b794c-175">Identity Protection</span></span>              | <span data-ttu-id="b794c-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="b794c-176">IdentityProtection</span></span> |
| <span data-ttu-id="b794c-177">사용자 초대</span><span class="sxs-lookup"><span data-stu-id="b794c-177">Invited Users</span></span>                    | <span data-ttu-id="b794c-178">사용자 초대</span><span class="sxs-lookup"><span data-stu-id="b794c-178">Invited Users</span></span> |
| <span data-ttu-id="b794c-179">MIM 서비스</span><span class="sxs-lookup"><span data-stu-id="b794c-179">MIM Service</span></span>                      | <span data-ttu-id="b794c-180">MIM 서비스</span><span class="sxs-lookup"><span data-stu-id="b794c-180">MIM Service</span></span> |



<span data-ttu-id="b794c-181">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="b794c-181">**Supported operators**: eq</span></span>

<span data-ttu-id="b794c-182">**예제**:</span><span class="sxs-lookup"><span data-stu-id="b794c-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="b794c-183">activityStatus</span><span class="sxs-lookup"><span data-stu-id="b794c-183">activityStatus</span></span>

<span data-ttu-id="b794c-184">**지원되는 값**:</span><span class="sxs-lookup"><span data-stu-id="b794c-184">**Supported values**:</span></span>

| <span data-ttu-id="b794c-185">활동 상태</span><span class="sxs-lookup"><span data-stu-id="b794c-185">Activity Status</span></span> | <span data-ttu-id="b794c-186">값</span><span class="sxs-lookup"><span data-stu-id="b794c-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="b794c-187">성공</span><span class="sxs-lookup"><span data-stu-id="b794c-187">Success</span></span>         | <span data-ttu-id="b794c-188">0</span><span class="sxs-lookup"><span data-stu-id="b794c-188">0</span></span>     |
| <span data-ttu-id="b794c-189">실패</span><span class="sxs-lookup"><span data-stu-id="b794c-189">Failure</span></span>         | <span data-ttu-id="b794c-190">- 1</span><span class="sxs-lookup"><span data-stu-id="b794c-190">- 1</span></span>   |

<span data-ttu-id="b794c-191">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="b794c-191">**Supported operators**: eq</span></span>

<span data-ttu-id="b794c-192">**예제**:</span><span class="sxs-lookup"><span data-stu-id="b794c-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="b794c-193">activityType</span><span class="sxs-lookup"><span data-stu-id="b794c-193">activityType</span></span>
<span data-ttu-id="b794c-194">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="b794c-194">**Supported operators**: eq</span></span>

<span data-ttu-id="b794c-195">**예제**:</span><span class="sxs-lookup"><span data-stu-id="b794c-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="b794c-196">**참고**:</span><span class="sxs-lookup"><span data-stu-id="b794c-196">**Notes**:</span></span>

<span data-ttu-id="b794c-197">대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="b794c-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="b794c-198">활동</span><span class="sxs-lookup"><span data-stu-id="b794c-198">activity</span></span>
<span data-ttu-id="b794c-199">**연산자 지원**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="b794c-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="b794c-200">**예제**:</span><span class="sxs-lookup"><span data-stu-id="b794c-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="b794c-201">**참고**:</span><span class="sxs-lookup"><span data-stu-id="b794c-201">**Notes**:</span></span>

<span data-ttu-id="b794c-202">대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="b794c-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="b794c-203">행위자/이름</span><span class="sxs-lookup"><span data-stu-id="b794c-203">actor/name</span></span>
<span data-ttu-id="b794c-204">**연산자 지원**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="b794c-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="b794c-205">**예제**:</span><span class="sxs-lookup"><span data-stu-id="b794c-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="b794c-206">**참고**:</span><span class="sxs-lookup"><span data-stu-id="b794c-206">**Notes**:</span></span>

<span data-ttu-id="b794c-207">대/소문자 구분하지 않음</span><span class="sxs-lookup"><span data-stu-id="b794c-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="b794c-208">행위자/objectid</span><span class="sxs-lookup"><span data-stu-id="b794c-208">actor/objectId</span></span>
<span data-ttu-id="b794c-209">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="b794c-209">**Supported operators**: eq</span></span>

<span data-ttu-id="b794c-210">**예제**:</span><span class="sxs-lookup"><span data-stu-id="b794c-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="b794c-211">대상/이름</span><span class="sxs-lookup"><span data-stu-id="b794c-211">target/name</span></span>
<span data-ttu-id="b794c-212">**연산자 지원**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="b794c-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="b794c-213">**예제**:</span><span class="sxs-lookup"><span data-stu-id="b794c-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="b794c-214">**참고**:</span><span class="sxs-lookup"><span data-stu-id="b794c-214">**Notes**:</span></span>

<span data-ttu-id="b794c-215">대/소문자 구분하지 않음</span><span class="sxs-lookup"><span data-stu-id="b794c-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="b794c-216">대상/upn</span><span class="sxs-lookup"><span data-stu-id="b794c-216">target/upn</span></span>
<span data-ttu-id="b794c-217">**연산자 지원**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="b794c-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="b794c-218">**예제**:</span><span class="sxs-lookup"><span data-stu-id="b794c-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="b794c-219">**참고**:</span><span class="sxs-lookup"><span data-stu-id="b794c-219">**Notes**:</span></span>

* <span data-ttu-id="b794c-220">대/소문자 구분하지 않음</span><span class="sxs-lookup"><span data-stu-id="b794c-220">Case-insensitive</span></span>
* <span data-ttu-id="b794c-221">Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity를 쿼리할 때 전체 네임스페이스를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-221">You need to add the full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="b794c-222">대상/objectid</span><span class="sxs-lookup"><span data-stu-id="b794c-222">target/objectId</span></span>
<span data-ttu-id="b794c-223">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="b794c-223">**Supported operators**: eq</span></span>

<span data-ttu-id="b794c-224">**예제**:</span><span class="sxs-lookup"><span data-stu-id="b794c-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="b794c-225">행위자/upn</span><span class="sxs-lookup"><span data-stu-id="b794c-225">actor/upn</span></span>
<span data-ttu-id="b794c-226">**연산자 지원**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="b794c-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="b794c-227">**예제**:</span><span class="sxs-lookup"><span data-stu-id="b794c-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="b794c-228">**참고**:</span><span class="sxs-lookup"><span data-stu-id="b794c-228">**Notes**:</span></span>

* <span data-ttu-id="b794c-229">대/소문자 구분하지 않음</span><span class="sxs-lookup"><span data-stu-id="b794c-229">Case-insensitive</span></span> 
* <span data-ttu-id="b794c-230">Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity를 쿼리할 때 전체 네임스페이스를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b794c-230">You need to add the full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="b794c-231">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b794c-231">Next Steps</span></span>
* <span data-ttu-id="b794c-232">필터링된 시스템 활동에 대한 예제를 참조하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="b794c-232">Do you want to see examples for filtered system activities?</span></span> <span data-ttu-id="b794c-233">[Azure Active Directory 감사 API 샘플](active-directory-reporting-api-audit-samples.md)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="b794c-233">Check out the [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="b794c-234">Azure AD Reporting API에 대해 자세히 살펴보시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="b794c-234">Do you want to know more about the Azure AD reporting API?</span></span> <span data-ttu-id="b794c-235">[Azure Active Directory Reporting API 시작](active-directory-reporting-api-getting-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b794c-235">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

