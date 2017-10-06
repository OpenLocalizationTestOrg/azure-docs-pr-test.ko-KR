---
title: "hello Azure 포털에서에서 보고서를 aaaFind 활동 | Microsoft Docs"
description: "Azure Active Directory 작업 toofind hello Azure 포털에서에서 보고 하는 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a>Hello Azure 포털에서에서 작업 보고서를 찾기

Azure 포털에서 Azure 클래식 포털 toohello hello 이동 하는, Azure Active Directory (Azure AD) 활동 로그에서 새로운 모양을 얻게 됩니다. 최근에서 [블로그 게시물](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), 활동에서 hello Azure 포털에서 작업 하는 hello 리소스의 hello 컨텍스트에서 로그를 볼 수는 방법을 설명 합니다. 이 문서에서는 toofind 보고 하는 hello hello Azure 포털에서에서 Azure 클래식 포털에서에서 사용 하 여는 방법을 설명 합니다.

## <a name="whats-new"></a>새로운 기능

Hello Azure 클래식 포털의에서 보고서 범주로 구분 됩니다.

1.  보안 보고서
2.  작업 보고서
3.  통합 앱 보고서

### <a name="activity-and-integrated-app-reports"></a>활동 및 통합 앱 보고서

컨텍스트 기반 hello Azure 포털에서에서 보고를 위해 기존 보고서는 단일 보기에 병합 됩니다. 단일, 기본 API hello 데이터 toohello 보기를 제공합니다.

hello에이 보기는 toosee **Azure Active Directory** 블레이드 아래에서 **활동**선택, **감사 로그**합니다.

![감사 로그](./media/active-directory-reporting-migration/482.png "감사 로그")

이 보기에서 보고서를 다음 hello 통합 됩니다.

-   감사 보고서
-   암호 재설정 활동
-   암호 재설정 등록 활동
-   셀프 서비스 그룹 작업
-   Office 365 그룹 이름 변경
-   계정 프로비전 활동
-   암호 롤오버 상태
-   계정 프로비전 오류


hello 응용 프로그램 사용 현황 보고서가 향상 되었으며 및 hello에 포함 된 **로그인** 보기. hello에이 보기는 toosee **Azure Active Directory** 블레이드 아래에서 **활동**선택, **로그인**합니다.

![로그인 보기](./media/active-directory-reporting-migration/483.png "로그인 보기")

hello **로그인** 뷰에 모든 사용자 로그인이 포함 됩니다. 이 정보 tooget 응용 프로그램 사용 정보를 사용할 수 있습니다. 또한 hello에 응용 프로그램 사용 정보를 볼 수 있습니다 **엔터프라이즈 응용 프로그램** hello에 개요 **관리** 섹션.

![Enterprise 응용 프로그램](./media/active-directory-reporting-migration/484.png "Enterprise 응용 프로그램")

## <a name="access-a-specific-report"></a>특정 보고서에 액세스

Hello Azure 포털에서는 단일 보기를 제공 하지만 또한 살펴보면 특정 보고서.

### <a name="audit-logs"></a>감사 로그

Hello Azure 포털에서에서 응답 toocustomer 피드백에 고급 필터링 tooaccess hello 원하는 데이터를 사용할 수 있습니다. 하나의 필터를 사용할 수는 *활동 범주*, Azure AD 로그인 hello 다양 한 유형의 작업을 나열 하 합니다. toonarrow 결과 대 한 원하는 toowhat, 범주를 선택할 수 있습니다.

예를 들어 활동 관련된 tooself 서비스 암호 재설정에만 관심이 경우 선택할 수 있습니다 hello **셀프 서비스 암호 관리** 범주입니다. 표시 되는 hello 범주에서 작업 하는 hello 리소스를 기반으로 합니다.  

![Hello 필터 감사 로그 페이지의 옵션 범주](./media/active-directory-reporting-migration/06.png "hello 필터 감사 로그 페이지의 옵션 범주")

작업 범주에는 다음과 같은 항목이 포함됩니다.

- 핵심 디렉터리
- 셀프 서비스 암호 관리
- 셀프 서비스 그룹 관리
- 계정 프로비전

### <a name="application-usage"></a>응용 프로그램 사용 현황

tooview 아래에서 모든 앱에 대 한 또는 단일 앱에 대 한 응용 프로그램 사용에 대 한 세부 정보 **활동**선택, **로그인**. toonarrow hello 결과 사용자 이름 또는 응용 프로그램 이름을 필터링 할 수 있습니다.

![로그인 이벤트 필터링 페이지](./media/active-directory-reporting-migration/07.png "로그인 이벤트 필터링 페이지")

### <a name="security-reports"></a>보안 보고서

#### <a name="azure-ad-anomalous-activity-reports"></a>Azure AD 비정상 작업 보고서

Azure AD의 비정상적인 활동 보안 통합된 tooprovide 된 hello Azure 클래식 포털에서에서 보고서 하나, 중앙 뷰부터 있습니다. 이 보기에는 Azure AD가 감지하여 보고할 수 있는 모든 보안 관련 위험 이벤트가 표시됩니다.

다음 표에서 hello hello Azure AD의 비정상적인 활동 보안 보고서 및 hello Azure 포털에서에서 해당 위험 이벤트 유형을 나열 합니다.

| Azure AD 비정상 작업 보고서 |  ID 보호 위험 이벤트 유형|
| :--- | :--- |
| 자격 증명이 손실된 사용자 | 유출된 자격 증명 |
| 비정상적인 로그인 작업 | 이동 불가능 tooatypical 위치 |
| 감염 가능성이 있는 장치에서 로그인 | 감염된 장치에서 로그인|
| 알 수 없는 원본에서 로그인 | 익명 IP 주소에서 로그인 |
| 의심스러운 작업이 있는 IP 주소에서 로그인 | 의심스러운 작업이 있는 IP 주소에서 로그인 |
| - | 알 수 없는 위치에서 로그인 |

Azure AD의 비정상적인 활동 보안 다음 hello 보고 hello Azure 포털의에서 위험 이벤트로 포함 되지 않습니다.

* 여러 번의 실패 후 로그인
* 여러 지역에서의 로그인

이러한 보고서는 hello Azure 클래식 포털에서에서 계속 제공 하지만 향후 hello에 중단 될 예정입니다.

자세한 내용은 [Azure Active Directory 위험 이벤트](active-directory-identity-protection-risk-events.md)를 참조하세요.  


#### <a name="detected-risk-events"></a>검색된 위험 이벤트

Hello에 검색 된 위험 이벤트에 대 한 보고서에 액세스할 수 hello Azure 포털에서에서 **Azure Active Directory** 블레이드 아래 **보안**합니다. Hello 다음 보고서에서에서 검색 된 위험 이벤트가 추적 됩니다.   

- 위험에 노출된 사용자
- 위험한 로그인

![보안 보고서](./media/active-directory-reporting-migration/04.png "보안 보고서")

보안 보고서에 대한 자세한 내용은 다음 항목을 참조하세요.

- [Hello Azure Active Directory 포털에서 위험 보안 보고서에 있는 사용자](active-directory-reporting-security-user-at-risk.md)
- [Hello Azure Active Directory 포털에서 위험한 로그인 보고서](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a>Hello hello Azure 포털 및 Azure 클래식 포털에서에서 활동 보고서

이 섹션의 표 hello hello Azure 클래식 포털에서에서 기존 보고서를 나열합니다. 또한를 가져오는 방법을 설명 hello hello Azure 포털에서에서 동일한 정보입니다.

모든 tooview hello에 데이터 감사 **Azure Active Directory** 블레이드 아래 **활동**, 너무 이동**감사 로그**합니다.

![감사 로그](./media/active-directory-reporting-migration/61.png "감사 로그")

| Azure 클래식 포털                 | toofind hello Azure 포털에서                                                         |
| ---                                  | ---                                                                        |
| 감사 로그                           | **작업 범주**로 **핵심 디렉터리**를 선택합니다.                       |
| 암호 재설정 활동              | **작업 범주**로 **셀프 서비스 암호 관리**를 선택합니다. |
| 암호 재설정 등록 활동 | **작업 범주**로 **셀프 서비스 암호 관리**를 선택합니다.     |
| 셀프 서비스 그룹 작업         | **작업 범주**로 **셀프 서비스 그룹 관리**를 선택합니다.        |
| 계정 프로비전 활동        | **작업 범주**로 **계정 사용자 프로비전**을 선택합니다.         |
| 암호 롤오버 상태             | **작업 범주**로 **자동 앱 암호 롤오버**를 선택합니다.      |
| 계정 프로비전 오류          | **작업 범주**로 **계정 사용자 프로비전**을 선택합니다.        |
| Office 365 그룹 이름 변경         | **작업 범주**로 **셀프 서비스 암호 관리**를 선택합니다. **작업 리소스 유형**으로 **그룹**을 선택합니다. **작업 원본**으로 **O365 그룹**을 선택합니다.|

tooview hello **응용 프로그램 사용** hello에 보고서 **Azure Active Directory** 블레이드 아래 **관리**선택, **엔터프라이즈 응용 프로그램**를 선택한 후 **로그인**합니다.


![Enterprise 응용 프로그램 로그인 보고서](./media/active-directory-reporting-migration/199.png "Enterprise 응용 프로그램 로그인 보고서")

## <a name="next-steps"></a>다음 단계

Reporting의 개요를 참조 hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md)합니다.
