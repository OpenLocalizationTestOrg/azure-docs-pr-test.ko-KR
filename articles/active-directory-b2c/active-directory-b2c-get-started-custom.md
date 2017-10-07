---
title: "Azure Active Directory B2C: 사용자 지정 정책 시작 | Microsoft Docs"
description: "Azure Active Directory B2C 사용자 지정 정책을 사용 하 여 tooget 시작 하는 방법"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja;parahk;gsacavdm
ms.openlocfilehash: 5ee133806395cddf18682769a6cad149889d82d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-get-started-with-custom-policies"></a>Azure Active Directory B2C: 사용자 지정 정책 시작

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

사용자 지정 정책을 "로컬 계정" 지원할 hello이이 문서의 단계를 완료 한 후 등록 또는 로그인 전자 메일 주소와 암호를 통해 합니다. 또한 Facebook 또는 Azure Active Directory와 같은 추가 ID 공급자를 추가하는 환경도 준비합니다. Hello (Azure AD) Azure Active Directory B2C Id 경험 프레임 워크의 다른 방법에 대 한 읽기 전에 이러한 단계를 사용 하는 toocomplete를 좋습니다.

## <a name="prerequisites"></a>필수 조건

계속하기 전에 모든 사용자, 응용 프로그램, 정책 등을 위한 컨테이너인 Azure AD B2C 테넌트가 있어야 합니다. 너무 필요 없는 경우 하나 이미,[Azure AD B2C 테 넌 트 만들기](active-directory-b2c-get-started.md)합니다. म 강력한 모든 개발자가 toocomplete hello Azure AD B2C 기본 제공 정책 연습 들이 고 계속 하기 전에 기본 제공 정책을 사용 하 여 응용 프로그램을 구성 합니다. 최소 변경 toohello 정책 이름 tooinvoke hello 사용자 지정 정책을 확인 한 후 응용 프로그램 두 가지 정책 유형을 사용 합니다.

>[!NOTE]
>사용자 지정 정책 편집 tooaccess, 올바른 Azure 구독과 연결 된 tooyour 테 넌 트가 필요 합니다. 그렇지 않은 경우 [Azure AD B2C 테 넌 트 tooan Azure 구독 연결](active-directory-b2c-how-to-enable-billing.md) 또는 Azure 구독이 사용 되지 않는지, hello Id 경험 프레임 워크 단추를 사용할 수 없습니다.

## <a name="add-signing-and-encryption-keys-tooyour-b2c-tenant-for-use-by-custom-policies"></a>사용자 지정 정책에 의해 서명 및 암호화 키 tooyour B2C 테 넌 트 사용 하기 위해 추가

1. 열기 hello **Id 경험 프레임 워크** 블레이드 Azure AD B2C 테 넌 트 설정에서 합니다.
2. 선택 **정책 키** 테 넌 트에 사용할 수 있는 tooview hello 키입니다.
3. B2C_1A_TokenSigningKeyContainer가 없으면 만듭니다.<br>
    a. **추가**를 선택합니다. <br>
    b. **생성**을 선택합니다.<br>
    c. **이름**에는 `TokenSigningKeyContainer`를 사용합니다. <br> 
    hello 접두사 `B2C_1A_` 자동으로 추가 될 수도 있습니다.<br>
    d. **키 유형**에는 **RSA**를 사용합니다.<br>
    e. 에 대 한 **날짜**, hello 기본값을 사용 합니다. <br>
    f. **키 사용**에는 **서명**을 사용합니다.<br>
    g. **만들기**를 선택합니다.<br>
4. B2C_1A_TokenEncryptionKeyContainer가 없으면 만듭니다.<br>
 a. **추가**를 선택합니다.<br>
 b. **생성**을 선택합니다.<br>
 c. **이름**에는 `TokenEncryptionKeyContainer`를 사용합니다. <br>
   hello 접두사 `B2C_1A`_를 자동으로 추가 될 수도 있습니다.<br>
 d. **키 유형**에는 **RSA**를 사용합니다.<br>
 e. 에 대 한 **날짜**, hello 기본값을 사용 합니다.<br>
 f. **키 사용**에는 **암호화**를 사용합니다.<br>
 g. **만들기**를 선택합니다.<br>
5. B2C_1A_FacebookSecret를 만듭니다. <br>
Facebook 응용 프로그램 암호를 이미 있는 경우 정책 키 tooyour 테 넌 트로 추가 합니다. 그렇지 않으면 hello 키를 만들어야 자리 표시자 값으로 정책 유효성 검사를 통과 되도록 합니다.<br>
 a. **추가**를 선택합니다.<br>
 b. **옵션**에는 **수동**을 사용합니다.<br>
 c. **이름**에는 `FacebookSecret`를 사용합니다. <br>
 hello 접두사 `B2C_1A_` 자동으로 추가 될 수도 있습니다.<br>
 d. Hello에 **비밀** 상자를 여 FacebookSecret developers.facebook.com에서 입력 또는 `0` 자리 표시자로 합니다. *Facebook 앱 ID가 아닙니다.* <br>
 e. **키 사용**에는 **서명**을 사용합니다. <br>
 f. **만들기**를 선택하고 이 만들기를 확인합니다.

## <a name="register-identity-experience-framework-applications"></a>ID 경험 프레임워크 응용 프로그램 등록

Azure AD B2C tooregister에 hello 엔진 toosign를에서 사용 되 고 사용자가 로그인 하는 두 개의 추가 응용 프로그램이 필요 합니다.

>[!NOTE]
>해당 사용에 대 한 로그인 로컬 계정을 사용 하 여 두 개의 응용 프로그램을 만들어야 합니다: IdentityExperienceFramework (웹 응용 프로그램) 및 (네이티브 응용 프로그램)와 ProxyIdentityExperienceFramework hello IdentityExperienceFramework 앱에서 권한을 위임 합니다. 로컬 계정은 테넌트에만 존재합니다. 사용자가 등록 고유한 전자 메일 주소/암호 조합 tooaccess 테 넌 트가 등록 응용 프로그램.

### <a name="create-hello-identityexperienceframework-application"></a>Hello IdentityExperienceFramework 응용 프로그램 만들기

1. Hello에 [Azure 포털](https://portal.azure.com), hello를 전환 [Azure AD B2C 테 넌 트의 상황에 맞는](active-directory-b2c-navigate-to-b2c-context.md)합니다.
2. 열기 hello **Azure Active Directory** 블레이드 (하지 hello **Azure AD B2C** 블레이드)입니다. Tooselect 해야 **더 서비스** toofind 것입니다.
3. **앱 등록**을 선택합니다.
4. **새 응용 프로그램 등록**을 선택합니다.
   * **이름**에는 `IdentityExperienceFramework`를 사용합니다.
   * **응용 프로그램 종류**에는 **웹앱/API**를 사용합니다.
   * **로그온 URL**에는 `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`을 사용합니다. 여기서 `yourtenant`는 Azure AD B2C 테넌트 도메인 이름입니다.
5. **만들기**를 선택합니다.
6. 을 만든 후 hello 새로 만든 응용 프로그램을 선택 합니다. **IdentityExperienceFramework**합니다.<br>
   * **속성**을 선택합니다.<br>
   * Hello 응용 프로그램 ID를 복사 하 고 나중에 저장 합니다.

### <a name="create-hello-proxyidentityexperienceframework-application"></a>Hello ProxyIdentityExperienceFramework 응용 프로그램 만들기

1. **앱 등록**을 선택합니다.
1. **새 응용 프로그램 등록**을 선택합니다.
   * **이름**에는 `ProxyIdentityExperienceFramework`를 사용합니다.
   * **응용 프로그램 종류**에는 **네이티브**를 사용합니다.
   * **리디렉션 URI**에는 `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`을 사용합니다. 여기서 `yourtenant`는 Azure AD B2C 테넌트입니다.
1. **만들기**를 선택합니다.
1. 를 만든 후 hello 응용 프로그램을 선택 합니다. **ProxyIdentityExperienceFramework**합니다.<br>
   * **속성**을 선택합니다. <br>
   * Hello 응용 프로그램 ID를 복사 하 고 나중에 저장 합니다.
1. **필요한 권한**을 선택합니다.
1. **추가**를 선택합니다.
1. **API 선택**을 선택합니다.
1. IdentityExperienceFramework hello 이름에 대 한 검색입니다. 선택 **IdentityExperienceFramework** 에 결과 얻으려면 hello 및 클릭 **선택**합니다.
1. 다음 너무 hello 확인란을 선택한**액세스 IdentityExperienceFramework**, 클릭 하 고 **선택**합니다.
1. **완료**를 선택합니다.
1. **권한 부여**을 선택하고 **예**를 선택하여 확인합니다.

## <a name="download-starter-pack-and-modify-policies"></a>시작 팩 다운로드 및 정책 수정

사용자 지정 정책은 업로드 toobe tooyour Azure AD B2C 테 넌 트를 필요로 하는 XML 파일의 집합입니다. 스타터 팩 tooget 제공 신속 하 게 될 것입니다. Hello 목록 다음의 각 스타터 팩 hello 가장 적은 수의 기술 프로필에 포함 및 사용자 친구에 설명 된 tooachieve hello 시나리오 필요:
 * LocalAccounts - Hello 로컬 계정에만 사용할을 수 있습니다.
 * SocialAccounts - Hello 소셜 (또는 페더레이션) 계정에만 사용할을 수 있습니다.
 * **SocialAndLocalAccounts** - Hello 연습에이 파일을 사용 합니다.
 * SocialAndLocalAccountsWithMFA - 소셜, 로컬 및 Multi-Factor Authentication 옵션이 여기에 포함됩니다.

시작 팩 각각에는 다음이 포함됩니다.

* hello [기본 파일](active-directory-b2c-overview-custom.md#policy-files) hello 정책입니다. 몇 가지 수정이 필요한 toohello 기본 합니다.
* hello [확장 파일](active-directory-b2c-overview-custom.md#policy-files) hello 정책입니다.  이 파일은 구성이 대부분 변경되었습니다.
* [신뢰 당사자 파일](active-directory-b2c-overview-custom.md#policy-files)은 응용 프로그램에서 호출하는 작업 관련 파일입니다.

>[!NOTE]
>XML 편집기에서 유효성 검사를 지 원하는 경우 hello 스타터 팩 hello 루트 디렉터리에 있는 hello TrustFrameworkPolicy_0.3.0.0.xsd XML 스키마에 대해 hello 파일의 유효성을 검사 합니다. 업로드하기 전에 XML 스키마 유효성 검사가 오류를 식별합니다.

 이제 시작하겠습니다.

1. GitHub에서 active-directory-b2c-custom-policy-starterpack을 다운로드합니다. [Hello.zip 파일을 다운로드](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) 또는 실행

    ```console
    git clone https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack
    ```
2. Hello SocialAndLocalAccounts 폴더를 엽니다.  hello 기본 파일 (TrustFrameworkBase.xml)이이 폴더에 로컬 및 사회/회사 계정에 필요한 콘텐츠를 포함 합니다. 로컬 계정 시작 및 실행에 대 한 hello 단계 hello 소셜 콘텐츠 방해 하지 않습니다.
3. TrustFrameworkBase.xml을 엽니다. XML 편집기가 필요하면 간단한 플랫폼 간 편집기인 [Visual Studio Code를 사용해 보세요](https://code.visualstudio.com/download).
4. Hello 루트에 `TrustFrameworkPolicy` 요소, 업데이트 hello `TenantId` 및 `PublicPolicyUri` 대체 특성 `yourtenant.onmicrosoft.com` 된 Azure AD B2C 테 넌 트의 도메인 이름이 hello:
   ```xml
    <TrustFrameworkPolicy
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
    PolicySchemaVersion="0.3.0.0"
    TenantId="yourtenant.onmicrosoft.com"
    PolicyId="B2C_1A_TrustFrameworkBase"
    PublicPolicyUri="http://yourtenant.onmicrosoft.com">
    ```
   >[!NOTE]
   >`PolicyId`이 정책 파일은 다른 정책 파일에서 참조 하는 기준인 hello 이름과 hello 정책 이름을 hello 포털에서 볼 수 있는 경우

5. Hello 파일을 저장 합니다.
6. TrustFrameworkExtensions.xml을 엽니다. Hello 같은 두 가지 사항을 변경 대체 하 여 `yourtenant.onmicrosoft.com` Azure AD B2C 테 넌 트와 합니다. 동일한 hello 확인 hello에서 대체 `<TenantId>` 총 3 개의 변경 내용에 대 한 요소입니다. Hello 파일을 저장 합니다.
7. SignUpOrSignIn.xml을 엽니다. 동일 하 게 hello 변경 대체 하 여 `yourtenant.onmicrosoft.com` 다음 세 위치에 Azure AD B2C 테 넌 트와 합니다. Hello 파일을 저장 합니다.
8. 열기 hello 암호 다시 설정 하 고 프로필 파일을 편집 합니다. 동일 하 게 hello 변경 대체 하 여 `yourtenant.onmicrosoft.com` 각 파일에 다음 세 위치에 Azure AD B2C 테 넌 트와 합니다. Hello 파일을 저장 합니다.

### <a name="add-hello-application-ids-tooyour-custom-policy"></a>Hello tooyour 사용자 지정 정책 응용 프로그램 Id를 추가 합니다.
Hello 응용 프로그램 Id toohello 확장 파일에 추가 (`TrustFrameworkExtensions.xml`):

1. Hello 요소 찾기 (TrustFrameworkExtensions.xml) 하는 hello 확장 파일에서 `<TechnicalProfile Id="login-NonInteractive">`합니다.
2. 모두 `IdentityExperienceFrameworkAppId` hello 이전에 만든 Id 경험 프레임 워크 응용 프로그램의 hello 응용 프로그램 id입니다. 다음은 예제입니다.

   ```xml
   <Item Key="client_id">8322dedc-cbf4-43bc-8bb6-141d16f0f489</Item>
   ```
3. 모두 `ProxyIdentityExperienceFrameworkAppId` hello 이전에 만든 프록시 Id 경험 프레임 워크 응용 프로그램의 hello 응용 프로그램 id입니다.
4. 확장 파일을 저장합니다.

## <a name="upload-hello-policies-tooyour-tenant"></a>Hello 정책 tooyour 테 넌 트에 업로드

1. Hello에 [Azure 포털](https://portal.azure.com), hello를 전환 [Azure AD B2C 테 넌 트의 상황에 맞는](active-directory-b2c-navigate-to-b2c-context.md), 및 열기 hello **Azure AD B2C** 블레이드입니다.
2. **ID 경험 프레임워크**를 선택합니다.
3. **정책 업로드**를 선택합니다.

    >[!WARNING]
    >순서에 따라 hello에 hello 사용자 지정 정책 파일을 업로드 해야 합니다.

1. TrustFrameworkBase.xml을 업로드합니다.
2. TrustFrameworkExtensions.xml을 업로드합니다.
3. SignUpOrSignin.xml을 업로드합니다.
4. 다른 정책 파일을 업로드합니다.

파일을 업로드 하면 hello hello 정책 파일의 붙습니다 `B2C_1A_`합니다.

## <a name="test-hello-custom-policy-by-using-run-now"></a>지금 실행에 사용 하 여 hello 사용자 지정 정책 테스트

1. 열기 **Azure AD B2C 설정** 너무 이동**Id 경험 프레임 워크**합니다.

   >[!NOTE]
   >**지금 실행** hello 테 넌 트에 응용 프로그램이 하나 이상 toobe 미리 등록 필요 합니다. Hello를 사용 하 여 hello B2C 테 넌 트에서 응용 프로그램을 등록 해야 **응용 프로그램** 메뉴 선택 Azure AD B2C 또는 Id 경험 프레임 워크 tooinvoke hello를 사용 하 여 기본 및 사용자 지정 정책입니다. 응용 프로그램당 한 번만 등록하면 됩니다.<br><br>
   toolearn tooregister 응용 프로그램을 확인 하려면 어떻게 해야 Azure AD B2C hello [시작](active-directory-b2c-get-started.md) 문서 또는 hello [응용 프로그램 등록](active-directory-b2c-app-registration.md) 문서.  

2. 업로드 하는 신뢰 당사자 (RP) 사용자 지정 정책 hello를 B2C_1A_signup_signin 열고 합니다. **지금 실행**을 선택합니다.

3. 전자 메일 주소를 사용 하 여 수 toosign 있어야 합니다.

4. 동일한 계정 tooconfirm 해야 하는 hello 사용 하 여 로그인 hello 올바른 구성 합니다.

>[!NOTE]
>로그인이 실패하는 것은 일반적으로 잘못 구성된 IdentityExperienceFramework 앱 때문입니다.


## <a name="next-steps"></a>다음 단계

### <a name="add-facebook-as-an-identity-provider"></a>Facebook을 ID 공급자로 추가
Facebook tooset:
1. [developers.facebook.com에서 Facebook 응용 프로그램을 구성합니다](active-directory-b2c-setup-fb-app.md).
2. [Hello Facebook 응용 프로그램 보안 tooyour Azure AD B2C 테 넌 트 추가](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies)합니다.
3. Hello TrustFrameworkExtensions 정책 파일에서의 hello 값 대체 `client_id` hello Facebook 응용 프로그램 id:

   ```xml
   <TechnicalProfile Id="Facebook-OAUTH">
     <Metadata>
     <!--Replace hello value of client_id in this technical profile with hello Facebook app ID"-->
       <Item Key="client_id">00000000000000</Item>
   ```
4. Hello TrustFrameworkExtensions.xml 정책 파일 tooyour 테 넌 트를 업로드 합니다.
5. 사용 하 여 테스트 **지금 실행** hello 정책을 등록 된 응용 프로그램에서 직접 호출 하 여 합니다.

### <a name="add-azure-active-directory-as-an-identity-provider"></a>Azure Active Directory를 ID 공급자로 추가
이 시작된 가이드에서 이미 사용 하는 hello 기본 파일 기타 id 공급자를 추가 하는 데 필요한 hello 콘텐츠 중 일부를 포함 합니다. 로그인 설정에 대 한 자세한 내용은 참조 hello [Azure Active Directory B2C: Azure AD 계정을 사용 하 여 로그인](active-directory-b2c-setup-aad-custom.md) 문서.

Hello Id 경험 프레임 워크를 사용 하는 Azure AD B2C의 사용자 지정 정책 개요를 보려면 hello [Azure Active Directory B2C: 사용자 지정 정책의](active-directory-b2c-overview-custom.md) 문서. 
