---
title: "Azure CDN에서 aaaReal 시간 통계 | Microsoft Docs"
description: "실시간 통계 콘텐츠 tooyour 클라이언트 배달할 때 Azure CDN의 hello 성능에 대 한 실시간 데이터를 제공 합니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a>Microsoft Azure CDN의 실시간 통계
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>개요
이 문서에서는 Microsoft Azure CDN의 실시간 통계에 대해 설명합니다.  이 기능은 대역폭, 캐시 상태 및 동시 연결 tooyour CDN 프로필 콘텐츠 tooyour 클라이언트 배달할 때 같은 실시간 데이터를 제공 합니다. 이렇게 하면 언제 든 지 go 라이브 이벤트를 포함 하 여 서비스의 hello 상태에 대 한 지속적인 모니터링입니다.

다음 그래프 hello 사용할 수 있습니다.

* [대역폭](#bandwidth)
* [상태 코드](#status-codes)
* [캐시 상태](#cache-statuses)
* [연결](#connections)

## <a name="accessing-real-time-stats"></a>실시간 통계에 액세스
1. Hello에 [Azure 포털](https://portal.azure.com), tooyour CDN 프로필을 찾습니다.
   
    ![CDN 프로필 블레이드](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. Hello CDN 프로필 블레이드에서 hello 클릭 **관리** 단추입니다.
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    hello CDN 관리 포털이 열립니다.
3. 마우스 포인터를 놓고 hello **분석** 누른 마우스 포인터를 놓고 hello **실시간 통계** 플라이 아웃입니다.  **HTTP 큰 개체**를 클릭합니다.
   
    ![CDN 관리 포털](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    hello 실시간 통계 그래프가 표시 됩니다.

Hello 그래프의 각 hello 페이지가 로드 될 때 시작 시간 범위를 선택 하는 hello에 대 한 실시간 통계를 표시 합니다.  hello 그래프는 몇 초 마다 자동으로 업데이트 합니다.  hello **새로 고침 그래프** 단추, 있는 경우 지워집니다 hello 그래프는 하나만 표시 됩니다 hello 선택한 데이터입니다.

## <a name="bandwidth"></a>대역폭
![대역폭 그래프](./media/cdn-real-time-stats/cdn-bandwidth.png)

hello **대역폭** hello hello 선택한 시간 범위를 통한 hello 현재 플랫폼에 사용 되는 대역폭 양을 그래프에 표시 됩니다. hello 그래프의 음영 처리 된 부분 hello 대역폭 사용량을 나타냅니다. 현재 사용 중인 대역폭의 hello 정확한 양은 hello 선 그래프 바로 아래에 표시 됩니다.

## <a name="status-codes"></a>상태 코드
![상태 코드 그래프](./media/cdn-real-time-stats/cdn-status-codes.png)

hello **상태 코드** 그래프 hello 선택한 시간 범위를 통해 특정 HTTP 응답 코드 발생 빈도 나타냅니다.

> [!TIP]
> 각 HTTP 상태 코드 옵션에 대한 설명은 [Azure CDN HTTP 상태 코드](https://msdn.microsoft.com/library/mt759238.aspx)를 참조하세요.
> 
> 

HTTP 상태 코드의 목록은 hello 그래프 바로 위에 표시 됩니다. 이 목록은 hello 선 그래프 및 hello 현재 해당 상태 코드에 대 한 초당 발생 수에 포함 될 수 있는 각 상태 코드를 나타냅니다. 기본적으로 줄은 각각 hello 그래프에서이 상태 코드에 대해 표시 됩니다. 그러나 CDN 구성에 대 한 특별 한 의미가 모니터 hello 상태 코드 tooonly를 선택할 수 있습니다. toodo이 확인 hello 원하는 상태 코드 및 다른 모든 옵션의 선택을 취소 한 다음 클릭 **새로 고침 그래프**합니다. 

특정 상태 코드에 대해 기록된 데이터를 임시로 숨길 수 있습니다.  Hello hello 그래프 바로 아래 범례에서 원하는 toohide hello 상태 코드를 클릭 합니다. hello 상태 코드는 hello 그래프에서 즉시 표시 되지 것입니다. 해당 상태 코드를 다시 클릭 하면 해당 옵션 toobe 다시 표시 하면 됩니다.

## <a name="cache-statuses"></a>캐시 상태
![캐시 상태 그래프](./media/cdn-real-time-stats/cdn-cache-status.png)

hello **캐시 상태** 그래프 hello 선택한 시간 범위를 통해 특정 유형의 캐시 상태 발생 빈도 나타냅니다. 

> [!TIP]
> 각 캐시 상태 코드 옵션에 대한 설명은 [Azure CDN 캐시 상태 코드](https://msdn.microsoft.com/library/mt759237.aspx)를 참조하세요.
> 
> 

캐시 상태 코드의 목록은 hello 그래프 바로 위에 표시 됩니다. 이 목록은 hello 선 그래프 및 hello 현재 해당 상태 코드에 대 한 초당 발생 수에 포함 될 수 있는 각 상태 코드를 나타냅니다. 기본적으로 줄은 각각 hello 그래프에서이 상태 코드에 대해 표시 됩니다. 그러나 CDN 구성에 대 한 특별 한 의미가 모니터 hello 상태 코드 tooonly를 선택할 수 있습니다. toodo이 확인 hello 원하는 상태 코드 및 다른 모든 옵션의 선택을 취소 한 다음 클릭 **새로 고침 그래프**합니다. 

특정 상태 코드에 대해 기록된 데이터를 임시로 숨길 수 있습니다.  Hello hello 그래프 바로 아래 범례에서 원하는 toohide hello 상태 코드를 클릭 합니다. hello 상태 코드는 hello 그래프에서 즉시 표시 되지 것입니다. 해당 상태 코드를 다시 클릭 하면 해당 옵션 toobe 다시 표시 하면 됩니다.

## <a name="connections"></a>연결
![연결 그래프](./media/cdn-real-time-stats/cdn-connections.png)

이 그래프는 연결 수 설정 된 tooyour에 지 서버 였을 나타냅니다. CDN을 통과하는 자산에 대한 각 요청은 연결을 발생시킵니다.

## <a name="next-steps"></a>다음 단계
* [Azure CDN에서 실시간 경고](cdn-real-time-alerts.md)
* [고급 HTTP 보고서](cdn-advanced-http-reports.md)
* [사용 패턴](cdn-analyze-usage-patterns.md)

