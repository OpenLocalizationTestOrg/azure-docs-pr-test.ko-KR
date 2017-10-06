---
title: "그룹에 대 한 동적 멤버 자격 aaaTroubleshooting | Microsoft Docs"
description: "Azure AD의 그룹에 대한 동적 멤버 자격 문제 해결 팁입니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a>그룹의 동적 멤버 자격 문제 해결
**그룹에 대 한 규칙을 구성 하지만 hello 그룹에 없는 멤버 자격 업데이트**<br/>해당 hello 확인 **위임 된 그룹 관리 사용** 너무 설정은**예** hello에 **구성** 탭 합니다. 이 설정은 사용자 toowhom Azure Active Directory Premium 라이선스가 할당 될 때 로그인 한 경우에 표시 됩니다. Hello 규칙의 사용자 특성에 대 한 hello 값 확인: hello 규칙을 만족 하는 사용자가 있습니까?

**한 규칙을 구성 하지만 hello hello 규칙의 기존 구성원 제거**<br/>이는 정상적인 동작입니다. 규칙을 사용 하도록 설정 하거나 변경할 hello 그룹의 기존 구성원 제거 됩니다. hello 규칙의 평가에서 반환 된 hello 사용자 toohello 그룹 구성원으로 추가 됩니다.     

**규칙을 추가하거나 변경하는 즉시 멤버 자격 변경 내용이 표시되지 않는 이유는?**<br/>위임된 구성원은 비동기식 백그라운드 프로세스에서 주기적으로 평가되기 때문입니다. 시간 hello 프로세스는 hello 사용자 수에 hello 규칙의 결과로 만들어진 hello 그룹의 디렉터리 및 hello 크기에 따라 결정 됩니다. 일반적으로 적은 수의 사용자를 디렉터리 보다 작은 잠시 후에 hello 그룹 구성원 자격 변경 사항을 표시 됩니다. 많은 수의 사용자를 사용 하 여 디렉터리는 30 분 또는 toopopulate 더 오래 걸릴 수 있습니다.

### <a name="next-steps"></a>다음 단계
이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.

* [Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리](active-directory-manage-groups.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [Azure Active Directory란?](active-directory-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
