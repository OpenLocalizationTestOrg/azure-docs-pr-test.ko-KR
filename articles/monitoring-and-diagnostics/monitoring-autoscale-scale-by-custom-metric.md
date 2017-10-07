---
title: "자동 크기 조정 하 여 Azure에서 사용자 지정 메트릭을 aaaGet 시작 | Microsoft Docs"
description: "자세한 내용은 방법 tooscale Azure에서 사용자 지정 메트릭 별 리소스입니다."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a>Azure에서 사용자 지정 메트릭을 기준으로 자동 크기 조정 시작
이 문서에서는 설명 방법을 tooscale Azure 포털에서 사용자 지정 메트릭 별 리소스입니다.

모니터 자동 크기 조정 azure tooVirtual 컴퓨터 눈금 집합 (VMSS), 클라우드 서비스, 앱 서비스 계획 및 앱 서비스 환경에 적용합니다. 

# <a name="lets-get-started"></a>시작
이 문서에서는 Application Insights가 구성된 웹앱이 있다고 가정합니다. 아직 없으면 [ASP.NET 웹 사이트에 대한 Application Insights를 설정할 수 있습니다][1].

- [Azure Portal][2]을 엽니다.
- Hello 왼쪽된 탐색 창에서 Azure 모니터 아이콘을 클릭 합니다.
  ![Azure Monitor 시작][3]
- 자동 크기 조정 설정 tooview는 자동 크기 조정 현재 자동 크기 조정 상태와 함께 적용 되는 모든 hello 리소스 클릭 ![자동 크기 조정 Azure 모니터에서 검색][4]
- Azure 모니터에서 '자동 크기 조정' 블레이드를 열고 tooscale 원하는 리소스를 선택 합니다.
> 참고: 다음 hello 단계 app insights 구성 된 웹 앱과 연결 된 하는 앱 서비스 계획을 사용 합니다.
- Hello 리소스에 대 한 크기 조정 설정 블레이드에서 hello hello 현재 인스턴스 수가 1 인지 확인 합니다. '자동 크기 조정 사용'을 클릭합니다.
  ![새 웹앱에 대한 크기 조정 설정][5]
- 이름을 지정 hello 비율 설정을, 고 hello 클릭 "규칙을 추가 합니다."입니다. Hello 오른쪽의 컨텍스트 창으로 열리는 hello 크기 조정 규칙 옵션을 확인 합니다. 기본적으로 hello 옵션 tooscale 인스턴스 수가 1 hello CPU percetage hello 리소스의 70%를 초과 하는 경우 설정 합니다. Hello 메트릭 소스 변경 hello 위쪽에 너무 선택 "Application Insights" hello app insights 리소스 hello 'Resource' 드롭다운와 선택 hello 사용자 지정 메트릭을 기반 tooscale 원하는 합니다.
  ![사용자 지정 메트릭 기준 크기 조정][6]
- 위의 비슷한 toohello 과정으로 크기를 조정 되며 hello 사용자 지정 메트릭이 임계값 미만이 면 hello 확장 개수를 1 씩 감소 하는 크기 조정 규칙을 추가 합니다.
  ![CPU 기준 크기 조정][7]
- Hello 제한 인스턴스를 설정 합니다. 예를 들어 tooscale hello 사용자 지정 메트릭 변동에 따라 2-5 인스턴스 간에, 설정 '최소' 너무 '2', '최대' 너무 '5' 및 '기본' 너무 '2'
> 참고: hello 리소스 메트릭을 읽는 데 문제가 않으며 hello 기본 용량 보다는 hello 현재 용량, 경우에 다음 tooensure hello 가용성 hello 리소스의 자동 크기 조정 됩니다 확장할 toohello 기본값. Hello 현재 용량이 이미 기본 용량 보다 높은 경우 자동 크기 조정에 조정 하지 않습니다.
- '저장'을 클릭합니다.

축하합니다. 사용자 지정 메트릭을 기반 웹 앱을 확장 이제 성공적으로 크기 조정 설정을 tooauto 만들어져 있습니다.

> 참고: hello 동일한 단계는 적용 가능한 tooget VMSS 또는 클라우드 서비스 역할을 시작 합니다.

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
