---
title: "Azure Active Directory B2C: QQ 구성 | Microsoft Docs"
description: "등록 및 로그인 tooconsumers QQ 계정 Azure Active Directory B2C에 의해 보안 되는 응용 프로그램에 제공 합니다."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a>Azure Active Directory B2C: QQ 계정 등록 및 로그인 tooconsumers 제공

> [!NOTE]
> 이 기능은 미리 보기 상태입니다.
> 

## <a name="create-a-qq-application"></a>QQ 응용 프로그램 만들기

toouse QQ (Azure AD) Azure Active Directory B2C에을 id 공급자로 toocreate QQ 응용 프로그램에 필요 하 고이 hello 오른쪽 매개 변수를 제공 합니다. 하면 QQ 계정 toodo이 필요합니다. 없는 경우 [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033)에서 가져올 수 있습니다.

### <a name="register-for-hello-qq-developer-program"></a>Hello QQ 개발자 프로그램에 대 한 등록

1. Toohello 이동 [QQ 개발자 포털](http://open.qq.com) QQ 계정 자격 증명으로 로그인 합니다.
2. 로그인 한 후 이동 너무[http://open.qq.com/reg](http://open.qq.com/reg) tooregister 개발자로 서 사용자가 직접 합니다.
3. Hello 메뉴에서 선택**个人**(개별 개발자).
4. Hello 양식으로 hello 필요한 정보를 입력 하 고 클릭**下一步**(다음 단계).
5. Hello 전자 메일 확인 프로세스를 완료 합니다.

> [!NOTE]
> Toowait 몇 일 toobe 개발자 등록 한 후 승인 해야 합니다. 

### <a name="register-a-qq-application"></a>QQ 응용 프로그램 등록

1. 너무 이동[https://connect.qq.com/index.html](https://connect.qq.com/index.html)합니다.
2. **应用管理**(앱 관리)를 클릭합니다.
3. **创建应用**(앱 만들기)를 클릭합니다.
4. Hello 필요한 응용 프로그램 정보를 입력 합니다.
5. **创建应用**(앱 만들기)를 클릭합니다.
6. Hello 필요한 정보를 입력 합니다.
7. Hello에 대 한**授权回调域**(콜백 URL) 필드에, 입력 `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`합니다. 예를 들어 경우 프로그램 `tenant_name` contoso.onmicrosoft.com 집합 hello URL toobe은 `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`합니다.
8. **创建应用**(앱 만들기)를 클릭합니다.
9. Hello 확인 페이지에서 클릭**应用管理**tooreturn toohello 응용 프로그램 관리 페이지 (앱 관리).
10. 클릭**查看**방금 만든 (뷰) 다음 toohello 앱.
11. **修改**(편집)을 클릭합니다.
12. Hello hello 페이지의 위쪽에서 복사 hello **앱 ID** 및 **응용 프로그램 키는**합니다.

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a>테넌트에서 QQ를 ID 공급자로 구성
1. 다음 단계를 너무[toohello B2C 기능 블레이드를 탐색](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure 포털에 있습니다.
2. Hello B2C 기능 블레이드에서 클릭 **Id 공급자**합니다.
3. 클릭 **+ 추가** hello hello 블레이드 위쪽에 있습니다.
4. 친숙 한 제공 **이름** hello id 공급자 구성에 대 한 합니다. 예를 들어 "QQ"를 입력합니다.
5. **ID 공급자 형식**을 클릭하고 **QQ**를 선택한 다음 **확인**을 클릭합니다.
6. **이 ID 공급자 설정**을 클릭합니다.
7. Hello 입력 **응용 프로그램 키는** hello로 앞에서 복사한 **클라이언트 ID**합니다.
8. Hello 입력 **응용 프로그램 암호** hello로 앞에서 복사한 **클라이언트 암호**합니다.
9. 클릭 **확인** 클릭 하 고 **만들기** toosave QQ 구성 합니다.

