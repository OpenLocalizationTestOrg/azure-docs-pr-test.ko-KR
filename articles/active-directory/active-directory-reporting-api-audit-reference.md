---
title: "aaaAzure Active Directory 감사 API 참조 | Microsoft Docs"
description: "Tooget은 hello Azure Active Directory 감사 API로 시작 하는 방법"
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
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="7bd69-103">Azure Active Directory 감사 API 참조</span><span class="sxs-lookup"><span data-stu-id="7bd69-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="7bd69-104">이 항목은 Azure Active Directory hello에 대 한 항목 컬렉션의 일부 API를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="7bd69-105">Azure AD 보고 하면 있도록 API 코드 또는 관련된 도구를 사용 하 여 tooaccess 감사 데이터 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-105">Azure AD reporting provides you with an API that enables you tooaccess audit data using code or related tools.</span></span>
<span data-ttu-id="7bd69-106">이 항목의 hello 범위는 tooprovide hello에 대 한 참조 정보는 **API 감사**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-106">hello scope of this topic is tooprovide you with reference information about hello **audit API**.</span></span>

<span data-ttu-id="7bd69-107">다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7bd69-107">See:</span></span>

* <span data-ttu-id="7bd69-108">자세한 개념 정보는 [감사 로그](active-directory-reporting-azure-portal.md#activity-reports)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7bd69-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="7bd69-109">[Hello Azure Active Directory 보고 API 시작](active-directory-reporting-api-getting-started.md) hello 보고 API에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


<span data-ttu-id="7bd69-110">관련 작업:</span><span class="sxs-lookup"><span data-stu-id="7bd69-110">For:</span></span>

- <span data-ttu-id="7bd69-111">질문과 대답(FAQ)은 [FAQ](active-directory-reporting-faq.md)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="7bd69-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="7bd69-112">문제는 [지원 티켓을 파일로 저장하세요](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="7bd69-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-hello-data"></a><span data-ttu-id="7bd69-113">Hello 데이터에 액세스할 수 있는 사용자?</span><span class="sxs-lookup"><span data-stu-id="7bd69-113">Who can access hello data?</span></span>
* <span data-ttu-id="7bd69-114">Hello 보안 판독기 또는 보안 관리자 역할의 사용자</span><span class="sxs-lookup"><span data-stu-id="7bd69-114">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="7bd69-115">전역 관리자</span><span class="sxs-lookup"><span data-stu-id="7bd69-115">Global Admins</span></span>
* <span data-ttu-id="7bd69-116">권한 부여 tooaccess hello API를 모든 앱 (앱 권한 부여 가능 설치 전역 관리자의 사용 권한을 기반만)</span><span class="sxs-lookup"><span data-stu-id="7bd69-116">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bd69-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7bd69-117">Prerequisites</span></span>
<span data-ttu-id="7bd69-118">Hello Reporting API를 통해 보고이 순서 tooaccess에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-118">In order tooaccess this report through hello Reporting API, you must have:</span></span>

* <span data-ttu-id="7bd69-119">[Azure Active Directory 무료 이상 버전](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="7bd69-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="7bd69-120">완료 된 hello [필수 구성 요소 tooaccess hello Azure AD 보고 API](active-directory-reporting-api-prerequisites.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-120">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="7bd69-121">Hello API 액세스</span><span class="sxs-lookup"><span data-stu-id="7bd69-121">Accessing hello API</span></span>
<span data-ttu-id="7bd69-122">Hello를 통해이 API를 액세스 하거나 [그래프 탐색기](https://graphexplorer2.cloudapp.net) 프로그래밍 방식으로 사용 하거나, 예를 들어 PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7bd69-122">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="7bd69-123">순서 대로 PowerShell toocorrectly 해석 AAD Graph REST 호출에 사용 된 hello OData 필터 구문에 대 한 사용 해야 hello 억음 악센트 기호 (즉,: 억음 악센트 기호) 문자 너무 "문자는 이스케이프 처리할" hello $.</span><span class="sxs-lookup"><span data-stu-id="7bd69-123">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="7bd69-124">hello 억음 악센트 문자 역할을 [PowerShell의 이스케이프 문자](https://technet.microsoft.com/library/hh847755.aspx), PowerShell toodo hello $ 문자를 해석 하는 리터럴 허용 하 고 PowerShell 변수 이름으로 혼동 하지 않도록 (예: $filter).</span><span class="sxs-lookup"><span data-stu-id="7bd69-124">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="7bd69-125">이 항목의 포커스를 hello hello 그래프 탐색기 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-125">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="7bd69-126">PowerShell 예제는 이 [PowerShell 스크립트](active-directory-reporting-api-audit-samples.md#powershell-script)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7bd69-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="7bd69-127">API 끝점</span><span class="sxs-lookup"><span data-stu-id="7bd69-127">API Endpoint</span></span>
<span data-ttu-id="7bd69-128">다음 URI는 hello를 사용 하 여이 API에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-128">You can access this API using hello following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="7bd69-129">Hello hello Azure AD 감사 API (OData 페이지 매김을 사용)에서 반환 된 레코드 수에 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-129">There is no limit on hello number of records returned by hello Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="7bd69-130">데이터 보고에서 보존 제한은 [보존 정책 보고](active-directory-reporting-retention.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="7bd69-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="7bd69-131">이 호출 일괄 처리로 hello 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-131">This call returns hello data in batches.</span></span> <span data-ttu-id="7bd69-132">각 배치에는 최대 1000개 레코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="7bd69-133">tooget hello의 다음 일괄 처리 레코드를 사용 하 여 hello 다음 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-133">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="7bd69-134">반환 된 레코드의 첫 번째 집합 hello hello skiptoken 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-134">Get hello skiptoken information from hello first set of returned records.</span></span> <span data-ttu-id="7bd69-135">hello skip 토큰 hello 결과 집합의 hello 끝에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-135">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="7bd69-136">지원되는 필터</span><span class="sxs-lookup"><span data-stu-id="7bd69-136">Supported filters</span></span>
<span data-ttu-id="7bd69-137">Hello API에 의해 반환 된 레코드 수를 좁힐 수 있는 필터의 양식에서.</span><span class="sxs-lookup"><span data-stu-id="7bd69-137">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="7bd69-138">로그인 API에 대 한 관련된 데이터를 필터에 따라 hello 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-138">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="7bd69-139">**$top =\<반환 된 레코드 toobe 수가\>**  -toolimit hello 반환 된 레코드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-139">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="7bd69-140">이 작업은 비용이 많이 드는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-140">This is an expensive operation.</span></span> <span data-ttu-id="7bd69-141">개체의 tooreturn 수천을 원하는 경우이 필터를 사용 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-141">You should not use this filter if you want tooreturn thousands of objects.</span></span>     
* <span data-ttu-id="7bd69-142">**$filter =\<필터 문을\>**  -toospecify hello 별로 지원 되는 필터 필드, 중요 한 레코드의 hello 종류</span><span class="sxs-lookup"><span data-stu-id="7bd69-142">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="7bd69-143">지원되는 필터 필드 및 연산자</span><span class="sxs-lookup"><span data-stu-id="7bd69-143">Supported filter fields and operators</span></span>
<span data-ttu-id="7bd69-144">toospecify hello 유형 중요 한 레코드를 하나 또는 hello 필터 필드를 다음의 조합을 포함할 수 있는 필터 문을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-144">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="7bd69-145">[activityDate](#activitydate) - 날짜 또는 날짜 범위를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="7bd69-146">[범주](#category) -toofilter에서 원하는 hello 범주를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-146">[category](#category) - defines hello category you want toofilter on.</span></span>
* <span data-ttu-id="7bd69-147">[activityStatus](#activitystatus) -작업의 hello 상태 정의</span><span class="sxs-lookup"><span data-stu-id="7bd69-147">[activityStatus](#activitystatus) - defines hello status of an activity</span></span>
* <span data-ttu-id="7bd69-148">[activityType](#activitytype) -hello 유형의 활동을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-148">[activityType](#activitytype)  - defines hello type of an activity</span></span>
* <span data-ttu-id="7bd69-149">[활동](#activity) -문자열로 hello 활동을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-149">[activity](#activity) - defines hello activity as string</span></span>  
* <span data-ttu-id="7bd69-150">[행위자/이름](#actorname) -hello 행위자의 이름 형식으로의 hello 행위자를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-150">[actor/name](#actorname) -   defines hello actor in form of hello actor's name</span></span>
* <span data-ttu-id="7bd69-151">[행위자/objectid](#actorobjectid) -hello 행위자 ID의 형태로 hello 행위자를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-151">[actor/objectid](#actorobjectid) - defines hello actor in form of hello actor's ID</span></span>   
* <span data-ttu-id="7bd69-152">[행위자/upn](#actorupn) -hello 행위자의 사용자 계정 이름 (UPN)의 형태로 hello 행위자를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-152">[actor/upn](#actorupn)  - defines hello actor in form of hello actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="7bd69-153">[대상/이름](#targetname) -hello 행위자의 이름 형식으로의 hello 대상 정의</span><span class="sxs-lookup"><span data-stu-id="7bd69-153">[target/name](#targetname)  - defines hello target in form of hello actor's name</span></span>
* <span data-ttu-id="7bd69-154">[대상/objectid](#targetobjectid) -hello 대상 ID의 형태로 hello 대상을 정의</span><span class="sxs-lookup"><span data-stu-id="7bd69-154">[target/objectid](#targetobjectid) - defines hello target in form of hello target's ID</span></span>  
* <span data-ttu-id="7bd69-155">[대상/upn](#targetupn) -hello 행위자의 사용자 계정 이름 (UPN)의 형태로 hello 행위자를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-155">[target/upn](#targetupn) - defines hello actor in form of hello actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="7bd69-156">activityDate</span><span class="sxs-lookup"><span data-stu-id="7bd69-156">activityDate</span></span>
<span data-ttu-id="7bd69-157">**지원되는 연산자**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="7bd69-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="7bd69-158">**예제**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="7bd69-159">**참고**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-159">**Notes**:</span></span>

<span data-ttu-id="7bd69-160">datetime는 UTC 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="7bd69-161">카테고리</span><span class="sxs-lookup"><span data-stu-id="7bd69-161">category</span></span>

<span data-ttu-id="7bd69-162">**지원되는 값**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-162">**Supported values**:</span></span>

| <span data-ttu-id="7bd69-163">Category</span><span class="sxs-lookup"><span data-stu-id="7bd69-163">Category</span></span>                         | <span data-ttu-id="7bd69-164">값</span><span class="sxs-lookup"><span data-stu-id="7bd69-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="7bd69-165">핵심 디렉터리</span><span class="sxs-lookup"><span data-stu-id="7bd69-165">Core Directory</span></span>                   | <span data-ttu-id="7bd69-166">디렉터리</span><span class="sxs-lookup"><span data-stu-id="7bd69-166">Directory</span></span> |
| <span data-ttu-id="7bd69-167">셀프 서비스 암호 관리</span><span class="sxs-lookup"><span data-stu-id="7bd69-167">Self-service Password Management</span></span> | <span data-ttu-id="7bd69-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="7bd69-168">SSPR</span></span>      |
| <span data-ttu-id="7bd69-169">셀프 서비스 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="7bd69-169">Self-service Group Management</span></span>    | <span data-ttu-id="7bd69-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="7bd69-170">SSGM</span></span>      |
| <span data-ttu-id="7bd69-171">계정 프로비전</span><span class="sxs-lookup"><span data-stu-id="7bd69-171">Account Provisioning</span></span>             | <span data-ttu-id="7bd69-172">동기화</span><span class="sxs-lookup"><span data-stu-id="7bd69-172">Sync</span></span>      |
| <span data-ttu-id="7bd69-173">자동화된 암호 롤오버</span><span class="sxs-lookup"><span data-stu-id="7bd69-173">Automated Password Rollover</span></span>      | <span data-ttu-id="7bd69-174">자동화된 암호 롤오버</span><span class="sxs-lookup"><span data-stu-id="7bd69-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="7bd69-175">ID 보호</span><span class="sxs-lookup"><span data-stu-id="7bd69-175">Identity Protection</span></span>              | <span data-ttu-id="7bd69-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="7bd69-176">IdentityProtection</span></span> |
| <span data-ttu-id="7bd69-177">사용자 초대</span><span class="sxs-lookup"><span data-stu-id="7bd69-177">Invited Users</span></span>                    | <span data-ttu-id="7bd69-178">사용자 초대</span><span class="sxs-lookup"><span data-stu-id="7bd69-178">Invited Users</span></span> |
| <span data-ttu-id="7bd69-179">MIM 서비스</span><span class="sxs-lookup"><span data-stu-id="7bd69-179">MIM Service</span></span>                      | <span data-ttu-id="7bd69-180">MIM 서비스</span><span class="sxs-lookup"><span data-stu-id="7bd69-180">MIM Service</span></span> |



<span data-ttu-id="7bd69-181">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="7bd69-181">**Supported operators**: eq</span></span>

<span data-ttu-id="7bd69-182">**예제**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="7bd69-183">activityStatus</span><span class="sxs-lookup"><span data-stu-id="7bd69-183">activityStatus</span></span>

<span data-ttu-id="7bd69-184">**지원되는 값**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-184">**Supported values**:</span></span>

| <span data-ttu-id="7bd69-185">활동 상태</span><span class="sxs-lookup"><span data-stu-id="7bd69-185">Activity Status</span></span> | <span data-ttu-id="7bd69-186">값</span><span class="sxs-lookup"><span data-stu-id="7bd69-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="7bd69-187">성공</span><span class="sxs-lookup"><span data-stu-id="7bd69-187">Success</span></span>         | <span data-ttu-id="7bd69-188">0</span><span class="sxs-lookup"><span data-stu-id="7bd69-188">0</span></span>     |
| <span data-ttu-id="7bd69-189">실패</span><span class="sxs-lookup"><span data-stu-id="7bd69-189">Failure</span></span>         | <span data-ttu-id="7bd69-190">- 1</span><span class="sxs-lookup"><span data-stu-id="7bd69-190">- 1</span></span>   |

<span data-ttu-id="7bd69-191">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="7bd69-191">**Supported operators**: eq</span></span>

<span data-ttu-id="7bd69-192">**예제**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="7bd69-193">activityType</span><span class="sxs-lookup"><span data-stu-id="7bd69-193">activityType</span></span>
<span data-ttu-id="7bd69-194">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="7bd69-194">**Supported operators**: eq</span></span>

<span data-ttu-id="7bd69-195">**예제**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="7bd69-196">**참고**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-196">**Notes**:</span></span>

<span data-ttu-id="7bd69-197">대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="7bd69-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="7bd69-198">활동</span><span class="sxs-lookup"><span data-stu-id="7bd69-198">activity</span></span>
<span data-ttu-id="7bd69-199">**연산자 지원**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="7bd69-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="7bd69-200">**예제**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="7bd69-201">**참고**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-201">**Notes**:</span></span>

<span data-ttu-id="7bd69-202">대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="7bd69-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="7bd69-203">행위자/이름</span><span class="sxs-lookup"><span data-stu-id="7bd69-203">actor/name</span></span>
<span data-ttu-id="7bd69-204">**연산자 지원**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="7bd69-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="7bd69-205">**예제**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="7bd69-206">**참고**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-206">**Notes**:</span></span>

<span data-ttu-id="7bd69-207">대/소문자 구분하지 않음</span><span class="sxs-lookup"><span data-stu-id="7bd69-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="7bd69-208">행위자/objectid</span><span class="sxs-lookup"><span data-stu-id="7bd69-208">actor/objectId</span></span>
<span data-ttu-id="7bd69-209">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="7bd69-209">**Supported operators**: eq</span></span>

<span data-ttu-id="7bd69-210">**예제**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="7bd69-211">대상/이름</span><span class="sxs-lookup"><span data-stu-id="7bd69-211">target/name</span></span>
<span data-ttu-id="7bd69-212">**연산자 지원**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="7bd69-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="7bd69-213">**예제**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="7bd69-214">**참고**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-214">**Notes**:</span></span>

<span data-ttu-id="7bd69-215">대/소문자 구분하지 않음</span><span class="sxs-lookup"><span data-stu-id="7bd69-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="7bd69-216">대상/upn</span><span class="sxs-lookup"><span data-stu-id="7bd69-216">target/upn</span></span>
<span data-ttu-id="7bd69-217">**연산자 지원**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="7bd69-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="7bd69-218">**예제**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="7bd69-219">**참고**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-219">**Notes**:</span></span>

* <span data-ttu-id="7bd69-220">대/소문자 구분하지 않음</span><span class="sxs-lookup"><span data-stu-id="7bd69-220">Case-insensitive</span></span>
* <span data-ttu-id="7bd69-221">Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity 쿼리할 때 필요한 tooadd hello 전체 네임 스페이스</span><span class="sxs-lookup"><span data-stu-id="7bd69-221">You need tooadd hello full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="7bd69-222">대상/objectid</span><span class="sxs-lookup"><span data-stu-id="7bd69-222">target/objectId</span></span>
<span data-ttu-id="7bd69-223">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="7bd69-223">**Supported operators**: eq</span></span>

<span data-ttu-id="7bd69-224">**예제**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="7bd69-225">행위자/upn</span><span class="sxs-lookup"><span data-stu-id="7bd69-225">actor/upn</span></span>
<span data-ttu-id="7bd69-226">**연산자 지원**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="7bd69-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="7bd69-227">**예제**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="7bd69-228">**참고**:</span><span class="sxs-lookup"><span data-stu-id="7bd69-228">**Notes**:</span></span>

* <span data-ttu-id="7bd69-229">대/소문자 구분하지 않음</span><span class="sxs-lookup"><span data-stu-id="7bd69-229">Case-insensitive</span></span> 
* <span data-ttu-id="7bd69-230">Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity 쿼리할 때 필요한 tooadd hello 전체 네임 스페이스</span><span class="sxs-lookup"><span data-stu-id="7bd69-230">You need tooadd hello full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="7bd69-231">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7bd69-231">Next Steps</span></span>
* <span data-ttu-id="7bd69-232">필터링 된 시스템 작업에 대 한 toosee 예제 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="7bd69-232">Do you want toosee examples for filtered system activities?</span></span> <span data-ttu-id="7bd69-233">체크 아웃 hello [Azure Active Directory 감사 API 예제](active-directory-reporting-api-audit-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-233">Check out hello [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="7bd69-234">Tooknow hello Azure AD 보고 API에 대 한 자세한 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="7bd69-234">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="7bd69-235">참조 [hello Azure Active Directory 보고 API 시작](active-directory-reporting-api-getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bd69-235">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

