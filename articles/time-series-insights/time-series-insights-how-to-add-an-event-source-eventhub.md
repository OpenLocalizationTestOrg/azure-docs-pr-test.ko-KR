---
title: "aaaHow tooadd는 이벤트 허브 이벤트 소스 tooyour Azure 시간 계열 Insights 환경 | Microsoft Docs"
description: "이 자습서에서는 어떻게 tooadd 이벤트 원본 즉 tooan 연결 된 이벤트 허브 tooyour 시간 계열 Insights 환경"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: a98cd91deb51c829084a00c5f2a80b39d0fc511c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-event-hub-event-source"></a>어떻게 tooadd 이벤트 허브 이벤트 소스

이 자습서에서는 어떻게 toouse hello Azure 포털 tooadd 이벤트 허브 tooyour 시간 계열 Insights 환경에서 읽을 수 있는 이벤트 소스를 설명 합니다.

## <a name="prerequisites"></a>필수 조건

이벤트 허브를 만든 및 이벤트 tooit를 작성 하는 합니다. 이벤트 허브에 대한 자세한 내용은 <https://azure.microsoft.com/services/event-hubs/>를 참조하세요.

> [소비자 그룹] 각 시간 시계열 Insights 이벤트 소스 toohave 다른 소비자와 공유 되지 않은 자체 전용된 소비자 그룹을 필요 합니다. 여러 판독기를 사용 하는 경우 이벤트를 hello 같은 소비자 그룹, 모든 판독기는 가능성이 toosee 실패 합니다. 또한 이벤트 허브당 20개의 소비자 그룹으로 제한됩니다. 자세한 내용은 참조 hello [이벤트 허브 프로그래밍 가이드](../event-hubs/event-hubs-programming-guide.md)합니다.

## <a name="choose-an-import-option"></a>가져오기 옵션 선택

hello 이벤트 소스에 대 한 hello 설정을 수동으로 입력할 수 또는 사용할 수 있는 tooyou 있는 hello 이벤트 허브에서 이벤트 허브를 선택할 수 있습니다.
Hello에 **가져오기 옵션** 선택기 hello 다음 옵션 중 하나를 선택 합니다.

* 이벤트 허브 설정 직접 입력
* 사용 가능한 구독에서 이벤트 허브 사용

### <a name="select-an-available-event-hub"></a>사용 가능한 이벤트 허브를 선택

hello 다음 표에서 설명 된 hello 새 이벤트 원본을 탭의 각 옵션 이벤트 소스로 사용할 수 있는 이벤트 허브를 선택 하는 경우:

| 속성 이름 | 설명 |
| --- | --- |
| 이벤트 원본 이름 | 이벤트 소스의 hello 이름입니다. 이 이름은 Time Series Insights 환경 내에서 고유해야 합니다.
| 원본 | 선택 **이벤트 허브** toocreate 이벤트 허브 이벤트 소스입니다.
| 구독 ID | 이 이벤트 허브를 만든 hello 구독을 선택 합니다.
| Service Bus 네임스페이스 | Hello 이벤트 허브를 포함 하는 hello 서비스 버스 네임 스페이스를 선택 합니다.
| 이벤트 허브 이름 | Hello 이벤트 허브의 hello 이름을 선택 합니다.
| 이벤트 허브 정책 이름 | Hello 이벤트 허브 구성 탭에서 만들 수 있는 hello 공유 액세스 정책을 선택 합니다. 각 공유 액세스 정책에는 이름, 사용자가 설정한 사용 권한 및 액세스 키가 있습니다. hello 공유 액세스 정책 이벤트 소스에 대 한 *해야* 가 **읽을** 사용 권한.
| 이벤트 허브 소비자 그룹 | hello 소비자 그룹 tooread hello 이벤트 허브에서에서 이벤트입니다. 이 뛰어납니다 toouse 이벤트 소스에 대 한 전용된 소비자 그룹을 권장 합니다.

### <a name="provide-event-hub-settings-manually"></a>이벤트 허브 설정 직접 입력

hello 다음 표에서 설명 된 hello 새 이벤트 원본을 탭의 각 속성 설정을 입력할 때 수동으로:

| 속성 이름 | 설명 |
| --- | --- |
| 이벤트 원본 이름 | 이벤트 소스의 hello 이름입니다. 이 이름은 Time Series Insights 환경 내에서 고유해야 합니다.
| 원본 | 선택 **이벤트 허브** toocreate 이벤트 허브 이벤트 소스입니다.
| 구독 ID | 이 이벤트 허브를 만든 hello 구독입니다.
| 리소스 그룹 | 이 이벤트 허브를 만든 hello 구독입니다.
| Service Bus 네임스페이스 | 서비스 버스 네임스페이스는 메시징 엔터티 집합에 대한 컨테이너입니다. 새 이벤트 허브를 만들 때 서비스 버스 네임스페이스도 만들었습니다.
| 이벤트 허브 이름 | 이벤트 허브의 hello 이름입니다. 이벤트 허브를 만들 때 지은 특정 이름입니다.
| 이벤트 허브 정책 이름 | hello 공유 액세스 정책 hello 이벤트 허브 구성 탭에서 만들 수 있습니다. 각 공유 액세스 정책에는 이름, 사용자가 설정한 사용 권한 및 액세스 키가 있습니다. hello 공유 액세스 정책 이벤트 소스에 대 한 *해야* 가 **읽을** 사용 권한.
| 이벤트 허브 정책 키 | hello 공유 액세스 키 tooauthenticate 액세스 toohello 서비스 버스 네임 스페이스를 사용합니다. Hello 기본 여기 또는 보조 키를 입력 합니다.
| 이벤트 허브 소비자 그룹 | hello 소비자 그룹 tooread hello 이벤트 허브에서에서 이벤트입니다. 이 뛰어납니다 toouse 이벤트 소스에 대 한 전용된 소비자 그룹을 권장 합니다.

## <a name="next-steps"></a>다음 단계

1. 추가 데이터 액세스 정책 tooyour 환경 [정의 데이터 액세스 정책](time-series-insights-data-access.md)
1. 사용자 환경에서 hello 액세스 [시간 계열 Insights 포털](https://insights.timeseries.azure.com)
