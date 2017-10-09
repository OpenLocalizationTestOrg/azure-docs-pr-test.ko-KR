---
title: "로그 분석에서 Azure 자동화 Runbook 작업 aaaUser 시작 | Microsoft Docs"
description: "이 문서 toorun 로그 분석에서 자동화 runbook 요청 시 결과 검색 하는 방법에 대해 설명 합니다."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 53c25431572babd5fd54bf964e4683077e2a4c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="take-action-with-an-automation-runbook-from-a-log-analytics-log-search-result"></a>Log Analytics 로그 검색 결과에서 Automation Runbook으로 작업 수행

Azure 로그 분석에는 로그 검색 결과에서 선택할 수 있습니다 **조치** toorun 자동화 runbook입니다.  hello runbook 있습니다 사용할 tooremediate 문제 hello 또는 수집 문제 해결 정보 등의 다른 작업 수행, 전자 메일 보내기 또는 서비스 요청을 만듭니다. 

## <a name="components-and-features-used"></a>사용된 구성 요소 및 기능
* [Azure Automation 계정](../automation/automation-offering-get-started.md)
* [Log Analytics 작업 영역](../log-analytics/log-analytics-overview.md)

## <a name="tooinitiate-runbook-from-log-search"></a>로그 검색에서 tooinitiate runbook

로그 검색을 만들어 시작 이벤트 및 로그 검색 결과에서 runbook 시작 tootake 작업, 및 hello 결과에서 요청 시 runbook을 호출할 수 있습니다.  Hello Azure의에서 hello 로그 검색 기능에서 수행할 수 있습니다 또는 [OMS 포털](../log-analytics/log-analytics-log-searches.md)합니다.  이 예제에서는 hello이 기능의 기본 시연 Azure 포털에서 로그 검색을 수행합니다.

1. Hello Azure 포털의에서 hello 허브 메뉴에서 클릭 **더 많은 서비스** 선택 **로그 분석**합니다.  
2. Hello 로그 분석 블레이드에서 로그 분석 작업 영역을 선택 하 고 hello 작업 영역 블레이드 선택 **로그 검색**합니다.  
3. Hello 로그 검색 블레이드에서 로그 검색을 수행 합니다.  
4. Hello 로그 검색 결과에서 hello 타원 toohello 왼쪽의 hello 팝업 들어오고 hello 필드 중 하나를 클릭 **에 조치로**합니다.<br><br> ![검색 결과에서 작업 수행 선택](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png) 
5. Hello Take 작업 블레이드에서 선택 **runbook을 실행**, 등과 hello **runbook을 실행** 블레이드 runbook toorun를 선택할 수 있습니다.  자동화 계정에 연결 된 toohello 로그 분석 작업 영역으로 hello에서 모든 runbook을 선택할 수 있습니다.  참고 hello 다음.

    * Runbook은 태그로 구성됩니다.
    * Runbook 입력된 매개 변수 값은 hello 검색 결과의 hello 필드에서 직접 선택할 수 있습니다.  드롭다운 목록에서 결과 tooselect hello에서에서 모든 hello 사용 가능한 필드 표시 표시 됩니다.  
    * Toorun hello runbook에서 선택할 수 있습니다는 [하이브리드 runbook 작업자](../automation/automation-hybrid-runbook-worker.md) 을 구성원으로이 컴퓨터에만 포함 하는 해당 Hybrid Runbook Worker 그룹이 있는 경우 hello 문제는 hello 컴퓨터에 설치 해야 합니다.  Hello 로그 검색 결과에 있는 hello 컴퓨터의 hello 이름과 일치 하는 hello Hybrid Worker 그룹의 hello 이름, hello 그룹이 자동으로 선택 됩니다.    

6. 클릭 한 후 **실행**, hello runbook 작업 블레이드 tooallow 열립니다 있습니다 tooreview hello 작업의 상태 hello 합니다.   

Runbook 구성된 toobe을 선택 하는 경우 [로그 분석 경고를 통해 호출](../automation/automation-invoke-runbook-from-omsla-alert.md), 라는 입력된 매개 변수가 **WebhookData** 즉 **개체** 유형입니다.  Hello 입력된 매개 변수가 필수인 경우 해야 toopass hello 검색 결과 toohello runbook 때문에 JSON 형식의 문자열 hello runbook 작업에서 참조 하는 특정 항목에 toofilter를 허용 하는 개체 형식으로 변환할 수 있습니다.  선택 하 여이 작업을 수행 **검색 결과 (Object)** hello 드롭 다운 목록에서 합니다.<br><br> ![Runbook 매개 변수에 대한 웹후크 데이터 개체 선택](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)   
    
## <a name="next-steps"></a>다음 단계

* 검토 hello [로그 분석 로그 검색 참조](log-analytics-search-reference.md) tooview hello의 모든 필드 및 패싯 로그 분석에서 사용할 수를 검색 합니다.
* 자동화 runbook tooinvoke 자동으로 방법을 검토 toolearn [OMS 로그 분석 경고에서 Azure 자동화 runbook을 호출](../automation/automation-invoke-runbook-from-omsla-alert.md)합니다.  
