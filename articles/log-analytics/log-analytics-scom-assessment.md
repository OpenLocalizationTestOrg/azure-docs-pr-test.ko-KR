---
title: "aaaOptimize Azure 로그 분석으로 System Center Operations Manager 환경 | Microsoft Docs"
description: "System Center Operations Manager 평가 솔루션 tooassess 일정 한 간격으로 위험 및 상태를 서버 환경 hello hello를 사용할 수 있습니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: tysonn
ms.assetid: 49aad8b1-3e05-4588-956c-6fdd7715cda1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c024e53826e91524c120bdb98ae7d96d6dc37d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-environment-with-hello-system-center-operations-manager-assessment-preview-solution"></a>Hello System Center Operations Manager 평가 (미리 보기) 솔루션으로 환경 최적화

![System Center Operations Manager 평가 기호](./media/log-analytics-scom-assessment/scom-assessment-symbol.png)

System Center Operations Manager 평가 솔루션 tooassess 일정 한 간격으로 위험 및 상태를 System Center Operations Manager 서버 환경의 hello hello를 사용할 수 있습니다. 이 문서에서는 설치, 구성 및 솔루션 hello를 사용 하 여 잠재적인 문제에 대 한 수정 동작을 수행할 수 있도록 합니다.

이 솔루션은 권장 사항 특정 tooyour 배포 된 서버 인프라의 우선 순위 목록을 제공 합니다. hello 권장 사항은 신속 하 게 하는 데 있는 영역 이해 위험 hello 수정 작업을 수행 하는 4 개의 포커스도 분류 됩니다.

hello 권장 hello 지식과 수천 고객 방문에서에서 Microsoft 엔지니어가 얻은 경험을 기반으로 합니다. 각 권장 사항은 문제가 tooyou에 중요할 수 있는 이유 및 tooimplement hello 변경 내용을 제안 하는 방법에 대 한 지침을 제공 합니다.

가장 중요 한 tooyour 조직 되어 하 여 위험이 없는 정상 환경을 실행 하기 위한 진행률을 추적 하는 주요 영역을 선택할 수 있습니다.

Hello에 중점 영역에 대 한 정보를 표시 한 평가 결과 완료 된, 요약 hello 솔루션을 추가한 후 **System Center Operations Manager 평가** 인프라에 대 한 대시보드 합니다. hello 다음 섹션에서는 설명 toouse hello에 대 한 정보를 hello 방법을 **System Center Operations Manager 평가** 대시보드를 보고 하 고 취할 수 있는 권장 SCOM 인프라에 대 한 작업입니다.

![System Center Operations Manager 솔루션 타일](./media/log-analytics-scom-assessment/scom-tile.png)

![System Center Operations Manager 평가 대시보드](./media/log-analytics-scom-assessment/scom-dashboard01.png)

## <a name="installing-and-configuring-hello-solution"></a>설치 하 고 hello 솔루션 구성

hello 솔루션이 Microsoft 시스템 Operations Manager 2012 R2 및 2012 s p 1에 적용 됩니다.

다음 정보 tooinstall hello를 사용 하 고 hello 솔루션을 구성 합니다.

 - OMS에서 평가 솔루션을 사용 하려면 먼저 hello 솔루션이 설치 되어 있어야 합니다. 설치에서 솔루션을 hello [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) 또는 hello 지침에 따라 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.

 - Hello 솔루션 toohello 작업 영역을 추가한 후 hello 대시보드의 hello System Center Operations Manager 평가 타일 hello 추가 구성이 필요한 메시지를 표시 합니다. Hello 타일을 클릭 하 고 hello 페이지에 언급 된 hello 구성 단계를 수행 합니다.

 ![System Center Operations Manager 대시보드 타일](./media/log-analytics-scom-assessment/scom-configrequired-tile.png)

 Hello System Center Operations Manager의 구성 hello 구성 페이지의 hello 솔루션을 OMS에 언급 된 hello 단계를 수행 하 여 hello 스크립트를 통해 수행할 수 있습니다.

 대신, 아래에 따라 hello SCOM 콘솔을 통해 tooconfigure hello 평가 단계 hello에 동일 주문
1. [System Center Operations Manager 평가 대 한 hello 계정으로 실행 계정 설정](#operations-manager-run-as-accounts-for-oms)  
2. [Hello System Center Operations Manager 평가 규칙 구성](#configure-the-assessment-rule)

## <a name="system-center-operations-manager-assessment-data-collection-details"></a>System Center Operations Manager 평가 데이터 수집 세부 정보

System Center Operations Manager 평가 hello WMI 데이터, 레지스트리 데이터, 이벤트 로그 데이터, Windows PowerShell, SQL 쿼리, 사용 하도록 설정한 hello 서버를 사용 하 여 파일 정보 수집기를 통해 Operations Manager 데이터를 수집 합니다.

hello 다음 표에서 데이터 수집 방법과 System Center Operations Manager 평가 대 한 얼마나 자주 에이전트에서 데이터를 수집 합니다.

| 플랫폼 | 직접 에이전트 | SCOM 에이전트 | Azure 저장소 | SCOM 필요? | 관리 그룹을 통해 전송되는 SCOM 에이전트 데이터 | 수집 빈도 |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | | | | &#8226; | | 7일 |

## <a name="operations-manager-run-as-accounts-for-oms"></a>OMS용 Operations Manager 실행 계정

Tooprovide 워크 로드에 대 한 관리 팩에서 빌드를 OMS는 부가 가치 서비스. 각 작업은 도메인 계정과 같은 다른 보안 컨텍스트에서 작업 관련 권한이 toorun 관리 팩 필요 합니다. Operations Manager 계정으로 실행 계정 tooprovide 자격 증명 정보를 구성 합니다.

다음 정보 tooset System Center Operations Manager 평가 대 한 Operations Manager 실행 계정을 hello hello를 사용 합니다.

### <a name="set-hello-run-as-account"></a>집합 hello 실행 계정

1. Operations Manager 콘솔 hello 이동 toohello **관리** 탭 합니다.
2. Hello에서 **실행 구성**, 클릭 **계정**합니다.
3. Hello 실행 계정, hello Windows 계정 만들기 마법사를 통해 다음을 만듭니다. hello 계정 toouse hello 식별 하나 및 모든 hello 다음과 같은 전제 조건 것입니다.

    >[!NOTE]
    hello 실행 계정은 다음 요구 사항을 충족 해야 합니다.
    - Hello hello 환경 (모든 Operations Manager 역할-관리 서버, OpsMgr 데이터베이스, 데이터 웨어하우스, 보고, 웹 콘솔, 게이트웨이)에서 모든 서버에서 로컬 관리자 그룹의 도메인 계정 멤버
    - 평가 중인 hello 관리 그룹에 대 한 작업 Manager 관리자 역할
    - Hello 실행 [스크립트](#sql-script-to-grant-granular-permissions-to-the-run-as-account) toogrant Operations Manager에서 사용 하는 SQL 인스턴스에서 toohello 계정 세분화 된 사용 권한.
      참고:이 계정에 sysadmin 권한이 이미 건너뜁니다 hello 스크립트 실행.

4. **배포 보안**에서 **More secure**(보다 안전)을 선택합니다.
5. Hello 관리 서버 hello 계정을 배포할 위치를 지정 합니다.
3. 실행 구성 toohello 돌아가서 클릭 **프로필**합니다.
4. Hello에 대 한 검색 *SCOM 평가 프로필*합니다.
5. hello 프로필 이름 이어야 합니다: *Microsoft System Center Advisor SCOM 평가 실행 프로필*합니다.
6. 마우스 오른쪽 단추로 클릭 하 고 해당 속성을 업데이트 실행 계정 3 단계에서 만든를 최근에 만든 hello에 추가 합니다.

### <a name="sql-script-toogrant-granular-permissions-toohello-run-as-account"></a>SQL 스크립트 toogrant 세부적인 권한 toohello 실행 계정

Hello SQL 스크립트 toogrant 필요한 사용 권한을 toohello 실행 계정이 Operations Manager에서 사용 하는 hello SQL 인스턴스에서 다음을 실행 합니다.

```
-- Replace <UserName> with hello actual user name being used as Run As Account.
USE master

-- Create login for hello user, comment this line if login is already created.
CREATE LOGIN [UserName] FROM WINDOWS


--GRANT permissions toouser.
GRANT VIEW SERVER STATE too[UserName]
GRANT VIEW ANY DEFINITION too[UserName]
GRANT VIEW ANY DATABASE too[UserName]

-- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
-- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
EXEC sp_msforeachdb N'USE [?]; CREATE USER [UserName] FOR LOGIN [UserName];'

Use msdb
GRANT SELECT too[UserName]
Go

--Give SELECT permission on all Operations Manager related Databases

--Replace hello Operations Manager database name with hello one in your environment
Use [OperationsManager];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager DatawareHouse database name with hello one in your environment
Use [OperationsManagerDW];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager Audit Collection database name with hello one in your environment
Use [OperationsManagerAC];
GRANT SELECT too[UserName]
GO

--Give db_owner on [OperationsManager] DB
--Replace hello Operations Manager database name with hello one in your environment
USE [OperationsManager]
GO
ALTER ROLE [db_owner] ADD MEMBER [UserName]

```


### <a name="configure-hello-assessment-rule"></a>Hello 평가 규칙 구성

System Center Operations Manager 평가 솔루션의 관리 팩 규칙을 포함 hello *Microsoft System Center Advisor SCOM 평가 평가 규칙 실행*합니다. 이 규칙은 hello 평가 실행 합니다. tooenable 규칙 hello 및 hello 빈도 사용 하 여 hello 아래 절차를 구성 합니다.

기본적으로 hello Microsoft System Center Advisor SCOM 평가 실행 평가 규칙을 사용 하는 사용할 수 없습니다. toorun hello 평가, 관리 서버에 hello 규칙을 활성화 해야 합니다. 단계를 수행 하는 hello를 사용 합니다.

#### <a name="enable-hello-rule-for-a-specific-management-server"></a>특정 관리 서버에 대 한 hello 규칙을 사용 하도록 설정

1. Hello에 **제작** hello 규칙에 대 한 검색 hello Operations Manager 콘솔의 작업 영역 *Microsoft System Center Advisor SCOM 평가 평가 규칙 실행* hello에 **규칙** 창.
2. Hello 검색 결과에서 선택 hello 텍스트를 포함 하는 hello *유형: 관리 서버*합니다.
3. Hello 규칙을 마우스 오른쪽 단추로 누른 **재정의** > **클래스의 특정 개체: 관리 서버**합니다.
4.  Hello 사용 가능한 관리 서버 목록에 hello 규칙 실행 해야 하는 hello 관리 서버를 선택 합니다.
5.  재정의 값을 너무 변경 해야**True** hello에 대 한 **Enabled** 매개 변수 값입니다.  
    ![재정의 매개 변수](./media/log-analytics-scom-assessment/rule.png)

이 창에 여전히 동안 hello hello hello 다음 절차를 사용 하 여 실행 빈도 구성 합니다.

#### <a name="configure-hello-run-frequency"></a>Hello 실행 빈도 구성 합니다.

hello 평가 모든 10, 080 분 (또는 7 일), 구성 된 toorun hello 기본 간격입니다. Hello 값 tooa 1440 분 (또는 1 일)의 최소 값을 재정의할 수 있습니다. hello 값 연속 평가 실행 사이 필요한 hello 최소 시간 간격을 나타냅니다. toooverride hello 간격을 사용 하 여 hello 다음 단계를 수행 합니다.

1. Hello에 **제작** hello 규칙에 대 한 검색 hello Operations Manager 콘솔의 작업 영역 *Microsoft System Center Advisor SCOM 평가 평가 규칙 실행* hello에 **규칙** 창.
2. Hello 검색 결과에서 선택 hello 텍스트를 포함 하는 hello *유형: 관리 서버*합니다.
3. Hello 규칙을 마우스 오른쪽 단추로 누른 **재정의 hello 규칙** > **클래스의 모든 개체: 관리 서버**합니다.
4. 변경 hello **간격** 매개 변수 값 tooyour 원하는 간격 값입니다. Hello 아래 예제에서는 hello 값은 설정 too1440 분 (1 일)입니다.  
    ![간격 매개 변수](./media/log-analytics-scom-assessment/interval.png)  
    Hello 값 1440 분 보다 tooless 설정 되 면 hello 규칙 1 일 간격으로 실행 합니다. 이 예제에서는 hello 규칙 hello 간격 값을 무시 하 고 1 일의 주파수로 실행 합니다.


## <a name="understanding-how-recommendations-are-prioritized"></a>권장 사항 우선 순위 이해

작성 된 모든 권장 hello hello 권장 사항의 상대적 중요도 식별 하는 가중치 값을 제공 됩니다. Hello 10 가장 중요 한 권장 구성만 표시 됩니다.

### <a name="how-weights-are-calculated"></a>가중치 계산 방법

가중치는 3개의 주요 요인을 기반으로 하는 집계 값입니다.

- hello *확률* 식별 된 문제로 인해 문제가 발생 될 합니다. 더 높은 확률을 tooa hello 권장 사항의 전체 점을 수도 높아집니다.
- hello *영향* 문제가 발생 하는 경우 조직에 hello 문제입니다. 영향이 높을수록 tooa hello 권장 사항의 전체 점을 수도 높아집니다.
- hello *노력* tooimplement hello 권장 구성이 필요 합니다. 노력이 높을수록 tooa 전체 점수가 작아집니다 hello 권장 사항에 대 한 것과 같습니다.

각 권장 사항에 대 한 가중치 hello은 각 주요 영역에 대해 사용할 수 있는 총 점수 hello에 대 한 백분율로 표현 됩니다. 예를 들어 hello 가용성 및 비즈니스 연속성 중점 영역 권장 사항 점수가 5%가 있으면 해당 권장 사항을 구현 전체 가용성 및 비즈니스 연속성 점수에서 5% 증가 합니다.

### <a name="focus-areas"></a>주요 영역

**가용성 및 비즈니스 연속성** - 이 주요 영역은 서비스 가용성, 인프라 복원성 및 비즈니스 보호에 대한 권장 사항을 보여 줍니다.

**성능 및 확장성** -이 포커스 영역 표시 권장 사항을 toohelp 조직의 IT 인프라 증가, IT 환경의 현재 성능 요구 사항을 충족 하며 수 toorespond toochanging 있는지 확인 하십시오 인프라 필요합니다.

**업그레이드, 마이그레이션 및 배포** -이 포커스 영역 표시 권장 사항을 toohelp 업그레이드, 마이그레이션 및 SQL Server tooyour 기존 인프라를 배포 합니다.

**작업 및 모니터링** -이 포커스 영역 표시 권장 사항을 toohelp 약식 IT 운영을 예방 유지 관리를 구현 하 고 성능을 최대화 합니다.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>목표로 해야 tooscore 모든 중점 영역에서 100%?

그럴 필요는 없습니다. hello 권장 사항은 hello 지식과 수천 고객 방문에서 Microsoft 엔지니어가 얻은 경험을 기반으로 합니다. 그러나 서버 인프라는 동일 hello 및 특정 권장 사항의 관련성이 더 높을 tooyou 수 있습니다. 예를 들어 일부 보안 권장 사항의 관련성이 낮이 노출된 toohello 인터넷 없으면 가상 컴퓨터 수 있습니다. 일부 가용성 권장 사항은 우선순위가 낮은 임시 데이터 수집 및 보고를 제공하는 서비스와는 관련성이 떨어질 수 있습니다. 성숙한 비즈니스에 중요 한 tooa 문제도 tooa 시작에 덜 중요할 수 있습니다. 수 tooidentify 우선 하는 주요 영역을 다음 점수가 시간에 따라 어떻게 변경 되는지 확인 합니다.

모든 권장 사항에는 중요한 이유에 대한 지침이 포함됩니다. 이 지침 tooevaluate를 사용 하 여 hello 권장 사항 구현에 적절 한지, 조직의 IT 서비스 및 hello 비즈니스 요구의 hello 특성을 제공 합니다.

## <a name="use-assessment-focus-area-recommendations"></a>평가 주요 영역 권장 사항 사용

OMS에서 평가 솔루션을 사용 하려면 먼저 hello 솔루션이 설치 되어 있어야 합니다. 솔루션 설치에 대 한 더 tooread 참조 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다. 설치 된 후 OMS의 개요 페이지 hello에 hello System Center Operations Manager 평가 타일을 사용 하 여 hello 권장 사항 요약을 볼 수 있습니다.

보기 hello 인프라와 다음 권장 사항에 주입할에 대 한 호환성 평가 요약 되어 있습니다.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>포커스 영역과 take 해결 작업에 대 한 tooview 권장 사항

1. Hello에 **개요** 페이지에서 hello **System Center Operations Manager 평가** 바둑판식으로 배열입니다.
2. Hello에 **System Center Operations Manager 평가** 페이지 hello 중점 영역 블레이드 중 하나에 hello 요약 정보를 검토 한 다음 하나 해당 주요 영역에 대 한 권장 사항을 tooview를 클릭 합니다.
3. Hello 주요 영역 페이지에서 사용자 환경에 대 한 우선 순위를 지정 하는 hello 권장 사항을 볼 수 있습니다. 권장 클릭 **영향을 받는 개체** hello 권장 사항을 따르면 이유에 대 한 자세한 내용을 tooview 합니다.  
    ![주요 영역](./media/log-analytics-scom-assessment/focus-area.png)
4. **권장 조치**에 제안된 올바른 조치를 수행할 수 있습니다. Hello 항목 해결 되 면 이후 평가 기록 동작이 수행 되었습니다 및 규정 준수 점수를 권장 합니다. 수정된 항목은 **전달된 개체**로 나타납니다.

## <a name="ignore-recommendations"></a>권장 사항 무시

권장 사항을 tooignore 원하는 설정한 경우에 OMS 평가 결과에 나타나지 않도록 tooprevent 권장 사항을 사용 하는 텍스트 파일을 만들 수 있습니다.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-want-tooignore"></a>원하는 tooignore tooidentify 권장 사항

1. Tooyour 작업 영역에 로그인 하 고 로그 검색을 엽니다. 사용자 환경의 컴퓨터에 대 한 실패 한 쿼리 toolist 권장 사항을 따르면 hello를 사용 합니다.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

    표시 된 스크린 샷 hello 로그 검색 쿼리는 다음과 같습니다.  
    ![로그 검색](./media/log-analytics-scom-assessment/scom-log-search.png)

2. 권장 tooignore 되도록 선택 합니다. Hello 다음 절차에서 RecommendationId에 대 한 hello 값을 사용 합니다.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>IgnoreRecommendations.txt 텍스트 파일을 사용 하 여 toocreate

1. IgnoreRecommendations.txt라는 파일을 만듭니다.
2. 붙여넣거나 OMS tooignore 별도 줄에 원하는 하 고 저장 하 고 hello 파일을 닫고 각 권장 사항에 대 한 각 RecommendationId를 입력 합니다.
3. Hello 파일을 hello OMS tooignore 권장 사항을 원하는 각 컴퓨터에서 폴더를 다음에 넣습니다.
4. Hello Operations Manager 관리 서버- *SystemDrive*: files\microsoft System Center 2012 R2\Operations Manager\Server 합니다.

### <a name="tooverify-that-recommendations-are-ignored"></a>권장 사항이 무시 되는지 tooverify

1. 기본적으로 7 일 간격 hello 예약 된 다음 평가 실행 된 후 권장 사항은 무시 됨으로 표시 되 고 hello 평가 대시보드에 표시 되지 것입니다 hello 지정 합니다.
2. 다음 로그 검색 쿼리 toolist hello 모든 무시 하는 hello 권장 사항을 사용할 수 있습니다.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

3. 나중에 권장 사항을 무시 toosee 한다고 결정 하면 IgnoreRecommendations.txt 파일을 제거 하거나 Recommendationid를 제거할 수 있습니다.

## <a name="system-center-operations-manager-assessment-solution-faq"></a>System Center Operations Manager 평가 솔루션 FAQ

*Hello 평가 솔루션 toomy OMS 작업 영역을 추가 했습니다. 하지만 hello 권장 사항 표시 되지 않습니다. 이유* Hello 솔루션을 추가한 후 hello OMS 대시보드에서 단계 보기에 대 한 hello 권장 사항을 따르면 hello를 사용 합니다.  

- [System Center Operations Manager 평가 대 한 hello 계정으로 실행 계정 설정](#operations-manager-run-as-accounts-for-oms)  
- [Hello System Center Operations Manager 평가 규칙 구성](#configure-the-assessment-rule)


*이 방식으로 tooconfigure 얼마나 자주 hello 평가 실행 있습니까?* 예. 참조 [실행 빈도 구성 hello](#configure-the-run-frequency)합니다.

*System Center Operations Manager 평가 솔루션 hello 추가한 후 다른 서버가 발견 되 면이 서버를 평가?* 예, 검색된 이후 기본적으로 7일마다 평가됩니다.

*데이터 수집을 hello는 hello 프로세스의 hello 이름은 무엇입니까?* AdvisorAssessment.exe

*Hello AdvisorAssessment.exe 프로세스를 실행 하나요?* AdvisorAssessment.exe는 hello 평가 규칙이 활성화 되어 hello hello 관리 서버의 health Service에서 실행 됩니다. 이 프로세스를 사용하는 경우 전체 환경에 대한 검색은 원격 데이터 수집을 통해 수행됩니다.

*데이터 수집에 시간이 얼마나 걸리나요?* Hello 서버에서 데이터 수집에는 약 1 시간이 걸립니다. Operations Manager 인스턴스 또는 데이터베이스가 많은 환경에서는 더 오래 걸릴 수 있습니다.

*경우에 어떻게 1440 분 보다 hello 평가 tooless의 hello 간격 설정 해야 합니까?*  hello 평가 하루에 한 번의 최대는 미리 구성 된 toorun 됩니다. Hello 간격 값 tooa 값을 1440 분 안에 재정의할 hello 평가 hello 간격 값으로 분을 사용 합니다.

*어떻게 tooknow 필수 구성 요소 오류가 발생 하는 경우?* Hello 평가 실행 하는 경우 결과 표시 되지 않으면 다음 되었을 일부 hello hello 평가 대 한 필수 구성 요소 실패 했습니다. 쿼리를 실행할 수 있습니다: `Type=Operation Solution=SCOMAssessment` 및 `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` 로그 검색 toosee hello에 필수 구성 요소 실패 했습니다.

*필수 구성 요소 오류에 `Failed tooconnect toohello SQL Instance (….).` 메시지가 있습니다. Hello 문제는 무엇입니까?* AdvisorAssessment.exe, 데이터를 수집 하는 hello 프로세스 hello hello 관리 서버의 health Service에서 실행 됩니다. Hello 평가의 일부로 hello 프로세스 tooconnect toohello hello Operations Manager 데이터베이스는 존재 하는 SQL Server를 시도 합니다. 방화벽 규칙 hello 연결 toohello SQL Server 인스턴스를 차단 하는 경우이 오류가 발생할 수 있습니다.

*어떤 유형의 데이터를 수집 하나요?*  hello 데이터 형식에 따라 수집 됩니다: Windows PowerShell, SQL 쿼리 및 파일 정보 수집기를 통해 WMI-데이터 요금-레지스트리 데이터-이벤트 로그 데이터 요금-Operations Manager 데이터입니다.

*Tooconfigure 실행 계정으로 있는 이유* Operations Manager 서버의 경우 다양한 SQL 쿼리가 실행됩니다. 해당 템플릿을 toorun, 실행 계정을 사용 하 여 필요한 권한을 부여 해야 합니다. 또한 로컬 관리자 자격 증명이 필요한 tooquery WMI 합니다.

*왜 hello 상위 10 개의 권장 사항만 표시 하나요?* 작업의 완전 한 목록이 고 부담이 된 목록을 제공 하는 대신 먼저 hello 우선 순위가 지정 된 권장 사항 해결에 주의 기울여야 하는 것이 좋습니다. 권장 사항을 해결한 후에 추가 권장 사항을 사용할 수 있습니다. Toosee hello에 대 한 자세한 목록을 원하는 경우 로그 검색을 사용 하 여 모든 권장 사항을 볼 수 있습니다.

*방식으로 tooignore 권장 사항은 무엇입니까?* 예, hello 참조 [권장 구성은 무시할](#Ignore-recommendations)합니다.


## <a name="next-steps"></a>다음 단계

- [로그 검색](log-analytics-log-searches.md) tooview System Center Operations Manager 평가 데이터 및 권장 사항을 설명 합니다.
