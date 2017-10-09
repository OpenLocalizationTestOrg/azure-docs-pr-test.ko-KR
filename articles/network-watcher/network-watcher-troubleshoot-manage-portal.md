---
title: "aaaTroubleshoot Azure 가상 네트워크 게이트웨이 및 연결-PowerShell | Microsoft Docs"
description: "이 페이지에서는 toouse hello Azure 네트워크 감시자 PowerShell cmdlet을 해결 하는 방법을 설명 합니다."
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
ms.openlocfilehash: bd568d34091209390c57d22475559bdb99ad2c59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="514d9-103">Azure Network Watcher PowerShell을 사용하여 Virtual Network 게이트웨이 및 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="514d9-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="514d9-104">포털</span><span class="sxs-lookup"><span data-stu-id="514d9-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="514d9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="514d9-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="514d9-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="514d9-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="514d9-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="514d9-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="514d9-108">REST API</span><span class="sxs-lookup"><span data-stu-id="514d9-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="514d9-109">네트워크 감시자 toounderstanding Azure의 네트워크 리소스 관련해 서 다양 한 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="514d9-110">이러한 기능 중 하나는 리소스 문제 해결입니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="514d9-111">리소스 문제를 해결 하는 hello 포털, PowerShell, CLI 또는 REST API를 통해 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="514d9-112">호출 되 면 네트워크 감시자 가상 네트워크 게이트웨이 또는 연결의 hello 상태를 검사 하 고 해당 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="514d9-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="514d9-113">Before you begin</span></span>

<span data-ttu-id="514d9-114">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="514d9-115">지원되는 게이트웨이 유형 목록을 보려면 [지원되는 게이트웨이 유형](network-watcher-troubleshoot-overview.md#supported-gateway-types)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="514d9-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="514d9-116">개요</span><span class="sxs-lookup"><span data-stu-id="514d9-116">Overview</span></span>

<span data-ttu-id="514d9-117">Hello 기능을 제공 리소스 문제 해결 가상 네트워크 게이트웨이 및 연결 때 발생 하는 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-117">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="514d9-118">요청이 이루어지면 tooresource 문제 해결 로그 되는 쿼리 및 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-118">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="514d9-119">검사 완료 되 면 hello 결과가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-119">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="514d9-120">결과 여러 분 tooreturn를 수행할 수 있는 리소스 문제 해결 요청은 장기 실행 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-120">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="514d9-121">문제 해결에서 hello 로그에 지정 된 저장소 계정에 대 한 컨테이너에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-121">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="troubleshoot-a-gateway-or-connection"></a><span data-ttu-id="514d9-122">게이트웨이 또는 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="514d9-122">Troubleshoot a gateway or connection</span></span>

1. <span data-ttu-id="514d9-123">Toohello 이동 [Azure 포털](https://portal.azure.com) 클릭 **네트워킹** > **네트워크 감시자** > **VPN 진단**</span><span class="sxs-lookup"><span data-stu-id="514d9-123">Navigate toohello [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **VPN Diagnostics**</span></span>
2. <span data-ttu-id="514d9-124">**구독**, **리소스 그룹** 및 **위치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-124">Select a **Subscription**, **Resource Group**, and **Location**.</span></span>
3. <span data-ttu-id="514d9-125">문제 해결 리소스 hello 리소스의 hello 상태에 대 한 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-125">Resource troubleshooting returns data about hello health of hello resource.</span></span> <span data-ttu-id="514d9-126">또한 toobe 검토 하는 관련 로그 tooa 저장소 계정을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-126">It also saves relevant logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="514d9-127">클릭 **저장소 계정** tooselect 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-127">Click **Storage Account** tooselect a storage account.</span></span>
4. <span data-ttu-id="514d9-128">Hello에 **저장소 계정은** 블레이드를 기존 저장소 계정을 선택 하거나 클릭 **저장소 계정 추가** toocreate 새 합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-128">On hello **Storage accounts** blade, select an existing storage account or click **+ Storage account** toocreate a new one.</span></span>
5. <span data-ttu-id="514d9-129">Hello에 **컨테이너** 블레이드에서 기존 컨테이너를 선택 하거나 클릭 **+ 컨테이너** toocreate 새 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-129">On hello **Containers** blade, choose an existing container or click **+ Container** toocreate a new container.</span></span> <span data-ttu-id="514d9-130">완료되면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-130">When complete click **Select**</span></span>
6. <span data-ttu-id="514d9-131">Hello 게이트웨이와 연결 리소스 tootroubleshoot를 선택 하 고 클릭 **문제 해결 시작**</span><span class="sxs-lookup"><span data-stu-id="514d9-131">Select hello Gateway and Connection resources tootroubleshoot and click **Start Troubleshooting**</span></span>

<span data-ttu-id="514d9-132">여러 리소스를 선택한 경우 문제 해결은 게이트웨이 리소스에 동시에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-132">If multiple resources are selected, troubleshooting is run concurrently on gateway resources.</span></span> <span data-ttu-id="514d9-133">연결에서 실행할 수 없습니다 및 hello에 게이트웨이에 연결 된 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-133">It can not run on a connection and it's associated gateway at hello same time.</span></span> <span data-ttu-id="514d9-134">Tootroubleshoot 게이트웨이 것이 좋습니다 먼저 긴 프로세스는 연결 문제 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-134">It is recommended tootroubleshoot gateways first as connection troubleshooting is a longer process.</span></span> <span data-ttu-id="514d9-135">VPN 진단 리소스 hello에서 실행 되는 동안 **상태 문제 해결** 열의 상태가 표시 됩니다 **실행**</span><span class="sxs-lookup"><span data-stu-id="514d9-135">While VPN Diagnostics is running on a resource hello **TROUBLESHOOTING STATUS** column will show a status of **Running**</span></span>

<span data-ttu-id="514d9-136">완료 되 면 hello 상태 열 변경 내용 너무**정상** 또는 **Unhealthy**합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-136">When complete, hello status column changes too**Healthy** or **Unhealthy**.</span></span>

![문제 해결 완료][2]

## <a name="understanding-hello-results"></a><span data-ttu-id="514d9-138">Hello 결과 이해</span><span class="sxs-lookup"><span data-stu-id="514d9-138">Understanding hello results</span></span>

<span data-ttu-id="514d9-139">Hello에 **세부 정보** 섹션 hello 창의 hello **상태** 탭에 표시 hello 마지막 문제 해결의 hello 상태 실행 hello 선택한 리소스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-139">In hello **Details** section of hello window, hello **Status** tab shows hello status of hello last troubleshooting run on hello selected resource.</span></span> <span data-ttu-id="514d9-140">Hello 최신 진단 결과가 표시 된 xx 분 후에 hello 마지막으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-140">Results of hello latest diagnostic are shown xx minutes after hello last run.</span></span>

|<span data-ttu-id="514d9-141">속성</span><span class="sxs-lookup"><span data-stu-id="514d9-141">Property</span></span>  |<span data-ttu-id="514d9-142">설명</span><span class="sxs-lookup"><span data-stu-id="514d9-142">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="514d9-143">리소스</span><span class="sxs-lookup"><span data-stu-id="514d9-143">Resource</span></span>     | <span data-ttu-id="514d9-144">링크 toohello 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-144">A link toohello resource.</span></span>        |
|<span data-ttu-id="514d9-145">저장소 경로</span><span class="sxs-lookup"><span data-stu-id="514d9-145">Storage path</span></span>     |  <span data-ttu-id="514d9-146">경로 toohello 저장소 계정 및 컨테이너 (모든 hello를 실행 하는 동안 생성 된) 경우 hello 로그를 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-146">Path toohello storage account and container that contain hello logs (if any were produced during hello run).</span></span> <span data-ttu-id="514d9-147">Hello 포털을 나간 후에이 설정은 유지 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-147">This setting does not persist after you leave hello portal.</span></span>        |
|<span data-ttu-id="514d9-148">요약</span><span class="sxs-lookup"><span data-stu-id="514d9-148">Summary</span></span>     | <span data-ttu-id="514d9-149">요약 hello 리소스 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-149">Summary of hello resource health.</span></span>        |
|<span data-ttu-id="514d9-150">세부 정보</span><span class="sxs-lookup"><span data-stu-id="514d9-150">Detail</span></span>     | <span data-ttu-id="514d9-151">Hello 리소스 상태에 대 한 자세한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-151">Detailed information on hello resource health.</span></span>        |
|<span data-ttu-id="514d9-152">마지막 실행</span><span class="sxs-lookup"><span data-stu-id="514d9-152">Last run</span></span>     | <span data-ttu-id="514d9-153">마지막 시간 hello hello 실행 된 시간 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-153">hello time hello last time troubleshooting was ran.</span></span>        |


<span data-ttu-id="514d9-154">hello **동작** 탭 어떻게 tooresolve hello 문제에 일반적인 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-154">hello **Action** tab provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="514d9-155">Hello 문제에 대 한 작업을 수행할 수, 링크를 추가 하는 지침과 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-155">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="514d9-156">Hello 경우에서 hello 응답을 자세한 지침은 없으며가 있는 hello url tooopen 지원 사례를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-156">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="514d9-157">Hello 응답 및 포함 된 항목의 hello 속성에 대 한 자세한 내용은 방문 [네트워크 감시자 문제 해결 개요](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="514d9-157">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>


## <a name="next-steps"></a><span data-ttu-id="514d9-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="514d9-158">Next steps</span></span>

<span data-ttu-id="514d9-159">해당 중지 VPN 연결 설정이 변경 되었으며, 참조 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack 아래로 hello 네트워크 보안 그룹 및 보안 규칙을 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="514d9-159">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
