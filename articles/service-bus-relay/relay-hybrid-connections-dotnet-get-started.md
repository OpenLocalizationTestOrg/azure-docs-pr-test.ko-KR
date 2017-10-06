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
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="e5bab-103">릴레이 하이브리드 연결 시작</span><span class="sxs-lookup"><span data-stu-id="e5bab-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="e5bab-104">이 자습서에서는 소개 너무[Azure 릴레이 하이브리드 연결](relay-what-is-it.md#hybrid-connections), toouse.NET toocreate 전송 하는 클라이언트 응용 프로그램 tooa 해당 수신기 응용 프로그램 메시지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e5bab-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse .NET toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="e5bab-105">수행될 작업</span><span class="sxs-lookup"><span data-stu-id="e5bab-105">What will be accomplished</span></span>
<span data-ttu-id="e5bab-106">하이브리드 연결 클라이언트와 서버 구성 요소를 필요로 하므로 hello 자습서에서는 두 개의 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5bab-106">Because Hybrid Connections requires both a client and a server component, hello tutorial creates two console applications.</span></span> <span data-ttu-id="e5bab-107">Hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e5bab-107">Here are hello steps:</span></span>

1. <span data-ttu-id="e5bab-108">Hello Azure 포털을 사용 하 여 릴레이 네임 스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5bab-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="e5bab-109">Hello Azure 포털을 사용 하 여 해당 네임 스페이스에서 하이브리드 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5bab-109">Create a hybrid connection in that namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="e5bab-110">서버 (수신기) 콘솔 응용 프로그램 tooreceive 메시지를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5bab-110">Write a server (listener) console application tooreceive messages.</span></span>
4. <span data-ttu-id="e5bab-111">클라이언트 (발신자) 콘솔 응용 프로그램 toosend 메시지를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5bab-111">Write a client (sender) console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5bab-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e5bab-112">Prerequisites</span></span>

<span data-ttu-id="e5bab-113">toocomplete이이 자습서에서는 다음 필수 구성 요소는 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5bab-113">toocomplete this tutorial, you'll need hello following prerequisites:</span></span>

1. <span data-ttu-id="e5bab-114">[Visual Studio 2015 이상](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="e5bab-114">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="e5bab-115">이 자습서의 hello 예제에서는 Visual Studio 2017를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5bab-115">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="e5bab-116">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="e5bab-116">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="e5bab-117">1. Hello Azure 포털을 사용 하 여 네임 스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="e5bab-117">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="e5bab-118">이미 릴레이 네임 스페이스를 만든 경우 점프 toohello [hello Azure 포털을 사용 하 여 하이브리드 연결을 만들](#2-create-a-hybrid-connection-using-the-azure-portal) 섹션.</span><span class="sxs-lookup"><span data-stu-id="e5bab-118">If you have already created a Relay namespace, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="e5bab-119">2. Hello Azure 포털을 사용 하는 하이브리드 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="e5bab-119">2. Create a hybrid connection using hello Azure portal</span></span>
<span data-ttu-id="e5bab-120">하이브리드 연결을 이미 만든 경우 점프 toohello [서버 응용 프로그램을 만들](#3-create-a-server-application-listener) 섹션.</span><span class="sxs-lookup"><span data-stu-id="e5bab-120">If you have already created a hybrid connection, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="e5bab-121">3. 서버 응용 프로그램(수신기) 만들기</span><span class="sxs-lookup"><span data-stu-id="e5bab-121">3. Create a server application (listener)</span></span>
<span data-ttu-id="e5bab-122">toolisten 메시지를 주고받을 릴레이 hello에서 Visual Studio를 사용 하 여 C# 콘솔 응용 프로그램 작성 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5bab-122">toolisten and receive messages from hello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="e5bab-123">4. 클라이언트 응용 프로그램(보낸 사람) 만들기</span><span class="sxs-lookup"><span data-stu-id="e5bab-123">4. Create a client application (sender)</span></span>
<span data-ttu-id="e5bab-124">Visual Studio를 사용 하 여 C# 콘솔 응용 프로그램 작성 하 toosend 메시지 toohello 릴레이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5bab-124">toosend messages toohello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="e5bab-125">5. Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="e5bab-125">5. Run hello applications</span></span>
1. <span data-ttu-id="e5bab-126">Hello 서버 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5bab-126">Run hello server application.</span></span>
2. <span data-ttu-id="e5bab-127">Hello 클라이언트 응용 프로그램을 실행 하 고 일부 텍스트를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5bab-127">Run hello client application and enter some text.</span></span>
3. <span data-ttu-id="e5bab-128">응용 프로그램 콘솔 출력 hello 텍스트 hello 클라이언트 응용 프로그램에 입력 한 hello 서버를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5bab-128">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![응용 프로그램 실행](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="e5bab-130">축하합니다. 종단 간 하이브리드 연결 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e5bab-130">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5bab-131">다음 단계:</span><span class="sxs-lookup"><span data-stu-id="e5bab-131">Next steps:</span></span>
* [<span data-ttu-id="e5bab-132">릴레이 FAQ</span><span class="sxs-lookup"><span data-stu-id="e5bab-132">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="e5bab-133">네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="e5bab-133">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="e5bab-134">Node 시작</span><span class="sxs-lookup"><span data-stu-id="e5bab-134">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

