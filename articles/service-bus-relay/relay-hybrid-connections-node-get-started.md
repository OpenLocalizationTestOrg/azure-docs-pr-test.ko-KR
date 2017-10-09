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
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="4e192-103">릴레이 하이브리드 연결 시작</span><span class="sxs-lookup"><span data-stu-id="4e192-103">Get started with Relay Hybrid Connections</span></span>

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="4e192-104">이 자습서에서는 소개 너무[Azure 릴레이 하이브리드 연결](relay-what-is-it.md#hybrid-connections), toouse Node.js toocreate 전송 하는 클라이언트 응용 프로그램 tooa 해당 수신기 응용 프로그램 메시지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4e192-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse Node.js toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="4e192-105">수행될 작업</span><span class="sxs-lookup"><span data-stu-id="4e192-105">What will be accomplished</span></span>

<span data-ttu-id="4e192-106">하이브리드 연결에는 클라이언트와 서버 구성 요소가 모두 필요하기 대문에 이 자습서에서는 두 개의 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e192-106">Because Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span></span> <span data-ttu-id="4e192-107">Hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4e192-107">Here are hello steps:</span></span>

1. <span data-ttu-id="4e192-108">Hello Azure 포털을 사용 하 여 릴레이 네임 스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e192-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="4e192-109">Hello Azure 포털을 사용 하 여 하이브리드 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e192-109">Create a hybrid connection, using hello Azure portal.</span></span>
3. <span data-ttu-id="4e192-110">콘솔 응용 프로그램 tooreceive 메시지는 서버를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e192-110">Write a server console application tooreceive messages.</span></span>
4. <span data-ttu-id="4e192-111">클라이언트 콘솔 응용 프로그램 toosend 메시지를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e192-111">Write a client console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e192-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4e192-112">Prerequisites</span></span>

1. <span data-ttu-id="4e192-113">[Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="4e192-113">[Node.js](https://nodejs.org/en/).</span></span>
2. <span data-ttu-id="4e192-114">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="4e192-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="4e192-115">1. Hello Azure 포털을 사용 하 여 네임 스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="4e192-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="4e192-116">릴레이 네임 스페이스를 만들어야 이미 있는 경우 점프 toohello [hello Azure 포털을 사용 하 여 하이브리드 연결을 만들](#2-create-a-hybrid-connection-using-the-azure-portal) 섹션.</span><span class="sxs-lookup"><span data-stu-id="4e192-116">If you already have a Relay namespace created, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="4e192-117">2. Hello Azure 포털을 사용 하는 하이브리드 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="4e192-117">2. Create a hybrid connection using hello Azure portal</span></span>

<span data-ttu-id="4e192-118">생성 한 하이브리드 연결이 이미 있는 경우 점프 toohello [서버 응용 프로그램을 만들](#3-create-a-server-application-listener) 섹션.</span><span class="sxs-lookup"><span data-stu-id="4e192-118">If you already have a hybrid connection created, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="4e192-119">3. 서버 응용 프로그램(수신기) 만들기</span><span class="sxs-lookup"><span data-stu-id="4e192-119">3. Create a server application (listener)</span></span>

<span data-ttu-id="4e192-120">toolisten hello 릴레이에서 메시지를 받을 Node.js 콘솔 응용 프로그램을 작성 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e192-120">toolisten and receive messages from hello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="4e192-121">4. 클라이언트 응용 프로그램(보낸 사람) 만들기</span><span class="sxs-lookup"><span data-stu-id="4e192-121">4. Create a client application (sender)</span></span>

<span data-ttu-id="4e192-122">toosend 메시지 Node.js 콘솔 응용 프로그램을 작성 하 toohello 릴레이 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e192-122">toosend messages toohello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="4e192-123">5. Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="4e192-123">5. Run hello applications</span></span>

1. <span data-ttu-id="4e192-124">Hello 서버 응용 프로그램을 실행: Node.js 명령 프롬프트 형식에서 `node listener.js`합니다.</span><span class="sxs-lookup"><span data-stu-id="4e192-124">Run hello server application: from a Node.js command prompt type `node listener.js`.</span></span>
2. <span data-ttu-id="4e192-125">Hello 클라이언트 응용 프로그램을 실행: Node.js 명령 프롬프트 형식에서 `node sender.js`, 일부 텍스트를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e192-125">Run hello client application: from a Node.js command prompt type `node sender.js`, and enter some text.</span></span>
3. <span data-ttu-id="4e192-126">응용 프로그램 콘솔 출력 hello 텍스트 hello 클라이언트 응용 프로그램에 입력 한 hello 서버를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e192-126">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![응용 프로그램 실행](./media/relay-hybrid-connections-node-get-started/running-applications.png)

<span data-ttu-id="4e192-128">축하합니다. Node.js를 사용하여 종단 간 하이브리드 연결 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="4e192-128">Congratulations, you have created an end-to-end Hybrid Connections application using Node.js!</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e192-129">다음 단계:</span><span class="sxs-lookup"><span data-stu-id="4e192-129">Next steps:</span></span>

* [<span data-ttu-id="4e192-130">릴레이 FAQ</span><span class="sxs-lookup"><span data-stu-id="4e192-130">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="4e192-131">네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="4e192-131">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="4e192-132">.NET 시작</span><span class="sxs-lookup"><span data-stu-id="4e192-132">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="4e192-133">노드 시작</span><span class="sxs-lookup"><span data-stu-id="4e192-133">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

