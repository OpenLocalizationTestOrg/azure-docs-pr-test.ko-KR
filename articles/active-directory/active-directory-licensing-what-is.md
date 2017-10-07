---
title: "hello Azure 클래식 포털에서에서 Azure Active Directory 사용자 aaaLicense | Microsoft Docs"
description: "Microsoft Azure Active Directory 라이선스의 설명, 작동 방법, tooget 시작 하는 방법 및 Office 365, Microsoft Intune 및 Azure Active Directory Premium 및 Basic edition을 포함 하는 모범 사례"
services: active-directory
keywords: "Azure AD 라이선스"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d769e8c6-7581-43f5-a3b4-de4b1dca2344
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;H1Hack27Feb2017
ms.openlocfilehash: 4d5f244cbee2ae37a30976f70b5d4f21c3516d90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-azure-active-directory-licensing-in-hello-azure-classic-portal"></a>Microsoft Azure Active Directory hello Azure 클래식 포털에서에서 무엇을 라이선스?

> [!div class="op_single_selector"]
> * [Azure Portal 지침 확인](active-directory-licensing-get-started-azure-portal.md)
> * [Azure 클래식 포털 정보](active-directory-licensing-what-is.md)
>
>

Azure AD(Azure Active Directory)는 Microsoft의 IDaaS(Identity as a Service) 솔루션 및 플랫폼입니다. Azure AD는 다양 한 기능 및 기술 버전에서 Office 365, Dynamics, Microsoft Intune 및 Azure와 같은 모든 Microsoft 서비스와 함께 사용할 수 있는 Azure AD Free 사이의 값으로 제공 됩니다 (Azure AD 생성 하지 않습니다는 사용료가 부과이 모드로), AD tooAzure 지불 될 Enterprise Mobility Suite (EMS), Azure AD Premium 및 Basic 같은 버전 뿐만 아니라 Azure Multi-factor Authentication (MFA)입니다. 많은 Microsoft 온라인 서비스와 마찬가지로 대부분의 Azure AD 유료 버전은 Office 365, Microsoft Intune 및 Azure AD에서 사용자별 권한 부여를 통해 제공됩니다. 이러한 경우 hello 서비스 구매는 하나 이상의 구독으로 표시 됩니다. 포함 하 고 각 구독 사전 구매 라이선스의 테 넌 트에 있습니다. 사용자 단위 자격 hello 사용자와 hello 사용자에 대 한 hello 서비스 구성 요소를 사용 하도록 설정 하는 hello 제품 간의 링크를 만들어 라이선스 할당을 통해 실현 됩니다 및 라이선스 선불 hello 중 하나를 사용 합니다.

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다. Admin 님 안녕하세요 Azure AD에서에서 관리자 역할 tooassign 센터 하는 방법에 대 한 참조 [자신과 사용자가 Azure AD에서 라이선스](active-directory-licensing-get-started-azure-portal.md)합니다.

[이제 Azure AD premium을 시도합니다.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

> [!NOTE]
> Azure AD 관리 포털 hello Azure 클래식 포털의 일부입니다. Azure AD를 사용하기 위해 Azure를 구매할 필요는 없지만 이 포털에 액세스하려면 활성 Azure 구독 또는 [Azure 평가판 구독](https://azure.microsoft.com/pricing/free-trial/)이 필요합니다.
>
>

Azure AD 서비스 기능에 대한 광범위한 개요는 [Azure AD란?](active-directory-whatis.md)을 참조하세요.
[Azure AD 서비스 수준에 대한 자세한 정보](https://azure.microsoft.com/support/legal/sla/)

> [!NOTE]
> Azure 사용량 기준 과금 방식의 구독은 다른: 또한 디렉터리에 표시 되는 동안 이러한 Azure 리소스를 만들 수 있도록 구독과 tooyour 지불 방법으로 매핑합니다. 이 경우 hello 구독과 관련 된 라이센스 수 없는 있습니다. 사용자의 연결 hello 구독에서 toomanaging 구독 리소스에 액세스 hello 사용자의 권한을 toooperate toohello 구독 매핑된 Azure 리소스에 부여 하 여 이루어집니다.
>
>

## <a name="how-does-azure-ad-licensing-work"></a>Azure AD 라이선스 작동 방식
라이선스 기반(자격 기반) Azure AD 서비스는 Azure AD 디렉터리/서비스 테넌트에서 구독을 활성화하면 작동됩니다. Hello 구독 옵션이 활성화 되 면 hello 서비스 기능을 디렉터리/서비스 관리자에 의해 관리 하 고 사용이 허가 된 사용자가 사용할 수 있습니다.

구매 또는 Enterprise Mobility Suite, Azure AD Premium 또는 Azure AD Basic에서는 디렉터리 활성화 hello 구독에서 유효 기간을 포함 하 여 업데이트 되 고 선불 라이선스. 구독 정보, 상태, 다음 수명 주기 이벤트 및 hello 할당 또는 사용 가능한 라이선스 수를 포함 하 여 hello hello 특정 디렉터리에 대 한 hello 라이선스 탭 아래에서 Azure 클래식 포털을 통해 ´ ù. 이 또한 toobest 위치 toomanage 라이선스 할당 합니다.

각 구독은 하나 이상의 서비스 계획으로 구성 됩니다, 그리고 각 매핑 hello hello 서비스 유형의; 기능 수준 포함 예를 들어 Azure AD, Azure MFA, Microsoft Intune, Exchange Online 또는 SharePoint Online 합니다. Azure AD 라이선스 관리에는 서비스 계획 수준 관리가 필요하지 않습니다. 이이 고급 구성 모드 toomanage 액세스 tooincluded 서비스에 의존 하는 Office 365와에서 다릅니다. Azure AD 서비스 구성, tooenable 기능에에서 의존 하 고 개별 사용 권한을 관리 합니다.

일반적으로 Azure AD 구독 정보는 hello hello 특정 디렉터리에 대 한 hello 라이선스 탭 아래에서 Azure 클래식 포털을 통해 관리 됩니다. Azure AD Premium의 hello 예외와 함께 azure AD 구독 hello Office 포털에 표시 되지 않습니다.

> [!IMPORTANT]
> Azure AD Premium 및 Basic, Enterprise Mobility Suite 구독 뿐만 아니라 디렉터리/테 넌 트에 사용자를 프로 비전 예외일된 tootheir 됩니다. 디렉터리나 다른 디렉터리에서 사용 되는 tooentitle 사용자 사이의 구독을 분할할 수 없습니다. 구독 디렉터리 간에 이동 가능 되지만 지원 티켓 또는 취소 및 다시 직접 구매 hello 경우에서 구매를 제출 합니다.
>
> Azure AD를 구입할 때 또는 Enterprise Mobility Suite 구독 활성화 볼륨 라이선스를 통해 수행 됩니다 자동으로 hello 계약 다른 Microsoft Online services를 예: Office 365를 포함 하는 경우.
>
>

Azure AD 기능 hello 디렉터리의 범위 hello 너비를 지불 해야 합니다. 예를 들면 다음과 같습니다.

* 그룹 기반 할당 tooapplications-관리 하는 hello 특정 응용 프로그램에서 사용 하도록 설정 됩니다.
* 고급 및 셀프 서비스 그룹 관리 기능을 hello 디렉터리 구성 또는 hello 특정 그룹 내에서 사용할 수 있습니다.
* Hello 보고 탭에 있는 프리미엄 보안 보고서
* 클라우드 응용 프로그램 검색에에서 표시 hello Azure 포털 id입니다.

### <a name="assigning-licenses"></a>라이선스 할당
구독을 가져오는 것이 모든 필요한 tooconfigure 유료 기능을 하는 동안 Azure AD 유료 기능을 사용 하 여 라이선스 toohello 사용자 배포 필요 합니다. 일반적으로 Azure AD 유료 기능을 통해 관리 되는 액세스 tooor 가져야 하는 모든 사용자의 라이선스를 할당 되어야 합니다. 라이선스 할당은 Azure AD Premium, Basic 또는 Enterprise Mobility Suite 등의 구매한 서비스와 사용자 간의 매핑입니다.

디렉터리의 어떤 사용자에게 라이선스가 있어야 하는지 관리하는 것은 간단합니다. Tooa 그룹 toocreate hello Azure AD 관리 포털을 통해 할당 규칙을 할당 하 여 또는 포털, PowerShell 또는 Api를 통해 toohello 사용자 라이선스를 직접 할당 하 여 수행할 수 있습니다. 라이선스 tooa 그룹에 할당할 때 라이선스 모든 그룹 구성원 할당 됩니다. 사용자가 더하거나 hello 그룹에서 제거 하는 경우 적절 한 라이선스를 할당 또는 제거 된 hello 됩니다. 그룹 할당 모든 그룹 관리 사용 가능한 tooyou를 활용할 수 있으며 그룹 기반 할당 tooapplications와 일치. 이 접근 방식을 사용 디렉터리의 모든 사용자는 자동으로 할당 되도록 규칙을 설정할 hello 적절 한 직책을 가진 모든 사용자의 라이선스 하거나도 hello 조직의 hello 의사 결정 tooother 관리자를 위임할 수 있습니다.

사용 위치 누락 된 모든 사용자 그룹 기반의 라이선스 할당을 할당 하는 동안 hello 디렉터리 위치를 상속 합니다. 이 위치는 hello 관리자가 언제 든 지 변경할 수 있습니다. 여기서 hello 자동 실패 했습니다 할당 하는 경우에 tooerror, 사용자 정보에서 hello 라이선스 유형을 해당 상태를 반영 합니다.

## <a name="getting-started-with-azure-ad-licensing"></a>Azure AD 라이선스 시작
Azure AD로 시작 하는 것은 간단 합니다. 항상 서명 tooa 무료 Azure 평가판의 일부로 디렉터리를 만들 수 있습니다. [조직으로 등록하는 방법에 대해 자세히 알아보세요](sign-up-organization.md). hello 다음 유용 디렉터리는 사용 중일 수 있지만 또는 tooconsume, 및 가져오는 hello 서비스 목표를 계획 하는 다른 Microsoft 서비스와 가장 정렬 있는지 확인 합니다.

몇 가지 모범 사례가 있습니다.

* Microsoft의 조직 서비스를 이미 사용 중이면 이미 Azure AD 디렉터리가 있는 것입니다. 이 경우 계속 해야 toouse hello 다른 서비스에 대 한 동일한 디렉터리 hello 서비스 전반에 걸쳐 프로비저닝 및 하이브리드 SSO 비롯 한 핵심 id 관리를 활용할 수 있도록 합니다. 사용자가 단일 로그온 경험을 hello 서비스 전반에 걸쳐 다양 한 기능에서 활용 합니다. 결과적으로, Azure AD는 toobuy 직원에 대 한 서비스를 유료 기능을 결정 하는 경우 권장를 사용 하는 동일한 디렉터리 toodo이 hello 합니다.
* Toouse 다른 일련의 사용자 (파트너, 고객 및 등)에 대 한 Azure AD를 계획 하는 경우 또는 tooevaluate Azure AD 서비스 ु toodo 원하는 경우 프로덕션 서비스의 격리에는 샌드박스 환경 toosetup를 조회 하는 경우 또는 서비스에 대 한 hello Azure Azure 클래식 포털을 통해 새 디렉터리를 먼저 만드는 것이 좋습니다. [새로 만드는 방법에 대 한 자세한 정보 hello Azure 클래식 포털에서에서 Azure AD 디렉터리](active-directory-licensing-directory-independence.md)합니다. hello 새 디렉터리 전역 관리자 권한이 있는 외부 사용자로 계정을 사용 하 여 생성 됩니다. Azure 클래식 toohello에 로그인 할 때이 계정을 사용 하 여 포털 있습니다 수 toosee이이 디렉터리 되며 모든 디렉터리 관리 작업에 액세스 합니다. 로컬 계정을 만드는 toomanage 적절 한 권한이 있는 다른 Microsoft 서비스 (하 hello Azure 클래식 포털을 통해 액세스할 수 없음) 하는 것이 좋습니다. [Azure AD에서 사용자 계정을 만드는 방법에 대해 자세히 알아보세요](active-directory-create-users.md).

> [!NOTE]
> Azure AD는 "외부 사용자"를 지원하는데, 이 외부 사용자는 Microsoft 계정(MSA) 또는 다른 디렉터리의 Azure AD ID 중 하나를 사용하여 생성된 Azure AD 인스턴스의 사용자 계정입니다. 사용 하는 동안 확장이 기능은 모든 Microsoft의 조직 구성 서비스를 지금 바로 이러한 계정에서 지원 되지 않는 hello 서비스 경험;의 일부 예를 들어 hello Office 365 관리 포털은 현재 이러한 사용자를 지원 하지 않습니다. 결과적으로, Microsoft 계정은 외부 사용자에 게 되지 않습니다 수 tooaccess hello Office 365 관리 포털, 반면에 다른 Azure AD 디렉터리의 외부 사용자가 무시 합니다. 여기서 hello 사용자를 처음 만들 디렉터리는 hello 후자의 경우, 유일한 hello 사용자의 로컬 계정, Azure AD hello 또는 Office 365에서 이러한 환경을 통해 액세스할 수 있는 것입니다.
>
>

표시된 대로 Azure AD에는 다른 유료 버전이 있습니다. 이러한 버전은 구매 가용성에 약간의 차이가 있습니다.

| 제품 | EA/VL | 열기 | CSP | MPN 사용 권한 | 직접 구매 | 평가판 |
| --- | --- | --- | --- | --- | --- | --- |
| Enterprise Mobility Suite |X |X |X |X | |X |
| Azure AD Premium |X |X |X | |X |X |
| Azure AD Basic |X |X |X |X |<br /> |<br /> |

### <a name="select-one-or-more-license-trials"></a>하나 이상의 라이선스 평가판 선택
 모든 경우에 디렉터리의 hello 라이선스 탭에서 원하는 hello 특정 평가판을 선택 하 여 Azure AD Premium 또는 Enterprise Mobility Suite 평가판 구독을 활성화할 수 있습니다. 어느 평가판이든 라이선스 100개에 30일 구독이 포함됩니다.

![Azure Active Directory 평가판 라이선스 계획](./media/active-directory-licensing-what-is/trial_plans.png)

![Enterprise Mobility Suite 평가판 라이선스 계획](./media/active-directory-licensing-what-is/EMS_trial_plan.png)

![활성 평가판 라이선스 계획](./media/active-directory-licensing-what-is/active_license_trials.png)

### <a name="assign-licenses"></a>라이선스 할당
Hello 구독 옵션이 활성화 되 면 라이선스 tooyourself 할당 하 고 모든 기능을 표시 하는 hello 브라우저 tooensure 새로 고침 해야 합니다. hello 다음 단계는 tooassign 라이선스 tooaccess 필요 합니다 또는에 포함 되어야 하는 toohello 사용자 유료 Azure AD 기능입니다. 에서 언급 했 듯이 위에 할당 라이선스"," hello 가장 좋은 방법은 toodo이 tooidentify hello 그룹 hello 필요 청중을 나타내는 이며; toohello 라이선스 할당 이러한 방식으로 수명 주기 동안 hello 그룹에서 제거 되거나 추가 된 사용자를 tooor hello 라이선스에서 제거할 할당 됩니다.

tooassign 라이선스 tooa 그룹 또는 개별 사용자 라이선스 계획 tooassign 선택한 클릭 hello **할당** hello 명령 모음에서 합니다.

![활성 평가판 라이선스 계획](./media/active-directory-licensing-what-is/assign_licenses.png)

Hello 할당 hello 선택한 계획에 대 한 대화 상자에서 사용자 및 toohello 추가한를 선택할 수 면 **할당** hello 오른쪽에 열입니다. Hello에 유리 hello 조회를 사용 하 여 특정 개인을 검색 하거나 hello 사용자 목록 방식을 지정할 수 있습니다 hello 사용자 눈금의 오른쪽 위에 있습니다. tooassign 그룹 hello에서 "Groups"를 선택 **표시** 메뉴 및 표시 되는 hello 오른쪽 toorefresh hello 할당에 hello 확인 단추를 클릭 합니다.

![라이선스 toogroups 할당](./media/active-directory-licensing-what-is/assign_licenses_to_groups.png)

지금 검색 수 또는 페이지 그룹을 통해 고 toohello 추가할 **할당** 열 hello에 동일한 방식으로 합니다. 한 번에 이러한 tooassign 사용자 및 그룹의 조합을 사용할 수 있습니다. toocomplete 할당 프로세스 hello, hello의 오른쪽 아래 모서리 hello 페이지 hello 확인 단추를 클릭 합니다.

![라이선스 할당 진행률 메시지](./media/active-directory-licensing-what-is/license_assignment_progress_message.png)

그룹이 할당 된 경우 해당 멤버는 30 분 내에 있지만 일반적으로 1-2 분 이내 hello 라이선스를 상속 합니다.

Azure AD 라이선스 할당 중에 할당 오류가 발생할 수 있지만 상대적으로 드문 경우입니다. 잠재적 할당 오류는 다음으로 제한됩니다.

* 할당 충돌-사용자가 이전에 hello 현재 라이선스와 호환 되지 않는 라이선스를 할당 하는 경우. 이 경우 hello 새 라이선스를 할당에서는 이전 hello를 제거 합니다.
* 초과 사용 가능한 라이선스가-할당 된 그룹에 사용자 수가 hello 사용 가능한 라이선스를 초과 하는 경우 hello 사용자의 할당 상태가 toomissing 라이선스 기한 오류 tooassign을 반영 됩니다.

### <a name="view-assigned-licenses"></a>할당된 라이선스 보기
사용 가능, 다시 할당 하 고 다음 구독 수명 주기 이벤트를 비롯 하 여 할당 된 라이선스의 요약 보기 hello에 표시 됩니다 **라이선스** 탭 합니다.

![할당 된 라이선스의 hello 번호 보기](./media/active-directory-licensing-what-is/view_assigned_licenses.png)

라이선스 계획으로 이동하면 할당 상태 및 경로(직접 또는 하나 이상의 그룹에서 상속)를 비롯하여 할당된 사용자 및 그룹의 세부 목록을 사용할 수 있습니다.

![라이선스 계획에 대해 할당된 라이선스의 세부 정보 표시](./media/active-directory-licensing-what-is/assigned_licenses_detail.png)

라이선스 제거는 할당하는 것만큼 쉽습니다. Hello 사용자가 직접 할당 하거나 할당된 된 그룹에 대 한 hello 라이선스 유형을 선택 하 여 hello 라이선스를 제거할 수 있습니다을 선택 하면 **제거**, hello 사용자 또는 그룹 toohello 제거 목록에 추가 하 고 hello 동작을 확인 합니다. 또는 라이선스 유형, 선택 hello 특정 사용자 또는 그룹을 열 수를 탭 **제거** hello 명령 모음에서 합니다. tooend 사용자의 라이선스 그룹에서 상속 hello 그룹에서 단순히 hello 사용자를 제거 합니다.

### <a name="extending-trials"></a>평가판 확장
고객에 대 한 평가판 확장은 사용할 수 hello Office 365 포털을 통해 셀프 서비스입니다. 고객 관리자 toohello 탐색할 수 [Office 포털](https://portal.office.com/#Billing) (액세스 hello Office 포털에 대 한 권한을에 따라 다름) 하 고 사용자가 Azure AD Premium 평가판을 선택 합니다. Hello 클릭 **평가판 확장** 에 연결 하 고 hello 지침을 따릅니다. 신용 카드 tooenter 필요 하지만 요금이 청구 되지 않습니다.

![Hello Office 포털에서 평가판을 라이선스를 확장합니다.](./media/active-directory-licensing-what-is/extend_license_trial.png)

또한 고객이 지원 요청을 제출하여 평가판 확장을 요청할 수도 있습니다. 고객 관리자 toohello Office 365 포털을 탐색할 수 [지원 페이지](http://aka.ms/extendAADtrial) (액세스 hello Office 지원 페이지에 대 한 권한을에 따라 다름). 이 페이지에서 기능 아래의 "구독 및 평가판" 및 증상 아래의 "평가판 질문"을 선택합니다. 마지막으로 hello 상황에 정보 입력

![지원 요청을 사용하여 라이선스 평가판 확장](./media/active-directory-licensing-what-is/alternate_office_aad_trial_extension.png)

## <a name="next-steps"></a>다음 단계
이제 준비 tooconfigure 될 수도 있으며 일부 Azure AD Premium 기능을 사용할 수 있습니다.

* [셀프 서비스 암호 재설정](active-directory-manage-passwords.md)
* [셀프 서비스 그룹 관리](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect 상태](active-directory-aadconnect-health.md)
* [그룹 할당 tooapplications](active-directory-manage-groups.md)
* [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [Azure AD Premium 라이선스 직접 구매](http://aka.ms/buyaadp)
