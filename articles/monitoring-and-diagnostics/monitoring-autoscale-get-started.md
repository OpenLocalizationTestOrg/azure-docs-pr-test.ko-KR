---
title: "Azure에서 자동 크기 조정이 시작 aaaGet | Microsoft Docs"
description: "자세한 내용은 방법 tooscale Azure의 리소스입니다."
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a>Azure에서 자동 크기 조정 시작
이 문서에서는 설명 어떻게 tooset hello Microsoft Azure 포털에서 리소스에 대 한 자동 크기 조정 설정 구성 합니다.

Azure 모니터의 자동 크기 조정 toovirtual 컴퓨터 크기 집합, 클라우드 서비스, Azure 앱 서비스 계획 및 앱 서비스 환경에 적용합니다. 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a>구독에서 hello 자동 크기 조정 설정을 검색 합니다.
자동 크기 조정 Azure 모니터에 적용 되는 모든 hello 리소스를 검색할 수 있습니다. 단계별 연습에 대 한 단계를 수행 하는 hello를 사용 합니다.

1. 열기 hello [Azure 포털입니다.][1]
2. Hello 왼쪽된 창의 hello Azure 모니터 아이콘을 클릭 합니다.
  ![Azure Monitor 열기][2]
3. 클릭 **자동 크기 조정** tooview 모든 hello 리소스는 자동 크기 조정에 대 한 현재 자동 크기 조정 상태와 함께 적용 됩니다.
  ![Azure Monitor에서 자동 크기 조정 검색][3]

특정 리소스 그룹, 특정 리소스 종류 또는 특정 리소스의 hello 목록 tooselect 리소스 아래로 상위 tooscope hello에 hello 필터 창을 사용할 수 있습니다.

각 리소스에 대 한 hello 현재 인스턴스 수 및 hello 자동 크기 조정 상태를 찾을 수 있습니다. 자동 크기 조정 상태 hello 될 수 있습니다.

- **구성되지 않음**: 이 리소스에 대해 자동 크기 조정 설정을 아직 사용하도록 설정하지 않았습니다.
- **사용**: 이 리소스에 대해 자동 크기 조정 설정을 사용하도록 설정했습니다.
- **사용 안 함**: 이 리소스에 대해 자동 크기 조정 설정을 사용하지 않도록 설정했습니다.

## <a name="create-your-first-autoscale-setting"></a>첫 번째 자동 크기 조정 설정 만들기

보겠습니다 진행 간단한 단계별 연습 toocreate 첫 번째 자동 크기 조정 설정에 있습니다.

1. 열기 hello **자동 크기 조정** 블레이드에서 Azure 모니터를 tooscale 원하는 리소스를 선택 합니다. (hello 다음 단계 사용 하 여 웹 앱에 연결 된 앱 서비스 계획 합니다. [Azure에서 5분 내에 첫 번째 ASP.NET 웹앱을 만들 수 있습니다.][4]
2. 참고 hello 현재 인스턴스 수는 1입니다. **자동 크기 조정 사용**을 클릭합니다.
  ![새 웹앱에 대한 크기 조정 설정][5]
3. Hello 크기 조정 설정에 대 한 이름을 입력 한 다음 **규칙 추가**합니다. Hello 오른쪽의 컨텍스트 창으로 열려면 hello 크기 조정 규칙 옵션을 확인 합니다. 기본적으로이 hello 옵션 tooscale 인스턴스 수가 1 hello CPU 비율 hello 리소스의 70%를 초과 하는 경우 설정 합니다. 규칙을 기본값으로 유지하고 **추가**를 클릭합니다.
  ![웹앱에 대한 크기 조정 설정 만들기][6]
4. 이제 첫 번째 크기 조정 규칙을 만들었습니다. UX 최선의 방법 및 없다는 것을 권장 하는 hello 참고 "toohave 것이 좋습니다 규칙에서 눈금이 최소 하나 이상 있습니다." toodo 하므로:
  
    a. **규칙 추가**를 클릭합니다. 

    b. 설정 **연산자** 너무**미만**합니다.

    c. 설정 **임계값** 너무**20**합니다.

    d. 설정 **작업** 너무**수를 줄이려면**합니다.

   이제 CPU 사용량을 기준으로 확장/축소하는 크기 조정 설정이 있어야 합니다.
   ![CPU 기준 크기 조정][8]
5. **Save**를 클릭합니다.

축하합니다. 이제 웹 응용 프로그램 CPU 사용량에 따라 첫 번째 눈금 설정을 tooautoscale 프로그램 성공적으로 만드는 마쳤습니다.

> [!NOTE] 
> hello 동일한 단계는 적용 가능한 tooget 시작 가상 컴퓨터 크기 집합 또는 클라우드 서비스 역할입니다.

## <a name="other-considerations"></a>기타 고려 사항
### <a name="scale-based-on-a-schedule"></a>일정을 기준으로 크기 조정
또한 CPU에 따라 tooscale를 설정할 수 있습니다 눈금 다르게 hello 주 중 특정 일에 대 한 합니다.

1. **크기 조정 조건 추가**를 클릭합니다.
2. Hello 크기 조정 모드와 hello 규칙 설정는 hello 동일 hello 기본 조건으로 합니다.
3. 선택 **특정 날짜를 반복** hello 일정에 대 한 합니다.
4. Hello 일과 hello 크기 조정 상태를 적용 해야 하는 경우에 대 한 hello 시작/종료 시간을 선택 합니다.

![일정 기준 크기 조정 조건][9]
### <a name="scale-differently-on-specific-dates"></a>특정 날짜에 대해 다르게 크기 조정
또한 CPU에 따라 tooscale를 설정할 수 있습니다 눈금 다르게 특정 날짜에 대 한 합니다.

1. **크기 조정 조건 추가**를 클릭합니다.
2. Hello 크기 조정 모드와 hello 규칙 설정는 hello 동일 hello 기본 조건으로 합니다.
3. 선택 **시작/종료 날짜 지정** hello 일정에 대 한 합니다.
4. Hello 시작/종료 날짜와 hello 크기 조정 상태를 적용 해야 하는 경우에 대 한 hello 시작/종료 시간을 선택 합니다.

![날짜 크기 조정 조건][10]

### <a name="view-hello-scale-history-of-your-resource"></a>리소스의 hello 눈금 기록 보기
리소스 확장 또는 축소할, 때마다 hello 활동 로그에 이벤트가 기록 됩니다. Toohello 전환 하 여 hello에 대 한 리소스의 크기 조정 기록을 hello 지난 24 시간을 볼 수 있습니다 **실행 기록이** 탭 합니다.

![실행 기록][11]

Tooview hello 전체 눈금 기록 하려는 경우 (에 대 한 일 수까지)을 선택 **여기를 클릭 toosee 자세한 내용을 보려면**합니다. 리소스와 범주를 위해 미리 선택 된 자동 크기 조정이 hello 활동 로그가 열립니다.

### <a name="view-hello-scale-definition-of-your-resource"></a>리소스의 hello 눈금 정의 보기
자동 크기 조정은 Azure Resource Manager의 리소스입니다. Toohello 전환 하 여 JSON에서 hello 눈금 정의 볼 수 **JSON** 탭 합니다.

![크기 조정 정의][12]

필요한 경우 JSON에서 직접 변경할 수 있습니다. 이러한 변경 내용은 저장하고 나면 반영됩니다.

### <a name="disable-autoscale-and-manually-scale-your-instances"></a>자동 크기 조정을 사용하지 않도록 설정하고 인스턴스 크기를 수동으로 조정
있을 시간 원하는 toodisable 현재 크기 조정 설정 하 고 리소스를 수동으로 확장할 수 있습니다.

Hello 클릭 **자동 크기 조정 사용 안 함** hello 위쪽에 단추입니다.
![자동 크기 조정 사용 안 함][13]

> [!NOTE] 
> 이 옵션은 구성을 사용하지 않도록 설정합니다. 그러나 돌아갈 수 있습니다 tooit 다시 자동 크기 조정을 사용 하도록 설정한 후 합니다. 

이제 hello tooscale toomanually 되도록 하는 인스턴스 수를 설정할 수 있습니다.

![수동 크기 조정 설정][14]

클릭 하 여 tooAutoscale를 항상 반환할 수 있습니다 **조정을 사용할** 차례로 **저장**합니다.

## <a name="next-steps"></a>다음 단계
- [활동 로그 경고 toomonitor 구독에 대 한 모든 자동 크기 조정 엔진 작업 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [만들기 작업 로그 경고 toomonitor 구독에 대해 실패 한 모든 자동 크기 조정 눈금-/ 스케일 아웃 작업](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png

