---
title: "다중 테 넌 트 응용 프로그램에서 Azure SQL 데이터베이스 aaaRestore | Microsoft Docs"
description: "단일 toorestore SQL 테 넌 트에서 방법에 대해 알아봅니다 데이터를 실수로 삭제 한 후 데이터베이스"
keywords: "SQL Database 자습서"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: billgib;sstein
ms.openlocfilehash: 8507ecec2424c135f1859b88ebf2bb4e17538a58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-wingtip-saas-tenants-sql-database"></a>Wingtip SaaS 테넌트 SQL Database 복원

각 테 넌 트는 자체 데이터베이스에 있는 테 넌 당 데이터베이스 모델을 사용 하 여 hello Wingtip SaaS 앱이 만들어집니다. 이 모델의 hello 이점 중 하나는 쉽게 toorestore 다른 테 넌 트에 영향을 주지 않고 격리에 단일 테 넌 트의 데이터입니다.

이 자습서에서는 다음 두 가지 데이터 복구 패턴에 대해 알아봅니다.

> [!div class="checklist"]

> * 병렬 데이터베이스에 데이터베이스 복원(병렬)
> * 원래 위치에 데이터베이스 복원


|||
|:--|:--|
| **병렬 데이터베이스에 시간 내에 테 넌 트 tooa 이전 지점 복원** | 검토, 감사, 규정 준수에 대 한 hello 테 넌 트 별로이 패턴을 사용할 수 있습니다, 그리고 등 hello 원본 데이터베이스에 온라인 상태이 고 변경 되지 않은 상태로 유지 됩니다. |
| **원래 위치에 테넌트 복원** | 이 방법은 일반적으로 사용 되는 테 넌 트 tooa 이전 지점 toorecover 테 넌 트 데이터를 실수로 삭제 한 후 시간 내에입니다. hello 원본 데이터베이스는 오프 라인으로 전환 하 고 hello 복원 된 데이터베이스 대체 됩니다. |
|||

toocomplete이이 자습서에서는 다음 필수 구성 요소 확인 되었는지 hello 완료 됩니다.

* hello Wingtip SaaS 앱을 배포 합니다. 5 분 이내에 toodeploy 참조 [배포 하 고 hello Wingtip SaaS 응용 프로그램 탐색](sql-database-saas-tutorial.md)
* Azure PowerShell이 설치되었습니다. 자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.

## <a name="introduction-toohello-saas-tenant-restore-pattern"></a>소개 toohello SaaS 테 넌 트 복원 패턴

Hello 테 넌 트에 대 한 복원 패턴, 개별 테 넌 트의 데이터를 복원 하기 위한 두 가지 간단한 패턴. 테넌트 데이터베이스가 서로 격리되어 있기 때문에 하나의 테넌트를 복원해도 다른 테넌트의 데이터에는 영향을 주지 않습니다.

Hello 첫 번째 패턴에서는 데이터가 있는 새 데이터베이스로 복원 됩니다. hello 테 넌 트 프로덕션 데이터와 함께 access toothis 데이터베이스를 부여 됩니다. 이 패턴을 사용 하면 테 넌 트 관리자 tooreview 복원 hello 데이터 및 잠재적으로 사용 하 여 tooselectively 현재 데이터 값을 덮어씁니다. 가 toohello SaaS 응용 프로그램 디자이너 toodetermine 얼마나 정교한 hello 데이터 복구 옵션을 수 있습니다. 단순히 hello의 상태로 지정 된 시점으로 데이터를 수 tooreview 되 고 일부 시나리오에서는 필요한 모든 수 있습니다. Hello 데이터베이스를 사용 하는 경우 [지리적 복제](sql-database-geo-replication-overview.md), hello 원래 데이터베이스에 복원 하는 hello 복사본에서 hello 필요한 데이터를 복사 하는 것이 좋습니다. 데이터베이스를 복원 하는 hello와 hello 원래 데이터베이스를 대체 하는 경우 tooreconfigure 필요 하 고 지리적 복제를 다시 동기화 합니다.

이 경우 해당 hello 테 넌 트 손실 되거나 데이터 손상 되었다는 가정, 두 번째 패턴에서는 hello hello 테 넌 트의 프로덕션 데이터베이스를 복원 tooa 이전 지정 시간입니다. Hello 복원 시 위치 패턴이에 hello 테 넌 트는 동안 오프 라인 짧은 시간에 대 한 hello 데이터베이스가 복원 되 고 다시 온라인 상태가 됩니다. hello 원본 데이터베이스는 삭제 되지만 여전히에서 복원할 수 있습니다 toogo 백 tooan 해야 할 경우에 이전 시점입니다. Hello 데이터베이스 이름 바꾸기 데이터 보안과 관련 없는 추가적인 이점도 제공 하지만이 패턴의 변형에, 삭제 하는 대신 hello 데이터베이스 이름을 바꿀 수 없습니다.

## <a name="get-hello-wingtip-application-scripts"></a>Hello Wingtip 응용 프로그램 스크립트 가져오기

hello Wingtip SaaS 스크립트 및 응용 프로그램 소스 코드에서에서 사용할 수 있는 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 리포지토리 합니다. [Toodownload hello Wingtip SaaS 스크립트 단계](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)합니다.

## <a name="simulate-a-tenant-accidentally-deleting-data"></a>실수로 데이터를 삭제하는 테넌트 시뮬레이션

toodemonstrate 이러한 복구 시나리오에 필요한 너무*실수로* hello 테 넌 트 데이터베이스 중 하나에 일부 데이터를 삭제 합니다. 모든 레코드를 삭제 하려면 동안 hello 데모 toonot 다음 단계 집합 hello 참조 무결성 위반을 통해 차단 될! 또한 일부 티켓 구매 데이터를 사용할 수 있습니다 hello의 뒷부분에 나오는 추가 *Wingtip SaaS 분석 자습서*합니다.

Hello 티켓 생성기 스크립트를 실행 하 고 추가 데이터를 만듭니다. 의도적으로 hello 티켓 생성기는 각 테 넌 트 마지막 이벤트에 대 한 티켓을 구매 하지 않습니다.

1. 열기... \\학습 모듈\\유틸리티\\*데모 TicketGenerator.ps1* hello에 *PowerShell ISE*
1. 키를 눌러 **F5** toorun 스크립트 hello 및 고객을 생성 및 티켓 판매 데이터가 있습니다.


### <a name="open-hello-events-app-tooreview-hello-current-events"></a>Hello 이벤트 응용 프로그램 tooreview hello 현재 이벤트를 열려면

1. 열기 hello *이벤트 허브* (http://events.wtp.&lt; 사용자&gt;. trafficmanager.net)를 클릭 하 고 **Contoso 함께 Hall**:

   ![Events Hub](media/sql-database-saas-tutorial-restore-single-tenant/events-hub.png)

1. Hello 이벤트 목록을 스크롤하여 hello 목록에서 hello 마지막 이벤트 확인:

   ![마지막 이벤트](media/sql-database-saas-tutorial-restore-single-tenant/last-event.png)


### <a name="run-hello-demo-scenario-tooaccidentally-delete-hello-last-event"></a>Hello 데모 시나리오 tooaccidentally delete hello 마지막 이벤트를 실행 합니다.

1. 열기... \\학습 모듈\\비즈니스 연속성 및 재해 복구\\RestoreTenant\\*데모 RestoreTenant.ps1* hello에 *PowerShell ISE*, 다음 값 집합 hello 및:
   * **$DemoScenario** = **1**너무 설정,**1** -티켓 판매량이 없는 이벤트를 삭제 합니다.
1. 키를 눌러 **F5** toorun 스크립트 hello 및 hello 마지막 이벤트를 삭제 합니다. 확인 메시지와 비슷한 toohello 다음을 나타나야 합니다.

   ```Console
   Deleting unsold events from Contoso Concert Hall ...
   Deleted event 'Seriously Strauss' from Contoso Concert Hall venue.
   ```

1. hello Contoso 이벤트 페이지가 열립니다. 아래로 스크롤하여 hello 이벤트는 삭제를 확인 합니다. Hello 이벤트 hello 목록에 여전히 있는 경우 새로 고침을 클릭 하 고이 삭제 되 확인 합니다.

   ![마지막 이벤트](media/sql-database-saas-tutorial-restore-single-tenant/last-event-deleted.png)


## <a name="restore-a-tenant-database-in-parallel-with-hello-production-database"></a>Hello 프로덕션 데이터베이스와 동시에 테 넌 트 데이터베이스를 복원 합니다.

이 연습 hello Contoso 함께 Hall 데이터베이스 tooa 지정 시간 hello 이벤트가 삭제 되기 전에 복원 합니다. Hello 이벤트 hello 이전 단계에서 삭제 된 후 toorecover을 삭제 하는 hello 데이터를 참조 하십시오. Toorestore 프로덕션 데이터베이스를 삭제 하는 hello 레코드와 필요는 없지만 비즈니스 사유로 toorecover hello 이전 데이터베이스 tooaccess hello 이전 데이터를 필요 합니다.

 hello *복원 TenantInParallel.ps1* 스크립트 병렬 테 넌 트 데이터베이스 만들고, 병렬 카탈로그 항목을 모두 라는 *ContosoConcertHall\_이전*합니다. 이 복원 패턴은 사소한 데이터 손실로부터의 복구 또는 복구 시나리오에 대한 규정 준수 및 감사에 가장 적합합니다. 권장 접근법을 사용 중인 경우 hello 이기도 [지리적 복제](sql-database-geo-replication-overview.md)합니다.

1. 전체 hello [실수로 데이터를 삭제 하는 사용자를 시뮬레이트합니다](#simulate-a-tenant-accidentally-deleting-data) 섹션.
1. 열기... \\학습 모듈\\비즈니스 연속성 및 재해 복구\\RestoreTenant\\_데모 RestoreTenant.ps1_ hello에 *PowerShell ISE*.
1. 설정 **$DemoScenario** = **2**, 너무 설정**2** 너무*병렬로 복원 테 넌 트*합니다.
1. 키를 눌러 **F5** toorun hello 스크립트입니다.

hello 스크립트는 hello 테 넌 트 데이터베이스 (tooa 병렬 데이터베이스) tooa 지점 hello 이전 단원의 hello 이벤트를 삭제 하기 전에 시간으로 복원 합니다. 두 번째 데이터베이스를 만들고,이 데이터베이스에 존재 하며 hello에서 hello 데이터베이스 toohello 카탈로그를 추가 하는 기존 카탈로그 메타 데이터를 제거 *ContosoConcertHall\_이전* 항목입니다.

hello 데모 스크립트 브라우저에서 hello 이벤트 페이지를 엽니다. Hello URL에서 참고: ```http://events.wtp.&lt;user&gt;.trafficmanager.net/contosoconcerthall_old``` hello 복원 된 데이터베이스의에서 데이터를 보여 주는이 위치 *_old* toohello 이름이 추가 됩니다.

스크롤 hello에에서 나열 된 이벤트 hello 브라우저 tooconfirm hello 이벤트 hello 이전 섹션에서 삭제 하는 복원 되었습니다.

추가 테 넌 트를 고유 이벤트 앱 toobrowse 티켓와 같이 드문 상황이 toobe 어떻게에 제공 하는 데 사용 tooeasily 아니라 테 넌 트 액세스 toorestored 데이터가 hello 복원 패턴을 보여 줍니다.은 해당 노출을 복원 hello 테 넌 트를 note 합니다.

실제로 정의된 기간 동안 복원된 이 데이터베이스만 유지합니다. Hello를 호출 하 여 완료 된 후 복원 하는 hello 테 넌 트 항목을 삭제할 수 *제거 RestoredTenant.ps1* 스크립트입니다.

1. 설정 **$DemoScenario** 너무**4** tooselect hello *복원 제거 테 넌 트* 시나리오입니다.
1. **F5** **키를 사용하여** **실행합니다**.
1. hello *ContosoConcertHall\_이전* 항목은 이제 hello 카탈로그에서 삭제 됩니다. 계속 진행 하 고 브라우저에서이 테 넌이 트에 대 한 hello 이벤트 페이지를 닫습니다.


## <a name="restore-a-tenant-in-place-replacing-hello-existing-tenant-database"></a>테 넌 트 원위치에서 hello 기존 테 넌 트 데이터베이스를 복원 합니다.

이 연습 hello Contoso 함께 Hall 테 넌 트 tooa 지점 시간 hello 이벤트가 삭제 되기 전에 복원 합니다. hello *복원 TenantInPlace* 삭제 hello 원래 데이터베이스 및 스크립트 hello 현재 테 넌 트 데이터베이스 tooa 새 데이터베이스 시간 내에 tooa 이전 시점을 가리키는 복원 합니다. 이 패턴의 복원 tooaccommodate 갖기 테 넌 트 hello 많은 양의 데이터가 손실 될 수 있으므로 심각한 데이터 손상 으로부터 복구에 대 한 가장 잘 맞습니다.

1. PowerShell ISE에서 **Demo-RestoreTenant.ps1** 파일을 엽니다.
1. 설정 **$DemoScenario** 너무**5** tooselect hello *전체 시나리오에서 테 넌 트 복원*합니다.
1. **F5** 키를 사용하여 실행합니다.

hello 스크립트 hello 테 넌 트 데이터베이스 tooa 지점 hello 이벤트가 삭제 되기 전에 5 분을 복원 합니다. 이렇게 하기 첫 번째 라인 hello Contoso 함께 Hall 더 이상 없으면 하므로 오프 라인으로 테 넌 트 toohello 데이터를 업데이트 합니다. 그런 다음 병렬 데이터베이스 hello 복원 지점에서 복원 하 여 만든를 명명 된 타임 스탬프를 갖는 tooensure hello 데이터베이스 이름을 hello 기존 테 넌 트 데이터베이스 이름을와 충돌 하지 않습니다. 다음으로 이전 테 넌 트 데이터베이스 hello 삭제 되 고, hello 복원 된 데이터베이스는 이름이 바뀐된 toohello 원래 데이터베이스 이름입니다. 마지막으로, Contoso 함께 Hall 온라인 tooallow hello 응용 프로그램 액세스 복원 toohello 데이터베이스를 상태가 됩니다.

Hello 데이터베이스 tooa 지정 hello 이벤트가 삭제 되기 전에 시간으로 복원 했습니다. 이벤트 페이지가 열리면 hello, 확인 하므로 hello 마지막 이벤트 복원 되었습니다.


## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행하는 방법에 대해 알아보았습니다.

> [!div class="checklist"]

> * 병렬 데이터베이스에 데이터베이스 복원(병렬)
> * 원래 위치에 데이터베이스 복원

[테넌트 데이터베이스 스키마 관리](sql-database-saas-tutorial-schema-management.md)

## <a name="additional-resources"></a>추가 리소스

* 추가 [hello Wingtip SaaS 응용 프로그램을 구축 하는 자습서](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Azure SQL 데이터베이스의 비즈니스 연속성 개요](sql-database-business-continuity.md)
* [SQL Database 백업에 대한 자세한 정보](sql-database-automated-backups.md)
