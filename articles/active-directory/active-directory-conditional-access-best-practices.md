---
title: "Azure Active Directory의 조건부 액세스에 대 한 aaaBest 사례 | Microsoft Docs"
description: "조건부 액세스 정책을 구성할 때 알아야 할 사항과 수행하지 않아야 할 사항에 대해 자세히 알아봅니다."
services: active-directory
keywords: "조건부 액세스 tooapps, Azure AD 사용 하 여 조건부 액세스 조건부 액세스 정책 toocompany 리소스 액세스 보안"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a>Azure Active Directory의 조건부 액세스 모범 사례

이 항목에서는 조건부 액세스 정책을 구성할 때 알아야 할 사항과 수행하지 않아야 할 사항에 대한 정보를 제공합니다. 이 항목을 읽기 전에 알아야 할 hello 개념 및 용어 hello에 설명 된 [Azure Active Directory의 조건부 액세스](active-directory-conditional-access-azure-portal.md)

## <a name="what-you-should-know"></a>알아야 할 사항

### <a name="whats-required-toomake-a-policy-work"></a>Toomake 정책 작업에 필요한 항목

새 정책을 만들 경우 선택된 사용자, 그룹, 앱 또는 액세스 제어가 없습니다.

![클라우드 앱](./media/active-directory-conditional-access-best-practices/02.png)


toomake 정책상 작업, hello 다음을 구성 해야 합니다.


|대상           | 방법                                  | 이유|
|:--            | :--                                  | :-- |
|**클라우드 앱** |Tooselect 앱을 하나 이상 필요합니다.  | 조건부 액세스 정책의 hello ֲ tooenable 있습니다 toofine 조정 권한이 있는 사용자가 앱에 액세스할 수 있는 방법입니다.|
| **사용자 및 그룹** | Tooselect 하나 이상 필요한 사용자 또는 그룹을 선택한 tooaccess hello 클라우드 앱 권한을 부여 합니다. | 할당된 사용자와 그룹이 없는 조건부 액세스 정책은 트리거되지 않습니다. |
| **액세스 제어** | 하나 이상의 tooselect 필요한 액세스 제어 합니다. | 정책 프로세서 조건을 충족 하는 경우 어떤 toodo tooknow를 필요 합니다.|


더하기 toothese 기본 요구 사항은 대부분의 경우에서에 조건을 구성 해야 합니다. 정책 구성 된 조건 없이 작동, 동안 tooyour 앱 액세스를 미세 조정에 대 한 주요 요인인 hello 조건은입니다.


![클라우드 앱](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a>할당은 어떻게 평가됩니까?

모든 할당은 논리적으로 **and**가 적용됩니다. 둘 이상의 할당을 구성 tootrigger을 정책에 있는 경우에 모든 할당을 충족 되어야 합니다.  

조직의 네트워크 외부에서 만든 tooall 연결 적용 되는 위치 조건을 tooconfigure 해야 할 경우이 수행할 수 있습니다.

- **모든 위치** 포함
- **모든 신뢰할 수 있는 IP** 제외

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a>Hello Azure 클래식 포털에서에서 정책 및 Azure 포털이 구성 되어 있는 경우 어떻게 되나요?  
및이 두 정책은 Azure Active Directory에서 적용 되는 모든 요구 사항을 충족 하는 경우에 hello 사용자 액세스를 가져옵니다.

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a>Hello Intune Silverlight 포털에에서 정책과 hello Azure 포털에 있는 경우 어떻게 되나요?
및이 두 정책은 Azure Active Directory에서 적용 되는 모든 요구 사항을 충족 하는 경우에 hello 사용자 액세스를 가져옵니다.

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a>여러 정책을 같은 사용자 구성 hello에 대 한이 있는 경우 어떻게 되나요?  
모든 로그인에 대 한 Azure Active Directory 모든 정책을 평가 하 고 부여한 액세스 toohello 사용자 하기 전에 모든 요구 사항이 충족 되었는지 확인 합니다.


### <a name="does-conditional-access-work-with-exchange-activesync"></a>조건부 액세스가 Exchange ActiveSync에서 작동합니까?

예, 조건부 액세스 정책에서 Exchange ActiveSync를 사용할 수 있습니다.


## <a name="what-you-should-avoid-doing"></a>금지해야 할 기능

hello 조건부 액세스 프레임 워크 구성 뛰어난 유연성을 제공합니다. 그러나 뛰어난 유연성도 의미 각 구성 정책 이전 tooreleasing 주의 깊게 검토 해야 하기 tooavoid 잘못 된 결과입니다. 이 컨텍스트에서 사용할 때 특히 주의 tooassignments와 같은 집합 전체에 영향을 주는 기울여야 **모든 사용자 / 그룹 / 클라우드 앱**합니다.

사용자 환경에는 구성을 따르고 hello를 피해 야 합니다.


**모든 사용자에 대한 모든 클라우드 앱:**

- **액세스 차단** - 이 구성은 사용자 전체 조직을 차단하므로 사용하지 않는 것이 좋습니다.

- **준수 장치 필요** -사용자에 대 한 하지 않는 등록 장치를 아직이 정책은 액세스 toohello Intune 포털을 포함 한 모든 액세스를 차단 합니다. 등록된 된 장치가 없는 관리자 인 경우이 정책은 hello Azure 포털 toochange hello 정책에는 도달에서 차단 됩니다.

- **도메인 가입을 요구** -이 정책 블록 액세스도 hello 잠재적인 tooblock에 대 한 권한이 모든 사용자가 조직에는 도메인에 가입 된 장치 아직 없는 경우.


**모든 사용자 경우 모든 클라우드 앱, 모든 장치 플랫폼은 다음과 같습니다.**

- **액세스 차단** - 이 구성은 사용자 전체 조직을 차단하므로 사용하지 않는 것이 좋습니다.


## <a name="common-scenarios"></a>일반적인 시나리오

### <a name="requiring-multi-factor-authentication-for-apps"></a>앱에 다단계 인증 필요

많은 환경 다른 hello 보다 더 높은 수준의 보호를 요구 하는 앱에 포함 합니다.
이 경우, 예를 들어 hello toosensitive 데이터에 액세스 된 응용 프로그램에 대 한 합니다.
보호 toothese 앱의 다른 레이어 tooadd을 원하는 경우 사용자가 이러한 앱에 액세스 하는 다단계 인증을 요구 하는 조건부 액세스 정책을 구성할 수 있습니다.


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>신뢰할 수 없는 네트워크에서 액세스하기 위한 다단계 인증 필요

이 시나리오는 multi-factor authentication에 대해 요구 사항을 추가 하기 때문에 비슷한 toohello 이전 시나리오는입니다.
그러나 hello 주요 차이점은이 요구 사항에 대 한 hello 조건입니다.  
Hello 이전 시나리오의 hello 포커스 toosensitve 데이터 액세스를 사용 하 여 앱에 때 hello이이 시나리오는 신뢰할 수 있는 위치에.  
즉 사용자가 신뢰할 수 없는 네트워크에서 앱에 액세스하는 경우 다단계 인증에 대한 요구 사항이 있을 수 있습니다.


### <a name="only-trusted-devices-can-access-office-365-services"></a>신뢰할 수 있는 장치만 Office 365 서비스에 액세스 가능

사용자 환경에서 Intune을 사용 하는 경우 hello Azure 콘솔에서에서 조건부 액세스 정책 인터페이스 hello 사용을 즉시 시작할 수 있습니다.

많은 Intune 고객 신뢰할 수 있는 장치에만 Office 365 서비스에 액세스할 수 있도록 조건부 액세스 tooensure를 사용 중입니다. 이 의미 있고 Windows Pc 조인된 tooan 온-프레미스 도메인은 모바일 장치는 Intune에 등록 된 및 규정 준수 정책 요구 사항을 충족 합니다. 주요한 개선 사항은 하지 않았는지 tooset 각 hello Office 365 서비스에 대해 같은 정책 hello 합니다.  새 정책을 만들 때 hello 클라우드 앱 tooinclude 각와 tooprotect 조건부 액세스를 사용 하 여 원하는 hello O365 앱을 구성 합니다.

## <a name="next-steps"></a>다음 단계

Tooknow tooconfigure 조건부 액세스 정책을 참조 하는 방법을 원하면 [Azure Active Directory의 조건부 액세스 시작](active-directory-conditional-access-azure-portal-get-started.md)합니다.
