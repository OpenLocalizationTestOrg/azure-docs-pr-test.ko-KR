---
title: "aaaOMSManagement 솔루션에 대 한 유용한 정보 | Microsoft Docs"
description: 
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 08cf1c101e301d24fb5c2bf4bc02a978e508a198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-management-solutions-in-operations-management-suite-oms-preview"></a>OMS(Operations Management Suite)(미리 보기)의 관리 솔루션 만들기 모범 사례
> [!NOTE]
> 현재 Preview로 제공되는 OMS의 사용자 지정 솔루션 만들기에 대한 예비 설명서입니다. 아래에 설명 된 모든 스키마 주체 toochange입니다.  

이 문서에서는 OMS(Operations Management Suite)에서 [관리 솔루션 파일 만들기](operations-management-suite-solutions-solution-file.md)에 대한 모범 사례를 제공합니다.  이 정보는 추가 모범 사례가 있으면 업데이트됩니다.

## <a name="data-sources"></a>데이터 원본
- 데이터 원본은 [Resource Manager 템플릿을 사용하여 구성](../log-analytics/log-analytics-template-workspace-configuration.md)할 수 있으나 솔루션 파일에 포함되지 않아야 합니다.  hello는 데이터 원본을 구성 하는 하지 현재 idempotent 솔루션 hello 사용자 작업 영역에서 기존 구성을 덮어쓸 수 있는지를 의미 합니다.<br><br>예를 들어 솔루션 hello 응용 프로그램 이벤트 로그에서 경고 및 오류 이벤트를 할 수 있습니다.  을 지정 하면이 데이터 원본으로 솔루션에 정보 이벤트를 제거 하 여 hello 사용자에 게이 작업 영역에 구성 된 경우 발생할 수 있습니다.  모든 이벤트를 포함 하는 경우 다음 있습니다 수 과도 한 정보 이벤트 수집 hello 사용자 작업 영역에서 합니다.

- 솔루션 hello 표준 데이터 원본 중 하나에서 데이터가 필요한 경우 그런 다음 정의 해야이 필수 구성 요소.  설명서에 상태 해당 hello 고객 hello 데이터 원본을 구성 해야 자체적으로 합니다.  
- 추가 [데이터 흐름 확인](../log-analytics/log-analytics-view-designer-tiles.md) tooany에 뷰 솔루션 tooinstruct hello 사용자 데이터 원본에 필요한 데이터 toobe에 대해 구성 필요 toobe 해당 메시지를 수집 합니다.  이 메시지는 필요한 데이터를 찾을 수 hello 보기의 hello 타일에 표시 됩니다.


## <a name="runbooks"></a>Runbook
- 추가 [자동화 일정](../automation/automation-schedules.md) toorun 일정에 따라 필요한 솔루션의 각 runbook에 대 한 합니다.
- Hello 포함 [IngestionAPI 모듈](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) toohello 로그 분석 저장소 데이터를 작성 하는 runbook에서 사용 하 여 솔루션 toobe에 있습니다.  너무 hello 솔루션 구성[참조](operations-management-suite-solutions-solution-file.md#solution-resource) 이 리소스를 hello 솔루션 제거 되 게 합니다.  따라서 여러 솔루션 tooshare hello 모듈을 수 있습니다.
- 사용 하 여 [자동화 변수](../automation/automation-schedules.md) tooprovide 값 toohello 솔루션 사용자 toochange를 나중에 사용할 수 있습니다.  Hello 솔루션에 구성 된 toocontain hello 변수가, 경우에 해당 값도 변경할 수 있습니다.

## <a name="views"></a>뷰
- 모든 솔루션 hello 사용자 포털에 표시 되는 단일 뷰를 포함 해야 합니다.  hello 보기 수 다 수 포함할 [시각화 부분](../log-analytics/log-analytics-view-designer-parts.md) tooillustrate 서로 다른 데이터 집합입니다.
- 추가 [데이터 흐름 확인](../log-analytics/log-analytics-view-designer-tiles.md) tooany에 뷰 솔루션 tooinstruct hello 사용자 데이터 원본에 필요한 데이터 toobe에 대해 구성 필요 toobe 해당 메시지를 수집 합니다.
- 너무 hello 솔루션 구성[포함](operations-management-suite-solutions-solution-file.md#solution-resource) hello 솔루션을 제거할 경우 제거 되도록 보기 hello 합니다.

## <a name="alerts"></a>경고
- Hello 사용자 hello 솔루션을 설치할 때에 정의할 수 있도록 hello 받는 사람 목록 hello 솔루션 파일에 매개 변수로 정의 합니다.
- 너무 hello 솔루션 구성[참조](operations-management-suite-solutions-solution-file.md#solution-resource) 경고 규칙을 해당 사용자의 구성을 변경할 수 있습니다.  Hello 받는 사람 목록을 수정, hello 경고의 hello 임계값을 변경 또는 hello 경고 규칙을 사용 하지 않도록 설정 하는 등 toomake 변경 할 수 있습니다. 


## <a name="next-steps"></a>다음 단계
* Hello 기본 과정을 안내 [디자인 및 관리 솔루션을 구축](operations-management-suite-solutions-creating.md)합니다.
* 너무 방법에 대해 알아봅니다[솔루션 파일을 만들](operations-management-suite-solutions-solution-file.md)합니다.
* [저장 된 검색 및 알림 추가](operations-management-suite-solutions-resources-searches-alerts.md) tooyour 관리 솔루션입니다.
* [뷰 추가](operations-management-suite-solutions-resources-views.md) tooyour 관리 솔루션입니다.
* [자동화 runbook 및 기타 리소스를 추가](operations-management-suite-solutions-resources-automation.md) tooyour 관리 솔루션입니다.

