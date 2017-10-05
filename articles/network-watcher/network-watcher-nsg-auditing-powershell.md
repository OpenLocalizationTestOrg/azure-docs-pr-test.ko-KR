---
title: "Azure Network Watcher 보안 그룹 보기를 사용하여 NSG 감사 자동화 | Microsoft Docs"
description: "이 페이지에서는 네트워크 보안 그룹의 감사를 구성하는 방법에 대한 설명을 제공합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 78a01bcf-74fe-402a-9812-285f3501f877
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a91da330e677c85f16f6f4e506613576b6507d7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a><span data-ttu-id="dfae2-103">Azure Network Watcher 보안 그룹 보기를 사용하여 NSG 감사 자동화</span><span class="sxs-lookup"><span data-stu-id="dfae2-103">Automate NSG auditing with Azure Network Watcher Security group view</span></span>

<span data-ttu-id="dfae2-104">고객은 흔히 인프라의 보안 상태를 확인하는 문제에 직면합니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-104">Customers are often faced with the challenge of verifying the security posture of their infrastructure.</span></span> <span data-ttu-id="dfae2-105">이 문제는 Azure의 VM에 대해서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-105">This challenge is no different for their VMs in Azure.</span></span> <span data-ttu-id="dfae2-106">적용된 NSG(네트워크 보안 그룹) 규칙에 따라 유사한 보안 프로필을 포함하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-106">It is important to have a similar security profile based on the Network Security Group (NSG) rules applied.</span></span> <span data-ttu-id="dfae2-107">보안 그룹 보기를 사용하여 이제 NSG 내의 VM에 적용된 규칙 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-107">Using the Security Group View, you can now get the list of rules applied to a VM within an NSG.</span></span> <span data-ttu-id="dfae2-108">골든 NSG 보안 프로필을 정의하고 매주 보안 그룹 보기를 시작하며 출력을 골든 프로필과 비교하여 보고서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare the output to the golden profile and create a report.</span></span> <span data-ttu-id="dfae2-109">이 방법으로 미리 정해진 보안 프로필을 준수하지 않는 모든 VM을 쉽게 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-109">This way you can identify with ease all the VMs that do not conform to the prescribed security profile.</span></span>

<span data-ttu-id="dfae2-110">네트워크 보안 그룹에 대해 잘 모르는 경우 [네트워크 보안 개요](../virtual-network/virtual-networks-nsg.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="dfae2-110">If you are unfamiliar with Network Security Groups, visit [Network Security Overview](../virtual-network/virtual-networks-nsg.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dfae2-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="dfae2-111">Before you begin</span></span>

<span data-ttu-id="dfae2-112">이 시나리오에서는 가상 컴퓨터에서 반환된 보안 그룹 보기 결과를 알려진 적합한 기준선과 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-112">In this scenario, you compare a known good baseline to the security group view results returned for a virtual machine.</span></span>

<span data-ttu-id="dfae2-113">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="dfae2-114">또한 시나리오에서는 유효한 가상 컴퓨터를 포함한 리소스 그룹을 사용할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="dfae2-115">시나리오</span><span class="sxs-lookup"><span data-stu-id="dfae2-115">Scenario</span></span>

<span data-ttu-id="dfae2-116">이 문서에서 다루는 시나리오는 가상 컴퓨터에 대한 보안 그룹 보기를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-116">The scenario covered in this article gets the security group view for a virtual machine.</span></span>

<span data-ttu-id="dfae2-117">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-117">In this scenario, you will:</span></span>

- <span data-ttu-id="dfae2-118">알려진 적합한 규칙 집합 검색</span><span class="sxs-lookup"><span data-stu-id="dfae2-118">Retrieve a known good rule set</span></span>
- <span data-ttu-id="dfae2-119">Rest API로 가상 컴퓨터 검색</span><span class="sxs-lookup"><span data-stu-id="dfae2-119">Retrieve a virtual machine with Rest API</span></span>
- <span data-ttu-id="dfae2-120">가상 컴퓨터에 대한 보안 그룹 보기 가져오기</span><span class="sxs-lookup"><span data-stu-id="dfae2-120">Get security group view for virtual machine</span></span>
- <span data-ttu-id="dfae2-121">응답 평가</span><span class="sxs-lookup"><span data-stu-id="dfae2-121">Evaluate Response</span></span>

## <a name="retrieve-rule-set"></a><span data-ttu-id="dfae2-122">규칙 집합 검색</span><span class="sxs-lookup"><span data-stu-id="dfae2-122">Retrieve rule set</span></span>

<span data-ttu-id="dfae2-123">이 예제의 첫 번째 단계는 기존 기준선으로 작업하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-123">The first step in this example is to work with an existing baseline.</span></span> <span data-ttu-id="dfae2-124">다음 예제는 이 예제에 대한 기준선으로 사용된 `Get-AzureRmNetworkSecurityGroup` cmdlet을 사용하여 기존 네트워크 보안 그룹에서 추출한 json입니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-124">The following example is some json extracted from an existing Network Security Group using the `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as the baseline for this example.</span></span>

```json
[
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "3389",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1000,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "default-allow-rdp",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/default-allow-rdp"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "111",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1010,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "MyRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/MyRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "112",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1020,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "My2ndRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/My2ndRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "5672",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Deny",
        "Priority":  1030,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "ThisRuleNeedsToStay",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/ThisRuleNeedsToStay"
    }
]
```

## <a name="convert-rule-set-to-powershell-objects"></a><span data-ttu-id="dfae2-125">규칙 집합을 PowerShell 개체로 변환</span><span class="sxs-lookup"><span data-stu-id="dfae2-125">Convert rule set to PowerShell objects</span></span>

<span data-ttu-id="dfae2-126">이 단계에서는 이 예제에 대한 네트워크 보안 그룹에 있는 것으로 예상되는 규칙을 사용하여 이전에 만든 json 파일을 읽고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-126">In this step, we are reading a json file that was created earlier with the rules that are expected to be on the Network Security Group for this example.</span></span>

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a><span data-ttu-id="dfae2-127">Network Watcher 검색</span><span class="sxs-lookup"><span data-stu-id="dfae2-127">Retrieve Network Watcher</span></span>

<span data-ttu-id="dfae2-128">다음 단계는 Network Watcher 인스턴스를 검색하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-128">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="dfae2-129">`$networkWatcher` 변수는 `AzureRmNetworkWatcherSecurityGroupView` cmdlet으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-129">The `$networkWatcher` variable is passed to the `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="dfae2-130">VM 확인</span><span class="sxs-lookup"><span data-stu-id="dfae2-130">Get a VM</span></span>

<span data-ttu-id="dfae2-131">`Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet을 실행하려면 가상 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-131">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="dfae2-132">다음 예제는 VM 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-132">The following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="dfae2-133">보안 그룹 보기 검색</span><span class="sxs-lookup"><span data-stu-id="dfae2-133">Retrieve security group view</span></span>

<span data-ttu-id="dfae2-134">다음 단계에서는 보안 그룹 보기 결과 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-134">The next step is to retrieve the security group view result.</span></span> <span data-ttu-id="dfae2-135">이 결과를 이전에 표시된 "기준선" json과 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-135">This result is compared to the "baseline" json that was shown earlier.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-the-results"></a><span data-ttu-id="dfae2-136">결과 분석</span><span class="sxs-lookup"><span data-stu-id="dfae2-136">Analyzing the results</span></span>

<span data-ttu-id="dfae2-137">응답은 네트워크 인터페이스별로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-137">The response is grouped by Network interfaces.</span></span> <span data-ttu-id="dfae2-138">반환된 다양한 형식의 규칙 및 기본 보안 규칙이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-138">The different types of rules returned are effective and default security rules.</span></span> <span data-ttu-id="dfae2-139">결과는 서브넷 또는 가상 NIC에서 적용된 방식에 따라 세분화됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-139">The result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span></span>

<span data-ttu-id="dfae2-140">다음 PowerShell 스크립트는 보안 그룹 보기의 결과를 기존 NSG 출력과 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-140">The following PowerShell script compares the results of the Security Group View to an existing output of an NSG.</span></span> <span data-ttu-id="dfae2-141">다음 예제는 결과를 `Compare-Object` cmdlet과 비교하는 방법을 보여 주는 간단한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-141">The following example is a simple example of how the results can be compared with `Compare-Object` cmdlet.</span></span>

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

<span data-ttu-id="dfae2-142">다음 예제는 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-142">The following example is the result.</span></span> <span data-ttu-id="dfae2-143">첫 번째 규칙 집합에 있었던 규칙 중 두 가지는 비교에 표시되지 않는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-143">You can see two of the rules that were in the first rule set were not present in the comparison.</span></span>

```
Name                     : My2ndRuleDoNotDelete
Description              : 
Protocol                 : *
SourcePortRange          : *
DestinationPortRange     : 112
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Allow
Priority                 : 1020
Direction                : Inbound
SideIndicator            : <=

Name                     : ThisRuleNeedsToStay
Description              : 
Protocol                 : TCP
SourcePortRange          : *
DestinationPortRange     : 5672
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Deny
Priority                 : 1030
Direction                : Inbound
SideIndicator            : <=
```

## <a name="next-steps"></a><span data-ttu-id="dfae2-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dfae2-144">Next steps</span></span>

<span data-ttu-id="dfae2-145">설정이 변경된 경우 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md)를 참조하여 문제가 될 수 있는 네트워크 보안 그룹 및 보안 규칙을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="dfae2-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are in question.</span></span>













