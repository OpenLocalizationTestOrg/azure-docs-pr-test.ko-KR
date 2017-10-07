---
title: "Azure Active Directory B2C: Google+ 구성 | Microsoft Docs"
description: "Azure Active Directory B2C에 의해 보안 되는 응용 프로그램에서 Google + 계정 등록 및 로그인 tooconsumers를 제공 합니다."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a>Azure Active Directory B2C: Google + 계정 등록 및 로그인 tooconsumers 제공
## <a name="create-a-google-application"></a>Google+ 응용 프로그램 만들기
toouse Google + (Azure AD) Azure Active Directory B2C에을 id 공급자로 toocreate Google + 응용 프로그램에 필요 하 고이 hello 오른쪽 매개 변수를 제공 합니다. 사용자는 Google + 계정 toodo이 필요합니다. 계정이 없으면 [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)에서 만들 수 있습니다.

1. Toohello 이동 [Google 개발자 콘솔](https://console.developers.google.com/) 및 Google + 계정 자격 증명을 사용 하 여 로그인 합니다.
2. **프로젝트 만들기**를 클릭하고 **프로젝트 이름**을 입력한 다음 **만들기**를 클릭합니다.
   
    ![Google+ - 시작](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+ - 새 프로젝트](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. 클릭 **API 관리자** 클릭 하 고 **자격 증명** 왼쪽 탐색 hello에 있습니다.
4. Hello 클릭 **OAuth 동의 화면** hello 위쪽 탭 합니다.
   
    ![Google+ - 자격 증명](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. 유효한 **메일 주소**를 선택하거나 지정하고 **제품 이름**을 제공한 후 **저장**을 클릭합니다.
   
    ![Google+ - OAuth 동의 화면](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. **새 자격 증명**을 클릭한 다음 **OAuth 클라이언트 ID**를 선택합니다.
   
    ![Google+ - OAuth 동의 화면](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. **응용 프로그램 형식**에서 **웹 응용 프로그램**을 선택합니다.
   
    ![Google+ - OAuth 동의 화면](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. 제공는 **이름** 응용 프로그램에 대 한 입력 `https://login.microsoftonline.com` hello에 **승인 된 자바 스크립트 원본** 필드 및 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello에 **권한이 부여 된 리디렉션 URIs**필드입니다. **{tenant}** 를 사용자의 테넌트 이름(예: contosob2c.onmicrosoft.com)으로 바꿉니다. hello **{tenant}** 값은 대/소문자 구분 합니다. **만들기**를 클릭합니다.
   
    ![Google+ - 클라이언트 ID 만들기](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. Hello 값의 복사 **클라이언트 ID** 및 **클라이언트 암호**합니다. 둘 모두 필요 합니다 tooconfigure Google + 테 넌 트를 id 공급자로 합니다. **클라이언트 암호** 는 중요한 보안 자격 증명입니다.
   
    ![Google+ - 클라이언트 암호](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a>테넌트에서 Google+를 ID 공급자로 구성
1. 다음 단계를 너무[toohello B2C 기능 블레이드를 탐색](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure 포털에 있습니다.
2. Hello B2C 기능 블레이드에서 클릭 **Id 공급자**합니다.
3. 클릭 **+ 추가** hello hello 블레이드 위쪽에 있습니다.
4. 친숙 한 제공 **이름** hello id 공급자 구성에 대 한 합니다. 예를 들어 "G+"를 입력합니다.
5. **ID 공급자 형식**을 클릭하고 **Google**을 선택한 다음 **확인**을 클릭합니다.
6. 클릭 **이 id 공급자 설정** hello 앞에서 만든 Google + 응용 프로그램의 hello 클라이언트 ID와 클라이언트 암호를 입력 합니다.
7. 클릭 **확인** 클릭 하 고 **만들기** toosave Google + 구성 합니다.

