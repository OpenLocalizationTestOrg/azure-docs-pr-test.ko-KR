---
title: "Azure 네트워크 감시자 인스턴스 aaaCreate | Microsoft Docs"
description: "이 페이지에서는 hello 단계 toocreate 네트워크 감시자의 인스턴스 hello 포털 및 Azure REST API를 사용 하 여"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="a1a9a-103">Azure Network Watcher 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="a1a9a-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="a1a9a-104">네트워크 감시자는 toomonitor 있습니다 수 있도록 하는 지역 서비스 및 네트워크 시나리오의 수준에서 및 Azure에서 상태를 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a9a-104">Network Watcher is a regional service that enables you toomonitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="a1a9a-105">수준 모니터링 시나리오는 최종 tooend 네트워크 수준 보기에서 toodiagnose 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1a9a-105">Scenario level monitoring enables you toodiagnose problems at an end tooend network level view.</span></span> <span data-ttu-id="a1a9a-106">네트워크 문제 진단 및 시각화 도구를 사용할 수 있는 네트워크 감시자 insights tooyour Azure 네트워크에에서 가져오고 이해, 진단, 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1a9a-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights tooyour network in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="a1a9a-107">네트워크 감시자는 현재 지원 CLI 1.0, hello 지침 toocreate 새 네트워크 감시자 인스턴스 제공 됩니다 CLI 1.0에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a9a-107">As Network Watcher currently only supports CLI 1.0, hello instructions toocreate a new Network Watcher instance is provided for CLI 1.0.</span></span>

## <a name="create-a-network-watcher-in-hello-portal"></a><span data-ttu-id="a1a9a-108">네트워크 감시자 hello 포털에서 만들기</span><span class="sxs-lookup"><span data-stu-id="a1a9a-108">Create a Network Watcher in hello portal</span></span>

<span data-ttu-id="a1a9a-109">너무 이동**더 서비스** > **네트워킹** > **네트워크 감시자**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a9a-109">Navigate too**More Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="a1a9a-110">네트워크 감시자 tooenable 원하는 모든 hello 구독을 선택할 수 있습니다에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a9a-110">You can select all hello subscriptions you want tooenable Network Watcher for.</span></span> <span data-ttu-id="a1a9a-111">이 작업은 사용할 수 있는 모든 지역에서 Network Watcher를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1a9a-111">This action creates a Network Watcher in every region that is available.</span></span>

![Network Watcher 만들기][1]

<span data-ttu-id="a1a9a-113">네트워크 감시자 hello 포털을 사용 하 여 사용 하도록 설정 하면 hello hello 네트워크 감시자 인스턴스 이름이 자동으로 설정 됩니다 tooNetworkWatcher_region_name region_name toohello hello 인스턴스가 활성화 된 Azure 영역을 해당 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a1a9a-113">When you enable Network Watcher using hello Portal, hello name of hello Network Watcher instance will automatically be set tooNetworkWatcher_region_name where region_name corresponds toohello Azure Region where hello instance was enabled.</span></span>  <span data-ttu-id="a1a9a-114">예를 들어 미국 중서부에서 활성화된 Network Watcher의 이름은 NetworkWatcher_westcentralus입니다.</span><span class="sxs-lookup"><span data-stu-id="a1a9a-114">For example, a Network Watcher enabled in West Central US region will be named NetworkWatcher_westcentralus</span></span>

<span data-ttu-id="a1a9a-115">또한 hello 네트워크 감시자 인스턴스 NetworkWatcherRG 라는 리소스 그룹에 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1a9a-115">Additionally, hello Network Watcher instance will automatically be added into a Resource Group called NetworkWatcherRG.</span></span>  <span data-ttu-id="a1a9a-116">이 리소스 그룹은 아직 존재하지 않는 경우 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a1a9a-116">This Resource Group will be created if it does not already exist.</span></span>

<span data-ttu-id="a1a9a-117">네트워크 감시자 인스턴스와 hello의 toocustomize hello 이름이 필요한 경우 리소스 그룹에 배치 됩니다, 그리고 아래에서 설명 하는 Powershell, REST API hello 또는 ARMClient 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1a9a-117">If you wish toocustomize hello name of a Network Watcher instance and hello Resource Group it's placed into, you can use Powershell, hello REST API, or ARMClient methods described below.</span></span>  <span data-ttu-id="a1a9a-118">각 옵션에 hello 네트워크 감시자를 배치 하기 전에 hello 리소스 그룹이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a9a-118">In each option, hello Resource Group must exist before you place hello Network Watcher into it.</span></span>  

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="a1a9a-119">PowerShell을 사용하여 Network Watcher 만들기</span><span class="sxs-lookup"><span data-stu-id="a1a9a-119">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="a1a9a-120">다음 예제는 hello를 실행 하는 네트워크 감시자의 인스턴스 toocreate:</span><span class="sxs-lookup"><span data-stu-id="a1a9a-120">toocreate an instance of Network Watcher, run hello following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a><span data-ttu-id="a1a9a-121">네트워크 감시자 hello REST API를 사용 하 여 만들기</span><span class="sxs-lookup"><span data-stu-id="a1a9a-121">Create a Network Watcher with hello REST API</span></span>

<span data-ttu-id="a1a9a-122">ARMclient는 PowerShell을 사용 하 여 사용 되는 toocall hello REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="a1a9a-122">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="a1a9a-123">ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1a9a-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="a1a9a-124">ARMClient에 로그인</span><span class="sxs-lookup"><span data-stu-id="a1a9a-124">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a><span data-ttu-id="a1a9a-125">네트워크 감시자 hello 만들기</span><span class="sxs-lookup"><span data-stu-id="a1a9a-125">Create hello network watcher</span></span>

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a><span data-ttu-id="a1a9a-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a1a9a-126">Next steps</span></span>

<span data-ttu-id="a1a9a-127">네트워크 감시자의 인스턴스를가지고 있습니다 사용할 수 있는 hello 기능에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a1a9a-127">Now that you have an instance of Network Watcher, learn about hello features available:</span></span>

* [<span data-ttu-id="a1a9a-128">토폴로지</span><span class="sxs-lookup"><span data-stu-id="a1a9a-128">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="a1a9a-129">패킷 캡처</span><span class="sxs-lookup"><span data-stu-id="a1a9a-129">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="a1a9a-130">IP 흐름 확인</span><span class="sxs-lookup"><span data-stu-id="a1a9a-130">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="a1a9a-131">다음 홉</span><span class="sxs-lookup"><span data-stu-id="a1a9a-131">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="a1a9a-132">보안 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="a1a9a-132">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="a1a9a-133">NSG 흐름 로깅</span><span class="sxs-lookup"><span data-stu-id="a1a9a-133">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="a1a9a-134">Virtual Network 게이트웨이 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a1a9a-134">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="a1a9a-135">네트워크 감시자 인스턴스를 만든 후 다음 hello 문서가 패키지 캡처를 구성할 수 있습니다: [경고 트리거된 패킷 캡처를 만들려면](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="a1a9a-135">Once a Network Watcher instance has been created, package capture can be configured by following hello article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

[1]: ./media/network-watcher-create/figure1.png











