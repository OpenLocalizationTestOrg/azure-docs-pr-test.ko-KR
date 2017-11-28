---
title: "서버 탐색기에서 Azure Virtual Machines 액세스 | Microsoft Docs"
description: "Visure Studio에서 Azure 서버 탐색기 (VM) 만들기 및 관리하기를 보는 방법에 대한 개요를 가져옵니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: fcbb00cc2f00691e25ea84333e8c418b08210a67
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a><span data-ttu-id="e135d-103">서버 탐색기에서 Azure 가상 컴퓨터 액세스(영문)</span><span class="sxs-lookup"><span data-stu-id="e135d-103">Accessing Azure Virtual Machines from Server Explorer</span></span>
<span data-ttu-id="e135d-104">Visure Studio에서 서버 탐색기를 사용하여 Azure에서 호스팅되는 가상 컴퓨터에 대한 정보를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-104">By using Server Explorer in Visual Studio, you can display information about your virtual machines hosted by Azure.</span></span>

## <a name="accessing-virtual-machines-in-server-explorer"></a><span data-ttu-id="e135d-105">서버 탐색기의 Azure 가상 컴퓨터 액세스</span><span class="sxs-lookup"><span data-stu-id="e135d-105">Accessing virtual machines in Server Explorer</span></span>
<span data-ttu-id="e135d-106">Azure에서 호스팅되는 가상 컴퓨터가 있는 경우 서버 탐색기에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-106">If you have virtual machines hosted by Azure, you can access them in Server Explorer.</span></span> <span data-ttu-id="e135d-107">처음에 Azure 구독에 로그인해야 모바일 서비스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-107">You must first sign in to your Azure subscription to view your mobile services.</span></span> <span data-ttu-id="e135d-108">로그인하려면 서버 탐색기에서 Azure 노드에 대한 바로 가기 메뉴를 열고 **Microsoft Azure에 연결**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-108">To sign in, open the shortcut menu for the Azure node in Server Explorer, and choose **Connect to Microsoft Azure**.</span></span>

### <a name="to-get-information-about-your-virtual-machines"></a><span data-ttu-id="e135d-109">가상 컴퓨터에 대한 정보를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="e135d-109">To get information about your virtual machines</span></span>
1. <span data-ttu-id="e135d-110">서버 탐색기에서 가상 컴퓨터를 선택한 다음 F4 키를 선택하여 속성 창을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-110">In Server Explorer, choose a virtual machine, and then choose the F4 key to show its properties window.</span></span>
   
    <span data-ttu-id="e135d-111">다음의 테이블은 사용 가능하지만 모두 읽기 전용인 속성을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-111">The following table shows what properties are available, but they are all read-only.</span></span> <span data-ttu-id="e135d-112">변경하려면 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-112">To change them, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>
   
   | <span data-ttu-id="e135d-113">속성</span><span class="sxs-lookup"><span data-stu-id="e135d-113">Property</span></span> | <span data-ttu-id="e135d-114">설명</span><span class="sxs-lookup"><span data-stu-id="e135d-114">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="e135d-115">DNS 이름</span><span class="sxs-lookup"><span data-stu-id="e135d-115">DNS Name</span></span> |<span data-ttu-id="e135d-116">가상 컴퓨터의 인터넷 주소 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-116">The URL with the Internet address of the virtual machine.</span></span> |
   | <span data-ttu-id="e135d-117">Environment</span><span class="sxs-lookup"><span data-stu-id="e135d-117">Environment</span></span> |<span data-ttu-id="e135d-118">가상 컴퓨터에 대한 이 속성의 값은 항상 프로덕션입니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-118">For a virtual machine, the value of this property is always Production.</span></span> |
   | <span data-ttu-id="e135d-119">이름</span><span class="sxs-lookup"><span data-stu-id="e135d-119">Name</span></span> |<span data-ttu-id="e135d-120">가상 컴퓨터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-120">The name of the virtual machine.</span></span> |
   | <span data-ttu-id="e135d-121">크기</span><span class="sxs-lookup"><span data-stu-id="e135d-121">Size</span></span> |<span data-ttu-id="e135d-122">사용 가능한 디스크 공간과 메모리의 양이 반영된 가상 컴퓨터의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-122">The size of the virtual machine, which reflects the amount of memory and disk space that’s available.</span></span> <span data-ttu-id="e135d-123">자세한 내용은 가상 컴퓨터 구성 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e135d-123">For more information, see How To: Configure Virtual Machine Sizes.</span></span> |
   | <span data-ttu-id="e135d-124">가동 상태</span><span class="sxs-lookup"><span data-stu-id="e135d-124">Status</span></span> |<span data-ttu-id="e135d-125">값은 시작, 시작됨, 중지, 중지됨 및 상태 검색을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-125">Values include Starting, Started, Stopping, Stopped, and Retrieving Status.</span></span> <span data-ttu-id="e135d-126">상태 검색이 나타나면 현재 상태는 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-126">If Retrieving Status appears, the current status is unknown.</span></span> <span data-ttu-id="e135d-127">이 속성의 값은 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)에서 사용된 값과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-127">The values for this property differ from the values that are used on the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> |
   | <span data-ttu-id="e135d-128">구독 ID</span><span class="sxs-lookup"><span data-stu-id="e135d-128">SubscriptionID</span></span> |<span data-ttu-id="e135d-129">Azure 계정에 대한 구독 ID</span><span class="sxs-lookup"><span data-stu-id="e135d-129">The subscription ID for your Azure account.</span></span> <span data-ttu-id="e135d-130">구독 속성을 확인하여 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)에 대한 정보를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-130">You can show this information on the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) by viewing the properties for a subscription.</span></span> |
2. <span data-ttu-id="e135d-131">끝점 노드를 선택한 다음 **속성** 창을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-131">Choose an endpoint node, and then view the **Properties** window.</span></span>
3. <span data-ttu-id="e135d-132">다음 테이블은 사용 가능하지만 읽기 전용인 끝점 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-132">The following table describes the available properties of endpoints, but they are read-only.</span></span> <span data-ttu-id="e135d-133">가상 컴퓨터에 대해 끝점을 추가 또는 편집하려면 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-133">To add or edit the endpoints for a virtual machine, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> 
   
   | <span data-ttu-id="e135d-134">속성</span><span class="sxs-lookup"><span data-stu-id="e135d-134">Property</span></span> | <span data-ttu-id="e135d-135">설명</span><span class="sxs-lookup"><span data-stu-id="e135d-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="e135d-136">이름</span><span class="sxs-lookup"><span data-stu-id="e135d-136">Name</span></span> |<span data-ttu-id="e135d-137">끝점에 대한 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-137">An identifier for the endpoint.</span></span> |
   | <span data-ttu-id="e135d-138">개인 포트</span><span class="sxs-lookup"><span data-stu-id="e135d-138">Private Port</span></span> |<span data-ttu-id="e135d-139">응용 프로그램의 내부 네트워크 액세스 용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-139">The port for network access internal to your application.</span></span> |
   | <span data-ttu-id="e135d-140">프로토콜</span><span class="sxs-lookup"><span data-stu-id="e135d-140">Protocol</span></span> |<span data-ttu-id="e135d-141">이 끝점에 대한 전송 계층이 사용하는 프로토콜로, TCP 또는 UDP입니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-141">The protocol that the transport layer for this endpoint uses, either TCP or UDP.</span></span> |
   | <span data-ttu-id="e135d-142">공용 포트</span><span class="sxs-lookup"><span data-stu-id="e135d-142">Public Port</span></span> |<span data-ttu-id="e135d-143">응용 프로그램에 대한 공용 액세스에 사용되는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="e135d-143">The port that’s used for public access to your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e135d-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e135d-144">Next steps</span></span>
<span data-ttu-id="e135d-145">Visual Studio에서 Azure 역할을 사용하는 방법에 대한 자세한 내용은 [Azure 역할로 원격 데스크톱 사용](vs-azure-tools-remote-desktop-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e135d-145">To learn more about using Azure roles in Visual Studio, see [Using Remote Desktop with Azure Roles](vs-azure-tools-remote-desktop-roles.md).</span></span>

