---
title: "서버 탐색기에서 Azure 가상 컴퓨터 aaaAccessing | Microsoft Docs"
description: "Tooview 만들고 Visual Studio 서버 탐색기에서 Azure 가상 컴퓨터 (Vm) 관리에 대 한 개요를 가져옵니다."
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
ms.openlocfilehash: f8326aed105a64ca558f766d712cc68701f82c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a><span data-ttu-id="fe431-103">서버 탐색기에서 Azure 가상 컴퓨터 액세스(영문)</span><span class="sxs-lookup"><span data-stu-id="fe431-103">Accessing Azure Virtual Machines from Server Explorer</span></span>
<span data-ttu-id="fe431-104">Visure Studio에서 서버 탐색기를 사용하여 Azure에서 호스팅되는 가상 컴퓨터에 대한 정보를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-104">By using Server Explorer in Visual Studio, you can display information about your virtual machines hosted by Azure.</span></span>

## <a name="accessing-virtual-machines-in-server-explorer"></a><span data-ttu-id="fe431-105">서버 탐색기의 Azure 가상 컴퓨터 액세스</span><span class="sxs-lookup"><span data-stu-id="fe431-105">Accessing virtual machines in Server Explorer</span></span>
<span data-ttu-id="fe431-106">Azure에서 호스팅되는 가상 컴퓨터가 있는 경우 서버 탐색기에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-106">If you have virtual machines hosted by Azure, you can access them in Server Explorer.</span></span> <span data-ttu-id="fe431-107">먼저 로그인 해야 tooyour Azure 구독 tooview 모바일 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-107">You must first sign in tooyour Azure subscription tooview your mobile services.</span></span> <span data-ttu-id="fe431-108">에서는 toosign가 서버 탐색기에서 Azure 노드 hello에 대 한 hello 바로 가기 메뉴를 열고 선택 **tooMicrosoft Azure 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-108">toosign in, open hello shortcut menu for hello Azure node in Server Explorer, and choose **Connect tooMicrosoft Azure**.</span></span>

### <a name="tooget-information-about-your-virtual-machines"></a><span data-ttu-id="fe431-109">가상 컴퓨터에 대 한 tooget 정보</span><span class="sxs-lookup"><span data-stu-id="fe431-109">tooget information about your virtual machines</span></span>
1. <span data-ttu-id="fe431-110">서버 탐색기에서 가상 컴퓨터를 선택 하 고 hello F4 키 tooshow 고 속성 창을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-110">In Server Explorer, choose a virtual machine, and then choose hello F4 key tooshow its properties window.</span></span>
   
    <span data-ttu-id="fe431-111">다음 표에 hello 속성을 보여 줍니다를 사용할 수 있지만 모든 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-111">hello following table shows what properties are available, but they are all read-only.</span></span> <span data-ttu-id="fe431-112">toochange hello를 사용 하 여, [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-112">toochange them, use hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>
   
   | <span data-ttu-id="fe431-113">속성</span><span class="sxs-lookup"><span data-stu-id="fe431-113">Property</span></span> | <span data-ttu-id="fe431-114">설명</span><span class="sxs-lookup"><span data-stu-id="fe431-114">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="fe431-115">DNS 이름</span><span class="sxs-lookup"><span data-stu-id="fe431-115">DNS Name</span></span> |<span data-ttu-id="fe431-116">hello 가상 컴퓨터의 인터넷 주소 hello로 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-116">hello URL with hello Internet address of hello virtual machine.</span></span> |
   | <span data-ttu-id="fe431-117">Environment</span><span class="sxs-lookup"><span data-stu-id="fe431-117">Environment</span></span> |<span data-ttu-id="fe431-118">가상 컴퓨터에 대 한이 속성의 hello 값은 항상 프로덕션입니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-118">For a virtual machine, hello value of this property is always Production.</span></span> |
   | <span data-ttu-id="fe431-119">이름</span><span class="sxs-lookup"><span data-stu-id="fe431-119">Name</span></span> |<span data-ttu-id="fe431-120">hello 가상 컴퓨터의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-120">hello name of hello virtual machine.</span></span> |
   | <span data-ttu-id="fe431-121">크기</span><span class="sxs-lookup"><span data-stu-id="fe431-121">Size</span></span> |<span data-ttu-id="fe431-122">hello 양을 사용할 수 있는 메모리와 디스크 공간을 반영 하는 hello 가상 컴퓨터의 hello 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-122">hello size of hello virtual machine, which reflects hello amount of memory and disk space that’s available.</span></span> <span data-ttu-id="fe431-123">자세한 내용은 가상 컴퓨터 구성 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe431-123">For more information, see How To: Configure Virtual Machine Sizes.</span></span> |
   | <span data-ttu-id="fe431-124">가동 상태</span><span class="sxs-lookup"><span data-stu-id="fe431-124">Status</span></span> |<span data-ttu-id="fe431-125">값은 시작, 시작됨, 중지, 중지됨 및 상태 검색을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-125">Values include Starting, Started, Stopping, Stopped, and Retrieving Status.</span></span> <span data-ttu-id="fe431-126">상태 검색에 표시 되 면 hello 현재 상태를 알 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-126">If Retrieving Status appears, hello current status is unknown.</span></span> <span data-ttu-id="fe431-127">hello에 사용 되는 hello 값에서이 속성에 대 한 hello 값이 다른 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-127">hello values for this property differ from hello values that are used on hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> |
   | <span data-ttu-id="fe431-128">구독 ID</span><span class="sxs-lookup"><span data-stu-id="fe431-128">SubscriptionID</span></span> |<span data-ttu-id="fe431-129">Azure 계정에 대 한 hello 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-129">hello subscription ID for your Azure account.</span></span> <span data-ttu-id="fe431-130">Hello에이 정보를 표시할 수 있습니다 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885) 구독에 대 한 hello 속성을 확인 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-130">You can show this information on hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) by viewing hello properties for a subscription.</span></span> |
2. <span data-ttu-id="fe431-131">끝점 노드를 선택한 다음 hello 볼 **속성** 창.</span><span class="sxs-lookup"><span data-stu-id="fe431-131">Choose an endpoint node, and then view hello **Properties** window.</span></span>
3. <span data-ttu-id="fe431-132">hello 다음 표에서 설명 hello 끝점의 사용 가능한 속성이 있지만 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-132">hello following table describes hello available properties of endpoints, but they are read-only.</span></span> <span data-ttu-id="fe431-133">가상 컴퓨터에 대 한 hello 끝점 tooadd 또는 편집 hello를 사용 하 여 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-133">tooadd or edit hello endpoints for a virtual machine, use hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> 
   
   | <span data-ttu-id="fe431-134">속성</span><span class="sxs-lookup"><span data-stu-id="fe431-134">Property</span></span> | <span data-ttu-id="fe431-135">설명</span><span class="sxs-lookup"><span data-stu-id="fe431-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="fe431-136">이름</span><span class="sxs-lookup"><span data-stu-id="fe431-136">Name</span></span> |<span data-ttu-id="fe431-137">Hello 끝점에 대 한 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-137">An identifier for hello endpoint.</span></span> |
   | <span data-ttu-id="fe431-138">개인 포트</span><span class="sxs-lookup"><span data-stu-id="fe431-138">Private Port</span></span> |<span data-ttu-id="fe431-139">네트워크 액세스에 대 한 내부 tooyour 응용 프로그램에 대 한 hello 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-139">hello port for network access internal tooyour application.</span></span> |
   | <span data-ttu-id="fe431-140">프로토콜</span><span class="sxs-lookup"><span data-stu-id="fe431-140">Protocol</span></span> |<span data-ttu-id="fe431-141">TCP 또는 UDP hello 프로토콜 hello이 끝점에 대 한 전송 계층을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-141">hello protocol that hello transport layer for this endpoint uses, either TCP or UDP.</span></span> |
   | <span data-ttu-id="fe431-142">공용 포트</span><span class="sxs-lookup"><span data-stu-id="fe431-142">Public Port</span></span> |<span data-ttu-id="fe431-143">공용 액세스 tooyour 응용 프로그램에 사용 되는 hello 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-143">hello port that’s used for public access tooyour application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fe431-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fe431-144">Next steps</span></span>
<span data-ttu-id="fe431-145">Visual Studio에서 Azure 역할 사용에 대 한 더 toolearn 참조 [Azure 역할과 함께 원격 데스크톱 사용 하 여](vs-azure-tools-remote-desktop-roles.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe431-145">toolearn more about using Azure roles in Visual Studio, see [Using Remote Desktop with Azure Roles](vs-azure-tools-remote-desktop-roles.md).</span></span>

