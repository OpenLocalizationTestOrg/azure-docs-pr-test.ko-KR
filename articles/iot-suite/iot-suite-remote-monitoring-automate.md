---
title: "원격 모니터링 솔루션에서 장치 문제 감지 - Azure | Microsoft Docs"
description: "이 자습서에서는 규칙 및 작업을 사용하여 원격 모니터링 솔루션에서 임계값 기반 장치 문제를 자동으로 감지하는 방법을 보여 줍니다."
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
ms.openlocfilehash: e00c4ab2fc8bb13a765f7c2154555607dddfc651
ms.sourcegitcommit: 922687d91838b77c038c68b415ab87d94729555e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2017
---
# <a name="detect-issues-using-threshold-based-rules"></a>임계값 기반 규칙을 사용하여 문제 감지

이 자습서는 원격 모니터링 솔루션에서 규칙 엔진의 기능을 보여 줍니다. 이러한 기능을 소개하기 위해 자습서에서는 Contoso IoT 응용 프로그램에서 시나리오를 사용합니다.

Contoso에는 **냉각기** 장치에서 보고된 압력이 250PSI를 초과하는 경우 중요한 경보를 생성하는 규칙이 있습니다. 운영자로서 초기 압력 스파이크를 찾아 문제가 있는 센서가 있을 수 있는 **냉각기** 장치를 식별하려고 합니다. 이러한 장치를 식별하려면 압력이 150PSI를 초과할 때 경고를 생성하는 규칙을 만듭니다.

이 자습서에서는 다음 방법에 대해 알아봅니다.

>[!div class="checklist"]
> * 솔루션에서 규칙 보기
> * 새 규칙 만들기
> * 기존 규칙 편집
> * 규칙 삭제

## <a name="prerequisites"></a>필수 조건

이 자습서를 수행하려면 Azure 구독에서 원격 모니터링 솔루션의 배포된 인스턴스가 필요합니다.

원격 모니터링 솔루션을 아직 배포하지 않은 경우 [미리 구성된 원격 모니터링 솔루션 배포](iot-suite-remote-monitoring-deploy.md) 자습서를 완료해야 합니다.

## <a name="view-the-rules-in-your-solution"></a>솔루션에서 규칙 보기

솔루션에서 **규칙 및 작업** 페이지는 현재 모든 규칙의 목록을 표시합니다.

![규칙 및 작업 페이지](media/iot-suite-remote-monitoring-automate/rulesactions.png)

**냉각기** 장치에 적용되는 규칙만 보려면 필터를 적용합니다.

![규칙의 목록 필터링](media/iot-suite-remote-monitoring-automate/rulesactionsfilter.png)

규칙에 대한 자세한 내용을 보고 목록에서 선택하면 편집할 수 있습니다.

![규칙 세부 정보 보기](media/iot-suite-remote-monitoring-automate/rulesactionsdetail.png)

하나 이상의 규칙을 비활성화, 활성화 또는 삭제하려면 목록에서 여러 개의 규칙을 선택합니다.

![여러 규칙 선택](media/iot-suite-remote-monitoring-automate/rulesactionsmultiselect.png)

## <a name="create-a-new-rule"></a>새 규칙 만들기

**냉각기** 장치의 압력이 150PSI를 초과할 때 경고를 생성하는 새 규칙을 추가하려면 **새 규칙**을 선택합니다.

![규칙 만들기](media/iot-suite-remote-monitoring-automate/rulesactionsnewrule.png)

다음 값을 사용하여 규칙을 만듭니다.

| 설정          | 값                                 |
| ---------------- | ------------------------------------- |
| 이름             | 냉각기 경고                       |
| 원본           | **냉각기** 장치 그룹             |
| 트리거 필드    | pressure                              |
| 트리거 연산자 | 다음보다 큼                          |
| 트리거 값    | 150                                   |
| 심각도 수준   | Warning                               |
| 설명      | 냉각기 압력이 150PSI를 초과함 |

새 규칙을 저장하려면 **적용**을 선택합니다.

규칙이 **규칙 및 작업** 페이지 또는 **대시보드** 페이지에서 트리거되는 경우 볼 수 있습니다.

## <a name="edit-an-existing-rule"></a>기존 규칙 편집

기존 규칙을 변경하려면 규칙의 목록에서 선택합니다. 그런 다음 **규칙 세부 정보** 패널에서 **모드 편집**을 선택합니다.

![규칙 편집](media/iot-suite-remote-monitoring-automate/rulesactionsedit.png)

## <a name="disable-a-rule"></a>규칙 사용 안 함

규칙을 일시적으로 해제하기 위해 규칙 목록에서 비활성화할 수 있습니다. 비활성화할 규칙을 선택한 다음 **사용 안 함**을 선택합니다. 목록에서 규칙의 **상태**가 규칙이 이제 비활성화됨을 나타내기 위해 변경됩니다. 동일한 절차를 사용하여 이전에 비활성화한 규칙을 다시 활성화할 수 있습니다.

![규칙 사용 안 함](media/iot-suite-remote-monitoring-automate/rulesactionsdisable.png)

목록에서 여러 규칙을 선택하는 경우 동시에 여러 규칙을 활성화 및 비활성화할 수 있습니다.

## <a name="delete-a-rule"></a>규칙 삭제

규칙을 영구적으로 삭제하려면 규칙의 목록에서 규칙을 선택한 다음 **삭제**를 선택합니다.

목록에서 여러 규칙을 선택하는 경우 동시에 여러 규칙을 삭제할 수 있습니다.

## <a name="next-steps"></a>다음 단계

이 자습서는 다음 방법을 보여 줬습니다.

<!-- Repeat task list from intro -->
>[!div class="checklist"]
> * 솔루션에서 규칙 보기
> * 새 규칙 만들기
> * 기존 규칙 편집
> * 규칙 삭제

이제 임계값 기반 규칙을 사용하여 문제를 감지하는 방법을 배웠으므로 제안된 다음 단계는 다음 방법을 배우기 위한 것입니다.

* [장치 관리 및 구성](./iot-suite-remote-monitoring-manage.md)
* [장치 문제 해결 및 수정](./iot-suite-remote-monitoring-maintain.md)
* [시뮬레이트된 장치로 솔루션 테스트](iot-suite-remote-monitoring-test.md)

<!-- Next tutorials in the sequence -->