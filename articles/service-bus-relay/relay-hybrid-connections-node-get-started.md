---
title: "Node에서 Azure 릴레이 하이브리드 연결 시작 | Microsoft Docs"
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
ms.openlocfilehash: c3bfc45969f250059988129f532edd12dfe3dcfe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="7755a-103">릴레이 하이브리드 연결 시작</span><span class="sxs-lookup"><span data-stu-id="7755a-103">Get started with Relay Hybrid Connections</span></span>

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="7755a-104">이 자습서에서는 [Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections)를 소개하고 Node.js를 사용하여 메시지를 해당 수신기 응용 프로그램으로 보내는 클라이언트 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7755a-104">This tutorial provides an introduction to [Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how to use Node.js to create a client application that sends messages to a corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="7755a-105">수행될 작업</span><span class="sxs-lookup"><span data-stu-id="7755a-105">What will be accomplished</span></span>

<span data-ttu-id="7755a-106">하이브리드 연결에는 클라이언트와 서버 구성 요소가 모두 필요하기 대문에 이 자습서에서는 두 개의 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7755a-106">Because Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span></span> <span data-ttu-id="7755a-107">단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7755a-107">Here are the steps:</span></span>

1. <span data-ttu-id="7755a-108">Azure 포털을 사용하여 릴레이 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7755a-108">Create a Relay namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="7755a-109">Azure Portal을 사용하여 하이브리드 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7755a-109">Create a hybrid connection, using the Azure portal.</span></span>
3. <span data-ttu-id="7755a-110">메시지를 수신하는 서버 콘솔 응용 프로그램을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="7755a-110">Write a server console application to receive messages.</span></span>
4. <span data-ttu-id="7755a-111">메시지를 보내는 클라이언트 콘솔 응용 프로그램을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="7755a-111">Write a client console application to send messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7755a-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7755a-112">Prerequisites</span></span>

1. <span data-ttu-id="7755a-113">[Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="7755a-113">[Node.js](https://nodejs.org/en/).</span></span>
2. <span data-ttu-id="7755a-114">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="7755a-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="7755a-115">1. Azure Portal을 사용하여 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="7755a-115">1. Create a namespace using the Azure portal</span></span>

<span data-ttu-id="7755a-116">릴레이 네임스페이스를 이미 만든 경우 [Azure Portal을 사용하여 하이브리드 연결 만들기](#2-create-a-hybrid-connection-using-the-azure-portal) 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7755a-116">If you already have a Relay namespace created, jump to the [Create a hybrid connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-the-azure-portal"></a><span data-ttu-id="7755a-117">2. Azure Portal을 사용하여 하이브리드 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="7755a-117">2. Create a hybrid connection using the Azure portal</span></span>

<span data-ttu-id="7755a-118">하이브리드 연결을 이미 만든 경우 [서버 응용 프로그램 만들기](#3-create-a-server-application-listener) 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7755a-118">If you already have a hybrid connection created, jump to the [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="7755a-119">3. 서버 응용 프로그램(수신기) 만들기</span><span class="sxs-lookup"><span data-stu-id="7755a-119">3. Create a server application (listener)</span></span>

<span data-ttu-id="7755a-120">릴레이에서 메시지를 수신하고 받으려면 Node.js 콘솔 응용 프로그램을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="7755a-120">To listen and receive messages from the Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="7755a-121">4. 클라이언트 응용 프로그램(보낸 사람) 만들기</span><span class="sxs-lookup"><span data-stu-id="7755a-121">4. Create a client application (sender)</span></span>

<span data-ttu-id="7755a-122">릴레이에 메시지를 보내려면 Node.js 콘솔 응용 프로그램을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="7755a-122">To send messages to the Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-the-applications"></a><span data-ttu-id="7755a-123">5. 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="7755a-123">5. Run the applications</span></span>

1. <span data-ttu-id="7755a-124">Node.js 명령 프롬프트 형식 `node listener.js`의 서버 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7755a-124">Run the server application: from a Node.js command prompt type `node listener.js`.</span></span>
2. <span data-ttu-id="7755a-125">Node.js 명령 프롬프트 형식 `node sender.js`의 클라이언트 응용 프로그램을 실행하고 일부 텍스트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7755a-125">Run the client application: from a Node.js command prompt type `node sender.js`, and enter some text.</span></span>
3. <span data-ttu-id="7755a-126">서버 응용 프로그램 콘솔이 클라이언트 응용 프로그램에 입력된 텍스트를 출력하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7755a-126">Ensure that the server application console outputs the text that was entered in the client application.</span></span>

![응용 프로그램 실행](./media/relay-hybrid-connections-node-get-started/running-applications.png)

<span data-ttu-id="7755a-128">축하합니다. Node.js를 사용하여 종단 간 하이브리드 연결 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7755a-128">Congratulations, you have created an end-to-end Hybrid Connections application using Node.js!</span></span>

## <a name="next-steps"></a><span data-ttu-id="7755a-129">다음 단계:</span><span class="sxs-lookup"><span data-stu-id="7755a-129">Next steps:</span></span>

* [<span data-ttu-id="7755a-130">릴레이 FAQ</span><span class="sxs-lookup"><span data-stu-id="7755a-130">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="7755a-131">네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="7755a-131">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="7755a-132">.NET 시작</span><span class="sxs-lookup"><span data-stu-id="7755a-132">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="7755a-133">노드 시작</span><span class="sxs-lookup"><span data-stu-id="7755a-133">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

