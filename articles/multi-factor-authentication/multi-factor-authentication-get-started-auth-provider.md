---
title: "aaaGet Azure Multi-factor Auth 공급자를 시작 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Azure 다단계 인증 공급자입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: a7dd5030-7d40-4654-8fbd-88e53ddc1ef5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 00ea967a80b43baff38c1de586c54d95c9abac2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-an-azure-multi-factor-auth-provider"></a>Azure Multi-Factor Auth 공급자 시작
두 단계 인증은 기본적으로 Azure Active Directory 및 Office 365 사용자가 있는 전역 관리자를 위해 사용할 수 있습니다. 그러나 tootake 활용 하려는 경우 [고급 기능](multi-factor-authentication-whats-next.md) hello 정식 버전의 Azure Multi-factor Authentication (MFA)을 구입 해야 합니다.

Azure Multi-factor Auth 공급자가 사용 됩니다 tootake hello Azure MFA의 전체 버전에서 제공 하는 기능을 사용 합니다. **Azure MFA, Azure AD Premium 또는 EMS(Enterprise Mobility + Security)를 통해 라이선스를 갖고 있지 않은** 사용자를 위한 기능입니다.  Azure MFA, Azure AD Premium 및 EMS hello 정식 버전의 Azure MFA 기본적으로 포함 됩니다. 라이선스를 보유한 경우 Multi-Factor Auth 공급자가 필요하지 않습니다.

Azure Multi-factor Auth 공급자는 필요한 toodownload hello SDK입니다.

> [!IMPORTANT]
> toodownload SDK hello Azure MFA, AAD Premium 또는 EMS 라이선스를 보유 하는 경우에 Azure Multi-factor Auth 공급자 toocreate 사용 해야 합니다.  이 목적을 위해 Azure Multi-factor Auth 공급자를 만들고 이미 라이선스가, 수 hello로 있는지 toocreate hello 공급자 **활성화 된 사용자별** 모델입니다. 그런 다음 연결할 hello Azure MFA, Azure AD Premium 또는 EMS 라이선스를 포함 하는 hello 공급자 toohello 디렉터리입니다. 이 구성을 통해만 고유 사용자 수가 hello 소유한 라이선스 개수 보다 2 단계 인증을 수행 하는 경우 청구 됩니다.

## <a name="what-is-an-azure-multi-factor-auth-provider"></a>Azure Multi-Factor Auth 공급자란?

Azure Multi-factor Authentication에 대 한 라이선스 없다면 사용자에 게는 인증 공급자 toorequire 2 단계 인증을 만들 수 있습니다. 사용자 지정 앱을 개발 하는 Azure MFA tooenable를 원하는 경우 인증 공급자 만들기 및 [hello SDK 다운로드](multi-factor-authentication-sdk.md)합니다.

두 가지 유형의 인증 공급자 있으며 Azure 구독 요금이 부과 됩니다 어떻게 주위 hello 차이. hello 인증 단위 옵션 hello 한 달에 테 넌 트에 대해 수행 하는 인증 수를 계산 합니다. 이 옵션은 사용자 지정 응용 프로그램에 대해 MFA를 요구하는 경우처럼 가끔씩만 인증하는 여러 사용자가 있는 경우 가장 적합합니다. hello 사용자별 옵션 한 달에 2 단계 인증을 수행 하는 테 넌 트에 대 한 개인 hello 수를 계산 합니다. 일부 사용자 라이선스를 갖고 있는 하지만 프로그램 라이선스 한도 넘어 tooextend MFA toomore 사용자가 할 경우이 옵션이 가장 좋습니다.

## <a name="create-a-multi-factor-auth-provider"></a>Multi-Factor Auth 공급자 만들기
다음 단계는 Azure Multi-factor Auth 공급자 toocreate hello를 사용 합니다. Azure Multi-factor Auth 공급자 hello Azure 클래식 포털에에서만 만들 수 있습니다. Azure AD 테 넌 트 인지 toomake 확인 toohello Azure 클래식 포털에에서 로그인 할 수 없습니다, [Azure 구독과 연결 된](../active-directory/active-directory-how-subscriptions-associated-directory.md)합니다. 

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com) 관리자 권한으로 합니다.
2. Hello 왼쪽에서 선택 **Active Directory**합니다.
3. Hello 위쪽에, hello Active Directory 페이지에서 선택 **Multi-factor Authentication 공급자**합니다.
   
   ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider1.png)

4. Hello 맨 아래에 클릭 **새로**합니다.
   
   ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider2.png)

5. App Services 아래에서 **Multi-Factor Auth 공급자**를 선택합니다.
   
   ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider3.png)

6. **빠른 생성**을 선택합니다.
   
   ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider4.png)

7. Hello 다음 필드를 입력 하 고 선택 **만들기**합니다.
   1. **이름** – hello hello Multi-factor Auth 공급자의 이름입니다.
   2. **사용 모델** – 두 가지 옵션 중 하나를 선택합니다.
      * 인증당 - 인증 단위로 요금이 청구되는 구매 모델입니다. 일반적으로 소비자 지향 응용 프로그램에서 Azure Multi-Factor Authentication을 사용하는 시나리오에 사용됩니다.
      * 활성화된 사용자별 – 활성화된 사용자 단위로 요금이 청구되는 구매 모델입니다. Office 365와 같은 액세스 tooapplications 직원에 대 한 일반적으로 사용 합니다. 이미 Azure MFA에 대한 사용이 허가된 사용자가 있는 경우 이 옵션을 선택합니다.
   3. **디렉터리** – hello Azure Active Directory에 Multi-factor Authentication 공급자가 연결 된 해당 hello 테 넌 트입니다. Hello 다음에 유의 해야 합니다.
      * Azure AD 디렉터리 toocreate Multi-factor Auth 공급자를 사용할 필요가 없습니다. 이 상자 toodownload hello Azure Multi-factor Authentication 서버 또는 SDK만 계획이 있는 경우 비워 둡니다.
      * hello Multi-factor Auth 공급자는 Azure AD 디렉터리 tootake 활용 고급 기능 hello와 연결 되어야 합니다.
      * 한 Multi-Factor Auth 공급자를 한 Azure AD 디렉터리에만 연결할 수 있습니다.  
      ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider5.png)

8. 클릭 하면 만들기, Multi-factor Authentication 공급자가 생성 하는 hello 및 수 없다는 메시지가 표시 됩니다: **다단계 인증 공급자를 만들었습니다**합니다. **Ok**를 클릭합니다.  
   
   ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider6.png)  

## <a name="manage-your-multi-factor-auth-provider"></a>Multi-Factor Auth 공급자 관리

Hello 사용법을 변경할 수 없습니다 (활성화 된 사용자별 또는 인증 단위)는 MFA 공급자를 만든 후 모델입니다. 그러나 hello MFA 공급자를 삭제 하 고에 다른 사용 모델 하나를 만들 수 있습니다.

Hello 현재 Multi-factor Auth 공급자와 연결 된 경우 Azure AD 디렉터리 (Azure AD 테 넌 라고도 함)와 안전 하 게 hello MFA 공급자를 삭제 고 만들 수 있습니다 연결된 toohello 동일한 Azure AD 테 넌 트 되는 것입니다. 또는 모든 사용자가 MFA에 대해 사용할 수 있는 충분 한 MFA, Azure AD Premium 또는 Enterprise Mobility + 보안 (EMS) 라이선스 toocover를 구입, hello MFA 공급자를 완전히 삭제할 수 있습니다.

MFA 공급자, 연결 된 tooan Azure AD 테 넌 트 아니거나 hello 새 MFA 공급자 tooa 다른 Azure AD 테 넌 트를 연결 하면 사용자 설정 및 구성 옵션 전송 되지 않습니다. 또한 Azure MFA 서버를 기존 필요를 통해 생성 되는 정품 인증 자격 증명을 사용 하 여 다시 활성화 toobe hello 새 MFA 공급자입니다. MFA 서버 toolink hello를 다시 활성화 하 toohello 새 MFA 공급자에 영향을 주지 전화 통화 및 문자 메시지 인증 하지만 모바일 앱 알림을 hello 모바일 앱을 다시 활성화 될 때까지 모든 사용자에 대해 작동이 중지 됩니다.

## <a name="next-steps"></a>다음 단계

[Hello Multi-factor Authentication SDK 다운로드](multi-factor-authentication-sdk.md)

[Multi-Factor Authentication 설정 구성](multi-factor-authentication-whats-next.md)
