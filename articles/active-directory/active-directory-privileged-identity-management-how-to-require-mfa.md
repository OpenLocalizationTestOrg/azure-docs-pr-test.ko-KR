---
title: aaaHow toorequire multi-factor authentication | Microsoft Docs
description: "방법에 대해 toorequire multi-factor authentication (MFA) privileged hello Azure Active Directory Privileged Identity Management 확장 id에 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1e3dc4ad-3a6a-4a52-8417-3ca4f84ae05c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: c08fad9dc80c09a14a4bd7497da4942fa227c3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-mfa-in-azure-ad-privileged-identity-management"></a>어떻게 MFA에 Azure AD Privileged Identity Management toorequire
모든 관리자에 대해 Multi-Factor Authentication(MFA)을 요구하는 것이 좋습니다. 이렇게 하면 손상 tooa 암호 인해 공격의 hello 위험이 줄어듭니다.

사용자가 로그인할 때 MFA 챌린지를 완료하도록 요구할 수 있습니다. 블로그 게시물 hello [Office 365 및 azure MFA에 대 한 MFA](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/) hello Microsoft Azure Multi-factor Authentication 서비스에 포함 된 hello 기능을 통해 Office 및 Azure 구독에 포함 된 항목을 비교 합니다.

사용자가 Azure AD PIM의 역할을 활성화하는 경우 MFA 챌린지를 완료하도록 요구할 수도 있습니다. 이러한 방식으로 hello 사용자에 로그인 하는 경우 MFA 챌린지를 완료 하지 않은, 수 있으며이 경우 증명된 toodo PIM으로 너무 합니다.

## <a name="requiring-mfa-in-azure-ad-privileged-identity-management"></a>Azure AD Privileged Identity Management에서 MFA 요구
권한 있는 역할 관리자가 PIM의 ID를 관리하는 경우 권한 있는 계정에 대해 MFA를 권장하는 경고가 표시될 수 있습니다. Hello 보안 MFA를 요구 해야 하는 hello 관리자 계정 목록이 알리미 hello PIM 대시보드와 새 블레이드가 열립니다.  여러 역할을 선택 하 고 hello를 클릭 하 여 MFA를 요구할 수 있습니다 **해결** 단추 또는 있습니다 수 hello 줄임표 다음 tooindividual 역할을 클릭 하 고 클릭 hello **해결** 단추입니다.

> [!IMPORTANT]
> 이제 오른쪽 Azure MFA 작업 에서만 작동 또는 학교 계정, Microsoft 계정 (일반적으로 개인 계정 toosign Skype, Xbox, Outlook.com 등과 같은 tooMicrosoft 서비스에서 사용 합니다.) 되지 않습니다. 이 때문에 Microsoft 계정을 사용 하 여 모든 사용자가 적격 관리자 MFA tooactivate의 역할을 사용할 수 없으므로 일 수 없습니다. 이러한 사용자가 필요한 toocontinue Microsoft 계정을 사용 하는 작업을 관리 하는 경우 해당 toopermanent 관리자에 사용할 상승 지금은 합니다.
> 
> 

또한 특정 역할에 대 한 MFA 요구 사항을 hello hello hello PIM 대시보드의 역할 섹션에서에서 클릭 하 여 변경할 수 있습니다. 클릭 합니다 **설정** 에서 다음을 선택 하 고 hello 역할 블레이드 **사용** 다단계 인증에서 합니다.

## <a name="how-azure-ad-pim-validates-mfa"></a>Azure AD PIM에서 MFA의 유효성을 검사하는 방법
사용자가 역할을 활성화할 때 MFA 유효성을 검사하는 두 가지 방법이 있습니다.

hello 가장 간단한 방법은 사용자에 게 권한 있는 역할을 활성화 하는 Azure MFA에 toorely입니다. toodo 해당 사용자, 필요한 경우에 사용이 허가 된 있고 Azure MFA에 대해 등록 하는이 첫 번째 확인 합니다. 어떻게 toodo 이것이에 대 한 자세한 내용은 [hello 클라우드에서 Azure Multi-factor Authentication 시작](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)합니다. 권장 되지만 않아도에 로그인 할 때 이러한 사용자에 대 한 Azure AD tooenforce MFA를 구성 합니다. 자체 Azure AD PIM으로 hello MFA 검사를 수행할 수는 때문입니다.

또는 사용자가 온-프레미스를 인증하는 경우 MFA에 대해 책임지는 ID 공급자를 사용할 수 있습니다. 예를 들어, Azure AD에 액세스 하기 전에 AD 페더레이션 서비스 toorequire 스마트 카드 기반 인증이 구성 되어 있는 경우 [Azure Multi-factor Authentication 및 AD FS를 사용 하 여 클라우드 리소스 보안](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md) 지침이 포함 됩니다. AD FS toosend 클레임 tooAzure AD 구성할 수 있습니다. 사용자가 tooactivate 역할을 Azure AD PIM는 MFA의 유효성을 이미 hello 사용자에 대 한 hello 적절 한 클레임을 받으면 수락 합니다.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>다음 단계
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

