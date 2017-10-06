---
title: "aaaAzure Active Directory 로그인 활동 보고서 API 예제 | Microsoft Docs"
description: "Tooget은 hello Azure Active Directory 보고 API로 시작 하는 방법"
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
ms.openlocfilehash: d4fbbea95fe0b52828673b997681ae37481e21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a>Azure Active Directory 로그인 활동 보고서 API 샘플
이 항목은 Azure Active Directory hello에 대 한 항목 컬렉션의 일부 API를 보고 합니다.  
Azure AD 보고 하면 있도록 API 코드 또는 관련된 도구를 사용 하 여 tooaccess 로그인 활동 데이터 있습니다.  
hello이 항목의 범위는 hello에 대 한 코드 예제는 tooprovide **로그인 활동 API**합니다.

다음을 참조하세요.

* 자세한 개념 정보는 [감사 로그](active-directory-reporting-azure-portal.md#activity-reports)를 참조하세요.
* [Hello Azure Active Directory 보고 API 시작](active-directory-reporting-api-getting-started.md) hello 보고 API에 대 한 자세한 내용은 합니다.


## <a name="prerequisites"></a>필수 조건
이 항목의 hello 샘플을 사용 하려면 먼저 toocomplete hello [필수 구성 요소 tooaccess hello Azure AD 보고 API](active-directory-reporting-api-prerequisites.md)합니다.  

## <a name="powershell-script"></a>PowerShell 스크립트
    # This script will require hello Web Application and permissions setup in Azure Active Directory
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
        Write-Output "Save hello output tooa file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-hello-script"></a>Hello 스크립트 실행
한 번 hello 스크립트를 편집, 실행 끝나고 해당 hello 예상 hello 감사 로그 보고서에서에서 데이터 반환 되는지 확인 합니다.

hello 스크립트 JSON 형식에 hello 로그인 보고서의 출력을 반환합니다. 또한 만듭니다는 `SigninActivities.json` hello로 동일 파일 출력 합니다. 다른 보고서 및 필요 하지 않은 hello 출력 형식 주석에서 hello 스크립트 tooreturn 데이터를 수정 하 여 테스트할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* 이 항목의 toocustomize hello 샘플 하 시겠습니까? 체크 아웃 hello [Azure Active Directory 로그인 활동이 API 참조](active-directory-reporting-api-sign-in-activity-reference.md)합니다. 
* Azure Active Directory 보고 API hello toosee 전체적인 개요를 사용 하 여 원하는 경우를 참조 하십시오 [Azure Active Directory 보고 API hello 시작](active-directory-reporting-api-getting-started.md)합니다.
* Azure Active Directory 보고에 대 한 자세한 내용을 toofind 싶으시면 참조 hello [Azure Active Directory Reporting 가이드](active-directory-reporting-guide.md)합니다.  

