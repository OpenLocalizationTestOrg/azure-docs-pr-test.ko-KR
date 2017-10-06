---
title: "Azure Active Directory B2C: Weibo 구성 | Microsoft Docs"
description: "등록 및 로그인 tooconsumers Weibo 계정 Azure Active Directory B2C에 의해 보안 되는 응용 프로그램에 제공 합니다."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a>Azure Active Directory B2C: Weibo 계정 등록 및 로그인 tooconsumers 제공

> [!NOTE]
> 이 기능은 미리 보기 상태입니다. 프로덕션 환경에서는 이 ID 공급자를 사용하지 마세요.
> 

## <a name="create-a-weibo-application"></a>Weibo 응용 프로그램 만들기

toouse Weibo (Azure AD) Azure Active Directory B2C에을 id 공급자로 toocreate Weibo 응용 프로그램에 필요 하 고이 hello 오른쪽 매개 변수를 제공 합니다. 하면 Weibo 계정 toodo이 필요합니다. 없는 경우 [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us)에서 가져올 수 있습니다.

### <a name="register-for-hello-weibo-developer-program"></a>Hello Weibo 개발자 프로그램에 대 한 등록

1. Toohello 이동 [Weibo 개발자 포털](http://open.weibo.com/) Weibo 계정 자격 증명으로 로그인 합니다.
2. 로그인 한 후 hello 오른쪽 위 모서리에는 표시 이름을 클릭 합니다.
3. Hello 드롭다운에서 선택**编辑开发者信息**(개발자 정보 편집).
4. Hello 양식으로 hello 필요한 정보를 입력 하 고 클릭**提交**(전송) 합니다.
5. Hello 전자 메일 확인 프로세스를 완료 합니다.
6. Toohello 이동 [id 확인 페이지](http://open.weibo.com/developers/identity/edit)합니다.
7. Hello 양식으로 hello 필요한 정보를 입력 하 고 클릭**提交**(전송) 합니다.

### <a name="register-a-weibo-application"></a>Weibo 응용 프로그램 등록

1. Toohello 이동 [새 Weibo 응용 프로그램 등록 페이지](http://open.weibo.com/apps/new)합니다.
2. Hello 필요한 응용 프로그램 정보를 입력 합니다.
3. **创 建**(만들기)를 클릭합니다.
4. Hello 값의 복사 **응용 프로그램 키는** 및 **응용 프로그램 암호**합니다. 이 ID는 나중에 필요합니다.
5. 필요한 hello 사진을 업로드 하 고 hello 필요한 정보를 입력 합니다.
6. **保存以上信息**(저장)을 클릭합니다.
7. **高级信息**(고급 정보)를 클릭합니다.
8. 클릭**编辑**oauth 2.0에 대 한 다음 toohello 필드 (편집)**授权设置**(URL 리디렉션).
9. OAuth2.0 **授权设置**(리디렉션 URL)에 `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`를 입력합니다. 예를 들어 경우 프로그램 `tenant_name` contoso.onmicrosoft.com 집합 hello URL toobe은 `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`합니다.
10. **提交**(제출)을 클릭합니다.  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a>테넌트에서 Weibo를 ID 공급자로 구성
1. 다음 단계를 너무[toohello B2C 기능 블레이드를 탐색](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure 포털에 있습니다.
2. Hello B2C 기능 블레이드에서 클릭 **Id 공급자**합니다.
3. 클릭 **+ 추가** hello hello 블레이드 위쪽에 있습니다.
4. 친숙 한 제공 **이름** hello id 공급자 구성에 대 한 합니다. 예를 들어 "Weibo"를 입력합니다.
5. **ID 공급자 형식**을 클릭하고 **Weibo**를 선택한 다음 **확인**을 클릭합니다.
6. **이 ID 공급자 설정**을 클릭합니다.
7. Hello 입력 **응용 프로그램 키는** hello로 앞에서 복사한 **클라이언트 ID**합니다.
8. Hello 입력 **응용 프로그램 암호** hello로 앞에서 복사한 **클라이언트 암호**합니다.
9. 클릭 **확인** 클릭 하 고 **만들기** toosave Weibo 구성 합니다.

