---
title: "Azure Active Directory B2C: WeChat 구성 | Microsoft Docs"
description: "등록 및 로그인 tooconsumers WeChat 계정 Azure Active Directory B2C에 의해 보안 되는 응용 프로그램에 제공 합니다."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a>Azure Active Directory B2C: WeChat 계정 등록 및 로그인 tooconsumers 제공

> [!NOTE]
> 이 기능은 미리 보기 상태입니다.
> 

## <a name="create-a-wechat-application"></a>WeChat 응용 프로그램 만들기

toouse WeChat (Azure AD) Azure Active Directory B2C에을 id 공급자로 toocreate WeChat 응용 프로그램에 필요 하 고이 hello 오른쪽 매개 변수를 제공 합니다. 하면 WeChat 계정 toodo이 필요합니다. 없는 경우 모바일 앱 중 하나를 통해 등록하거나 QQ 번호를 사용하여 하나를 얻을 수 있습니다. 그 후에 등록 된 hello WeChat 개발자 프로그램 계정을 가져옵니다. 자세한 내용은 [여기](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html)에서 찾을 수 있습니다.

### <a name="register-a-wechat-application"></a>WeChat 응용 프로그램 등록

1. 너무 이동[https://open.weixin.qq.com/](https://open.weixin.qq.com/) 로그인 하십시오.
2. **管理中心**(관리 센터)를 클릭합니다.
3. Hello 필요한 단계 tooregister 새 응용 프로그램을 따릅니다.
4. **授权回调域**(콜백 URL)에 `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`를 입력합니다. 예를 들어 경우 프로그램 `tenant_name` contoso.onmicrosoft.com 집합 hello URL toobe은 `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`합니다.
5. 찾기 및 복사 hello **앱 ID** 및 **응용 프로그램 키는**합니다. 나중에 필요합니다.

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a>테넌트에서 WeChat을 ID 공급자로 구성
1. 다음 단계를 너무[toohello B2C 기능 블레이드를 탐색](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure 포털에 있습니다.
2. Hello B2C 기능 블레이드에서 클릭 **Id 공급자**합니다.
3. 클릭 **+ 추가** hello hello 블레이드 위쪽에 있습니다.
4. 친숙 한 제공 **이름** hello id 공급자 구성에 대 한 합니다. 예를 들어 "WeChat"을 입력합니다.
5. **ID 공급자 형식**을 클릭하고 **WeChat**을 선택한 다음 **확인**을 클릭합니다.
6. **이 ID 공급자 설정**을 클릭합니다.
7. Hello 입력 **응용 프로그램 키는** hello로 앞에서 복사한 **클라이언트 ID**합니다.
8. Hello 입력 **응용 프로그램 암호** hello로 앞에서 복사한 **클라이언트 암호**합니다.
9. 클릭 **확인** 클릭 하 고 **만들기** toosave WeChat 구성 합니다.

