---
title: "hello Azure Active Directory 포털에서 aaaSign 기능 작업 보고서 | Microsoft Docs"
description: "Hello Azure Active Directory 포털에서 소개 toosign 기능 작업 보고서"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a>Hello Azure Active Directory 포털의 로그인 활동 보고서

Azure Active Directory (Azure AD) hello에 보고 [Azure 포털](https://portal.azure.com), 환경을 어떻게 진행 되는 toodetermine 필요한 hello 정보를 가져올 수 있습니다.

Azure Active Directory의 보고 아키텍처 hello hello 다음과 같은 구성 요소가 구성 되어 있습니다.

- **활동** 
    - **로그인 활동** – 관리 되는 응용 프로그램 및 사용자 로그인 활동의 hello 사용에 대 한 정보
    - **감사 로그** - 사용자 및 그룹 관리, 관리되는 응용 프로그램 및 디렉터리 활동에 대한 시스템 작업 정보
- **보안** 
    - **위험한 로그인** -위험한 로그인이 사용자 계정의 hello 정당한 소유자가 아닌 사용자에 의해 수행 된 로그인 시도에 대 한 표시기입니다. 자세한 내용은 위험한 로그인을 참조하세요.
    - **위험 플래그가 지정된 사용자** - 위험한 사용자는 손상되었을 수 있는 사용자 계정에 대한 표시기입니다. 자세한 내용은 위험 플래그가 지정된 사용자를 참조하세요.

이 항목에서는 hello 로그인 작업의 개요를 제공 합니다.

## <a name="pre-requisite"></a>필수 구성 요소

### <a name="who-can-access-hello-data"></a>Hello 데이터에 액세스할 수 있는 사용자?
* Hello 보안 판독기 또는 보안 관리자 역할의 사용자
* 전역 관리자
* 모든 사용자(비관리자)가 자신의 로그인에 액세스할 수 있습니다. 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a>어떤 Azure AD 라이선스가 tooaccess 로그인 활동이 필요 한가요?
* 테 넌 트에 연결 된 Azure AD Premium 라이선스가 있어야 합니다. toosee hello 모두에 대 한 로그인 활동 보고서


## <a name="signs-in-activities"></a>로그인 활동

Hello 사용자 로그인 보고서에서 제공 하는 hello 정보를 통해 답변 tooquestions와 같은 찾을 수 있습니다.

* 사용자의 hello 로그인 패턴 이란?
* 한 주 동안 얼마나 많은 사용자가 로그인했나요?
* 이러한 로그인의 hello 상태는 무엇입니까?

첫 번째 항목 지점 tooall 로그인 활동 데이터는 **로그인** 의 hello 활동 섹션에서 **Azure Active**합니다.


![로그인 활동](./media/active-directory-reporting-activity-sign-ins/61.png "로그인 활동")


감사 로그에는 다음 항목을 보여 주는 기본 목록 보기가 있습니다.

- hello 관련된 사용자
- hello 응용 프로그램 hello 사용자가 로그인 하려면
- hello 로그인 상태
- hello 로그인 시간

![로그인 활동](./media/active-directory-reporting-activity-sign-ins/41.png "로그인 활동")

클릭 하 여 hello 목록 보기를 사용자 지정할 수 있습니다 **열** hello 도구 모음에서입니다.

![로그인 활동](./media/active-directory-reporting-activity-sign-ins/19.png "로그인 활동")

이 toodisplay 추가 필드를 사용 하면 하거나 이미 표시 되는 필드를 제거 합니다.

![로그인 활동](./media/active-directory-reporting-activity-sign-ins/42.png "로그인 활동")

Hello 목록 뷰에서 항목을 클릭 하 여 항목에 대 한 모든 사용 가능한 세부 정보를 가져옵니다.

![로그인 활동](./media/active-directory-reporting-activity-sign-ins/43.png "로그인 활동")


## <a name="filtering-sign-in-activities"></a>로그인 활동 필터링

hello 아래로 toonarrow 데이터 tooa 수준 수에 대 한 작동을 필터링 할 수 필드를 다음 hello를 사용 하 여 hello 로그인 데이터를 보고.

- 시간 간격
- 사용자
- 응용 프로그램
- 클라이언트
- 로그인 상태

![로그인 활동](./media/active-directory-reporting-activity-sign-ins/44.png "로그인 활동")


hello **시간 간격** 필터 사용 tooyou toodefine hello에 대 한 시간 범위는 데이터를 반환 합니다.  
가능한 값은 다음과 같습니다.

- 1개월
- 7 일
- 24시간
- 사용자 지정

사용자 지정 시간 범위를 선택하면 시작 시간과 종료 시간을 구성할 수 있습니다.

hello **사용자** toospecify hello 이름이 나 hello 사용자 계정 이름 (UPN) hello 사용자에 대 한 관심의 필터 수 있습니다.

hello **응용 프로그램** 필터 하면 중요 한 hello 응용 프로그램의 toospecify hello 이름입니다.

hello **클라이언트** 필터 사용 하면 중요 한 hello 장치에 대 한 toospecify 정보입니다.

hello **로그인 상태** 필터를 사용 하면 다음 필터는 hello의 tooselect 하나:

- 모두
- 성공
- 실패


## <a name="sign-in-activities-shortcuts"></a>로그인 활동 바로 가기

또한 Active Directory tooAzure hello Azure 포털 하면 두 개의 추가 항목 지점 toosign 기능 작업 데이터:

- 개요
- Enterprise 응용 프로그램


### <a name="users-and-groups-sign-ins-activities"></a>사용자 및 그룹 로그인 활동

Hello 사용자 로그인 보고서에서 제공 하는 hello 정보를 통해 답변 tooquestions와 같은 찾을 수 있습니다.

- 사용자의 hello 로그인 패턴 이란?
- 한 주 동안 얼마나 많은 사용자가 로그인했나요?
- 이러한 로그인의 hello 상태는 무엇입니까?



항목 지점 toothis 데이터는 hello 사용자 로그인에서 그래프 hello **개요** 섹션 아래 **사용자 및 그룹**합니다.

![로그인 활동](./media/active-directory-reporting-activity-sign-ins/45.png "로그인 활동")

부호 주간 집계를 표시 하는 hello 사용자 로그인 그래프의 지정된 된 기간 동안 모든 사용자에 대 한 기능입니다. hello에 대 한 hello 기본 기간 30 일입니다.

![로그인 활동](./media/active-directory-reporting-activity-sign-ins/46.png "로그인 활동")

Hello 로그인 그래프에서 날짜를 클릭 하는 경우이 날짜에 대 한 hello 로그인 활동의 자세한 목록을 가져옵니다.

![로그인 활동](./media/active-directory-reporting-activity-sign-ins/41.png "로그인 활동")

각 행에 선택한 hello 로그인과 같은 대 한 자세한 내용은 hello hello 로그인 활동 목록 제공 합니다.

* 누가 로그인했나요?
* UPN을 관련 hello 무엇 이었습니까?
* 어떤 응용 프로그램을 hello에 대 한 로그인의 대상 hello?
* Hello에 대 한 로그인의 hello IP 주소는 무엇입니까?
* Hello에 대 한 로그인의 hello 상태는 무엇 이었습니까?

hello **로그인** 옵션 모든 사용자 로그인의 전체적인 개요를 제공 합니다.

![로그인 활동](./media/active-directory-reporting-activity-sign-ins/51.png "로그인 활동")



## <a name="usage-of-managed-applications"></a>관리되는 응용 프로그램의 사용량

로그인 데이터의 응용 프로그램 중심 보기를 사용하여 다음과 같은 질문에 대답할 수 있습니다.

* 누가 내 응용 프로그램을 사용하나요?
* Hello 상위 3 개의 응용 프로그램에서 조직 이란?
* 최근에 응용 프로그램을 롤아웃했습니다. 어떻게 작동하고 있나요?

항목 지점 toothis 데이터는 hello 상위 3 개의 응용 프로그램에 hello hello 마지막 30 일 보고서 내에서 조직의 **개요** 섹션 아래 **엔터프라이즈 응용 프로그램**합니다.

![로그인 활동](./media/active-directory-reporting-activity-sign-ins/64.png "로그인 활동")

상위 3 응용 프로그램에 대 한 기능 지정된 된 기간 동안에 로그인 하는 hello 응용 프로그램 사용 현황 그래프 주간 집계 합니다. hello에 대 한 hello 기본 기간 30 일입니다.

![로그인 활동](./media/active-directory-reporting-activity-sign-ins/47.png "로그인 활동")

원하는 경우에 특정 응용 프로그램에 hello 포커스를 설정할 수 있습니다.


![보고](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")

하루에 hello 앱 사용량 그래프를 클릭할 때 hello 로그인 활동의 자세한 목록을 가져옵니다.


![로그인 활동](./media/active-directory-reporting-activity-sign-ins/48.png "로그인 활동")


hello **로그인** 옵션 모든 로그인 이벤트 tooyour 응용 프로그램의 전체적인 개요를 제공 합니다.

![로그인 활동](./media/active-directory-reporting-activity-sign-ins/49.png "로그인 활동")



## <a name="next-steps"></a>다음 단계

로그인 활동이 오류 코드에 대 한 자세한 tooknow hello를 참조 하십시오 [로그인 활동 보고서의에서 오류 코드 hello Azure Active Directory 포털](active-directory-reporting-activity-sign-ins-errors.md)합니다.

