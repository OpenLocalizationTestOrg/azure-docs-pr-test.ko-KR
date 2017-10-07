---
title: "서비스 알림 aaaReceive 활동 로그 경고 | Microsoft Docs"
description: "Azure 서비스가 발생할 때 SMS, 전자 메일 또는 웹후크를 통해 알림을 받습니다."
author: johnkemnetz
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
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a>서비스 알림에 대한 활동 로그 경고 만들기
## <a name="overview"></a>개요
이 문서에서는 hello Azure 포털을 사용 하 여 활동 로그를 tooset 서비스 상태 알림에 대 한 경고 하는 방법을 설명 합니다.  

Azure에서 서비스 상태 알림 tooyour Azure 구독을 보낼 때 경고를 받을 수 있습니다. 에 기반 하는 hello 경고를 구성할 수 있습니다.

- 서비스 상태 알림 (인시던트, 유지 관리, 정보 등)의 hello 클래스입니다.
- 영향을 받는 hello 서비스입니다.
- 영향을 받는 hello 지역입니다.
- hello 상태 (활성 및 해결) hello 알림입니다.
- hello 수준의 hello 알림 (정보, 경고, 오류).

구성할 수도 있습니다 hello 경고를 보낼 사용자:

- 기존 작업 그룹을 선택합니다.
- 새 작업 그룹을 만듭니다(향후 경고에 사용할 수 있음).

동작 그룹에 대해 자세히 toolearn 참조 [만들기 동작 그룹 및 관리](monitoring-action-groups.md)합니다.

Azure 리소스 관리자 템플릿을 사용 하 여 tooconfigure 서비스 상태 알림 경고 하는 방법에 대 한 정보를 참조 하십시오. [리소스 관리자 템플릿을](monitoring-create-activity-log-alerts-with-resource-manager-template.md)합니다.

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 새 작업 그룹에 대 한 서비스 상태 알림 경고 만들기
1. Hello에 [포털](https://portal.azure.com)선택, **모니터**합니다.

    ![hello 서비스 "모니터 임계값"](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. Hello에 **활동 로그** 섹션에서 **경고**합니다.

    ![hello "경고" 탭](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. 선택 **추가 활동 로그 경고**, 고 hello 필드를 입력 합니다.

    ![hello "추가 활동 로그 경고" 명령](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. Hello에 이름을 입력 **활동 로그 경고 이름** 고 제공 된 **설명**합니다.

    ![hello "활동 로그 경고 추가" 대화 상자](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. hello **구독** 현재 구독과 autofills 상자입니다. 이 구독에 사용 되는 toosave hello 활동 로그 경고입니다. hello 경고 리소스에 대 한 hello 활동 로그에서 배포 된 toothis 구독 및 모니터 이벤트입니다.

6. 선택 hello **리소스 그룹** 는 hello 경고 리소스가 생성 됩니다. 이것은 hello 경고에서 모니터링 하는 hello 리소스 그룹 되지 않습니다. 만으로도 hello 경고 리소스 위치한 hello 리소스 그룹입니다.

7. Hello에 **이벤트 범주** 상자 **서비스 상태**합니다. 필요에 따라 hello 선택 **서비스**, **지역**, **형식**, **상태**, 및 **수준** 서비스의 상태 알림 tooreceive 한다는 것입니다.

8. 아래 **를 통해 경고**선택, hello **새로 만들기** 작업 그룹 단추입니다. Hello에 이름을 입력 **동작 그룹 이름** hello에 이름을 입력 하 고 상자의 **약식 이름** 상자입니다. hello 약식 이름은이 경고가 발생할 때 보낸 hello 알림을에서 참조 됩니다.

9. Hello 수신기를 제공 하 여 수신기의 목록을 정의 합니다.

    a. **이름**: hello 수신기의 이름, 별칭 또는 식별자를 입력 합니다.

    b. **작업 유형**: SMS, 전자 메일 또는 웹후크를 선택합니다.

    c. **세부 정보**: 전화 번호, 전자 메일 주소 또는 URI webhook 입력 선택 hello 동작 형식을 기반으로 합니다.

10. 선택 **확인** toocreate hello 경고 합니다.

몇 분 안에 hello 경고가 활성 이며 tootrigger를 만들 때 지정한 hello 조건에 따라 시작 됩니다.

활동 로그 경고에 대 한 webhook 스키마 hello에 대 한 자세한 내용은 참조 하십시오. [Webhook에 대 한 Azure 활동 로그 경고](monitoring-activity-log-alerts-webhook.md)합니다.

>[!NOTE]
>다음이 단계에 정의 된 hello 동작 그룹은 모든 이후 경고 정의 대 한 기존 작업 그룹으로 다시 사용할 수 있는입니다.
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 기존 작업 그룹에 대 한 서비스 상태 알림 경고 만들기

1. 서비스 상태 알림-7 이전 섹션 toocreate hello에에서 1 단계를 수행 합니다. 

2. 아래 **를 통해 경고**선택, hello **기존** 작업 그룹 단추입니다. Hello 적절 한 작업 그룹을 선택 합니다.

3. 선택 **확인** toocreate hello 경고 합니다.

몇 분 안에 hello 경고가 활성 이며 tootrigger를 만들 때 지정한 hello 조건에 따라 시작 됩니다.

## <a name="manage-your-alerts"></a>경고 관리

Hello에 표시 되는 경고를 만든 후 **경고** hello 섹션 **모니터** 블레이드입니다. toomanage hello 경고를 선택 합니다.

* 편집합니다.
* 삭제합니다.
* 또는 tootemporarily 중지 하거나 재개 hello 경고에 대 한 알림을 수신 하는 경우, 사용 안 함.

## <a name="next-steps"></a>다음 단계
- [서비스 상태 알림](monitoring-service-notifications.md)에 대해 자세히 알아보세요.
- [알림 속도 제한](monitoring-alerts-rate-limiting.md)에 대해 자세히 알아보세요.
- 검토 hello [활동 로그 경고 webhook 스키마](monitoring-activity-log-alerts-webhook.md)합니다.
- 가져오기는 [활동 로그 경고의 개요](monitoring-overview-alerts.md), 알아봅니다 어떻게 tooreceive 경고 합니다. 
- [작업 그룹](monitoring-action-groups.md)에 대해 자세히 알아보세요.
