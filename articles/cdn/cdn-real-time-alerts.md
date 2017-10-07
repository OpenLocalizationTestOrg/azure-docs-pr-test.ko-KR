---
title: "aaaAzure CDN 실시간 경고 | Microsoft Docs"
description: "Microsoft Azure CDN의 실시간 경고입니다. 실시간 경고 hello 끝점에서 CDN 프로필의 hello 성능에 대 한 알림을 제공합니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 1e85b809-e1a9-4473-b835-69d1b4ed3393
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 269c90437088bbc41bf899a8c02749e8e6f3006c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a>Microsoft Azure CDN의 실시간 경고
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>개요
이 문서에서는 Microsoft Azure CDN의 실시간 경고에 대해 설명합니다. 이 기능은 CDN 프로필의 hello 끝점 hello 성능에 대 한 실시간 알림을 제공합니다.  다음을 기반으로 전자 메일 또는 HTTP 경고를 설정할 수 있습니다.

* 대역폭
* 상태 코드
* 캐시 상태
* 연결

## <a name="creating-a-real-time-alert"></a>실시간 경고 만들기
1. Hello에 [Azure 포털](https://portal.azure.com), tooyour CDN 프로필을 찾습니다.
   
    ![CDN 프로필 블레이드](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. Hello CDN 프로필 블레이드에서 hello 클릭 **관리** 단추입니다.
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    hello CDN 관리 포털이 열립니다.
3. 마우스 포인터를 놓고 hello **분석** 누른 마우스 포인터를 놓고 hello **실시간 통계** 플라이 아웃입니다.  **실시간 경고**를 클릭합니다.
   
    ![CDN 관리 포털](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    기존 경고 구성 (있는 경우)의 hello 목록이 표시 됩니다.
4. Hello 클릭 **경고 추가** 단추입니다.
   
    ![경고 추가 단추](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    새 경고를 만드는 양식이 표시됩니다.
   
    ![새 경고 양식](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. 이 경고 toobe 활성 하려면 클릭할 때 **저장**, hello 확인 **경고가 활성화** 확인란을 선택 합니다.
6. Hello에 따라 경고에 대 한 설명이 포함 된 이름을 입력 **이름** 필드입니다.
7. Hello에 **미디어 유형** 드롭다운 **HTTP 대형 개체**합니다.
   
    ![HTTP LOB(Large Object)를 선택한 미디어 유형](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > 선택 해야 **HTTP 대형 개체** hello로 **미디어 유형**합니다.  hello 다른 선택 항목에서 사용 하지 않는 **Verizon에서 Azure CDN**합니다.  오류 tooselect **HTTP 대형 개체** 결제 경고가 발생 합니다 toonever 트리거될 수 있습니다.
   > 
   > 
8. 만들기는 **식** 선택 하 여 toomonitor는 **메트릭을**, **연산자**, 및 **값 트리거할**합니다.
   
   * 에 대 한 **메트릭을**를 모니터링할 조건의 hello 유형을 선택 합니다.  **대역폭 Mbps** hello 양의 초당 메가 비트에서 대역폭 사용 합니다.  **총 연결** 동시 HTTP 연결 tooour hello 수에 지 서버입니다.  다양 한 캐시 상태 및 상태 코드 참조에 대 한 hello 정의 [Azure CDN 캐시 상태 코드](https://msdn.microsoft.com/library/mt759237.aspx) 및 [Azure CDN HTTP 상태 코드](https://msdn.microsoft.com/library/mt759238.aspx)
   * **연산자** hello 메트릭 및 hello 트리거 값 간에 hello 관계를 설정 하는 hello 수학 연산자.
   * **트리거 값** hello 알림이 전송 하기 위해 충족 되어야 하는 것이 임계값은 합니다.
     
     아래 예제는 hello, 만든 hello 식 404 상태 코드의 hello 수는 25 보다 큰 경우 알림을 받는 toobe 싶습니다 나타냅니다.
     
     ![실시간 경고 샘플 식](./media/cdn-real-time-alerts/cdn-expression.png)
9. 에 대 한 **간격**를 얼마나 자주 원하는 hello 식이 입력 합니다.
10. Hello에 **알림** 드롭다운을 toobe 때 알림을 받으려면 hello 식이 true 인 경우 선택 합니다.
    
    * **시작 조건** hello를 지정 된 조건이 처음 감지 된 경우 알림이 전송 되지 않음을 나타내는입니다.
    * **끝 조건을** hello를 지정 된 조건이 더 이상 검색 하는 경우 알림이 전송 되지 않음을 나타내는입니다. 모니터링 시스템이 네트워크에 지정 된 해당 hello 검색 된 후에이 알림 메시지를 트리거할 수 조건이 발생 합니다.
    * **연속** 네트워크 모니터링 시스템 hello 때마다 지정 된 hello 검색으로 알림을 보낼 수 나타냅니다 조건입니다. 모니터링 시스템을 검사 한 번 hello에 대 한 간격 마다 지정 조건에만 해당 hello 네트워크를 명심 하십시오.
    * **조건 시작 및 끝** hello hello 지정 된 조건이 처음으로 검색 되 고 다시 한 번 hello 조건이 감지 되 면 더 이상으로 알림이 전송 수를 나타냅니다.
11. 전자 메일을 통해 tooreceive 알림을 원하는 경우 확인 hello **알림 전자 메일을 통해** 확인란을 선택 합니다.  
    
    ![전자 메일로 알림 양식](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    Hello에 **를** 필드 알림을 원하는 보낸 hello 전자 메일 주소를 입력 합니다. 에 대 한 **주체** 및 **본문**hello 기본 수준은 낮아질 수 있습니다, 또는 hello를 사용 하 여 hello 메시지를 사용자 지정할 수 있습니다 **사용할 수 있는 키워드** 목록 toodynamically 경고 데이터를 삽입할 때 hello 메시지가 전송 됩니다.
    
    > [!NOTE]
    > Hello를 클릭 하 여 hello 전자 메일 알림을 테스트할 수 있습니다 **테스트 알림** 단추만 hello 경고 구성을 저장 한 후 합니다.
    > 
    > 
12. 알림 toobe tooa 웹 서버에 게시 하려는 경우 확인 hello **HTTP Post로 알림** 확인란을 선택 합니다.
    
    ![HTTP 게시로 알림 양식](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    Hello에 **Url** 필드 hello URL을 게시 하려는 HTTP hello 메시지를 입력 합니다. Hello에 **헤더** textbox hello 요청에서 전송 하는 hello HTTP 헤더 toobe를 입력 합니다.  에 대 한 **본문** hello를 사용 하 여 hello 메시지를 사용자 지정할 수 있습니다 **사용할 수 있는 키워드** 목록 toodynamically hello 메시지를 보낼 때 경고 데이터를 삽입 합니다.  **헤더** 및 **본문** tooan XML 페이로드 아래 예제와 비슷한 toohello 기본 합니다.
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > Hello를 클릭 하 여 HTTP Post 알림 hello를 테스트할 수 있습니다 **테스트 알림** 단추만 hello 경고 구성을 저장 한 후 합니다.
    > 
    > 
13. Hello 클릭 **저장** 단추 toosave 경고 구성 합니다.  5단계에서 **경고 사용** 을 선택한 경우 경고는 지금 활성화됩니다.

## <a name="next-steps"></a>다음 단계
* [Azure CDN의 실시간 통계](cdn-real-time-stats.md)
* [고급 HTTP 보고서](cdn-advanced-http-reports.md)
* [사용 패턴](cdn-analyze-usage-patterns.md)

