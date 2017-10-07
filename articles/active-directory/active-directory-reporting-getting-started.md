---
title: "Azure Active Directory Reporting: 시작 | Microsoft Docs"
description: "목록 hello Azure Active Directory reporting에서 사용할 수 있는 다양 한 보고서"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: f47875708398391dd7f3efdc56a741fdba273b76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a>Azure Active Directory Reporting 시작하기
## <a name="what-it-is"></a>정의
Azure AD(Azure Active Directory)에는 디렉터리에 대한 보안, 활동 및 감사 보고서가 포함되어 있습니다. 포함 된 hello 보고서 목록은 다음과 같습니다.

### <a name="security-reports"></a>보안 보고서
* 알 수 없는 원본에서 로그인
* 여러 번의 실패 후 로그인
* 여러 지역에서의 로그인
* 의심스러운 작업이 있는 IP 주소에서 로그인
* 비정상적인 로그인 작업
* 감염 가능성이 있는 장치에서 로그인
* 비정상적인 로그인 활동을 포함하는 사용자

### <a name="activity-reports"></a>작업 보고서
* 응용 프로그램 사용: 요약
* 응용 프로그램 사용: 세부
* 응용 프로그램 대시보드
* 계정 프로비전 오류
* 개별 사용자 장치
* 개별 사용자 활동
* 그룹 활동 보고서
* 암호 재설정 등록 활동 보고서
* 암호 재설정 활동

### <a name="audit-reports"></a>감사 보고서
* 디렉터리 감사 보고서

> [!TIP]
> Azure AD Reporting에 대한 설명서에 대해서는 [액세스 및 사용 보고서 보기](active-directory-view-access-usage-reports.md)를 확인하세요.
> 
> 

## <a name="how-it-works"></a>작동 방법
### <a name="reporting-pipeline"></a>보고 파이프라인
hello 보고 파이프라인 세 개의 주요 단계로 구성 됩니다. 사용자가 로그인 또는 인증 만들어질 때마다 hello 다음과 같은 상황이 발생 합니다.

* 첫째, (성공 여부), hello 사용자가 인증 되 고 hello 결과가 hello Azure Active Directory 서비스 데이터베이스에 저장 됩니다.
* 정기적으로 최근의 모든 로그인이 처리됩니다. 이때 보안 및 비정상적인 활동 알고리즘은 최근의 모든 로그인에서 의심스러운 활동을 검색합니다.
* 처리 후 hello 보고서 작성 되, 캐시, 고 hello Azure 클래식 포털에서에서 제공 합니다.

### <a name="report-generation-times"></a>보고서 생성 시간
인증 및 서명 기능 처리 hello Azure AD 플랫폼의 toohello 큰 볼륨, 기한 hello 가장 최근 로그인 처리는 평균적으로 1 시간 전의. 드문 경우 지만 too8 시간 tooprocess hello 가장 최근 로그인을 걸릴 수 있습니다.

각 보고서의 hello 위쪽 hello 도움말 텍스트를 검사 하 여 처리 hello 가장 최근 로그인에서 찾을 수 있습니다.

![각 보고서의 위쪽 hello에 대 한 도움말 텍스트](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> Azure AD Reporting에 대한 설명서에 대해서는 [액세스 및 사용 보고서 보기](active-directory-view-access-usage-reports.md)를 확인하세요.
> 
> 

## <a name="getting-started"></a>시작
### <a name="sign-into-hello-azure-classic-portal"></a>Azure 클래식 포털 hello에 로그인
첫째, 해야 toosign hello에 [Azure 클래식 포털](https://manage.windowsazure.com) 전역 또는 규정 준수 관리자 권한으로 합니다. Azure 구독의 서비스 관리자 또는 공동 관리자 여야 하거나 hello "액세스 tooAzure AD"에 사용할 Azure 구독.

### <a name="navigate-tooreports"></a>TooReports 이동
tooview 보고서 디렉터리의 hello 위쪽 toohello 보고서 탭을 이동 합니다.

처음으로 hello 보고서를 보는 경우 hello 보고서를 볼 수 전에 tooagree tooa 대화 상자를 해야 합니다. 이 조직 tooview 관리자 임을 tooensure이이 데이터를 일부 국가에서 개인 정보 고려 될 수 있습니다.

![대화 상자](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a>각 보고서 탐색
각 보고서 toosee hello 데이터를 수집 하 고 hello 로그인 처리 합니다. 찾을 수 있습니다는 [모든 hello이 보고서의 목록](active-directory-reporting-guide.md)합니다.

![모든 보고서](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-hello-reports-as-csv"></a>Hello 보고서를 CSV로 다운로드
각 보고서를 CSV(쉼표로 구분 된 값) 파일로 다운로드할 수 있습니다. Excel, PowerBI 또는 제 3 자 분석 데이터를 분석 하는 프로그램 toofurther에서 이러한 파일을 사용할 수 있습니다.

하나의 CSV로 보고 하는 모든 toodownload toohello 보고서 이동한 hello 맨 아래에 "다운로드"를 클릭 합니다.

![다운로드 단추](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> Azure AD Reporting에 대한 설명서에 대해서는 [액세스 및 사용 보고서 보기](active-directory-view-access-usage-reports.md)를 확인하세요.
> 
> 

## <a name="next-steps"></a>다음 단계
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a>비정상적인 로그인 활동에 대한 경고 사용자 지정
Toohello "구성" 디렉터리의 탭으로 이동 합니다.

Toohello "알림" 섹션을 스크롤하십시오.

Hello "비정상적인 로그인 전자 메일 알림" 섹션을 사용 하지 않도록 설정 하거나 사용 합니다.

![hello 알림 섹션](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-hello-azure-ad-reporting-api"></a>Azure AD Reporting API hello와 통합
참조 [Reporting API hello 시작](active-directory-reporting-api-getting-started.md)합니다.

### <a name="engage-multi-factor-authentication-on-users"></a>사용자에 대해 Multi-Factor Authentication 적용
보고서에서 사용자를 선택합니다.

Hello hello 화면 맨 아래에 hello "MFA를 사용 하도록 설정" 단추를 클릭 합니다.

![hello hello 화면 맨 아래에 hello Multi-factor Authentication 단추](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> Azure AD Reporting에 대한 설명서에 대해서는 [액세스 및 사용 보고서 보기](active-directory-view-access-usage-reports.md)를 확인하세요.
> 
> 

## <a name="learn-more"></a>자세한 정보
### <a name="audit-events"></a>감사 이벤트
Hello 디렉터리에 감사 되는 이벤트에 대 한 자세한 내용은 [Azure Active Directory Reporting 감사 이벤트](active-directory-reporting-audit-events.md)합니다.

### <a name="api-integration"></a>API 통합
참조 [Reporting API hello 시작](active-directory-reporting-api-getting-started.md) 및 hello [API 참조 설명서](https://msdn.microsoft.com/library/azure/mt126081.aspx)합니다.

### <a name="get-in-touch"></a>문의하기
피드백을 제공하거나, 도움이 필요하거나, 질문이 있는 경우 [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) 으로 전자 메일을 보내세요.

> [!TIP]
> Azure AD Reporting에 대한 설명서에 대해서는 [액세스 및 사용 보고서 보기](active-directory-view-access-usage-reports.md)를 확인하세요.
> 
> 

