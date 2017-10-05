---
title: "Azure Active Directory B2C: 사용량 보고 API 샘플 및 정의 | Microsoft Docs"
description: "Azure AD B2C 테넌트 사용자, 인증 및 다단계 인증에 대한 보고서를 얻는 방법에 대한 가이드 및 샘플입니다."
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 52180b760046d273c5a75720df0a73532d0343ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-the-reporting-api"></a><span data-ttu-id="d63be-103">보고 API를 통해 Azure AD B2C에서 사용량 보고서에 액세스</span><span class="sxs-lookup"><span data-stu-id="d63be-103">Accessing usage reports in Azure AD B2C via the reporting API</span></span>

<span data-ttu-id="d63be-104">Azure AD B2C(Azure Active Directory B2C)는 사용자 로그인 및 Azure Multi-Factor Authentication 기반 인증을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="d63be-105">인증은 ID 공급자를 통해 응용 프로그램 제품군의 최종 사용자에게 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="d63be-106">테넌트에 등록된 사용자의 수, 등록하는 데 사용된 공급자 및 유형별 인증 수를 알고 있으면 다음과 같은 질문에 답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-106">When you know the number of users registered in the tenant, the providers they used to register, and the number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="d63be-107">각 유형의 ID 공급자(예: Microsoft 또는 LinkedIn 계정)에서 지난 10일 동안 등록한 사용자는 몇 명인가요?</span><span class="sxs-lookup"><span data-stu-id="d63be-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in the last 10 days?</span></span>
* <span data-ttu-id="d63be-108">지난 달에 Multi-Factor Authentication을 통해 성공적으로 완료된 인증은 몇 번인가요?</span><span class="sxs-lookup"><span data-stu-id="d63be-108">How many authentications using Multi-Factor Authentication have completed successfully in the last month?</span></span>
* <span data-ttu-id="d63be-109">이번 달에 완료된 로그인 기반 인증은 몇 번인가요?</span><span class="sxs-lookup"><span data-stu-id="d63be-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="d63be-110">일일?</span><span class="sxs-lookup"><span data-stu-id="d63be-110">Per day?</span></span> <span data-ttu-id="d63be-111">응용 프로그램 당?</span><span class="sxs-lookup"><span data-stu-id="d63be-111">Per application?</span></span>
* <span data-ttu-id="d63be-112">내 Azure AD B2C 테넌트 활동에 대한 월별 예상 비용은 어떻게 추정해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="d63be-112">How can I estimate the expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="d63be-113">이 문서에서는 사용자 수, 청구 가능한 로그인 기반 인증 수 및 다단계 인증 수에 기반한 청구 활동에 연결된 보고서에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-113">This article focuses on reports tied to billing activity, which is based on the number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d63be-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d63be-114">Prerequisites</span></span>
<span data-ttu-id="d63be-115">시작하기 전에 [Azure AD Reporting API에 액세스하기 위한 필수 구성 요소](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/)의 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-115">Before you get started, you need to complete the steps in [Prerequisites to access the Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="d63be-116">응용 프로그램을 만들고, 그 암호를 가져오고, Azure AD B2C 테넌트의 보고서에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-116">Create an application, obtain a secret for it, and grant it access rights to your Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="d63be-117">*Bash 스크립트* 및 *Python 스크립트* 예제도 여기에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="d63be-118">PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="d63be-118">PowerShell script</span></span>
<span data-ttu-id="d63be-119">이 스크립트에서는 `TimeStamp` 매개 변수 및 `ApplicationId` 필터를 사용하여 4개의 사용량 보고서를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-119">This script demonstrates the creation of four usage reports by using the `TimeStamp` parameter and the `ApplicationId` filter.</span></span>

```powershell
# This script will require the Web Application and permissions setup in Azure Active Directory

# Constants
$ClientID      = "your-client-application-id-here"  
$ClientSecret  = "your-client-application-secret-here"
$loginURL      = "https://login.microsoftonline.com"
$tenantdomain  = "your-b2c-tenant-domain.onmicrosoft.com"  
# Get an Oauth 2 access token based on client id, secret and tenant domain
$body          = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth         = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
if ($oauth.access_token -ne $null) {
    $headerParams  = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    Write-host Data from the tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for the report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for the " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a><span data-ttu-id="d63be-120">사용량 보고서 정의</span><span class="sxs-lookup"><span data-stu-id="d63be-120">Usage report definitions</span></span>
* <span data-ttu-id="d63be-121">**tenantUserCount** - 지난 30일 이내 ID 공급자 유형별 일일 테넌트 사용자 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-121">**tenantUserCount**: The number of users in the tenant by type of identity provider, per day in the last 30 days.</span></span> <span data-ttu-id="d63be-122">(선택 사항: `TimeStamp` 필터는 지정된 날짜부터 현재 날짜까지의 사용자 수를 제공합니다.)</span><span class="sxs-lookup"><span data-stu-id="d63be-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date to the current date).</span></span> <span data-ttu-id="d63be-123">보고서에서 다음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-123">The report provides:</span></span>
  * <span data-ttu-id="d63be-124">**TotalUserCount**: 모든 사용자 개체의 수</span><span class="sxs-lookup"><span data-stu-id="d63be-124">**TotalUserCount**: The number of all user objects.</span></span>
  * <span data-ttu-id="d63be-125">**OtherUserCount**: Azure Active Directory 사용자(Azure AD B2C 사용자가 아님)의 수</span><span class="sxs-lookup"><span data-stu-id="d63be-125">**OtherUserCount**: The number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="d63be-126">**LocalUserCount**: Azure AD B2C 테넌트에 대한 로컬 자격 증명으로 만든 Azure AD B2C 사용자 계정의 수</span><span class="sxs-lookup"><span data-stu-id="d63be-126">**LocalUserCount**: The number of Azure AD B2C user accounts created with credentials local to the Azure AD B2C tenant.</span></span>

* <span data-ttu-id="d63be-127">**AlternateIdUserCount** - 외부 ID 공급자(예: Facebook, Microsoft 계정 또는 다른 Azure Active Directory 테넌트, `OrgId`라고도 함)에 등록된 Azure AD B2C 사용자 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-127">**AlternateIdUserCount**: The number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred to as an `OrgId`).</span></span>

* <span data-ttu-id="d63be-128">**b2cAuthenticationCountSummary** - 지난 30일 동안 일별 및 인증 흐름 유형별 청구 가능한 일일 인증 수의 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-128">**b2cAuthenticationCountSummary**: Summary of the daily number of billable authentications over the last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="d63be-129">**b2cAuthenticationCount** - 한 기간 내 인증 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-129">**b2cAuthenticationCount**: The number of authentications within a time period.</span></span> <span data-ttu-id="d63be-130">기본값은 지난 30일입니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-130">The default is the last 30 days.</span></span>  <span data-ttu-id="d63be-131">(선택 사항: 시작 및 종료 `TimeStamp` 매개 변수의 시작과 끝은 특정 기간을 정의합니다.) 출력에는 `StartTimeStamp`(이 테넌트에 대한 활동의 가장 빠른 날짜)와 `EndTimeStamp`(최신 업데이트)가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-131">(Optional: The beginning and ending `TimeStamp` parameters define a specific time period.) The output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="d63be-132">**b2cMfaRequestCountSummary** - 일별 및 유형별(SMS 또는 음성) 일일 다단계 인증 수의 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-132">**b2cMfaRequestCountSummary**: Summary of the daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="d63be-133">제한 사항</span><span class="sxs-lookup"><span data-stu-id="d63be-133">Limitations</span></span>
<span data-ttu-id="d63be-134">사용자 수 데이터는 24-48시간마다 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-134">User count data is refreshed every 24 to 48 hours.</span></span> <span data-ttu-id="d63be-135">인증은 하루에도 여러 번 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="d63be-136">`ApplicationId` 필터를 사용하는 경우 다음 조건 중 하나로 인해 보고서 응답이 비어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-136">When using the `ApplicationId` filter, an empty report response can be due to one of following conditions:</span></span>
  * <span data-ttu-id="d63be-137">응용 프로그램 ID가 테넌트에 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-137">The application ID does not exist in the tenant.</span></span> <span data-ttu-id="d63be-138">정확한지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d63be-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="d63be-139">응용 프로그램 ID가 있지만 보고 기간에 존재하는 데이터가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-139">The application ID exists, but no data was found in the reporting period.</span></span> <span data-ttu-id="d63be-140">날짜/시간 매개 변수를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="d63be-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d63be-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d63be-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="d63be-142">Azure AD에 대한 월별 예상 청구 비용 견적</span><span class="sxs-lookup"><span data-stu-id="d63be-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="d63be-143">[사용 가능한 최근 Azure AD B2C 가격 책정](https://azure.microsoft.com/pricing/details/active-directory-b2c/)과 결합한 경우 일별, 주별 및 월별 Azure 소비를 예측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-143">When combined with [the most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="d63be-144">견적은 전체 비용에 영향을 줄 수 있는 테넌트 동작의 변경 내용을 계획할 때 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="d63be-145">[연결된 Azure 구독](active-directory-b2c-how-to-enable-billing.md)에서 실제 비용을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="d63be-146">다른 출력 형식의 옵션</span><span class="sxs-lookup"><span data-stu-id="d63be-146">Options for other output formats</span></span>
<span data-ttu-id="d63be-147">다음 코드에서는 JSON, 이름 값 목록 및 XML로 출력을 보내는 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d63be-147">The following code shows examples of sending output to JSON, a name value list, and XML:</span></span>
```powershell
# to output to JSON use following line in the PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# to output the content to a name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# to output the content in XML use the following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
