---
title: "aaaHow tooconfigure 셀프 서비스 응용 프로그램 할당 | Microsoft Docs"
description: "셀프 서비스 응용 프로그램 액세스 tooallow 사용자 toofind 자신의 응용 프로그램 사용"
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
ms.openlocfilehash: d25a0146c4c8cebf9c2ae8c516f094a8eccb4570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-self-service-application-assignment"></a>어떻게 tooconfigure 셀프 서비스 응용 프로그램 할당

사용자가 액세스 패널에서 응용 프로그램을 검색할 자체 수, 먼저 tooenable **셀프 서비스 응용 프로그램 액세스** tooallow 사용자 tooself 한다고 tooany 응용 프로그램-검색 및 액세스를 요청 합니다.

이 기능은 수 있는 좋은 방법을 toosave 시간과 비용은 IT 그룹으로 이며 Azure Active Directory와 최신 응용 프로그램 배포의 일부로 작성 된 것이 좋습니다.

이 기능을 사용하면 다음을 수행할 수 있습니다.

-   사용자가 자체 hello에서 응용 프로그램을 검색할 수 있도록 [응용 프로그램 액세스 패널로](https://myapps.microsoft.com/) hello IT 하지 않고 그룹입니다.

-   액세스를 요청한 사용자가 참조 하,이 대 한 액세스를 제거 하 고 hello 역할 toothem 할당을 관리할 수 있도록 해당 사용자가 tooa 미리 구성 된 그룹을 추가 합니다.

-   필요에 따라 비즈니스 승인자 tooapprove 응용 프로그램 액세스 요청을 허용 하므로 IT 그룹이 있어 hello를 필요 하지 않습니다.

-   필요에 따라 too10 개인에 게 액세스 toothis 응용 프로그램을 승인 수를 구성 합니다.

-   필요에 따라 비즈니스 승인자 tooset hello 암호를 허용 사용자 צ ְ ײ toosign toohello 응용 프로그램에서는 hello 비즈니스 승인자 로부터 오른쪽 [응용 프로그램 액세스 패널](https://myapps.microsoft.com/)합니다.

-   필요에 따라 자동으로 할당 된 셀프 서비스 사용자 tooan 응용 프로그램 역할을 직접 지정 합니다.

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a>셀프 서비스 응용 프로그램 액세스 tooallow 사용자 toofind 자신의 응용 프로그램 사용

셀프 서비스 응용 프로그램 액세스는 좋은 방법 tooallow 사용자 tooself-필요에 따라 hello 비즈니스 그룹 액세스 하도록 허용 tooapprove toothose 응용 프로그램, 응용 프로그램을 검색 합니다. Hello 비즈니스 그룹 toomanage hello 자격 증명 toothose 사용자가 액세스 패널에서 응용 프로그램에 Single-sign 암호 오른쪽에 대 한 할당을 허용할 수 있습니다.

tooenable 셀프 서비스 응용 프로그램 액세스 tooan 응용 프로그램, 다음 단계에 따라 hello:

1.  열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**

2.  열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.

3.  에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.

4.  클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.

5.  클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.

  * 여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**

6.  Tooenable 셀프 서비스 액세스 toofrom hello 목록을 사용 하려는 hello 응용 프로그램을 선택 합니다.

7.  Hello 응용 프로그램 로드 되 면 클릭 **셀프 서비스** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.

8.  이 응용 프로그램에 대 한 셀프 서비스 응용 프로그램 액세스 tooenable hello 설정 **toorequest access toothis 응용 프로그램 사용자가 허용?** 너무 설정/해제**예입니다.**

9.  Tooselect hello 그룹 toowhich 요청 하는 사용자 액세스 toothis 응용 프로그램을 추가 하도록 hello 선택기 다음 toohello 레이블을 클릭 하는 다음으로, **toowhich 그룹은 할당 된 사용자를 추가할 수?** 그룹을 선택 합니다.

10. **선택 사항:** 원할 경우 toorequire 비즈니스 승인 사용자의 액세스가 허용 되기 전에 설정 hello **toothis 응용 프로그램 액세스 권한을 부여 하기 전에 승인 필요?** 너무 설정/해제**예**합니다.

11. **선택 사항:에 대 한 응용 프로그램에서 사용 하 여 암호 단일 로그인만** toothis 응용 프로그램 승인 된 사용자가을 전송 하는 이러한 비즈니스 승인자 toospecify hello 암호 tooallow 하려는 경우 설정 hello **승인자 tooset 허용 이 응용 프로그램에 대 한 사용자의 암호?**  너무 설정/해제**예**합니다.

12. **선택 사항:** tooapprove access toothis 응용 프로그램 수 있는 toospecify hello 비즈니스 승인자 hello 선택기 다음 toohello 레이블을 클릭 **tooapprove 액세스 toothis 응용 프로그램이 허용 되는 사용자?** tooselect를 too10 개별 비즈니스 승인자 합니다.

   >[!NOTE]
   >그룹은 지원되지 않습니다.
   >
   >

13. **선택 사항:** **역할을 표시 하는 응용 프로그램에 대 한**tooassign 승인 된 사용자가 셀프 서비스 tooa 역할 하려는 경우, hello 선택기 다음 toohello 클릭 **toowhich 역할이이 사용자가 할당 해야 응용 프로그램?**  tooselect hello 역할 toowhich 이러한 사용자만 할당 해야 합니다.

14. Hello 클릭 **저장** hello 블레이드 toofinish hello 위쪽에 단추입니다.

셀프 서비스 응용 프로그램 구성을 완료 한 후 탐색할 수 tootheir [응용 프로그램 액세스 패널로](https://myapps.microsoft.com/) hello를 클릭 하 고 **+ 추가** 단추 toofind hello 앱 toowhich 사용 하도록 설정한 셀프 서비스 액세스 합니다. 비즈니스 승인자는 [응용 프로그램 액세스 패널](https://myapps.microsoft.com/)에서 알림을 볼 수도 있습니다. 사용자가 승인을 해야 하는 액세스 tooan 응용 프로그램을 요청 하는 경우 사용자에 게 알리는 전자 메일을 활성화할 수 있습니다. 

이러한 승인은 즉 여러 승인자를 지정 하면 모든 단일 승인자 수 승인자 액세스 toohello 응용 프로그램이 단일 승인 워크플로만 지원 합니다.

## <a name="next-steps"></a>다음 단계
[셀프 서비스 그룹 관리를 위한 Azure Active Directory 설정](active-directory-accessmanagement-self-service-group-management.md)
