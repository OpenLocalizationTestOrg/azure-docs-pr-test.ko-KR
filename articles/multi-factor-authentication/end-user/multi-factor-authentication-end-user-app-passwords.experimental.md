---
title: "aaaHow toouse Azure MFA에서 앱 암호? | Microsoft Docs"
description: "이 페이지에 앱 암호 및 무엇 인지에 대해 설명 하는 사용자가 도움이 될 큰지에 tooAzure MFA에 사용 합니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 3afa2003d8e87576f035bf9440a1dba67bd85f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a>Azure Multi-factor Authentication에서 앱 암호란 무엇인가요?
현재 Exchange Active Sync를 사용 하는 hello Apple 네이티브 메일 클라이언트와 같은 특정 비 브라우저 앱은 다단계 인증을 지원 하지 않습니다. 다단계 인증은 사용자 기준으로 사용되도록 설정됩니다.  즉, 다음과 같은 경우 사용자가 다단계 인증을 사용할 수 없습니다.

- multi-factor authentication에 대해 hello 사용자가 활성화
- hello 사용자가 비 브라우저 앱 toouse를 시도 합니다.

앱 암호에는 hello 사용자 toouse hello 앱을 수 있습니다.

앱 암호를 만든 후 이러한 비브라우저 앱에서 원래 암호 대신 사용할 수 있습니다. 2 단계 인증에 대 한 등록도 hello 두 번째 확인을 수행할 수 없는 경우 Microsoft 서명 누구나 toolet 하지 암호를 사용 하 여 지시 하는 합니다. 휴대폰에서 hello Apple 네이티브 메일 클라이언트 로그인 할 수 없습니다와 2 단계 인증을 요청할 수 없습니다. hello 솔루션 toothis 문제는 사용 하지 않는 좀 더 안전한 앱 암호 toocreate 일상적인 합니다. 앱 암호는 2단계 인증을 지원하지 않는 그러한 앱을 위한 것입니다. 앱에서 multi-factor authentication을 바이패스 하 고 toowork 계속할 수 있도록 hello 앱 암호를 사용 합니다.


> [!NOTE]
> Outlook을 포함한 Office 2013 클라이언트는 새로운 인증 프로토콜을 지원하며 2단계 인증과 함께 사용할 수 있습니다. Office 2013 클라이언트는 앱 암호를 사용할 필요가 없습니다.  자세한 내용은 [발표된 Office 2013 최신 인증 공개 미리 보기](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)를 참조하세요.


## <a name="how-toouse-app-passwords"></a>어떻게 toouse 앱 암호
다음은 일부의 tooknow प ् ल ि입니다.

* 사용자 고유의 앱 암호를 만들지 않습니다. 자동으로 생성됩니다.
* 현재 사용자 당 40개의 암호로 제한되어 있습니다. 
* Hello 제한에 도달한 후 toocreate 앱 암호를 시도 하면 해야 toodelete 기존 앱 암호 중 하나 새를 만들어야 합니다.
* 응용 프로그램 단위가 아니라 장치별로 앱 암호 하나만 사용합니다. 예를 들어 노트북에 사용할 앱 암호를 하나 만든 다음 노트북의 모든 응용 프로그램에 이 앱 암호를 사용할 수 있습니다. 그런 다음 모든 앱에 대 한 두 번째 응용 프로그램 암호 toouse를 바탕 화면에 만듭니다. 
* 처음 등록할 때 2 단계 인증에 대 한 하나의 앱 암호 hello를 제공 됩니다.  추가 암호가 필요한 경우 만들 수 있습니다.



## <a name="creating-and-deleting-app-passwords"></a>앱 암호 만들기 및 삭제
초기 로그인 중에 사용할 수 있는 앱 암호가 제공됩니다.  또한 나중에 앱 암호를 만들고 삭제할 수도 있습니다. 앱 암호 삭제 방법은 다단계 인증을 사용하는 방법에 따라 달라집니다. 다음 응답 hello toomanage 앱 암호를 어디로 해야 toodetermine 관련 질문: 

1. 개인 Microsoft 계정에 대해 2단계 인증을 사용합니까? 그렇다면 toohello 참조 해야 [앱 암호와 2 단계 인증](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) 문서에 대 한 도움말입니다. 그렇지 않은 경우, 두 tooquestion을 계속 합니다.

2. 이제 직장이나 학교 계정에 대해 2단계 인증을 사용합니다. 사용 합니까 것 toosign tooOffice 365 앱에서? 그러한 경우를 참조 해야 너무[Office 365에 대 한 앱 암호를 만들](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) 에 대 한 도움말입니다. 그렇지 않은 경우, 3 tooquestion를 계속 합니다. 

3. Microsoft Azure에서 2단계 인증을 사용합니까? 그러한 경우 계속 toohello [hello Azure 포털에서에서 앱 암호를 관리](#manage-app-passwords-in-the-Azure-portal) 이 문서의 섹션. 그렇지 않은 경우, tooquestion 4를 계속 합니다.

4. 2단계 인증을 사용하는 위치를 모르십니까? Toohello 계속 [hello MyApps 포털과 응용 프로그램 암호 관리](#manage-app-passwords-with-the-myapps-portal) 이 문서의 섹션. 


## <a name="manage-app-passwords-in-hello-azure-portal"></a>Hello Azure 포털에서에서 앱 암호를 관리
Azure를 사용한 2 단계 인증을 사용 하는 경우 원하는 hello Azure 포털을 통해 toocreate 앱 암호입니다.

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a>hello Azure 포털에서에서 toocreate 앱 암호
1. Azure 클래식 포털 toohello에 로그인 합니다.
2. Hello 위쪽에 사용자 이름을 마우스 오른쪽 단추로 클릭 하 고 추가 보안 확인을 선택 합니다.
3. Hello 위쪽에, hello 검사 페이지에서 앱 암호를 선택 합니다.
4. **만들기**를 클릭합니다.
5. Hello 앱 암호에 대 한 이름을 입력 하 고 클릭 **다음**
6. Hello 앱 암호 toohello 클립보드로 복사한 응용 프로그램에 붙여 넣습니다.
   
   ![클라우드](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a>hello Azure 포털에서에서 toodelete 앱 암호
1. Azure 클래식 포털 toohello에 로그인 합니다.
2. Hello 위쪽에 사용자 이름을 마우스 오른쪽 단추로 클릭 하 고 추가 보안 확인을 선택 합니다.
3. 다음 tooadditional 보안 확인 hello 위쪽 선택 **앱 암호입니다.**
4. 다음 toohello 앱 암호 toodelete, 원하는 **삭제**합니다.
5. 클릭 하 여 hello 삭제를 확인 **예**합니다.
6. Hello 앱 암호를 삭제 한 후 클릭할 수 있는 **닫습니다**합니다.


## <a name="manage-app-passwords-with-hello-myapps-portal"></a>Hello MyApps 포털과 앱 암호를 관리 합니다.
다단계 인증을 사용 하는 방법을 확실 하지 않은 경우 다음 수 항상 만들고 hello myapps 포털을 통해 앱 암호 삭제 합니다.

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a>사용 하 여 앱 암호 toocreate hello Myapps 포털
1. 역시 로그인[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. Hello 위쪽, 오른쪽에 있는 사용자 이름을 클릭 하 고 선택 **프로필**합니다.
3. **추가 보안 인증**을 선택합니다.
   ![추가 보안 인증 선택 - 스크린샷](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. **앱 암호**를 선택합니다.
   ![앱 암호 선택 - 스크린샷](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. **만들기**를 클릭합니다.
6. Hello 앱 암호에 대 한 이름을 입력 하 고 클릭 **다음**합니다.
7. Hello 앱 암호 toohello 클립보드로 복사한 응용 프로그램에 붙여 넣습니다.
   ![앱 암호 만들기](./media/multi-factor-authentication-end-user-app-passwords/create2.png)

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a>사용 하 여 앱 암호 toodelete hello Myapps 포털
1. 역시 로그인[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. Hello 위쪽에, 프로필을 선택 합니다.
3. **추가 보안 인증**을 선택합니다.

   ![추가 보안 인증 선택 - 스크린샷](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. **앱 암호**를 선택합니다.

   ![앱 암호 선택 - 스크린샷](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. 다음 toohello 앱 암호 toodelete, 원하는 클릭 **삭제**합니다.

   ![앱 암호 삭제](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. 것인지 확인 하는 toodelete 해당 암호를 클릭 하 여 **예**합니다.
7. Hello 앱 암호를 삭제 한 후 클릭할 수 있는 **닫습니다**합니다.

## <a name="next-steps"></a>다음 단계

- [2단계 인증 설정 관리](multi-factor-authentication-end-user-manage-settings.md)

- Hello 사용해 [Microsoft Authenticator 앱](microsoft-authenticator-app-how-to.md) tooverify 사용자 로그인을 대신 텍스트 또는 호출 응용 프로그램 알림입니다. 
