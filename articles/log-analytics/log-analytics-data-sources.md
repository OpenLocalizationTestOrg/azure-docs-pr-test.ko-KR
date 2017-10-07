---
title: "OMS 로그 분석에서 데이터 원본을 aaaConfigure | Microsoft Docs"
description: "로그 분석 수집 에이전트 및 기타에서 연결 된 원본 hello 데이터를 정의 하는 데이터 원본.  이 문서 로그 분석 데이터 소스를 사용 하는 방법의 hello 개념을 설명, hello 방법 자세히 설명 tooconfigure, 사용 가능한 hello 서로 다른 데이터 원본에 대 한 요약을 제공 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 67710115-c861-40f8-a377-57c7fa6909b4
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: ebe8d29a2442a654b98004f624181ff406868e2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-in-log-analytics"></a>Log Analytics의 데이터 원본
OMS 작업 영역에서 hello 연결 된 원본에서 데이터를 수집 하 고 OMS 리포지토리에 저장 하는 로그 분석 합니다.  hello 수집 된 데이터를 각각 hello 구성 하는 데이터 원본으로 정의 됩니다.  Hello OMS 리포지토리에서 데이터를에서 레코드 집합으로 저장 됩니다.  각 데이터 원본은 각각 고유한 속성 집합이 있는 특정 유형의 레코드를 만듭니다.

![Log Analytics 데이터 수집](./media/log-analytics-data-sources/overview.png)

데이터 소스는 또한 연결 된 원본에서 데이터를 수집 하 고 hello OMS 저장소에서 레코드를 작성 하는 OMS 솔루션 다릅니다.  솔루션은 hello 솔루션 갤러리에서에서 tooyour 작업 영역을 추가할 수 있으며, 일반적으로 hello OMS 포털에서 추가 분석 도구를 제공 합니다.  

## <a name="summary-of-data-sources"></a>데이터 원본 요약
현재 로그 분석에 사용할 수 있는 hello 데이터 소스는 다음 표에 hello에 나열 됩니다.  각 해당 데이터 원본에 대 한 세부 정보를 제공 하는 링크 tooa 별도 문서를 있습니다.

| 데이터 원본 | 이벤트 유형 | 설명 |
|:--- |:--- |:--- |
| [사용자 지정 로그](log-analytics-data-sources-custom-logs.md) |\<LogName\>_CL |로그 정보가 포함된 Windows 또는 Linux 에이전트의 텍스트 파일. |
| [Windows 이벤트 로그](log-analytics-data-sources-windows-events.md) |이벤트 |Hello 이벤트 로그에서 Windows 컴퓨터에서 이벤트를 수집 합니다. |
| [Windows 성능 카운터](log-analytics-data-sources-performance-counters.md) |Perf |Windows 컴퓨터에서 수집한 성능 카운터. |
| [Linux 성능 카운터](log-analytics-data-sources-performance-counters.md) |Perf |Linux 컴퓨터에서 수집한 성능 카운터. |
| [IIS 로그](log-analytics-data-sources-iis-logs.md) |W3CIISLog |W3C 형식의 IIS(인터넷 정보 서비스) 로그. |
| [Syslog](log-analytics-data-sources-syslog.md) |syslog |Windows 또는 Linux 컴퓨터의 Syslog 이벤트. |

## <a name="configuring-data-sources"></a>데이터 원본 구성
Hello에서 데이터 원본을 구성한 **데이터** 로그 분석에서 메뉴 **설정을**합니다.  모든 구성에는 OMS 작업 영역에서 연결 된 tooall 소스 배달 됩니다.  현재 이 구성에서 에이전트를 제외할 수는 없습니다.

![Windows 이벤트 구성](./media/log-analytics-data-sources/configure-events.png)

1. Hello OMS 콘솔에서 클릭 hello **설정** 타일 또는 hello **설정을** hello hello 화면 위쪽에 단추입니다.
2. **데이터**를 선택합니다.
3. 데이터 원본 tooconfigure hello 클릭 합니다.
4. 해당 구성에 대 한 자세한 내용은 테이블 위에 hello의 각 데이터 원본에 대 한 hello 링크 toohello 설명서에 따라.

> [!NOTE]
> 현재 hello Azure 포털에서에서 로그 분석 데이터 소스를 구성할 수 없습니다.

## <a name="data-collection"></a>데이터 수집
데이터 원본 구성에는 몇 분 내에 있는 직접 연결 된 tooLog 분석 tooagents를 배달 됩니다.  hello는 데이터 hello 에이전트에서 수집 되 고 배달 tooLog 분석 간격으로 특정 tooeach 데이터 소스에 직접 지정 합니다.  이러한 세부 사항에 대 한 각 데이터 원본에 대 한 hello 설명서를 참조 하십시오.

System Center Operations Manager (SCOM) 에이전트 키 연결된 된 관리 그룹에 대 한 데이터 원본 구성은 관리 팩으로 변환 되며 기본적으로 5 분 마다 toohello 관리 그룹을 제공 합니다.  hello 에이전트 같은 다른 관리 팩 hello를 다운로드 하 고 지정 된 데이터를 hello를 수집 합니다. 데이터 소스 hello hello에 따라 데이터 보내지거나 hello 데이터 toohello 로그 분석 전달 tooa 관리 서버 인지 또는 hello 에이전트는 hello 관리 서버를 통해 이동 하지 않고도 hello 데이터 tooLog 분석을 전송 전송 합니다. 너무 참조[OMS 기능 및 솔루션에 대 한 데이터 수집 정보](log-analytics-add-solutions.md#data-collection-details) 대 한 자세한 내용은 합니다.  해당 구성을 SCOM을 OMS를 연결 하 고 hello 빈도 수정에 대 한 세부 정보에 대 한 읽을 수 있습니다에 배달 [System Center Operations Manager와의 통합 구성](log-analytics-om-agents.md)합니다.

Hello 에이전트 수 없습니다 tooconnect tooLog 분석 또는 Operations Manager 이면 연결을 설정할 때 제공 하는 toocollect 데이터 계속 됩니다.  데이터의 양을 hello hello 클라이언트에 대 한 hello 최대 캐시 크기에 도달 하면 또는 hello 에이전트가 수 tooestablish 24 시간 내에 연결 되지 않으면 데이터가 손실 될 수 있습니다.

## <a name="log-analytics-records"></a>Log Analytics 레코드
로그 분석에 의해 수집 된 모든 데이터는 레코드로 hello OMS 리포지토리에 저장 됩니다.  여러 데이터 원본에서 수집된 레코드는 고유한 속성 집합이 있으며 해당 **Type** 속성으로 식별됩니다.  각 레코드 종류에 각 데이터 원본에 대 한 hello 설명서 및 세부 정보에 대 한 솔루션을 참조 하십시오.

## <a name="next-steps"></a>다음 단계
* 에 대 한 자세한 내용은 [솔루션](log-analytics-add-solutions.md) 기능 tooLog 분석을 추가 하 고 hello OMS 리포지토리에 데이터를 수집할 수도 있습니다.
* 에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) tooanalyze hello 데이터가 데이터 원본 및 솔루션에서 수집 합니다.  
* 구성 [경고](log-analytics-alerts.md) tooproactively 솔루션 및 데이터 원본에서 수집 하는 중요 한 데이터의 알려 줍니다.
