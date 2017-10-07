---
title: "Azure Active Directory의 조건부 액세스 시작 aaaGet | Microsoft Docs"
description: "위치 조건을 사용하여 조건부 액세스를 테스트합니다."
services: active-directory
keywords: "조건부 액세스 tooapps, Azure AD 사용 하 여 조건부 액세스 조건부 액세스 정책 toocompany 리소스 액세스 보안"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a>Azure Active Directory에서 조건부 액세스 시작

조건부 액세스는 하면 toodefine 조건 권한이 있는 사용자는 앱에 액세스할 수 있도록 Azure Active Directory의 기능입니다. 

이 항목에서는 사용자 환경의 위치 조건에 따라 조건부 액세스를 테스트하기 위한 지침을 제공합니다.  


## <a name="scenario-description"></a>시나리오 설명

많은 조직에서 일반적인 요구 사항 하나는 tooonly hello 회사 인트라넷에서 수행 되지 않는 액세스 tooapps에 대 한 multi-factor authentication을 요구 합니다. Azure Active Directory를 사용하면 위치 기반 조건부 액세스 정책을 구성하여 이 목표를 쉽게 달성할 수 있습니다. 여기서는 관련 정책 구성에 대한 자세한 지침을 제공합니다. 정책을 이용 하 여 hello [신뢰할 수 있는 Ip](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) hello 회사에서 만든 액세스 시도 간에 toodistinguish 인트라넷 및 다른 모든 위치로 합니다.


## <a name="prerequisites"></a>필수 조건

hello이 항목에 설명 된 시나리오에서는 가정에 설명 된 hello 개념에 익숙한 [Azure Active Directory의 조건부 액세스](active-directory-conditional-access-azure-portal.md)합니다.

tootest이이 시나리오를 해야 합니다.

- 테스트 사용자 만들기 

- 할당 된 Azure AD Premium 라이선스 toohello 테스트 사용자

- 관리 되는 앱을 구성 하 고 테스트 사용자 tooit를 할당 합니다.

- 신뢰할 수 있는 IP 구성

신뢰할 수 있는 IP에 대한 자세한 내용은 [신뢰할 수 있는 IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)를 참조하세요.


## <a name="policy-configuration-steps"></a>정책 구성 단계

**tooconfigure 조건부 액세스 정책에 수행:**

1. Hello hello 왼쪽된 탐색 모음에서 Azure 포털에서에서 클릭 **Azure Active Directory**합니다. 

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. Hello에 **Azure Active Directory** 블레이드 hello **관리** 섹션에서 클릭 **조건부 액세스**합니다.

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. Hello에 **조건부 액세스** 블레이드, tooopen hello **새로** 블레이드 hello 바탕 화면에서 hello 도구 모음에서 클릭 **추가**합니다.

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. Hello에 **새로** 블레이드 hello **이름** 텍스트 상자 정책의 이름 입력 합니다.

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. Hello에 **할당** 섹션에서 클릭 **사용자 및 그룹**합니다.

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. Hello에 **사용자 및 그룹** 블레이드에서 hello 다음 단계를 수행 합니다.

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    a. **사용자 및 그룹 선택**을 클릭합니다.

    b. **선택**을 클릭합니다.

    c. Hello에 **선택** 블레이드에서 테스트 사용자를 선택한 다음 클릭 **선택**합니다.

    d. Hello에 **사용자 및 그룹** 블레이드에서 클릭 **수행**합니다.

7. Hello에 **새로** 블레이드, tooopen hello **클라우드 앱** 블레이드 hello **할당** 섹션에서 클릭 **클라우드 앱**합니다.

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. Hello에 **클라우드 앱** 블레이드에서 hello 다음 단계를 수행 합니다.

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    a. **앱 선택**을 클릭합니다.

    b. **선택**을 클릭합니다.

    c. Hello에 **선택** 블레이드에서 클라우드 응용 프로그램을 선택한 다음 클릭 **선택**합니다.

    d. Hello에 **클라우드 앱** 블레이드에서 클릭 **수행**합니다.

9. Hello에 **새로** 블레이드, tooopen hello **조건** 블레이드 hello **할당** 섹션에서 클릭 **조건**합니다.

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. Hello에 **조건** 블레이드, tooopen hello **위치** 블레이드에서 클릭 **위치**합니다.

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. Hello에 **위치** 블레이드에서 hello 다음 단계를 수행 합니다.

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    a. **구성** 아래에서 **예**를 클릭합니다.

    b. **포함**에서 **모든 위치**를 클릭합니다.

    c. **제외**를 클릭한 다음 **모든 신뢰할 수 있는 IP**를 클릭합니다.

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    ㄹ. **Done**을 클릭합니다.

12. Hello에 **조건** 블레이드에서 클릭 **수행**합니다.

13. Hello에 **새로** 블레이드, tooopen hello **Grant** 블레이드 hello **컨트롤** 섹션에서 클릭 **Grant**합니다.

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. Hello에 **Grant** 블레이드에서 hello 다음 단계를 수행 합니다.

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    a. **다단계 인증 필요**를 선택합니다.

    b. **선택**을 클릭합니다.

15. Hello에 **새로** 블레이드 아래 **정책 사용**, 클릭 **에**합니다.

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. Hello에 **새로** 블레이드에서 클릭 **만들기**합니다.


## <a name="testing-hello-policy"></a>Hello 정책 테스트

tootest 정책에 장치에서 앱에 액세스 해야 하는: 

1. 구성된 신뢰할 수 있는 IP에 속한 IP 주소가 있는 장치 

1. 구성된 신뢰할 수 있는 IP에 속하지 않은 IP 주소가 있는 장치

다단계 인증은 구성된 신뢰할 수 있는 IP에 속하지 않은 장치에서 수행되는 연결 시도에서만 필요합니다. 


## <a name="next-steps"></a>다음 단계

조건부 액세스에 대 한 자세한 toolearn 싶으시면 참조 [Azure Active Directory의 조건부 액세스](active-directory-conditional-access-azure-portal.md)합니다.

