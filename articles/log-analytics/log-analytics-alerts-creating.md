---
title: "OMS 로그 분석에서 aaaCreating 경고 | Microsoft Docs"
description: "로그 분석에 OMS 리포지토리에 중요 한 정보를 식별 및 수 사전 문제점을 알려 경고나 작업 tooattempt toocorrect 호출을 합니다.  이 문서에서는 어떻게 toocreate 경고 규칙 및 세부 정보 hello 다양 한 작업 취할 수를 설명 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: 3d035b2426dda9645b19e6c993dc26a2d95a2a78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-alert-rules-in-log-analytics"></a>Log Analytics에서 경고 규칙 작업
경고는 일정한 간격으로 로그 검색을 자동으로 실행하는 경고 규칙에 의해 만들어집니다.  hello 결과 특정 조건과 일치 하는 경우 경고는 레코드를 만듭니다.  hello 규칙 수 후 자동으로 하나를 실행 하거나 더 많은 작업 tooproactively hello 경고의 알림을 또는 다른 프로세스를 호출 합니다.   

이 문서는 hello 프로세스 toocreate에 설명 하 고 hello OMS 포털을 사용 하 여 경고 규칙을 편집 합니다.  Hello 다양 한 설정 및 tooimplement 논리 필요한 하는 방법에 대 한 세부 정보를 참조 하십시오. [로그 분석에서 경고 이해](log-analytics-alerts.md)합니다.

>[!NOTE]
> 현재 만들 하거나 hello Azure 포털을 사용 하 여 경고 규칙을 수정할 수 없습니다. 

## <a name="create-an-alert-rule"></a>경고 규칙 만들기

로그를 만들어 시작 hello OMS 포털을 사용 하 여 경고 규칙을 toocreate hello 경고를 호출 해야 하는 hello 레코드를 검색 합니다.  hello **경고** 만들고 hello 경고 규칙을 구성할 수 있도록 단추를 한 다음 사용할 수 있습니다.

>[!NOTE]
> 현재 OMS 작업 영역에서 최대 250개의 경고 규칙을 만들 수 있습니다. 

1. Hello OMS 개요 페이지에서 클릭 **로그 검색**합니다.
2. 새 로그 검색 쿼리를 만들거나 저장된 로그 검색을 선택합니다. 
3. 클릭 **경고** hello 페이지 tooopen hello의 hello 위쪽 **경고 규칙 추가** 화면입니다.
4. 구성 정보를 사용 하는 hello 경고 규칙 [경고 규칙의 세부 정보](#details-of-alert-rules) 아래 합니다.
6. 클릭 **저장** toocomplete hello 경고 규칙입니다.  실행을 즉시 시작합니다.


## <a name="edit-an-alert-rule"></a>경고 규칙 편집
Hello에서 모든 경고 규칙의 목록을 가져올 수 있습니다 **경고** 로그 분석에서 메뉴 **설정을**합니다.  

![경고 관리](./media/log-analytics-alerts/configure.png)

1. Hello OMS 콘솔 선택 hello에 **설정** 바둑판식으로 배열입니다.
2. **경고**를 선택합니다.

이 뷰에서 여러 작업을 수행할 수 있습니다.

* 규칙을 사용 하지 않도록 선택 하 여 **오프** 다음 tooit 합니다.
* Hello 연필 아이콘 다음 tooit를 클릭 하 여 경고 규칙을 편집 합니다.
* Hello를 클릭 하 여 경고 규칙을 제거할 **X** 다음 tooit 아이콘입니다. 

## <a name="details-of-alert-rules"></a>경고 규칙의 세부 정보
Hello를 사용 하 여 작업할 만들거나 hello OMS 포털의 경고 규칙을 편집할 때 **경고 규칙 추가** 또는 **경고 규칙 편집** 페이지.  다음 표에서 hello hello 필드가이 화면에 설명 합니다.

![경고 규칙](media/log-analytics-alerts/add-alert-rule.png)

### <a name="alert-information"></a>경고 정보
이 hello 경고 규칙 및 생성 하는 hello 경고에 대 한 기본 설정.

| 속성 | 설명 |
|:--- |:---|
| 이름 | 고유 이름 tooidentify hello 경고 규칙입니다. 이 이름은 hello 규칙에 의해 생성 된 모든 경고에 포함 됩니다.  |
| 설명 | Hello 경고 규칙의 선택적 설명입니다. |
| 심각도 |이 규칙에 의해 생성된 모든 경고의 심각도입니다. |

### <a name="search-query-and-time-window"></a>검색 쿼리 및 기간
모든 경고를 생성 하면 평가 toodetermine 있는 hello 레코드를 반환 하는 hello 검색 쿼리 및 시간 창.

| 속성 | 설명 |
|:--- |:---|
| 검색 쿼리 | 이것은 실행 되는 hello 쿼리입니다.  이 쿼리에서 반환 된 hello 레코드 경고가 만들어지고 여부를 사용 하는 toodetermine 됩니다.<br><br>선택 **현재 검색 쿼리 사용** toouse 현재 쿼리 hello 하거나 기존에 저장 된 검색 hello 목록에서 선택 합니다.  hello 쿼리 구문은 수정할 수 있는 필요한 경우 hello 텍스트 상자에 제공 됩니다. |
| 기간 |Hello 쿼리에 대 한 hello 시간 범위를 지정합니다.  hello 쿼리는 현재 시간 hello이이 범위 내에서 생성 된 레코드만 반환 합니다.  이는 5 분에서 24 시간 사이의 임의 값일 수 있습니다.  알림 빈도 보다 크거나 같은 toohello 이어야 합니다.  <br><br> 예를 들어 hello too60 분과 hello 쿼리 창을 설정 된 시간에 실행 된 경우 오후 1 시 15 분 오후 12시 15분와 오후 1시 15분 사이 레코드만 반환 됩니다. |

Hello 경고 규칙에 대 한 hello 기간을 지정할 때는 hello 해당 기간에 대 한 hello 검색 조건과 일치 하는 기존 레코드 수가 표시 됩니다.  제공 하는 hello 빈도 확인할 수 있습니다이 hello 예상 되는 결과의 수입니다.

### <a name="schedule"></a>일정
Hello 검색 쿼리는 실행 빈도 정의 합니다.

| 속성 | 설명 |
|:--- |:---|
| 경고 빈도 | 얼마나 자주 hello 쿼리 실행 되도록 지정 합니다. 5 분에서 24 시간 사이의 임의 값일 수 있습니다. Hello 기간 보다 작은 tooor 동일 해야 합니다.  Hello 값 hello 기간 보다 큰 경우 레코드가 누락 될 위험이 있습니다.<br><br>예를 들어 30분의 기간과 60분의 빈도를 사용하는 것이 좋습니다.  Hello 쿼리 1:00에 실행 된 경우 오후 12시 30분 1시 사이 레코드를 반환 합니다.  hello는 hello 쿼리는 실행 하는 다음에 2:00 때 1시 30분 2시 사이 레코드를 반환 합니다.  1:00 및 1:30 사이에 생성된 레코드는 평가되지 않습니다. |


### <a name="generate-alert-based-on"></a>경고 생성 조건
Hello 평가 되는 경우 경고 hello 검색 쿼리 toodetermine의 hello 결과 대해 링크 조건을 생성할 수를 정의 합니다.  이러한 세부 사항을 선택 하는 경고 규칙의 hello 유형에 따라 달라 집니다.  다른 경고 규칙 유형을 hello에 대 한 세부 정보를 얻을 수 있습니다 [로그 분석에서 경고 이해](log-analytics-alerts.md)합니다.

| 속성 | 설명 |
|:--- |:---|
| 알림 표시 안 함 | 억제 (suppression) hello 경고 규칙에 대 한을 설정 하면 새 경고를 만든 후 정의 된 기간에 대 한 hello 규칙에 대 한 작업을 사용할 수 없게 됩니다. hello 규칙 실행 되 고 hello 조건을 충족할 경우 경고 레코드를 만듭니다. 중복 작업을 실행 하지 않고 toocorrect hello 문제 시간 tooallow입니다. |

#### <a name="number-of-results-alert-rules"></a>결과 수 경고 규칙

| 속성 | 설명 |
|:--- |:---|
| 결과의 수 |Hello hello 쿼리에서 반환 된 레코드 수가 경고가 만들어지고 **보다 큰** 또는 **미만** hello 값을 제공 합니다.  |

#### <a name="metric-measurement-alert-rules"></a>미터법 경고 규칙

| 속성 | 설명 |
|:--- |:---|
| 집계 값 | Hello 결과의 각 집계 값 toobe를 초과 해야 하는 임계값 위반으로 간주 합니다. |
| 경고 트리거 조건 | hello 생성 하는 경고 toobe에 대 한 위반 수입니다.  지정할 수 있습니다 **위반 총** hello 결과에서 즘 조합에 대 한 설정 또는 **연속 위반** 위반 hello toorequire 연속 샘플에서 발생 해야 합니다. |

### <a name="actions"></a>작업
경고 규칙을 항상 만듭니다는 [레코드 경고](#alert-records) hello 임계값을 충족 하는 경우.  또한 정의할 수 있습니다 또는 전자 메일을 보낼 runbook 시작 등 자세한 응답 toobe 실행 합니다.



#### <a name="email-actions"></a>전자 메일 작업
전자 메일 작업 hello 경고 tooone 또는 더 많은 수신자 한 hello 세부 정보가 포함 된 전자 메일을 보냅니다.

| 속성 | 설명 |
|:--- |:---|
| 메일 알림 |지정 **예** hello 경고가 트리거될 때 전송 되는 전자 메일 toobe 하려는 경우. |
| 제목 |Hello 전자 메일의 제목입니다.  Hello 메일의 본문 hello를 수정할 수 없습니다. |
| 받는 사람 |모든 전자 메일 받는 사람의 주소입니다.  세미콜론 (;)를 사용 하 여 여러 개의 주소가 다음 별도 hello 주소를 지정 합니다. |

#### <a name="webhook-actions"></a>웹후크 작업
Webhook 작업 tooinvoke 단일 HTTP POST 요청을 통해 외부 프로세스를 허용 합니다.

| 속성 | 설명 |
|:--- |:---|
| 웹후크 |지정 **예** hello 경고가 트리거될 때 toocall 여 webhook을 사용할지를 선택 합니다. |
| Webhook URL |hello webhook의 hello URL입니다. |
| 사용자 지정 JSON 페이로드 포함 |사용자 지정 페이로드를 사용한 tooreplace hello 기본 페이로드를 원하는 경우이 옵션을 선택 합니다. |
| 사용자 지정 JSON 페이로드 입력 |hello hello webhook에 대 한 사용자 지정 페이로드입니다.  자세한 내용은 이전 섹션을 참조하세요. |

#### <a name="runbook-actions"></a>Runbook 작업
Runbook 작업은 Azure 자동화에서 Runbook을 시작합니다. 

>[!NOTE]
> Hello 자동화 솔루션이이 동작 toobe 사용에 대 한 작업 영역에 설치 되어 있어야 합니다. 


| 속성 | 설명 |
|:--- |:---|
| Runbook | 지정 **예** hello 경고가 트리거될 때 toostart Azure 자동화 runbook을 선택 합니다.  |
| Automation 계정 | Hello runbook에서 선택 된 자동화 계정을 지정 합니다.  연결 된 작업 영역 toohello hello 작업 계정입니다. |
| Runbook 선택 | 경고를 만들 때 않겠다고 toostart hello runbook을 선택 합니다. |
| 실행 | 선택 **Azure** hello 클라우드에서 toorun hello runbook입니다.  선택 **Hybrid worker** 와 에이전트에서 toorun hello runbook [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) 설치 합니다.  |




## <a name="next-steps"></a>다음 단계
* Hello 설치 [경고 관리 솔루션](log-analytics-solution-alert-management.md) tooanalyze 경고 경고와 함께 로그 분석에서 만든 System Center Operations Manager (SCOM)에서 수집 합니다.
* 경고를 생성할 수 있는 [로그 검색](log-analytics-log-searches.md) 에 대해 자세한 내용을 읽습니다.
* 경고 규칙을 사용하여 [웹후크를 구성](log-analytics-alerts-webhooks.md) 하는 연습을 완료합니다.  
* 자세한 내용은 어떻게 toowrite [Azure 자동화의 runbook](https://azure.microsoft.com/documentation/services/automation) tooremediate 문제를 경고로 식별 합니다.

