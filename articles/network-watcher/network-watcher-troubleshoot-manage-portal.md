---
title: "Azure Virtual Network 게이트웨이 및 연결 문제 해결 - PowerShell | Microsoft Docs"
description: "이 페이지에서는 Azure Network Watcher 문제 해결 PowerShell cmdlet을 사용하는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: e135e719d8f267f6a189d0f8a903a49980a5a035
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="6bded-103">Azure Network Watcher PowerShell을 사용하여 Virtual Network 게이트웨이 및 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="6bded-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6bded-104">포털</span><span class="sxs-lookup"><span data-stu-id="6bded-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="6bded-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bded-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="6bded-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6bded-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="6bded-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6bded-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="6bded-108">REST API</span><span class="sxs-lookup"><span data-stu-id="6bded-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="6bded-109">Network Watcher는 Azure에서 네트워크 리소스를 이해하는 데 관련된 다양한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="6bded-110">이러한 기능 중 하나는 리소스 문제 해결입니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="6bded-111">리소스 문제 해결은 포털, PowerShell, CLI 또는 REST API를 통해 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="6bded-112">Network Watcher가 호출되면 Virtual Network 게이트웨이 또는 연결의 상태를 검사하거나 해당 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6bded-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="6bded-113">Before you begin</span></span>

<span data-ttu-id="6bded-114">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="6bded-115">지원되는 게이트웨이 유형 목록을 보려면 [지원되는 게이트웨이 유형](network-watcher-troubleshoot-overview.md#supported-gateway-types)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="6bded-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="6bded-116">개요</span><span class="sxs-lookup"><span data-stu-id="6bded-116">Overview</span></span>

<span data-ttu-id="6bded-117">리소스 문제 해결은 Virtual Network 게이트웨이 및 연결에 발생한 문제를 해결하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-117">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="6bded-118">리소스 문제 해결을 요청하는 경우 로그를 쿼리하고 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-118">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="6bded-119">검사가 완료되면 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-119">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="6bded-120">리소스 문제 해결 요청은 장기 실행 요청이며 결과를 반환하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-120">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="6bded-121">문제를 해결하는 로그는 지정된 저장소 계정의 컨테이너에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-121">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="troubleshoot-a-gateway-or-connection"></a><span data-ttu-id="6bded-122">게이트웨이 또는 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="6bded-122">Troubleshoot a gateway or connection</span></span>

1. <span data-ttu-id="6bded-123">[Azure Portal](https://portal.azure.com)로 이동하여 **네트워킹** > **Network Watcher** > **VPN 진단**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-123">Navigate to the [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **VPN Diagnostics**</span></span>
2. <span data-ttu-id="6bded-124">**구독**, **리소스 그룹** 및 **위치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-124">Select a **Subscription**, **Resource Group**, and **Location**.</span></span>
3. <span data-ttu-id="6bded-125">리소스 문제 해결은 리소스 상태에 대한 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-125">Resource troubleshooting returns data about the health of the resource.</span></span> <span data-ttu-id="6bded-126">또한 검토할 관련 로그를 저장소 계정에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-126">It also saves relevant logs to a storage account to be reviewed.</span></span> <span data-ttu-id="6bded-127">**저장소 계정**을 클릭하여 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-127">Click **Storage Account** to select a storage account.</span></span>
4. <span data-ttu-id="6bded-128">**저장소 계정** 블레이드에서 기존 저장소 계정을 선택하거나 **+ 저장소 계정**을 클릭하여 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-128">On the **Storage accounts** blade, select an existing storage account or click **+ Storage account** to create a new one.</span></span>
5. <span data-ttu-id="6bded-129">**컨테이너** 블레이드에서 기존 컨테이너를 선택하거나 **+ 컨테이너**를 클릭하여 새 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-129">On the **Containers** blade, choose an existing container or click **+ Container** to create a new container.</span></span> <span data-ttu-id="6bded-130">완료되면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-130">When complete click **Select**</span></span>
6. <span data-ttu-id="6bded-131">문제를 해결할 게이트웨이 및 연결 리소스를 선택하고 **문제 해결 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-131">Select the Gateway and Connection resources to troubleshoot and click **Start Troubleshooting**</span></span>

<span data-ttu-id="6bded-132">여러 리소스를 선택한 경우 문제 해결은 게이트웨이 리소스에 동시에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-132">If multiple resources are selected, troubleshooting is run concurrently on gateway resources.</span></span> <span data-ttu-id="6bded-133">연결 및 그와 연결된 게이트웨이에서 동시에 실행될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-133">It can not run on a connection and it's associated gateway at the same time.</span></span> <span data-ttu-id="6bded-134">연결 문제 해결이 더 긴 프로세스이므로 게이트웨이 문제를 먼저 해결하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-134">It is recommended to troubleshoot gateways first as connection troubleshooting is a longer process.</span></span> <span data-ttu-id="6bded-135">VPN 진단이 리소스에서 실행 중일 때 **문제 해결 상태** 열에 **실행 중** 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-135">While VPN Diagnostics is running on a resource the **TROUBLESHOOTING STATUS** column will show a status of **Running**</span></span>

<span data-ttu-id="6bded-136">완료되면 상태 열이 **정상** 또는 **비정상**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-136">When complete, the status column changes to **Healthy** or **Unhealthy**.</span></span>

![문제 해결 완료][2]

## <a name="understanding-the-results"></a><span data-ttu-id="6bded-138">결과 이해</span><span class="sxs-lookup"><span data-stu-id="6bded-138">Understanding the results</span></span>

<span data-ttu-id="6bded-139">창의 **세부 정보** 섹션에 있는 **상태** 탭에는 선택한 리소스에 대한 마지막 문제 해결 실행의 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-139">In the **Details** section of the window, the **Status** tab shows the status of the last troubleshooting run on the selected resource.</span></span> <span data-ttu-id="6bded-140">마지막 진단 결과는 마지막 실행 xx분 후에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-140">Results of the latest diagnostic are shown xx minutes after the last run.</span></span>

|<span data-ttu-id="6bded-141">속성</span><span class="sxs-lookup"><span data-stu-id="6bded-141">Property</span></span>  |<span data-ttu-id="6bded-142">설명</span><span class="sxs-lookup"><span data-stu-id="6bded-142">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="6bded-143">리소스</span><span class="sxs-lookup"><span data-stu-id="6bded-143">Resource</span></span>     | <span data-ttu-id="6bded-144">리소스에 대한 링크</span><span class="sxs-lookup"><span data-stu-id="6bded-144">A link to the resource.</span></span>        |
|<span data-ttu-id="6bded-145">저장소 경로</span><span class="sxs-lookup"><span data-stu-id="6bded-145">Storage path</span></span>     |  <span data-ttu-id="6bded-146">로그(실행 중에 생성된 경우)가 포함된 컨테이너 및 저장소 계정 경로</span><span class="sxs-lookup"><span data-stu-id="6bded-146">Path to the storage account and container that contain the logs (if any were produced during the run).</span></span> <span data-ttu-id="6bded-147">이 설정은 포털을 벗어난 후에는 유지되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-147">This setting does not persist after you leave the portal.</span></span>        |
|<span data-ttu-id="6bded-148">요약</span><span class="sxs-lookup"><span data-stu-id="6bded-148">Summary</span></span>     | <span data-ttu-id="6bded-149">리소스 상태에 대한 요약</span><span class="sxs-lookup"><span data-stu-id="6bded-149">Summary of the resource health.</span></span>        |
|<span data-ttu-id="6bded-150">세부 정보</span><span class="sxs-lookup"><span data-stu-id="6bded-150">Detail</span></span>     | <span data-ttu-id="6bded-151">리소스 상태에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="6bded-151">Detailed information on the resource health.</span></span>        |
|<span data-ttu-id="6bded-152">마지막 실행</span><span class="sxs-lookup"><span data-stu-id="6bded-152">Last run</span></span>     | <span data-ttu-id="6bded-153">마지막 문제 해결이 실행된 시간</span><span class="sxs-lookup"><span data-stu-id="6bded-153">The time the last time troubleshooting was ran.</span></span>        |


<span data-ttu-id="6bded-154">**Action** 탭에는 문제를 해결하는 방법에 대한 일반적인 지침이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-154">The **Action** tab provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="6bded-155">문제에 대한 조치를 취할 수 있는 경우 링크는 추가 설명서와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-155">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="6bded-156">추가 지침이 없는 경우에 응답은 지원 사례를 열 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-156">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="6bded-157">응답의 속성 및 포함된 항목에 대한 자세한 내용은 [Network Watcher 문제 해결 개요](network-watcher-troubleshoot-overview.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="6bded-157">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>


## <a name="next-steps"></a><span data-ttu-id="6bded-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6bded-158">Next steps</span></span>

<span data-ttu-id="6bded-159">VPN 연결을 중지하도록 설정이 변경된 경우 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md)를 참조하여 문제가 될 수 있는 네트워크 보안 그룹 및 보안 규칙을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="6bded-159">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
