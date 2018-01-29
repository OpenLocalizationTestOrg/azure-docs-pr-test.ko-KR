---
title: "원격 모니터링 솔루션에서 장치 문제 해결 - Azure | Microsoft Docs"
description: "이 자습서에서는 원격 모니터링 솔루션에서 장치 문제를 해결하고 수정하는 방법을 보여 줍니다."
services: 
suite: iot-suite
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-suite
ms.date: 12/12/2017
ms.topic: article
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.workload: NA
ms.openlocfilehash: d26275b6b03115b775990c9efb5d4706fcb829d1
ms.sourcegitcommit: 922687d91838b77c038c68b415ab87d94729555e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2017
---
# <a name="troubleshoot-and-remediate-device-issues"></a>장치 문제 해결 및 수정

이 자습서는 솔루션에서 **유지 관리** 페이지를 사용하여 장치 문제를 해결하고 수정하는 방법을 보여 줍니다. 이러한 기능을 소개하기 위해 자습서에서는 Contoso IoT 응용 프로그램에서 시나리오를 사용합니다.

Contoso는 필드에서 새로운 **프로토타입** 장치를 테스트하고 있습니다. Contoso 운영자로서 테스트하는 동안 **프로토타입** 장치가 대시보드에서 온도 경보를 예기치 않게 트리거하는 것을 알게 됩니다. 이제 이 결함이 있는 **프로토타입** 장치의 동작을 조사해야 합니다.

이 자습서에서는 다음 방법에 대해 알아봅니다.

>[!div class="checklist"]
> * **유지 관리** 페이지를 사용하여 경보 조사
> * 장치 메서드를 호출하여 문제 수정

## <a name="prerequisites"></a>필수 조건

이 자습서를 수행하려면 Azure 구독에서 원격 모니터링 솔루션의 배포된 인스턴스가 필요합니다.

원격 모니터링 솔루션을 아직 배포하지 않은 경우 [미리 구성된 원격 모니터링 솔루션 배포](iot-suite-remote-monitoring-deploy.md) 자습서를 완료해야 합니다.

## <a name="use-the-maintenance-dashboard"></a>유지 관리 대시보드 사용

**대시보드** 페이지에서 **프로토타입** 장치와 관련된 규칙에서 들어오는 예기치 않은 온도 경보가 있다는 것을 알게 됩니다.

![대시보드에서 표시되는 경보](media/iot-suite-remote-monitoring-maintain/dashboardalarm.png)

문제를 자세히 조사하려면 경보 옆의 **경보 탐색** 옵션을 선택합니다.

![대시보드에서 경보 탐색](media/iot-suite-remote-monitoring-maintain/dashboardexplorealarm.png)

경보의 세부 정보 보기는 다음을 보여 줍니다.

* 경보가 트리거된 시점
* 경보와 연결된 장치에 대한 상태 정보
* 경보와 연결된 장치의 원격 분석

![경보 세부 정보](media/iot-suite-remote-monitoring-maintain/maintenancealarmdetail.png)

경보를 승인하려면 **경보 발생**을 선택하고 **승인**을 선택합니다. 이 작업을 통해 다른 작업자는 운영자가 경보를 확인했고 작업 중임을 알 수 있습니다.

![경보 승인](media/iot-suite-remote-monitoring-maintain/maintenanceacknowledge.png)

목록에서 온도 경보 발생에 책임이 있는 **프로토타입** 장치를 확인할 수 있습니다.

![경보를 발생시키는 장치 나열](media/iot-suite-remote-monitoring-maintain/maintenanceresponsibledevice.png)

## <a name="remediate-the-issue"></a>문제 수정

**프로토타입** 장치의 문제를 수정하려면 장치에서 **DecreaseTemperature** 메서드를 호출해야 합니다.

장치에서 작동하려면 장치 목록에서 선택한 다음 **일정**을 선택합니다. **프로토타입** 장치 모델은 장치에서 지원해야 하는 4개의 메서드를 지정합니다.

![장치에서 지원하는 메서드 보기](media/iot-suite-remote-monitoring-maintain/maintenancemethods.png)

**DecreaseTemperature**를 선택하고 작업 이름을 **DecreaseTemperature**로 설정합니다. 그런 다음 **적용**을 선택합니다.

![온도를 줄이는 작업 만들기](media/iot-suite-remote-monitoring-maintain/maintenancecreatejob.png)

**유지 관리** 페이지에서 작업의 상태를 추적하려면 **작업**을 선택합니다. **작업** 보기를 사용하여 솔루션에서 모든 작업 및 메서드 호출을 추적합니다.

![온도를 줄이는 작업 모니터링](media/iot-suite-remote-monitoring-maintain/maintenancerunningjob.png)

특정 작업 또는 메서드 호출의 세부 정보를 보려면 **작업** 보기의 목록에서 선택합니다.

![작업 세부 정보 보기](media/iot-suite-remote-monitoring-maintain/maintenancejobdetail.png)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 방법을 보여 줬습니다.

<!-- Repeat task list from intro -->
>[!div class="checklist"]
> * **유지 관리** 페이지를 사용하여 경보 조사
> * 장치 메서드를 호출하여 문제 수정

이제 장치 문제를 관리하는 방법을 배웠으며 제안된 다음 단계는 [시뮬레이트된 장치 솔루션으로 테스트](iot-suite-remote-monitoring-test.md)하는 방법을 알아보는 것입니다.

<!-- Next tutorials in the sequence -->