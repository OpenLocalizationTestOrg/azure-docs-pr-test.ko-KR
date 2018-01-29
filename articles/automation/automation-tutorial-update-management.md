---
title: "Azure Windows VM에 대한 업데이트 및 패치 관리 | Microsoft Docs"
description: "이 문서에서는 Azure Automation - 업데이트 관리를 사용하여 Azure Windows VM에 대한 업데이트 및 패치를 관리하는 방법에 대한 개요를 제공합니다."
services: automation
documentationcenter: 
author: zjalexander
manager: jwhit
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 12/14/2017
ms.author: zachal
ms.custom: mvc
ms.openlocfilehash: 615618e0e78f97e3f41dc2c0e1ca9a6e4b1b47bf
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2018
---
# <a name="manage-windows-updates-with-azure-automation"></a>Azure Automation을 사용하여 Windows 업데이트 관리

업데이트 관리를 사용하면 가상 머신에 대한 업데이트 및 패치를 관리할 수 있습니다.
이 자습서에서는 사용 가능한 업데이트의 상태를 빠르게 평가하고, 필수 업데이트의 설치를 예약하고, 배포 결과를 검토하여 업데이트가 성공적으로 적용되었는지 확인하는 방법에 대해 알아봅니다.

가격 책정 정보에 대해서는 [업데이트 관리를 위한 Automation 가격 책정](https://azure.microsoft.com/pricing/details/automation/)을 참조하세요.

이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * 업데이트 관리를 위한 VM 등록
> * 업데이트 평가 보기
> * 업데이트 배포 예약
> * 배포 결과 보기

## <a name="prerequisites"></a>필수 조건

이 자습서를 완료하려면 다음이 필요합니다.

* Azure 구독. 구독이 아직 없는 경우 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)하거나 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 등록할 수 있습니다.
* 감시자, 작업 Runbook 및 감시자 태스크를 보관할 [Automation 계정](automation-offering-get-started.md)
* 등록할 [가상 머신](../virtual-machines/windows/quick-create-portal.md)

## <a name="log-in-to-azure"></a>Azure에 로그인

Azure Portal( http://portal.azure.com )에 로그인합니다.

## <a name="enable-update-management"></a>업데이트 관리 사용

먼저 이 자습서에서 VM에 대한 업데이트 관리를 사용하도록 설정해야 합니다. 이전에 VM에 대해 다른 자동화 솔루션을 사용하도록 설정한 경우에는 이 단계가 필요하지 않습니다.

1. 왼쪽 메뉴에서 **가상 머신**을 선택하고 목록에서 VM을 선택합니다.
2. 왼쪽 메뉴의 **작업** 섹션 아래에서 **업데이트 관리**를 클릭합니다. **업데이트 관리 사용** 페이지가 열립니다.

이 VM에 대해 업데이트 관리가 사용되도록 설정되어 있는지를 확인하기 위해 유효성 검사가 수행됩니다.
유효성 검사 중에는 Log Analytics 작업 영역 및 연결된 Automation 계정이 확인되고 솔루션이 작업 영역에 있는지 여부가 확인됩니다.

[Log Analytics](../log-analytics/log-analytics-overview.md?toc=%2fazure%2fautomation%2ftoc.json) 작업 영역은 기능 및 서비스(예: 업데이트 관리)에서 생성된 데이터를 수집하는 데 사용됩니다.
이 작업 영역은 여러 원본의 데이터를 검토 및 분석하는 단일 위치를 제공합니다.
업데이트가 필요한 VM에서 추가 작업을 수행하려면 Azure Automation에서 VM에 대해 Runbook(예: 업데이트 다운로드 및 적용)을 실행할 수 있습니다.

또한 유효성 검사 프로세스는 VM이 MMA 및 Automation 하이브리드 Runbook 작업자를 통해 프로비전되는지 확인합니다.
이 에이전트는 VM과 통신하고 업데이트 상태에 대한 정보를 얻습니다.

이러한 필수 구성 요소가 충족되지 않으면 솔루션을 사용하도록 설정하는 옵션을 제공하는 배너가 표시됩니다.

![업데이트 관리 온보드 구성 배너](./media/automation-tutorial-update-management/manageupdates-onboard-solution-banner.png)

솔루션을 사용하도록 설정하려면 배너를 클릭합니다.
유효성 검사 후에 다음 필수 구성 요소 중 하나라도 누락된 것으로 확인되면 자동으로 추가됩니다.

* [Log Analytics](../log-analytics/log-analytics-overview.md?toc=%2fazure%2fautomation%2ftoc.json) 작업 영역
* [Automation](./automation-offering-get-started.md)
* [Hybrid Runbook Worker](./automation-hybrid-runbook-worker.md)가 VM에서 사용되도록 설정됩니다.

**업데이트 관리** 화면이 열립니다. 사용할 위치, Log Analytics 작업 영역 및 Automation 계정을 구성하고 **사용**을 클릭합니다. 필드가 회색으로 표시되면 해당 VM에 대해 다른 자동화 솔루션을 사용하도록 설정하고 동일한 작업 영역과 Automation 계정을 사용해야 함을 의미합니다.

![업데이트 관리 솔루션 사용 창](./media/automation-tutorial-update-management/manageupdates-update-enable.png)

솔루션을 사용하도록 설정하는 데 최대 15분이 걸릴 수 있습니다. 이 시간 동안에는 브라우저 창을 닫으면 안됩니다.
솔루션이 사용되도록 설정되면 VM의 누락된 업데이트에 대한 정보가 Log Analytics로 이동됩니다.
이 데이터를 분석에 사용할 수 있게 되는 데 30분에서 6시간까지 걸릴 수 있습니다.

## <a name="view-update-assessment"></a>업데이트 평가 보기

**업데이트 관리**를 사용하도록 설정하면 **업데이트 관리** 화면이 나타납니다.
누락된 업데이트가 있으면 **누락 업데이트** 탭에 누락된 업데이트 목록이 표시됩니다.

업데이트에 대한 **정보 링크**를 선택하여 새 창에서 업데이트에 대한 지원 문서를 엽니다. 여기서는 업데이트와 관련된 중요한 정보를 알아볼 수 있습니다.

![업데이트 상태 보기](./media/automation-tutorial-update-management/manageupdates-view-status-win.png)

업데이트의 다른 위치를 클릭하면 선택한 업데이트에 대한 **로그 검색** 창이 열립니다. 로그 검색에 대한 쿼리는 해당 특정 업데이트에 대해 미리 정의되어 있습니다. 이 쿼리를 수정하거나 사용자 고유의 쿼리를 만들어 환경에서 배포되었거나 누락된 업데이트에 대한 자세한 정보를 볼 수 있습니다.

![업데이트 상태 보기](./media/automation-tutorial-update-management/logsearch.png)

## <a name="schedule-an-update-deployment"></a>업데이트 배포 예약

이제 VM에 업데이트가 누락되어 있음을 알게 되었습니다. 업데이트를 설치하려면 릴리스 일정 및 서비스 기간 이후로 배포를 예약합니다.
배포에 포함할 업데이트 형식을 선택할 수 있습니다.
예를 들어 중요 업데이트나 보안 업데이트를 포함하고 업데이트 롤업은 제외할 수 있습니다.

> [!WARNING]
> 업데이트로 인해 다시 부팅해야 하는 경우 VM이 자동으로 다시 시작됩니다.

**업데이트 관리**로 다시 이동하고 화면 위쪽에서 **업데이트 배포 예약**을 선택하여 VM에 대한 새 업데이트 배포를 예약합니다.

**새 배포 업데이트** 화면에서 다음 정보를 지정합니다.

* **이름** - 업데이트 배포에 대한 고유한 이름을 제공합니다.
* **업데이트 분류** - 배포에 포함되는 업데이트 배포 소프트웨어의 종류를 선택합니다. 이 자습서에서는 모든 종류가 선택된 상태로 둡니다.

  분류 형식은 다음과 같습니다.

  * 중요 업데이트
  * 보안 업데이트
  * 업데이트 롤업
  * 기능 팩
  * 서비스 팩
  * 정의 업데이트
  * 도구
  * 업데이트

* **일정 설정** - 나중에 시간을 5분으로 설정합니다. 기본값(현재 시간 이후 30분)을 그대로 사용할 수도 있습니다.
배포가 한 번만 수행될지 여부를 지정하거나 되풀이 일정을 설정할 수도 있습니다.
**되풀이** 아래에서 **정기**를 선택합니다. 기본값인 1일을 그대로 적용하고 **확인**을 클릭합니다. 이렇게 하면 되풀이 일정이 설정됩니다.

* **유지 관리 기간(분)** - 기본값으로 그대로 둡니다. 업데이트 배포를 수행할 기간을 지정할 수 있습니다. 이 설정을 사용하면 정의된 서비스 창 내에서 변경이 수행되도록 보장할 수 있습니다.

![업데이트 일정 설정 화면](./media/automation-tutorial-update-management/manageupdates-schedule-win.png)

일정 구성이 완료되면 **만들기** 단추를 클릭합니다. 상태 대시보드로 돌아갑니다. **예약된 업데이트 배포**를 선택하여 만든 배포 일정을 표시합니다.

## <a name="view-results-of-an-update-deployment"></a>업데이트 배포의 결과 보기

예약된 배포가 시작되면 **업데이트 관리** 화면의 **업데이트 배포** 탭에서 해당 배포에 대한 상태를 볼 수 있습니다.
현재 실행 중인 경우 상태는 **진행 중**으로 표시됩니다.
성공적으로 완료되면 **성공**으로 바뀝니다.
배포에서 하나 이상의 업데이트에 오류가 발생하는 경우 상태는 **부분적으로 실패**입니다.
완료된 배포 업데이트를 클릭하여 해당 업데이트 배포에 대한 대시보드를 확인합니다.

![특정 배포에 대한 업데이트 배포 상태 대시보드](./media/automation-tutorial-update-management/manageupdates-view-results.png)

**업데이트 결과** 타일에서 요약은 VM에 대한 총 업데이트 수 및 배포 결과를 제공합니다.
오른쪽 테이블에는 각 업데이트에 대한 자세한 분석 및 설치 결과가 표시됩니다.
다음 목록에서는 사용 가능한 값을 보여 줍니다.

* **시도 안 함** - 정의된 유지 관리 기간에 따라 사용할 수 있는 시간이 충분하지 않기 때문에 업데이트가 설치되지 않았습니다.
* **성공** - 업데이트했습니다.
* **실패** -업데이트하지 못했습니다.

배포를 통해 생성된 항목에 대한 모든 로그를 보려면 **모든 로그**를 클릭합니다.

**출력** 타일을 클릭하여 대상 VM의 업데이트 배포를 관리하는 runbook의 작업 스트림을 확인합니다.

배포의 모든 오류에 대한 자세한 정보를 보려면 **오류**를 클릭합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * 업데이트 관리를 위한 VM 등록
> * 업데이트 평가 보기
> * 업데이트 배포 예약
> * 배포 결과 보기

업데이트 관리 솔루션에 대한 개요로 계속 진행하세요.

> [!div class="nextstepaction"]
> [업데이트 관리 솔루션](../operations-management-suite/oms-solution-update-management.md?toc=%2fazure%2fautomation%2ftoc.json)
