---
title: "aaaCreate Azure 시간 계열 Insights 환경 | Microsoft Docs"
description: "이 자습서에서는 toocreate 시계열 환경은 tooan 이벤트 소스 연결 하 고 분에서 tooanalyze 이벤트 데이터를 준비 하는 방법을 배웁니다."
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a>Hello Azure 포털에서에서 새 시간 시계열 Insights 환경 만들기

Time Series Insights 환경은 수신 및 저장 기능이 있는 Azure 리소스입니다. 고객 환경 hello Azure 포털을 통해 필요한 hello 용량 프로 비전합니다.

## <a name="steps-toocreate-hello-environment"></a>단계 toocreate hello 환경

이러한 단계 toocreate 환경을 수행 합니다.

1.  Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2.  Hello 왼쪽 위 모서리의에서 hello 더하기 기호 ("+")를 클릭 합니다.
3.  Hello 검색 상자에 "시간 시계열 Insights"를 검색 합니다.

  ![Hello 시간 계열 Insights 환경 만들기](media/get-started/getstarted-create-environment1.png)

4.  “Time Series Insights”를 선택하고 “만들기”를 클릭합니다.

  ![Hello 시간 계열 Insights 리소스 그룹 만들기](media/get-started/getstarted-create-environment2.png)

5.  환경 이름을 지정합니다. 이 이름은 hello 환경을 나타낼 [시간 시계열 탐색기](https://insights.timeseries.azure.com)합니다.
6.  구독을 선택합니다. 이벤트 원본이 포함된 구독을 선택해야 합니다. 시간 시계열 Insights 수 자동 검색 Azure IoT Hub 및 이벤트 허브 리소스에 있는 hello 동일한 구독 합니다.
7.  리소스 그룹을 선택하거나 만듭니다. 리소스 그룹은 함께 사용되는 Azure 리소스 컬렉션입니다.
8.  호스팅 위치를 선택합니다. 여러 데이터 tooavoid 이동 데이터 센터는 이벤트 소스를 포함 하는 위치를 선택 합니다.
9.  가격 책정 계층을 선택합니다.
10. 용량을 선택합니다. 환경을 만든 후 환경의 용량을 변경할 수 있습니다.
11. 환경을 만듭니다. 또한에 로그인 할 때마다 쉬운 액세스를 위해 환경 toohello 대시보드를 고정할 수 있습니다.

  ![Hello 시간 계열 Insights pin toodashboard 만들기](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a>다음 단계

* [데이터 액세스 정책을 정의할](time-series-insights-data-access.md) tooaccess 사용자 환경에서 [시간 계열 Insights 포털](https://insights.timeseries.azure.com)
* [이벤트 원본 만들기](time-series-insights-add-event-source.md)
* [이벤트를 보내는](time-series-insights-send-events.md) toohello 이벤트 소스
