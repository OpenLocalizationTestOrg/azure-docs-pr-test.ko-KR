---
title: "큐 저장소 aaaIntroduction tooAzure | Microsoft Docs"
description: "소개 tooAzure 큐 저장소"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: robinsh
ms.openlocfilehash: 669effedff7beedde8a119c350a2a70edafedcf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooqueues"></a>소개 tooQueues

Azure 큐 저장소는 많은 수의 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 사용 하 여 인증 된 호출을 통해 hello world에 메시지를 저장 하기 위한 서비스입니다. 단일 큐 메시지의 크기 (kb) too64 될 수 있습니다 및 큐 수많은 메시지 저장소 계정의 toohello 총 용량 한계를 포함할 수 있습니다.

## <a name="common-uses"></a>일반적인 사용

큐 저장소의 일반적인 사용은 다음과 같습니다.

* 작업 tooprocess의 백로그를 비동기적으로 만들기
* Azure 웹 역할 tooan Azure 작업자 역할에서 메시지를 전달합니다.

## <a name="queue-service-concepts"></a>큐 서비스 개념

hello를 큐 서비스는 hello를 다음과 같은 구성 요소가 포함 되어 있습니다.

![큐 개념](./media/storage-queues-introduction/queue1.png)

* **URL 형식:** 큐는 주소 지정 가능한 URL 형식에 따라 hello를 사용 하 여:   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    url hello hello 다이어그램의 큐를 해결할 수 있습니다.  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **저장소 계정:** 저장소 계정을 통해 모든 액세스 tooAzure 저장소 작업은 수행 됩니다. 저장소 계정 용량에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) (영문)를 참조하십시오.

* **큐:** 큐에는 메시지 집합이 포함됩니다. 모든 메시지는 큐에 있어야 합니다. Note 해당 hello 큐 이름은 모두 소문자 여야 합니다. 큐의 명명에 대한 자세한 내용은 [큐 및 메타데이터 명명](https://msdn.microsoft.com/library/azure/dd179349.aspx)을 참조하세요.

* **메시지:** A 메시지, 모든 형식으로의 too64 KB를 합니다. hello 메시지 hello 큐에 남아 있을 수 있는 최대 시간은 7 일입니다.

## <a name="next-steps"></a>다음 단계

* [저장소 계정을 만드는](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [.NET을 사용하여 큐 시작하기](storage-dotnet-how-to-use-queues.md)
