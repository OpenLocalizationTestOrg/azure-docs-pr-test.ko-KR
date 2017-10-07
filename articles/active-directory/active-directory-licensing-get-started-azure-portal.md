---
title: "Azure Active Directory에서 라이선스를 사용한 aaaGet 시작 | Microsoft Docs"
description: "Azure Active Directory 라이선스 작동 방식 tooget를 어떻게 시작 모범 사례"
services: active-directory
keywords: "Azure AD 라이선스"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 268dab806b8b959790341d630a0355c6a43871d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="license-yourself-and-your-users-in-azure-active-directory"></a>Azure Active Directory에서 사용자 본인 및 사용자의 사용자 라이선스

> [!div class="op_single_selector"]
> * [Azure Portal 지침](active-directory-licensing-get-started-azure-portal.md)
> * [Azure 클래식 포털 정보](active-directory-licensing-what-is.md)
>
>

Azure AD(Azure Active Directory)는 Microsoft의 IDaaS(Identity as a Service) 솔루션 및 플랫폼입니다. Azure AD는 다양한 서비스 버전으로 제공됩니다.

* Azure Active Directory Free - Office 365, Dynamics, Microsoft Intune 또는 Azure와 같은 Microsoft 서비스에서 사용할 수 있습니다. Azure AD는 이 모드에서 사용량 요금을 생성하지 않습니다.

* Azure AD 유료 버전은 다음과 같습니다.
  - Enterprise Mobility + Security 
  - Azure AD Premium(P1 및 P2)
  - Azure AD Basic
  - Azure Multi-Factor Authentication

많은 Microsoft 온라인 서비스와 마찬가지로 대부분의 Azure AD 유료 버전은 Office 365, Microsoft Intune 및 Azure AD에서 사용자별 권한 부여를 통해 제공됩니다. 이러한 경우 하나 이상의 구독 hello 서비스 구매 표시 되 고 각 구독 테 넌 트의 몇 가지 prepurchased 라이선스를 포함 합니다. 사용자 단위 자격은 다음을 통해 취득합니다.

* 라이선스 할당. 
* Hello 사용자와 hello 제품 간의 링크를 만듭니다.
* Hello 사용자에 대 한 hello 서비스 구성 요소를 사용 하도록 설정 합니다.
* 라이선스 선불 hello 중 하나를 사용 합니다.

[이제 Azure AD premium을 시도합니다.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

Azure AD 서비스 기능에 대한 광범위한 개요는 [Azure AD란?](active-directory-whatis.md)을 참조하세요. 자세한 내용은 [Azure Active Directory에 대한 SLA](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/) 페이지를 참조하세요.

> [!NOTE]
> Azure 리소스를 만들 수 있도록 하 고 tooyour 지불 메서드 매핑할 azure 종 량 제 구독 합니다. Hello 구독과 관련 된 없는 라이선스 수 있습니다. Azure 리소스에 사용자 권한 toooperate 매핑된 toohello 구독에 부여 된 hello 구독에 연결 되며 구독 리소스를 관리할 수 있습니다.

## <a name="how-does-azure-active-directory-licensing-work"></a>Azure Active Directory 라이선스는 어떻게 작동하나요?

라이선스 기반 Azure AD 서비스는 Azure AD 서비스 테넌트에서 구독을 활성화하면 작동됩니다. Hello 구독이 활성 상태 이면 hello 서비스 기능이 Azure AD 관리자가 관리 되 고 사용이 허가 된 사용자가 사용 합니다.

### <a name="manage-subscription-information"></a>구독 정보 관리

Enterprise Mobility + 보안, Azure AD Premium 또는 Azure AD Basic에서는 테 넌 트을 구입할 때 선불 라이선스로 hello 구독에서 유효 기간을 포함 하 여 업데이트 됩니다. Hello 할당 또는 사용 가능한 라이선스 수를 포함 하 여 구독 정보는 hello Azure 포털을 통해 사용할 수 있는: 아래 **Azure Active Directory**개방형 hello **라이선스** hello에 대 한 바둑판식으로 배열 특정 디렉터리입니다. hello **라이선스** 블레이드 최상의 위치 toomanage 라이선스 할당 hello도 됩니다.

각 구독은 Azure AD, Multi-Factor Authentication, Intune, Exchange Online 또는 SharePoint Online과 같은 하나 이상의 서비스 계획으로 구성됩니다.  Azure AD 라이선스 관리에는 서비스 계획 수준 관리가 필요하지 *않습니다*. Office 365는이 고급 구성 모드 toomanage 액세스 tooincluded 서비스에 사용 하기 때문에 다릅니다. Azure AD는 in service 구성 tooenable 기능을 사용 하 고 개별 사용 권한을 관리 합니다.

> [!IMPORTANT]
> Azure AD Premium, Azure AD Basic 및 Enterprise Mobility + 보안 서비스는 사용자를 프로 비전 예외일된 tootheir 디렉터리/테 넌 트. 디렉터리나 다른 디렉터리에서 사용 되는 tooentitle 사용자 사이의 구독을 분할할 수 없습니다. 구독을 디렉터리 간에 이동하는 것은 가능하지만 지원 티켓을 제출하거나, 직접 구매의 경우 취소 후 다시 구매해야 합니다.
>
> 때 Azure AD 또는 볼륨 라이선스 구독을 통해 구매한 Enterprise Mobility + 보안 및 활성화가 자동으로 수행 hello 계약 다른 Microsoft Online 서비스 (예를 들어 Office 365)에 포함 합니다. 

### <a name="assign-licenses"></a>라이선스 할당

경우에 구독을 가져오는 모든 필요한 기능을 유료 tooconfigure 기능 toousers 유료 Azure AD에 대 한 라이선스를 계속 배포 해야 합니다. Azure AD 유료 기능을 통해 관리 되는 액세스 tooor 가져야 하는 모든 사용자 라이선스를 할당 되어야 합니다. 라이선스 할당은 Azure AD Premium, Basic 또는 Enterprise Mobility + Security 등의 구매한 서비스와 사용자 간의 매핑입니다.


디렉터리의 어떤 사용자에게 라이선스가 있어야 하는지 관리하려면 다음 작업을 수행하면 됩니다. 

* Toogroups hello에 라이선스 할당 [Azure 포털](active-directory-licensing-whatis-azure-portal.md)합니다.
* Toousers hello 포털, PowerShell 또는 Api를 통해 직접 라이선스를 할당 합니다. 

라이선스 tooa 그룹을 할당 하는 모든 그룹 구성원 라이선스가 할당 됩니다. 사용자가 더하거나 hello 그룹에서 제거 하는 경우에 hello 적절 한 라이선스 할당 하거나 제거 합니다. 그룹 할당 된 그룹 관리 사용 가능한 tooyou 활용할 수 있습니다 및 그룹 기반 할당 tooapplications와 일치 합니다.

사용할 수 있습니다 [그룹 기반의 라이선스 할당](active-directory-licensing-whatis-azure-portal.md) hello 다음과 같은 규칙을 tooset:
* 디렉터리의 모든 사용자가 자동으로 라이선스를 얻습니다.
* Hello 적절 한 직책을 가진 모든 사람에 게 라이선스
* Hello 조직에서 hello 의사 결정 tooother 관리자를 위임할 수 있습니다 (사용 하 여 [셀프 서비스 그룹](active-directory-accessmanagement-self-service-group-management.md))

라이선스 할당 toogroups, 대 한 자세한 내용은 포함 하 여 고급 시나리오 및 Office 365 라이선스 시나리오 참조 [toousers Azure Active Directory 그룹 멤버 자격을 통해 라이선스를 할당](active-directory-licensing-group-assignment-azure-portal.md)합니다.

## <a name="get-started-with-azure-ad-licensing"></a>Azure AD 라이선스 시작

Azure AD를 시작하는 것은 쉽습니다. 언제든지 [Azure 평가판](https://azure.microsoft.com/offers/ms-azr-0044p/) 등록의 일부로 디렉터리를 만들 수 있습니다.

hello 다음 모범 사례 보장할 수 있습니다 hello 서비스에 대 한 목표와 있습니다를 사용 하는 다른 Microsoft 서비스와 테 넌 트 정렬 됩니다.

- 이미 사용 하는 Microsoft에서 조직 서비스 hello, 이미 있는 경우 Azure AD 테 넌 트입니다. 것이 유용한 toouse hello 동일한 테 넌 트 다른 서비스에 대 한 프로 비전을 포함 하 여 핵심 id 관리 및 하이브리드 single sign on (SSO) hello 서비스에서 사용할 수 있도록 합니다. Single sign-on을 사용자에 게는 hello 서비스 전반에 걸쳐 hello 다양 한 기능에서 도움이 됩니다. 따라서 toobuy 직원에 대 한 Azure AD 유료 서비스를 결정 하는 경우 다시 테 넌 동일 hello를 사용 하는 것이 좋습니다.

- 계획인 경우 hello Azure 포털에서에서 새 테 넌 트에 사용 하는 것이 좋습니다.
  - 다른 사용자 집합(예: 파트너 또는 고객)에 대해 Azure AD를 사용합니다.
  - 프로덕션 서비스와 별개로 Azure AD 서비스를 평가합니다.
  - 서비스에 대한 샌드박스 환경을 설정합니다.

  전역 관리자 권한이 있는 외부 사용자로 계정을 사용 하 여 hello 새 디렉터리가 만들어집니다. Toohello이이 계정 사용 하 여 Azure 포털에 로그인 할 때이 테 넌이 트를 보고 모든 관리 작업에 액세스할 수 있습니다.

> [!NOTE]
> Azure AD는 “게스트 사용자”를 지원하는데, 이 외부 사용자는 Microsoft 계정 또는 다른 테넌트의 Azure AD ID 중 하나를 통해 생성된 Azure AD 테넌트의 사용자 계정입니다. hello Office 365 관리 포털은 이러한 사용자를 현재 지원 하지 않습니다. Microsoft 계정 가진 사용자가 게스트 수 tooaccess hello Office 365 관리 포털, 동안 없는 다른 Azure AD 테 넌 트의 게스트 사용자는 무시 됩니다. Hello 후자의 경우에만 hello Azure AD에서에서 사용자의 로컬 계정 hello 되었거나 여기서 hello 사용자가 원래 만들어진 Office 365 테 넌 액세스할 수 있습니다.

### <a name="select-one-or-more-license-trials"></a>하나 이상의 라이선스 평가판 선택

**Azure Active Directory** &gt; **빠른 시작** 아래에서 Azure AD Premium 또는 Enterprise Mobility + Security 평가판 구독을 활성화할 수 있습니다.

![라이선스 평가판 선택](media/active-directory-licensing-get-started-azure-portal/select-a-license-trial.png)

Hello에 사용할 수 있는 평가판 라이선스 **라이선스** 블레이드입니다.

### <a name="assign-licenses-toousers-and-groups"></a>라이선스 toousers 및 그룹 지정

Hello 구독이 활성 상태 이면 후 라이선스 tooyourself를 할당 해야 합니다. Hello 브라우저 tooensure를 hello 기능을 모두 표시를 새로 고칩니다. hello 다음 단계 toopaid Azure AD 기능에 액세스 해야 하는 tooassign 라이선스 toohello 사용자입니다. 에 설명 된 대로 [라이선스 할당](#assign-licenses), tooidentify hello hello 나타내는 필요 청중 그룹과 할당 hello 라이선스 tooit tooassign 라이선스는 한 가지 쉬운 방법은 합니다. 이러한 방식으로 수명 주기 동안 hello 그룹에서 제거 되거나 추가 된 사용자를은 할당 되거나 각각 hello 라이선스에서 제거 합니다.

> [!NOTE]
> 일부 Microsoft 서비스는 모든 위치에서 사용할 수 없습니다. 관리자에 게 hello를 지정 해야 tooa 사용자 라이선스를 할당할 수 있습니다, 전에 **사용 위치** hello 사용자에 대 한 속성. 이 속성을 설정할 수 있습니다 **사용자** &gt; **프로필** &gt; **설정을** hello Azure 포털의에서. 그룹 라이선스 할당을 사용할 경우 사용 위치가 지정 되지 않은 모든 사용자는 hello 디렉터리의 hello 위치를 상속 합니다.

tooassign 라이선스 아래에서 **Azure Active Directory** &gt; **라이선스** &gt; **모든 제품**하나 이상의 제품을 선택한 다음 선택 **할당** hello 명령 모음에서 합니다.

![라이선스 tooassign 선택](media/active-directory-licensing-get-started-azure-portal/select-license-to-assign.png)

Hello를 사용할 수 있습니다 **사용자 및 그룹** 블레이드 toochoose hello 제품의 여러 사용자 또는 그룹 또는 toodisable 서비스 계획 합니다. 사용자 및 그룹 이름에 대 한 상위 toosearch에 hello 검색 상자를 사용 합니다.

![라이선스 할당을 위한 사용자 또는 그룹 선택](media/active-directory-licensing-get-started-azure-portal/select-user-for-license-assignment.png)

라이선스 tooa 그룹을 할당 하는 경우 모든 사용자가 상속 hello hello 그룹의 사용자 수에 따라 hello 라이선스 되기까지 다소 시간이 걸릴 수 있습니다. Hello에 hello 처리 상태를 확인할 수 **그룹** hello 아래 블레이드 **라이선스** 바둑판식으로 배열입니다.

![라이선스 할당 상태](media/active-directory-licensing-get-started-azure-portal/license-assignment-status.png)

Azure AD 라이선스 할당 중에 할당 오류가 발생할 수 있지만 Azure AD 및 Enterprise Mobility + Security 제품을 관리할 경우에는 상대적으로 드물게 오류가 발생합니다. 잠재적 할당 오류는 다음으로 제한됩니다.
- 할당 충돌: 사용자 hello 현재 라이선스와 호환 되지 않는 라이선스를 이전에 할당 되었습니다. 이 경우 hello 새 라이선스를 할당 합니다. 현재 hello를 제거 해야 합니다.
- 사용 가능한 라이선스를 초과 했습니다: 사용자의 할당 상태가 반영 toomissing 라이선스 기한 오류 tooassign hello 할당 된 그룹에 사용자 수가 hello 사용 가능한 라이선스를 초과 합니다.

#### <a name="azure-ad-b2b-collaboration-licensing"></a>Azure AD B2B 공동 작업 라이선스

B2B 공동 작업 tooinvite 게스트 사용자에 게 Azure AD 테 넌 트 tooprovide 액세스 tooAzure AD 서비스에 및 있습니다 사용할 수 있도록 모든 Azure 리소스 있습니다.  

무료 B2B 사용자 초대 및 Azure AD에서 응용 프로그램 tooan를 할당 합니다. 게스트 당 too10 앱을 사용자와 3 기본 보고서는 B2B 공동 작업 사용자에 게 무료로 합니다. 게스트 사용자 hello 파트너의 Azure AD 테 넌 트에 할당 된 적절 한 라이선스가 있으면은 합니다 라이선스를 취득 내용에 합니다.

필요 하지는 않지만 tooprovide 액세스 toopaid Azure AD 기능을 사용 하도록 하려는 경우 이러한 B2B 게스트 사용자에 게 사용 허가 받아야 적절 한 Azure AD 라이선스를 사용 합니다. 라이선스를 지불 하는 Azure AD와 테 넌 트 초대 B2B 공동 작업 사용자 권한 초대 tooan 추가 5 게스트 사용자에 게 할당할 수 toohello 테 넌 트입니다. 시나리오와 정보는 [B2B 공동 작업 라이선스 지침](active-directory-b2b-licensing.md)을 참조하세요.

### <a name="view-assigned-licenses"></a>할당된 라이선스 보기

할당된 라이선스 및 사용 가능한 라이선스에 대한 요약 보기는 **Azure Active Directory** &gt; **라이선스** &gt; **모든 제품** 아래 표시됩니다.

![라이선스 요약 보기](media/active-directory-licensing-get-started-azure-portal/view-license-summary.png)

특정 제품을 선택할 때 사용 가능한 할당된 사용자 및 그룹의 자세한 목록입니다. hello **사용이 허가 된 사용자가** 목록 현재 사용 하는 라이선스 및 여부 hello 라이선스가 할당 된 직접 toohello 사용자 또는 그룹에서 상속 하는 모든 사용자를 표시 합니다.

![라이선스 세부 정보 보기](media/active-directory-licensing-get-started-azure-portal/view-license-detail.png)

마찬가지로, hello **사용이 허가 된 그룹** 목록 toowhich 라이선스 할당 된 모든 그룹이 표시 됩니다. 사용자 또는 그룹 tooopen hello 선택 **라이선스** 모든 라이선스를 보여 주는 블레이드 toothat 개체를 할당 합니다.

### <a name="remove-a-license"></a>라이선스 제거

에 게 라이선스를 tooremove toohello 사용자 또는 그룹을 이동한 hello **라이선스** 바둑판식으로 배열입니다. Hello 라이선스를 선택 하 고 클릭 **제거**합니다.

![라이선스 제거](media/active-directory-licensing-get-started-azure-portal/remove-license.png)

라이선스 그룹에서 hello 사용자가 상속 직접 제거할 수 없습니다. 대신, hello 라이선스 상속 되는지은 hello 그룹에서 hello 사용자를 제거 합니다.

### <a name="extend-trials"></a>평가판 연장

고객에 대 한 평가판 확장을 사용할 수로 셀프 서비스 hello Office 365 포털을 통해 등록 합니다. 고객 관리자 toohello Office 포털을 이동할 수 있습니다 (액세스 hello Office 포털에 대 한 권한을에 따라 다름) hello Azure AD Premium 평가판을 선택 합니다. 클릭 하 여 hello **평가판 확장** 링크 hello 확장 프로세스를 시작 합니다. 신용 카드가 필요하지만 요금이 부과되지는 않습니다.

![Hello Azure 포털에서에서 평가판을 확장 합니다.](media/active-directory-licensing-get-started-azure-portal/extend-trial-beginning.png)

## <a name="next-steps"></a>다음 단계

hello 문서를 읽기에 대해 더 알아봅니다 toolearn 고급 그룹을 통해 라이선스 관리에 대 한 시나리오 [할당 라이선스 tooa 그룹](active-directory-licensing-group-assignment-azure-portal.md)합니다.

다음 방법에 대 한 정보를은 tooconfigure 다른 Azure AD 유료 기능을 사용 하 여:

* [셀프 서비스 암호 재설정](active-directory-manage-passwords.md)
* [셀프 서비스 그룹 관리](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [Azure AD Premium 라이선스 직접 구매](http://aka.ms/buyaadp)
