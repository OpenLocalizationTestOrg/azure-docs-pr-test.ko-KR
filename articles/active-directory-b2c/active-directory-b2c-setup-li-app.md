---
title: "Azure Active Directory B2C: LinkedIn 구성 | Microsoft Docs"
description: "Azure Active Directory B2C에 의해 보안 되는 응용 프로그램에서 LinkedIn 계정 등록 및 로그인 tooconsumers 제공"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a>Azure Active Directory B2C: LinkedIn 계정 등록 및 로그인 tooconsumers 제공
## <a name="create-a-linkedin-application"></a>LinkedIn 응용 프로그램 만들기
LinkedIn toouse (Azure AD) Azure Active Directory B2C에을 id 공급자로 toocreate LinkedIn 응용 프로그램에 필요 하 고이 hello 오른쪽 매개 변수를 제공 합니다. 하면 LinkedIn 계정 toodo이 필요합니다. 계정이 없는 경우 [https://www.linkedin.com/](https://www.linkedin.com/)에서 가져올 수 있습니다.

1. Toohello 이동 [LinkedIn 개발자 웹 사이트](https://www.developer.linkedin.com/) LinkedIn 계정 자격 증명으로 로그인 합니다.
2. 클릭 **My Apps** 상단 메뉴 모음 hello와 클릭 **응용 프로그램 만들기**합니다.
   
    ![LinkedIn - 새 앱](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. Hello에 **새 응용 프로그램 만들기** 양식에서 hello 관련 정보를 입력 (**회사 이름**, **이름**, **설명**, **응용 프로그램 로고 URL**, **응용 프로그램 사용**, **웹 사이트 URL**, **비즈니스 메일** 및 **회사전화**).
4. Toohello 동의 **LinkedIn 사용 약관 API** 클릭 **전송**합니다.
   
    ![LinkedIn - 앱 등록](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. Hello 값의 복사 **클라이언트 ID** 및 **클라이언트 암호**합니다. (**인증 키** 아래에서 찾을 수 있습니다.) 둘 모두 필요 합니다 tooconfigure 테 넌 트를 id 공급자로 LinkedIn 합니다.
   
   > [!NOTE]
   > **클라이언트 암호** 는 중요한 보안 자격 증명입니다.
   > 
   > 
6. 입력 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello에 **리디렉션 Url 권한이** 필드 (아래 **OAuth 2.0**). **{tenant}** 를 사용자의 테넌트 이름(예: contoso.onmicrosoft.com)으로 바꿉니다. **추가**를 클릭한 후 **업데이트**를 클릭합니다. hello **{tenant}** 값은 대/소문자 구분 합니다.
   
    ![LinkedIn - 앱 설정](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a>테넌트에서 LinkedIn을 ID 공급자로 구성
1. 다음 단계를 너무[toohello B2C 기능 블레이드를 탐색](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure 포털에 있습니다.
2. Hello B2C 기능 블레이드에서 클릭 **Id 공급자**합니다.
3. 클릭 **+ 추가** hello hello 블레이드 위쪽에 있습니다.
4. 친숙 한 제공 **이름** hello id 공급자 구성에 대 한 합니다. 예를 들어 "LI"를 입력합니다.
5. **ID 공급자 형식**을 클릭하고 **LinkedIn**을 선택한 다음 **확인**을 클릭합니다.
6. 클릭 **이 id 공급자 설정** hello 앞에서 만든 LinkedIn 응용 프로그램의 hello 클라이언트 ID와 클라이언트 암호를 입력 합니다.
7. 클릭 **확인** 클릭 하 고 **만들기** toosave LinkedIn 구성 합니다.

