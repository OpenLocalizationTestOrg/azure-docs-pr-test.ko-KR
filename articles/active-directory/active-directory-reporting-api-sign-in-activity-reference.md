---
title: "Azure Active Directory 로그인 활동 보고서 API 참조 | Microsoft Docs"
description: "Azure Active Directory 로그인 활동 보고서 API에 대한 참조"
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
ms.openlocfilehash: d83f1a899ba38dab2c1c1661adede87db6f88c20
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a><span data-ttu-id="b4866-103">Azure Active Directory 로그인 활동 보고서 API 참조</span><span class="sxs-lookup"><span data-stu-id="b4866-103">Azure Active Directory sign-in activity report API reference</span></span>
<span data-ttu-id="b4866-104">이 항목은 Azure Active Directory Reporting API에 대한 항목 컬렉션의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="b4866-105">Azure AD Reporting은 코드 또는 관련된 도구를 사용하여 로그인 활동 보고서 데이터에 액세스할 수 있는 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-105">Azure AD reporting provides you with an API that enables you to access sign-in activity report data using code or related tools.</span></span>
<span data-ttu-id="b4866-106">이 항목은 **로그인 활동 보고서 API**에 대한 참조 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-106">The scope of this topic is to provide you with reference information about the **sign-in activity report API**.</span></span>

<span data-ttu-id="b4866-107">다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4866-107">See:</span></span>

* <span data-ttu-id="b4866-108">[로그인 활동](active-directory-reporting-azure-portal.md#activity-reports) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4866-108">[Sign-in activities](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="b4866-109">[Azure Active Directory Reporting API 시작](active-directory-reporting-api-getting-started.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4866-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


## <a name="who-can-access-the-api-data"></a><span data-ttu-id="b4866-110">API 데이터에 액세스할 수 있는 사용자는 누구인가요?</span><span class="sxs-lookup"><span data-stu-id="b4866-110">Who can access the API data?</span></span>
* <span data-ttu-id="b4866-111">보안 관리자 또는 보안 읽기 권한자 역할의 사용자 및 서비스 주체</span><span class="sxs-lookup"><span data-stu-id="b4866-111">Users and Service Principals in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="b4866-112">전역 관리자</span><span class="sxs-lookup"><span data-stu-id="b4866-112">Global Admins</span></span>
* <span data-ttu-id="b4866-113">API에 액세스하는 인증이 있는 모든 앱(전역 관리자의 사용 권한에 따라 앱 권한 부여를 설정할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="b4866-113">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span></span>

<span data-ttu-id="b4866-114">서명 이벤트와 같이 보안 API에 액세스하기 위해 응용 프로그램에 대한 액세스를 구성하려면 다음 PowerShell을 사용하여 응용 프로그램 서비스 주체를 보안 읽기 권한자 역할에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-114">To configure access for an application to access security APIs such as signin events, use the following PowerShell to add the applications Service Principal into the Security Reader role</span></span>

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a><span data-ttu-id="b4866-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b4866-115">Prerequisites</span></span>
<span data-ttu-id="b4866-116">Reporting API를 통해 이 보고서에 액세스하려면 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-116">To access this report through the reporting API, you must have:</span></span>

* <span data-ttu-id="b4866-117">[Azure Active Directory Premium P1 또는 P2 Edition](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="b4866-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="b4866-118">[Azure AD Reporting API에 액세스하기 위한 필수 구성 요소](active-directory-reporting-api-prerequisites.md)를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-118">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-the-api"></a><span data-ttu-id="b4866-119">API에 액세스</span><span class="sxs-lookup"><span data-stu-id="b4866-119">Accessing the API</span></span>
<span data-ttu-id="b4866-120">예를 들어 [Graph Explorer](https://graphexplorer2.cloudapp.net) 를 통해 또는 프로그래밍 방식으로 PowerShell을 사용하여 이 API에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-120">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="b4866-121">PowerShell이 AAD Graph REST 호출에 사용된 OData 필터 구문을 올바르게 해석하기 위해 '(억음 부호) 기호를 사용하여 $ 기호를 "이스케이프"해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-121">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span></span> <span data-ttu-id="b4866-122">' 기호는 [PowerShell의 이스케이프 문자](https://technet.microsoft.com/library/hh847755.aspx)로 사용되어 PowerShell에서 $ 기호의 리터럴 해석을 수행하고 PowerShell 변수 이름(예: $filter)으로 혼동하지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-122">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="b4866-123">이 항목은 Graph Explorer에 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-123">The focus of this topic is on the Graph Explorer.</span></span> <span data-ttu-id="b4866-124">PowerShell 예제는 이 [PowerShell 스크립트](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4866-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="b4866-125">API 끝점</span><span class="sxs-lookup"><span data-stu-id="b4866-125">API Endpoint</span></span>
<span data-ttu-id="b4866-126">다음과 같은 기본 URI를 사용하여 이 API에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-126">You can access this API using the following base URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



<span data-ttu-id="b4866-127">데이터의 볼륨 때문에 이 API는 백만 개의 반환된 레코드로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-127">Due to the volume of data, this API has a limit of one million returned records.</span></span> 

<span data-ttu-id="b4866-128">이 호출은 배치에서 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-128">This call returns the data in batches.</span></span> <span data-ttu-id="b4866-129">각 배치에는 최대 1000개 레코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-129">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="b4866-130">레코드의 다음 배치를 가져오려면 [다음] 링크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-130">To get the next batch of records, use the Next link.</span></span> <span data-ttu-id="b4866-131">첫 번째 반환되는 레코드의 집합에서 [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-131">Get the [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from the first set of returned records.</span></span> <span data-ttu-id="b4866-132">건너뛰기 토큰은 결과 집합의 끝에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-132">The skip token will be at the end of the result set.</span></span>  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a><span data-ttu-id="b4866-133">지원되는 필터</span><span class="sxs-lookup"><span data-stu-id="b4866-133">Supported filters</span></span>
<span data-ttu-id="b4866-134">필터의 형태로 API 호출에서 반환되는 레코드의 수를 좁힐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-134">You can narrow down the number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="b4866-135">로그인 API 관련 데이터의 경우 다음 필터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-135">For sign-in API related data, the following filters are supported:</span></span>

* <span data-ttu-id="b4866-136">**$top=\<반환될 레코드의 수\>** - 반환된 레코드의 수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-136">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span></span> <span data-ttu-id="b4866-137">이 작업은 비용이 많이 드는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-137">This is an expensive operation.</span></span> <span data-ttu-id="b4866-138">수천 개의 개체를 반환하려는 경우 이 필터를 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-138">You should not use this filter if you want to return thousands of objects.</span></span>  
* <span data-ttu-id="b4866-139">**$filter=\<필터 문\>** - 지원되는 필터 필드를 기반으로 원하는 레코드 종류를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-139">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="b4866-140">지원되는 필터 필드 및 연산자</span><span class="sxs-lookup"><span data-stu-id="b4866-140">Supported filter fields and operators</span></span>
<span data-ttu-id="b4866-141">원하는 레코드의 종류를 지정하려면 다음 필터 필드 중 하나 또는 조합을 포함할 수 있는 필터 문을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-141">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span></span>

* <span data-ttu-id="b4866-142">[signinDateTime](#signindatetime) - 날짜 또는 날짜 범위를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-142">[signinDateTime](#signindatetime) - defines a date or date range</span></span>
* <span data-ttu-id="b4866-143">[userId](#userid) - 특정 사용자 기반 사용자의 ID를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-143">[userId](#userid) - defines a specific user based the user's ID.</span></span>
* <span data-ttu-id="b4866-144">[userPrincipalName](#userprincipalname) - 특정 사용자 기반 사용자의 사용자 계정 이름(UPN)을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-144">[userPrincipalName](#userprincipalname) - defines a specific user based the user's user principal name (UPN)</span></span>
* <span data-ttu-id="b4866-145">[appId](#appid) - 특정 앱 기반 응용 프로그램의 ID를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-145">[appId](#appid) - defines a specific app based the app's ID</span></span>
* <span data-ttu-id="b4866-146">[appDisplayName](#appdisplayname) - 특정 앱 기반 앱의 표시 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-146">[appDisplayName](#appdisplayname) - defines a specific app based the app's display name</span></span>
* <span data-ttu-id="b4866-147">[loginStatus](#loginStatus) - 로그인의 상태를 정의합니다(성공/실패).</span><span class="sxs-lookup"><span data-stu-id="b4866-147">[loginStatus](#loginStatus) - defines the status of the logins (success / failure)</span></span>

> [!NOTE]
> <span data-ttu-id="b4866-148">Graph Explorer를 사용하는 경우 필터 필드인 각 문자에 대한 정확한 대/소문자를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-148">When using Graph Explorer, you the need to use the correct case for each letter is your filter fields.</span></span>
> 
> 

<span data-ttu-id="b4866-149">반환된 데이터의 범위를 좁히기 위해 지원되는 필터 및 필터 필드의 조합을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-149">To narrow down the scope of the returned data, you can build combinations of the supported filters and filter fields.</span></span> <span data-ttu-id="b4866-150">예를 들어, 다음 문은 2016년 7월 1일과 2016년 7월 6일 사이에 상위 10개의 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-150">For example, the following statement returns the top 10 records between July 1st 2016 and July 6th 2016:</span></span>

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a><span data-ttu-id="b4866-151">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="b4866-151">signinDateTime</span></span>
<span data-ttu-id="b4866-152">**지원되는 연산자**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="b4866-152">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="b4866-153">**예제**:</span><span class="sxs-lookup"><span data-stu-id="b4866-153">**Example**:</span></span>

<span data-ttu-id="b4866-154">특정 날짜 사용</span><span class="sxs-lookup"><span data-stu-id="b4866-154">Using a specific date</span></span>

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



<span data-ttu-id="b4866-155">날짜 범위 사용</span><span class="sxs-lookup"><span data-stu-id="b4866-155">Using a date range</span></span>    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


<span data-ttu-id="b4866-156">**참고**:</span><span class="sxs-lookup"><span data-stu-id="b4866-156">**Notes**:</span></span>

<span data-ttu-id="b4866-157">날짜/시간 매개 변수는 UTC 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-157">The datetime parameter should be in the UTC format</span></span> 

- - -
### <a name="userid"></a><span data-ttu-id="b4866-158">userId</span><span class="sxs-lookup"><span data-stu-id="b4866-158">userId</span></span>
<span data-ttu-id="b4866-159">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="b4866-159">**Supported operators**: eq</span></span>

<span data-ttu-id="b4866-160">**예제**:</span><span class="sxs-lookup"><span data-stu-id="b4866-160">**Example**:</span></span>

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

<span data-ttu-id="b4866-161">**참고**:</span><span class="sxs-lookup"><span data-stu-id="b4866-161">**Notes**:</span></span>

<span data-ttu-id="b4866-162">userId의 값은 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-162">The value of userId is a string value</span></span>

- - -
### <a name="userprincipalname"></a><span data-ttu-id="b4866-163">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="b4866-163">userPrincipalName</span></span>
<span data-ttu-id="b4866-164">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="b4866-164">**Supported operators**: eq</span></span>

<span data-ttu-id="b4866-165">**예제**:</span><span class="sxs-lookup"><span data-stu-id="b4866-165">**Example**:</span></span>

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


<span data-ttu-id="b4866-166">**참고**:</span><span class="sxs-lookup"><span data-stu-id="b4866-166">**Notes**:</span></span>

<span data-ttu-id="b4866-167">userPrincipalName의 값은 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-167">The value of userPrincipalName is a string value</span></span>

- - -
### <a name="appid"></a><span data-ttu-id="b4866-168">appId</span><span class="sxs-lookup"><span data-stu-id="b4866-168">appId</span></span>
<span data-ttu-id="b4866-169">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="b4866-169">**Supported operators**: eq</span></span>

<span data-ttu-id="b4866-170">**예제**:</span><span class="sxs-lookup"><span data-stu-id="b4866-170">**Example**:</span></span>

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



<span data-ttu-id="b4866-171">**참고**:</span><span class="sxs-lookup"><span data-stu-id="b4866-171">**Notes**:</span></span>

<span data-ttu-id="b4866-172">appId의 값은 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-172">The value of appId is a string value</span></span>

- - -
### <a name="appdisplayname"></a><span data-ttu-id="b4866-173">appDisplayName</span><span class="sxs-lookup"><span data-stu-id="b4866-173">appDisplayName</span></span>
<span data-ttu-id="b4866-174">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="b4866-174">**Supported operators**: eq</span></span>

<span data-ttu-id="b4866-175">**예제**:</span><span class="sxs-lookup"><span data-stu-id="b4866-175">**Example**:</span></span>

    $filter=appDisplayName+eq+'Azure+Portal' 


<span data-ttu-id="b4866-176">**참고**:</span><span class="sxs-lookup"><span data-stu-id="b4866-176">**Notes**:</span></span>

<span data-ttu-id="b4866-177">appDisplayName의 값은 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-177">The value of appDisplayName is a string value</span></span>

- - -
### <a name="loginstatus"></a><span data-ttu-id="b4866-178">loginStatus</span><span class="sxs-lookup"><span data-stu-id="b4866-178">loginStatus</span></span>
<span data-ttu-id="b4866-179">**지원되는 연산자**: eq</span><span class="sxs-lookup"><span data-stu-id="b4866-179">**Supported operators**: eq</span></span>

<span data-ttu-id="b4866-180">**예제**:</span><span class="sxs-lookup"><span data-stu-id="b4866-180">**Example**:</span></span>

    $filter=loginStatus+eq+'1'  


<span data-ttu-id="b4866-181">**참고**:</span><span class="sxs-lookup"><span data-stu-id="b4866-181">**Notes**:</span></span>

<span data-ttu-id="b4866-182">loginStatus에는 0 - 성공, 1 - 오류라는 두 개의 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4866-182">There are two options for the loginStatus: 0 - success, 1 - failure</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="b4866-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4866-183">Next steps</span></span>
* <span data-ttu-id="b4866-184">필터링된 로그인 활동에 대한 예제를 참조하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="b4866-184">Do you want to see examples for filtered sign-in activities?</span></span> <span data-ttu-id="b4866-185">[Azure Active Directory 로그인 활동 보고서 API 샘플](active-directory-reporting-api-sign-in-activity-samples.md)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="b4866-185">Check out the [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span></span>
* <span data-ttu-id="b4866-186">Azure AD Reporting API에 대해 자세히 살펴보시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="b4866-186">Do you want to know more about the Azure AD reporting API?</span></span> <span data-ttu-id="b4866-187">[Azure Active Directory Reporting API 시작](active-directory-reporting-api-getting-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4866-187">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

