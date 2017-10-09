---
title: "aaaSelf 서비스 응용 프로그램 액세스 및 Azure Active Directory와 위임 된 관리 | Microsoft Docs"
description: "이 문서에서는 tooenable 셀프 서비스 응용 프로그램 액세스 하는 방법 및 Azure Active Directory와 위임 된 관리를 설명 합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 448a7fe8-a162-475e-9ba2-2e3ab59302bc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: asmalser
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 90bec3bd71796f22a782929b028db0d18c3aa1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-application-access-and-delegated-management-with-azure-active-directory"></a>Azure Active Directory를 사용하는 셀프 서비스 응용 프로그램 액세스 및 위임된 관리
최종 사용자에 대한 셀프 서비스 기능을 사용하는 작업은 엔터프라이즈 IT에 대한 일반적인 시나리오입니다. 사용자, 응용 프로그램 및 hello 사용자에 게 best-informed toomake 액세스 다양 한 많은 결정 디렉터리 관리자에 게 되지 않을 수 있습니다 권한을 부여 합니다. 종종 hello 최상의 사람 toodecide 응용 프로그램에 액세스할 수 있는 다른 위임 된 관리자 또는 팀 리더는입니다. 그러나 hello 앱을 사용 하는 hello 사용자 및 hello 사용자 무엇을 알고 toobe 수 toodo 업무 필요 합니다.

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다. 

셀프 서비스 응용 프로그램 액세스는 디렉터리 관리자가 다음을 수행할 수 있도록 하는 [Azure Active Directory Premium](https://azure.microsoft.com/trial/get-started-active-directory/) P1 및 P2 라이선스의 기능입니다.

* Hello에 바둑판식으로 배열 tooapplications "Get 더 많은 응용 프로그램"를 사용 하 여 사용자가 toorequest 액세스할 수 있도록 [Azure AD 액세스 패널](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)
* 액세스를 요청할 수 있는 응용 프로그램 사용자 설정
* 사용자가 toobe 수 tooself 할당 액세스 tooan 응용 프로그램에 필요한 승인 되는지 여부를 설정 합니다.
* Hello 요청을 승인 하 고 각 응용 프로그램에 대 한 액세스를 관리 해야 사용자 설정

이 기능은 모든 사전 통합 및 사용자 지정 앱에서에서 지 원하는 페더레이션 또는 암호 기반 single sign on hello 대해서는 오늘 [Azure Active Directory 응용 프로그램 갤러리](https://azure.microsoft.com/marketplace/active-directory/all/), Salesforce, Dropbox, 같은 앱을 포함 하 여 Google Apps 등입니다.
이 문서에서는 다음과 같이 방법을 설명합니다.

* 최종 사용자에게 선택적 승인 워크플로의 구성을 비롯한 셀프 서비스 응용 프로그램 액세스를 구성합니다. 
* 특정 응용 프로그램 toohello 가장 적합 한 하면 조직의 사용자에 대 한 액세스 관리를 위임 하 고 toouse hello Azure AD 액세스 패널 tooapprove 액세스 요청을 다시 설정, tooselected 사용자 액세스에 직접 할당 또는 설정 (선택 사항) 암호 기반 single sign on 구성 된 경우 응용 프로그램 액세스에 대 한 자격 증명

## <a name="configuring-self-service-application-access"></a>셀프 서비스 응용 프로그램 액세스 구성
tooenable 셀프 서비스 응용 프로그램 액세스 및 응용 프로그램을 추가할 수 있습니다 또는 다음이 지침을 따라 최종 사용자가 요청한 사용자를 구성 합니다.

1. Hello에 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/)합니다.

2.   Hello에서 **Active Directory** 섹션, 디렉터리를 선택한 다음 선택 hello **응용 프로그램** 탭 합니다. 

3. 선택 hello **추가** , 단추 및 hello 갤러리 옵션 tooselect 사용 하 여 응용 프로그램을 추가 합니다.

4. 앱 추가 된 후에 hello 앱 빠른 시작 페이지를 볼 수 있습니다. 클릭 **구성 Single Sign-on**, hello 원하는 single sign-on 모드를 선택 하 고 hello 구성을 저장 합니다. 

5. 다음으로, 선택 hello **구성** 탭 tooenable 사용자 toorequest access toothis 앱 hello Azure AD 액세스 패널에서 설정 **셀프 서비스 응용 프로그램 액세스를 허용** 너무**예**.
  
  ![][1]

6. 액세스 요청에 대 한 승인 워크플로 구성 하는 toooptionally 설정 **액세스 권한을 부여 하기 전에 승인 필요** 너무**예**합니다. Hello를 사용 하 여 하나 이상의 승인자를 선택할 수 있습니다 다음 **승인자** 단추입니다.

  승인자는 Azure AD 계정 사용 하는 hello 조직에서 모든 사용자 일 수를 유발할 수 계정 프로 비전에 대 한 라이선스 또는 조직에 tooan 앱 액세스 권한을 부여 하기 전에 필요한 다른 비즈니스 프로세스입니다. 하나 이상의 hello 그룹 소유자 계정 그룹을 공유 하 고가 공유 계정을 통해 액세스 권한을 이러한 그룹 toogive의 hello 사용자 tooone를 할당할 수 hello 승인자도 수 있습니다. 

  승인이 필요한 경우 그런 다음 사용자가 즉시 가져오기 hello 응용 프로그램 추가 tootheir Azure AD 액세스 패널 Hello 응용 프로그램에 설정 된 경우 [자동 사용자 프로 비전](active-directory-saas-app-provisioning.md),이 설정 되었는지 또는 ["사용자 관리" 암호 SSO 모드](active-directory-appssoaccess-whatis.md#password-based-single-sign-on), hello 사용자는 이미 사용자 계정 및 hello 암호를 알고 있어야 합니다.

7. Hello 응용 프로그램에 구성 된 toouse 되었으면 암호 기반 single sign on, 각 사용자를 대신 하 여 hello SSO 자격 증명 tooset hello 승인자를 허용 하기 위한 옵션 제공 됩니다. 자세한 내용은 hello 섹션을 참조 [액세스 관리를 위임](#delegated-application-access-management)합니다.

8. 마지막으로, hello **Self-Assigned 사용자에 대 한 그룹** 표시 hello hello 그룹을 사용 하는 toostore hello 사용자에 게 부여 되었거나 할당 된 액세스 toohello 응용 프로그램의 이름입니다. hello 액세스 승인자에는이 그룹의 hello 소유자가 됩니다. 표시 된 hello 그룹 이름을 없는 경우 자동으로 생성 됩니다. 필요에 따라 hello 그룹 이름에는 기존 그룹의 toohello 이름이 설정할 수 있습니다.

9. toosave hello 구성 클릭 **저장** hello hello 화면 맨 아래에 있습니다. 이제 사용자는 hello 액세스 패널에서 toorequest 액세스 toothis 앱을 수 있습니다.

10. tootry hello 최종 사용자에 게 앱 승인자 아닌 다른 계정을 사용 하 여 https://myapps.microsoft.com에서 조직의 Azure AD 액세스 패널에 로그인 합니다. 

11. Hello에서 **응용 프로그램** 탭에서 hello **추가 응용 프로그램 가져오기** 바둑판식으로 배열입니다. 이 타일의 모든 셀프 서비스 응용 프로그램 액세스 기능 toosearch hello 및 hello 왼쪽에 앱 범주별으로 필터 hello 디렉터리에 대 한 활성화 된 hello 응용 프로그램 갤러리를 표시 합니다. 

12. 앱에 대해 클릭 하면 hello 요청 프로세스를 시작 합니다. 승인 프로세스가 필요한 경우 hello 아래 hello 응용 프로그램에 즉시 추가 됩니다 **응용 프로그램** 짧은 확인 한 후 탭 합니다. 승인이 필요한 경우이 나타내는 대화 상자를 표시 하 고 전자 메일 toohello 승인자를 전송 됩니다. Hello에 서명 해야이 요청 프로세스 아닌 승인자 toosee로 액세스 패널입니다.

13. hello 전자 메일 hello 승인자 toosign hello Azure AD 액세스 패널에 지시 하 고 hello 요청을 승인 합니다. 아래에 표시 하는 hello 응용 프로그램 hello 사용자에 게 표시 hello 요청이 승인 되 (및 정의 하는 특별 한 프로세스 hello 승인자에서 수행 된) 되 면 해당 **응용 프로그램** 탭에 서명할 수 있습니다.

## <a name="delegated-application-access-management"></a>위임된 응용 프로그램 액세스 관리
응용 프로그램 액세스 승인자 toohello 응용 프로그램에 대 한 액세스를 거부 또는 hello 가장 적합 한 사람 tooapprove 인 조직에서 모든 사용자를 수 있습니다. 이 사용자를 유발할 수 계정 프로 비전에 대 한 라이선스 또는 조직에 tooan 앱 액세스 권한을 부여 하기 전에 필요한 다른 비즈니스 프로세스입니다.

위에서 설명한 셀프 서비스 응용 프로그램 액세스를 구성할 때 모든 할당 된 응용 프로그램 승인자 참조 추가 **응용 프로그램 관리** 더 응용 프로그램 찍고 hello Azure AD 액세스 패널에서 타일 에 대 한 액세스 관리자에 게 합니다. 앱을 클릭하면 몇 가지 옵션이 있는 화면을 보여줍니다.

![][2]

### <a name="approve-requests"></a>요청 승인
hello **승인 요청** 타일 허용 승인자 toosee 확인 하거나 거부할 수 모든 보류 중인 승인 특정 toothat 응용 프로그램 및 리디렉션 toohello 승인 탭 hello를 요청 합니다. 또한 hello 승인자 어떤 toodo 하도록 지시 하는 요청을 만들 때마다 자동화 된 전자 메일을 받습니다.

### <a name="add-users"></a>사용자 추가
hello **사용자 추가** 타일 toodirectly grant 선택한 사용자가 액세스 toohello 응용 프로그램이 승인자 수 있도록 합니다. 이 타일을 클릭 하면 hello 승인자에 게 대화 수 있도록 tooview 및 사용자 검색 자신의 디렉터리에 표시 됩니다. 해당 사용자의 Azure AD 액세스 패널 또는 Office 365에 표시 되는 hello 응용 프로그램에서 사용자 결과 추가 합니다. 모든 수동 사용자 프로세스를 프로 비전 해야 하는 경우 hello 사용자 하기 전에 hello 앱 수 toosign에 다음 hello 승인자에 대 한 액세스를 할당 하기 전에이 프로세스를 수행 해야 합니다.  

### <a name="manage-users"></a>사용자 관리
hello **사용자 관리** 승인자 toodirectly 업데이트 어댑터나 제거 액세스할 수 있는 사용자 타일 허용 toohello 응용 프로그램입니다. 

### <a name="configure-password-sso-credentials-if-applicable"></a>암호 SSO 자격 증명 구성(적용 가능한 경우)
hello **구성** hello 응용 프로그램에서 IT 관리자 toouse 암호 기반 single sign on, hello 구성 되 고 관리자에 게 부여 hello 승인자 hello 기능 tooset 암호 SSO 자격 증명 하는 경우 타일만 표시 앞서 설명한 합니다. 옵션을 선택 하면 hello 자격 증명 전파 tooassigned 사용자를가 하는 방법에 대 한 몇 가지 옵션 hello 승인자 표시 됩니다.

![][3]

* **사용자가 자신의 암호를 사용 하 여 로그인** -이 모드에서는 hello 할당 된 사용자에 대해 알고 자신의 사용자 이름 및 암호 hello 응용 프로그램에 대 한 증명된 tooenter는 첫 번째 로그인 toohello 응용 프로그램에 해당 합니다. hello 시나리오 해당 toohello 암호 SSO 경우 여기서 hello [사용자 자격 증명 관리](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)합니다.
* **사용자를 관리 하는 별도 계정을 사용 하 여 자동으로 로그인** -이 모드에서는 할당 된 hello 사용자 tooenter 필요 없는 또는 hello 응용 프로그램에 로그인 할 경우 응용 프로그램 특정 자격 증명을 알고 있습니다. 대신, hello 승인자 hello 자격 증명을 설정 각 사용자에 대 한 hello를 사용 하 여 액세스를 할당 한 후 **사용자 추가** 바둑판식으로 배열입니다. Hello 사용자가 액세스 패널 또는 Office 365에 hello 응용 프로그램을 클릭 하면 자동으로 hello 승인자가 설정 된 hello 자격 증명을 사용 하 여 서명 됩니다. hello 시나리오 해당 toohello 암호 SSO 경우 여기서 hello [관리자 자격 증명 관리](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)합니다.
* **사용자는 자동으로 관리 하는 단일 계정을 사용 하 여 로그** -특수 한 경우,이 경우에도 적절 한 toouse 할당 된 모든 사용자가 단일 공유 계정을 사용 하 여 액세스를 부여 toobe 필요 합니다. 이 기능에 대 한 가장 일반적인 사용 사례 hello은 소셜 미디어 및 응용 프로그램과 함께, 여기서 조직 단일 "company" 계정에 여러 사용자가 toomake 업데이트 toothat 계정이 필요 합니다. hello 시나리오 또한 해당 toohello 암호 SSO 경우 여기서 hello [관리자 자격 증명 관리](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)합니다. 그러나,이 옵션을 선택한 후 hello 승인자 증명된 tooenter hello 사용자 이름 및 hello 단일 공유 계정에 대 한 암호를 수 있습니다. 완료 되 면 할당 된 모든 사용자가 Office 365 또는 Azure AD 액세스 패널에 hello 응용 프로그램을 클릭할 때이 계정을 사용 하 여 서명 됩니다.

## <a name="additional-resources"></a>추가 리소스
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)

<!--Image references-->
[1]: ./media/active-directory-self-service-application-access/ssaa_admin.PNG
[2]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app.PNG
[3]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app_config.PNG
