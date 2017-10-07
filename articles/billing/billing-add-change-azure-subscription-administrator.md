---
title: "Azure 관리자 구독 역할 aaaAdd 또는 변경 | Microsoft Docs"
description: "설명 방법을 tooadd Azure 공동 관리자, 서비스 관리자 및 계정 관리자 또는 변경"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 13a72d76-e043-4212-bcac-a35f4a27ee26
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: genli
ms.openlocfilehash: 14eaecf2dbfd7152775ac3552bf3a7ae3db596b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-change-azure-administrator-roles-that-manage-hello-subscription-or-services"></a>추가 하거나 hello 구독 또는 서비스를 관리 하는 Azure 관리자 역할 변경
변경할 수 있습니다를 Azure 구독을 관리 하거나 관리 하는 Azure 관리자 hello hello 구독에 사용 되는 Azure 서비스입니다. Azure 청구 정보 tooview 및 구독 관리, toohello에 로그인 해야 [r e 계정 센터](https://account.windowsazure.com/Home/Index) 계정 관리자 hello으로 합니다. 

## <a name="add-an-admin-for-a-subscription"></a>구독에 대한 관리자 추가
Azure 관리자 또는 Azure 클래식 포털 hello hello Azure 포털에에서 추가할 수 있습니다.

**Azure 포털**

tooadd hello Azure 포털에서에서 구독에 대 한 관리자의 사용자 제공 하면 hello 소유자 역할입니다. hello 소유자 역할 할당 하는 hello 구독의 hello 리소스 관리할 수 있습니다. 액세스 권한 tooother 구독 없는 합니다. hello를 통해 추가 된 소유자 hello [Azure 포털](https://portal.azure.com) hello에 리소스를 관리할 수 없는 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 허브 메뉴에서 선택 **구독** > *hello 관리자 tooaccess 구독 hello*합니다.

    ![선택한 구독을 보여 주는 스크린샷](./media/billing-add-change-azure-subscription-administrator/newselectsub.png)

3. 구독 블레이드에서 hello 선택 **액세스 제어 (IAM)**합니다.
4. **추가** > **역할** > **소유자**를 선택합니다. Hello 사용자 tooadd 소유자로 선택 hello 사용자 한 다음 선택의 hello 전자 메일 주소 입력 **저장**합니다.

    ![선택한 hello 소유자 역할을 보여 주는 스크린샷](./media/billing-add-change-azure-subscription-administrator/add-role.png)

5. Hello에 공동 관리자로 tooadd hello 소유자 계정을 원하는 **액세스 제어 (IAM)** 페이지를 hello 사용자를 마우스 오른쪽 단추로 클릭 한 다음 선택 **공동 관리자로 추가**합니다. 이 기능은 이제 [Azure 미리 보기 포털](https://preview.portal.azure.com/)에서 사용할 수 있습니다. 

     ![공동 관리자를 추가하는 스크린샷](./media/billing-add-change-azure-subscription-administrator/add-coadmin.png)

    >[!TIP]
    >해야 tooadd hello "소유자" 사용자 공동 관리자로 hello 사용자 toomanage 있어야 하는 경우에서 Azure 서비스 hello [Azure 클래식 포털](https://manage.windowsazure.com/)합니다.

    tooremove hello 공동 관리자 권한을 hello "공동 관리자" 사용자를 마우스 오른쪽 단추로 클릭 한 다음 선택 **공동 관리자 제거**합니다.

    ![공동 관리자를 제거하는 스크린샷](./media/billing-add-change-azure-subscription-administrator/remove-coadmin.png)


**Azure 클래식 포털**

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/)합니다.
2. Hello 탐색 창에서 선택 **설정**> **관리자**> **추가**합니다. </br>

    ![Tooget toohello 단추를 추가 하는 방법을 보여 주는 스크린샷](./media/billing-add-change-azure-subscription-administrator/addcoadmin.png)
3. 공동 관리자 및 공동 관리자 tooaccess hello를 선택한 후 hello 구독으로 tooadd 원하는 hello 사람의 hello 전자 메일 주소를 입력 합니다.</br>

    ![선택한 구독을 보여 주는 스크린샷 ](./media/billing-add-change-azure-subscription-administrator/addcoadmin2.png)</br>

전자 메일 주소 다음 hello 공동 관리자로 추가할 수 있습니다.

* **Microsoft 계정**(이전 Windows Live ID) </br>
  Microsoft 계정 toosign tooall 소비자 중심 Microsoft 제품에서 사용할 수 있으며 Outlook (Hotmail), (MSN) Skype, OneDrive, Windows Phone 및 Xbox LIVE 등 클라우드 서비스와 수도 있습니다.
* **Organizational account**</br>
  조직 계정은 Azure Active Directory에 만들어지는 계정입니다. hello 조직 계정 주소이 형식은 다음과 같습니다.

    user@&lt;도메인&gt;.onmicrosoft.com

## <a name="change-service-administrator-for-a-subscription"></a>구독에 대한 서비스 관리자 변경
Hello 계정 관리자만 hello 서비스 관리자는 구독에 대 한 변경할 수 있습니다.

1. 역시 로그인[Azure 계정 센터](https://account.windowsazure.com/subscriptions) hello 계정 관리자를 사용 하 여 합니다.
2. Toochange hello 구독을 선택 합니다.
3. Hello 오른쪽에 선택 **구독 편집** 세부 정보입니다. </br>

    ![editsub](./media/billing-add-change-azure-subscription-administrator/editsub.png)
4. Hello에 **서비스 관리자** 상자 hello의 hello 전자 메일 주소를 입력 새 서비스 관리자. </br>

    ![changeSA](./media/billing-add-change-azure-subscription-administrator/changeSA.png)

## <a name="change-hello-account-administrator"></a>계정 관리자 hello 변경
Azure 계정 tooanother 계정 hello의 tootransfer 소유권 참조 [Azure 구독의 소유권을 전송](billing-subscription-transfer.md)합니다.

삭제 하거나 이름을 hello 계정 관리자의 전자 메일 주소를 변경 하지 않는 것이 좋습니다. Azure 계정 hello로 예기치 않은 또는 원하지 않는 동작이 발생할 수 있습니다. 해당 계정으로 수 로그인 tooAzure 수, toohello 계정을 변경 하거나 수 해당 계정으로 리소스를 관리 합니다. 

## <a name="check-hello-account-administrator-of-hello-subscription"></a>Hello hello 구독의 계정 관리자를 확인 합니다.
확실 하지 않은 구독에 대 한 계정 관리자에 게 인을 하는 경우 아웃 toofind 단계를 수행 하는 hello를 사용 합니다.

  1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
  2. Hello 허브 메뉴에서 선택 **구독**합니다.
  3. Hello 구독 toocheck을 다음 선택 **설정을**합니다.
  4. **속성**을 선택합니다. hello에 hello 구독의 계정 관리자에 게 표시 되 **계정 관리자** 상자입니다.  

## <a name="types-of-azure-admin-accounts"></a>Azure 관리자 계정 유형
 계정 관리자, 서비스 관리자 및 공동 관리자 hello 세 가지 Microsoft Azure에서 역할 관리자입니다. hello 다음 표에 hello 차이 이러한 세 가지 관리 역할이 있습니다.

| 관리 역할 | 제한 | 설명 |
| --- | --- | --- |
| 계정 관리자(AA) |Azure 계정당 1개 |에 등록 또는 Azure 구독을 구입 하 고는 권한 있는 tooaccess hello hello 사람 이것이 [r e 계정 센터](https://account.windowsazure.com/Home/Index) 다양 한 관리 작업을 수행 합니다. 이러한 수 toocreate 구독 되, 구독 취소, 구독에 대 한 hello 청구 변경 및 hello 서비스 관리자를 변경 합니다. |
| 서비스 관리자(SA) |Azure 구독당 1개 |이 역할은 hello에 권한이 부여 된 toomanage 서비스 [Azure 포털](https://portal.azure.com)합니다. 기본적으로 새 구독에 대 한 hello 계정 관리자는 또한 hello 서비스 관리자입니다. |
| Hello에 공동 관리자 (CA) [Azure 클래식 포털](https://manage.windowsazure.com) |구독당 200 |이 역할 hello에 대 한 액세스 권한이 hello 서비스 관리자와 동일 하지만 구독 tooAzure 디렉터리의 hello 연결을 변경할 수 없습니다. |

Azure Active Directory 역할 기반 액세스 제어 (RBAC)를 사용 하면 toobe toomultiple 역할을 추가 합니다. 자세한 내용은 [Azure Active Directory 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)를 참조하세요.

## <a name="limitations-and-restrictions-for-admin-accounts"></a>관리자 계정에 대한 제한 사항
* 각 구독은 Azure AD 디렉터리 (라고도 hello 기본 디렉터리)와 연결 됩니다. 기본 디렉터리 hello 구독 toofind hello 이동 toohello와 연결 된 [Azure 클래식 포털](https://manage.windowsazure.com/)선택, **설정** > **구독**합니다. Hello 구독 ID toofind hello 기본 디렉터리를 확인 합니다.
* Microsoft 계정으로 로그인 한 경우 공동 관리자로 서 다른 Microsoft 계정 또는 hello 기본 디렉터리 내에서 사용자가 추가할만 있습니다.
* 조직 계정으로 로그인하는 경우 해당 조직의 다른 조직 계정을 공동 관리자로 추가할 수 있습니다. 예를 들어 abby@contoso.com은 bob@contoso.com을 서비스 관리자 또는 공동 관리자로 추가할 수 있지만 john@notcontoso.com이 기본 디렉터리에 있지 않으면 john@notcontoso.com은 추가할 수 없습니다. 조직 계정을 사용 하 여 로그인 하는 사용자가 공동 관리자 또는 서비스 관리자로 Microsoft 계정 사용자 tooadd 계속 수 있습니다.
* 조직 계정이 있는 tooAzure에서 가능한 toosign 이면이 hello 변경 tooService 관리자 및 공동 관리자 계정 요구 사항:

  | 로그인 방법 | 기본 디렉터리 내에서 Microsoft 계정 또는 사용자를 CA 또는 SA로 추가하나요? | Hello에서 조직 계정을 추가 SA 또는 CA와 동일한 조직? | 다른 조직의 조직 계정을 CA 또는 SA로 추가하나요? |
  | --- | --- | --- | --- |
  |  Microsoft 계정 |예 |아니요 |아니요 |
  |  조직 계정 |예 |예 |아니요 |

## <a name="learn-more-about-resource-access-control-and-active-directory"></a>리소스 액세스 제어 및 Active Directory에 대해 자세히 알아보기
* Microsoft Azure에서 리소스 액세스 제어 하는 방법에 대 한 자세한 toolearn 참조 [Azure에서 리소스 액세스 이해](../active-directory/active-directory-understanding-resource-access.md)합니다.
* Azure Active Directory에 대한 자세한 내용은 [Azure 구독을 Azure Active Directory에 연결하는 방법](../active-directory/active-directory-how-subscriptions-associated-directory.md) 및 [Azure Active Directory에서 관리자 역할 할당](../active-directory/active-directory-assign-admin-roles.md)을 참조하세요.

## <a name="need-help-contact-support"></a>도움이 필요하세요? 지원에 문의하세요.
도움이 필요 하면 여전히 필요 하면 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget 문제가 해결 신속 하 게 합니다.
