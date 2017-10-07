---
title: "Azure Active Directory B2C: Amazon 구성 | Microsoft Docs"
description: "등록 및 로그인 tooconsumers Amazon 계정 Azure Active Directory B2C에 의해 보안 되는 응용 프로그램에 제공 합니다."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a>Azure Active Directory B2C: Amazon 계정 등록 및 로그인 tooconsumers 제공
## <a name="create-an-amazon-application"></a>Amazon 응용 프로그램 만들기
Amazon toouse (Azure AD) Azure Active Directory B2C에을 id 공급자로 toocreate Amazon 응용 프로그램에 필요 하 고이 hello 오른쪽 매개 변수를 제공 합니다. 하면 Amazon 계정 toodo이 필요합니다. 계정이 없는 경우 [http://www.amazon.com/](http://www.amazon.com/)에서 가져올 수 있습니다.

1. Toohello 이동 [Amazon Developer Center](https://login.amazon.com/) Amazon 계정 자격 증명으로 로그인 합니다.
2. 이미 수행 하는 경우 클릭 **등록**hello 개발자 등록 단계를 수행 하 고 hello 방침에 동의 합니다.
3. **새 응용 프로그램 등록**을 클릭합니다.
   
    ![Hello Amazon 웹 사이트에서 새 응용 프로그램 등록](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. 응용 프로그램 정보(**이름**, **설명** 및 **개인 정보 알림 URL**)를 제공하고 **저장**을 클릭합니다.
   
    ![Amazon에 새 응용 프로그램을 등록하기 위한 응용 프로그램 정보 제공](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. Hello에 **웹 설정** 섹션의 hello 값 복사 **클라이언트 ID** 및 **클라이언트 암호**합니다. (Tooclick hello 필요한 **암호 표시** toosee 단추입니다.) 둘 다 필요 tooconfigure 테 넌 트를 id 공급자로 Amazon 합니다. 클릭 **편집** hello hello 섹션 맨 아래에 있습니다. **클라이언트 암호** 는 중요한 보안 자격 증명입니다.
   
    ![Amazon에 새 응용 프로그램에 대한 클라이언트 ID 및 클라이언트 암호 제공](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. 입력 `https://login.microsoftonline.com` hello에 **허용 자바 스크립트 원본** 필드 및 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello에 **반환 Url 허용** 필드입니다. **{tenant}** 를 사용자의 테넌트 이름(예: contoso.onmicrosoft.com)으로 바꿉니다. **Save**를 클릭합니다. hello **{tenant}** 값은 대/소문자 구분 합니다.
   
    ![Amazon에 새 응용 프로그램에 대한 JavaScript 원본 및 반환 URL 제공](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a>테넌트에서 Amazon을 ID 공급자로 구성
1. 다음 단계를 너무[toohello B2C 기능 블레이드를 탐색](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure 포털에 있습니다.
2. Hello B2C 기능 블레이드에서 클릭 **Id 공급자**합니다.
3. 클릭 **+ 추가** hello hello 블레이드 위쪽에 있습니다.
4. 친숙 한 제공 **이름** hello id 공급자 구성에 대 한 합니다. 예를 들어 "Amzn"을 입력합니다.
5. **ID 공급자 형식**을 클릭하고 **Amazon**을 선택한 다음 **확인**을 클릭합니다.
6. 클릭 **이 id 공급자 설정** hello 앞에서 만든 Amazon 응용 프로그램의 hello 클라이언트 ID와 클라이언트 암호를 입력 합니다.
7. 클릭 **확인** 클릭 하 고 **만들기** toosave Amazon 구성 합니다.

