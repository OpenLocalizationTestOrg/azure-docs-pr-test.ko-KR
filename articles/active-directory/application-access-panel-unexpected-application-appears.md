---
title: "hello 액세스 패널에 나타나는 aaaHow 응용 프로그램 | Microsoft Docs"
description: "응용 프로그램은 hello 액세스 패널에에서 나타나지 않는 문제 해결"
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
ms.reviewr: japere
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a>Hello 액세스 패널에 응용 프로그램이 표시 하는 방법

hello 액세스 패널은 작업으로는 사용할 수 있는 웹 기반 포털 또는 학교 계정을 Azure Active Directory (Azure AD) tooview 및 시작 클라우드 기반 응용 프로그램에서 해당 hello Azure AD 관리자가 부여 해 준에 대 한 액세스. 이러한 응용 프로그램 hello Azure AD 포털에서 hello 사용자를 대신 하 여 구성 됩니다. admin 님 안녕하세요 hello 응용 프로그램 toohello 사용자 직접 또는 사용자가 hello 사용자의 액세스 패널에 표시 되는 hello 응용 프로그램에서 결과의 일부 tooa 그룹 프로 비전 할 수 있습니다.

## <a name="general-issues-toocheck-first"></a>일반 toocheck를 먼저 문제

-   응용 프로그램 사용자 로부터 방금 제거한 hello 사용자 그룹의 멤버인 경우 다시 toosign 및 축소 hello 사용자의 액세스 패널에 몇 분 toosee 후 hello 응용 프로그램을 제거 하는 경우.

-   사용자 또는 그룹 hello 사용자에서 라이선스가 제거 방금 되었으면는이 멤버는 변경 내용 toobe 수행에 대 한 hello 그룹의 hello 크기와 복잡성에 따라 시간이 오래 걸릴 수 있습니다. Hello 액세스 패널에 로그인 하기 전에 추가 시간을 허용 합니다.

## <a name="problems-related-tooassigning-applications-toousers"></a>문제 관련된 tooassigning 응용 프로그램 toousers

사용자 표시 될 수는 응용 프로그램 액세스 패널에서은 이전에 할당 된 tooit 합니다. 다음은 몇 가지 방법으로 toocheck입니다.

-   [사용자가 toohello 응용 프로그램을 할당 하는 경우 확인](#check-if-a-user-is-assigned-to-the-application)

-   [사용자 라이선스 인지 확인 toohello 응용 프로그램 관련](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a>사용자가 toohello 응용 프로그램을 할당 하는 경우 확인

toocheck 사용자 toohello 응용 프로그램에 지정 되 면 hello 아래의 단계를 수행 합니다.

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

6.  **검색** hello 응용 프로그램과의 hello 이름에 대 한 합니다.

7.  **사용자 및 그룹**을 클릭합니다.

8.  이때 회원님의 사용자 toohello 응용 프로그램에 할당 된 경우 toosee를 확인 합니다.

  * Hello 응용 프로그램에서 사용자가 tooremove hello **hello 행 클릭** hello 사용자를 선택 **삭제**합니다.

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a>사용자 라이선스 인지 확인 toohello 응용 프로그램 관련

toocheck 사용자의 라이선스를 다음 단계에 따라 hello 할당:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.

5.  **모든 사용자**를 클릭합니다.

6.  **검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.

7.  클릭 **라이선스** toosee 현재 어떤 라이선스 hello 사용자에 게 할당 합니다.

   * Hello 사용자가 할당 된 tooan Office 라이선스 하는 경우 첫 번째 파티 Office 응용 프로그램 tooappear hello 사용자의 액세스 패널에 사용 하도록 설정 합니다.

## <a name="problems-related-tooassigning-applications-toogroups"></a>문제 관련된 tooassigning 응용 프로그램 toogroups

사용자 표시 될 수는 응용 프로그램 액세스 패널에서 hello 응용 프로그램 할당 된 그룹의 일부입니다. 다음은 몇 가지 방법으로 toocheck입니다.

-   [사용자의 그룹 구성원 자격 확인](#check-a-users-group-memberships)

-   [사용자 tooa 라이선스를 할당 된 그룹의 구성원 인지 확인](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a>사용자의 그룹 구성원 자격 확인

toocheck 그룹의 구성원, 다음 단계에 따라 hello:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.

5.  **모든 사용자**를 클릭합니다.

6.  **검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.

7.  **그룹**을 클릭합니다.

8.  이때 회원님의 사용자는 할당 된 그룹 toohello 응용 프로그램의 일부인 경우 toosee를 확인 합니다.

   * Hello 그룹에서 사용자가 tooremove hello **hello 행 클릭** hello 그룹 및 삭제를 선택 합니다.

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a>사용자 tooa 라이선스를 할당 된 그룹의 구성원 인지 확인

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.

5.  **모든 사용자**를 클릭합니다.

6.  **검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.

7.  **그룹**을 클릭합니다.

8.  특정 그룹의 hello 행을 클릭 합니다.

9.  클릭 **라이선스** toosee 라이선스 hello 그룹 tooit에 할당 합니다.

  * Hello 그룹이 할당 된 tooan Office 라이선스 이면이 hello 사용자의 액세스 패널에 첫 번째 파티 Office 응용 프로그램 tooappear 특정로 설정 될 수 있습니다.


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>이러한 문제 해결 단계 hello 하지 않는 경우 hello 문제 해결

사용 가능한 경우 다음 정보는 hello로 지원 티켓을 엽니다.

-   상관 관계 오류 ID

-   UPN(사용자 전자 메일 주소)

-   테넌트 ID

-   브라우저 종류

-   오류가 발생하는 동안 표준 시간대 및 시간/기간

-   Fiddler 추적

## <a name="next-steps"></a>다음 단계
[Azure Active Directory로 응용 프로그램 관리](active-directory-enable-sso-scenario.md)
