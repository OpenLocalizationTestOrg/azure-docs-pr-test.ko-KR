---
title: "Azure Network Watcher 보안 그룹 보기를 사용하여 네트워크 보안 분석 - Azure CLI 1.0 | Microsoft Docs"
description: "이 문서에서는 보안 그룹 보기를 사용하여 가상 컴퓨터 보안을 분석하기 위해 Azure CLI 1.0을 사용하는 방법을 설명합니다."
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
ms.openlocfilehash: 2c4c494dcc4fe1a85c5feb29506c35fb03066479
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a><span data-ttu-id="26a63-103">Azure CLI 1.0을 사용하는 보안 그룹 보기에서 가상 컴퓨터 보안 분석</span><span class="sxs-lookup"><span data-stu-id="26a63-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="26a63-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="26a63-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="26a63-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="26a63-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="26a63-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="26a63-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="26a63-107">REST API</span><span class="sxs-lookup"><span data-stu-id="26a63-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="26a63-108">보안 그룹 보기는 가상 컴퓨터에 적용되는 효과적으로 구성된 네트워크 보안 규칙을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="26a63-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="26a63-109">이 기능은 VM에 구성된 네트워크 보안 그룹 및 규칙을 감사하고 진단하여 트래픽을 올바르게 허용하거나 거부하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="26a63-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="26a63-110">이 문서에서는 Azure CLI를 사용하여 가상 컴퓨터에 구성된 효과적인 보안 규칙을 검색하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="26a63-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using Azure CLI</span></span>

<span data-ttu-id="26a63-111">이 문서에서는 Windows, Mac 및 Linux에 사용할 수 있는 플랫폼 간 Azure CLI 1.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26a63-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="26a63-112">Network Watcher는 현재 CLI 지원을 위한 Azure CLI 1.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26a63-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="26a63-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="26a63-113">Before you begin</span></span>

<span data-ttu-id="26a63-114">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="26a63-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="26a63-115">시나리오</span><span class="sxs-lookup"><span data-stu-id="26a63-115">Scenario</span></span>

<span data-ttu-id="26a63-116">이 문서에서 다루는 시나리오는 지정된 가상 컴퓨터에 대한 효과적으로 구성된 보안 규칙을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="26a63-116">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="26a63-117">VM 확인</span><span class="sxs-lookup"><span data-stu-id="26a63-117">Get a VM</span></span>

<span data-ttu-id="26a63-118">가상 컴퓨터는 `vm list` cmdlet을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a63-118">A virtual machine is required to run the `vm list` cmdlet.</span></span> <span data-ttu-id="26a63-119">다음 명령은 리소스 그룹에서 가상 컴퓨터를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="26a63-119">The following command lists the virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="26a63-120">가상 컴퓨터를 알고 있다면 `vm show` cmdlet을 사용하여 리소스 ID를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26a63-120">Once you know the virtual machine, you can use the `vm show` cmdlet to get its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="26a63-121">보안 그룹 보기 검색</span><span class="sxs-lookup"><span data-stu-id="26a63-121">Retrieve security group view</span></span>

<span data-ttu-id="26a63-122">다음 단계에서는 보안 그룹 보기 결과 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="26a63-122">The next step is to retrieve the security group view result.</span></span> <span data-ttu-id="26a63-123">"-json" 플래그를 추가하면 결과의 서식을 json으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="26a63-123">Adding the "--json" flag will format the results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-the-results"></a><span data-ttu-id="26a63-124">결과 보기</span><span class="sxs-lookup"><span data-stu-id="26a63-124">Viewing the results</span></span>

<span data-ttu-id="26a63-125">다음 예제는 반환된 결과의 축약된 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="26a63-125">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="26a63-126">결과는 **NetworkInterfaceSecurityRules**, **DefaultSecurityRules** 및 **EffectiveSecurityRules**라는 그룹으로 구분되는 가상 컴퓨터에서 효과적으로 적용된 보안 규칙을 모두 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="26a63-126">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testnic",
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testvm",
          "securityRules": [
            {
              "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/test-nsg/securityRules/default-allow-rdp",
              "protocol": "TCP",
              "sourcePortRange": "*",
              "destinationPortRange": "3389",
              "sourceAddressPrefix": "*",
              "destinationAddressPrefix": "*",
              "access": "Allow",
              "priority": 1000,
              "direction": "Inbound",
              "provisioningState": "Succeeded",
              "name": "default-allow-rdp",
              "etag": "W/\"00000000-0000-0000-0000-000000000000\""
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/networkSecurityGroups//defaultSecurityRules/",
            "description": "Allow inbound traffic from all VMs in VNET",
            "protocol": "*",
            "sourcePortRange": "*",
            "destinationPortRange": "*",
            "sourceAddressPrefix": "VirtualNetwork",
            "destinationAddressPrefix": "VirtualNetwork",
            "access": "Allow",
            "priority": 65000,
            "direction": "Inbound",
            "provisioningState": "Succeeded",
            "name": "AllowVnetInBound"
          }
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="26a63-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="26a63-127">Next steps</span></span>

<span data-ttu-id="26a63-128">[Network Watcher를 사용하여 NSG(네트워크 보안 그룹) 감사](network-watcher-nsg-auditing-powershell.md)를 방문하여 네트워크 보안 그룹의 유효성 검사를 자동화하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="26a63-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>

<span data-ttu-id="26a63-129">[보안 그룹 개요 보기](network-watcher-security-group-view-overview.md)를 방문하여 네트워크 리소스에 적용되는 보안 규칙에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="26a63-129">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
