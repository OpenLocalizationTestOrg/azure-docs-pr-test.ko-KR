---
title: "Azure IoT Edge 개요 | Microsoft Docs"
description: "게이트웨이, 모듈 및 브로커와 같은 Azure IoT Edge의 주요 아키텍처 개념을 설명합니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: ecdd56c91a8fc2011b3d7abe93b9d27c1e1e0bef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="b4ed0-103">Azure IoT Edge 아키텍처 개념</span><span class="sxs-lookup"><span data-stu-id="b4ed0-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="b4ed0-104">IoT Edge를 사용하여 샘플 코드를 검사하거나 사용자 고유 필드 게이트웨이를 만들기 전에 먼저 IoT Edge 아키텍처의 기반이 되는 주요 개념을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand the key concepts that underpin the architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="b4ed0-105">IoT Edge 모듈</span><span class="sxs-lookup"><span data-stu-id="b4ed0-105">IoT Edge modules</span></span>

<span data-ttu-id="b4ed0-106">*IoT Edge 모듈*을 만들고 조합하여 Azure IoT Edge를 통해 게이트웨이를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="b4ed0-107">모듈은 *메시지* 를 사용하여 서로 데이터를 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-107">Modules use *messages* to exchange data with each other.</span></span> <span data-ttu-id="b4ed0-108">모듈은 메시지를 수신하고, 그에 대해 작업을 수행하고, 필요에 따라 새 메시지로 변환한 다음, 다른 모듈이 처리하도록 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules to process.</span></span> <span data-ttu-id="b4ed0-109">일부 모듈은 새 메시지만 생성하고, 들어오는 메시지를 전혀 처리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="b4ed0-110">일련의 모듈은 각 모듈이 파이프라인 내의 한 지점에서 데이터에 대한 변환을 수행하는 데이터 처리 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-110">A chain of modules creates a data processing pipeline with each module performing a transformation on the data at one point in that pipeline.</span></span>

![Azure IoT Edge로 만든 게이트웨이의 모듈 체인][1]

<span data-ttu-id="b4ed0-112">IoT Edge에는 다음 구성 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-112">IoT Edge contains the following components:</span></span>

* <span data-ttu-id="b4ed0-113">일반 게이트웨이 기능을 수행하는 미리 작성된 모듈.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="b4ed0-114">일반 모듈을 작성하기 위해 개발자가 사용할 수 있는 인터페이스.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-114">The interfaces a developer can use to write custom modules.</span></span>
* <span data-ttu-id="b4ed0-115">모듈 집합을 배포하고 실행하는 데 필요한 인프라.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-115">The infrastructure necessary to deploy and run a set of modules.</span></span>

<span data-ttu-id="b4ed0-116">SDK는 다양한 운영 체제 및 플랫폼에서 실행되는 게이트웨이를 만들 수 있는 추상화 계층을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-116">The SDK provides an abstraction layer that enables you to build gateways to run on various operating systems and platforms.</span></span>

![Azure IoT Edge 추상화 계층][2]

## <a name="messages"></a><span data-ttu-id="b4ed0-118">메시지</span><span class="sxs-lookup"><span data-stu-id="b4ed0-118">Messages</span></span>

<span data-ttu-id="b4ed0-119">모듈이 서로 메시지를 전달하는 것으로 생각하는 것이 게이트웨이 작동 방식을 개념화하는 편리한 방식이지만, 이것은 벌어지는 상황을 정확하게 반영하지는 못합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-119">Although thinking about modules passing messages to each other is a convenient way to conceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="b4ed0-120">IoT Edge 모듈에는 서로 통신하는 broker를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-120">IoT Edge modules use a broker to communicate with each other.</span></span> <span data-ttu-id="b4ed0-121">모듈은 메시지를 broker에 게시하고(버스 또는 게시/가입과 같은 메시징 패턴 사용) broker가 메시지를 연결된 모듈로 라우팅하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-121">Modules publish messages to the broker (using messaging patterns such as bus, or publish/subscribe) and then let the broker route the message to the modules connected to it.</span></span>

<span data-ttu-id="b4ed0-122">모듈은 **Broker_Publish** 함수를 사용하여 broker에 메시지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-122">A module uses the **Broker_Publish** function to publish a message to the broker.</span></span> <span data-ttu-id="b4ed0-123">broker는 콜백 함수를 호출하여 모듈에 메시지를 배달합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-123">The broker delivers messages to a module by invoking a callback function.</span></span> <span data-ttu-id="b4ed0-124">메시지는 키/값 속성 및 메모리 블록으로 전달되는 콘텐츠의 집합으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![Azure IoT Edge에서 broker의 역할][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="b4ed0-126">메시지 라우팅 및 필터링</span><span class="sxs-lookup"><span data-stu-id="b4ed0-126">Message routing and filtering</span></span>

<span data-ttu-id="b4ed0-127">메시지를 올바른 IoT Edge 모듈로 보내는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-127">There are two ways to direct messages to the correct IoT Edge modules:</span></span>

* <span data-ttu-id="b4ed0-128">broker가 각 모듈에 대한 원본 및 싱크를 알 수 있도록 링크 집합을 broker에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-128">You can pass a set of links can be passed to the broker so the broker knows the source and sink for each module.</span></span>
* <span data-ttu-id="b4ed0-129">모듈은 메시지의 속성에서 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-129">A module can filter on the properties of the message.</span></span>

<span data-ttu-id="b4ed0-130">그렇게 의도한 경우에 모듈은 메시지에서만 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-130">A module should only act upon a message if the message is intended for it.</span></span> <span data-ttu-id="b4ed0-131">링크 및 메시지 필터링은 메시지 파이프라인을 효과적으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4ed0-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4ed0-132">Next steps</span></span>

<span data-ttu-id="b4ed0-133">실행할 수 있는 샘플에 이러한 개념이 적용된 것을 확인하려면 [Azure IoT Edge 아키텍처 탐색][lnk-hello-world]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4ed0-133">To see these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md