---
title: "Azure Network Watcher 보안 그룹 보기를 사용하여 네트워크 보안 분석 - PowerShell | Microsoft Docs"
description: "이 문서에서는 보안 그룹 보기를 사용하여 가상 컴퓨터 보안을 분석하기 위해 PowerShell을 사용하는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04e76b49-6a1b-4d0f-9a9b-51cf2f4df5a2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 363fdd9f1de933bb4050f91e1e111aaf3e419058
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a><span data-ttu-id="61d86-103">PowerShell를 사용하는 보안 그룹 보기에서 가상 컴퓨터 보안 분석</span><span class="sxs-lookup"><span data-stu-id="61d86-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="61d86-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="61d86-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="61d86-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="61d86-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="61d86-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="61d86-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="61d86-107">REST API</span><span class="sxs-lookup"><span data-stu-id="61d86-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="61d86-108">보안 그룹 보기는 가상 컴퓨터에 적용되는 효과적으로 구성된 네트워크 보안 규칙을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="61d86-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="61d86-109">이 기능은 VM에 구성된 네트워크 보안 그룹 및 규칙을 감사하고 진단하여 트래픽을 올바르게 허용하거나 거부하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="61d86-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="61d86-110">이 문서에서는 PowerShell을 사용하여 가상 컴퓨터에 구성된 효과적인 보안 규칙을 검색하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="61d86-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using PowerShell</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="61d86-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="61d86-111">Before you begin</span></span>

<span data-ttu-id="61d86-112">이 시나리오에서는 `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet을 실행하여 보안 규칙 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="61d86-112">In this scenario, you run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet to retrieve the security rule information.</span></span>

<span data-ttu-id="61d86-113">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="61d86-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="61d86-114">시나리오</span><span class="sxs-lookup"><span data-stu-id="61d86-114">Scenario</span></span>

<span data-ttu-id="61d86-115">이 문서에서 다루는 시나리오는 지정된 가상 컴퓨터에 대한 효과적으로 구성된 보안 규칙을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="61d86-115">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="61d86-116">Network Watcher 검색</span><span class="sxs-lookup"><span data-stu-id="61d86-116">Retrieve Network Watcher</span></span>

<span data-ttu-id="61d86-117">첫 번째 단계는 Network Watcher 인스턴스를 검색하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="61d86-117">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="61d86-118">이 변수는 `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="61d86-118">This variable is passed to the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a><span data-ttu-id="61d86-119">VM 확인</span><span class="sxs-lookup"><span data-stu-id="61d86-119">Get a VM</span></span>

<span data-ttu-id="61d86-120">`Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet을 실행하려면 가상 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="61d86-120">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="61d86-121">다음 예제는 VM 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="61d86-121">The following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="61d86-122">보안 그룹 보기 검색</span><span class="sxs-lookup"><span data-stu-id="61d86-122">Retrieve security group view</span></span>

<span data-ttu-id="61d86-123">다음 단계에서는 보안 그룹 보기 결과 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="61d86-123">The next step is to retrieve the security group view result.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-the-results"></a><span data-ttu-id="61d86-124">결과 보기</span><span class="sxs-lookup"><span data-stu-id="61d86-124">Viewing the results</span></span>

<span data-ttu-id="61d86-125">다음 예제는 반환된 결과의 축약된 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="61d86-125">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="61d86-126">결과는 **NetworkInterfaceSecurityRules**, **DefaultSecurityRules** 및 **EffectiveSecurityRules**라는 그룹으로 구분되는 가상 컴퓨터에서 효과적으로 적용된 보안 규칙을 모두 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="61d86-126">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```
NetworkInterfaces : [
                      {
                        "NetworkInterfaceSecurityRules": [
                          {
                            "Name": "default-allow-rdp",
                            "Etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
                            "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/securityRules/default-allow-rdp",
                            "Protocol": "TCP",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "3389",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "Access": "Allow",
                            "Priority": 1000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "DefaultSecurityRules": [
                          {
                            "Name": "AllowVnetInBound",
                            "Id": "/subscriptions00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/defaultSecurityRules/",
                            "Description": "Allow inbound traffic from all VMs in VNET",
                            "Protocol": "*",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "*",
                            "SourceAddressPrefix": "VirtualNetwork",
                            "DestinationAddressPrefix": "VirtualNetwork",
                            "Access": "Allow",
                            "Priority": 65000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "EffectiveSecurityRules": [
                          {
                            "Name": "DefaultOutboundDenyAll",
                            "Protocol": "All",
                            "SourcePortRange": "0-65535",
                            "DestinationPortRange": "0-65535",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "ExpandedSourceAddressPrefix": [],
                            "ExpandedDestinationAddressPrefix": [],
                            "Access": "Deny",
                            "Priority": 65500,
                            "Direction": "Outbound"
                          },
                          ...
                        ]
                      }
                    ]
```

## <a name="next-steps"></a><span data-ttu-id="61d86-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="61d86-127">Next steps</span></span>

<span data-ttu-id="61d86-128">[Network Watcher를 사용하여 NSG(네트워크 보안 그룹) 감사](network-watcher-nsg-auditing-powershell.md)를 방문하여 네트워크 보안 그룹의 유효성 검사를 자동화하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="61d86-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>


