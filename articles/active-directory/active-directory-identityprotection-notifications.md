---
title: "Active Directory Id 보호 알림 aaaAzure | Microsoft Docs"
description: "알림에서 조사 활동을 지원하는 방법에 대해 알아봅니다."
services: active-directory
keywords: "Azure Active Directory ID 보호, 클라우드 앱 검색, 응용 프로그램 관리, 보안, 위험, 위험 수준, 취약점, 보안 정책"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 19e62374873f034591c658a779f97d935766c612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a>Azure Active Directory ID 보호 알림
Azure AD Id 보호는 두 가지 유형의 자동화 된 알림 사용자 위험 및 위험 이벤트 관리 toohelp 전자 메일로 보냅니다.

* 사용자 손상된 경고 전자 메일
* 주간 다이제스트 전자 메일

## <a name="user-compromised-alert-email"></a>사용자 손상된 경고 전자 메일
Azure AD ID 보호가 계정이 손상되었다고 식별하는 경우 사용자 손상된 전자 메일 경고를 생성합니다. hello 전자 메일에 사용자가을 hello Identity Protection 대시보드에서 위험 보고서에 대 한 플래그가 지정 된 링크 toohello를 포함 됩니다. 손상된 계정에 대한 알림을 즉시 조사하는 것이 좋습니다.

## <a name="weekly-digest-email"></a>주간 다이제스트 전자 메일
주 단위 요약 전자 메일 hello 새 위험 이벤트의 요약을 포함 합니다.<br>
 다음을 포함합니다.

* 위험에 노출된 사용자
* 의심스러운 활동
* 감지된 취약점
* 링크 toohello Id 보호에서 보고서와 관련 된

<br>
![업데이트 관리](./media/active-directory-identityprotection-notifications/400.png "업데이트 관리")
<br>

주 단위 요약 메일 보내기를 끌 수 있습니다.
<br><br>
![사용자 위험](./media/active-directory-identityprotection-notifications/62.png "사용자 위험")
<br>

**tooopen hello 관련된 구성 대화 상자**:

1. Hello에 **Azure AD Identity Protection** 블레이드에서 클릭 **설정을**합니다.
   <br><br>
   ![사용자 위험 정책](./media/active-directory-identityprotection-notifications/401.png "사용자 위험 정책")
   <br>
2. Hello에 **일반** 섹션에서 클릭 **알림**합니다.
   <br><br>
   ![사용자 위험 정책](./media/active-directory-identityprotection-notifications/405.png "사용자 위험 정책")
   <br>

## <a name="see-also"></a>참고 항목
* [Azure Active Directory ID 보호](active-directory-identityprotection.md)
