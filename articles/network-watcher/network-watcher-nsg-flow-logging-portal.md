---
title: "Azure 네트워크 감시자를 사용 하 여 aaaManage 네트워크 보안 그룹 흐름 로그 | Microsoft Docs"
description: "이 페이지에서는 toomanage 네트워크 보안 그룹 흐름 Azure 네트워크 감시자 로그인 하는 방법을 설명 합니다."
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
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a><span data-ttu-id="7b58a-103">Hello Azure 포털에서에서 네트워크 보안 그룹 흐름 로그 관리</span><span class="sxs-lookup"><span data-stu-id="7b58a-103">Manage network security group flow logs in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="7b58a-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="7b58a-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="7b58a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b58a-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="7b58a-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7b58a-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="7b58a-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7b58a-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="7b58a-108">REST API</span><span class="sxs-lookup"><span data-stu-id="7b58a-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="7b58a-109">네트워크 보안 그룹 흐름 로그는 네트워크 보안 그룹을 통해 IP 트래픽 ingress 및 egress에 대 한 tooview 정보를 사용 하면 네트워크 감시자의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-109">Network security group flow logs are a feature of Network Watcher that enables you tooview information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="7b58a-110">이러한 흐름 로그는 JSON 형식으로 작성되며 다음과 같은 중요한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="7b58a-111">규칙 단위 기반의 아웃바운드 및 인바운드 흐름</span><span class="sxs-lookup"><span data-stu-id="7b58a-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="7b58a-112">hello 흐름 hello NIC에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-112">hello NIC that hello flow applies to.</span></span>
- <span data-ttu-id="7b58a-113">hello 흐름 (소스/대상 IP, 소스/대상 포트, 프로토콜)에 대 한 정보를 5-튜플입니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-113">5-tuple information about hello flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="7b58a-114">트래픽에 대한 허용 또는 거부 여부 정보</span><span class="sxs-lookup"><span data-stu-id="7b58a-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7b58a-115">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="7b58a-115">Before you begin</span></span>

<span data-ttu-id="7b58a-116">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자 인스턴스를 만들고](network-watcher-create.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="7b58a-117">hello 시나리오도 있다고 가정 합니다는 적합 한 가상 컴퓨터가 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-117">hello scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="7b58a-118">Insights 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="7b58a-118">Register Insights provider</span></span>

<span data-ttu-id="7b58a-119">흐름에 대 한 로깅 toowork 성공적으로 hello **Microsoft.Insights** 공급자를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-119">For flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="7b58a-120">단계를 수행 하는 내용이 hello tooregister hello 공급자:</span><span class="sxs-lookup"><span data-stu-id="7b58a-120">tooregister hello provider, take hello following steps:</span></span> 

1. <span data-ttu-id="7b58a-121">너무 이동**구독**, 한 다음 tooenable 흐름 로그 원하는 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-121">Go too**Subscriptions**, and then select hello subscription for which you want tooenable flow logs.</span></span> 
2. <span data-ttu-id="7b58a-122">Hello에 **구독** 블레이드를 **리소스 공급자**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-122">On hello **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="7b58a-123">공급자의 hello 목록을 확인 하 고 해당 hello 확인 **microsoft.insights** 공급자가 등록 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-123">Look at hello list of providers, and verify that hello **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="7b58a-124">그렇지 않으면 **등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-124">If not, then select **Register**.</span></span>

![공급자 보기][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="7b58a-126">흐름 로그를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="7b58a-126">Enable flow logs</span></span>

<span data-ttu-id="7b58a-127">다음이 단계 흐름 로그를 네트워크 보안 그룹을 사용 하도록 설정 hello 프로세스를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-127">These steps take you through hello process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="7b58a-128">1단계</span><span class="sxs-lookup"><span data-stu-id="7b58a-128">Step 1</span></span>

<span data-ttu-id="7b58a-129">Tooa 네트워크 감시자 인스턴스를 이동 하 고 다음 선택 **기록 NSG 흐름**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-129">Go tooa Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![흐름 로그 개요][1]

### <a name="step-2"></a><span data-ttu-id="7b58a-131">2단계</span><span class="sxs-lookup"><span data-stu-id="7b58a-131">Step 2</span></span>

<span data-ttu-id="7b58a-132">Hello 목록에서 네트워크 보안 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-132">Select a network security group from hello list.</span></span>

![흐름 로그 개요][2]

### <a name="step-3"></a><span data-ttu-id="7b58a-134">3단계</span><span class="sxs-lookup"><span data-stu-id="7b58a-134">Step 3</span></span> 

<span data-ttu-id="7b58a-135">Hello에 **흐름 로그 설정을** 블레이드에서 너무 hello 상태 설정**에**, 고 저장소 계정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-135">On hello **Flow logs settings** blade, set hello status too**On**, and then configure a storage account.</span></span>  <span data-ttu-id="7b58a-136">완료되면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-136">When you're done, select **OK**.</span></span> <span data-ttu-id="7b58a-137">그런 다음 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-137">Then select **Save**.</span></span>

![흐름 로그 개요][3]

## <a name="download-flow-logs"></a><span data-ttu-id="7b58a-139">흐름 로그 다운로드</span><span class="sxs-lookup"><span data-stu-id="7b58a-139">Download flow logs</span></span>

<span data-ttu-id="7b58a-140">흐름 로그는 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="7b58a-141">흐름 로그 tooview 다운로드 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-141">Download your flow logs tooview them.</span></span>

### <a name="step-1"></a><span data-ttu-id="7b58a-142">1단계</span><span class="sxs-lookup"><span data-stu-id="7b58a-142">Step 1</span></span>

<span data-ttu-id="7b58a-143">toodownload 흐름 로그 선택 **구성 된 저장소 계정에서 흐름 로그를 다운로드할 수**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-143">toodownload flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="7b58a-144">이 단계에서는 있습니다 tooa 저장소 계정 보기는 로그 toodownload를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-144">This step takes you tooa storage account view where you can choose which logs toodownload.</span></span>

![흐름 로그 설정][4]

### <a name="step-2"></a><span data-ttu-id="7b58a-146">2단계</span><span class="sxs-lookup"><span data-stu-id="7b58a-146">Step 2</span></span>

<span data-ttu-id="7b58a-147">Toohello 올바른 저장소 계정 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-147">Go toohello correct storage account.</span></span> <span data-ttu-id="7b58a-148">그런 다음 **컨테이너** > **insights-log-networksecuritygroupflowevent**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![흐름 로그 설정][5]

### <a name="step-3"></a><span data-ttu-id="7b58a-150">3단계</span><span class="sxs-lookup"><span data-stu-id="7b58a-150">Step 3</span></span>

<span data-ttu-id="7b58a-151">Hello 흐름 로그의 toohello 위치,를 선택한 다음 선택 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-151">Go toohello location of hello flow log, select it, and then select **Download**.</span></span>

![흐름 로그 설정][6]

<span data-ttu-id="7b58a-153">Hello 로그의 hello 구조에 대 한 내용은 방문 [네트워크 보안 그룹 흐름 로그 개요](network-watcher-nsg-flow-logging-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-153">For information about hello structure of hello log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b58a-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7b58a-154">Next steps</span></span>

<span data-ttu-id="7b58a-155">너무 방법에 대해 알아봅니다[PowerBI 사용 하 여 프로그램 NSG 흐름 로그 시각화](network-watcher-visualize-nsg-flow-logs-power-bi.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b58a-155">Learn how too[visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
