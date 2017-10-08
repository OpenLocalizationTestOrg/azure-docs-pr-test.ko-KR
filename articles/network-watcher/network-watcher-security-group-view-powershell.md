---
title: "Azure 네트워크 감시자 보안 그룹 보기-PowerShell 통한 aaaAnalyze 네트워크 보안 | Microsoft Docs"
description: "이 문서는 어떻게 toouse PowerShell tooanalyze a 가상 컴퓨터 보안 보안 그룹을 설명 합니다."
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
ms.openlocfilehash: 5e1990d97899bd8585025ec13dd556ab2e034c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a><span data-ttu-id="8019e-103">PowerShell를 사용하는 보안 그룹 보기에서 가상 컴퓨터 보안 분석</span><span class="sxs-lookup"><span data-stu-id="8019e-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8019e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8019e-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="8019e-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8019e-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="8019e-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8019e-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="8019e-107">REST API</span><span class="sxs-lookup"><span data-stu-id="8019e-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="8019e-108">보안 그룹 보기 구성 하 고 효과적인 네트워크 보안 규칙을 적용된 tooa 가상 컴퓨터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8019e-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="8019e-109">이 기능은 유용 tooaudit은 네트워크 보안 그룹 진단 및 VM tooensure 트래픽이에 구성 되어 있는 규칙은 올바르게 허용 또는 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="8019e-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="8019e-110">이 문서에서는 보여줍니다 tooretrieve hello 구성 하는 방법 및 PowerShell을 사용 하 여 효과적인 보안 규칙 tooa 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="8019e-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using PowerShell</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8019e-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="8019e-111">Before you begin</span></span>

<span data-ttu-id="8019e-112">Hello를 실행 하면이 시나리오에서는 `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tooretrieve hello 보안 규칙 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="8019e-112">In this scenario, you run hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tooretrieve hello security rule information.</span></span>

<span data-ttu-id="8019e-113">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.</span><span class="sxs-lookup"><span data-stu-id="8019e-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="8019e-114">시나리오</span><span class="sxs-lookup"><span data-stu-id="8019e-114">Scenario</span></span>

<span data-ttu-id="8019e-115">이 문서에서 다루는 hello 시나리오를 구성 하는 hello 및 지정된 된 가상 컴퓨터에 대 한 효과적인 보안 규칙 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="8019e-115">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="8019e-116">Network Watcher 검색</span><span class="sxs-lookup"><span data-stu-id="8019e-116">Retrieve Network Watcher</span></span>

<span data-ttu-id="8019e-117">hello 첫 번째 단계는 tooretrieve hello 네트워크 감시자 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="8019e-117">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="8019e-118">이 변수 toohello 전달 `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8019e-118">This variable is passed toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a><span data-ttu-id="8019e-119">VM 확인</span><span class="sxs-lookup"><span data-stu-id="8019e-119">Get a VM</span></span>

<span data-ttu-id="8019e-120">가상 컴퓨터는 필요한 toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8019e-120">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="8019e-121">다음 예제는 hello VM 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8019e-121">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="8019e-122">보안 그룹 보기 검색</span><span class="sxs-lookup"><span data-stu-id="8019e-122">Retrieve security group view</span></span>

<span data-ttu-id="8019e-123">hello 다음 단계 tooretrieve hello 보안 그룹 뷰 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="8019e-123">hello next step is tooretrieve hello security group view result.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-hello-results"></a><span data-ttu-id="8019e-124">Hello 결과 보기</span><span class="sxs-lookup"><span data-stu-id="8019e-124">Viewing hello results</span></span>

<span data-ttu-id="8019e-125">hello 다음 예제는 반환 된 hello 결과의 축약된 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="8019e-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="8019e-126">hello 결과 표시 모든 hello 효과적이 고 적용 된 보안 규칙의 그룹에 세분화 hello 가상 컴퓨터에서 **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, 및  **EffectiveSecurityRules**합니다.</span><span class="sxs-lookup"><span data-stu-id="8019e-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8019e-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8019e-127">Next steps</span></span>

<span data-ttu-id="8019e-128">방문 [감사 보안 그룹 NSG (네트워크)와 네트워크 감시자](network-watcher-nsg-auditing-powershell.md) toolearn 방법을 네트워크 보안 그룹의 tooautomate 유효성 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="8019e-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


