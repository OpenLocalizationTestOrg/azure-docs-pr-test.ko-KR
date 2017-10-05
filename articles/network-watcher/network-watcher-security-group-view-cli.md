---
title: "Azure Network Watcher 보안 그룹 보기를 사용하여 네트워크 보안 분석 - Azure CLI 2.0 | Microsoft Docs"
description: "이 문서에서는 보안 그룹 보기를 사용하여 가상 컴퓨터 보안을 분석하기 위해 Azure CLI 2.0을 사용하는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 1756e14819e3b7c79361c193413a1fcd7f24a4e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a><span data-ttu-id="b1db4-103">Azure CLI 2.0을 사용하는 보안 그룹 보기에서 가상 컴퓨터 보안 분석</span><span class="sxs-lookup"><span data-stu-id="b1db4-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="b1db4-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1db4-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="b1db4-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b1db4-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="b1db4-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b1db4-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="b1db4-107">REST API</span><span class="sxs-lookup"><span data-stu-id="b1db4-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="b1db4-108">보안 그룹 보기는 가상 컴퓨터에 적용되는 효과적으로 구성된 네트워크 보안 규칙을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b1db4-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="b1db4-109">이 기능은 VM에 구성된 네트워크 보안 그룹 및 규칙을 감사하고 진단하여 트래픽을 올바르게 허용하거나 거부하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1db4-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="b1db4-110">이 문서에서는 Azure CLI를 사용하여 가상 컴퓨터에 구성된 효과적인 보안 규칙을 검색하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b1db4-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using Azure CLI</span></span>


<span data-ttu-id="b1db4-111">이 문서에서는 Windows, Mac 및 Linux에서 사용할 수 있는 리소스 관리 배포 모델용 차세대 CLI인 Azure CLI 2.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1db4-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="b1db4-112">이 문서의 단계를 수행하려면 [Mac, Linux 및 Windows용 Azure 명령줄 인터페이스(Azure CLI)를 설치](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1db4-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b1db4-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="b1db4-113">Before you begin</span></span>

<span data-ttu-id="b1db4-114">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1db4-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="b1db4-115">시나리오</span><span class="sxs-lookup"><span data-stu-id="b1db4-115">Scenario</span></span>

<span data-ttu-id="b1db4-116">이 문서에서 다루는 시나리오는 지정된 가상 컴퓨터에 대한 효과적으로 구성된 보안 규칙을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b1db4-116">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="b1db4-117">VM 확인</span><span class="sxs-lookup"><span data-stu-id="b1db4-117">Get a VM</span></span>

<span data-ttu-id="b1db4-118">가상 컴퓨터는 `vm list` cmdlet을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1db4-118">A virtual machine is required to run the `vm list` cmdlet.</span></span> <span data-ttu-id="b1db4-119">다음 명령은 리소스 그룹에서 가상 컴퓨터를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b1db4-119">The following command lists the virtual machines in a resource group:</span></span>

```azurecli
az vm list -resource-group resourceGroupName
```

<span data-ttu-id="b1db4-120">가상 컴퓨터를 알고 있다면 `vm show` cmdlet을 사용하여 리소스 ID를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1db4-120">Once you know the virtual machine, you can use the `vm show` cmdlet to get its resource Id:</span></span>

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="b1db4-121">보안 그룹 보기 검색</span><span class="sxs-lookup"><span data-stu-id="b1db4-121">Retrieve security group view</span></span>

<span data-ttu-id="b1db4-122">다음 단계에서는 보안 그룹 보기 결과 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b1db4-122">The next step is to retrieve the security group view result.</span></span>

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-the-results"></a><span data-ttu-id="b1db4-123">결과 보기</span><span class="sxs-lookup"><span data-stu-id="b1db4-123">Viewing the results</span></span>

<span data-ttu-id="b1db4-124">다음 예제는 반환된 결과의 축약된 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="b1db4-124">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="b1db4-125">결과는 **NetworkInterfaceSecurityRules**, **DefaultSecurityRules** 및 **EffectiveSecurityRules**라는 그룹으로 구분되는 가상 컴퓨터에서 효과적으로 적용된 보안 규칙을 모두 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b1db4-125">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
      "resourceGroup": "{resourceGroupName}",
      "securityRuleAssociations": {
        "defaultSecurityRules": [
          {
            "access": "Allow",
            "description": "Allow inbound traffic from all VMs in VNET",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "*",
            "direction": "Inbound",
            "etag": null,
            "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups//providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/AllowVnetInBound",
            "name": "AllowVnetInBound",
            "priority": 65000,
            "protocol": "*",
            "provisioningState": "Succeeded",
            "resourceGroup": "",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "*"
          }...
        ],
        "effectiveSecurityRules": [
          {
            "access": "Deny",
            "destinationAddressPrefix": "*",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": null,
            "expandedSourceAddressPrefix": null,
            "name": "DefaultOutboundDenyAll",
            "priority": 65500,
            "protocol": "All",
            "sourceAddressPrefix": "*",
            "sourcePortRange": "0-65535"
          },
          {
            "access": "Allow",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "expandedSourceAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "name": "DefaultRule_AllowVnetOutBound",
            "priority": 65000,
            "protocol": "All",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "0-65535"
          },...
        ],
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "resourceGroup": "{resourceGroupName}",
          "securityRules": [
            {
              "access": "Allow",
              "description": null,
              "destinationAddressPrefix": "*",
              "destinationPortRange": "3389",
              "direction": "Inbound",
              "etag": "W/\"efb606c1-2d54-475a-ab20-da3f80393577\"",
              "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "name": "default-allow-rdp",
              "priority": 1000,
              "protocol": "TCP",
              "provisioningState": "Succeeded",
              "resourceGroup": "{resourceGroupName}",
              "sourceAddressPrefix": "*",
              "sourcePortRange": "*"
            }
          ]
        },
        "subnetAssociation": null
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="b1db4-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b1db4-126">Next steps</span></span>

<span data-ttu-id="b1db4-127">[Network Watcher를 사용하여 NSG(네트워크 보안 그룹) 감사](network-watcher-nsg-auditing-powershell.md)를 방문하여 네트워크 보안 그룹의 유효성 검사를 자동화하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b1db4-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>

<span data-ttu-id="b1db4-128">[보안 그룹 개요 보기](network-watcher-security-group-view-overview.md)를 방문하여 네트워크 리소스에 적용되는 보안 규칙에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b1db4-128">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
