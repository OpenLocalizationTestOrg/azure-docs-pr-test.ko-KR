---
title: "aaaAzure Active Directory 인증 및 리소스 관리자 | Microsoft Docs"
description: "개발자 가이드 tooauthentication hello Azure 리소스 관리자 API 및 Azure Active Directory와 응용 프로그램 통합 다른 Azure 구독에 대 한 합니다."
services: azure-resource-manager,active-directory
documentationcenter: na
author: dushyantgill
manager: timlt
editor: tysonn
ms.assetid: 17b2b40d-bf42-4c7d-9a88-9938409c5088
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/27/2016
ms.author: dugill;tomfitz
ms.openlocfilehash: 757e45fdb28488b45de70647746461888bf35a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-resource-manager-authentication-api-tooaccess-subscriptions"></a>리소스 관리자 API 인증 tooaccess 구독 사용
## <a name="introduction"></a>소개
소프트웨어 개발자에 게 toocreate 고객의 Azure 리소스를 관리 하는 응용 프로그램의 경우와 tooauthenticate hello Azure 리소스 관리자 Api 및 액세스 tooresources 다른 구독에 대 한 권한을 얻는 방법을이 항목에서는 합니다.

앱 hello 여러 가지 방법으로 리소스 관리자 Api에 액세스할 수 있습니다.

1. **사용자 + 앱 액세스**: 로그인한 사용자를 대신하여 리소스에 액세스하는 앱. 이 방법은 웹앱 및 명령줄 도구 등 Azure 리소스의 "대화형 관리"만 처리하는 앱에만 적용됩니다.
2. **앱 전용 액세스**: 디먼 서비스 및 예약된 작업을 실행하는 앱. hello 응용 프로그램 id toohello 리소스에 직접 액세스 권한이 부여 됩니다. 이 방법은 장기 헤드리스 (무인된) 액세스 tooAzure 해야 하는 앱에 대 한 작동 합니다.

이 항목에서는 단계별 지침 toocreate 두 가지 권한 부여 방식은 사용 하는 응용 프로그램. REST API 또는 C# 사용 tooperform 각 단계 하는 방법을 보여 줍니다. ASP.NET MVC 응용 프로그램을 완료 하는 hello에서 제공 됩니다. [https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense)합니다.

## <a name="what-hello-web-app-does"></a>어떤 hello 웹 앱은
hello 웹 앱:

1. Azure 사용자를 로그인합니다.
2. 사용자 toogrant hello 웹 응용 프로그램 액세스 tooResource 관리자에 게 요청합니다.
3. Resource Manager에 액세스하기 위한 사용자 + 앱 액세스 토큰을 가져옵니다.
4. Hello 앱 장기 액세스 toohello 구독을 제공 하는 hello 구독에서 리소스 관리자 (3 단계)에서 토큰 toocall 및 할당 hello 앱 서비스 주 tooa 역할을 사용 합니다.
5. 앱 전용 액세스 토큰을 가져옵니다.
6. 리소스 관리자를 통해 hello 구독에서 (5 단계)에서 토큰 toomanage 리소스를 사용합니다.

Hello 웹 응용 프로그램의 hello 종단 간 흐름은 다음과 같습니다.

![Resource Manager 인증 흐름](./media/resource-manager-api-authentication/Auth-Swim-Lane.png)

Hello 구독 id를 제공 하는 사용자로 toouse hello 구독에 대 한 원하는:

![구독 ID 제공](./media/resource-manager-api-authentication/sample-ux-1.png)

로그인 하기 위한 계정 toouse hello를 선택 합니다.

![계정 선택](./media/resource-manager-api-authentication/sample-ux-2.png)

자격 증명을 제공 합니다.

![자격 증명 제공](./media/resource-manager-api-authentication/sample-ux-3.png)

Azure 구독을 hello 앱 액세스 tooyour에 권한을 부여 합니다.

![액세스 권한 부여](./media/resource-manager-api-authentication/sample-ux-4.png)

연결된 구독을 관리합니다.

![구독 연결](./media/resource-manager-api-authentication/sample-ux-7.png)

## <a name="register-application"></a>응용 프로그램 등록
코딩을 시작하기 전에 Azure Active Directory(AD)를 사용하여 웹앱을 등록합니다. 앱 등록을 hello Azure AD에서 앱에 대 한 중앙 id를 만듭니다. 응용 프로그램 tooauthenticate 및 액세스 Azure 리소스 관리자 Api를 사용 하도록 OAuth 클라이언트 ID, 회신 Url과 자격 증명와 같은 응용 프로그램에 대 한 기본 정보를 저장 합니다. 또한 hello 앱 등록 응용 프로그램에 필요한 hello 사용자를 대신 하 여 Microsoft Api에 액세스할 때 사용 권한이 위임 다양 한 hello를 기록 합니다.

앱에서 다른 구독에 액세스하므로 다중 테넌트 응용 프로그램으로 구성해야 합니다. toopass 유효성 검사를 Azure Active Directory와 연결 된 도메인을 제공 합니다. Azure Active Directory, toohello 로그인와 연결 된 toosee hello 도메인 [클래식 포털](https://manage.windowsazure.com)합니다. Azure Active Directory를 선택한 다음 **도메인**을 선택합니다.

다음 예제는 hello tooregister Azure PowerShell을 사용 하 여 앱을 hello 하는 방법을 보여 줍니다. Hello 최신 버전 (2016 년 8 월)의 Azure PowerShell이 명령 toowork에 있어야 합니다.

    $app = New-AzureRmADApplication -DisplayName "{app name}" -HomePage "https://{your domain}/{app name}" -IdentifierUris "https://{your domain}/{app name}" -Password "{your password}" -AvailableToOtherTenants $true

AD 응용 프로그램 hello로 toolog hello 응용 프로그램 id와 암호 해야합니다. 사용 하 여 hello 이전 명령에서 반환 되는 toosee hello 응용 프로그램 id:

    $app.ApplicationId

다음 예제는 hello tooregister Azure CLI를 사용 하 여 앱을 hello 하는 방법을 보여 줍니다.

    azure ad app create --name {app name} --home-page https://{your domain}/{app name} --identifier-uris https://{your domain}/{app name} --password {your password} --available true

hello 결과 hello hello 응용 프로그램으로 인증할 때 필요한 AppId를 포함 합니다.

### <a name="optional-configuration---certificate-credential"></a>선택적 구성 - 인증서 자격 증명
또한 azure AD 응용 프로그램을 위한 인증서 자격 증명을 지원 합니다: 자체 서명 된 인증서 만들기, hello 개인 키를 유지 하 고 hello 공개 키 tooyour Azure AD 응용 프로그램 등록을 추가 합니다. 인증을 위해 응용 프로그램에서 사용자의 개인 키를 사용 하 여 서명 하는 AD와 Azure AD 작은 페이로드 tooAzure 등록 hello 공개 키를 사용 하 여 hello 서명의 유효성을 검사 합니다.

인증서와 함께 AD 응용 프로그램을 만드는 방법은 참조 [toocreate Azure PowerShell을 사용 하 여 서비스 사용자 tooaccess 리소스](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) 또는 [서비스 주체를 사용 하 여 Azure CLI toocreate tooaccess 리소스](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate).

## <a name="get-tenant-id-from-subscription-id"></a>구독 ID에서 테넌트 ID 가져오기
toorequest 토큰을 사용 하는 toocall 리소스 관리자 일 수 있는 응용 프로그램 tooknow hello Azure 구독을 호스팅하는 hello Azure AD 테 넌 트의 테 넌 트 ID를 hello에 필요 합니다. 대부분의 경우 사용자는 자신의 구독 ID를 알고 있지만 Azure Active Directory에 대한 테넌트 ID는 모를 수 있습니다. tooget hello 구독 id에 대 한 hello 사용자에 게 확인 hello 사용자의 테 넌 트 id입니다. Hello 구독에 대 한 요청을 보낼 경우 해당 구독 id를 제공 합니다.

    https://management.azure.com/subscriptions/{subscription-id}?api-version=2015-01-01

hello 요청 하지만 때문에 실패 hello 사용자가 아직 로그인 하지 않은 hello 응답에서 hello 테 넌 트 id를 검색할 수 있습니다. 해당 예외에 대 한 hello 응답 헤더 값에서 hello 테 넌 트 id 검색 **Www-authenticate**합니다. Hello에이 구현을 참조 [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20) 메서드.

## <a name="get-user--app-access-token"></a>사용자 + 앱 액세스 토큰 가져오기
응용 프로그램 hello 사용자 tooAzure는 OAuth 2.0 권한 부여 요청-tooauthenticate hello 사용자의 자격 증명으로 AD 리디렉션하고 인증 코드 가져오기 다시 합니다. 응용 프로그램 리소스 관리자에 대 한 hello 권한 부여 코드 tooget 액세스 토큰을 사용 합니다. hello [ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42) 메서드 hello 권한 부여 요청을 만듭니다.

이 항목에서는 hello REST API 요청 tooauthenticate hello 사용자를 보여 줍니다. 코드에 도우미 라이브러리 tooperform 인증도 사용할 수 있습니다. 이러한 라이브러리에 대한 자세한 내용은 [Azure Active Directory 인증 라이브러리](../active-directory/active-directory-authentication-libraries.md)를 참조하세요. 응용 프로그램에서 ID 관리를 통합하는 지침은 [Azure Active Directory 개발자 가이드](../active-directory/active-directory-developers-guide.md)를 참조하세요.

### <a name="auth-request-oauth-20"></a>인증 요청(OAuth 2.0)
Open ID 연결/oauth 2.0 권한 부여 요청 toohello Azure AD 권한 부여 끝점을 실행 합니다.

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize

이 요청에 사용할 수 있는 hello 쿼리 문자열 매개 변수는 hello에 설명 된 [인증 코드 요청](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code) 항목입니다.

hello 방법을 예제와 다음 toorequest oauth 2.0 권한 부여:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=query&response_type=code&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&domain_hint=live.com

Azure AD hello 사용자를 인증 하 고 필요한 경우 hello 사용자 toogrant 권한 toohello 응용 프로그램을 요청 합니다. Hello 권한 부여 코드 toohello 응용 프로그램의 회신 URL을 반환합니다. Hello에 따라 response_mode를, 어느 보냅니다 다시 hello 데이터 게시 데이터 또는 쿼리 문자열에 Azure AD가 요청 했습니다.

    code=AAABAAAAiL****FDMZBUwZ8eCAA&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="auth-request-open-id-connect"></a>인증 요청(Open ID Connect)
뿐만 아니라 hello 사용자를 대신 하 여 Azure 리소스 관리자 tooaccess 원하는 하지만 tooyour 응용 프로그램을 통해 Azure AD 계정을 사용 하 여 hello 사용자 toosign 통해서도으로 Open ID 연결 권한 부여 요청을 실행 합니다. Open ID Connect와 함께 응용 프로그램 앱 toosign hello 사용자에 사용할 수 있는 Azure AD에서는 id_token을 받습니다.

이 요청에 사용할 수 있는 hello 쿼리 문자열 매개 변수는 hello에 설명 된 [hello 로그인 요청 보내기](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request) 항목입니다.

Open ID Connect 요청 예제:

     https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=form_post&response_type=code+id_token&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&scope=openid+profile&nonce=63567Dc4MDAw&domain_hint=live.com&state=M_12tMyKaM8

Azure AD hello 사용자를 인증 하 고 필요한 경우 hello 사용자 toogrant 권한 toohello 응용 프로그램을 요청 합니다. Hello 권한 부여 코드 toohello 응용 프로그램의 회신 URL을 반환합니다. Hello에 따라 response_mode를, 어느 보냅니다 다시 hello 데이터 게시 데이터 또는 쿼리 문자열에 Azure AD가 요청 했습니다.

Open ID Connect 응답 예제:

    code=AAABAAAAiL*****I4rDWd7zXsH6WUjlkIEQxIAA&id_token=eyJ0eXAiOiJKV1Q*****T3GrzzSFxg&state=M_12tMyKaM8&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="token-request-oauth20-code-grant-flow"></a>토큰 요청(OAuth2.0 코드 부여 흐름)
이제 응용 프로그램이 Azure AD에서 인증 코드 hello 받은 경우 시간 tooget hello 액세스 토큰에 대 한 Azure 리소스 관리자입니다.  Oauth 2.0 코드 부여 토큰 요청 toohello Azure AD 토큰 끝점을 게시 합니다.

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

이 요청에 사용할 수 있는 hello 쿼리 문자열 매개 변수는 hello에 설명 된 [hello 인증 코드를 사용 하 여](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token) 항목입니다.

다음 예제는 hello 암호 자격 증명을 가진 코드 부여 토큰에 대 한 요청을 보여 줍니다.

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

자격 증명 인증서를 사용할 때 JSON 웹 토큰 (JWT) 및 기호 (RSA SHA256) hello 응용 프로그램의 인증서 자격 증명의 개인 키를 사용 하 여 만듭니다. hello hello 토큰에 대 한 클레임 형식에 표시 되어 [JWT 토큰 클레임](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims)합니다. 참조를 위해 참조 hello [Active Directory 인증 라이브러리 (.NET) 코드](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs) toosign 클라이언트 어설션 JWT 토큰입니다.

Hello 참조 [Open ID 연결 사양](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication) 클라이언트 인증에 대 한 자세한 내용은 합니다.

다음 예제는 hello 인증서 자격 증명 코드 부여 토큰에 대 한 요청을 보여 줍니다.

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbG*****Y9cYo8nEjMyA

코드 부여 토큰에 대한 응답 예제:

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039858","not_before":"1432035958","resource":"https://management.core.windows.net/","access_token":"eyJ0eXAiOiJKV1Q****M7Cw6JWtfY2lGc5A","refresh_token":"AAABAAAAiL9Kn2Z****55j-sjnyYgAA","scope":"user_impersonation","id_token":"eyJ0eXAiOiJKV*****-drP1J3P-HnHi9Rr46kGZnukEBH4dsg"}

#### <a name="handle-code-grant-token-response"></a>코드 부여 토큰 응답 처리
성공적인 토큰 응답 Azure 리소스 관리자에 대 한 액세스 토큰 hello (사용자 + 응용 프로그램)를 포함합니다. 응용 프로그램에서이 액세스 토큰 tooaccess 리소스 관리자 hello 사용자 대신 사용 합니다. hello Azure AD에서 발급 하는 액세스 토큰의 수명은 1 시간입니다. 웹 응용 프로그램 toorenew hello (사용자 + 응용 프로그램) 액세스 토큰이 필요 함을 가능성이 아닙니다. Toorenew hello 액세스 토큰을 해야 하는 경우 응용 프로그램 hello 토큰 응답에서 부여 하는 hello 새로 고침 토큰을 사용 합니다. Oauth 2.0 토큰 요청 toohello Azure AD 토큰 끝점을 게시 합니다.

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

hello 매개 변수 toouse hello 새로 고침 요청에 설명 되어 있음 [hello 액세스 토큰 새로 고침](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens)합니다.

hello 다음 보여 주는 예제 toouse hello 새로 고침 하는 토큰:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=refresh_token&refresh_token=AAABAAAAiL9Kn2Z****55j-sjnyYgAA&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

새로 고침 토큰이 사용 되는 tooget 새 액세스 토큰에 대 한 Azure 리소스 관리자를 사용할 수 있지만 응용 프로그램에서 오프 라인 액세스에 적합 하지 않습니다. hello 새로 고침 토큰 수명을 제한 되며 새로 고침 토큰은 바인딩된 toohello 사용자입니다. Hello 사용자가 조직 hello를 hello 새로 고침 토큰을 사용 하 여 hello 응용 프로그램 액세스를 잃습니다. 이 방법을 사용 되는 응용 프로그램에 적합 하지 팀 toomanage 하 여 Azure 리소스를 사용 합니다.

## <a name="check-if-user-can-assign-access-toosubscription"></a>사용자 액세스 toosubscription 할당할 수 확인
이제 응용 프로그램에 hello 사용자 대신 토큰 tooaccess Azure 리소스 관리자에 있습니다. hello 다음 단계는 tooconnect 앱 toohello 구독 합니다. 에 연결한 후 앱 hello 사용자를 사용할 수 없는 경우에 해당 구독을 관리할 수 (장기 오프 라인 액세스).

각 구독 tooconnect 호출 hello [목록 사용 권한 리소스 관리자](https://docs.microsoft.com/rest/api/authorization/permissions) API toodetermine hello 사용자의 hello 구독에 대 한 액세스 관리 권한이 있는지 여부.

hello [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44) 메서드 hello ASP.NET MVC 샘플 응용 프로그램의이 호출을 구현 합니다.

hello 방법을 예제와 다음 toorequest 구독에 대 한 사용자의 권한을 합니다. 83cfe939-2402-4581-b761-4f59b0a041e4은 hello id hello 구독입니다.

    GET https://management.azure.com/subscriptions/83cfe939-2402-4581-b761-4f59b0a041e4/providers/microsoft.authorization/permissions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiLC***lwO1mM7Cw6JWtfY2lGc5A

구독에 대 한 hello 응답 tooget 사용자의 권한의 예는.

    HTTP/1.1 200 OK

    {"value":[{"actions":["*"],"notActions":["Microsoft.Authorization/*/Write","Microsoft.Authorization/*/Delete"]},{"actions":["*/read"],"notActions":[]}]}

hello 권한을 API 여러 사용 권한을 반환 합니다. 각 사용 권한은 허용되는 작업(actions) 및 허용되지 않는 작업(notactions)으로 구성됩니다. 작업에 대 한 사용 권한의 작업 목록 허용 hello 있고 hello 사용자가 없거나 해당 권한의 hello notactions 목록의 tooperform 해당 작업을 허용 합니다. **microsoft.authorization/roleassignments/write** hello 동작 하는 액세스 관리 권한을 부여 합니다. 응용 프로그램 hello 작업 및 각 사용 권한의 notactions에서이 동작 문자열에 정규식 일치에 대 한 사용 권한 결과 toolook hello 구문 분석 해야 합니다.

## <a name="get-app-only-access-token"></a>앱 전용 액세스 토큰 가져오기
이제 알 수 hello 사용자 액세스 toohello Azure 구독을 할당할 수 있습니다. hello 다음 단계는.

1. Hello 적절 한 RBAC 역할 tooyour 응용 프로그램의 id hello 구독에 할당 합니다.
2. Hello 구독에 대 한 사용 권한의 hello 응용 프로그램의 쿼리를 통해 또는 응용 프로그램 전용 토큰을 사용 하 여 리소스 관리자에 액세스 하 여 hello 액세스 할당의 유효성을 검사 합니다.
3. Hello hello 구독의 id를 유지 하면 응용 프로그램 "연결 된 구독" 데이터 구조의-레코드 hello 연결입니다.

Hello 첫 번째 단계에서 자세히 살펴보겠습니다. tooassign hello 적절 한 RBAC 역할 toohello 응용 프로그램의 id를 있습니다 결정 해야 합니다.

* hello 사용자의 Azure Active Directory에서 응용 프로그램의 id의 hello 개체 id
* 응용 프로그램에 필요한 hello 구독에 대해 hello RBAC 역할의 hello 식별자

응용 프로그램이 Azure AD에서 사용자를 인증할 때 응용 프로그램에 대한 서비스 주체 개체가 해당 Azure AD에 생성됩니다. Azure는 RBAC 역할 toobe 할당 한 Azure 리소스에 대 한 직접 액세스 toocorresponding 응용 프로그램 toogrant tooservice 주체 허용 됩니다. 이 작업을 정확 하 게 toodo 했는데도 기능. 쿼리 hello Azure AD Graph API toodetermine hello 식별자 hello 로그인 한 사용자의 응용 프로그램의 hello 서비스 사용자의 Azure AD의입니다.

액세스 토큰에 대 한 Azure 리소스 관리자와 하면 새 액세스 토큰 toocall hello Azure AD Graph API를 해야 합니다. Azure AD에서 모든 응용 프로그램에 권한이 tooquery 서비스 사용자 개체는 자체 응용 프로그램 전용 액세스 토큰은 충분 한 있으므로.

<a id="app-azure-ad-graph" />

### <a name="get-app-only-access-token-for-azure-ad-graph-api"></a>Azure AD Graph API에 대한 응용 프로그램 전용 액세스 토큰 가져오기
tooauthenticate 앱과 get 토큰 tooAzure AD Graph API 발급 한 클라이언트 자격 증명 부여 oauth 2.0 흐름 토큰 요청 tooAzure AD 토큰 끝점 (**https://login.microsoftonline.com/ {directory_domain_name} / OAuth2/토큰**).

hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs) ASP.net MVC 샘플 응용 앱 전용 액세스를 사용 하 여 Graph API에 대 한 토큰을 가져옵니다 hello 방식의.NET에 대 한 Active Directory 인증 라이브러리를 hello 합니다.

이 요청에 사용할 수 있는 hello 쿼리 문자열 매개 변수는 hello에 설명 된 [액세스 토큰 요청](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token) 항목입니다.

클라이언트 자격 증명 부여 토큰에 대한 요청 예제:

    POST https://login.microsoftonline.com/62e173e9-301e-423e-bcd4-29121ec1aa24/oauth2/token HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 187</pre>
    <pre>grant_type=client_credentials&client_id=a0448380-c346-4f9f-b897-c18733de9394&resource=https%3A%2F%2Fgraph.windows.net%2F &client_secret=olna8C*****Og%3D

클라이언트 자격 증명 부여 토큰에 대한 응답 예제:

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039862","not_before":"1432035962","resource":"https://graph.windows.net/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRv****G5gUTV-kKorR-pg"}

### <a name="get-objectid-of-application-service-principal-in-user-azure-ad"></a>사용자 Azure AD에서 응용 프로그램 서비스 주체의 ObjectId 가져오기
이제 hello 앱 전용 액세스 토큰 tooquery hello를 사용 하 여 [서비스 사용자를 Azure AD 그래프](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity) API toodetermine hello hello 디렉터리에 hello 응용 프로그램의 서비스 사용자의 개체 Id입니다.

hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#) 메서드 hello ASP.net MVC 샘플 응용 프로그램의이 호출을 구현 합니다.

hello 방법을 예제와 다음 toorequest 응용 프로그램의 서비스 사용자입니다. a0448380-c346-4f9f-b897-c18733de9394는 hello 응용 프로그램의 hello 클라이언트 id입니다.

    GET https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/servicePrincipals?api-version=1.5&$filter=appId%20eq%20'a0448380-c346-4f9f-b897-c18733de9394' HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJK*****-kKorR-pg

hello 다음 보여 주는 예제 응용 프로그램의 서비스에 대 한 응답 toohello 요청 주

    HTTP/1.1 200 OK

    {"odata.metadata":"https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/$metadata#directoryObjects/Microsoft.DirectoryServices.ServicePrincipal","value":[{"odata.type":"Microsoft.DirectoryServices.ServicePrincipal","objectType":"ServicePrincipal","objectId":"9b5018d4-6951-42ed-8a92-f11ec283ccec","deletionTimestamp":null,"accountEnabled":true,"appDisplayName":"CloudSense","appId":"a0448380-c346-4f9f-b897-c18733de9394","appOwnerTenantId":"62e173e9-301e-423e-bcd4-29121ec1aa24","appRoleAssignmentRequired":false,"appRoles":[],"displayName":"CloudSense","errorUrl":null,"homepage":"http://www.vipswapper.com/cloudsense","keyCredentials":[],"logoutUrl":null,"oauth2Permissions":[{"adminConsentDescription":"Allow hello application tooaccess CloudSense on behalf of hello signed-in user.","adminConsentDisplayName":"Access CloudSense","id":"b7b7338e-683a-4796-b95e-60c10380de1c","isEnabled":true,"type":"User","userConsentDescription":"Allow hello application tooaccess CloudSense on your behalf.","userConsentDisplayName":"Access CloudSense","value":"user_impersonation"}],"passwordCredentials":[],"preferredTokenSigningKeyThumbprint":null,"publisherName":"vipswapper"quot;,"replyUrls":["http://www.vipswapper.com/cloudsense","http://www.vipswapper.com","http://vipswapper.com","http://vipswapper.azurewebsites.net","http://localhost:62080"],"samlMetadataUrl":null,"servicePrincipalNames":["http://www.vipswapper.com/cloudsense","a0448380-c346-4f9f-b897-c18733de9394"],"tags":["WindowsAzureActiveDirectoryIntegratedApp"]}]}

### <a name="get-azure-rbac-role-identifier"></a>Azure RBAC 역할 ID 가져오기
tooassign hello 적절 한 RBAC 역할 tooyour 서비스 사용자, hello Azure RBAC 역할의 hello 식별자를 결정 해야 합니다.

hello RBAC에 대해 올바른 역할 응용 프로그램:

* 응용 프로그램 변경 하지 않고 hello 구독을 모니터링 하는 경우에 hello 구독에 대해 판독기 권한만 필요 합니다. Hello 할당 **판독기** 역할입니다.
* 응용 프로그램에 Azure hello 구독을 만들기/수정/삭제 하는 엔터티를 관리 하는 경우 hello 참가자 권한 중 하나가 필요 합니다.
  * 특정 유형의 리소스를 toomanage 할당 hello 리소스별 참가자 역할 (가상 컴퓨터 참가자, 가상 네트워크 참가자, 저장소 계정 참가자 등)
  * toomanage 모든 리소스 종류, 할당 hello **참가자** 역할입니다.

응용 프로그램에 대 한 역할 할당 hello 표시 toousers 이므로 선택 hello 최소 필수 권한.

Hello 호출 [리소스 관리자 역할 정의 API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) 모든 Azure RBAC 역할 및 검색 반복 hello 결과 toofind hello toolist 이름으로 역할 정의 필요 합니다.

hello [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246) 메서드 hello ASP.net MVC 샘플 응용 프로그램의이 호출을 구현 합니다.

hello 다음 요청 예제와 방법을 tooget Azure RBAC 역할 식별자입니다. 09cbd307-aa71-4aca-b346-5f253e6e3ebb은 hello id hello 구독입니다.

    GET https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV*****fY2lGc5

hello 응답 형식에 따라 hello 다음과 같습니다.

    HTTP/1.1 200 OK

    {"value":[{"properties":{"roleName":"API Management Service Contributor","type":"BuiltInRole","description":"Lets you manage API Management services, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.ApiManagement/Services/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/312a565d-c81f-4fd8-895a-4e21e48d571c","type":"Microsoft.Authorization/roleDefinitions","name":"312a565d-c81f-4fd8-895a-4e21e48d571c"},{"properties":{"roleName":"Application Insights Component Contributor","type":"BuiltInRole","description":"Lets you manage Application Insights components, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.Insights/components/*","Microsoft.Insights/webtests/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/ae349356-3a1b-4a5e-921d-050484c6347e","type":"Microsoft.Authorization/roleDefinitions","name":"ae349356-3a1b-4a5e-921d-050484c6347e"}]}

Toocall 필요 하지 않습니다이 API는 지속적으로. 확인 한 후 hello 역할 정의의 잘 알려진 GUID hello,으로 hello 역할 정의 id를 생성할 수 있습니다.

    /subscriptions/{subscription_id}/providers/Microsoft.Authorization/roleDefinitions/{well-known-role-guid}

다음은 자주 사용 되는 기본 제공 역할의 hello 잘 알려진 guid가입니다.

| 역할 | Guid |
| --- | --- |
| 독자 |acdd72a7-3385-48ef-bd42-f606fba81ae7 |
| 참가자 |b24988ac-6180-42a0-ab88-20f7382dd24c |
| 가상 컴퓨터 참여자 |d73bb868-a0df-4d4d-bd69-98a00b01fccb |
| 가상 네트워크 참여자 |b34d265f-36f7-4a0d-a4d4-e158ca92e90f |
| 저장소 계정 참여자 |86e8f5dc-a6e9-4c67-9d15-de283e8eac25 |
| 웹 사이트 참여자 |de139f84-1756-47ae-9be6-808fbbe84772 |
| 웹 계획 참여자 |2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b |
| SQL Server 참여자 |6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437 |
| SQL DB 참여자 |9b7fa17d-e63e-47b0-bb0a-15c516ac86ec |

### <a name="assign-rbac-role-tooapplication"></a>RBAC 역할 tooapplication 할당
Hello를 사용 하 여 tooassign hello 적절 한 RBAC 역할 tooyour 서비스 사용자를 원하는 대로 [리소스 관리자 역할 할당을 만들](https://docs.microsoft.com/rest/api/authorization/roleassignments) API입니다.

hello [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170) 메서드 hello ASP.net MVC 샘플 응용 프로그램의이 호출을 구현 합니다.

예제 요청 tooassign RBAC 역할 tooapplication의:

    PUT https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/microsoft.authorization/roleassignments/4f87261d-2816-465d-8311-70a27558df4c?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiL*****FlwO1mM7Cw6JWtfY2lGc5
    Content-Type: application/json
    Content-Length: 230

    {"properties": {"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2"}}

Hello 요청에 다음 값에는 hello 사용 됩니다.

| Guid | 설명 |
| --- | --- |
| 09cbd307-aa71-4aca-b346-5f253e6e3ebb |hello 구독의 hello id |
| c3097b31-7309-4c59-b4e3-770f8406bad2 |hello 응용 프로그램의 hello 서비스 사용자의 hello 개체 id |
| acdd72a7-3385-48ef-bd42-f606fba81ae7 |hello 읽기 역할의 hello id |
| 4f87261d-2816-465d-8311-70a27558df4c |만든 hello 새 역할 할당에 대 한 새 guid |

hello 응답 형식에 따라 hello 다음과 같습니다.

    HTTP/1.1 201 Created

    {"properties":{"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2","scope":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb"},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleAssignments/4f87261d-2816-465d-8311-70a27558df4c","type":"Microsoft.Authorization/roleAssignments","name":"4f87261d-2816-465d-8311-70a27558df4c"}

### <a name="get-app-only-access-token-for-azure-resource-manager"></a>Azure Resource Manager에 대한 응용 프로그램 전용 액세스 토큰 가져오기
toovalidate hello 구독에서 해당 앱은 필요한 hello 액세스할, 응용 프로그램 전용 토큰을 사용 하 여 hello 구독에서 테스트 작업을 수행 합니다.

응용 프로그램 전용 액세스 토큰을 tooget 섹션에서 지침에 따라 [Azure AD Graph API에 대 한 앱 전용 액세스 토큰 가져오기](#app-azure-ad-graph), hello 리소스 매개 변수에 대 한 다른 값으로:

    https://management.core.windows.net/

hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) ASP.NET MVC 샘플 응용 앱 전용 액세스를 사용 하 여 Azure 리소스 관리자에 대 한 토큰을 가져옵니다 hello 방식의.net에 대 한 Active Directory 인증 라이브러리를 hello 합니다.

#### <a name="get-applications-permissions-on-subscription"></a>구독에 대한 응용 프로그램의 권한 가져오기
Azure 구독에 대 한 액세스를 원하는 응용 프로그램에 hello toocheck, hello를 호출할 수도 있습니다 [리소스 관리자 사용 권한을](https://docs.microsoft.com/rest/api/authorization/permissions) API입니다. 이 방법은 비슷한 toohow hello 사용자에 게 hello 구독에 대 한 액세스 관리 권한이 있는지 여부를 결정 합니다. 그러나이 이번에는 hello 이전 단계에서 받은 hello 응용 프로그램 전용 액세스 토큰으로 hello 권한을 API를 호출 합니다.

hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) 메서드 hello ASP.NET MVC 샘플 응용 프로그램의이 호출을 구현 합니다.

## <a name="manage-connected-subscriptions"></a>연결된 구독 관리
적절 한 RBAC 역할 hello hello 구독에서 tooyour 응용 프로그램의 서비스 사용자에 게 할당 되 면 응용 프로그램 수 유지 모니터링/관리 Azure 리소스 관리자에 대 한 앱 전용 액세스 토큰을 사용 하 여 합니다.

구독 소유자 hello 클래식 포털 또는 명령줄 도구, 응용 프로그램을 사용 하 여 응용 프로그램의 역할 할당을 제거 하는 경우 더 이상 수 tooaccess 해당 구독입니다. 이 경우 hello 구독과 hello 연결 hello 응용 프로그램 외부에서 손상 되었습니다 hello 사용자에 게 알리는 하 고 hello 연결 옵션 너무 "복구"으로 지정 해야 합니다. "복구" 다시 오프 라인으로 삭제 된 hello 역할 할당을 만들면가 됩니다.

Hello 사용자 tooconnect 구독 tooyour 응용 프로그램을 사용 하도록 설정한 것 처럼 너무 hello 사용자 toodisconnect 구독 허용 해야 합니다. 액세스 관리의 관점에서 hello 응용 프로그램의 서비스 사용자에 미치는 hello 구독 hello 역할 할당을 제거 하는 수단을 분리 합니다. 필요에 따라 hello 구독에 대 한 hello 응용 프로그램의 모든 상태는 너무 제거 될 수 있습니다.
Hello 구독에 대 한 액세스 관리 권한 가진 사용자만 수 toodisconnect hello 구독 됩니다.

hello [RevokeRoleFromServicePrincipalOnSubscription 메서드](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200) 샘플 응용 프로그램의 ASP.net MVC hello이이 호출을 구현 합니다.

이와 같이 사용자는 이제 응용 프로그램을 사용하여 쉽게 Azure 구독을 연결 및 관리할 수 있습니다.
