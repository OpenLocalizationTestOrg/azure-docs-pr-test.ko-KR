---
title: "Multi-factor Authentication-aaaAzure 작동 방법"
description: "Azure Multi-factor Authentication 간단한 로그인 프로세스에 대 한 사용자 요구를 충족 하면서 보호 액세스 toodata 및 응용 프로그램을 지원 합니다. 두 번째 형식의 인증을 요구하여 추가 보안을 제공하고 다양한 쉬운 확인 옵션을 통해 강력한 인증을 제공합니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a>Azure Multi-Factor Authentication 작동 방법
2 단계 인증의 hello 보안은 계층형된 방식을 있다는 점입니다. 다단계 인증 요소를 손상시키는 일은 공격자에게 매우 어렵습니다. 공격자가 toolearn hello 사용자의 암호를 관리 하는 경우에 것은 의미가 없습니다 hello 신뢰할 수 있는 장치를 확보 하지 않고 있습니다. 

![검사](./media/multi-factor-authentication-how-it-works/howitworks.png)

Azure Multi-factor Authentication 간단한 로그인 프로세스에 대 한 사용자 요구를 충족 하면서 보호 액세스 toodata 및 응용 프로그램을 지원 합니다.  두 번째 형식의 인증을 요구하여 추가 보안을 제공하고 다양한 쉬운 확인 옵션을 통해 강력한 인증을 제공합니다.


## <a name="methods-available-for-two-step-verification"></a>2단계 인증을 위한 방법
사용자가 로그인 할 때 추가 확인 toohello 사용자를 전송 됩니다.  hello 다음은이 두 번째 확인에 사용할 수 있는 메서드의 목록입니다.

| 확인 방법 | 설명 |
| --- | --- |
| 전화 통화 |호출은 tooa 사용자의 등록 된 전화 번호에 배치 됩니다. hello 사용자 필요한 경우 PIN을 입력 한 다음 hello # 키를 누를 합니다. |
| 문자 메시지 |문자 메시지 tooa 사용자의 휴대폰 6 자리 코드가 전송 됩니다. hello 사용자 hello 로그인 페이지에서이 코드를 입력합니다. |
| 모바일 앱 알림 |확인 요청 tooa 사용자의 스마트폰을 전송 됩니다. hello 사용자 필요한 경우 PIN을 입력 한 다음 선택 **확인** hello 모바일 앱에 있습니다. |
| 모바일 앱 확인 코드 |사용자의 스마트 폰에서 실행 되는 모바일 앱, hello 30 초 간격으로 변경 하는 확인 코드를 표시 합니다. hello 사용자 hello 가장 최근 코드를 찾아 hello 로그인 페이지에 입력 합니다. |
| 타사 OATH 토큰 | Azure Multi-factor Authentication 서버에 구성 된 tooaccept 제 3 자 확인 방법을 수 있습니다. |

Azure Multi-Factor Authentication은 클라우드와 서버 모두에 대해 선택 가능한 확인 방법을 제공합니다. 전화 통화, 텍스트, 앱 알림, 앱 코드 중에서 사용자에게 제공할 방법을 선택할 수 있습니다. 자세한 내용은 [선택 가능한 확인 방법](multi-factor-authentication-whats-next.md#selectable-verification-methods)을 참조하세요.

## <a name="next-steps"></a>다음 단계

- 다른 hello에 대 한 읽기 [버전 및 Azure Multi-factor Authentication에 대 한 소비 메서드](multi-factor-authentication-versions-plans.md)

- 선택 여부 toodeploy Azure MFA [hello 클라우드 또는 온-프레미스](multi-factor-authentication-get-started.md)

- [자주 묻는 질문](multi-factor-authentication-faq.md)에 대한 답변을 읽어봅니다.