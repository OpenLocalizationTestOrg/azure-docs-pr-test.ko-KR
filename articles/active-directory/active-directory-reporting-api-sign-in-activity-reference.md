---
title: "aaaAzure Active Directory 로그인 활동 보고서 API 참조 | Microsoft Docs"
description: "Hello Azure Active Directory 로그인 활동 보고서 API에 대 한 참조"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 8123f308a291503f2c61ac5de26696806c6402ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a><span data-ttu-id="3ec46-103">Azure Active Directory 로그인 활동 보고서 API 참조</span><span class="sxs-lookup"><span data-stu-id="3ec46-103">Azure Active Directory sign-in activity report API reference</span></span>
<span data-ttu-id="3ec46-104">이 항목은 Azure Active Directory hello에 대 한 항목 컬렉션의 일부 API를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="3ec46-105">Azure AD 보고 하면 있도록 API 코드 또는 관련된 도구를 사용 하 여 tooaccess 로그인 활동 보고서 데이터 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity report data using code or related tools.</span></span>
<span data-ttu-id="3ec46-106">이 항목의 hello 범위는 tooprovide hello에 대 한 참조 정보는 **로그인 활동 보고서 API**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-106">hello scope of this topic is tooprovide you with reference information about hello **sign-in activity report API**.</span></span>

<span data-ttu-id="3ec46-107">다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ec46-107">See:</span></span>

* <span data-ttu-id="3ec46-108">[로그인 활동](active-directory-reporting-azure-portal.md#activity-reports) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ec46-108">[Sign-in activities](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="3ec46-109">[Hello Azure Active Directory 보고 API 시작](active-directory-reporting-api-getting-started.md) hello 보고 API에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="who-can-access-hello-api-data"></a><span data-ttu-id="3ec46-110">Hello API 데이터에 액세스할 수 있는 사용자?</span><span class="sxs-lookup"><span data-stu-id="3ec46-110">Who can access hello API data?</span></span>
* <span data-ttu-id="3ec46-111">사용자 및 서비스 사용자 역할 hello 보안 판독기 또는 보안 관리자 역할</span><span class="sxs-lookup"><span data-stu-id="3ec46-111">Users and Service Principals in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="3ec46-112">전역 관리자</span><span class="sxs-lookup"><span data-stu-id="3ec46-112">Global Admins</span></span>
* <span data-ttu-id="3ec46-113">권한 부여 tooaccess hello API를 모든 앱 (앱 권한 부여 가능 설치 전역 관리자의 사용 권한을 기반만)</span><span class="sxs-lookup"><span data-stu-id="3ec46-113">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

<span data-ttu-id="3ec46-114">응용 프로그램 tooaccess 보안 Api signin 이벤트와 같은 PowerShell tooadd hello 응용 프로그램 서비스 사용자 hello 보안 읽기 역할에 따라 사용 하 여 hello에 대 한 tooconfigure 액세스</span><span class="sxs-lookup"><span data-stu-id="3ec46-114">tooconfigure access for an application tooaccess security APIs such as signin events, use hello following PowerShell tooadd hello applications Service Principal into hello Security Reader role</span></span>

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a><span data-ttu-id="3ec46-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3ec46-115">Prerequisites</span></span>
<span data-ttu-id="3ec46-116">이 통해 보고 tooaccess hello 보고 API 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-116">tooaccess this report through hello reporting API, you must have:</span></span>

* <span data-ttu-id="3ec46-117">[Azure Active Directory Premium P1 또는 P2 Edition](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="3ec46-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="3ec46-118">완료 된 hello [필수 구성 요소 tooaccess hello Azure AD 보고 API](active-directory-reporting-api-prerequisites.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-118">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="3ec46-119">Hello API 액세스</span><span class="sxs-lookup"><span data-stu-id="3ec46-119">Accessing hello API</span></span>
<span data-ttu-id="3ec46-120">Hello를 통해이 API를 액세스 하거나 [그래프 탐색기](https://graphexplorer2.cloudapp.net) 프로그래밍 방식으로 사용 하거나, 예를 들어 PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ec46-120">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="3ec46-121">순서 대로 PowerShell toocorrectly 해석 AAD Graph REST 호출에 사용 된 hello OData 필터 구문에 대 한 사용 해야 hello 억음 악센트 기호 (즉,: 억음 악센트 기호) 문자 너무 "문자는 이스케이프 처리할" hello $.</span><span class="sxs-lookup"><span data-stu-id="3ec46-121">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="3ec46-122">hello 억음 악센트 문자 역할을 [PowerShell의 이스케이프 문자](https://technet.microsoft.com/library/hh847755.aspx), PowerShell toodo hello $ 문자를 해석 하는 리터럴 허용 하 고 PowerShell 변수 이름으로 혼동 하지 않도록 (예: $filter).</span><span class="sxs-lookup"><span data-stu-id="3ec46-122">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="3ec46-123">이 항목의 포커스를 hello hello 그래프 탐색기 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-123">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="3ec46-124">PowerShell 예제는 이 [PowerShell 스크립트](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ec46-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="3ec46-125">API 끝점</span><span class="sxs-lookup"><span data-stu-id="3ec46-125">API Endpoint</span></span>
<span data-ttu-id="3ec46-126">기본 URI 뒤 hello를 사용 하 여이 API에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-126">You can access this API using hello following base URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



<span data-ttu-id="3ec46-127">이 API는 toohello 양의 데이터가 인해 1 백만 레코드의 제한을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-127">Due toohello volume of data, this API has a limit of one million returned records.</span></span> 

<span data-ttu-id="3ec46-128">이 호출 일괄 처리로 hello 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-128">This call returns hello data in batches.</span></span> <span data-ttu-id="3ec46-129">각 배치에는 최대 1000개 레코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-129">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="3ec46-130">tooget hello의 다음 일괄 처리 레코드를 사용 하 여 hello 다음 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-130">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="3ec46-131">Hello 가져오기 [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) hello 반환 되는 레코드의 첫 번째 집합의 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-131">Get hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from hello first set of returned records.</span></span> <span data-ttu-id="3ec46-132">hello skip 토큰 hello 결과 집합의 hello 끝에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-132">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a><span data-ttu-id="3ec46-133">지원되는 필터</span><span class="sxs-lookup"><span data-stu-id="3ec46-133">Supported filters</span></span>
<span data-ttu-id="3ec46-134">Hello API에 의해 반환 된 레코드 수를 좁힐 수 있는 필터의 양식에서.</span><span class="sxs-lookup"><span data-stu-id="3ec46-134">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="3ec46-135">로그인 API에 대 한 관련된 데이터를 필터에 따라 hello 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-135">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="3ec46-136">**$top =\<반환 된 레코드 toobe 수가\>**  -toolimit hello 반환 된 레코드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-136">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="3ec46-137">이 작업은 비용이 많이 드는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-137">This is an expensive operation.</span></span> <span data-ttu-id="3ec46-138">개체의 tooreturn 수천을 원하는 경우이 필터를 사용 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-138">You should not use this filter if you want tooreturn thousands of objects.</span></span>  
* <span data-ttu-id="3ec46-139">**$filter =\<필터 문을\>**  -toospecify hello 별로 지원 되는 필터 필드, 중요 한 레코드의 hello 종류</span><span class="sxs-lookup"><span data-stu-id="3ec46-139">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="3ec46-140">지원되는 필터 필드 및 연산자</span><span class="sxs-lookup"><span data-stu-id="3ec46-140">Supported filter fields and operators</span></span>
<span data-ttu-id="3ec46-141">toospecify hello 유형 중요 한 레코드를 하나 또는 hello 필터 필드를 다음의 조합을 포함할 수 있는 필터 문을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-141">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="3ec46-142">[signinDateTime](#signindatetime) - 날짜 또는 날짜 범위를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-142">[signinDateTime](#signindatetime) - defines a date or date range</span></span>
* <span data-ttu-id="3ec46-143">[userId](#userid) -정의 기반으로 특정 사용자 hello 사용자의 id입니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-143">[userId](#userid) - defines a specific user based hello user's ID.</span></span>
* <span data-ttu-id="3ec46-144">[userPrincipalName](#userprincipalname) -특정 사용자 기반 hello 사용자의 사용자 계정 이름 (UPN)을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-144">[userPrincipalName](#userprincipalname) - defines a specific user based hello user's user principal name (UPN)</span></span>
* <span data-ttu-id="3ec46-145">[appId](#appid) -특정 응용 프로그램 기반 hello 앱의 ID를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-145">[appId](#appid) - defines a specific app based hello app's ID</span></span>
* <span data-ttu-id="3ec46-146">[appDisplayName](#appdisplayname) -정의 기반으로 하는 특정 앱 hello 응용 프로그램의 표시 이름</span><span class="sxs-lookup"><span data-stu-id="3ec46-146">[appDisplayName](#appdisplayname) - defines a specific app based hello app's display name</span></span>
* <span data-ttu-id="3ec46-147">[loginStatus](#loginStatus) -정의 hello 로그인의 hello 상태 (성공 / 실패)</span><span class="sxs-lookup"><span data-stu-id="3ec46-147">[loginStatus](#loginStatus) - defines hello status of hello logins (success / failure)</span></span>

> [!NOTE]
> <span data-ttu-id="3ec46-148">그래프 탐색기를 사용할 때는 hello 있습니다 각 문자에 대 한 사례 필터 필드는 올바른 toouse hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-148">When using Graph Explorer, you hello need toouse hello correct case for each letter is your filter fields.</span></span>
> 
> 

<span data-ttu-id="3ec46-149">데이터를 반환 하는 hello hello 범위 아래로 toonarrow를 hello 지원 필터 및 필터 필드의 조합을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-149">toonarrow down hello scope of hello returned data, you can build combinations of hello supported filters and filter fields.</span></span> <span data-ttu-id="3ec46-150">예를 들어 hello 다음 반환 명령문 hello 1 일부 터 2016 년 7 월 6 일 2016 년 7 월 사이의 상위 10 개의 레코드:</span><span class="sxs-lookup"><span data-stu-id="3ec46-150">For example, hello following statement returns hello top 10 records between July 1st 2016 and July 6th 2016:</span></span>

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a><span data-ttu-id="3ec46-151">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="3ec46-151">signinDateTime</span></span>
<span data-ttu-id="3ec46-152">**지원되는 연산자**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="3ec46-152">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="3ec46-153">**예제**:</span><span class="sxs-lookup"><span data-stu-id="3ec46-153">**Example**:</span></span>

<span data-ttu-id="3ec46-154">특정 날짜 사용</span><span class="sxs-lookup"><span data-stu-id="3ec46-154">Using a specific date</span></span>

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



<span data-ttu-id="3ec46-155">날짜 범위 사용</span><span class="sxs-lookup"><span data-stu-id="3ec46-155">Using a date range</span></span>    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


<span data-ttu-id="3ec46-156">**참고**:</span><span class="sxs-lookup"><span data-stu-id="3ec46-156">**Notes**:</span></span>

<span data-ttu-id="3ec46-157">hello datetime 매개 변수는 hello UTC 형식에서 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-157">hello datetime parameter should be in hello UTC format</span></span> 

- - -
### <a name="userid"></a><span data-ttu-id="3ec46-158">userId</span><span class="sxs-lookup"><span data-stu-id="3ec46-158">userId</span></span>
<span data-ttu-id="3ec46-159">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="3ec46-159">**Supported operators**: eq</span></span>

<span data-ttu-id="3ec46-160">**예제**:</span><span class="sxs-lookup"><span data-stu-id="3ec46-160">**Example**:</span></span>

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

<span data-ttu-id="3ec46-161">**참고**:</span><span class="sxs-lookup"><span data-stu-id="3ec46-161">**Notes**:</span></span>

<span data-ttu-id="3ec46-162">사용자 Id의 hello 값은 문자열 값</span><span class="sxs-lookup"><span data-stu-id="3ec46-162">hello value of userId is a string value</span></span>

- - -
### <a name="userprincipalname"></a><span data-ttu-id="3ec46-163">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="3ec46-163">userPrincipalName</span></span>
<span data-ttu-id="3ec46-164">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="3ec46-164">**Supported operators**: eq</span></span>

<span data-ttu-id="3ec46-165">**예제**:</span><span class="sxs-lookup"><span data-stu-id="3ec46-165">**Example**:</span></span>

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


<span data-ttu-id="3ec46-166">**참고**:</span><span class="sxs-lookup"><span data-stu-id="3ec46-166">**Notes**:</span></span>

<span data-ttu-id="3ec46-167">userPrincipalName의 hello 값은 문자열 값</span><span class="sxs-lookup"><span data-stu-id="3ec46-167">hello value of userPrincipalName is a string value</span></span>

- - -
### <a name="appid"></a><span data-ttu-id="3ec46-168">appId</span><span class="sxs-lookup"><span data-stu-id="3ec46-168">appId</span></span>
<span data-ttu-id="3ec46-169">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="3ec46-169">**Supported operators**: eq</span></span>

<span data-ttu-id="3ec46-170">**예제**:</span><span class="sxs-lookup"><span data-stu-id="3ec46-170">**Example**:</span></span>

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



<span data-ttu-id="3ec46-171">**참고**:</span><span class="sxs-lookup"><span data-stu-id="3ec46-171">**Notes**:</span></span>

<span data-ttu-id="3ec46-172">appId의 hello 값은 문자열 값</span><span class="sxs-lookup"><span data-stu-id="3ec46-172">hello value of appId is a string value</span></span>

- - -
### <a name="appdisplayname"></a><span data-ttu-id="3ec46-173">appDisplayName</span><span class="sxs-lookup"><span data-stu-id="3ec46-173">appDisplayName</span></span>
<span data-ttu-id="3ec46-174">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="3ec46-174">**Supported operators**: eq</span></span>

<span data-ttu-id="3ec46-175">**예제**:</span><span class="sxs-lookup"><span data-stu-id="3ec46-175">**Example**:</span></span>

    $filter=appDisplayName+eq+'Azure+Portal' 


<span data-ttu-id="3ec46-176">**참고**:</span><span class="sxs-lookup"><span data-stu-id="3ec46-176">**Notes**:</span></span>

<span data-ttu-id="3ec46-177">appDisplayName의 hello 값은 문자열 값</span><span class="sxs-lookup"><span data-stu-id="3ec46-177">hello value of appDisplayName is a string value</span></span>

- - -
### <a name="loginstatus"></a><span data-ttu-id="3ec46-178">loginStatus</span><span class="sxs-lookup"><span data-stu-id="3ec46-178">loginStatus</span></span>
<span data-ttu-id="3ec46-179">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="3ec46-179">**Supported operators**: eq</span></span>

<span data-ttu-id="3ec46-180">**예제**:</span><span class="sxs-lookup"><span data-stu-id="3ec46-180">**Example**:</span></span>

    $filter=loginStatus+eq+'1'  


<span data-ttu-id="3ec46-181">**참고**:</span><span class="sxs-lookup"><span data-stu-id="3ec46-181">**Notes**:</span></span>

<span data-ttu-id="3ec46-182">LoginStatus hello에 대 한 두 가지가 있습니다: 0-성공을, 1-실패</span><span class="sxs-lookup"><span data-stu-id="3ec46-182">There are two options for hello loginStatus: 0 - success, 1 - failure</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="3ec46-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3ec46-183">Next steps</span></span>
* <span data-ttu-id="3ec46-184">필터링 된 로그인 활동에 대 한 toosee 예제 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="3ec46-184">Do you want toosee examples for filtered sign-in activities?</span></span> <span data-ttu-id="3ec46-185">체크 아웃 hello [Azure Active Directory 로그인 활동 보고서 API 예제](active-directory-reporting-api-sign-in-activity-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-185">Check out hello [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span></span>
* <span data-ttu-id="3ec46-186">Tooknow hello Azure AD 보고 API에 대 한 자세한 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="3ec46-186">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="3ec46-187">참조 [hello Azure Active Directory 보고 API 시작](active-directory-reporting-api-getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ec46-187">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

