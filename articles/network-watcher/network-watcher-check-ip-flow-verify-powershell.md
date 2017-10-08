---
title: "Azure 네트워크 감시자 IP 흐름을 사용 하 여 aaaverify 트래픽을 확인-PowerShell | Microsoft Docs"
description: "이 문서에서는 설명 방법을 toocheck 가상 컴퓨터에서 트래픽 tooor 허용 또는 PowerShell을 사용 하 여 거부 된 경우"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 924da1de1bd554e15816886f8e51d7f170f0e7ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="87bbb-103">트래픽은 허용 되거나 tooor IP 흐름을 사용 하 여 VM에서 거부 되었는지 확인 하 고 Azure 네트워크 감시자의 구성 요소 확인</span><span class="sxs-lookup"><span data-stu-id="87bbb-103">Check if traffic is allowed or denied tooor from a VM with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="87bbb-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="87bbb-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="87bbb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="87bbb-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="87bbb-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="87bbb-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="87bbb-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="87bbb-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="87bbb-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="87bbb-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="87bbb-109">IP 흐름은 tooor 가상 컴퓨터에서 트래픽을 허용 하는 경우 tooverify 수 있는 네트워크 감시자의 기능을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="87bbb-110">이 시나리오는 유용한 tooget tooan 외부 리소스 또는 백 엔드 가상 컴퓨터를 서로 연결할 수 있는지 여부의 현재 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="87bbb-111">IP 흐름 보안 그룹 NSG (네트워크) 규칙에 올바르게 구성 되어 NSG 규칙에 의해 차단 되는 흐름 문제를 해결 하는 경우 사용 되는 tooverify 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="87bbb-112">IP를 사용 하는 또 다른 이유 흐름 tooensure 트래픽이 차단 되도록 제대로 hello NSG 차단 하 고이 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="87bbb-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="87bbb-113">Before you begin</span></span>

<span data-ttu-id="87bbb-114">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 네트워크 감시자의 기존 인스턴스가 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="87bbb-115">hello 시나리오는 또한 적합 한 가상 컴퓨터가 리소스 그룹 사용 toobe 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="87bbb-116">시나리오</span><span class="sxs-lookup"><span data-stu-id="87bbb-116">Scenario</span></span>

<span data-ttu-id="87bbb-117">이 시나리오에서는 IP 흐름 tooverify 확인 하는 가상 컴퓨터 수와 통신 tooa 알려진 경우 Bing IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-117">This scenario uses IP flow verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="87bbb-118">Hello 트래픽이 거부 되 면 해당 트래픽을 거부 하는 hello 보안 규칙을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-118">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="87bbb-119">toolearn 방문 확인 IP 흐름에 대 한 자세한 [IP 흐름 개요를 확인 하십시오.](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="87bbb-119">toolearn more about IP flow verify, visit [IP flow verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="87bbb-120">Network Watcher 검색</span><span class="sxs-lookup"><span data-stu-id="87bbb-120">Retrieve Network Watcher</span></span>

<span data-ttu-id="87bbb-121">hello 첫 번째 단계는 tooretrieve hello 네트워크 감시자 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-121">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="87bbb-122">hello `$networkWatcher` 변수 toohello IP 전달 흐름 cmdlet를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-122">hello `$networkWatcher` variable is passed toohello IP flow verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="87bbb-123">VM 확인</span><span class="sxs-lookup"><span data-stu-id="87bbb-123">Get a VM</span></span>

<span data-ttu-id="87bbb-124">IP 흐름에서의 원격 대상에서 가상 컴퓨터 tooor IP 주소를 트래픽 tooor 테스트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-124">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="87bbb-125">가상 컴퓨터의 Id가 hello cmdlet에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-125">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="87bbb-126">가상 컴퓨터 toouse hello의 hello ID를 알고 있는 경우이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-126">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-hello-nics"></a><span data-ttu-id="87bbb-127">Hello NIC 가져오기</span><span class="sxs-lookup"><span data-stu-id="87bbb-127">Get hello NICS</span></span>

<span data-ttu-id="87bbb-128">hello 가상 컴퓨터에서 NIC의 IP 주소가 hello hello Nic는 가상 컴퓨터에서 검색 하는이 예에서 필요할 때.</span><span class="sxs-lookup"><span data-stu-id="87bbb-128">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="87bbb-129">원하는 tootest hello IP 주소를 알고 있으면 hello 가상 컴퓨터에서이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-129">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="87bbb-130">IP 흐름 확인 실행</span><span class="sxs-lookup"><span data-stu-id="87bbb-130">Run IP flow verify</span></span>

<span data-ttu-id="87bbb-131">Hello 았 hello 정보 toorun hello 필요한 cmdlet을 실행할 `Test-AzureRmNetworkWatcherIPFlow` cmdlet tootest hello 트래픽입니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-131">Now that we have hello information needed toorun hello cmdlet, we run hello `Test-AzureRmNetworkWatcherIPFlow` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="87bbb-132">이 예제에서 사용 하 여 첫 번째 IP 주소가 hello hello 첫 번째 NIC에서</span><span class="sxs-lookup"><span data-stu-id="87bbb-132">In this example, we are using hello first IP address on hello first NIC.</span></span>

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> <span data-ttu-id="87bbb-133">IP 흐름 hello VM 리소스 toorun가 할당 되는 요구를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-133">IP flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="87bbb-134">결과 검토</span><span class="sxs-lookup"><span data-stu-id="87bbb-134">Review Results</span></span>

<span data-ttu-id="87bbb-135">실행 된 후 `Test-AzureRmNetworkWatcherIPFlow` hello 다음 예제는 hello 앞 단계에서에서 반환 된 hello 결과, hello 결과가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-135">After running `Test-AzureRmNetworkWatcherIPFlow` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a><span data-ttu-id="87bbb-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="87bbb-136">Next steps</span></span>

<span data-ttu-id="87bbb-137">트래픽을 차단 하지 않아야 하는 경우 참조 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hello 네트워크 보안 그룹 및 보안 정의 된 규칙을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="87bbb-137">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













