---
title: "Azure AD 응용 프로그램 프록시를 사용 하 여 aaaPublish 앱 | Microsoft Docs"
description: "Hello 클래식 포털에서 Azure AD 응용 프로그램 프록시를 통해 온-프레미스 응용 프로그램 toohello 클라우드를 게시 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7926998314c65521ae48aebcceb33cb0c67e0b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시

> [!div class="op_single_selector"]
> * [Azure Portal](application-proxy-publish-azure-portal.md)
> * [Azure 클래식 포털](active-directory-application-proxy-publish.md)

Azure AD 응용 프로그램 프록시를 사용 하면 온-프레미스 응용 프로그램 toobe hello를 통해 액세스를 게시 하 여 원격 작업자를 지 원하는 인터넷 합니다. 이제 이미 있어야 [hello Azure 클래식 포털에서에서 응용 프로그램 프록시를 사용 하도록 설정](active-directory-application-proxy-enable.md)합니다. 이 문서는 로컬 네트워크에서 실행 되는 hello 단계 toopublish 응용 프로그램을 단계별로 하 고 네트워크 외부에서 보안 원격 액세스를 제공 합니다. 이 문서를 완료 한 후 개인 설정 된 정보 또는 보안 요구 사항과 준비 tooconfigure hello 응용 프로그램 수 수 있습니다.

> [!NOTE]
> 응용 프로그램 프록시는 toohello Premium 또는 Azure Active directory Basic edition을 업그레이드 한 경우에 사용할 수 있는 기능입니다. 자세한 내용은 [Azure Active Directory 버전](active-directory-editions.md)을 참조하세요. 응용 프로그램 프록시 toouse 하려는 경우 다음을 할 수 있습니다 [hello Azure 포털에서에서 응용 프로그램을 게시](application-proxy-publish-azure-portal.md)합니다.

## <a name="publish-an-app-using-hello-wizard"></a>Hello 마법사를 사용 하 여 앱 게시
1. Hello에 관리자 권한으로 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/)합니다.
2. 디렉터리 tooActive 이동한 다음 응용 프로그램 프록시를 설정한 hello 디렉터리를 선택 합니다.
   
    ![Active Directory - 아이콘](./media/active-directory-application-proxy-publish/ad_icon.png)
3. Hello 클릭 **응용 프로그램** 탭을 클릭 한 다음 hello **추가** hello hello 화면 맨 아래에 단추
   
    ![응용 프로그램 추가](./media/active-directory-application-proxy-publish/aad_appproxy_selectdirectory.png)
4. **네트워크 외부에서 액세스할 수 있는 응용 프로그램 게시**를 선택합니다.
   
    ![네트워크 외부에서 액세스할 수 있는 응용 프로그램 게시](./media/active-directory-application-proxy-publish/aad_appproxy_addapp.png)
5. Hello 다음 응용 프로그램에 대 한 정보를 제공 합니다.
   
   * **이름**: hello 응용 프로그램에 대 한 알기 쉬운 이름. 디렉터리 내에서 고유해야 합니다.
   * **내부 URL**: 응용 프로그램 프록시 커넥터 hello hello 주소 tooaccess hello 내부에서 응용 프로그램 사용자가 개인 네트워크를 사용 합니다. Hello 서버 hello 나머지 게시 하지 않은 동안 hello 백 엔드 서버 toopublish에 특정 경로 제공할 수 있습니다. 이러한 방식으로 서로 다른 사이트를 게시할 수 있습니다 동일한 서버 hello 되 고 각각 고유한 이름 및 액세스 규칙을 지정 합니다.
     
     > [!TIP]
     > 경로 게시 하는 경우 모든 hello 필요한 이미지, 스크립트 및 응용 프로그램에 대 한 스타일 시트를 포함 하는지 확인 합니다. 예를 들어 앱 https://yourapp/app에 https://yourapp/media에 있는 이미지를 사용 하는 경우 다음 게시 해야 https://yourapp/ hello 경로로 합니다.
     > 
     > 
   * **사전 인증 방법을**: 응용 프로그램 프록시에 어떻게 액세스 tooyour 응용 프로그램을 제공 하기 전에 사용자를 확인 합니다. Hello 드롭 다운 메뉴에서 hello 옵션 중 하나를 선택 합니다.
     
     * Azure Active Directory: 응용 프로그램 프록시는 hello 디렉터리와 응용 프로그램에 대 한 사용 권한을 인증 하는 Azure AD 사용 하 여 사용자가 toosign을 리디렉션합니다.
     * 사용자가 통과: tooauthenticate tooaccess hello 응용 프로그램을 않아도 됩니다.
     
     ![응용 프로그램 속성](./media/active-directory-application-proxy-publish/aad_appproxy_appproperties.png)  
6. toofinish hello 마법사 hello hello 화면 맨 아래에 hello 확인 표시를 클릭 합니다. hello 응용 프로그램은 이제 Azure AD에서 정의 됩니다.

## <a name="assign-users-and-groups-toohello-application"></a>사용자 및 그룹 toohello 응용 프로그램 할당
tooaccess 게시 된 응용 프로그램 사용자에 대 한 주문, tooassign 필요한을 개별적으로 또는 그룹에 있습니다. (Tooassign 기억 너무 직접 액세스 합니다.) 할당되는 사용자마다 Azure Basic 이상의 라이선스가 필요합니다. 개별적으로 라이선스를 할당할 수 있습니다 또는 toogroups 합니다. 자세한 내용은 참조 [tooan 응용 프로그램 사용자를 할당](active-directory-applications-guiding-developers-assigning-users.md)합니다. 

사전 인증 필요로 하는 응용 프로그램의 경우 toouse hello 응용 프로그램 사용 권한 부여에 사용자 지정 합니다. 필요 하지 않은 앱에 대 한 사전 인증을 사용자 지정 의미 해당 hello 사용자 hello 액세스 패널을 통해 hello 응용 프로그램에 액세스할 수 있습니다.

1. Hello 앱 추가 마법사 완료 후 빠른 응용 프로그램 페이지를 시작 하는 hello를 볼 수 있습니다. access toohello 앱을 가진 toomanage 선택 **사용자 및 그룹**합니다.
   
    ![응용 프로그램 프록시 빠른 시작 할당 사용자 - 스크린샷](./media/active-directory-application-proxy-publish/aad_appproxy_usersgroups.png)
2. 디렉터리에서 특정 그룹을 검색 하거나 모든 사용자를 표시합니다. toodisplay hello 검색 결과 hello 확인 표시를 클릭 합니다.
   
      ![그룹 또는 사용자 검색 - 스크린샷](./media/active-directory-application-proxy-publish/aad_appproxy_search.png)
3. 각 사용자 또는 그룹 tooassign toothis 응용 프로그램을 클릭 하 여 **할당**합니다. tooconfirm이이 작업을 요청 합니다.

> [!NOTE]
> Windows 통합 인증 앱에 대해 온-프레미스 Active Directory에서 동기화되는 사용자와 그룹만 할당할 수 있습니다. Microsoft 계정 및 게스트를 사용하여 로그인하는 사용자는 Azure Active Directory 응용 프로그램 프록시를 사용하여 게시된 앱에 할당할 수 없습니다. Hello의 일부인 자격 증명으로 로그인 사용자가 있는지 확인 hello 앱을 게시 하는 동일한 도메인입니다.
> 
> 

## <a name="test-your-published-application"></a>게시된 응용 프로그램 테스트
응용 프로그램을 게시 한 게시 toohello URL을 탐색 하 여 아웃를 테스트할 수 있습니다. 액세스할 수 있는지, 올바르게 렌더링되었는지 및 모든 것이 예상대로 작동하는지 확인합니다. 문제가 발생 하거나 오류 메시지가 나타날 경우 시도 hello [문제 해결 가이드](active-directory-application-proxy-troubleshoot.md)합니다.

## <a name="configure-your-application"></a>응용 프로그램 구성
게시 된 앱을 수정 하거나 hello 구성 페이지에서 고급 옵션을 설정할 수 있습니다. 이 페이지에서는 hello 이름 변경 또는 로고를 업로드 하 여 앱을 사용자 지정할 수 있습니다. 또한 사전 인증 방법 또는 multi-factor authentication hello와 같은 액세스 규칙을 관리할 수 있습니다.

![고급 구성](./media/active-directory-application-proxy-publish/aad_appproxy_configure.png)

응용 프로그램을 게시 한 후 Azure Active Directory 응용 프로그램 프록시를 사용 하 여 Azure AD에서 hello 응용 프로그램 목록에 표시 하 고 있습니다 관리할 수 있습니다.

응용 프로그램 프록시 서비스를 사용 하지 않도록 응용 프로그램을 게시 한 후, hello 응용 프로그램은 개인 네트워크 외부에서 액세스할 수 있는 더 이상. 사용자가 계속 수 액세스 hello 응용 프로그램이 온-프레미스 평소와 같이 합니다.

입력 한 tooview 응용 프로그램 있는지 한다는 액세스할 수 hello 응용 프로그램의 hello 이름을 두 번 클릭 합니다. Hello 응용 프로그램 프록시 서비스를 사용 하지 않도록 설정 하는 경우 hello 응용 프로그램을 사용할 수 없으면 hello hello 화면 위쪽에 경고 메시지가 나타납니다.

응용 프로그램 toodelete hello 목록에서 응용 프로그램을 선택 하 고 클릭 **삭제**합니다.

## <a name="next-steps"></a>다음 단계
* [고유한 도메인 이름을 사용하여 응용 프로그램 게시](active-directory-application-proxy-custom-domains.md)
* [Single Sign-On 사용](active-directory-application-proxy-sso-using-kcd.md)
* [조건부 액세스 사용](active-directory-application-proxy-conditional-access.md)
* [클레임 인식 응용 프로그램으로 작업](active-directory-application-proxy-claims-aware-apps.md)

Hello 최신 뉴스 및 업데이트에 대 한 체크 아웃 hello [응용 프로그램 프록시 블로그](http://blogs.technet.com/b/applicationproxyblog/)

