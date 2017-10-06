---
title: "Azure AD Connect 동기화: hello AD DS 계정 암호를 변경할 | Microsoft Docs"
description: "이 항목 문서 tooupdate hello 계정의 암호를 AD DS hello 후 Azure AD Connect가 변경 하는 방법을 설명 합니다."
services: active-directory
keywords: "AD DS 계정, Active Directory 계정, 암호"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a>Hello AD DS 계정 암호 변경
hello AD DS 계정 toohello 사용자 계정을 온-프레미스 Active Directory와 Azure AD Connect toocommunicate에서 사용 하는 참조 합니다. AD DS 계정 hello hello 암호를 변경 하는 경우 Azure AD Connect 동기화 Service hello 새 암호로 업데이트 해야 합니다. 그렇지 않으면 hello 동기화 더 이상 동기화 할 수 올바르게 hello로 온-프레미스 Active Directory 및 hello 다음 오류를 발생 합니다.

* Hello에 동기화 서비스 관리자, 가져오기 또는 내보내기 작업을 온-프레미스 AD 실패 하 고 **자격 증명 없음-시작** 오류입니다.

* Hello 응용 프로그램 이벤트 로그에서 Windows 이벤트 뷰어 오류가 포함 되어 **이벤트 ID 6000** 및 메시지 **'hello 관리 에이전트 "contoso.com" 이므로 실패 toorun hello 자격 증명이 잘못 되었습니다.'** .


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a>AD DS 계정에 대 한 새 암호로 tooupdate 동기화 서비스 hello 하는 방법
hello 새 암호로 tooupdate hello 동기화 서비스:

1. Hello 동기화 서비스 관리자 (→ 시작 동기화 서비스)를 시작 합니다.
</br>![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  

2. Toohello 이동 **커넥터** 탭 합니다.

3. 선택 hello **AD 커넥터** 해당 암호가 변경 된 것 toohello AD DS 계정에 해당 합니다.

4. **작업** 아래에서 **속성**을 선택합니다.

5. Hello 팝업 대화 상자에서 선택 **tooActive Directory 포리스트에 연결**:

6. Hello에 hello hello AD DS 계정의 새 암호를 입력 **암호** 텍스트 상자에 붙여넣습니다.

7. 클릭 **확인** toosave hello 새 암호와 닫기 hello 팝업 대화 상자.

8. Azure AD Connect 동기화 Service Windows 서비스 제어 관리자에서 hello 하는 다시 시작 합니다. 이 tooensure 모든 참조 toohello 이전 암호 hello 메모리 내 캐시에서 제거 된 합니다.

## <a name="next-steps"></a>다음 단계
**개요 항목**

* [Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정](active-directory-aadconnectsync-whatis.md)

* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
