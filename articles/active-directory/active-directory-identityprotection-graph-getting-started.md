---
title: "Azure Active Directory Id 보호 및 Microsoft Graph aaaGet 시작 | Microsoft Docs"
description: "Azure Active Directory에서 소개 tooquery Microsoft Graph 위험 이벤트 및 관련된 정보의 목록을 제공합니다."
services: active-directory
keywords: "Azure Active Directory ID 보호, 위험 이벤트, 취약점, 보안 정책, Microsoft Graph"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a>Azure Active Directory ID 보호 및 Microsoft Graph 시작
Microsoft API 끝점을 통합 하는 hello 및의 홈 hello을 [Azure Active Directory Id 보호](active-directory-identityprotection.md) Api입니다. hello 첫 번째 API **identityRiskEvents**, 목록에 대 한 Microsoft Graph tooquery 있습니다의 [이벤트 위험](active-directory-identityprotection-risk-events-types.md) 관련 정보 및 합니다. 이 문서는 이 API를 쿼리하는 작업부터 시작합니다. 심층 분석 소개, 전체 설명서 및 액세스 toohello 그래프 탐색기에 대 한 참조 hello [Microsoft Graph 사이트](https://graph.microsoft.io/)합니다.

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.

Microsoft Graph 통해 세 개의 단계 tooaccessing Id 보호 데이터 가지가 있습니다.

1. 클라이언트 암호와 응용 프로그램을 추가합니다. 
2. 이 암호와 다른 몇 가지 정보 tooauthenticate tooMicrosoft 인증 토큰 나타나는 그래프를 사용 합니다. 
3. 이 토큰 toomake 요청 toohello API 끝점을 사용 하 고 Id 보호 데이터를 다시 가져옵니다.

시작하기 전에 다음 항목이 필요합니다.

* Azure AD에서 관리자 권한 toocreate hello 응용
* 테 넌 트의 도메인 (예: contoso.onmicrosoft.com)의 hello 이름

## <a name="add-an-application-with-a-client-secret"></a>클라이언트 암호와 응용 프로그램을 추가합니다.
1. [로그인](https://manage.windowsazure.com) tooyour 관리자 권한으로 Azure 클래식 포털입니다. 
2. Hello 왼쪽된 탐색 창에서 클릭 **Active Directory**합니다. 
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.
4. Hello 메뉴에서 hello 위에 표시를 클릭 **응용 프로그램**합니다.
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **조직에서 개발 중인 응용 프로그램 추가**합니다.
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. Hello에 **응용 프로그램에 대해 알리기** 대화 상자에서 hello 다음 단계를 수행 합니다.
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    a. Hello에 **이름** 텍스트 상자에 응용 프로그램에 대 한 이름 (예:: AADIP 위험 이벤트 API 응용 프로그램).
   
    b. **유형**으로 **웹 응용 프로그램 및/또는 Web API**를 선택합니다.
   
    c. **다음**을 누릅니다.
8. Hello에 **앱 속성** 대화 상자에서 hello 다음 단계를 수행 합니다.
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    a. Hello에 **로그온 URL** 텍스트 상자에 `http://localhost`합니다.
   
    b. Hello에 **앱 ID URI** 텍스트 상자에 `http://localhost`합니다.
   
    c. 페이지 맨 아래에 있는 **완료**을 참조하세요.

이제 응용 프로그램을 구성할 수 있습니다.

![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a>응용 프로그램 권한 toouse hello API를 부여 합니다.
1. Hello 바탕 화면에서 hello 메뉴에서 응용 프로그램의 페이지에서 클릭 **구성**합니다. 
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. Hello에 **tooother 응용 프로그램 사용 권한** 섹션에서 클릭 **응용 프로그램을 추가**합니다.
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. Hello에 **tooother 응용 프로그램 사용 권한** 대화 상자에서 hello 다음 단계를 수행 합니다.
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    a. **Microsoft Graph**를 선택합니다.
   
    b. 페이지 맨 아래에 있는 **완료**을 참조하세요.
4. **응용 프로그램 사용 권한: 0**을 클릭한 다음 **모든 ID 위험 이벤트 정보 참고**를 선택합니다.
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. 클릭 **저장** hello hello 페이지 맨 아래에 있습니다.
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a>선택키 가져오기
1. 응용 프로그램의 페이지 hello **키** 섹션 1 년 기간을 선택 합니다.
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. 클릭 **저장** hello hello 페이지 맨 아래에 있습니다.
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. hello 키 섹션 트 새로 만든된 키의 hello 값을 복사 하 고 안전한 위치에 붙여 넣습니다.
   
    ![응용 프로그램 만들기](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > 이 키를 분실 하면 tooreturn toothis 섹션이 있는을 새 키를 만듭니다. 이 키의 비밀을 유지합니다. 키를 가진 사람은 누구나 데이터에 액세스할 수 있습니다.
   > 
   > 
4. Hello에 **속성** 섹션을 복사 hello **클라이언트 ID**를 안전한 위치에 붙여넣습니다. 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a>TooMicrosoft 그래프 및 쿼리 hello Id 위험 이벤트 API 인증
이 시점에서 다음 항목이 만들어 집니다.

* 위의 복사 hello 클라이언트 ID
* 위의 복사 hello 키
* hello 테 넌 트의 도메인 이름

tooauthenticate, post 보내기 요청 너무`https://login.microsoft.com` hello 본문에서 매개 변수 뒤 hello로:

* grant_type: “**client_credentials**”
* resource: “**https://graph.microsoft.com**”
* client_id: <your client ID>
* client_secret: <your key>

> [!NOTE]
> Hello에 대 한 tooprovide 값이 필요 하면 **client_id** 및 hello **client_secret** 매개 변수입니다.
> 
> 

성공하면 인증 토큰을 반환합니다.  
toocall hello API 매개 변수 다음 hello로는 헤더를 만듭니다.

    `Authorization`=”<token_type> <access_token>"


을 인증할 때 토큰을 반환 하는 hello에 hello 토큰 유형이 및 액세스 토큰을 찾을 수 있습니다.

API url 요청 toohello로이 헤더를 보냅니다.`https://graph.microsoft.com/beta/identityRiskEvents`

hello 응답 성공 하면 컬렉션 id의 위험 이벤트 이며 hello 구문 분석 하 고 적절 하 게 처리 될 수 있는 OData JSON 형식으로의 데이터에 연결 합니다.

다음은 샘플 코드를 인증 하 고 Powershell을 사용 하 여 hello API를 호출 합니다.  
클라이언트 ID, 키 및 테넌트 도메인을 추가합니다.

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a>다음 단계
축 하 합니다, 프로그램 첫 번째 호출 tooMicrosoft 그래프를 방금 만든!  
이제 identity 위험 이벤트를 쿼리 하 고 필요에 맞게 적절히 hello 데이터를 사용 하 여 수 있습니다.

Microsoft Graph에 대해 자세히 toolearn toobuild 응용 프로그램을 사용 하 여 Graph API를 hello 하는 방법을 확인 hello [설명서](https://graph.microsoft.io/docs) hello에 훨씬 더 많은 및 [Microsoft Graph 사이트](https://graph.microsoft.io/)합니다. 또한 있는지 toobookmark hello 확인 [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) hello 그래프에서 사용할 수 있는 Identity 보호 Api를 모두 나열 하는 페이지입니다. Id 보호 API 통해 새로운 방식으로 toowork, 추가 하는 대로 해당 페이지에 표시 됩니다.

## <a name="additional-resources"></a>추가 리소스
* [Azure Active Directory ID 보호](active-directory-identityprotection.md)
* [Azure Active Directory ID 보호에서 검색한 위험 이벤트의 유형](active-directory-identityprotection-risk-events-types.md)
* [Microsoft Graph](https://graph.microsoft.io/)
* [Microsoft Graph 개요](https://graph.microsoft.io/docs)
* [Azure AD ID 보호 서비스 루트](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

