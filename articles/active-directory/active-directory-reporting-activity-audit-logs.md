---
title: "hello Azure Active Directory 포털에서 aaaAudit 활동 보고 | Microsoft Docs"
description: "소개 toohello 감사 hello Azure Active Directory 포털에서 활동 보고서"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a>감사 hello Azure Active Directory 포털에서 활동 보고서 

Azure Active Directory (Azure AD)에 보고를 사용 하면 환경의 어떻게 진행 되는 toodetermine 필요한 hello 정보를 얻을 수 있습니다.

Azure AD의 보고 아키텍처 hello hello 다음과 같은 구성 요소가 구성 되어 있습니다.

- **활동** 
    - **로그인 활동** – 관리 되는 응용 프로그램 및 사용자 로그인 활동의 hello 사용에 대 한 정보
    - **감사 로그** - 사용자 및 그룹 관리, 관리되는 응용 프로그램 및 디렉터리 활동에 대한 시스템 작업 정보
- **보안** 
    - **위험한 로그인** -위험한 로그인이 사용자 계정의 hello 정당한 소유자가 아닌 사용자에 의해 수행 된 로그인 시도에 대 한 표시기입니다. 자세한 내용은 위험한 로그인을 참조하세요.
    - **위험 플래그가 지정된 사용자** - 위험한 사용자는 손상되었을 수 있는 사용자 계정에 대한 표시기입니다. 자세한 내용은 위험 플래그가 지정된 사용자를 참조하세요.

이 항목에서는 hello 감사 작업의 개요를 제공 합니다.
 
## <a name="who-can-access-hello-data"></a>Hello 데이터에 액세스할 수 있는 사용자?
* Hello 보안 판독기 또는 보안 관리자 역할의 사용자
* 전역 관리자
* 개별 사용자(비관리자)는 자신의 활동을 볼 수 있습니다.


## <a name="audit-logs"></a>감사 로그

Azure Active Directory에 hello 감사 로그는 규정 준수에 대 한 시스템 활동의 레코드를 제공합니다.  
데이터 감사 하 여 첫 번째 항목 지점 tooall는 **감사 로그** hello에 **활동** 섹션 **Azure Active Directory**합니다.

![감사 로그](./media/active-directory-reporting-activity-audit-logs/61.png "감사 로그")

감사 로그에는 다음 항목을 보여 주는 기본 목록 보기가 있습니다.

- hello 발생의 hello 날짜 및 시간
- 초기자 hello / 행위자 (*가*) 활동 
- 활동 hello (*어떤*) 
- hello 대상

![감사 로그](./media/active-directory-reporting-activity-audit-logs/18.png "감사 로그")

클릭 하 여 hello 목록 보기를 사용자 지정할 수 있습니다 **열** hello 도구 모음에서입니다.

![감사 로그](./media/active-directory-reporting-activity-audit-logs/19.png "감사 로그")

이 toodisplay 추가 필드를 사용 하면 하거나 이미 표시 되는 필드를 제거 합니다.

![감사 로그](./media/active-directory-reporting-activity-audit-logs/21.png "감사 로그")


Hello 목록 뷰에서 항목을 클릭 하 여 항목에 대 한 모든 사용 가능한 세부 정보를 가져옵니다.

![감사 로그](./media/active-directory-reporting-activity-audit-logs/22.png "감사 로그")


## <a name="filtering-audit-logs"></a>감사 로그 필터링

hello 아래로 toonarrow 데이터 tooa 수준 수에 대 한 작동을 필터링 할 수 필드를 다음 hello를 사용 하 여 hello 감사 데이터를 보고.

- 날짜 범위
- 초기자(작업자)
- Category
- 활동 리소스 종류
- 작업

![감사 로그](./media/active-directory-reporting-activity-audit-logs/23.png "감사 로그")


hello **날짜 범위** 필터 사용 tooyou toodefine hello에 대 한 시간 범위는 데이터를 반환 합니다.  
가능한 값은 다음과 같습니다.

- 1개월
- 7 일
- 24시간
- 사용자 지정

사용자 지정 시간 범위를 선택하면 시작 시간과 종료 시간을 구성할 수 있습니다.

hello **에 의해 시작** 필터를 사용 하면 있습니다 toodefine 행위자의 이름 또는 유니버설 보안 주체 이름 (UPN)입니다.

hello **범주** 필터를 사용 하면 다음 필터는 hello의 tooselect 하나:

- 모두
- 핵심 범주
- 핵심 디렉터리
- 셀프 서비스 암호 관리
- 셀프 서비스 그룹 관리
- 계정 프로비전 - 자동화된 암호 롤오버
- 사용자 초대
- MIM 서비스
- ID 보호
- B2C

hello **활동 리소스 종류** 필터를 사용 하면 tooselect hello 다음 중 하나를 필터링 합니다.

- 모두 
- 그룹
- 디렉터리
- 사용자
- 응용 프로그램
- 정책
- 장치
- 기타

선택 하는 경우 **그룹** 으로 **활동 리소스 종류**, 수 있는 추가 필터 범주 tooalso를 얻게 제공는 **소스**:

- Azure AD
- O365


hello **활동** 필터 hello 범주 및 작업 리소스 유형 선택한 내용에 기반 합니다. Toosee 모두 선택 하거나 특정 활동을 선택할 수 있습니다. 

Graph API https://graph.windows.net/$ hello tenantdomain/활동/auditActivityTypes를 사용 하 여 모든 감사 활동의 hello 목록을 가져올 수 있습니까? api 버전 = beta, 여기서 $tenantdomain = 도메인 이름 또는 toohello 문서를 참조 [감사 보고서 이벤트](active-directory-reporting-audit-events.md)합니다.


## <a name="audit-logs-shortcuts"></a>감사 로그 바로 가기

또한 너무**Azure Active Directory**, hello Azure 포털을 제공 두 개의 추가 진입점 tooaudit 데이터:

- 개요
- Enterprise 응용 프로그램

### <a name="users-and-groups-audit-logs"></a>사용자 및 그룹 감사 로그

사용자와 그룹 기반 감사 보고서를 같은 tooquestions 답변을 얻을 수 있습니다.

- 어떤 종류의 업데이트 된 사용자가 적용 된 hello?

- 얼마나 많은 사용자가 변경되었나요?

- 얼마나 많은 암호가 변경되었나요?

- 관리자가 디렉터리에서 무엇을 수행했나요?

- 추가 된 hello 그룹 이란?

- 멤버 자격이 변경된 그룹이 있나요?

- 변경 된 그룹의 소유자 hello?

- 어떤 라이선스 tooa 그룹 또는 사용자 지정 된?

아래에 있는 필터링 된 보기를 찾을 수 tooreview 감사 관련된 toousers 및 그룹 데이터를 원하는 경우 **감사 로그** hello에 **활동** hello의 섹션 **사용자 및 그룹**. 이 진입점에는 미리 선택된 **활동 리소스 종류**로 **사용자 및 그룹**이 있습니다.

![감사 로그](./media/active-directory-reporting-activity-audit-logs/93.png "감사 로그")

### <a name="enterprise-applications-audit-logs"></a>Enterprise 응용 프로그램 감사 로그

응용 프로그램을 기반으로 감사 보고서를 같은 tooquestions 답변을 얻을 수 있습니다.

* 추가 되거나 업데이트 된 하는 hello 응용 프로그램은 무엇입니까?
* 제거 된 hello 응용 프로그램은 무엇입니까?
* 응용 프로그램에 대한 서비스 원칙이 변경되었나요?
* 응용 프로그램의 hello 이름은 변경 되었습니다.
* 누가 동의 tooan 응용 프로그램을 줬?

아래에 있는 필터링 된 보기를 찾을 수 tooreview 관련된 tooyour 응용 프로그램은 데이터 감사를 원하는 경우 **감사 로그** hello에 **활동** hello의 섹션 **엔터프라이즈 응용 프로그램**  블레이드입니다. 이 진입점에는 미리 선택된 **활동 리소스 종류**인 **엔터프라이즈 응용 프로그램**이 있습니다.

![감사 로그](./media/active-directory-reporting-activity-audit-logs/134.png "감사 로그")

Toojust 아래로 더 이상이 보기를 필터링 할 수 있습니다 **그룹** 또는 그냥 **사용자**합니다.

![감사 로그](./media/active-directory-reporting-activity-audit-logs/25.png "감사 로그")


## <a name="next-steps"></a>다음 단계

Reporting의 개요를 참조 hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md)합니다.

