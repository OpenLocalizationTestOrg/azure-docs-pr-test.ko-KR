---
title: Azure AD Privileged Identity Management aaaConfigure | Microsoft Docs
description: "Azure AD Privileged Identity Management 란 설명 하는 항목 및 방법 toouse PIM tooimprove 클라우드 보안 합니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: c548ed2e-06e3-4eaf-a63d-0f02ee72da25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: dbe49fe4a0f6e5b46ed5a17fc7e8dcdacafe3846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-privileged-identity-management"></a>Azure AD Privileged Identity Management란?
Azure Active Directory(AD) Privileged Identity Management를 사용하여 조직 내에서 액세스를 관리, 제어 및 모니터링할 수 있습니다. Azure AD에서 액세스 tooresources 및 Microsoft Intune 또는 Office 365와 같은 다른 Microsoft 온라인 서비스에이 포함 됩니다.  

> [!NOTE]
> Privileged Identity Management 사용할 수 있는 tooyour 전체 조직 때 Azure Active Directory Premium P2 hello 버전 관리자를 사용 합니다. 자세한 내용은 [Azure Active Directory 버전](active-directory-editions.md)을 참조하세요.

Hello 악의적인 사용자가 해당 액세스 가능성을 줄여 주는 때문에 조직은 toominimize hello 수가 toosecure 정보에 액세스 또는 리소스를 가진 사용자가을 원합니다. 그러나 사용자는 Azure, Office 365 또는 SaaS 응용 프로그램에서 권한 있는 작업 toocarry 여전히 필요합니다. 조직은 사용자에게 Azure AD에서 권한 있는 액세스를 제공하며 사용자가 자신의 관리자 권한을 가지고 무엇을 하는지 모니터링하지 않습니다. Azure AD Privileged Identity Management tooresolve이이 위험을 수 있습니다.  

Azure AD Privileged Identity Management를 통해 다음을 할 수 있습니다.  

* Azure AD 관리자인 사용자를 확인할 수 있습니다.
* 요청 시 "just in time" Office 365 및 Intune 관리 액세스 tooMicrosoft 온라인 서비스와 같은 사용 하도록 설정
* 관리자 액세스 기록 및 관리자 할당 변경에 대한 보고서 가져오기
* 액세스 tooa 권한 있는 역할에 대 한 경고를 받으려면
* 필요한 승인 tooactivate (미리 보기)

Azure AD Privileged Identity Management (에 국한 되지 않습니다) 비롯 한 hello 기본 제공 Azure AD 조직 역할을 관리할 수 있습니다.  

* 전역 관리자
* 대금 청구 관리자
* 서비스 관리자  
* 사용자 관리자
* 암호 관리자

## <a name="just-in-time-administrator-access"></a>시간에 맞추는 관리자 액세스
지금까지 hello Azure 클래식 포털을 통해 사용자 tooan 관리자 역할 또는 Windows PowerShell을 할당할 수 있습니다. 결과적으로, 해당 사용자가을 **영구 관리자**hello 할당 된 역할에 항상 활성, 합니다. hello 개념을 소개 하는 azure AD Privileged Identity Management는 **적격 admin**합니다. 적격인 관리자는 매일은 아니지만 때때로 권한 있는 액세스가 필요한 사용자여야 합니다. hello 사용자 액세스를 해야 하는 서로 정품 인증 프로세스를 완료 하 고 미리 결정 된 시간 동안 활성 관리 될 때까지 hello 역할이 활성화 되었습니다.

## <a name="enable-privileged-identity-management-for-your-directory"></a>디렉터리에서 Privileged Identity Management 사용
Azure AD Privileged Identity Management를 사용 하 여 hello에서 시작할 수 있습니다 [Azure 포털](https://portal.azure.com/)합니다.

> [!NOTE]
> 조직 계정으로 전역 관리자 여야 합니다 (예를 들어 @yourdomain.com), Microsoft 계정이 아닌 (예를 들어 @outlook.com), 디렉터리에 대 한 Azure AD Privileged Identity Management tooenable 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/) 디렉터리의 전역 관리자입니다.
2. 조직에서 둘 이상의 디렉터리를 경우 hello hello Azure 포털의 상단 오른쪽 모서리에서 사용자 이름을 선택 합니다. Azure AD Privileged Identity Management ´ hello 디렉터리를 선택 합니다.
3. 선택 **더 많은 서비스** 에 대 한 필터 텍스트 상자에 붙여넣습니다 toosearch hello를 사용 하 여 **Azure AD Privileged Identity Management**합니다.
4. 확인 **Pin toodashboard** 클릭 하 고 **만들기**합니다. hello Privileged Identity Management 응용 프로그램을 엽니다.

디렉터리의 첫 번째 사람 toouse Azure AD Privileged Identity Management를 hello 하는, 하는 경우 다음 hello [보안 마법사](active-directory-privileged-identity-management-security-wizard.md) hello 초기 할당 경험을 안내 합니다. 그 후 자동으로 되 hello 먼저 **보안 관리자** 및 **권한 있는 역할 관리자** hello 디렉터리의 합니다.

권한 있는 역할 관리자만 다른 관리자의 액세스 권한을 관리할 수 있습니다. 있습니다 수 [PIM의 다른 사용자가 hello 기능 toomanage 제공](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)합니다.

## <a name="privileged-identity-management-admin-dashboard"></a>Privileged Identity Management 관리 대시보드
Azure AD 권한 있는 ID 관리자는 다음과 같은 중요한 정보를 전달하는 관리 대시보드를 제공합니다.

* 기회 tooimprove 보안 주는 경고
* hello tooeach 권한 있는 역할에 할당 된 사용자 수  
* 적격 및 영구 관리자의 hello 수
* 디렉터리의 권한 있는 역할 활성화 그래프

![PIM 대시보드 - 스크린샷][2]

## <a name="privileged-role-management"></a>권한 있는 역할 관리
Azure AD Privileged Identity management hello 관리자를 추가 하거나 영구 또는 적격 관리자 tooeach 역할을 제거 하 여 관리할 수 있습니다.

![PIM 추가/제거 관리자 - 스크린샷][3]

## <a name="configure-hello-role-activation-settings"></a>Hello 역할 활성화 설정을 구성 합니다.
Hello를 사용 하 여 [역할 설정](active-directory-privileged-identity-management-how-to-change-default-settings.md) hello 적격 역할 활성화 속성을 포함 하 여 구성할 수 있습니다.

* hello 기간의 hello 역할 정품 인증 기간
* hello 역할 활성화 알림
* hello 정보 사용자 tooprovide hello 역할 정품 인증 과정 중에 필요
* 서비스 티켓 또는 인시던트 번호
* [승인 워크플로 요구 사항 - 미리 보기](./privileged-identity-management/azure-ad-pim-approval-workflow.md)

![PIM 설정 - 관리자 활성화 - 스크린샷][4]

단추의 hello 이미지에 hello 컨트롤에 대 한 **Multi-factor Authentication** 을 사용할 수 없습니다. 높은 권한이 필요한 특정 역할에 대해 우리는 강화된 보호를 위해 MFA가 필요합니다.

## <a name="role-activation"></a>역할 활성화
너무[역할 활성화](active-directory-privileged-identity-management-how-to-activate-role.md), 적격 관리자 hello 역할에 대 한 시간으로 제한 "활성화"를 요청 합니다. hello를 사용 하 여 hello 정품 인증을 요청할 수 **내 역할 활성화** Azure AD Privileged Identity Management에 대 한 옵션입니다.

알고자 하는 역할 tooactivate 관리자 tooinitialize hello Azure 포털에서에서 Azure AD Privileged Identity Management 필요 합니다.

역할 활성화는 사용자 지정할 수 있습니다. Hello PIM 설정에서 hello 정품 인증 및 정보 hello 관리자에 게 무엇이 필요 tooprovide tooactivate hello 역할의 hello 길이 확인할 수 있습니다.

![PIM 관리자 요청 역할 활성화 - 스크린샷][5]

## <a name="review-role-activity"></a>역할 작업 검토
두 가지 방법으로 tootrack 역할 권한이 부여 된 직원 및 관리자 사용 하는 방법입니다. hello 첫 번째 옵션을 사용 하 여 [디렉터리 역할 감사 기록](active-directory-privileged-identity-management-how-to-use-audit-log.md)합니다. hello 감사 기록은 권한 있는 역할 할당과 역할 활성화 기록의 변경 내용 추적을 기록합니다.

![PIM 활성화 기록 - 스크린샷][6]

hello 두 번째 옵션은 regular tooset [검토 액세스](active-directory-privileged-identity-management-how-to-start-security-review.md)합니다. 이러한 액세스 검토를에서 수행 하 고 (예: 팀 관리자)는 검토자를 지정 된 수 또는 hello 직원 자체를 검토할 수 있습니다. 이 hello 가장 좋은 방법은 toomonitor 여전히 액세스를 필요로 하 고는 더 이상 없습니다.

## <a name="azure-ad-pim-at-subscription-expiration"></a>구독 만료 시 Azure AD PIM
테 넌 트 toopreview Azure AD PIM 이전 tooreaching 일반 가용성 Azure AD PIM 미리 보기에서 되었고 개가 라이선스가 있는지 확인 합니다.  Azure AD PIM 일반 가용성에 도달 했으므로 PIM를 사용 하 여 hello 테 넌 트 toocontinue의 toohello 관리자 평가판 또는 유료 라이선스 할당 되어야 합니다.  조직의 Azure AD Premium P2 구입 하지는 않습니다. 평가판, 모든 hello Azure AD PIM 기능 대부분은 더 이상 사용할 수 테 넌 트에 합니다.  자세한 내용은 hello에 [Azure AD PIM 구독 요구 사항](./privileged-identity-management/subscription-requirements.md)

## <a name="next-steps"></a>다음 단계
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-configure/PIM_Admin_Overview.png
[3]: ./media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: ./media/active-directory-privileged-identity-management-configure/PIM_Settings_w_Approval_Disabled.png
[5]: ./media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: ./media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png
