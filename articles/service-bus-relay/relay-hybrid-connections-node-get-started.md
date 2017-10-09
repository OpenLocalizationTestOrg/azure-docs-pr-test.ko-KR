---
title: "aaaGet 노드에 Azure 릴레이 하이브리드 연결 시작 | Microsoft Docs"
description: "Azure Relay Hybrid Connections에 대한 Node.js 콘솔 응용 프로그램 작성"
services: service-bus-relay
documentationcenter: node
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e44e4867-3cf3-46be-8f8a-7671e2013bc4
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: node
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 235548399570074f7fd160fec28de8d3633625c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a>릴레이 하이브리드 연결 시작

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

이 자습서에서는 소개 너무[Azure 릴레이 하이브리드 연결](relay-what-is-it.md#hybrid-connections), toouse Node.js toocreate 전송 하는 클라이언트 응용 프로그램 tooa 해당 수신기 응용 프로그램 메시지 하는 방법을 보여 줍니다. 

## <a name="what-will-be-accomplished"></a>수행될 작업

하이브리드 연결에는 클라이언트와 서버 구성 요소가 모두 필요하기 대문에 이 자습서에서는 두 개의 콘솔 응용 프로그램을 만듭니다. Hello 단계는 다음과 같습니다.

1. Hello Azure 포털을 사용 하 여 릴레이 네임 스페이스를 만듭니다.
2. Hello Azure 포털을 사용 하 여 하이브리드 연결을 만듭니다.
3. 콘솔 응용 프로그램 tooreceive 메시지는 서버를 작성 합니다.
4. 클라이언트 콘솔 응용 프로그램 toosend 메시지를 작성 합니다.

## <a name="prerequisites"></a>필수 조건

1. [Node.js](https://nodejs.org/en/).
2. Azure 구독.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Hello Azure 포털을 사용 하 여 네임 스페이스 만들기

릴레이 네임 스페이스를 만들어야 이미 있는 경우 점프 toohello [hello Azure 포털을 사용 하 여 하이브리드 연결을 만들](#2-create-a-hybrid-connection-using-the-azure-portal) 섹션.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Hello Azure 포털을 사용 하는 하이브리드 연결 만들기

생성 한 하이브리드 연결이 이미 있는 경우 점프 toohello [서버 응용 프로그램을 만들](#3-create-a-server-application-listener) 섹션.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. 서버 응용 프로그램(수신기) 만들기

toolisten hello 릴레이에서 메시지를 받을 Node.js 콘솔 응용 프로그램을 작성 하 고 있습니다.

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. 클라이언트 응용 프로그램(보낸 사람) 만들기

toosend 메시지 Node.js 콘솔 응용 프로그램을 작성 하 toohello 릴레이 합니다.

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Hello 응용 프로그램 실행

1. Hello 서버 응용 프로그램을 실행: Node.js 명령 프롬프트 형식에서 `node listener.js`합니다.
2. Hello 클라이언트 응용 프로그램을 실행: Node.js 명령 프롬프트 형식에서 `node sender.js`, 일부 텍스트를 입력 합니다.
3. 응용 프로그램 콘솔 출력 hello 텍스트 hello 클라이언트 응용 프로그램에 입력 한 hello 서버를 확인 합니다.

![응용 프로그램 실행](./media/relay-hybrid-connections-node-get-started/running-applications.png)

축하합니다. Node.js를 사용하여 종단 간 하이브리드 연결 응용 프로그램을 만들었습니다.

## <a name="next-steps"></a>다음 단계:

* [릴레이 FAQ](relay-faq.md)
* [네임스페이스 만들기](relay-create-namespace-portal.md)
* [.NET 시작](relay-hybrid-connections-dotnet-get-started.md)
* [노드 시작](relay-hybrid-connections-node-get-started.md)

