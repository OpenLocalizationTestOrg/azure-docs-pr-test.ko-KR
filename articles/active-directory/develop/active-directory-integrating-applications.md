---
title: "Azure Active Directory와 응용 프로그램 aaaIntegrating | Microsoft Docs"
description: "Tooadd, 업데이트 또는 Azure Active Directory (Azure AD)에 응용 프로그램을 제거 방법에 대 한 세부 정보입니다."
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: mbaldwin
ms.assetid: ae637be5-0b71-4b1e-b1fe-b83df3eb4845
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: lenalepa
ms.custom: aaddev
ms.reviewer: luleon
ms.openlocfilehash: c6bf1123bb3a4d78b55c1c55558e684fb844e687
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-applications-with-azure-active-directory"></a>Azure Active Directory와 응용 프로그램 통합
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

상업용 클라우드 서비스 또는 Azure Active Directory (Azure AD) tooprovide 보안 로그인 및 권한 부여에 대 한 통합 될 수 있는 비즈니스 응용 프로그램을 개발할 수 엔터프라이즈 개발자 및 소프트웨어-as a service (SaaS) 공급자가 서비스입니다. toointegrate 응용 프로그램 또는 서비스를 Azure AD와 개발자는 hello Azure 클래식 포털을 통해 Azure AD와 응용 프로그램에 대 한 세부 정보 hello 먼저 등록 해야 합니다.

이 문서에서는 어떻게 tooadd, 업데이트 또는 Azure AD에서 응용 프로그램을 제거 합니다. Hello 여러 유형의 방법을 Azure AD와 통합 될 수 있는 응용 프로그램에 대해 배우게 됩니다 tooconfigure 응용 프로그램 tooaccess 웹 Api와 같은 다른 리소스 등입니다.

등록 된 응용 프로그램 및 hello 관계를 나타내는 hello 두 Azure AD 개체에 대해 자세히 toolearn 참조 [응용 프로그램 개체 및 서비스 주체 개체](active-directory-application-objects.md); toolearn 브랜딩 지침 hello에 대 한 자세한 있습니다 Azure Active Directory와 응용 프로그램을 개발할 때 사용 하 여, 참조 해야 [통합 된 응용 프로그램에 대 한 브랜딩 지침](active-directory-branding-guidelines.md)합니다.

## <a name="adding-an-application"></a>응용 프로그램 추가
Azure AD의 toouse hello 기능을가 하는 모든 응용 프로그램은 Azure AD 테 넌 트에 먼저 등록 되어야 합니다. 여기서는 hello URL과 같은 응용 프로그램에 대 한 Azure AD 세부 정보를 제공 합니다.이 등록 프로세스에서는, 사용자가 인증 된 후 URL toosend 회신 hello, hello hello 앱 및 기타 등등을 식별 하는 URI입니다.

방금 Azure AD에서 사용자에 대 한 toosupport 로그인 필요로 하는 웹 응용 프로그램을 빌드하는 경우 단순히 아래 hello 지침을 따를 수 있습니다. Tooaccess Azure AD 테 넌 트에서 응용 프로그램 자격 증명이 나 권한을 tooaccess tooa 웹 API 또는 다른 tooallow 사용자가 필요한 경우, 참조 [응용 프로그램 업데이트](#updating-an-application) 섹션 toocontinue 응용 프로그램을 구성 합니다.

### <a name="tooregister-a-new-application-in-hello-azure-portal"></a>tooregister hello Azure 포털에서에서 새 응용 프로그램
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello hello 페이지의 맨 위 오른쪽 모서리에서 사용자 계정을 선택 하 여 Azure AD 테 넌 트를 선택 합니다.
3. Hello 왼쪽의 탐색 창에서 선택 **더 서비스**, 클릭 **앱 등록**를 클릭 하 고 **추가**합니다.
4. Hello 화면에 따라 수행 하 고 새 응용 프로그램을 만듭니다. 웹 응용 프로그램 또는 네이티브 응용 프로그램에 대한 구체적인 예제를 원하는 경우 [빠른 시작](active-directory-developers-guide.md)을 확인합니다.
  * 웹 응용 프로그램에서는 hello 제공 **로그온 URL**, hello 응용 프로그램의 기준 URL을 설정 하는 예: 사용자가 로그인이 변수인 `http://localhost:12345`합니다.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * 네이티브 응용 프로그램에 제공 된 **리디렉션 URI**, tooreturn 토큰 응답을 사용 하 여 Azure AD는 합니다. 값 특정 tooyour 응용 프로그램을 입력 합니다. 예:`http://MyFirstAADApp`
5. Azure AD 할당 hello 응용 프로그램 id입니다. 고유한 클라이언트 식별자, 응용 프로그램 등록을 마친 후 응용 프로그램을 추가 하 고 toohello 빠른 시작 페이지에 대 한 응용 프로그램에 연결 됩니다. 인지 여부에 따라 응용 프로그램을 웹 네이티브 응용 프로그램을 각기 다른 옵션이 표시 됩니다 tooadd 추가 기능 tooyour 응용 프로그램입니다. 응용 프로그램 추가 되 면에 다른 응용 프로그램의 액세스 웹 Api에는 응용 프로그램 tooenable 사용자 toosign 업데이트를 시작 하거나 다중 테 넌 트 응용 프로그램 (응용 프로그램 다른 조직 tooaccess 디렉션할 수 있음)를 구성할 수 있습니다.

> [!NOTE]
> 기본적으로 hello 새로 만든 응용 프로그램 등록에는 사용자 디렉터리 toosign tooyour 응용 프로그램에서에서 구성 된 tooallow 사용자입니다.
> 
> 

## <a name="updating-an-application"></a>응용프로그램 업데이트
Toobe 업데이트를 할 수 있는 응용 프로그램을 Azure AD와 등록 후 tooprovide tooweb Api에 액세스, 등 다른 조직에서 사용 가능 합니다. 이 섹션에서는 다양 한 방법으로는 할 수 있습니다 tooconfigure 응용 프로그램을 추가로 설명 합니다. 처음부터 시작 하겠습니다 hello 동의 프레임 워크에 대해 간략하게 중요 toounderstand 변수가 조직 또는 다른 조직에는 개발자가 클라이언트 응용 프로그램에서 사용 될 리소스/API 응용 프로그램을 작성 하는 경우.

Azure AD에서 작동 방식으로 인증 hello에 대 한 자세한 내용은 참조 하십시오 [Azure AD의 인증 시나리오](active-directory-authentication-scenarios.md)합니다.

### <a name="overview-of-hello-consent-framework"></a>Hello 승인 프레임 워크 개요
Azure AD의 승인 프레임 워크 쉽게 toodevelop 다중 테 넌 트 웹 있고 tooaccess 해야 하는 네이티브 클라이언트 응용 프로그램 웹 Api로 Azure AD 테 넌 트, hello 등록 된 hello 클라이언트 응용 프로그램 하나에서 다른 보호 합니다. Tooyour 웹 Api를 소유 하는 또한, 이러한 웹 Api hello Microsoft Graph API (Azure Active Directory tooaccess, Intune 및 Office 365의 서비스) 및 다른 Microsoft 서비스 Api 포함 합니다. hello 프레임 워크는 사용자 또는 toobe 해당 디렉터리에 등록, 디렉터리 데이터에 액세스 될 수 있습니다에 게 요청 하는 동의 tooan 응용 프로그램 관리자 기반으로 합니다.

예를 들어 웹 클라이언트 응용 프로그램에서 Office 365 사용자 hello에 대 한 일정 정보 tooread 경우, 해당 사용자에 필요한 tooconsent toohello 클라이언트 응용 프로그램이 됩니다. 사용자가 승인을 후 hello 클라이언트 응용 프로그램 수 toocall hello Microsoft Graph API hello 사용자 대신 되며 필요에 따라 hello 일정 정보를 사용 합니다. hello [Microsoft Graph API](https://graph.microsoft.io) (예: 일정 및 메시지 교환, 사이트 및 SharePoint, OneDrive에서 문서, OneNote, Planner에서 통합 문서에서 작업에서에서 전자 필기장의 목록에서 Office 365에 대 한 액세스 toodata를 제공 합니다. Excel, 등) 뿐만 아니라 사용자와 Azure AD에서 그룹 및 더 많은 Microsoft 클라우드 서비스에서 다른 데이터 개체입니다. 

hello 승인 프레임 워크는 OAuth 2.0 및 다양 한 해당 흐름을 기반으로 하며, 권한 부여 코드와 같이 권한 부여 및 클라이언트 자격 증명 부여를 공용 또는 기밀 클라이언트를 사용 하 여 합니다. OAuth 2.0을 사용 하 여 Azure AD는 가능한 toobuild 다양 한 유형의 같은 클라이언트 응용 프로그램, 휴대폰, 태블릿, 서버 또는 웹 응용 프로그램 및 필요한 toohello 리소스 액세스 합니다.

Hello 승인 프레임 워크에 대 한 정보를 자세한 참조 [Azure AD의 OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx), [Azure AD의 인증 시나리오](active-directory-authentication-scenarios.md)을 통해 권한이 부여 된 액세스 tooOffice 365 가져오기에 대 한 정보 Microsoft Graph 참조 [Microsoft Graph에 앱 인증](https://graph.microsoft.io/docs/authorization/auth_overview)합니다.

#### <a name="example-of-hello-consent-experience"></a>Hello 승인 환경의 예
hello 다음 단계에서는 설명 hello 응용 프로그램 개발자와 사용자 모두에 대 한 hello 승인 환경이 작동 하는 방식입니다.

1. Hello Azure 포털에서에서 웹 클라이언트 응용 프로그램 구성 페이지에서 hello 필요한 사용 권한 섹션에서에서 hello 메뉴를 사용 하 여 응용 프로그램에 필요한 hello 사용 권한을 설정 합니다.
   
    ![사용 권한 tooother 응용 프로그램](./media/active-directory-integrating-applications/requiredpermissions.png)
2. 응용 프로그램의 권한이 업데이트 되었고, hello 응용 프로그램을 실행 하며 사용자가 toouse에 대 한 것 hello에 대 한 처음으로 고려 합니다. Hello 응용 프로그램 액세스 또는 새로 고침 토큰, hello 응용 프로그램을 이미 획득 하지는 경우 새 액세스 및 새로 고침 토큰 toogo tooAzure AD의 권한 부여 끝점 tooobtain tooacquire 사용된 될 수 있는 인증 코드를 필요 합니다.
3. Hello 사용자가 아직 인증 되지 증명이 tooAzure AD에서에서 toosign을 요구 합니다.
   
    ![TooAzure AD 사용자 또는 관리자 로그인](./media/active-directory-integrating-applications/usersignin.png)
4. Hello 사용자가 로그인 한 후 Azure AD hello 사용자 toobe 승인 페이지를 표시 해야 하는 경우를 결정 합니다. 이 결정은 hello 사용자 (또는 해당 조직의 관리자)에 이미 hello 응용 프로그램 동의 부여 여부에 따라 됩니다. 동의 이미 부여 되지 않은 경우 Azure AD는 사용자 동의 hello 묻습니다 하 고 toofunction 필요한 hello 필요한 권한을 표시 합니다. hello 사용 권한 집합이 hello 승인 대화 상자에 표시 되는 Azure 포털 hello hello 위임 된 권한에서 선택한 항목으로 같은 hello 됩니다.
   
    ![사용자 동의 경험](./media/active-directory-integrating-applications/consent.png)
5. Hello 사용자 동의 허용 하는 후 교환된 tooacquire 액세스 토큰 및 새로 고침 토큰 수 있는 tooyour 응용 프로그램을 인증 코드에 반환 됩니다. 이 흐름에 대 한 자세한 내용은 참조 hello [웹 응용 프로그램 API tooweb 섹션](active-directory-authentication-scenarios.md#web-application-to-web-api) 섹션 [Azure AD의 인증 시나리오](active-directory-authentication-scenarios.md)합니다.

6. 관리자로 서 tooan 응용 프로그램의 모든 hello 사용자를 대신 하 여 위임 된 권한이 테 넌 트에 동의할 수 있습니다. 이렇게 하면 hello 승인 대화 상자 hello 테 넌 트의 모든 사용자에 대 한 메시지가 표시 되지 것입니다. Hello에서 이렇게 하려면 [Azure 포털](https://portal.azure.com) 응용 프로그램 페이지에서. Hello에서 **설정** 블레이드 응용 프로그램에 대 한 클릭 **필요한 권한** hello에서을 클릭 하 고 **사용 권한 부여** 단추입니다. 

    ![명시적 관리자 동의를 위한 권한 부여](./media/active-directory-integrating-applications/grantpermissions.png)
    
> [!NOTE]
> Hello를 사용 하 여 명시적인 동의가 부여 **사용 권한 부여** 단추는 동의 없으면 실패 합니다 동의 확인 프롬프트 없이 hello 액세스 토큰을 요청 하는 대로 ADAL.js를 사용 하 여 단일 페이지 응용 프로그램 (SPA)에 대 한 현재 필요 이미 부여 합니다.   

### <a name="configuring-a-client-application-tooaccess-web-apis"></a>클라이언트 응용 프로그램 tooaccess 웹 Api를 구성합니다.
웹/기밀 클라이언트 응용 프로그램 toobe 수 tooparticipate 인증이 필요한 (및 액세스 토큰을 가져올) 하는 권한 부여 권한 부여 흐름에 대 한 순서로 보안 자격 증명을 설정 해야 합니다. hello hello Azure 포털에서 지원 되는 기본 인증 방법은 클라이언트 ID + 대칭 키입니다. 이 섹션 클라이언트의 자격 증명 hello 구성 단계 필요 tooprovide hello 비밀 키를 설명 합니다.

또한 클라이언트 수 있다는 웹 API 액세스에 의해 노출은 리소스 응용 프로그램 (예: Microsoft Graph API), hello 승인 프레임 워크 hello 클라이언트 hello 권한 부여를 요청 하는 필요한 경우에 따라 hello 사용 권한을 가져옵니다 방법을 사용 하면 합니다. 기본적으로 모든 응용 프로그램은 hello Azure AD "Enable 로그온 및 사용자 프로필 읽기" 권한이 이미 기본적으로 선택 된 Azure Active Directory (Graph API) 및 Azure 서비스 관리 API에서 사용 권한을 선택할 수 있습니다. 클라이언트 응용 프로그램을 Office 365 Azure AD 테넌트에 등록하는 경우 SharePoint 및 Exchange Online의 웹 API 및 권한도 선택할 수 있습니다. 선택할 수 있습니다 [두 가지 유형의 사용 권한](active-directory-dev-glossary.md#permissions) 드롭 다운 메뉴 다음 toohello 필요한 웹 API hello에:

* 응용 프로그램 사용 권한: 클라이언트 응용 프로그램 자체 (사용자 컨텍스트 없이)로 직접 tooaccess hello 웹 API에 필요 합니다. 이 유형의 권한은 관리자의 동의가 필요하며 네이티브 클라이언트 응용 프로그램에 대해 사용할 수 없습니다.
* 위임 된 권한: 클라이언트 응용 프로그램 액세스가 hello 선택한 사용 권한 제한 하면서도 사용자 로그인 hello로 tooaccess hello 웹 API 필요 합니다. 이 유형의 사용 권한 hello 하도록 권한이 구성 된 관리자의 승인이 필요 하지 않으면 사용자가 부여할 수 있습니다. 

> [!NOTE]
> 위임 된 권한 tooan 응용 프로그램을 추가 부여 하지 않습니다 자동으로 동의 toohello 사용자 hello 테 넌 트 내에서 hello Azure 클래식 포털에서. hello 사용자가 동의 해야 함 수동으로 추가 하는 hello 런타임 시, 사용 권한 위임에 대 한 관리자에 게 hello 클릭 하지 않는 한 **사용 권한 부여** hello에서 단추 **필요한 권한** 섹션 hello hello Azure 포털에서에서 응용 프로그램 페이지입니다. 

#### <a name="tooadd-credentials-or-permissions-tooaccess-web-apis"></a>웹 Api tooadd 자격 증명 또는 사용 권한 tooaccess
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello hello 페이지의 맨 위 오른쪽 모서리에서 사용자 계정을 선택 하 여 Azure AD 테 넌 트를 선택 합니다.
3. Hello 위쪽 메뉴에서 선택 **Azure Active Directory**, 클릭 **앱 등록**, tooconfigure 원하는 hello 응용 프로그램을 클릭 하 고 있습니다. 이 됩니다 toohello 응용 프로그램의 빠른 시작 페이지에서 이동으로 hello 응용 프로그램에 대 한 hello 설정 블레이드를 엽니다.
4. 웹 응용 프로그램의 자격 증명에 대 한 비밀 키 tooadd hello 설정 블레이드에서 hello "키" 섹션을 클릭 합니다.  
   
   * 키에 대한 설명을 추가하고 기간으로 1년 또는 2년을 선택합니다. 
   * hello 구성 변경 내용을 저장 한 후 hello 맨 오른쪽 열 hello 키 값을 포함 됩니다. 있는지 toocome 다시 toothis 섹션과 복사 맞추면 저장을 위한 해야 사용할 런타임 시 인증 하는 동안 클라이언트 응용 프로그램에서 합니다.
5. 사용자 클라이언트에서 tooadd 권한이 tooaccess 리소스 Api hello 설정 블레이드에서 hello "필요한 사용 권한" 섹션을 클릭 합니다. 
   
   * 먼저, hello "추가" 단추를 클릭 합니다.
   * 리소스에서 toopick 원하는 유형의 tooselect hello "API 선택"을 클릭 합니다.
   * 사용 가능한 Api의 hello 목록에서 찾아보거나 hello 사용 가능한 리소스를 응용 프로그램에서 디렉터리의 웹 API를 노출 하는 검색 상자 tooselect hello를 사용 하십시오. 관심 있는 다음 클릭 hello 리소스 클릭 **선택**합니다.
   * Toohello를 이동할 수를 선택 하 고 나면 **Select 권한만** 메뉴에서 응용 프로그램에 대 한 hello "응용 프로그램 사용 권한" 및 "위임 된 권한"을 선택할 수 있는 합니다.
   
6. 완료 되 면 hello 클릭 **수행** 단추입니다.

> [!NOTE]
> 클릭 하 여 hello **수행** 디렉터리에서 응용 프로그램 hello 권한에 따라 사용자가 구성한 tooother 응용 프로그램에도 자동으로 단추 hello 사용 권한을 설정 합니다.  Hello 응용 프로그램 확인 하 여 이러한 응용 프로그램 권한을 볼 수 있습니다 **설정을** 블레이드입니다.
> 
> 

### <a name="configuring-a-resource-application-tooexpose-web-apis"></a>리소스 응용 프로그램 tooexpose 웹 Api를 구성합니다.
Web API를 개발 하 고 액세스를 노출 하 여 사용 가능한 tooclient 응용 프로그램을 확인 수 [범위](active-directory-dev-glossary.md#scopes) 및 [역할](active-directory-dev-glossary.md#roles)합니다. 것 처럼 다른 Microsoft 웹 Api를 hello Graph API를 포함 하 여 hello 및 Office 365 Api hello 올바르게 구성 된 웹 API는 사용할 수는 있습니다. 액세스 범위와 역할은 [응용 프로그램의 매니페스트](active-directory-dev-glossary.md#application-manifest)를 통해 공개되며, 이 매니페스트는 응용 프로그램의 ID 구성을 나타내는 JSON 파일입니다.  

다음 섹션 hello hello 리소스 응용 프로그램의 매니페스트를 수정 하 여 tooexpose 액세스 범위가 어떻게에 표시 됩니다.

#### <a name="adding-access-scopes-tooyour-resource-application"></a>액세스 범위 tooyour 리소스 응용 프로그램 추가
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello hello 페이지의 맨 위 오른쪽 모서리에서 사용자 계정을 선택 하 여 Azure AD 테 넌 트를 선택 합니다.
3. Hello 위쪽 메뉴에서 선택 **Azure Active Directory**, 클릭 **앱 등록**, tooconfigure 원하는 hello 응용 프로그램을 클릭 하 고 있습니다. 이 됩니다 toohello 응용 프로그램의 빠른 시작 페이지에서 이동으로 hello 응용 프로그램에 대 한 hello 설정 블레이드를 엽니다.
4. 클릭 **매니페스트** hello 응용 프로그램 페이지 tooopen hello 인라인 매니페스트 편집기에서. 
5. 다음 JSON 코드 조각은 hello로 "oauth2Permissions" 노드를 대체 합니다. 이 조각은 tooexpose의 형식을 클라이언트 응용 프로그램 리소스 소유자 toogive 허용 "사용자 가장" 이라는 범위 tooa 리소스 액세스를 위임 하는 방법의 예시입니다. 사용자의 응용 프로그램에 대 한 hello 텍스트 및 값을 변경 해야 합니다.
   
        "oauth2Permissions": [
        {
            "adminConsentDescription": "Allow hello application full access toohello Todo List service on behalf of hello signed-in     user",
            "adminConsentDisplayName": "Have full access toohello Todo List service",
            "id": "b69ee3c9-c40d-4f2a-ac80-961cd1534e40",
            "isEnabled": true,
            "type": "User",
            "userConsentDescription": "Allow hello application full access toohello todo service on your behalf",
            "userConsentDisplayName": "Have full access toohello todo service",
            "value": "user_impersonation"
            }
        ],
   
    id 값이 hello를 사용 하 여 만드는 새 생성 된 GUID 이어야 합니다는 [GUID 생성 도구](https://msdn.microsoft.com/library/ms241442%28v=vs.80%29.aspx) 또는 프로그래밍 방식으로 합니다. Hello 웹 API에 의해 노출 되는 hello 권한에 대 한 고유 식별자를 나타냅니다. 클라이언트 구성 적절 하 게 되 면 toorequest 액세스 tooyour 웹 API 및 호출 hello 웹 API, 값을 가진 hello 범위 (scp) 클레임 집합 toohello 위의 user_impersonation에이 경우에 OAuth 2.0 JWT 토큰을 제시 합니다.
   
   > [!NOTE]
   > 추가 범위를 나중에 필요한 대로 노출할 수 있습니다. 웹 API에서 다양한 기능과 관련된 여러 범위를 공개할 수도 있음을 고려하세요. 이제 수신 hello OAuth 2.0 JWT 토큰에 대 한 액세스 toohello hello 범위 (scp)를 사용 하 여 web API 클레임을 제어할 수 있습니다.
   > 
   > 
6. 클릭 **저장** toosave hello 매니페스트 합니다. 웹 API는 이제 toobe 디렉터리에 다른 응용 프로그램에서 구성 되었습니다.

#### <a name="tooverify-hello-web-api-is-exposed-tooother-applications-in-your-directory"></a>tooverify hello 웹 API 노출된 tooother 디렉터리에서 응용 프로그램은
1. Hello 최상위 메뉴를 클릭 **앱 등록**선택, hello 원하는 클라이언트 응용 프로그램 tooconfigure 액세스 toohello 웹 API를 원하고 toohello 설정 블레이드를 탐색 합니다.
2. Hello에서 **필요한 권한** 섹션에 대 한 권한을 공개 hello 웹 API를 선택 합니다. Hello 위임 된 권한 드롭 다운 메뉴에서 새 사용 권한 hello를 선택 합니다.

![해야 할 일 목록 권한이 표시됨](./media/active-directory-integrating-applications/todolistpermissions.png)

#### <a name="more-on-hello-application-manifest"></a>응용 프로그램 매니페스트 hello에 대 한 자세한
hello 응용 프로그램 매니페스트는 실제로 설명한 hello API 액세스 범위를 포함 하 여, Azure AD 응용 프로그램 id 구성의 모든 특성을 정의 하는 hello 응용 프로그램 엔터티를 업데이트 하기 위한 메커니즘으로 사용 됩니다. 응용 프로그램 엔터티 hello에 대 한 자세한 내용은 hello를 참조 하십시오 [그래프 API 응용 프로그램 엔터티 설명서](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity)합니다. API에 대 한 hello 응용 프로그램 엔터티 사용 되는 멤버 toospecify 권한에 대 한 전체 참조 정보를 찾을 수 있습니다.  

* 컬렉션인 hello appRoles 멤버의 [AppRole](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type) 사용된 toodefine hello 될 수 있는 엔터티가 **응용 프로그램 사용 권한** 웹 API에 대 한  
* 컬렉션인 hello oauth2Permissions 멤버의 [OAuth2Permission](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type) 사용된 toodefine hello 될 수 있는 엔터티가 **위임 된 권한** 웹 API에 대 한

응용 프로그램에 대 한 자세한 내용은 매니페스트 개념 일반적으로 참조 하십시오 너무[이해 hello Azure Active Directory 응용 프로그램 매니페스트](active-directory-application-manifest.md)합니다.

### <a name="accessing-hello-azure-ad-graph-and-office-365-via-microsoft-graph-apis"></a>Azure AD 그래프 hello 및 Microsoft Graph Api를 통해 Office 365에 액세스  
설명한 이전, 또한 tooexposing/액세스 Api에서 리소스는 응용 프로그램으로 클라이언트 응용 프로그램 tooaccess Microsoft 리소스에 의해 노출 된 Api를 업데이트할 수 있습니다.  "Microsoft Graph" hello 목록에 사용 권한 tooother 응용 프로그램의 라고, 사용할 수 있는 Microsoft Graph API 또는 Azure AD에 등록 된 모든 응용 프로그램 hello 합니다. Office 365에서 프로 비전 된 Azure AD 테 넌 트의 클라이언트 응용 프로그램을 등록 하는 경우 또한 hello Microsoft Graph API toovarious Office 365 리소스에 의해 노출 되는 hello 사용 권한을 모두 액세스할 수 있습니다.

Microsoft Graph API에서 노출 하는 액세스 범위에 대 한 자세한 내용은, hello를 참조 하십시오 [권한 범위 | Microsoft Graph API 개념](https://graph.microsoft.io/docs/authorization/permission_scopes) 문서.

> [!NOTE]
> 네이티브 클라이언트 응용 프로그램 tooa 현재 제한 때문만 hello "조직의 디렉터리에 액세스" 권한을 사용 하는 경우 hello Azure AD Graph API 호출할 수 있습니다.  이 제한은 웹 응용 프로그램에는 적용되지 않습니다.
> 
> 

### <a name="configuring-multi-tenant-applications"></a>다중 테넌트 응용 프로그램 구성
응용 프로그램 tooAzure 광고를 추가할 때 프로그램 응용 프로그램 toobe 조직 내에서 사용자만 액세스할 수도 있습니다. 또는 외부 조직의 사용자가 액세스 하 여 응용 프로그램 toobe를 할 수 있습니다. 이러한 두 응용 프로그램 종류를 단일 테넌트 및 다중 테넌트 응용 프로그램이라고 합니다. 단일 테 넌 트 응용 프로그램 toomake의 hello 구성을 수정할 수 있습니다 것이 섹션에서는 아래 설명 하는 다중 테 넌 트 응용 프로그램입니다.

단일 테 넌 트 및 다중 테 넌 트 응용 프로그램 간의 중요 한 toonote hello 차이점입니다.  

* 단일 테넌트 응용 프로그램은 단일 조직에서 사용하기 위한 것입니다. 일반적으로 엔터프라이즈 개발자가 작성한 LoB(기간 업무) 응용 프로그램이 이에 해당합니다. 단일 테 넌 트 응용 프로그램만 toobe 한 디렉터리의 사용자가 액세스 하며 결과적으로, 특정 디렉터리에서 사용자를 프로 비전 toobe만 필요 합니다.
* 다중 테넌트 응용 프로그램은 여러 조직에서 사용하기 위한 것입니다. 일반적으로 ISV(Independent Software Vendor)에서 작성한SaaS(Software-as-a-Service) 웹 응용 프로그램이 이에 해당합니다. 다중 테 넌 트 응용 프로그램은 사용자 또는 관리자 동의 tooregister 필요한 위치에 사용 될, 각 디렉터리에 사용자를 프로 비전 toobe 필요 하 hello Azure AD의 승인 프레임 워크를 통해 지원 합니다. 모든 네이티브 클라이언트 응용 프로그램을 기본적으로 다중 테 넌 트 hello 리소스 소유자의 장치에 설치 되었는지 확인 합니다. Hello 승인 프레임 워크에 hello hello에 대 한 자세한 내용은 위의 동의 프레임 워크 섹션의 개요를 참조 하십시오.

#### <a name="enabling-external-users-toogrant-your-application-access-tootheir-resources"></a>응용 프로그램 액세스 tootheir 리소스 toogrant 외부 사용자가 사용 하도록 설정
를 작성 하는 응용 프로그램 toomake 사용할 수 있는 tooyour 고객 또는 파트너 조직 외부의 원하는 hello Azure 포털에서에서 tooupdate hello 응용 프로그램 정의 해야 합니다.

> [!NOTE]
> 다중 테넌트를 사용하도록 설정하면 응용프로그램의 앱 ID URI가 확인된 도메인에 속하도록 해야 합니다. 또한 hello 반환 URL은 https://로 시작 해야 합니다. 자세한 내용은 [응용 프로그램 개체 및 서비스 사용자 개체](active-directory-application-objects.md)를 참조하세요.
> 
> 

외부 사용자를 위한 tooenable access tooyour 앱: 

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello hello 페이지의 맨 위 오른쪽 모서리에서 사용자 계정을 선택 하 여 Azure AD 테 넌 트를 선택 합니다.
3. Hello 위쪽 메뉴에서 선택 **Azure Active Directory**, 클릭 **앱 등록**, tooconfigure 원하는 hello 응용 프로그램을 클릭 하 고 있습니다. 이 됩니다 toohello 응용 프로그램의 빠른 시작 페이지에서 이동으로 hello 응용 프로그램에 대 한 hello 설정 블레이드를 엽니다.
4. Hello 설정 블레이드에서 클릭 **속성** 및 플립 hello **다중 테 넌 트** 너무 전환**예**합니다.

변경, 사용자 및 다른 조직의 관리자는 위의 hello 적용 하 고 나면 됩니다 수 toogrant 응용 프로그램 액세스 tootheir 디렉터리 및 기타 데이터.

#### <a name="triggering-hello-azure-ad-consent-framework-at-runtime"></a>런타임 시 Azure AD hello 승인 프레임 워크 트리거
toouse hello 승인 프레임 워크, 다중 테 넌 트 클라이언트 응용 프로그램이 OAuth 2.0을 사용 하 여 권한 부여를 요청 해야 합니다. [코드 샘플](https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multi-tenant) 는 toocall 토큰을 웹 응용 프로그램, 네이티브 응용 프로그램 또는 서버/디먼 응용 프로그램 요청 권한 부여 코드로 작성 하 고 액세스 방법을 사용할 수 있는 tooshow 웹 Api입니다.

또한 웹 응용 프로그램에서 사용자를 위한 등록 환경을 제공할 수 있습니다. 등록 경험을 제공 하는 경우 해당 hello 사용자는 기호를 클릭 한 위로 단추를 클릭 하는 리디렉션 hello 브라우저 toohello Azure AD oauth 2.0 권한 부여 끝점 또는 OpenID Connect 사용자 정보 끝점이 것으로 예상 됩니다. 이러한 끝점 hello id_token를 검사 하 여 hello 새 사용자에 대 한 응용 프로그램 tooget 정보 hello를 허용 합니다. Hello 등록 단계 다음 hello 사용자는 동의 프롬프트 비슷한 toohello hello hello 동의 프레임 워크 섹션의 개요에서에서 위에 표시 된 하나 표시 됩니다.

또는 웹 응용 프로그램 관리자가 "회사 등록" 너무 수 있는 환경을 제공할 수도 있습니다. 이 환경은 hello 사용자 toohello Azure AD OAuth 리디렉션합니다도 2.0 권한 부여 끝점입니다. 이 경우 프롬프트를 전달 하지만 admin_consent = 매개 변수가 toohello 인증 끝점 tooforce hello 승인 환경을 관리자에 게 조직 대신 승인을 하 게 부여 됩니다. Toohello 전역 관리자 역할이 속해 있는 계정으로 인증 하는 사용자 동의; 제공할 수 있습니다. 다른 오류가 표시 됩니다. 승인에 성공 hello 응답 admin_consent 포함 됩니다 = true입니다. 액세스 토큰을 사용 하는, id_token hello 조직에서 정보를 제공 하 고 응용 프로그램에 등록 하는 관리자에 게도 수신 됩니다.

### <a name="enabling-oauth-20-implicit-grant-for-single-page-applications"></a>단일 페이지 응용 프로그램에 OAuth 2.0 암시적 허용 사용
일반적으로 단일 페이지 응용 프로그램의 (SPAs)는 hello 응용 프로그램의 웹 API 백 엔드 tooperform는 비즈니스 논리를 호출 하는 hello 브라우저에서 실행 되는 JavaScript 많은 프런트 엔드를 사용 하 여 구성 됩니다. Azure AD에서 호스팅되는 SPAs에 대 한 OAuth 2.0 Implicit Grant tooauthenticate hello 사용자 Azure AD를 사용 하 고이 사용할 수 있는 토큰을 가져옵니다 toosecure JavaScript 클라이언트 tooits hello 응용 프로그램에서에서 다시 호출 끝 웹 API입니다. Hello 사용자가 승인 후에이 동일한 인증 프로토콜 hello 클라이언트와 hello 응용 프로그램에 대해 구성 된 다른 웹 API 리소스 간의 사용된 tooobtain 토큰 toosecure 호출 될 수 있습니다. hello 암시적 권한 부여 및 응용 프로그램 시나리오에 적합 한지 결정 하는 도움말에 대해 자세히 toolearn 참조 [이해 hello OAuth2 암시적 부여 흐름이 Azure Active Directory에서 ](active-directory-dev-understanding-oauth2-implicit-grant.md)합니다.

기본적으로 응용 프로그램에 대해 OAuth 2.0 암시적 허용이 사용되지 않도록 설정됩니다. Hello 설정 하 여 응용 프로그램에 대 한 OAuth 2.0 Implicit Grant를 사용할 수 있습니다 `oauth2AllowImplicitFlow` 에서 값을 해당 [응용 프로그램 매니페스트](active-directory-application-manifest.md), 응용 프로그램 id 구성을 나타내는 JSON 파일인 합니다.

#### <a name="tooenable-oauth-20-implicit-grant"></a>tooenable OAuth 2.0 암시적 부여
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello hello 페이지의 맨 위 오른쪽 모서리에서 사용자 계정을 선택 하 여 Azure AD 테 넌 트를 선택 합니다.
3. Hello 위쪽 메뉴에서 선택 **Azure Active Directory**, 클릭 **앱 등록**, tooconfigure 원하는 hello 응용 프로그램을 클릭 하 고 있습니다. 이 됩니다 toohello 응용 프로그램의 빠른 시작 페이지에서 이동으로 hello 응용 프로그램에 대 한 hello 설정 블레이드를 엽니다.
4. Hello 응용 프로그램 페이지에서 클릭 **매니페스트** tooopen hello 인라인 매니페스트 편집기입니다.
   찾아 너무 "true" hello "oauth2AllowImplicitFlow" 값을 설정 합니다. 기본적으로 “false”입니다.
   
    `"oauth2AllowImplicitFlow": true,`
5. 업데이트 하는 hello 매니페스트를 저장 합니다. 저장 한 후 웹 API는 이제 toouse OAuth 2.0 Implicit Grant tooauthenticate 사용자가 구성 합니다.


## <a name="removing-an-application"></a>응용 프로그램 제거
이 섹션에서는 어떻게 tooremove 응용 프로그램에서 Azure AD 테 넌 트를 설명 합니다.

### <a name="removing-an-application-authored-by-your-organization"></a>조직이 작성한 응용프로그램 제거
이들은 Azure AD 테 넌 트에 대 한 hello hello 기본 "응용 프로그램" 페이지에 대 한 "응용 프로그램 내 회사 소유 하 는" 필터에서 보여 주는 hello 응용 프로그램입니다. 기술 용어는 PowerShell을 통해 hello Azure 클래식 포털을 통해 수동으로 또는 프로그래밍 방식으로 등록 하는 응용 프로그램이 이러한 또는 Graph API를 환영 합니다. 구체적으로 말하면, 테넌트의 응용프로그램 및 서비스 주체 개체 모두에 의해 제공됩니다. 자세한 내용은 [응용 프로그램 개체 및 서비스 주체 개체](active-directory-application-objects.md) 를 참조하세요.

#### <a name="tooremove-a-single-tenant-application-from-your-directory"></a>tooremove 디렉터리에서 단일 테 넌 트 응용 프로그램
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello hello 페이지의 맨 위 오른쪽 모서리에서 사용자 계정을 선택 하 여 Azure AD 테 넌 트를 선택 합니다.
3. Hello 위쪽 메뉴에서 선택 **Azure Active Directory**, 클릭 **앱 등록**, tooconfigure 원하는 hello 응용 프로그램을 클릭 하 고 있습니다. 이 됩니다 toohello 응용 프로그램의 빠른 시작 페이지에서 이동으로 hello 응용 프로그램에 대 한 hello 설정 블레이드를 엽니다.
4. Hello 응용 프로그램 페이지에서 클릭 **삭제**합니다.
5. 클릭 **예** hello 확인 메시지에서 합니다.

#### <a name="tooremove-a-multi-tenant-application-from-your-directory"></a>tooremove 디렉터리에서 다중 테 넌 트 응용 프로그램
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello hello 페이지의 맨 위 오른쪽 모서리에서 사용자 계정을 선택 하 여 Azure AD 테 넌 트를 선택 합니다.
3. Hello 위쪽 메뉴에서 선택 **Azure Active Directory**, 클릭 **앱 등록**, tooconfigure 원하는 hello 응용 프로그램을 클릭 하 고 있습니다. 이 됩니다 toohello 응용 프로그램의 빠른 시작 페이지에서 이동으로 hello 응용 프로그램에 대 한 hello 설정 블레이드를 엽니다.
4. Hello 설정 블레이드에서 선택 **속성** 및 플립 hello **다중 테 넌 트** 너무 전환**아니요**합니다. 이렇게 변환 응용 프로그램 toobe 단일 테 넌 트에 있지만 hello 응용 프로그램이 tooit 동의 이미 조직 내에 계속 남아 있게 됩니다.
5. Hello 클릭 **삭제** hello 응용 프로그램 페이지에서 단추입니다.
6. 클릭 **예** hello 확인 메시지에서 합니다.

### <a name="removing-a-multi-tenant-application-authorized-by-another-organization"></a>다른 조직이 권한을 부여한 다중 테넌트 응용프로그램 제거
이들은 Azure AD 테 넌 트, 특히 hello hello "응용 프로그램 내 회사 소유" 목록에서 나열 되지 않은 것에 대 한 hello "응용 프로그램 사용" 필터 hello 주 "응용 프로그램" 페이지에 표시 되는 hello 응용 프로그램의 하위 집합입니다. 기술 용어, 이러한 항목은 다중 테 넌 트 응용 프로그램 hello 동의 프로세스 중에 등록 합니다. 구체적으로 말하면, 테넌트의 서비스 주체 개체에 의해서만 제공됩니다. 자세한 내용은 [응용 프로그램 개체 및 서비스 주체 개체](active-directory-application-objects.md) 를 참조하세요.

주문 tooremove 다중 테 넌 트 응용 프로그램의 액세스 tooyour 디렉터리 (승인한 후), 회사 관리자에 게 hello Azure 포털을 통해는 Azure 구독 tooremove 액세스할 수 있어야 합니다. 또는 회사 관리자에 게 hello를 사용할 수 [Azure AD PowerShell Cmdlet](http://go.microsoft.com/fwlink/?LinkId=294151) tooremove 액세스 합니다.

## <a name="next-steps"></a>다음 단계
* Hello 참조 [통합 된 응용 프로그램에 대 한 브랜딩 지침](active-directory-branding-guidelines.md) 앱에 대 한 시각적 지침에 대 한 팁입니다.
* 응용 프로그램의 응용 프로그램 및 서비스 사용자 개체 간의 hello 관계에 대 한 자세한 내용은 참조 하십시오. [응용 프로그램 개체 및 서비스 주체 개체](active-directory-application-objects.md)합니다.
* toolearn hello 역할 hello 응용 프로그램 매니페스트 재생에 대 한 자세한 참조 [이해 hello Azure Active Directory 응용 프로그램 매니페스트](active-directory-application-manifest.md)
* Hello 참조 [Azure AD 개발자 용어집](active-directory-dev-glossary.md) hello 핵심 Azure AD (Active Directory) 개발자 개념 중 일부에 대 한 정의입니다.
* Hello 방문 [Active Directory 개발자 가이드](active-directory-developers-guide.md) 관련 콘텐츠와 모든 개발자에 대 한 개요입니다.

