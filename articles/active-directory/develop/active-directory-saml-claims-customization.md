---
title: "Azure Active Directory에 사전 통합된 앱에 대 한 hello SAML 토큰에서 발급 된 aaaCustomizing 클레임 | Microsoft Docs"
description: "Toocustomize hello 클레임 발급 방식 hello에 Azure Active Directory에 사전 통합된 앱에 대 한 SAML 토큰에 알아봅니다"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f1daad62-ac8a-44cd-ac76-e97455e47803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.custom: aaddev
ms.openlocfilehash: a376318929472403e799f02fdd3fbddc91d0a70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-claims-issued-in-hello-saml-token-for-pre-integrated-apps-in-azure-active-directory"></a>Azure Active Directory에 사전 통합된 앱에 대 한 SAML 토큰 hello에 발급 클레임 사용자 지정
Azure Active Directory hello single sign-on 지원 360 보다를 포함 하 여 Azure AD 응용 프로그램 갤러리에서에서 수천 개의 미리 통합 된 응용 프로그램을 지 원하는 오늘 hello SAML 2.0 프로토콜을 사용 합니다. 사용자가 SAML을 사용 하 여 Azure AD 통해 tooan 응용 프로그램에 인증 하는 경우 Azure AD는 토큰 toohello 응용 프로그램을 (HTTP POST)를 통해 보냅니다. 및 그런 다음 hello 응용 프로그램의 유효성을 검사 하 고 사용자 이름 및 암호에 대 한 메시지를 표시 하는 대신에 hello 토큰 toolog hello 사용자를 사용 합니다. 이 SAML 토큰 "클레임" 이라고 하는 hello 사용자에 대 한 정보를 포함 합니다.

id 관점, "클레임"은 해당 사용자에 대해 발급 하는 hello 토큰 내에서 사용자에 대 한 id 공급자를 나타내는 정보입니다. [SAML 토큰](http://en.wikipedia.org/wiki/SAML_2.0),이 데이터는 일반적으로 SAML 특성 설명을 hello에 포함 됩니다. hello 사용자의 고유 ID는 일반적으로 표현 SAML 주체 이름을 식별자로 라고도 하는 hello에.

기본적으로 Azure Active Directory는 NameIdentifier 클레임 값이 Azure AD에서 hello 사용자의 사용자 이름 (즉, 사용자 계정 이름)을 포함 하는 SAML 토큰 tooyour 응용 프로그램을 실행 합니다. 이 값 hello 사용자를 식별할 수 있습니다. 또한 hello SAML 토큰 hello 사용자의 전자 메일 주소, 이름 및 성을 포함 하는 추가 클레임을 포함 합니다.

tooview 또는 편집 hello 클레임 SAML 토큰 toohello 응용 프로그램을 Azure 포털에서 열기 hello 응용 프로그램 hello에서 실행 됩니다. Hello 선택 **보기 및 다른 모든 사용자 특성을 편집** hello 확인란을 선택 **사용자 특성** hello 응용 프로그램의 섹션입니다.

![사용자 특성 섹션][1]

두 가지 가능한 원인은 hello SAML 토큰에서 발급 된 tooedit hello 클레임 할 수 있습니다.
* hello 응용 프로그램을 다른 클레임 Uri의 설정 또는 클레임 값 toorequire를 작성 되었습니다.
* hello 응용 프로그램 hello NameIdentifier 클레임 toobe 이외의 hello 사용자 이름 (즉, 사용자 계정 이름) Azure Active Directory에 저장 해야 하는 방식으로 배포 되었습니다.

Hello 기본 클레임 값을 편집할 수 있습니다. Hello SAML 토큰 특성 테이블의 hello 클레임 행을 선택 합니다. Hello 열립니다 **특성 편집** 클레임 이름, 값 및 hello 클레임과 연결 된 네임 스페이스 섹션 및 다음 편집할 수 있습니다.

![사용자 특성 편집][2]

Hello를 클릭 하 여 열 수 있는 hello 상황에 맞는 메뉴를 사용 하 여 (제외 NameIdentifier) 클레임을 제거할 수도 있습니다 **...**  아이콘입니다.  Hello를 사용 하 여 새 클레임을 추가할 수도 있습니다 **특성 추가** 단추입니다.

![사용자 특성 편집][3]

## <a name="editing-hello-nameidentifier-claim"></a>Hello NameIdentifier 클레임 편집
hello toosolve hello 문제 hello 응용 프로그램을 배포한 다른 사용자 이름을 사용 하 여 클릭 **사용자 식별자** hello에서 드롭 다운 **사용자 특성** 섹션. 이 작업을 수행하면 몇 가지 옵션이 있는 대화 상자가 제공됩니다.

![사용자 특성 편집][4]

Hello 드롭다운 목록에서에서 선택 **user.mail** tooset hello NameIdentifier 클레임 hello 디렉터리에 toobe hello 사용자의 전자 메일 주소입니다. 선택 또는 **user.onpremisessamaccountname** tooset toohello 사용자 SAM 계정 이름에서 동기화 된 온-프레미스 Azure AD.

특별 한 hello를 사용할 수도 있습니다 **ExtractMailPrefix()** hello 전자 메일 주소, SAM 계정 이름 또는 hello 사용자 계정 이름에서 함수 tooremove hello 도메인 접미사입니다. 통해 전달 되는 hello hello 사용자의 첫 번째 부분 이름을 추출 (예를 들어 "joe_smith" 대신 joe_smith@contoso.com).

![사용자 특성 편집][5]

Hello 또한 추가 이제 **join ()** 함수 toojoin hello hello 사용자 식별자 값을 사용 하 여 도메인을 확인 합니다. hello에 hello join () 함수를 선택 하면 **사용자 식별자** 첫 번째 select와 같은 전자 메일 주소 또는 사용자 계정 이름으로 사용자의 id를 hello 및 hello 두 번째 드롭다운 목록에서 확인 된 도메인을 선택 합니다. Hello 확인 된 도메인과 hello 전자 메일 주소를 선택한 다음 Azure AD에서 첫 번째 값 joe_smith hello에서에서 hello username 추출 joe_smith@contoso.com contoso.onmicrosoft.com에 추가 합니다. 다음 예제는 hello를 참조 하십시오.

![사용자 특성 편집][6]

## <a name="adding-claims"></a>클레임 추가
클레임을 추가할 때는 hello 특성 이름 (toofollow hello SAML 사양에 따라 URI 패턴을 필요 하지 않은 엄격 하 게)를 지정할 수 있습니다. Hello 디렉터리에 저장 된 hello 값 tooany 사용자 특성을 설정 합니다.

![사용자 특성 추가][7]

예를 들어 toosend 해야 사용자 hello hello 부서 속한 tooin 조직 (예: 판매)을 클레임으로 합니다. Hello 응용 프로그램에서 예상 대로 hello 클레임 이름을 입력 한 다음 선택 **user.department** hello 값으로.

> [!NOTE]
> 지정된 된 사용자에 대 한 선택한 특성에 대해 저장 된 값이 없는, hello 토큰에서 해당 클레임이 발급 되 고 됩니다.

> [!TIP]
> hello **user.onpremisesecurityidentifier** 및 **user.onpremisesamaccountname** 때 사용자 데이터를 동기화 온-프레미스 Active Directory hello를 사용 하 여만 지원 됩니다 [Azure AD Connect 도구](../active-directory-aadconnect.md)합니다.

## <a name="restricted-claims"></a>제한된 클레임

SAML에는 몇 가지 제한된 클레임이 있습니다. 이러한 클레임을 추가하면 Azure AD는 이러한 클레임을 보내지 않습니다. 다음은 hello SAML 클레임 집합을 제한 합니다.

    | 클레임 형식(URI) |
    | ------------------- |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/expired |
    | http://schemas.microsoft.com/identity/claims/accesstoken |
    | http://schemas.microsoft.com/identity/claims/openid2_id |
    | http://schemas.microsoft.com/identity/claims/identityprovider |
    | http://schemas.microsoft.com/identity/claims/objectidentifier |
    | http://schemas.microsoft.com/identity/claims/puid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1] |
    | http://schemas.microsoft.com/identity/claims/tenantid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod |
    | http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/groups |
    | http://schemas.microsoft.com/claims/groups.link |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/role |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/wids |
    | http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant |
    | http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown |
    | http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged |
    | http://schemas.microsoft.com/2014/03/psso |
    | http://schemas.microsoft.com/claims/authnmethodsreferences |
    | http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier |
    | http://schemas.microsoft.com/identity/claims/scope |

## <a name="next-steps"></a>다음 단계
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](../active-directory-apps-index.md)
* [Single sign on tooapplications hello Azure Active Directory 응용 프로그램 갤러리에 없는 구성](../active-directory-saas-custom-apps.md)
* [SAML 기반 Single Sign-On 문제 해결](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saml-claims-customization/user-attribute-section.png
[2]: ./media/active-directory-saml-claims-customization/edit-claim-name-value.png
[3]: ./media/active-directory-saml-claims-customization/delete-claim.png
[4]: ./media/active-directory-saml-claims-customization/user-identifier.png
[5]: ./media/active-directory-saml-claims-customization/extractemailprefix-function.png
[6]: ./media/active-directory-saml-claims-customization/join-function.png
[7]: ./media/active-directory-saml-claims-customization/add-attribute.png