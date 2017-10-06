---
title: ".NET에서 Azure 릴레이 하이브리드 연결이 aaaGet 시작 | Microsoft Docs"
description: "Azure Relay Hybrid Connections에 대한 C# 콘솔 응용 프로그램 작성"
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d1386900-b942-4abf-acfc-38d2ef826253
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 1e4af28e7cd4393c8ca965a149a0b83ebcc44f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a>릴레이 하이브리드 연결 시작
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

이 자습서에서는 소개 너무[Azure 릴레이 하이브리드 연결](relay-what-is-it.md#hybrid-connections), toouse.NET toocreate 전송 하는 클라이언트 응용 프로그램 tooa 해당 수신기 응용 프로그램 메시지 하는 방법을 보여 줍니다. 

## <a name="what-will-be-accomplished"></a>수행될 작업
하이브리드 연결 클라이언트와 서버 구성 요소를 필요로 하므로 hello 자습서에서는 두 개의 콘솔 응용 프로그램을 만듭니다. Hello 단계는 다음과 같습니다.

1. Hello Azure 포털을 사용 하 여 릴레이 네임 스페이스를 만듭니다.
2. Hello Azure 포털을 사용 하 여 해당 네임 스페이스에서 하이브리드 연결을 만듭니다.
3. 서버 (수신기) 콘솔 응용 프로그램 tooreceive 메시지를 작성 합니다.
4. 클라이언트 (발신자) 콘솔 응용 프로그램 toosend 메시지를 작성 합니다.

## <a name="prerequisites"></a>필수 조건

toocomplete이이 자습서에서는 다음 필수 구성 요소는 hello 필요 합니다.

1. [Visual Studio 2015 이상](http://www.visualstudio.com). 이 자습서의 hello 예제에서는 Visual Studio 2017를 사용 합니다.
2. Azure 구독.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Hello Azure 포털을 사용 하 여 네임 스페이스 만들기
이미 릴레이 네임 스페이스를 만든 경우 점프 toohello [hello Azure 포털을 사용 하 여 하이브리드 연결을 만들](#2-create-a-hybrid-connection-using-the-azure-portal) 섹션.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Hello Azure 포털을 사용 하는 하이브리드 연결 만들기
하이브리드 연결을 이미 만든 경우 점프 toohello [서버 응용 프로그램을 만들](#3-create-a-server-application-listener) 섹션.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. 서버 응용 프로그램(수신기) 만들기
toolisten 메시지를 주고받을 릴레이 hello에서 Visual Studio를 사용 하 여 C# 콘솔 응용 프로그램 작성 하 합니다.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. 클라이언트 응용 프로그램(보낸 사람) 만들기
Visual Studio를 사용 하 여 C# 콘솔 응용 프로그램 작성 하 toosend 메시지 toohello 릴레이 합니다.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Hello 응용 프로그램 실행
1. Hello 서버 응용 프로그램을 실행 합니다.
2. Hello 클라이언트 응용 프로그램을 실행 하 고 일부 텍스트를 입력 합니다.
3. 응용 프로그램 콘솔 출력 hello 텍스트 hello 클라이언트 응용 프로그램에 입력 한 hello 서버를 확인 합니다.

![응용 프로그램 실행](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

축하합니다. 종단 간 하이브리드 연결 응용 프로그램을 만들었습니다.

## <a name="next-steps"></a>다음 단계:
* [릴레이 FAQ](relay-faq.md)
* [네임스페이스 만들기](relay-create-namespace-portal.md)
* [Node 시작](relay-hybrid-connections-node-get-started.md)

