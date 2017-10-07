---
title: "Active Directory Id 보호-aaaAzure 어떻게 toounblock 사용자 | Microsoft Docs"
description: "Azure Active Directory ID 보호 정책에 의해 차단된 사용자를 차단 해제하는 방법을 알아봅니다."
services: active-directory
keywords: "Azure Active Directory ID 보호, 사용자 차단 해제"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a953d425-a3ef-41f8-a55d-0202c3f250a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: cdda2808822888f76aa75cf46478738c94df51a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection---how-toounblock-users"></a>Azure Active Directory Id 보호-어떻게 toounblock 사용자
Azure Active Directory Id 보호 tooblock 사용자 hello 구성 조건을 충족 하는 정책을 구성할 수 있습니다. 일반적으로 차단 된 사용자 연락처 도움말 센터 toobecome 차단 해제 합니다. 이 항목 toounblock 차단 된 사용자를 수행할 수 있는 hello 단계를 설명 합니다.

## <a name="determine-hello-reason-for-blocking"></a>차단에 대 한 hello 이유를 확인 합니다.
첫 번째 단계 toounblock 사용자,으로 다음 단계에 좌우 되 때문에 hello 사용자 차단 정책 toodetermine hello 형식이 필요 합니다.
Azure Active Directory ID보호를 사용하여 로그인 위험 정책 또는 사용자 위험 정책으로 사용자를 차단할 수 있습니다.

Hello 유형의 hello 머리글 toohello 사용자는 로그인 시도 중에 발표 hello 대화 상자에서에서 사용자를 차단 정책 얻을 수 있습니다.

| 정책 | 사용자 대화 상자 |
| --- | --- |
| 로그인 위험 |![차단된 로그인](./media/active-directory-identityprotection-unblock-howto/02.png) |
| 사용자 위험 |![차단된 계정](./media/active-directory-identityprotection-unblock-howto/104.png) |

다음에 의해 차단된 사용자:

* 로그인 위험 정책은 의심스러운 로그인이라고도 함
* 사용자 위험 정책은 위험한 계정이라고도 함

## <a name="unblocking-suspicious-sign-ins"></a>의심스러운 로그인 차단 해제
의심 스러운 로그인 toounblock, hello 다음 옵션을 사용할 수 있습니다.

1. **친숙한 위치 또는 장치에서 로그인** - 차단된 의심스러운 로그인에 대한 일반적인 이유는 알 수 없는 위치 또는 장치에서의 로그인 시도입니다. 사용자가 친숙 한 위치 또는 장치에서 toosign에서 시도 하 여 이유를 차단 하는 hello 인지 여부를 빠르게 확인할 수 있습니다.
2. **정책에서 제외** hello 정책에 로그인의 현재 구성을 특정 사용자에 대 한 문제를 일으키는지, 여기에서 hello 사용자가 제외할 수 있다고 생각 되 면-합니다. 자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.
3. **정책을 사용 하지 않도록** 정책 구성이 모든 사용자에 대 한 문제를 일으키는지, hello 정책을 해제할 수 있다고 생각 되 면-합니다. 자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.

## <a name="unblocking-accounts-at-risk"></a>위험한 계정 차단 해제
hello 다음 옵션을 사용할 수 있는 위험에 노출 하는 계정 toounblock, 있습니다.

1. **암호 재설정** -hello 사용자의 암호를 다시 설정할 수 있습니다. 자세한 내용은 [수동으로 안전한 암호 다시 설정](active-directory-identityprotection.md#manual-secure-password-reset) 을 참조하세요.
2. **위험 이벤트를 모두 해제** -hello 사용자 위험 정책 액세스를 차단 하는 것에 대 한 구성 hello 사용자 위험 수준에 도달 하면 사용자를 차단 합니다. 수동으로 보고된 위험 이벤트를 닫아서 사용자의 위험 수준을 줄일 수 있습니다. 자세한 내용은 [수동으로 위험 이벤트 닫기](active-directory-identityprotection.md#closing-risk-events-manually)를 참조하세요.
3. **정책에서 제외** hello 정책에 로그인의 현재 구성을 특정 사용자에 대 한 문제를 일으키는지, 여기에서 hello 사용자가 제외할 수 있다고 생각 되 면-합니다. 자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.
4. **정책을 사용 하지 않도록** 정책 구성이 모든 사용자에 대 한 문제를 일으키는지, hello 정책을 해제할 수 있다고 생각 되 면-합니다. 자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계
 Azure AD Identity Protection에 대 한 자세한 tooknow 하 시겠습니까? [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 확인하세요.
