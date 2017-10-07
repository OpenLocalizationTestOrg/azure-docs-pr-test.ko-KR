---
title: "Azure AD Identity Protection 사용한 aaaSign에서 경험 | Microsoft Docs"
description: "Id 보호 된 완화 있거나 사용자 또는 정책에 의해 multi-factor authentication 인증이 필요한 경우 재구성 hello 사용자 경험에 대 한 개요를 제공 합니다."
services: active-directory
keywords: "Azure Active Directory ID 보호, 클라우드 앱 검색, 응용 프로그램 관리, 보안, 위험, 위험 수준, 취약점, 보안 정책"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a>Azure AD ID 보호를 사용하는 로그인 환경
Azure Active Directory ID 보호를 사용하여 다음을 수행할 수 있습니다.

* multi-factor authentication 사용자가 tooregister 필요
* 위험한 로그인 및 손상된 사용자 처리

hello 시스템 toothese 문제의 hello 응답 방금 직접 로그인 사용자 이름과 암호를 제공 하 여 수 없기 때문에 가능한 더 이상 사용자의 로그인 환경에 영향을 미칩니다. 추가 단계는 필요한 tooget 안전 하 게 비즈니스 사용자에 스풀링됩니다.

이 항목에서는 발생할 수 있는 모든 경우의 사용자 로그인 환경에 대한 개요를 제공합니다.

**Multi-Factor Authentication**

* Multi-Factor Authentication 등록

**위험한 로그인**

* 위험한 로그인 복구
* 위험한 로그인 차단됨
* 위험한 로그인 시 Multi-Factor Authentication 등록

**위험한 사용자**

* 손상된 계정 복구
* 손상된 계정 차단됨

## <a name="multi-factor-authentication-registration"></a>Multi-Factor Authentication 등록
모두에 대 한 최상의 사용자 환경을 hello, 손상 된 계정 복구 흐름 hello 및 위험한 로그인 흐름 hello 때 hello 사용자 자체 복구할 수 있습니다. 사용자가 multi-factor authentication 등록을 하는 경우 보안 문제를 사용 하는 toopass 일 수 있는 자신의 계정과 연결 된 전화 번호를이 이미 있습니다. 도움말 센터 또는 관리자 관여 하지 않습니다는 필요한 toorecover 계정 손상 되지 않도록에서 합니다. 따라서 것이 좋습니다 tooget 사용자가 multi-factor authentication에 등록 합니다. 

관리자는 다음을 수행할 수 있습니다.

* 추가 보안 확인에 대 한 자신의 계정을 tooset 사용자가 요구 하는 정책을 설정 합니다. 
* toogive 사용자가 원하는 경우 건너뛴 too30 일 구성에 대 한 다단계 인증 등록 허용을 등록 하기 전에 유예 기간이 있습니다.

**hello 다단계 인증 등록에는 세 가지 단계가 있습니다.**

1. 첫 번째 단계는 hello hello 사용자는 multi-factor authentication에 hello 요구 사항 tooset hello 계정에 대 한 알림을 가져옵니다. 
   
    ![수정](./media/active-directory-identityprotection-flows/140.png "수정")
2. toolet hello 시스템이 필요를 tooset multi-factor authentication을 확인 하려는 toobe 연결 합니다.
   
    ![수정](./media/active-directory-identityprotection-flows/141.png "수정")
3. hello 시스템 챌린지 tooyou을 제출 하 고 toorespond 필요 합니다.
   
    ![수정](./media/active-directory-identityprotection-flows/142.png "수정")

## <a name="risky-sign-in-recovery"></a>위험한 로그인 복구
에 관리자가 로그인 위험에 대 한 정책을 구성한 경우에 toosign 하려고 할 때 hello 영향을 받는 사용자 알림이 표시 됩니다. 

**hello 위험한 로그인 흐름에 두 개의 단계가 있습니다.** 

1. hello 사용자는 로그인을 새 위치, 장치 또는 앱에서 로그인 등에 대 한 검색 되었습니다 특이 한 활동이 알림을 받습니다. 
   
    ![수정](./media/active-directory-identityprotection-flows/120.png "수정")
2. hello 사용자가 필요한 tooprove 신원을 보안 과제를 해결 합니다. Hello 사용자가 multi-factor authentication에 등록 하는 경우 tooround-여행 보안 코드 tootheir 전화 번호를 해야 합니다. Just 이므로 위험한 로그인 및 손상 된 계정이 아닌 hello 사용자는이 흐름에서 toochange hello 암호 없습니다. 
   
    ![수정](./media/active-directory-identityprotection-flows/121.png "수정")

## <a name="risky-sign-in-blocked"></a>위험한 로그인 차단됨
관리자가 tooset hello 위험 수준에 따라 로그인 시 로그인 위험 정책 tooblock 사용자 선택할 수도 있습니다. tooget 차단 해제 됨, 최종 사용자에 게 문의 해야 관리자나 지원 센터 또는 친숙 한 위치 또는 장치에서 로그인을 시도할 수 있습니다. 다단계 인증을 해결하는 자체 복구는 이 경우에 불가능합니다.

![수정](./media/active-directory-identityprotection-flows/200.png "수정")

## <a name="compromised-account-recovery"></a>손상된 계정 복구
사용자에 게 특히 hello 사용자 위험 hello 정책에 지정 된 수준을 사용자 위험 보안 정책 구성 된 경우 (따라서 이라고 가정 손상)은에 로그인 하기 전에 hello 사용자 손상 복구 흐름을 통해 이동 해야 합니다. 

**hello 사용자 손상 복구 흐름에는 세 가지 단계가 포함 됩니다.**

1. hello 사용자는 자신의 계정 보안 위험에는 의심 스러운 활동 때문 또는 자격 증명을 유출 알림을 받습니다.
   
    ![수정](./media/active-directory-identityprotection-flows/101.png "수정")
2. hello 사용자가 필요한 tooprove 신원을 보안 과제를 해결 합니다. Hello 사용자가 multi-factor authentication에 등록 하는 경우에 손상 되지 않도록 자체 복구할 수 있습니다. 이들은 tooround-여행 보안 코드 tootheir 전화 번호가 있어야 합니다. 
   
   ![수정](./media/active-directory-identityprotection-flows/110.png "수정")
3. 마지막으로, 사용자를 hello 이후 액세스 tootheir 계정이 있을 수 있으며 다른 사용자가 암호 강제 toochange가 있습니다. 
   이러한 환경의 스크린 샷은 다음과 같습니다.
   
   ![수정](./media/active-directory-identityprotection-flows/111.png "수정")

## <a name="compromised-account-blocked"></a>손상된 계정 차단됨
차단 해제 됨 사용자 위험 보안 정책에 의해 차단 된 사용자 tooget hello 사용자는 관리자나 기술 지원 서비스로 문의 해야 합니다. 다단계 인증을 해결하는 자체 복구는 이 경우에 불가능합니다.

![수정](./media/active-directory-identityprotection-flows/104.png "수정")

## <a name="reset-password"></a>암호 재설정
손상된 사용자가 로그인할 수 없으면 관리자가 해당 사용자에게 임시 암호를 생성할 수 있습니다. hello 사용자는 다음에 로그인 하는 동안 toochange 자신의 암호를 갖게 됩니다.

![수정](./media/active-directory-identityprotection-flows/160.png "수정")

## <a name="see-also"></a>참고 항목
* [Azure Active Directory ID 보호](active-directory-identityprotection.md) 

