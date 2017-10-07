---
title: "Azure Active Directory에서 그룹에 대 한 라이선스 문제 aaaResolve | Microsoft Docs"
description: "어떻게 tooidentify 및 해결 라이선스 할당 문제 Azure Active Directory 그룹 기반의 라이선스를 사용 하는 경우"
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
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ec9c74214a9e246f21fcf767b0bbd586ae702445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="identify-and-resolve-license-assignment-problems-for-a-group-in-azure-active-directory"></a>Azure Active Directory에서 그룹에 대한 라이선스 문제 식별 및 해결

Azure Active Directory (Azure AD)에서 라이선스 그룹 기반의 라이선스 오류 상태에 있는 사용자의 hello 개념이 도입 되었습니다. 이 문서에서는이 상태에서 사용자가 생길 수는 이유는 hello 이유에 설명 합니다.

그룹 기반 라이선스를 사용 하지 않고 직접 tooindividual 사용자 라이선스 할당 하면 hello 할당 작업이 실패할 수 있습니다. 예를 들어 hello PowerShell cmdlet을 실행 하는 하면 `Set-MsolUserLicense` hello cmdlet는 사용자에 다양 한 관련된 toobusiness 논리는 실패할 수 있습니다. 예를 들어 있을 수 있습니다 할당 될 수 없는 hello에 동일한 두 개의 서비스 계획 간의 충돌 또는 라이선스 수 부족 시간입니다. hello 문제는 즉시 보고 tooyou를 백업 합니다.

그룹 기반의 사용 하는 경우 라이선스, hello 같은 오류가 발생할 수 있지만 이러한 경우에 발생할 hello 백그라운드에서 hello Azure AD 서비스 라이선스를 할당 됩니다. 이러한 이유로 hello 오류에서 전달된 tooyou을 즉시 일 수 없습니다. 대신, hello 사용자 개체에 기록 하 고 있으면 hello 관리 포털을 통해 보고 합니다. Note hello 원래 의도 toolicense hello 사용자가 손실 되지 않지만 향후 조사 및 해결 방법에 대 한 오류 상태에 기록 됩니다.

## <a name="how-toofind-license-assignment-errors"></a>Toofind 할당 오류를 라이선스 하는 방법

1. 특정 그룹에 대 한 오류 상태, hello 그룹에 대 한 열기 hello 블레이드 toofind 사용자입니다. 오류 상태인 사용자가 있는 경우 **라이선스**에 알림이 표시됩니다.

![그룹, 오류 알림](media/active-directory-licensing-group-problem-resolution-azure-portal/group-error-notification.png)

2. Hello 알림 tooopen 모든 영향을 받는 사용자의 목록을 클릭 합니다. 클릭할 수 있는 각 사용자에 개별적으로 toosee 더 자세히 설명 합니다.

![그룹, 오류 상태인 사용자의 목록](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-users-with-errors.png)

3. toofind hello에 오류가 하나 이상 포함 하는 모든 그룹 **Azure Active Directory** 블레이드 선택 **라이선스** 차례로 **개요**합니다. 일부 그룹에서 주의가 필요한 경우 정보 상자가 표시됩니다.

![개요, 오류 상태인 그룹에 대한 정보](media/active-directory-licensing-group-problem-resolution-azure-portal/group-errors-widget.png)

4. Hello 상자 toosee 오류가 있는 모든 그룹의 목록을 클릭 합니다. 자세한 내용은 각 그룹을 클릭하면 됩니다.

![개요, 오류가 발생한 그룹의 목록](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-groups-with-errors.png)


다음은 각 잠재적인 문제 및 hello 방식으로 tooresolve에 대 한 설명을 것입니다.

## <a name="not-enough-licenses"></a>라이선스 부족

**문제:** hello 그룹에 지정 된 hello 제품 중 하나에 대 한 충분 한 사용 가능한 라이선스가 없습니다. Tooeither 필요한 hello 제품에 대 한 추가 라이선스를 구매 하거나 다른 사용자 또는 그룹에서 사용 하지 않는 라이선스를 확보 합니다.

toosee 사용할 수 있는 라이선스 수, 너무 이동**Azure Active Directory** > **라이선스** > **모든 제품**합니다.

사용자와 그룹을 사용 하는 라이선스를 toosee 제품을 클릭 합니다. **사용이 허가된 사용자**에는 라이선스가 직접 할당되었거나 하나 이상의 그룹을 통해 할당된 모든 사용자가 표시됩니다. **사용이 허가된 그룹**에는 제품이 할당된 모든 그룹이 표시됩니다.

**PowerShell:** PowerShell cmdlet은 이 오류를 _CountViolation_으로 보고합니다.

## <a name="conflicting-service-plans"></a>서비스 계획 충돌

**문제:** hello 그룹에 지정 된 hello 제품의 다른 제품을 통해 사용자를 할당 된 toohello 이미 있는 다른 서비스 계획으로 충돌 하는 서비스 계획을 포함 합니다. 일부 서비스 계획을 할당할 수 toohello 방식으로 구성 된 동일한 사용자에 게 다른 관련된 서비스 계획 합니다.

다음 예제는 hello를 것이 좋습니다. 사용자에 게 Office 365 Enterprise에 대 한 라이선스가 **E1** 를 직접 사용 하도록 설정 하는 모든 hello 계획에 할당 합니다. hello 사용자가 Office 365 Enterprise hello 있는 tooa 그룹 추가 **E3** 할당 제품 tooit 합니다. 이 제품에에서 포함 되어 있으면 E1, hello 그룹 라이선스 할당 hello "충돌 하는 서비스 계획" 오류와 함께 실패 합니다 hello 계획과 겹칠 수 없습니다 있는 서비스 계획을 포함 합니다. 이 예제에서는 서비스 계획을 충돌 하는 hello와 같습니다.

-   SharePoint Online(계획 2)은 SharePoint Online(계획 1)과 충돌합니다.
-   Exchange Online(계획 2)은 Exchange Online(계획 1)과 충돌합니다.

toosolve이이 충돌을 toodisable 이러한 두 계획을 직접 할당 된 toohello 사용자 라이선스 E1 hello에 필요 합니다. 또는 toomodify hello 전체 그룹 라이선스 할당 필요 하 고 hello hello E3 라이선스 계획을 사용 하지 않도록 설정 합니다. 또는 hello E3 라이선스의 hello 컨텍스트에서 중복 될 경우 hello 사용자 로부터 tooremove hello E1 라이선스를 결정할 수 있습니다.

충돌 하는 제품 tooresolve 항상 라이선스에 대 한 의사 결정 hello toohello 관리자를 속해 있습니다. Azure AD는 라이선스 충돌을 자동으로 해결하지 않습니다.

**PowerShell:** PowerShell cmdlet은 이 오류를 _MutuallyExclusiveViolation_으로 보고합니다.

## <a name="other-products-depend-on-this-license"></a>기타 제품은 이 라이선스에 종속됨

**문제:** hello 그룹에 지정 된 hello 제품 중 하나에 함수에 다른 제품에 다른 서비스 계획을 설정 해야 하는 서비스 계획을 포함 합니다. 이 오류는 Azure AD tooremove hello 기본 서비스 계획을 시도할 때 발생 합니다. 예를 들어 hello 그룹에서 제거 되 고 hello 사용자의 결과로이 발생할 수 있습니다.

toosolve이이 문제를 일부 다른 메서드를 통해 toousers 또는 해당 사용자에 대 한 종속 서비스 hello을 사용할 수 없음을 해당 hello 필수 계획 여전히 할당 되었는지 toomake 필요 합니다. 하에서 해당 사용자가 제대로 hello 그룹 라이선스를 제거할 수 있습니다.

**PowerShell:** PowerShell cmdlet은 이 오류를 _DependencyViolation_으로 보고합니다.

## <a name="usage-location-isnt-allowed"></a>사용 위치가 허용되지 않음

**문제:** 현지법 및 규정으로 인해 지역에 따라 일부 Microsoft 서비스가 제공되지 않을 수 있습니다. 라이선스 tooa 사용자를 할당할 수 있습니다, 전에 hello 사용자에 대 한 toospecify hello "사용 위치" 속성을 해야 합니다. Hello에서 이렇게 하려면 **사용자** > **프로필** > **설정을** hello Azure 포털의에서 섹션입니다.

Azure AD tooassign 사용 위치가 지원 되지 않습니다 그룹 라이선스 tooa 사용자가을 시도 하면 실패 하 고 hello 사용자에이 오류를 기록 합니다.

toosolve이이 문제를 hello 사용이 허가 된 그룹에서 지원 되지 않는 위치에서 사용자를 제거 합니다. 또는 사용 위치 값을 현재 hello hello 실제 사용자 위치를 나타낸다면 하지 수정할 수 있습니다 (hello 새 위치로 지원 됨) 하는 경우 hello 라이선스 다음에 올바르게 할당 되도록 합니다.

**PowerShell:** PowerShell cmdlet은 이 오류를 _ProhibitedInUsageLocationViolation_으로 보고합니다.

> [!NOTE]
> Azure AD에서 그룹 라이선스를 할당, hello 디렉터리의 hello 위치 사용 위치를 지정 하지 않고 모든 사용자가 상속 합니다. 관리자가 hello 올바른 사용 위치 값에 설정할 사용자 그룹 기반의 라이선스 toocomply 현지법 및 규정에 사용 하기 전에 것이 좋습니다.

## <a name="what-happens-when-theres-more-than-one-product-license-on-a-group"></a>한 그룹에 두 개 이상의 제품 라이선스가 있으면 어떻게 되나요?

둘 이상의 제품 라이선스 tooa 그룹을 할당할 수 있습니다. 예를 들어 Office 365 Enterprise E3를 할당할 수 있습니다 및 Enterprise Mobility + 보안 tooa 그룹 tooeasily 사용자에 대해 포함 된 모든 서비스를 사용 합니다.

Azure AD tooassign hello 그룹 tooeach 사용자에 지정 된 모든 라이선스를 시도 합니다. 하는 경우 Azure AD 또는 할당할 수 없습니다 hello 제품 중 비즈니스 논리 문제 때문에 (all에 대 한 라이선스가 충분 하지 않은 경우에 예를 들어 hello 사용자에 사용할 수 있는 다른 서비스와 충돌이 있을 경우), hello hello 그룹의 다른 라이선스가 할당 되지 않습니다 중 하나입니다.

사용자에 게 할당 된 tooget 실패 실패 수 toosee hello 및이 영향을 주는 제품 확인 됩니다.

## <a name="license-assignment-fails-silently-for-a-user-due-tooduplicate-proxy-addresses-in-exchange-online"></a>Exchange Online에서 tooduplicate 프록시 주소로 인해 사용자에 대 한 라이선스 할당은 자동으로 실패

Exchange Online을 사용 하는 경우 테 넌 트의 일부 사용자가 잘못 구성 하지 hello로 동일한 프록시 주소 값입니다. 라이선스 그룹 기반의 라이선스 toosuch 사용자 tooassign를 시도할 때 실패 하 고 오류가 기록 되지 것입니다 (달리에 hello 위에 설명 된 다른 오류 상황)-이이 기능의 hello 미리 보기 버전에 대 한 제한 사항 및 tooaddress 하겠습니다 하기 *일반 공급*합니다.

> [!TIP]
> 일부 사용자가 라이선스를 받지 못했으며 해당 사용자에 대해 기록된 오류가 없는 경우 먼저 중복된 프록시 주소를 갖고 있는지 확인합니다.
> Hello 다음 Exchange Online에 대 한 PowerShell cmdlet을 실행 하 여이 작업을 수행할 수 있습니다.
```
Run Get-Recipient | where {$_.EmailAddresses -match "user@contoso.onmicrosoft.com"} | fL Name, RecipientType,emailaddresses
```
> [이 문서](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online) 에 정보를 포함 하 여이 문제에 대 한 자세한 정보가 [어떻게 원격 PowerShell을 사용 하 여 온라인 tooconnect tooExchange](https://technet.microsoft.com/library/jj984289.aspx)합니다.

문제를 해결 하는 프록시를 hello 영향을 받는 사용자에 대 한 확인 된 후 hello 그룹 toomake 라이선스를 다시 적용 되는데 이제 있는지에 대 한 처리 있는지 tooforce 라이선스를 확인 합니다.

## <a name="how-do-you-force-license-processing-in-a-group-tooresolve-errors"></a>라이선스 그룹 tooresolve 오류 처리를 강제 적용 하는 수 있습니까?

Tooresolve 오류 지나온 있는 단계에 따라, 필요한 toomanually 트리거 처리 그룹 tooupdate hello 사용자 상태의 수 있습니다.

예를 들어, 사용자 로부터 직접 라이선스 할당을 제거 하 여 일부 라이선스를 확보 하는 경우 이전에 실패 한 toofully 라이선스 모든 사용자 멤버 그룹의 tootrigger 처리를 해야 합니다. toodo 찾을 hello 그룹 블레이드를 열고 **라이선스**, 및 선택 hello **다시 처리** hello 도구 모음 단추입니다.

## <a name="next-steps"></a>다음 단계

그룹을 통해 라이선스 관리에 대 한 다른 시나리오에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure Active Directory에서 tooa 그룹 라이선스 할당](active-directory-licensing-group-assignment-azure-portal.md)
* [Azure Active Directory의 그룹 기반 라이선스란?](active-directory-licensing-whatis-azure-portal.md)
* [Toomigrate 개별 toogroup 기반 라이선스 Azure Active Directory에서 사용자가 사용이 허가 된 방법](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory 그룹 기반 라이선스 추가 시나리오](active-directory-licensing-group-advanced.md)
