---
title: "Azure Active Directory에서 aaaNamed 위치 | Microsoft Docs"
description: "지정 된 위치를 구성 하지 않아도 IP 주소는 조직에서 소유 하는 hello 이동 불가능 tooatypical 위치 위험 이벤트 유형에 대 한 거짓 긍정을 생성 합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a>Azure Active Directory의 명명된 위치

Azure Active Directory의 위치 기능 라는 hello, 조직에서 신뢰할 수 있는 IP 주소 범위를 레이블을 지정할 수 있습니다. 사용자 환경에서의 hello 검색의 hello 컨텍스트에서 명명 된 위치를 사용할 수 있습니다 [이벤트 위험](active-directory-reporting-risk-events.md)합니다. hello 기능은 hello hello에 대 한 보고 된 거짓 긍정 수를 줄일 *이동 불가능 tooatypical 위치* 위험 이벤트 유형입니다. 

## <a name="configuration"></a>구성

tooconfigure 명명된 된 위치:

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 전역 관리자로 합니다.

2. Hello 왼쪽된 창에서 클릭 **Azure Active Directory**합니다.

    ![hello 왼쪽된 창에서 hello Azure Active Directory 링크](./media/active-directory-named-locations/01.png)

3. Hello에 **Azure Active Directory** 블레이드 hello **보안** 섹션에서 클릭 **조건부 액세스**합니다.

    ![hello 조건부 액세스 명령](./media/active-directory-named-locations/05.png)


4. Hello에 **조건부 액세스** 블레이드 hello **관리** 섹션에서 클릭 **명명 된 위치**합니다.

    ![명명 된 위치 명령 hello](./media/active-directory-named-locations/06.png)


5. Hello에 **명명 된 위치를** 블레이드에서 클릭 **새 위치로**합니다.

    ![hello 새 위치 명령](./media/active-directory-named-locations/07.png)


6. Hello에 **새로** 블레이드에서 다음 hello지 않습니다.

    ![hello 새 블레이드](./media/active-directory-named-locations/08.png)

    a. Hello에 **이름** 명명 된 위치에 대 한 이름을 입력 합니다.

    b. Hello에 **IP 범위** IP 범위를 입력 합니다. hello IP 범위 toobe hello에 필요한 *Classless Inter-domain Routing* (CIDR) 형식입니다.  

    c. **만들기**를 클릭합니다.



## <a name="what-you-should-know"></a>알아야 할 사항

**대량 업데이트**: 작성 하거나 대량 업데이트에 대 한 명명 된 위치를 업데이트할 때이 업로드 하거나 hello IP 범위와 관련 된 CSV 파일 다운로드 수 있습니다. 업로드는 hello 목록을 덮어쓰는 대신 hello 파일 toohello 목록에 hello IP 범위를 추가 합니다.

![hello 업로드 및 다운로드 링크](./media/active-directory-named-locations/09.png)


**제한 사항**: 그 중 하나의 IP 할당 범위 tooeach와 최대 60 명명 된 위치를 정의할 수 있습니다. 구성 된 하나의 명명 된 위치를 설정한 경우에 대 한 too500 IP 범위를 정의할 수 있습니다.


## <a name="next-steps"></a>다음 단계

위험 이벤트에 대해 자세히 toolearn 참조 [Azure Active Directory 위험 이벤트](active-directory-reporting-risk-events.md)합니다.

