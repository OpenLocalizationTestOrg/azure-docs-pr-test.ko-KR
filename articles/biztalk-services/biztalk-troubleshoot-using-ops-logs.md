---
title: "작업 로그를 사용 하 여 aaaTroubleshoot BizTalk 서비스 | Microsoft Docs"
description: "작업 로그를 사용하여 BizTalk 서비스의 문제를 해결합니다. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 1081a9c6-58cc-4a76-8ac8-11e5e7a6ea27
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 102779ed6e29784f190c28e4102a7d9670614914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-troubleshoot-using-operation-logs"></a>BizTalk 서비스: 작업 로그를 사용한 문제 해결

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="what-are-hello-operation-logs"></a>Hello 작업 로그는 무엇입니까
작업 로그에는 hello tooview BizTalk 서비스를 포함 한, Azure 서비스에 대 한 작업 기록 로그 수 있는 Azure 클래식 포털에서에서 사용할 수 있는 관리 서비스 기능입니다. 이렇게 하면 기록 데이터 tooview 관련 180 일 이전에 출시 BizTalk 서비스 구독에 대해 toomanagement 작업 합니다.

> [!NOTE]
> 이 기능은 등, 최대 백업 hello 서비스 시작 되었을 때와 같은 BizTalk 서비스에서 관리 작업에 대 한 로그를 캡처합니다만. Hello Azure 클래식 포털에서에서 또는 hello를 사용 하 여 수행 여부에 관계 없이 이러한 작업은 추적 [BizTalk 서비스 REST Api](http://msdn.microsoft.com/library/azure/dn232347.aspx)합니다. 관리 서비스를 사용하여 추적된 작업의 전체 목록을 보려면 [Azure 관리 서비스를 사용하여 추적된 작업](#bizops)를 사용하여 수행되었는지 여부에 관계없이 추적됩니다.<br/><br/>
> 활동 관련된 tooBizTalk 서비스 런타임 (예: 메시지 브리지에 의해 처리 됩니다.)에 대 한 hello 로그 캡처하지 않습니다. tooview 이러한 로그를 사용 하 여 hello hello BizTalk 서비스 포털에서 뷰를 추적 합니다. 자세한 내용은 [메시지 추적](http://msdn.microsoft.com/library/azure/hh949805.aspx)을 참조하세요.
> 
> 

## <a name="view-biztalk-services-operation-logs"></a>BizTalk 서비스 작업 로그 보기
1. Hello Azure 클래식 포털에서에서 선택 **관리 서비스**를 선택한 후 hello **작업 로그** 탭 합니다.
2. 구독, 날짜 범위, 서비스 유형 (예: BizTalk 서비스), 서비스 이름 또는 (Succeeded, Failed) hello 작업의 상태와 같은 다른 매개 변수를 기준으로 하는 hello 로그를 필터링 할 수 있습니다.
3. 선택 hello 확인 표시 tooview hello 필터링 된 목록입니다. hello 다음 그림에 나와 활동 관련된 tootestbiztalkservice: ![작업 로그를 보려면][ViewLogs] 
4. 특정 작업에 대해 자세히 tooview hello 행을 선택 하 고 클릭 **세부 정보** hello 맨 아래에 hello 작업 표시줄에서 합니다.

## <a name="bizops"></a>Azure 관리 서비스를 사용하여 추적된 작업
hello 다음 표에 나타난 hello Azure 관리 서비스를 사용 하 여 추적 되는 hello 작업.

| 작업 이름 | 작업 |
| --- | --- |
| CreateBizTalkService |작업 toocreate 새 BizTalk 서비스 |
| DeleteBizTalkService |작업 toodelete BizTalk 서비스 |
| RestartBizTalkService |작업 toorestart BizTalk 서비스 |
| StartBizTalkService |작업 toostart BizTalk 서비스 |
| StopBizTalkService |작업 toostop BizTalk 서비스 |
| DisableBizTalkService |작업 toodisable BizTalk 서비스 |
| EnableBizTalkService |작업 tooenable BizTalk 서비스 |
| BackupBizTalkService |BizTalk 서비스를 tooback 작업 |
| RestoreBizTalkService |작업 toorestore 지정 된 백업에서 BizTalk 서비스 |
| SuspendBizTalkService |작업 toosuspend BizTalk 서비스 |
| ResumeBizTalkService |작업 tooresume BizTalk 서비스 |
| ScaleBizTalkService |BizTalk service 위나 아래로 이동 작업 tooscale |
| ConfigUpdateBizTalkService |BizTalk 서비스의 작업 tooupdate hello 구성 |
| ServiceUpdateBizTalkService |작업 tooupgrade 하거나 BizTalk 서비스 tooa 다른 버전 다운 그레이드 |
| PurgeBackupBizTalkService |Hello 보존 기간이 hello BizTalk 서비스의 작업 toopurge 백업 |

## <a name="see-also"></a>참고 항목
* [BizTalk 서비스 백업](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [백업에서 BizTalk 서비스 복원](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [BizTalk 서비스: Developer, Basic, Standard 및 Premium Editions 차트](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [BizTalk 서비스: Azure 클래식 포털을 사용하여 프로비전](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [BizTalk 서비스: 프로비저닝 상태 차트](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [BizTalk 서비스: 대시보드, 모니터 및 크기 조정 탭](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [BizTalk 서비스: 제한](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [BizTalk 서비스: 발급자 이름 및 발급자 키](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [Azure BizTalk 서비스 SDK를 hello 어떻게 사용 하 여 시작 합니까](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[ViewLogs]: ./media/biztalk-troubleshoot-using-ops-logs/Operation-Logs.png

