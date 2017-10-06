---
title: "Azure 자동화 계정 로그 분석에서 aaaUnlink | Microsoft Docs"
description: "이 문서는 어떻게 toounlink Azure 자동화는 OMS 작업 영역에서을 계정에 대 한 개요를 제공 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a>어떻게 toounlink 자동화는 로그 분석 작업 영역에서을 계정합니다

Azure 자동화 로그 분석 toonot만 지원 사전 모니터링 runbook 작업의 자동화 계정의 모든와 통합 되어 뿐만 아니라 필요한 hello 다음 로그 분석에 의존 하는 솔루션을 가져올 때:

* [업데이트 관리](../operations-management-suite/oms-solution-update-management.md)
* [변경 내용 추적](../log-analytics/log-analytics-change-tracking.md)
* [작업이 없는 동안 VM 시작/중지](automation-solution-vm-management.md)
 
중단 toointegrate 자동화 계정 로그 분석을 결정 한 경우 hello Azure 포털에서 직접 계정 연결을 끊을 수 없습니다.  계속 진행 하기 전에 앞에서 언급 한 tooremove hello 솔루션을 만들어야 합니다, 그리고 그렇지 않으면 진행에서이 프로세스를 시작 하지 것입니다.  필요한 toounderstand hello 단계 가져온 hello 특정 솔루션에 대 한 검토 hello 항목 tooremove 것입니다.  

이러한 솔루션을 제거한 후에 다음 단계 toounlink hello 자동화 계정으로 수행할 수 있습니다.

## <a name="unlink-workspace"></a>작업 영역 연결 해제

1. Hello Azure 포털에서에서 자동화 계정을 열고 hello 자동화 계정 블레이드에서 hello 계정 블레이드 선택 **작업 공간 연결을 해제**합니다.<br><br> ![작업 영역 연결 해제 옵션](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)<br><br>  
2. Hello 연결 끊기 작업 영역 블레이드 클릭 **worksapce 연결 끊기**합니다.<br><br> ![작업 영역 연결 해제 블레이드](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).<br><br>  원하는 tooproceed 확인 메시지가 나타납니다.<br><br>
3. Azure 자동화는 toounlink hello 계정 로그 분석 작업 영역을 가져오려고 하는 동안에 아래 hello 진행률을 추적할 수 **알림** hello 메뉴에서 합니다.

Hello 업데이트 관리 솔루션을 사용 하는 경우 필요에 따라 좋습니다 tooremove hello 다음 hello 솔루션을 제거한 후 더 이상 필요 없는 항목입니다.

* 업데이트 일정.  각각 만든 hello 업데이트 배포를 일치 하는 이름을 갖습니다)

* 하이브리드 작업자 그룹 hello 솔루션에 대 한 생성 합니다.  각각 지정 됩니다. 마찬가지로 너무 machine1.contoso.com_9ceb8108-26 c 9-4051-b6b3-227600d715c8).

업무 시간 이후 솔루션 중 hello 시작/중지 Vm에 사용한, 필요에 따라 경우 tooremove hello 다음 hello 솔루션을 제거한 후 더 이상 필요 없는 항목입니다.

* VM runbook 시작 및 중지 일정 
* VM runbook 시작 및 중지
* 변수   

## <a name="next-steps"></a>다음 단계

tooreconfigure OMS 로그 분석을 하 여 자동화 계정 toointegrate 참조 [자동화 tooLog 분석 (OMS)에서 작업 상태 및 작업 스트림 전달](automation-manage-send-joblogs-log-analytics.md)합니다. 
