---
title: "Azure Active Directory에서 앱, 사용 권한 및 동의 | Microsoft Docs"
description: "Azure AD Connect는 온-프레미스 디렉터리와 Azure Active Directory를 통합니다. 이렇게 하면 tooprovide Office 365, Azure 및 SaaS 응용 프로그램에 대 한 일반 id를 Azure AD와 통합 되어 있습니다."
keywords: "Azure AD Connect 란 소개 tooAzure AD, 응용 프로그램, active directory를 설치 합니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a>Azure Active Directory에서 앱, 사용 권한 및 동의
Azure Active Directory 내에서 응용 프로그램 tooyour 디렉터리를 추가할 수 있습니다.  hello 응용 프로그램은 응용 프로그램의 hello 종류에 따라 달라질 수 있습니다.  hello 클래식 포털에서 tooview 응용 프로그램 디렉터리 선택 하 고 응용 프로그램을 선택 합니다.

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.

## <a name="types-of-apps"></a>앱 형식

1. **단일 테넌트 앱** </br>
    - **단일 테 넌 트 앱** -주로 tooas-업무 (LOB) 응용 프로그램을 의미 합니다. 즉 hello 경우 자체 앱을 개발 하 고, 조직 내의 누군가 및 hello 조직 toobe toohello 응용 프로그램에서 수 toosign에 사용자가 있습니다.
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - **응용 프로그램 프록시 앱** -Azure AD 응용 프로그램 프록시를 통해 온-프레미스 응용 프로그램을 노출 하는 경우 단일 테 넌 트 응용 프로그램 (더하기 toohello 응용 프로그램 프록시 서비스)에서 테 넌 트에 등록 되어 있습니다. 이 앱은 모든 클라우드 상호 작용(예: 인증)에 대한 온-프레미스 응용 프로그램을 나타냅니다. (앱 프록시에는 Azure AD Basic 이상이 필요)


2. **다중 테넌트 앱**
    - **다른 사용자에 동의할 수 있는 다중 테 넌 트 앱** 처럼 너무 "조직에서 개발 하는 단일 테 넌 트 앱"입니다. (외에도 hello 앱 자체에서 hello 논리) hello 주요 차이점 다른 테 넌 트의 사용자 tooand 로그인 toohello 응용 프로그램에 동의할 수도 수입니다.</br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - **Contoso에서 동의할 수 있고 다른 사용자가 개발하는 다중 테넌트 앱**. (또는 간략히 "동의한 앱") "다중 테 넌 트 앱 개발 하 고, 조직" hello 긍 적 적인 측면입니다. 다른 조직에서 개발 하는 다중 테 넌 트 응용 프로그램 때 조직의 사용자가 동의 toohello 앱을 업데이트 하 고 tooit 로그인 수 있습니다.
    - **Microsoft 자사 앱** - Microsoft 서비스를 나타내는 앱입니다. 동의는 hello 서비스에 가입 하는 hello 팩트에 의해 이루어집니다. 경우에 따라 특별 한 UX 및가 access toohello 앱 관련 된 정책을 설정할 때 주로 사용 되는 특정 자사 응용 프로그램에 대 한 논리</br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - **사전 통합된 앱** -hello 추가할 수 있는 Azure AD 앱 갤러리에서에서 제공 되는 앱 tooyour 디렉터리 tooprovide 단일 로그온 (및 경우에 따라 프로 비전) toopopular SaaS 앱.
    - **Azure AD single sign-on**: SAML 2.0 또는 OpenID Connect와 같은 지원되는 로그인 프로토콜을 통해 Azure AD와 통합할 수 있는 앱에 대한 "실제" SSO입니다. hello 마법사 설정 하는 과정을 안내 합니다.
    - **암호 single sign on**: Azure AD hello 앱에 대 한 hello 사용자의 자격 증명을 안전 하 게 저장 하 고 hello 자격 증명은 "" hello 로그인 폼에 의해 삽입 hello Azure AD 응용 프로그램 액세스 브라우저 확장 합니다. “암호 보관”이라고도 합니다.

## <a name="permissions"></a>권한

앱 등록 될 때 hello 앱 등록 (즉, hello 개발자)를 수행 하는 hello 사용자에 액세스 해야 하는 어떤 권한을 hello 앱 및 리소스를 정의 합니다. (hello 리소스가, 다른 앱으로 정의 된 자체입니다.) 예를 들어 앱 hello "Office 365 Exchange Online" 리소스에에서 대 한 hello "hello 로그인 한 사용자로는 사서함 액세스" 권한이 필요는 상태는 누군가가 메일 판독기 응용 프로그램을 구축:
    
![](media/active-directory-apps-permissions-consent/apps6.png)

하나의 응용 프로그램 (클라이언트 hello) toorequest 특정 권한 다른 응용 프로그램 (hello 리소스) 으로부터 hello 리소스 응용 프로그램의 hello 개발자는 존재 하는 hello 사용 권한을 정의 합니다. Microsoft, hello "Office 365 Exchange Online" 리소스 앱의 hello 소유자 예제에서는 "hello 로그인 한 사용자로는 사서함 액세스" 이라는 권한을 정의 했습니다.

사용 권한을 정의할 때는 hello 권한 승인할 수, 또는 관리자 동의 요구 하면 hello 앱 개발자 정의 해야 합니다. 이렇게 하면 개발자가 tooallow 사용자 tooconsent 자신의 tooapps만 중요도 낮은 권한 요청에 있지만 admins tooconsent toomore 중요 한 사용 권한이 필요 합니다. 예를 들어, "Azure Active Directory" 리소스 응용 프로그램을 hello, 정의 않으므로 사용자가 동의할 수 tooapps, 제한 된 읽기 전용 권한을 요청 합니다.  그러나 관리자 동의에는 전체 읽기 권한 및 전체 쓰기 권한이 필요합니다.

네이티브 클라이언트는 인증되지 않으므로 네이티브 클라이언트 앱으로 정의된 앱은 위임된 권한만 요청할 수 있습니다. 따라서 토큰을 획득할 때는 실제 관련된 사용자여야 합니다. Web Apps 및 Web API(기밀 클라이언트)는 액세스 토큰을 가져올 때 항상 Azure AD로 인증해야 합니다. 응용 프로그램 전용 권한 요청의 hello 가능성도 가집니다 의미 합니다. 예를 들어 한 백 엔드 서비스에 tooauthenticate tooanother 백 엔드 서비스가 필요 합니다. 앱 전용 권한을 요청하는 응용 프로그램은 관리자의 동의를 항상 필요로 합니다.

요약:



- 응용 프로그램 (클라이언트)에 다른 앱 (리소스)에 대 한 필요한 hello 권한을 상태입니다.
- (리소스) 응용 프로그램 권한을 노출된 tooother 앱 (클라이언트) 상태입니다.
- 권한은 앱 전용 권한이거나 위임된 권한일 수 있습니다.
- 위임된 권한은 “사용자 동의 허용” 또는 “관리자 동의 필요”로 표시할 수 있습니다.
- 응용 프로그램 (선언 노출 하는 권한을)를 여는 리소스 또는 둘 다로 (선언 하 여 필요 하다 고 권한 tooa 리소스)을 클라이언트로 작동할 수 있습니다.

## <a name="controls"></a>컨트롤

hello 다음은이 모든 동작에 사용할 수 있는 hello 다른 관리 컨트롤의 목록입니다. 컨트롤에서 hello 클래식 포털에 액세스할 수 있습니다 admin 님 안녕하세요 hello 디렉터리에서 구성 합니다.

![](media/active-directory-apps-permissions-consent/apps7.png)

hello Azure 포털에서 **관리**, **사용자 설정**합니다.

![](media/active-directory-apps-permissions-consent/apps11.png)



- Tooapps는 사용자가 동의할 수 있는지 여부를 제어할 수 있습니다.

Hello 클래식 포털에서 선택 **사용자가 응용 프로그램 사용 권한 tooaccess 데이터가 발생할 수 있습니다.**
![](media/active-directory-apps-permissions-consent/apps8.png)

Hello Azure 포털에서에서 선택 **사용자가 앱 tooaccess 데이터 허용 수**합니다.
![](media/active-directory-apps-permissions-consent/apps12.png)



- 사용자가 자신의 단일 테 넌 트 LOB 앱을 등록할 수 있는지 여부를 제어할 수 있습니다: hello 클래식 포털 Select에서 **사용자 통합 된 응용 프로그램을 추가할 수 있습니다.**
![](media/active-directory-apps-permissions-consent/apps9.png)

Hello Azure 포털에서에서 선택 **사용자가 앱 tooaccess 데이터 허용 수**합니다.
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
>사용자가 단일 테 넌 트 LOB 앱 tooregister 못하게, 경우에 제한은 toowhat를 등록할 수 있습니다.  
>예를 들어 디렉터리 관리자가 아닌 개발자는 다음 제한이 있습니다.
>
>- 사용자는 단일 테넌트 앱을 다중 테넌트 앱으로 만들 수 없습니다.
>- 단일 테 넌 트 LOB 앱을 등록할 때 사용자가 응용 프로그램 전용 권한을 tooother 응용 프로그램을 요청할 수 없습니다.
>- 단일 테 넌 트 LOB 앱을 등록할 때 사용자가 이러한 사용 권한 관리 동의가 필요한 경우 위임 된 사용 권한을 tooother 응용 프로그램을 요청할 수 없습니다.
>- 사용자가 변경 내용을 tooapps에 맞지 않음을의 소유자를 만들 수 없습니다.



- 사용자가 스스로 암호 SSO(즉, “암호 보관”)를 사용하는 사전 통합된 앱을 추가할 수 있는지 여부를 제어할 수 있습니다. ![](media/active-directory-apps-permissions-consent/apps10.png)



- 응용 프로그램에 액세스할 수 있는 조건(즉, 조건부 액세스)을 제어할 수 있습니다. 주의 toohello 클라이언트 응용 프로그램 및 toohello 리소스 응용 프로그램을 모두 적용 됩니다. 따라서 해당 hello "Office 365 Exchange Online" 앱 준수 하는 컴퓨터에서 액세스할 수만 조건부 액세스 정책을 설정 하면 말하십시오.  이 정책은 사용자가 toouse 권한을 tooExchange 온라인를 요청 하는 클라이언트 응용 프로그램에도 종료 됩니다.



- 앱에 알림을 사용 하는 승인된 tooand 된 표시를 해야 합니다.

1.  사용자가 tooan 응용 프로그램을 승인 하면 hello 테 넌 트에 ServicePrincipal 개체가 만들어집니다. ServicePrincipal 만들기가 hello 감사 보고서에 포함 됩니다.
2.  사용자 로그인 활동 보고서는 응용 프로그램 hello 사용자가 로그인을 알려 줍니다. 

## <a name="example"></a>예제

예를 들어 테 넌 트의 사용자가 로그인 할 알았습니다 hello "Office 365 용 FabrikamMail" 앱을 보겠습니다. “FabrikamMail”은 “Fabrikam, Inc.”에서 게시한 Android용 메일 읽기 프로그램 앱입니다. Hello로 설정 됨 "다중 테 넌 트 앱 Contoso 것에 동의할 수 있는 다른 개발"입니다.

사용자가 tooconsent 허용 하는 경우 처음으로 로그인 할 동의 프롬프트 hello를 가져올 있습니다.![](media/active-directory-apps-permissions-consent/apps14.png)

"사서함 액세스"은 "Office 365 Exchange Online" (즉, 교환)에 의해 노출 hello "hello 로그인 한 사용자로는 사서함 액세스" 권한을 hello 사용자 용 동의 문자열입니다.

Office 365에 등록할 때 추가 된 교환 (hello 리소스)에 대 한 hello ServicePrincipal 개체를 조회 하 여 hello 사용 권한을 볼 수 있습니다. 테 넌 트 기록 다양 한 옵션 및 구성 하는 데 사용 되는 hello 앱의 "인스턴스" hello ServicePrincipal 개체의 생각할 수 있습니다.  Hello를 사용 하 여 볼 수 있습니다 `Get-AzureADServicePrincipal` PowerShell에서 합니다.

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

동의는 hello 사용자가 "동의"를 클릭할 때 시작 됩니다. 첫째, hello 테 넌 트의 "Office 365 용 FabrikamMail"에 대 한 ServicePrincipal 개체가 만들어집니다. ServicePrincipal hello는 다음과 같습니다.

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

Tooan 앱 승인 hello 다음은 Oauth2PermissionGrant 연결을 만듭니다.
  
- hello 사용자 개체
- hello 클라이언트 응용 프로그램 서비스 사용자 이름 (SPN)
- hello 리소스 응용 프로그램 서비스 사용자 이름 (SPN)
- hello 리소스 응용 프로그램에서 권한입니다.  

Hello FabrikamMail의 경우에서 다음과 같은이:

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

(**ClientId** FabrikamMail의 서비스 보안 주체 개체 id (만들어진 방금 하나 hello) **PrincipalId** hello 사용자 개체 ID입니다 (hello 사용자가 동의한 것으로 간주), **ResourceId**은 Exchange의 서비스 보안 주체 개체 ID, 범위는 Exchange에 승인 된 하는 hello 권한).

사용자가 tooconsent을 허용 하지 않는 경우 사용 권한이 표시 되는 화면을 반드시 입력 해야 표시 됩니다.

