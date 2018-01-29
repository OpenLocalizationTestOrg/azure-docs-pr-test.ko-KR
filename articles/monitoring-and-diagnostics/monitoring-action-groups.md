---
title: "Azure Portal에서 작업 그룹 만들기 및 관리 | Microsoft Docs"
description: "Azure Portal에서 작업 그룹을 만들고 관리하는 방법에 대해 알아봅니다."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: 05775415e210333cf63565e7b5b554d014f6ba23
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2017
---
# <a name="create-and-manage-action-groups-in-the-azure-portal"></a>Azure Portal에서 작업 그룹 만들기 및 관리
## <a name="overview"></a>개요 ##
이 문서에서는 Azure Portal에서 작업 그룹을 만들고 관리하는 방법을 보여 줍니다.

작업 그룹을 사용하여 작업 목록을 구성할 수 있습니다. 그런 다음 이러한 그룹을 활동 로그 경고를 정의할 때 사용할 수 있습니다. 이러한 그룹은 사용자가 정의한 각 활동 로그 경고에서 다시 사용할 수 있습니다. 이를 통해 활동 로그 경고가 트리거될 때마다 동일한 작업이 수행되도록 합니다.

하나의 작업 그룹에는 각 작업 유형이 최대 10개 포함될 수 있습니다. 각 작업은 다음과 같은 속성으로 구성됩니다.

* **이름**: 작업 그룹 내의 고유 식별자입니다.  
* **동작 유형**: SMS 보내기, 이메일 보내기, 웹후크 호출, ITSM 도구에 데이터 보내기, Azure 앱 호출 또는 Automation Runbook 실행
* **세부 정보**: 해당 전화 번호, 이메일 주소, 웹후크 URI 또는 ITSM 연결 세부 정보입니다.

Azure 리소스 관리자 템플릿을 사용하여 작업 그룹을 구성하는 방법에 대한 자세한 내용은 [작업 그룹 리소스 관리자 템플릿](monitoring-create-action-group-with-resource-manager-template.md)을 참조하세요.

## <a name="create-an-action-group-by-using-the-azure-portal"></a>Azure Portal을 사용하여 작업 그룹 만들기 ##
1. [포털](https://portal.azure.com)에서 **모니터**를 선택합니다. **모니터** 블레이드는 모든 모니터링 설정 및 데이터를 하나의 뷰에 통합합니다.

    ![“모니터링” 서비스](./media/monitoring-action-groups/home-monitor.png)
2. **설정** 섹션에서 **작업 그룹**을 선택합니다.

    ![“작업 그룹” 탭](./media/monitoring-action-groups/action-groups-blade.png)
3. **작업 그룹 추가**를 선택하고 필드를 입력합니다.

    ![“작업 그룹 추가” 명령](./media/monitoring-action-groups/add-action-group.png)
4. **작업 그룹 이름** 상자에 이름을 입력하고 **약식 이름** 상자에 이름을 입력합니다. 약식 이름은 이 그룹을 사용하여 알림을 보내는 경우 전체 작업 그룹 이름 대신 사용됩니다.

      ![“작업 그룹 추가” 대화 상자](./media/monitoring-action-groups/action-group-define.png)

5. **구독** 상자가 현재 구독으로 자동으로 채워집니다. 이 구독은 작업 그룹이 저장되는 위치입니다.

6. 작업 그룹이 저장되는 **리소스 그룹**을 선택합니다.

7. 각 작업에 대해 다음 정보를 제공하여 작업 목록을 정의합니다.

    a. **이름**: 이 작업에 대한 고유 식별자를 입력합니다.

    나. **작업 유형**: SMS, 메일, 웹후크, Azure 앱, ITSM 또는 Automation Runbook을 선택합니다.

    다. **세부 정보**: 작업 유형에 따라 전화 번호, 이메일 주소, 웹후크 URI, Azure 앱, ITSM 연결 또는 Automation Runbook을 입력합니다. ITSM 작업의 경우 **작업 항목** 및 ITSM 도구에 필요한 다른 필드를 추가로 지정합니다. 

   > [!NOTE]
   > ITSM 작업에는 ITSM 연결이 필요합니다. [ITSM 연결](../log-analytics/log-analytics-itsmc-overview.md)을 만드는 방법에 대해 알아봅니다. 현재 ITSM 작업은 활동 로그 경고에 대해서만 작동합니다. 현재 다른 경고 유형의 경우 이 작업은 작동하지 않습니다.

8. **확인**을 선택하여 작업 그룹을 만듭니다.

## <a name="manage-your-action-groups"></a>작업 그룹 관리 ##
작업 그룹을 만들면 **모니터** 블레이드의 **작업 그룹** 섹션에 표시됩니다. 관리하려는 작업 그룹을 선택합니다.

* 작업을 추가, 편집 또는 제거합니다.
* 작업 그룹을 삭제합니다.

## <a name="next-steps"></a>다음 단계 ##
* [SMS 경고 동작](monitoring-sms-alert-behavior.md)에 대해 자세히 알아보세요.  
* [활동 로그 경고 웹후크 스키마의 이해](monitoring-activity-log-alerts-webhook.md)를 확인해 보세요.  
* [ITSM 커넥터](../log-analytics/log-analytics-itsmc-overview.md)에 대해 자세히 알아보세요.
* 경고의 [속도 제한](monitoring-alerts-rate-limiting.md)에 대해 자세히 알아보세요. 
* [활동 로그 경고의 개요](monitoring-overview-alerts.md)를 확인하고 경고를 받는 방법에 대해 알아보세요.  
* [서비스 상태 알림이 게시될 때마다 경고를 구성](monitoring-activity-log-alerts-on-service-notifications.md)하는 방법을 알아보세요.
