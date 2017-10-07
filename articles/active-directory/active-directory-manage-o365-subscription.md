---
title: "Azure에서 Office 365 구독에 대 한 aaaManage hello 디렉터리 | Microsoft Docs"
description: "Azure Active Directory 및 hello Azure 클래식 포털을 사용 하는 Office 365 구독 디렉터리 관리"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 746987b7-2dfd-4b35-819d-37c1b65c5c81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4faf9936d7e94b85356a18adfcf3d2a48e5b025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-directory-for-your-office-365-subscription-in-azure"></a>Hello Azure에서 Office 365 구독의 디렉터리 관리
이 문서에서는 설명 방법을 toomanage hello Azure 클래식 포털을 사용 하 여 Office 365 구독에 대해 생성 된 디렉터리입니다. Hello 서비스 관리자 또는 공동 관리자는 Azure 구독 toosign toohello Azure 클래식 포털에서에서 중 하나 여야 합니다. Azure 구독이 없는 경우 지금 [무료 30일 평가판](https://azure.microsoft.com/trial/get-started-active-directory/) 에 등록하면 이 링크를 사용하여 5분 내에 첫 번째 클라우드 솔루션을 배포할 수 있습니다. 있는지 toouse hello 작업이 ळ ा ख tooOffice 365에서는 toosign를 사용 합니다.

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.

Hello Azure 구독을 완료 한 후 toohello Azure 클래식 포털에에서 로그인 하 고 Azure 서비스에 액세스할 수 있습니다. Hello Active Directory 확장 클릭 toomanage hello Office 365 사용자를 인증 하는 동일한 디렉터리입니다.

Azure 구독이 있으면 이미 hello 프로세스 toomanage 추가 디렉터리는 프로세스도 간단 합니다. 예를 들어 Michael Smith는 Contoso.com에 대한 Office 365 구독을 보유하고 있습니다. 그에게는 본인의 Microsoft 계정인 msmith@hotmail.com을 사용하여 등록한 Azure 구독도 있습니다. 이 경우 두 개의 디렉터리를 관리하게 됩니다.

| 구독 | Office 365 | Azure |
| --- | --- | --- |
|   표시 이름 |Contoso |기본 Azure AD(Azure Active Directory) 디렉터리 |
|   도메인 이름 |contoso.com |msmithhotmail.onmicrosoft.com |

Multi-factor authentication과 같은 Azure AD 기능을 사용할 수 있도록 tooAzure 자신의 Microsoft 계정을 사용 하 여에 로그인 하는 동안 toomanage hello Contoso 디렉터리의 사용자 id를 hello 하고자 했습니다. 다음 다이어그램 hello tooillustrate hello 프로세스를 도움이 될 수 있습니다.

![두 개의 독립적인 디렉터리 toomanage 다이어그램](./media/active-directory-manage-o365-subscription/AAD_O365_03.png)

이 경우 hello 두 디렉터리는 서로 독립적입니다.

## <a name="toomanage-two-independent-directories"></a>두 toomanage 독립 디렉터리
순서로 Michael Smith toomanage에 대 한 디렉터리를 모두로 tooAzure에 로그인 하는 동안 msmith@hotmail.com, 그 hello 다음 단계를 완료 해야 합니다.

> [!NOTE]
> 이러한 단계는 사용자가 Microsoft 계정으로 로그인한 경우에만 완료할 수 있습니다. Hello 사용자가 회사 또는 학교 계정으로 로그인 하는 경우 hello 옵션 너무**기존 디렉터리를 사용 하 여** 사용할 수 없습니다. 홈 디렉터리 (즉, hello 디렉터리 위치 hello 회사 또는 학교 계정의 저장 하 고 해당 hello 업무 또는 학교 소유)에 의해서만 회사 또는 학교 계정을 인증할 수 있습니다.
>
>

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com) 으로 msmith@hotmail.com합니다.
2. **새로 만들기** > **App services** > **Active Directory** > **디렉터리** > **사용자 지정 만들기**를 클릭합니다.
3. 기존 디렉터리 및 선택 hello 사용 하 여 클릭 **지금 로그 아웃 준비 toobe 저는** 확인란을 선택 합니다.
4. Contoso.onmicrosoft.com의 전역 관리자로 Azure 클래식 포털을 toohello에 로그인 (예를 들어 msmith@contoso.com).
5. 너무 대화 상자가 나타나면**Azure와 함께 사용 하 여 hello Contoso 디렉터리?**, 클릭 **계속**합니다.
6. **지금 로그아웃**을 클릭합니다.
7. 로그인으로 Azure 클래식 포털을 toohello msmith@hotmail.com. hello Contoso 디렉터리와 hello 기본 디렉터리 hello Active Directory 확장에에서 표시 합니다.

다음이 단계를 완료 한 후 msmith@hotmail.com hello Contoso 디렉터리의 전역 관리자가 있습니다.

## <a name="tooadminister-resources-as-hello-global-admin"></a>전역 관리자 hello와 tooadminister 리소스
이제 Jane Doe 필요 웹 사이트를 관리 하며 데이터베이스 리소스와 연결 된 Azure 구독에 대 한 hello 한다고 가정해 보겠습니다 msmith@hotmail.com합니다. 이렇게 하려면 그녀 전에 Michael Smith 필요 toocomplete 이러한 단계를 더 합니다.

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com) hello Azure 구독에 대 한 hello 서비스 관리자 계정을 사용 하 여 (이 예제에서는 msmith@hotmail.com).
2. Hello 구독 toohello Contoso 디렉터리 전송: 클릭 **설정** > **구독** > hello 구독 선택 > **디렉터리 편집** > 선택 **Contoso (Contoso.com)**합니다. Hello 전송, 회사 또는 학교의 일환으로 hello 구독의 공동 관리자 인 계정은 제거 됩니다.
3. Jane Doe hello 구독의 공동 관리자로 추가: 클릭 **설정** > **관리자** > hello 구독 선택 > **추가** > 형식 **JohnDoe@Contoso.com**.

## <a name="next-steps"></a>다음 단계
구독과 디렉터리 간의 hello 관계에 대 한 자세한 내용은 참조 [구독이 디렉터리와 연결 된 방법을](active-directory-how-subscriptions-associated-directory.md)합니다.
