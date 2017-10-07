---
title: "aaaHow tooconfigure 암호 single sign on Azure AD 갤러리 응용 프로그램에 대 한 | Microsoft Docs"
description: "어떻게 tooconfigure 응용 프로그램에 대 한 보안 암호 기반 single sign on hello Azure AD 응용 프로그램 갤러리에에서 이미 나열 되어 있는 경우"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 7a93bff119b477d946368686fc2d9006ca2722a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Azure AD 갤러리 응용 프로그램에 대 한 sign-on tooconfigure 암호 single 방법

Hello에서 응용 프로그램을 추가할 때 [Azure AD 응용 프로그램 갤러리](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), 원하는 toothat 응용 프로그램에서 사용자가 toosign 프로그램 hello 선택할 수 있습니다. Hello를 선택 하 여 언제 든 지가 선택이 항목을 구성할 수 있습니다 **Single Sign on** hello에 엔터프라이즈 응용 프로그램에서 탐색 항목 [Azure 포털](https://portal.azure.com/)합니다.

Single sign on 방법의 사용 가능한 tooyou hello 중 하나는 hello [암호 기반 Single sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) 옵션입니다. 이 훌륭한 방법 tooget 신속 하 게 Azure AD에 응용 프로그램 통합을 시작 하 고 수 있습니다.

-   사용 하도록 설정 **Single Sign on 사용자를 위해** 안전 하 게 저장 하 여 사용자 이름 및 hello 응용 프로그램에 대 한 암호를 재생 하 여 Azure AD와 통합 했습니다

-   **여러 필드에 로그인 해야 하는 응용 프로그램을 지원** 것 이상의 사용자 이름 및 암호 필드 toosign에서 필요로 하는 응용 프로그램에 대 한

-   **Hello 레이블 사용자 지정** hello 사용자 이름 및 암호 입력된 필드의 사용자에 게 hello에서 표시 [응용 프로그램 액세스 패널로](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) 자격 증명을 입력 하는 경우

-   허용 하면 **사용자** tooprovide 자신의 사용자 이름 및 암호를 입력할에 수동으로 hello에 모든 기존 응용 프로그램 계정에 대 한 [응용 프로그램 액세스 패널](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)

-   허용 된 **hello 비즈니스 그룹의 구성원** toospecify hello 사용자 이름 및 암호 tooa 사용자 hello를 사용 하 여 할당 된 [셀프 서비스 응용 프로그램 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) 기능

-   허용 된 **관리자** toospecify hello 사용자 이름 및 암호가 tooa 사용자 hello 업데이트 자격 증명을 사용 하 여 할당 된 경우 기능 [사용자 tooan 응용 프로그램 할당](#assign-a-user-to-an-application-directly)

-   허용 된 **관리자** toospecify 공유 hello 사용자 이름 또는 암호가 hello 업데이트 자격 증명을 사용 하 여 사용자의 그룹에 사용 되는 경우 기능 [그룹 tooan 응용 프로그램 할당](#assign-an-application-to-a-group-directly)

아래 설정 하는 방법에 대해 설명 [암호 기반 Single sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) hello에 이미 있는 tooan 응용 프로그램 [Azure AD 응용 프로그램 갤러리](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery)합니다.

## <a name="overview-of-steps-required"></a>필요한 단계 개요
tooconfigure hello Azure AD 갤러리에서 응용 프로그램 해야합니다.

-   [Hello Azure AD 갤러리에서 응용 프로그램 추가](#add-an-application-from-the-azure-ad-gallery)

-   [암호 single sign on에 대 한 hello 응용 프로그램 구성](#configure-the-application-for-password-single-sign-on)

-   [Hello 응용 프로그램 tooa 사용자 또는 그룹을 할당 합니다.](#assign-the-application-to-a-user-or-a-group)

    -   [사용자 tooan 응용 프로그램을 직접 할당](#assign-a-user-to-an-application-directly)

    -   [응용 프로그램 tooa 그룹에 직접 할당](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a>Hello Azure AD 갤러리에서 응용 프로그램 추가

아래의 hello 단계를 수행 하는 tooadd hello Azure AD 갤러리에서에서 응용 프로그램:

1.  열기 hello [Azure 포털](https://portal.azure.com) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드

6.  Hello에 **이름을 입력** hello에서 textbox **hello 갤러리에서 추가** 섹션, hello 응용 프로그램의 형식 hello 이름

7.  Hello 응용 프로그램 선택 tooconfigure single sign on

8.  Hello 응용 프로그램을 추가 하기 전에 hello에서 이름을 변경할 수 **이름** 텍스트 상자에 붙여넣습니다.

9.  클릭 **추가** tooadd hello 응용 프로그램 단추입니다.

짧은 시간 후 수 toosee hello 응용 프로그램의 구성 블레이드에서 수 있습니다.

## <a name="configure-hello-application-for-password-single-sign-on"></a>암호 single sign on에 대 한 hello 응용 프로그램 구성

tooconfigure single sign on 응용 프로그램에 대 한 아래의 hello 단계를 수행 합니다.

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

  * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  Hello 응용 프로그램 선택 tooconfigure single sign on

7.  Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  선택 hello 모드 **암호 기반 로그온 합니다.**

9.  [Toohello 응용 프로그램 사용자를 할당](#assign-a-user-to-an-application-directly)합니다.

10. Hello 사용자의 hello 행을 선택 하 고를 클릭 하 여 hello 사용자 대신 자격 증명도 제공할 수 또한 **업데이트 자격 증명** hello 사용자를 대신해 서 hello 사용자 이름 및 암호를 입력 합니다. 그렇지 않은 경우 사용자 수 증명된 tooenter hello 자격 증명 자체 종료 합니다.

## <a name="assign-a-user-tooan-application-directly"></a>사용자 tooan 응용 프로그램을 직접 할당

tooassign 아래의 hello 단계를 직접 수행 하는 하나 이상의 사용자가 tooan 응용 프로그램:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

  * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  원하는 사용자 toofrom hello 목록 tooassign hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 **사용자 및 그룹** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  Hello 클릭 **추가** hello 위로 단추 **사용자 및 그룹** 목록 tooopen hello **할당 추가** 블레이드입니다.

9.  hello 클릭 **사용자 및 그룹** hello에서 선택기 **할당 추가** 블레이드입니다.

10. Hello 입력 **전체 이름** 또는 **전자 메일 주소** hello에 할당 하려는 hello 사용자의 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자입니다.

11. Hello 위로 마우스를 가져가고 **사용자** hello 목록 tooreveal에는 **확인란**합니다. Hello 확인란 다음 toohello 사용자의 프로필 사진 또는 로고 tooadd 사용자 toohello 클릭 **선택한** 목록입니다.

12. **선택 사항:** 너무 원하는 경우**둘 이상의 사용자를 추가**, 다른 유형 **전체 이름** 또는 **전자 메일 주소** hello에 **이름으로 검색 전자 메일 주소 또는** 상자에서 검색 하 고이 사용자 toohello hello 확인란 tooadd 클릭 **선택한** 목록입니다.

13. 사용자 선택을 완료 했으면 클릭 hello **선택** 단추 tooadd 해당 사용자 및 그룹 toobe toohello 목록이 toohello 응용 프로그램을 할당 합니다.

14. **선택 사항:** hello 클릭 **역할 선택** hello에 선택 기가 **할당 추가** 블레이드 tooselect 역할 tooassign toohello 사용자가 선택한 합니다.

15. Hello 클릭 **할당** 단추 tooassign hello 응용 프로그램 toohello 사용자를 선택 합니다.

## <a name="assign-an-application-tooa-group-directly"></a>응용 프로그램 tooa 그룹에 직접 할당

하나 이상의 tooassign 그룹 tooan 응용 프로그램을 직접 아래 hello 단계 수행:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

  * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  원하는 사용자 toofrom hello 목록 tooassign hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 **사용자 및 그룹** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  Hello 클릭 **추가** hello 위로 단추 **사용자 및 그룹** 목록 tooopen hello **할당 추가** 블레이드입니다.

9.  hello 클릭 **사용자 및 그룹** hello에서 선택기 **할당 추가** 블레이드입니다.

10. Hello 입력 **전체 그룹 이름** hello에 할당 하려는 hello 그룹의 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자입니다.

11. Hello 위로 마우스를 가져가고 **그룹** hello 목록 tooreveal에는 **확인란**합니다. Hello 확인란 다음 toohello 그룹의 프로필 사진 또는 로고 tooadd 사용자 toohello 클릭 **선택한** 목록입니다.

12. **선택 사항:** 너무 원하는 경우**둘 이상의 그룹을 추가**, 다른 유형 **전체 그룹 이름** hello에 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자 이 그룹 toohello hello 확인란 tooadd 클릭 **선택한** 목록입니다.

13. 그룹을 선택 하면 완료 했으면 클릭 hello **선택** 단추 tooadd 해당 사용자 및 그룹 toobe toohello 목록이 toohello 응용 프로그램을 할당 합니다.

14. **선택 사항:** hello 클릭 **역할 선택** hello에 선택 기가 **할당 추가** 블레이드 tooselect 역할 tooassign toohello 그룹 선택 했습니다.

15. Hello 클릭 **할당** 단추 tooassign hello 응용 프로그램 toohello 선택 된 그룹입니다.

짧은 기간 hello 사용자가 선택한 수 수 toolaunch에서 이러한 응용 프로그램 액세스 패널 hello 합니다.

## <a name="next-steps"></a>다음 단계
[응용 프로그램 프록시 single sign on tooyour 앱을 제공 합니다.](active-directory-application-proxy-sso-using-kcd.md)
