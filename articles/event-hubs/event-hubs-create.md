---
title: "Azure 이벤트 허브 aaaCreate | Microsoft Docs"
description: "Azure 이벤트 허브 네임 스페이스 및 hello Azure 포털을 사용 하 여 이벤트 허브 만들기"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a>이벤트 허브 네임 스페이스 및 hello Azure 포털을 사용 하 여 이벤트 허브 만들기

## <a name="create-an-event-hubs-namespace"></a>Event Hubs 네임스페이스 만들기
1. Toohello 로그온 [Azure 포털][Azure portal], 클릭 하 고 **새로** hello에 왼쪽 상단 hello 화면에 있습니다.
1. **사물 인터넷**을 클릭한 다음 **Event Hubs**를 클릭합니다.
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. Hello에 **네임 스페이스 만들기** 블레이드에서 네임 스페이스 이름을 입력 합니다. hello 시스템 hello 이름이 사용 가능한 경우 즉시 toosee를 확인 합니다.
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. 만드는 있는지 hello 네임 스페이스 이름을 사용할 수 있는 되 면 hello 가격 책정 계층 (기본 또는 표준)를 선택 합니다. 또한 toocreate hello 리소스에는 Azure 구독, 리소스 그룹 및 위치를 선택 합니다. 
1. 클릭 **만들기** toocreate hello 네임 스페이스입니다. Toowait 몇 분 정도 hello 시스템 toofully hello 리소스를 제공 해야 합니다.
2. 네임 스페이스의 hello 포털 목록에서 새로 생성 된 네임 스페이스 hello를 클릭 합니다.
2. **공유 액세스 정책**을 클릭한 후 **RootManageSharedAccessKey**를 클릭합니다.
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. Hello 복사 단추 toocopy hello 클릭 **RootManageSharedAccessKey** 연결 문자열 toohello 클립보드 합니다. 나중에 toouse 메모장 등의 임시 위치에이 연결 문자열을 저장 합니다.
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a>이벤트 허브 만들기

1. Hello 이벤트 허브 네임 스페이스 목록에서 새로 만든 hello 네임 스페이스를 클릭 합니다.      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. Hello 네임 스페이스 블레이드에서 클릭 **이벤트 허브**합니다.
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. Hello 블레이드의 hello 위쪽 클릭 **이벤트 허브 추가**합니다.
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. 이벤트 허브의 이름을 입력한 다음 **만들기**를 클릭합니다.
   
    ![](./media/event-hubs-create/create-event-hub5.png)

이벤트 허브 이제 만들어지고 hello 연결 문자열이 toosend 필요 하 고 이벤트를 수신 합니다.

## <a name="next-steps"></a>다음 단계
다음이 링크를 방문 하는 이벤트 허브에 대해 자세히 toolearn:

* [이벤트 허브 개요](event-hubs-what-is-event-hubs.md)
* [이벤트 허브 API 개요](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/