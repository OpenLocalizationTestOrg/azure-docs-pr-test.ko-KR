---
title: "Azure에서 Office 365 구독의 디렉터리 관리 | Microsoft Docs"
description: "Azure Active Directory 및 Azure 클래식 포털을 사용하여 Office 365 구독 디렉터리 관리"
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
ms.openlocfilehash: b520a5e96417fb766a757fabc384a1fc4eb0f14e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-the-directory-for-your-office-365-subscription-in-azure"></a>Azure에서 Office 365 구독의 디렉터리 관리
이 문서에서는 Azure 클래식 포털을 사용하여 Office 365 구독에 대해 만들어진 디렉터리를 관리하는 방법을 설명합니다. Azure 클래식 포털에 로그인하려면 Azure 구독의 서비스 관리자 또는 공동 관리자여야 합니다. Azure 구독이 없는 경우 지금 [무료 30일 평가판](https://azure.microsoft.com/trial/get-started-active-directory/) 에 등록하면 이 링크를 사용하여 5분 내에 첫 번째 클라우드 솔루션을 배포할 수 있습니다. Office 365에 로그인하는 데 사용하는 회사 또는 학교 계정을 사용해야 합니다.

> [!IMPORTANT]
> 이 문서에서 참조되는 Azure 클래식 포털을 사용하는 대신 Azure Portal에서 [Azure AD 관리 센터](https://aad.portal.azure.com)를 사용하여 Azure AD를 관리하는 것이 좋습니다.

Azure 구독을 완료한 후 Azure 클래식 포털에 로그인하고 Azure 서비스에 액세스할 수 있습니다. Active Directory 확장을 클릭하여 Office 365 사용자를 인증하는 동일한 디렉터리를 관리합니다.

Azure 구독이 이미 있는 경우 추가 디렉터리를 관리하는 프로세스도 간단히 수행할 수 있습니다. 예를 들어 Michael Smith는 Contoso.com에 대한 Office 365 구독을 보유하고 있습니다. 그에게는 본인의 Microsoft 계정인 msmith@hotmail.com을 사용하여 등록한 Azure 구독도 있습니다. 이 경우 두 개의 디렉터리를 관리하게 됩니다.

| 구독 | Office 365 | Azure |
| --- | --- | --- |
|   표시 이름 |Contoso |기본 Azure AD(Azure Active Directory) 디렉터리 |
|   도메인 이름 |contoso.com |msmithhotmail.onmicrosoft.com |

그는 다단계 인증 등의 Azure AD 기능을 설정할 수 있도록 Microsoft 계정을 사용하여 Azure에 로그인한 동안 Contoso 디렉터리의 사용자 ID를 관리하려고 합니다. 다음 다이어그램은 프로세스를 설명하는 데 도움이 될 수 있습니다.

![독립적인 두 디렉터리를 관리하는 다이어그램](./media/active-directory-manage-o365-subscription/AAD_O365_03.png)

이 경우 두 디렉터리는 서로 독립적입니다.

## <a name="to-manage-two-independent-directories"></a>독립적인 두 디렉터리를 관리하려면
Michael Smith는 Azure에 msmith@hotmail.com으로 로그인한 동안 두 디렉터리를 관리하기 위해 다음 단계를 완료해야 합니다.

> [!NOTE]
> 이러한 단계는 사용자가 Microsoft 계정으로 로그인한 경우에만 완료할 수 있습니다. 사용자가 회사 또는 학교 계정을 사용하여 로그인하는 경우 **기존 디렉터리 사용** 을 사용할 수 없습니다. 회사 또는 학교 계정은 홈 디렉터리(즉, 회사 또는 학교 계정이 저장되고 회사 또는 학교에서 소유한 디렉터리)에 의해서만 인증될 수 있습니다.
>
>

1. [Azure 클래식 포털](https://manage.windowsazure.com)에 msmith@hotmail.com으로 로그인합니다.
2. **새로 만들기** > **App services** > **Active Directory** > **디렉터리** > **사용자 지정 만들기**를 클릭합니다.
3. 기존 디렉터리 사용을 클릭하고 **지금 로그아웃** 확인란을 선택합니다.
4. Contoso.onmicrosoft.com의 전역 관리자로 Azure 클래식 포털에 로그인합니다(예: msmith@contoso.com).
5. **Azure로 Contoso 디렉터리를 사용할까요?**라는 메시지가 나타나면 **계속**을 클릭합니다.
6. **지금 로그아웃**을 클릭합니다.
7. msmith@hotmail.com에서와 같이 Azure 클래식 포털에 로그인합니다. Contoso 디렉터리와 기본 디렉터리가 Active Directory 확장에 표시됩니다.

다음 단계가 완료되면 msmith@hotmail.com은 Contoso 디렉터리의 전역 관리자가 됩니다.

## <a name="to-administer-resources-as-the-global-admin"></a>전역 관리자로 리소스를 관리하려면
이제 Jane Doe가 msmith@hotmail.com의 Azure 구독과 연결된 웹 사이트 및 데이터베이스 리소스를 관리해야 한다고 가정해 봅니다. 이렇게 하려면 Michael Smith는 다음 추가 단계를 완료해야 합니다.

1. Azure 구독의 서비스 관리자 계정(이 예의 경우 msmith@hotmail.com)을 사용하여 [Azure 클래식 포털](https://manage.windowsazure.com)에 로그인합니다.
2. Contoso 디렉터리로 구독을 전송합니다. 이를 위해 **설정** > **구독**을 클릭하고 구독 > **디렉터리 편집** > **Contoso(Contoso.com)**를 선택합니다. 전송 과정이 진행되면서 구독의 공동 관리자인 모든 회사 또는 학교 계정이 제거됩니다.
3. Jane Doe를 구독의 공동 관리자로 추가합니다. 이를 위해 **설정** > **관리자**를 클릭하고 구독 > **추가**를 선택한 다음 **JohnDoe@Contoso.com**을 입력합니다.

## <a name="next-steps"></a>다음 단계
구독과 디렉터리 간의 관계에 대한 자세한 내용은 [구독과 디렉터리의 연관 관계](active-directory-how-subscriptions-associated-directory.md)를 참조하세요.
