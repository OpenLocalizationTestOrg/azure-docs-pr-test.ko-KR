---
title: "Azure Network Watcher를 사용하여 네트워크 보안 그룹 흐름 로그 관리 | Microsoft Docs"
description: "이 페이지에서는 Azure Network Watcher의 네트워크 보안 그룹 흐름 로그를 관리하는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 41cb5ffab9bd3a3bed75ffdb6a7383ca1690f810
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-group-flow-logs-in-the-azure-portal"></a><span data-ttu-id="ace42-103">Azure Portal에서 네트워크 보안 그룹 흐름 로그 관리</span><span class="sxs-lookup"><span data-stu-id="ace42-103">Manage network security group flow logs in the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ace42-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="ace42-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="ace42-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ace42-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="ace42-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ace42-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="ace42-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ace42-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="ace42-108">REST API</span><span class="sxs-lookup"><span data-stu-id="ace42-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="ace42-109">네트워크 보안 그룹 흐름 로그는 네트워크 보안 그룹을 통해 수신 및 송신 IP 트래픽에 대한 정보를 볼 수 있는 Network Watcher의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-109">Network security group flow logs are a feature of Network Watcher that enables you to view information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="ace42-110">이러한 흐름 로그는 JSON 형식으로 작성되며 다음과 같은 중요한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="ace42-111">규칙 단위 기반의 아웃바운드 및 인바운드 흐름</span><span class="sxs-lookup"><span data-stu-id="ace42-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="ace42-112">흐름이 적용되는 NIC</span><span class="sxs-lookup"><span data-stu-id="ace42-112">The NIC that the flow applies to.</span></span>
- <span data-ttu-id="ace42-113">흐름에 대한 5-튜플 정보(원본/대상 IP, 원본/대상 포트, 프로토콜)</span><span class="sxs-lookup"><span data-stu-id="ace42-113">5-tuple information about the flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="ace42-114">트래픽에 대한 허용 또는 거부 여부 정보</span><span class="sxs-lookup"><span data-stu-id="ace42-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ace42-115">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="ace42-115">Before you begin</span></span>

<span data-ttu-id="ace42-116">이 시나리오에서는 [Network Watcher 인스턴스 생성](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-116">This scenario assumes you have already followed the steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="ace42-117">또한 시나리오에서는 유효한 가상 컴퓨터가 있는 리소스 그룹이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-117">The scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="ace42-118">Insights 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="ace42-118">Register Insights provider</span></span>

<span data-ttu-id="ace42-119">흐름 로깅이 성공적으로 작동하기 위해서 **Microsoft.Insights** 공급자를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-119">For flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="ace42-120">공급자를 등록하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-120">To register the provider, take the following steps:</span></span> 

1. <span data-ttu-id="ace42-121">**구독**으로 이동한 다음 흐름 로그를 사용하도록 설정할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-121">Go to **Subscriptions**, and then select the subscription for which you want to enable flow logs.</span></span> 
2. <span data-ttu-id="ace42-122">**구독** 블레이드에서 **리소스 공급자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-122">On the **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="ace42-123">공급자의 목록을 살펴보고 **microsoft.insights** 공급자가 등록되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-123">Look at the list of providers, and verify that the **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="ace42-124">그렇지 않으면 **등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-124">If not, then select **Register**.</span></span>

![공급자 보기][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="ace42-126">흐름 로그를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="ace42-126">Enable flow logs</span></span>

<span data-ttu-id="ace42-127">다음 단계는 네트워크 보안 그룹에서 흐름 로그를 사용하도록 설정하는 프로세스를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-127">These steps take you through the process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="ace42-128">1단계</span><span class="sxs-lookup"><span data-stu-id="ace42-128">Step 1</span></span>

<span data-ttu-id="ace42-129">Network Watcher 인스턴스로 이동한 다음 **NSG 흐름 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-129">Go to a Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![흐름 로그 개요][1]

### <a name="step-2"></a><span data-ttu-id="ace42-131">2단계</span><span class="sxs-lookup"><span data-stu-id="ace42-131">Step 2</span></span>

<span data-ttu-id="ace42-132">목록에서 네트워크 보안 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-132">Select a network security group from the list.</span></span>

![흐름 로그 개요][2]

### <a name="step-3"></a><span data-ttu-id="ace42-134">3단계</span><span class="sxs-lookup"><span data-stu-id="ace42-134">Step 3</span></span> 

<span data-ttu-id="ace42-135">**흐름 로그 설정** 블레이드에서 상태를 **켜기**로 설정한 다음 저장소 계정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-135">On the **Flow logs settings** blade, set the status to **On**, and then configure a storage account.</span></span>  <span data-ttu-id="ace42-136">완료되면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-136">When you're done, select **OK**.</span></span> <span data-ttu-id="ace42-137">그런 다음 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-137">Then select **Save**.</span></span>

![흐름 로그 개요][3]

## <a name="download-flow-logs"></a><span data-ttu-id="ace42-139">흐름 로그 다운로드</span><span class="sxs-lookup"><span data-stu-id="ace42-139">Download flow logs</span></span>

<span data-ttu-id="ace42-140">흐름 로그는 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="ace42-141">보려는 흐름 로그를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-141">Download your flow logs to view them.</span></span>

### <a name="step-1"></a><span data-ttu-id="ace42-142">1단계</span><span class="sxs-lookup"><span data-stu-id="ace42-142">Step 1</span></span>

<span data-ttu-id="ace42-143">흐름 로그를 다운로드하려면 **구성된 저장소 계정에서 흐름 로그를 다운로드할 수 있습니다**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-143">To download flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="ace42-144">이 단계에서는 저장소 계정 보기로 이동하여 다운로드할 로그를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-144">This step takes you to a storage account view where you can choose which logs to download.</span></span>

![흐름 로그 설정][4]

### <a name="step-2"></a><span data-ttu-id="ace42-146">2단계</span><span class="sxs-lookup"><span data-stu-id="ace42-146">Step 2</span></span>

<span data-ttu-id="ace42-147">올바른 저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-147">Go to the correct storage account.</span></span> <span data-ttu-id="ace42-148">그런 다음 **컨테이너** > **insights-log-networksecuritygroupflowevent**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![흐름 로그 설정][5]

### <a name="step-3"></a><span data-ttu-id="ace42-150">3단계</span><span class="sxs-lookup"><span data-stu-id="ace42-150">Step 3</span></span>

<span data-ttu-id="ace42-151">흐름 로그의 위치로 이동하여 선택한 다음 **다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ace42-151">Go to the location of the flow log, select it, and then select **Download**.</span></span>

![흐름 로그 설정][6]

<span data-ttu-id="ace42-153">로그의 구조에 대한 내용은 [네트워크 보안 그룹 흐름 로그 개요](network-watcher-nsg-flow-logging-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ace42-153">For information about the structure of the log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ace42-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ace42-154">Next steps</span></span>

<span data-ttu-id="ace42-155">[PowerBI를 사용하여 NSG 흐름 로그를 시각화](network-watcher-visualize-nsg-flow-logs-power-bi.md)하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="ace42-155">Learn how to [visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
