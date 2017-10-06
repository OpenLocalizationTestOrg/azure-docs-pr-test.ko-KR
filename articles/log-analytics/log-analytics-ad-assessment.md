---
title: "aaaOptimize Azure 로그 분석으로 Active Directory 환경 | Microsoft Docs"
description: "Active Directory 평가 솔루션 tooassess 일정 한 간격으로 위험 및 상태를 서버 환경 hello hello를 사용할 수 있습니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 81eb41b8-eb62-4eb2-9f7b-fde5c89c9b47
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 63290d95302a9e1d243cd993ac50556ed42b97bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-active-directory-environment-with-hello-active-directory-assessment-solution-in-log-analytics"></a>Hello 로그 분석에서 Active Directory 평가 솔루션으로 Active Directory 환경 최적화

![AD 평가 기호](./media/log-analytics-ad-assessment/ad-assessment-symbol.png)

Active Directory 평가 솔루션 tooassess 일정 한 간격으로 위험 및 상태를 서버 환경 hello hello를 사용할 수 있습니다. 이 문서에서는 설치 하 고 잠재적인 문제에 대 한 수정 동작을 수행할 수 있도록 hello 솔루션을 사용 합니다.

이 솔루션은 권장 사항 특정 tooyour 배포 된 서버 인프라의 우선 순위 목록을 제공 합니다. hello 권장 사항은 신속 하 게 하는 데 있는 영역 위험 hello 한 조치를 이해 하는 4 개의 포커스도 분류 됩니다.

hello 권장 사항은 hello 지식과 수천 고객 방문에서에서 Microsoft 엔지니어가 얻은 경험을 기반으로 합니다. 각 권장 사항은 문제가 tooyou에 중요할 수 있는 이유 및 tooimplement hello 변경 내용을 제안 하는 방법에 대 한 지침을 제공 합니다.

가장 중요 한 tooyour 조직 되어 하 여 위험이 없는 정상 환경을 실행 하기 위한 진행률을 추적 하는 주요 영역을 선택할 수 있습니다.

Hello에 중점 영역에 대 한 정보를 표시 한 평가 결과 완료 된, 요약 hello 솔루션을 추가한 후 **AD 평가** hello 사용자 환경의 인프라에에서 대 한 대시보드 합니다. hello 다음 섹션에서는 설명 toouse hello에 대 한 정보를 hello 방법을 **AD 평가** 대시보드를 보고 하 고 취할 수 있는 권장 Active Directory 서버 인프라에 대 한 작업입니다.

![SQL 평가 타일의 이미지](./media/log-analytics-ad-assessment/ad-tile.png)

![SQL 평가 대시보드의 이미지](./media/log-analytics-ad-assessment/ad-assessment.png)

## <a name="installing-and-configuring-hello-solution"></a>설치 하 고 hello 솔루션 구성
다음 정보 tooinstall hello를 사용 하 고 hello 솔루션을 구성 합니다.

* 에이전트는 평가 hello 도메인 toobe의 구성원 인 도메인 컨트롤러에 설치 되어야 합니다.
* Active Directory 평가 솔루션에 필요한 지원 되는 버전의.NET Framework 4 hello (4.5.2 이상을) OMS 에이전트가 각 컴퓨터에 설치 합니다.
* Hello Active Directory 평가 솔루션 tooyour OMS 작업 영역에서 추가 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview) 또는에 설명 된 hello 프로세스를 사용 하 여 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.  추가 구성은 필요 없습니다.

  > [!NOTE]
  > Hello 솔루션을 추가한 후 에이전트와 함께 tooservers hello AdvisorAssessment.exe 파일에 추가 됩니다. 구성 데이터를 읽고 처리를 위해 hello 클라우드에서 toohello OMS 서비스로 전송 됩니다. 논리는 수신 적용된 toohello 데이터 및 hello 클라우드 서비스는 hello 데이터를 기록 합니다.
  >
  >

## <a name="active-directory-assessment-data-collection-details"></a>Active Directory 평가 데이터 수집 정보

Active Directory 평가 hello를 사용 하도록 설정한 hello 에이전트를 사용 하 여 원본에서 데이터를 수집 합니다.

- 레지스트리 수집기
- LDAP 수집기
- .NET Framework
- 이벤트 로그 수집기
- ADSI(Active Directory 서비스 인터페이스)
- Windows PowerShell
- 파일 데이터 수집기
- WMI(Windows Management Instrumentation)
- DCDIAG 도구 API
- NTFRS(파일 복제 서비스) API
- 사용자 지정 C# 코드


hello 다음 표에서 데이터 수집 방법과 에이전트, Operations Manager (SCOM)가 필요한 지 여부와 방법을 에이전트에서 주로 데이터를 수집 합니다.

| 플랫폼 | 직접 에이전트 | SCOM 에이전트 | Azure 저장소 | SCOM 필요? | 관리 그룹을 통해 전송되는 SCOM 에이전트 데이터 | 수집 빈도 |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |7 일 |

## <a name="understanding-how-recommendations-are-prioritized"></a>권장 사항 우선 순위 이해
작성 된 모든 권장 hello hello 권장 사항의 상대적 중요도 식별 하는 가중치 값을 제공 됩니다. Hello 10 가장 중요 한 권장 구성만 표시 됩니다.

### <a name="how-weights-are-calculated"></a>가중치 계산 방법
가중치는 3개의 주요 요인을 기반으로 하는 집계 값입니다.

* hello *확률* 식별 하는 문제를 유발 합니다. 더 높은 확률을 tooa hello 권장 사항의 전체 점을 수도 높아집니다.
* hello *영향* 문제가 발생 하는 경우 조직에 hello 문제입니다. 영향이 높을수록 tooa hello 권장 사항의 전체 점을 수도 높아집니다.
* hello *노력* tooimplement hello 권장 구성이 필요 합니다. 노력이 높을수록 tooa 전체 점수가 작아집니다 hello 권장 사항에 대 한 것과 같습니다.

각 권장 사항에 대 한 가중치 hello은 각 주요 영역에 대해 사용할 수 있는 총 점수 hello에 대 한 백분율로 표현 됩니다. 예를 들어 hello 보안 및 규정 준수 주요 영역의 권장 사항 점수가 5%가 있으면 해당 권장 사항을 구현 전체 보안 및 규정 준수 점수에서 5% 증가 합니다.

### <a name="focus-areas"></a>주요 영역
**보안 및 규정 준수** - 이 주요 영역은 잠재적 보안 위협 및 위반, 회사 정책, 기술, 법률 및 규정 준수 요구 사항 등에 대한 권장 사항을 보여 줍니다.

**가용성 및 비즈니스 연속성** - 이 주요 영역은 서비스 가용성, 인프라 복원성 및 비즈니스 보호에 대한 권장 사항을 보여 줍니다.

**성능 및 확장성** -이 포커스 영역 표시 권장 사항을 toohelp 조직의 IT 인프라 증가, IT 환경의 현재 성능 요구 사항을 충족 하며 수 toorespond toochanging 있는지 확인 하십시오 인프라 필요합니다.

**업그레이드, 마이그레이션 및 배포** -이 포커스 영역 표시 권장 사항을 toohelp 업그레이드, 마이그레이션 및 Active Directory tooyour 기존 인프라를 배포 합니다.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>목표로 해야 tooscore 모든 중점 영역에서 100%?
그럴 필요는 없습니다. hello 권장 사항은 hello 지식과 수천 고객 방문에서 Microsoft 엔지니어가 얻은 경험을 기반으로 합니다. 그러나 서버 인프라는 동일 hello 및 특정 권장 사항의 관련성이 더 높을 tooyou 수 있습니다. 예를 들어 일부 보안 권장 사항의 관련성이 낮이 노출된 toohello 인터넷 없으면 가상 컴퓨터 수 있습니다. 일부 가용성 권장 사항은 우선순위가 낮은 임시 데이터 수집 및 보고를 제공하는 서비스와는 관련성이 떨어질 수 있습니다. 성숙한 비즈니스에 중요 한 tooa 문제도 tooa 시작에 덜 중요할 수 있습니다. 수 tooidentify 우선 하는 주요 영역을 다음 점수가 시간에 따라 어떻게 변경 되는지 확인 합니다.

모든 권장 사항에는 중요한 이유에 대한 지침이 포함됩니다. Hello 권장 사항 구현에 적절 한지, 조직의 IT 서비스 및 hello 비즈니스 요구의 hello 특성을 지정 된이 지침 tooevaluate를 사용 해야 합니다.

## <a name="use-assessment-focus-area-recommendations"></a>평가 주요 영역 권장 사항 사용
OMS에서 평가 솔루션을 사용 하려면 먼저 hello 솔루션이 설치 되어 있어야 합니다. 솔루션 설치에 대 한 더 tooread 참조 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다. 설치 된 후 OMS의 개요 페이지 hello에 hello 평가 타일을 사용 하 여 hello 권장 사항 요약을 볼 수 있습니다.

보기 hello 인프라와 다음 권장 사항에 주입할에 대 한 호환성 평가 요약 되어 있습니다.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>포커스 영역과 take 해결 작업에 대 한 tooview 권장 사항
1. Hello에 **개요** 페이지에서 hello **평가** 서버 인프라에 대 한 바둑판식으로 배열 합니다.
2. Hello에 **평가** 페이지 hello 중점 영역 블레이드 중 하나에 hello 요약 정보를 검토 한 다음 하나 해당 주요 영역에 대 한 권장 사항을 tooview를 클릭 합니다.
3. Hello 주요 영역 페이지에서 사용자 환경에 대 한 우선 순위를 지정 하는 hello 권장 사항을 볼 수 있습니다. 권장 클릭 **영향을 받는 개체** hello 권장 사항을 따르면 이유에 대 한 자세한 내용을 tooview 합니다.  
    ![평가 권장 사항의 이미지](./media/log-analytics-ad-assessment/ad-focus.png)
4. **권장 조치**에 제안된 올바른 조치를 수행할 수 있습니다. Hello 항목 해결 되 면 권장 되는 작업 하는 이후 평가 레코드 수행 되었습니다 및 준수 점수가 높아집니다. 수정된 항목은 **전달된 개체**로 나타납니다.

## <a name="ignore-recommendations"></a>권장 사항 무시
권장 사항을 tooignore 원하는 설정한 경우에 OMS 평가 결과에 나타나지 않도록 tooprevent 권장 사항을 사용 하는 텍스트 파일을 만들 수 있습니다.

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>tooidentify 권장 사항이 무시 합니다
1. Tooyour 작업 영역에 로그인 하 고 로그 검색을 엽니다. 사용자 환경의 컴퓨터에 대 한 실패 한 쿼리 toolist 권장 사항을 따르면 hello를 사용 합니다.

   ```
   Type=ADAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 쿼리 위에 hello toohello 다음 변경 합니다.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Failed" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

   표시 된 스크린 샷 hello 로그 검색 쿼리는 다음과 같습니다: ![권장 구성 하지 못했습니다.](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)
2. 권장 tooignore 되도록 선택 합니다. Hello 다음 절차에서 RecommendationId에 대 한 hello 값을 사용 합니다.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>IgnoreRecommendations.txt 텍스트 파일을 사용 하 여 toocreate
1. IgnoreRecommendations.txt라는 파일을 만듭니다.
2. 붙여 넣거나 로그 분석 tooignore 별도 줄에 원하는 하 고 저장 하 고 hello 파일을 닫고 각 권장 사항에 대 한 각 RecommendationId를 입력 합니다.
3. Hello 파일을 hello OMS tooignore 권장 사항을 원하는 각 컴퓨터에서 폴더를 다음에 넣습니다.
   * Microsoft Monitoring Agent (직접 또는 Operations Manager를 통해 연결)-hello로 컴퓨터에 *SystemDrive*: files\microsoft Monitoring Agent\Agent
   * Hello Operations Manager 관리 서버- *SystemDrive*: files\microsoft System Center 2012 R2\Operations Manager\Server

### <a name="tooverify-that-recommendations-are-ignored"></a>권장 사항이 무시 되는지 tooverify
Hello 기본적으로 7 일 간격 hello 예약 된 다음 평가 실행 된 후 권장 사항으로 표시 된 지정 된 *무시* hello 평가 대시보드에 표시 되지 것입니다.

1. 다음 로그 검색 쿼리 toolist hello 모든 무시 하는 hello 권장 사항을 사용할 수 있습니다.

    ```
    Type=ADAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```
>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 쿼리 위에 hello toohello 다음 변경 합니다.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Ignored" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

2. 나중에 권장 사항을 무시 toosee 한다고 결정 하면 IgnoreRecommendations.txt 파일을 제거 하거나 Recommendationid를 제거할 수 있습니다.

## <a name="ad-assessment-solutions-faq"></a>AD 평가 솔루션 FAQ
*얼마나 자주 평가를 실행하나요?*

* hello 평가 7 일 마다 실행 됩니다.

*이 방식으로 tooconfigure 얼마나 자주 hello 평가 실행 있습니까?*

* 지금은 없습니다.

*평가 솔루션을 추가한 후 다른 서버가 발견되면, 이 서버를 평가하나요?*

* 예, 발견되면 그 시간부터 7일마다 평가됩니다.

*서버 서비스를 해제 하 고 언제 수 제거 hello 평가에서?*

* 3주 동안 서버가 데이터를 전송하지 않은 경우 제거 됩니다.

*데이터 수집을 hello는 hello 프로세스의 hello 이름은 무엇입니까?*

* AdvisorAssessment.exe

*가 소요 데이터 toobe 수집에 대 한?*

* hello 서버의 hello 실제 데이터 수집은 약 1 시간이 걸립니다. Active Directory 서버가 많은 서버에서는 더 오래 걸릴 수 있습니다.

*방식으로 tooconfigure 데이터를 수집 하는 경우 무엇입니까?*

* 지금은 없습니다.

*왜 hello 상위 10 개의 권장 사항만 표시 하나요?*

* 작업의 포함 된 긴 목록을 제공 하는 대신 먼저 hello 우선 순위가 지정 된 권장 사항 해결에 주의 기울여야 하는 것이 좋습니다. 권장 사항을 해결한 후에 추가 권장 사항을 사용할 수 있습니다. Toosee hello에 대 한 자세한 목록을 원하는 경우 로그 검색을 사용 하 여 모든 권장 사항을 볼 수 있습니다.

*방식으로 tooignore 권장 사항은 무엇입니까?*

* 예, 위의 [권장 사항 무시](#ignore-recommendations) 섹션을 참조하세요.

## <a name="next-steps"></a>다음 단계
* 사용 하 여 [로그 분석 검색 로그인](log-analytics-log-searches.md) AD 평가 데이터와 권장 tooview 자세히 설명 합니다.
