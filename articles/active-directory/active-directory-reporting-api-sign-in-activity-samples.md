---
title: "Azure Active Directory 로그인 활동 보고서 API 샘플 | Microsoft Docs"
description: "Azure Active Directory Reporting API를 시작하는 방법"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: c41c1489-726b-4d3f-81d6-83beb932df9c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 7fc2b59fe37ed2ffe85925c457300ef8fd83c3c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a><span data-ttu-id="d20c4-103">Azure Active Directory 로그인 활동 보고서 API 샘플</span><span class="sxs-lookup"><span data-stu-id="d20c4-103">Azure Active Directory sign-in activity report API samples</span></span>
<span data-ttu-id="d20c4-104">이 항목은 Azure Active Directory Reporting API에 대한 항목 컬렉션의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="d20c4-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="d20c4-105">Azure AD Reporting은 코드 또는 관련된 도구를 사용하여 로그인 활동 데이터에 액세스할 수 있는 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d20c4-105">Azure AD reporting provides you with an API that enables you to access sign-in activity data using code or related tools.</span></span>  
<span data-ttu-id="d20c4-106">이 항목은 **로그인 활동 API**에 대한 샘플 코드를 제공하는 방법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="d20c4-106">The scope of this topic is to provide you with sample code for the **sign-in activity API**.</span></span>

<span data-ttu-id="d20c4-107">다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d20c4-107">See:</span></span>

* <span data-ttu-id="d20c4-108">자세한 개념 정보는 [감사 로그](active-directory-reporting-azure-portal.md#activity-reports)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d20c4-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>
* <span data-ttu-id="d20c4-109">[Azure Active Directory Reporting API 시작](active-directory-reporting-api-getting-started.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d20c4-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d20c4-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d20c4-110">Prerequisites</span></span>
<span data-ttu-id="d20c4-111">이 항목에서 샘플을 사용하기 전에 [Azure AD Reporting API에 액세스하기 위한 필수 구성 요소](active-directory-reporting-api-prerequisites.md)를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d20c4-111">Before you can use the samples in this topic, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="powershell-script"></a><span data-ttu-id="d20c4-112">PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="d20c4-112">PowerShell script</span></span>
    # This script will require the Web Application and permissions setup in Azure Active Directory
    $ClientID       = "<clientId>"             # Should be a ~35 character string insert your info here
    $ClientSecret   = "<clientSecret>"         # Should be a ~44 character string insert your info here
    $loginURL       = "https://login.microsoftonline.com/"
    $tenantdomain   = "<tenantDomain>"
    $ daterange            # For example, contoso.onmicrosoft.com

    $7daysago = "{0:s}" -f (get-date).AddDays(-7) + "Z"
    # or, AddMinutes(-5)

    Write-Output $7daysago

    # Get an Oauth 2 access token based on client id, secret and tenant domain
    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}

    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    if ($oauth.access_token -ne $null) {
    $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    $url = "https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&`$filter=signinDateTime ge $7daysago"

    $i=0

    Do{
        Write-Output "Fetching data using Uri: $url"
        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)
        Write-Output "Save the output to a file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-the-script"></a><span data-ttu-id="d20c4-113">스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="d20c4-113">Executing the script</span></span>
<span data-ttu-id="d20c4-114">스크립트를 편집한 후에는 실행하여 감사 로그 보고서에서 예상한 데이터가 반환되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d20c4-114">Once you finish editing the script, run it and verify that the expected data from the Audit logs report is returned.</span></span>

<span data-ttu-id="d20c4-115">스크립트는 JSON 형식으로 로그인 보고서의 출력을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d20c4-115">The script returns output from the sign-in report in JSON format.</span></span> <span data-ttu-id="d20c4-116">또한 동일한 출력으로 `SigninActivities.json` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d20c4-116">It also creates an `SigninActivities.json` file with the same output.</span></span> <span data-ttu-id="d20c4-117">다른 보고서의 데이터를 반환하도록 스크립트를 수정하고 필요 없는 출력 형식을 주석으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d20c4-117">You can experiment by modifying the script to return data from other reports, and comment out the output formats that you do not need.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d20c4-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d20c4-118">Next Steps</span></span>
* <span data-ttu-id="d20c4-119">이 항목의 샘플을 사용자 지정하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="d20c4-119">Would you like to customize the samples in this topic?</span></span> <span data-ttu-id="d20c4-120">[Azure Active Directory 로그인 활동 API 참조](active-directory-reporting-api-sign-in-activity-reference.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d20c4-120">Check out the [Azure Active Directory sign-in activity API reference](active-directory-reporting-api-sign-in-activity-reference.md).</span></span> 
* <span data-ttu-id="d20c4-121">Azure Active Directory Reporting API를 사용하는 전체적인 개요를 확인하려는 경우 [Azure Active Directory Reporting API 시작](active-directory-reporting-api-getting-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d20c4-121">If you want to see a complete overview of using the Azure Active Directory reporting API, see [Getting started with the Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="d20c4-122">Azure Active Directory Reporting에 대한 자세한 내용을 알아보려면 [Azure Active Directory Reporting 가이드](active-directory-reporting-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d20c4-122">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

