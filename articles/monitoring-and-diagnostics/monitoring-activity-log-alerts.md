---
title: "aaaCreate 활동 로그 경고 | Microsoft Docs"
description: "Hello 활동 로그에서 특정 이벤트가 발생할 때에 SMS, webhook, 및 전자 메일을 통해 알림을 받을 합니다."
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
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: ba0716cc12a0b3a0024ee5562a025f3f153f8982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts"></a>활동 로그 경고 만들기

## <a name="overview"></a>개요
활동 로그 경고는 hello 경고에 지정 하는 hello 조건과 일치 하는 경고를 활성화 하는 새 활동 로그 이벤트가 발생 합니다. 이는 Azure 리소스이므로 Azure 리소스 관리자 템플릿을 사용하여 만들 수 있습니다. 또한 수 생성, 업데이트 또는 hello Azure 포털에서에서 삭제 합니다. 이 문서는 활동 로그 경고 뒤에 있는 hello 개념을 소개 합니다. 그런 다음 표시 toouse 활동 이벤트 로그에 경고를 Azure 포털 tooset hello 하는 방법.

일반적으로 활동 로그 경고 tooreceive 알림을 만들 때:

* 그러면 특정 변경 내용이 Azure 구독, 종종 범위가 지정 된 tooparticular 리소스 그룹 또는 리소스의 리소스에 발생합니다. 예를 들어 myProductionResourceGroup 가상 컴퓨터가 삭제 될 때 알림을 toobe를 좋습니다. 또는 새 역할 tooa 사용자 구독에 할당 된 경우에 toobe 할 수 있습니다.
* 서비스 상태 이벤트가 발생하는 경우. 서비스 상태 이벤트에는 인시던트 및 tooresources 구독에 적용 되는 유지 관리 이벤트에 대 한 알림을 포함 됩니다.

두 경우 모두 어떤 hello 경고를 만드는 hello 구독에서 이벤트에 대 한 활동 로그 경고를 모니터링 합니다.

활동 로그 이벤트에 대 한 hello JSON 개체에서 모든 최상위 속성에 기반 하 여 활동 로그 경고를 구성할 수 있습니다. 그러나 hello 포털 hello 가장 일반적인 옵션이 나와 있습니다.

- **범주**: 관리, 서비스 상태, 자동 크기 조정 및 권장 사항 중 하나입니다. 자세한 내용은 참조 [hello Azure 활동 로그 간략하게](./monitoring-overview-activity-logs.md#categories-in-the-activity-log)합니다. 서비스 상태 이벤트에 대해 자세히 toolearn 참조 [서비스 알림에서 활동 로그 경고를 수신](./monitoring-activity-log-alerts-on-service-notifications.md)합니다.
- **리소스 그룹**
- **리소스**
- **리소스 종류**
- **작업 이름**: hello 리소스 관리자 역할 기반 액세스 제어 작업 이름입니다.
- **수준**: hello (Verbose, 알림, 경고, 오류 또는 위험) hello 이벤트의 심각도 수준입니다.
- **상태**: hello 상태의 hello 이벤트는 일반적으로 시작 하 고, 실패 또는 성공 합니다.
- **이벤트에 의해 시작**: hello "호출자" 라고도 함 hello 전자 메일 주소 또는 hello 작업을 수행한 hello 사용자의 Azure Active Directory 식별자입니다.

>[!NOTE]
>기준을 앞에 경고 중 하나를 사용 하는 hello 적어도 두 개를 지정 해야 hello 범주입니다. Hello 활동 로그에서 이벤트를 만들 때마다 활성화 하는 경고를 만들 수 없습니다.
>
>

작업 활동 로그 경고가 활성화 될 때 사용 하 여 그룹화 toogenerate 동작 또는 알림입니다. 작업 그룹은 이메일 주소, 웹후크 URL 또는 SMS 전화 번호와 같은 알림 수신자의 재사용 가능한 집합입니다. hello 수신기는 여러 경고 toocentralize에서 참조할 수 있습니다 및 알림 채널을 그룹화 합니다. 활동 로그 경고를 정의하는 경우 두 가지 옵션이 있습니다. 다음을 수행할 수 있습니다.

* 활동 로그 경고에서 기존 작업 그룹을 사용합니다. 
* 새 작업 그룹을 만듭니다. 

동작 그룹에 대해 자세히 toolearn 참조 [만들기 hello Azure 포털에서에서 작업 그룹 및 관리](monitoring-action-groups.md)합니다.

서비스 상태 알림에 대해 자세히 toolearn 참조 [서비스 상태 알림에서 활동 로그 경고를 수신](monitoring-activity-log-alerts-on-service-notifications.md)합니다.

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 새 작업 그룹을 사용 하 여 활동 로그 이벤트에는 경고 만들기
1. Hello에 [포털](https://portal.azure.com)선택, **모니터**합니다.

    ![hello 서비스 "모니터 임계값"](./media/monitoring-activity-log-alerts/home-monitor.png)
2. Hello에 **활동 로그** 섹션에서 **경고**합니다.

    ![hello "경고" 탭](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. 선택 **추가 활동 로그 경고**, 고 hello 필드를 입력 합니다.

4. Hello에 이름을 입력 **활동 로그 경고 이름** 고 선택 된 **설명**합니다.

    ![hello "추가 활동 로그 경고" 명령](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. hello **구독** 현재 구독과 autofills 상자입니다. 이 구독 하나 hello 저장 되는 hello 동작 그룹입니다. hello 경고 리소스는 여기에서 배포 된 toothis 구독 및 모니터 활동 로그 이벤트입니다.

    ![hello "활동 로그 경고 추가" 대화 상자](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. 선택 hello **리소스 그룹** 는 hello 경고 리소스가 생성 됩니다. 이것이 hello 경고에서 모니터링 하는 hello 리소스 그룹입니다. 만으로도 hello 경고 리소스 위치한 hello 리소스 그룹입니다.

7. 필요에 따라 선택 된 **이벤트 범주** toomodify hello 표시 되는 추가 필터입니다. Hello 필터에는 관리 이벤트에 대 한 **리소스 그룹**, **리소스**, **리소스 종류**, **operationname**, **수준**, **상태**, 및 **이벤트에 의해 시작**합니다. 이러한 값이 이 경고가 모니터링해야 하는 이벤트를 식별합니다.

    >[!NOTE]
    >Hello 조건 앞에 경고 중 하나 이상을 지정 해야 합니다. Hello 활동 로그에서 이벤트를 만들 때마다 활성화 하는 경고를 만들 수 없습니다.
    >
    >

8. Hello에 이름을 입력 **동작 그룹 이름** hello에 이름을 입력 하 고 상자의 **약식 이름** 상자입니다. hello 약식 이름은이 그룹을 사용 하 여 알림을 보내는 경우 전체 동작 그룹 이름 대신 사용 됩니다.

9.  Hello 동작을 제공 하 여 동작 목록을 정의 합니다.

    a. **이름**: hello 동작의 이름, 별칭 또는 식별자를 입력 합니다.

    b. **작업 유형**: SMS, 전자 메일 또는 웹후크를 선택합니다.

    c. **세부 정보**: 전화 번호, 전자 메일 주소 또는 URI webhook 입력 hello 동작 형식을 기반으로 합니다.

10. 선택 **확인** toocreate hello 경고 합니다.

hello 경고 toofully 전파 되 고 활성화 한 다음 몇 분이 걸립니다. 새 이벤트 hello 경고 조건과 일치 하는 경우를 트리거합니다.

자세한 내용은 참조 [활동 로그 경고에 사용 된 이해 hello webhook 스키마](monitoring-activity-log-alerts-webhook.md)합니다.

>[!NOTE]
>다음이 단계에 정의 된 hello 동작 그룹은 모든 이후 경고 정의 대 한 기존 작업 그룹으로 다시 사용할 수 있는입니다.
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 기존 작업 그룹에 대 한 활동 로그 이벤트에는 경고 만들기
1. 활동 로그 경고-7 이전 섹션 toocreate hello에에서 1 단계를 수행 합니다.

2. **통해 알림**선택, hello **기존** 작업 그룹 단추입니다. Hello 목록에서 기존 작업 그룹을 선택 합니다.

3. 선택 **확인** toocreate hello 경고 합니다.

hello 경고 toofully 전파 되 고 활성화 한 다음 몇 분이 걸립니다. 새 이벤트 hello 경고 조건과 일치 하는 경우를 트리거합니다.

## <a name="manage-your-alerts"></a>경고 관리

경고를 만든 후에 표시 됩니다 hello 모니터 블레이드의 hello 경고 섹션. toomanage hello 경고를 선택 합니다.

* 편집합니다.
* 삭제합니다.
* 또는 tootemporarily 중지 하거나 재개 hello 경고에 대 한 알림을 수신 하는 경우, 사용 안 함.

## <a name="next-steps"></a>다음 단계
- [경고 개요](monitoring-overview-alerts.md)를 확인하세요.
- [알림 속도 제한](monitoring-alerts-rate-limiting.md)에 대해 자세히 알아보세요.
- 검토 hello [활동 로그 경고 webhook 스키마](monitoring-activity-log-alerts-webhook.md)합니다.
- [작업 그룹](monitoring-action-groups.md)에 대해 자세히 알아보세요.  
- [서비스 상태 알림](monitoring-service-notifications.md)에 대해 자세히 알아보세요.
- 만들기는 [활동 로그 경고 toomonitor 구독에 대 한 모든 자동 크기 조정 엔진 작업](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)합니다.
- 만들기는 [활동 경고 toomonitor 구독에 대해 모든 실패 한 자동 크기 조정 눈금-/ 스케일 아웃 작업을 로그](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)합니다.
