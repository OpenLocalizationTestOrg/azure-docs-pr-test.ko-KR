---
title: "aaaHow Azure 구독은 Azure Active Directory와 연결 | Microsoft Docs"
description: "TooMicrosoft Azure에에서 로그인 하 고 관련 Azure 구독과 Azure Active Directory 간에 hello 관계와 같은 문제입니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bc4773c2-bc4a-4d21-9264-2267065f0aea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4f831cfb972efec57083fcaa63adb43fde7b2faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-subscriptions-are-associated-with-azure-active-directory"></a>Azure 구독과 Azure Active Directory의 연관 관계
이 문서에서는 Azure 구독과 Azure Active Directory (Azure AD) 간의 hello 관계에 대 한 정보 및 방법 tooadd 기존 구독 tooyour Azure AD 디렉터리입니다.

## <a name="your-azure-subscriptions-relationship-tooazure-ad"></a>Azure 구독 관계 tooAzure AD
Azure 구독에 hello directory tooauthenticate 사용자, 서비스 및 장치를 트러스트 하는 Azure AD와의 신뢰 관계가 있습니다. 여러 구독 hello 신뢰할 수 있는 동일한 디렉터리 하지만 각 구독 하나의 디렉터리만 트러스트 합니다. 

구독 디렉터리 개가 있는 hello 트러스트 관계 (웹 사이트, 데이터베이스 및 등)는 Azure의 다른 리소스와 있는 hello 관계와 달리입니다. 구독이 만료 되는 경우 액세스 toohello hello 구독과 연결 된 다른 리소스를 중지 합니다. 하지만 Azure에서 Azure AD 디렉터리 남아 있으며 해당 디렉터리와는 다른 구독을 연결 하 고 새 구독 hello를 사용 하 여 hello 디렉터리를 관리할 수 있습니다.

![구독과 다이어그램의 연관 관계](./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png)

모든 사용자는 자신을 인증하는 단일 홈 디렉터리를 가지고 있지만 다른 디렉터리의 게스트가 될 수도 있습니다. Azure ad에서는 사용자 계정에는 멤버 또는 게스트 hello 디렉터리를 볼 수 있습니다.

## <a name="azure-ad-and-cloud-service-subscriptions"></a>Azure AD 및 클라우드 서비스 구독
Azure AD hello 핵심 디렉터리 및 id 뒤에 있는 대부분의 Microsoft 클라우드 서비스를 포함 하 여 관리 기능을 제공 합니다.

* Azure
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

이 Microsoft 클라우드 서비스에 등록할 때 hello를 무료 Azure AD 서비스를 가져옵니다. 추가 Azure 구독 tooan Azure AD 디렉터리 tooadd 하려는 경우 Microsoft 계정으로 서명 합니다. 또는 학교 계정을, tooAzure 저작물에 로그인 하는 경우에 회사 또는 학교 계정을 Azure에서 직접 인증할 수 없어서 Azure 구독 tooan 기존 디렉터리를 추가할 수 없습니다. 

## <a name="tooadd-an-existing-subscription-tooyour-azure-ad-directory"></a>tooadd 기존 구독 tooyour Azure AD 디렉터리
hello 구독이 연결 된 두 hello 현재 디렉터리에 있는 계정으로 로그인 해야 하 고 tooadd hello 디렉터리에서 원하는 되 게 합니다. 

1. Toohello 로그인 [Azure 계정 센터](https://account.windowsazure.com/Home/Index) 원하는 tootransfer는 hello hello 구독의 계정 관리자에 소유권 있는 계정으로 합니다.
2. 해당 hello 게 사용자에 게 toobe hello 구독 소유자는 hello 대상 디렉터리를 확인 합니다.
3. **구독 이전**을 클릭합니다.
4. Hello 받는 사람을 지정 합니다. hello 받는 사람 전자 메일을 동의 링크를 자동으로 가져옵니다.
5. hello 받는 사람 hello 링크를 클릭 하 고 지불 정보를 입력 하는 등 hello 지침을 따릅니다. Hello 받는 사람에 성공 하면 hello 구독 전송 됩니다. 
6. hello 구독의 hello 기본 디렉터리 변경 toohello 디렉터리에는 해당 hello 사용자입니다.


## <a name="suggestions-toomanage-both-a-subscription-and-a-directory"></a>구독 및 디렉터리가 제안 toomanage
Azure 구독에 대 한 hello 관리 역할 연결 리소스 toohello Azure 구독을 관리합니다. 이 섹션에서는 Azure 구독 관리자와 Azure AD 디렉터리 관리자 간의 hello 차이점을 설명 합니다. 관리 역할 관리 및 구독에 대해서는 설명 toomanage 사용에 대 한 다른 제안 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles.md)합니다.

기본적으로 등록할 때는 hello 서비스 관리자 역할을 할당 됩니다. 다른 사용자에 toosign 고 hello를 사용 하 여 서비스에 액세스할 경우 동일한 구독을 추가할 수 있습니다 공동 관리자로 합니다. 

Azure AD에는 다른 일련의 관리 역할 toomanage hello 디렉터리 및 id 관련 기능입니다. 예를 들어 디렉터리의 전역 관리자에 게 사용자 및 그룹 toohello 디렉터리를 추가 하거나 사용자에 대 한 다단계 인증을 요구할 수 있습니다. 디렉터리를 만드는 사용자가 toohello 전역 관리자 역할이 할당 및 관리 역할 tooother 사용자를 할당할 수 있습니다. 또한 Azure AD 관리 역할은 Office 365 및 Microsoft Intune과 같은 다른 서비스에서도 사용됩니다. 

Azure 구독 관리자와 Azure AD 디렉터리 관리자는 서로 다른 역할입니다. 
* Azure 구독 관리자는 Azure의에서 리소스를 관리 하 고 (Azure 포털 자체 hello Azure 리소스 이므로) hello Azure 포털에서에서 Azure AD를 사용할 수 있습니다. 
* 디렉터리 관리자만 hello Azure AD 디렉터리에서에서 속성을 관리할 수 있습니다.

역할을 모두 담당할 수 있지만 그럴 필요는 없습니다. 디렉터리 전역 관리자는 Azure 구독의 서비스 관리자 또는 공동 관리자로 할당될 수 없고 반대도 그렇습니다. Hello 구독 관리자가 아니어도 hello 사용자 toohello Azure 포털에에서 서명할 수 있지만 hello 포털에서 해당 구독에 대 한 hello 디렉터리를 관리할 수 없습니다. 그러나이 사용자는 Azure AD PowerShell 또는 Office 365 관리 센터 hello와 같은 다른 도구를 사용 하 여 디렉터리를 관리할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* toochange 관리자는 Azure 구독에 대 한 참조 하는 방법에 대해 더 알아봅니다을 toolearn [의 Azure 구독 tooanother 계정 소유권 이전](../billing/billing-subscription-transfer.md)
* Microsoft Azure에서 리소스 액세스 제어 하는 방법에 대 한 자세한 toolearn 참조 [Azure에서 리소스 액세스 이해](active-directory-understanding-resource-access.md)
* 방법에 대 한 자세한 내용은 Azure AD에서 tooassign 역할 참조 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles-azure-portal.md)

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG
