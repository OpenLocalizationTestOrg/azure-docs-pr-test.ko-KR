---
title: "aaaHow toocreate hello Azure 포털에서에서 서비스 버스 네임 스페이스 | Microsoft Docs"
description: "Hello Azure 포털을 사용 하 여 서비스 버스 네임 스페이스를 만듭니다."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fbb10e62-b133-4851-9d27-40bd844db3ba
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: d8907e7e4a804056f6d66d5a177d9ace967ed2ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 서비스 버스 네임 스페이스 만들기

네임스페이스는 모든 메시징 구성 요소에 대한 영역 컨테이너입니다. 여러 큐 및 토픽은 단일 네임스페이스 내에 있을 수 있으며 네임스페이스는 종종 응용 프로그램 컨테이너로 사용됩니다. 두 가지 방법으로 toocreate 서비스 버스 네임 스페이스 가지가 있습니다.

1. Azure Portal(이 문서)
2. [Resource Manager 템플릿][create-namespace-using-arm]

## <a name="create-a-namespace-in-hello-azure-portal"></a>Hello Azure 포털에서에서 네임 스페이스 만들기

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

축하합니다. 이제 Service Bus 메시징 네임스페이스를 만들었습니다.

## <a name="next-steps"></a>다음 단계

체크 아웃 우리의 [GitHub 샘플][github-samples], Azure 서비스 버스 메시징 기능을 더 높은 수준의 hello 중 일부를 표시 하는 합니다.

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure/azure-service-bus/tree/master/samples
