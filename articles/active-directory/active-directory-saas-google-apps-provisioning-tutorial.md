---
title: "Tutorial: Azure에서 자동 사용자 프로비전에 대한 Google Apps 구성 | Microsoft Docs"
description: "Azure AD tooGoogle 앱에서에서 tooautomatically 프로 비전 및 프로 비전 해제 사용자 계정을 하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a>자습서: 자동 사용자 프로비전에 대한 Google Apps 구성

hello이이 자습서의 단계 tooperform Google Apps와 Azure AD tooautomatically 프로 비전에 필요 하 고 Azure AD tooGoogle 앱에서에서 사용자 계정을 프로 비전 해제할 hello tooshow가 합니다.

## <a name="prerequisites"></a>필수 조건

이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

*   Azure Active Directory 테넌트.
*   Google Apps for Work 또는 Google Apps for Education에 유효한 테넌트가 있어야 합니다. 어느 서비스에나 평가판 계정을 사용할 수 있습니다.
*   팀 관리자 권한이 있는 Google Apps의 사용자 계정

## <a name="assigning-users-toogoogle-apps"></a>TooGoogle 응용 프로그램 사용자를 할당합니다.

Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다. 자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다.

하기 전에 구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 해야 toodecide 어떤 사용자 및/또는 Azure AD의 그룹을 tooyour Google Apps 응용 프로그램에 액세스 해야 하는 hello 사용자를 나타냅니다. 여기 hello 지침에 따라 이러한 사용자 tooyour Google Apps 응용 프로그램을 결정 한 후에 할당할 수 있습니다: [사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

> [!IMPORTANT]
>*   것이 좋습니다는 단일 Azure AD 사용자 프로 비전 구성 tooGoogle 앱 tootest hello를 할당할 수 있습니다. 추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.
>*   사용자 tooGoogle 앱에 할당할 때는 hello 할당 대화 상자에서 hello 사용자 또는 역할 "그룹"를 선택 해야 합니다. hello "기본 액세스" 역할 프로 비전 하기 위한 작동 하지 않습니다.

## <a name="enable-automated-user-provisioning"></a>자동 사용자 프로비전 사용

이 섹션 API를 프로 비전 해당 Azure AD tooGoogle 앱의 사용자 계정을 연결 하는 방법을 안내 하 고 업데이트 hello 서비스 toocreate 프로 비전, 구성 및 Azure AD에서 사용자 및 그룹 할당을 기준으로 Google Apps에 할당 된 사용자 계정 사용 안 함 .

>[!Tip]
>Hello 지침에 제공 된 Google Apps에 대 한 SAML 기반 Single Sign-on tooenabled 선택할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다. Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.

### <a name="configure-automatic-user-account-provisioning"></a>자동 사용자 계정 프로비전 구성

> [!NOTE]
> 사용자 tooGoogle 앱 프로 비전을 자동화 하기 위한 또 다른 실행 가능한 옵션은 toouse [Google 앱 디렉터리 동기화 (GADS)](https://support.google.com/a/answer/106368?hl=en) 온-프레미스 Active Directory identities tooGoogle 앱 프로 비전입니다. 반면,이 자습서의 hello 솔루션에는 Azure Active Directory (클라우드) 사용자 및 메일 사용이 가능한 그룹 tooGoogle 앱 프로 비전합니다. 

1. Hello에 로그인 [Google 앱 관리 콘솔](http://admin.google.com/) 프로그램 관리자 계정을 사용 하 고 클릭 **보안**합니다. Hello 링크 보이지 않으면 hello 아래 숨겨질 수 있습니다 **기타 컨트롤** hello hello 화면 맨 아래에 메뉴입니다.
   
    ![보안을 클릭합니다.][10]

2. Hello에 **보안** 페이지 **API 참조**합니다.
   
    ![API 참조를 클릭합니다.][15]

3. **API 액세스 사용**을 선택합니다.
   
    ![API 참조를 클릭합니다.][16]

    > [!IMPORTANT]
    > 응용 프로그램을 Azure Active Directory에서 자신의 사용자 이름 tooprovision tooGoogle 하려는 모든 사용자에 대해 *해야* 동률된 tooa 사용자 지정 도메인 이어야 합니다. 예를 들면 bob@contoso.onmicrosoft.com과 같은 사용자 이름은 Google Apps에서 허용되지 않지만 bob@contoso.com은 허용됩니다. Azure AD에서 해당 속성을 편집하여 기존 사용자의 도메인을 변경할 수 있습니다. 지침에 다음 단계 tooset Azure Active Directory와 Google Apps에 대 한 사용자 지정 도메인은 포함 하는 방법에 대 한 합니다.
      
4. 사용자 지정 도메인 이름을 tooyour Azure Active Directory를 아직 추가 하지 않았다면, 다음 단계를 수행 하는 hello를 따르십시오.
  
    a. Hello에 [Azure 포털](https://portal.azure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다. Hello 디렉터리 목록에 디렉터리를 선택 합니다. 

    b. 클릭 **도메인 이름** 왼쪽된 탐색 창의 hello 되 고 클릭 **추가**합니다.
     
     ![도메인](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![도메인 추가](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    c. Hello에 도메인 이름을 입력 **도메인 이름** 필드입니다. 이 도메인 이름은 hello 해야 합니다. Google Apps toouse 만들려는 경우 같은 도메인 이름입니다. 준비가 되 면 클릭 hello **도메인 추가** 단추입니다.
     
     ![도메인 이름](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    d. 클릭 **다음** toogo toohello 확인 페이지. 이 도메인을 소유 하는 tooverify,이 페이지에 제공 된 toohello 값에 따라 hello 도메인의 DNS 레코드를 편집 해야 합니다. Tooverify 중 하나를 사용 하 여 선택할 수 있으며 **MX 레코드** 또는 **TXT 레코드**hello에 대 한 선택에 따라 **레코드 종류** 옵션입니다. 에 대 한 보다 포괄적인 지침은 Azure AD와 tooverify 도메인 이름을 어떻게, [고유한 도메인 이름을 tooAzure AD 추가](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409)합니다.
     
     ![도메인](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    e. Hello 이전 tooadd tooyour 디렉터리를 만들려는 경우 모든 hello 도메인에 대 한 단계를 반복 합니다.

5. Azure AD에서 모든 도메인을 확인했으므로 이제 Google Apps에서 다시 확인해야 합니다. Google Apps를 통해 이미 등록 되지 않은 각 도메인에 대 한 단계를 수행 하는 hello 수행.
   
    a. Hello에 [Google 앱 관리 콘솔](http://admin.google.com/), 클릭 **도메인**합니다.
     
     ![도메인을 클릭합니다.][20]

    b. **Add a domain or a domain alias(도메인 또는 도메인 별칭 추가)**를 클릭합니다.
     
     ![새 도메인 추가][21]

    c. 선택 **다른 도메인을 추가**, 싶다는 의사를 tooadd hello 도메인의 hello 이름 입력 합니다.
     
     ![사용자의 도메인 이름을 입력합니다.][22]

    d. **Continue and verify domain ownership**(계속해서 도메인 소유권 확인)을 클릭합니다. 그런 다음 hello 도메인 이름을 소유 하 고 있음을 hello 단계 tooverify를 따릅니다. 에 대 한 포괄적인 지침은 tooverify Google Apps를 통해 도메인 확인 하려면 어떻게 해야 합니다. [Google Apps에서 사이트 소유권 확인](https://support.google.com/webmasters/answer/35179)을 참조하세요.

    e. Hello 이전 tooadd tooGoogle 응용 프로그램을 만들려는 경우 다른 도메인에 대 한 단계를 반복 합니다.
     
     > [!WARNING]
     > 이미 있는 경우와 Azure ad single sign-on 구성 Google Apps 테 넌 트에 대 한 hello 주 도메인을 변경한 경우 아래의 toorepeat 단계 # 3에 있는 [2 단계: 사용 하도록 설정 Single Sign-on](#step-two-enable-single-sign-on)합니다.
       
6. Hello에 [Google 앱 관리 콘솔](http://admin.google.com/), 클릭 **관리자 역할이 할당**합니다.
   
     ![Google Apps 클릭][26]

7. 어떤 관리자 결정를 계정 toouse toomanage 사용자 프로 비전 합니다. Hello에 대 한 **관리자 역할이** 해당 계정의 hello 편집 **권한** 해당 역할에 대 한 합니다. 모든 hello 권한이 있는지 확인 **관리자 API 권한** 이 계정을 프로 비전에 사용할 수 있도록 설정 합니다.
   
     ![Google Apps 클릭][27]
   
    > [!NOTE]
    > 프로덕션 환경에 구성 하는 경우 toocreate 관리자 계정이 Google Apps에서이 단계에 대해 구체적으로 hello 가장 좋습니다. 이러한 계정은 연결 된 hello 필요한 API 권한이 있는 관리자 역할에 있어야 합니다.
     
8. Hello에 [Azure 포털](https://portal.azure.com), toohello 찾아보기 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션.

9. Single sign on에 대 한 Google Apps를 이미 구성한 경우 Google Apps hello 검색 필드를 사용 하 여 인스턴스에 대 한 검색 합니다. 그렇지 않은 경우 선택 **추가** 검색 한 **Google Apps** hello 응용 프로그램 갤러리에 있습니다. Google Apps hello 검색 결과에서 선택한 응용 프로그램의 tooyour 목록을 추가 합니다.

10. Google Apps의 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.

11. 집합 hello **프로 비전 모드** 너무**자동**합니다. 

     ![프로비전](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. Hello에서 **관리자 자격 증명** 섹션에서 클릭 **Authorize**합니다. 그러면 새 브라우저 창에서 Google Apps 권한 부여 대화 상자가 열립니다.

13. 싶다는 의사를 toogive Azure Active Directory 권한 toomake 변경 tooyour Google Apps 테 넌 트를 확인 합니다. **Accept**를 클릭합니다.
    
     ![사용 권한을 확인합니다.][28]

14. Hello Azure 포털에서에서 클릭 **연결 테스트** tooensure Azure AD tooyour Google Apps 응용 프로그램을 연결할 수 있습니다. Hello 연결이 실패 하는 경우 Google Apps 계정이 팀 관리자 권한을 확인 하 고 hello 시도 **"권한 부여"** 다시 합니다.

15. 개인 이나 hello에 프로 비전 오류 알림의 받을 그룹의 hello 전자 메일 주소를 입력 **알림 전자 메일** 필드 및 hello 확인란을 선택 합니다.

16. **저장**을 클릭합니다.

17. Hello 매핑 섹션에서 선택 **동기화 Azure Active Directory 사용자 tooGoogle 앱.**

18. Hello에 **특성 매핑을** 섹션에서 Azure AD tooGoogle 응용 프로그램에서에서 동기화 되는 hello 사용자 특성을 검토 합니다. 특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 Google Apps에서 되는 사용 되는 toomatch hello 사용자 계정입니다. 변경 내용을 저장 단추 toocommit hello를 선택 합니다.

19. tooenable hello Google Apps, 변경 hello에 대 한 Azure AD 프로 비전 서비스 **프로 비전 상태** 너무**에** hello 설정 섹션에서

20. **저장**을 클릭합니다.

모든 사용자의 hello 초기 동기화를 시작 및/또는 그룹이 hello 사용자 및 그룹 섹션에서 tooGoogle 응용 프로그램 할당 hello 초기 동기화는 hello 서비스가 실행 되 고으로 약 20 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform 합니다. Hello를 사용할 수 있습니다 **동기화 세부 정보와** toomonitor 진행률 섹션 및 Google Apps 응용 프로그램에서 서비스를 프로 비전 하는 hello에서 수행 하는 모든 작업을 설명 하는 링크 tooprovisioning 작업 보고서를 따릅니다.

## <a name="additional-resources"></a>추가 리소스

* [엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)
* [Single Sign-On 구성](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png