---
title: "Azure Network Watcher 보안 그룹 보기를 사용하여 네트워크 보안 분석 - REST API | Microsoft Docs"
description: "이 문서에서는 보안 그룹 보기를 사용하여 가상 컴퓨터 보안을 분석하기 위해 PowerShell을 사용하는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a2f418fe-f5d2-43ed-8dc3-df0ed2a4d4ac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: afced52b3ae6f3b7f400364f5ec7d049aa166590
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a><span data-ttu-id="5fdb4-103">REST API를 사용하는 보안 그룹 보기에서 Virtual Machine 보안 분석</span><span class="sxs-lookup"><span data-stu-id="5fdb4-103">Analyze your Virtual Machine security with Security Group View using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="5fdb4-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5fdb4-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="5fdb4-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5fdb4-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="5fdb4-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5fdb4-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="5fdb4-107">REST API</span><span class="sxs-lookup"><span data-stu-id="5fdb4-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="5fdb4-108">보안 그룹 보기는 가상 컴퓨터에 적용되는 효과적으로 구성된 네트워크 보안 규칙을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="5fdb4-109">이 기능은 VM에 구성된 네트워크 보안 그룹 및 규칙을 감사하고 진단하여 트래픽을 올바르게 허용하거나 거부하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="5fdb4-110">이 문서에서는 REST API를 사용하여 가상 컴퓨터에 효과적으로 적용된 보안 규칙을 검색하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-110">In this article, we show you how to retrieve the effective and applied security rules to a virtual machine using REST API</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5fdb4-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="5fdb4-111">Before you begin</span></span>

<span data-ttu-id="5fdb4-112">이 시나리오에서는 Network Watcher Rest API를 호출하여 가상 컴퓨터에 대한 보안 그룹 보기를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-112">In this scenario, you call the Network Watcher Rest API to get the security group view for a virtual machine.</span></span> <span data-ttu-id="5fdb4-113">PowerShell을 사용하여 REST API를 호출하는 데 ARMclient가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-113">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="5fdb4-114">ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="5fdb4-115">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="5fdb4-116">또한 시나리오에서는 유효한 가상 컴퓨터를 포함한 리소스 그룹을 사용할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="5fdb4-117">시나리오</span><span class="sxs-lookup"><span data-stu-id="5fdb4-117">Scenario</span></span>

<span data-ttu-id="5fdb4-118">이 문서에서 다루는 시나리오는 지정된 가상 컴퓨터에 대한 효과적으로 적용된 보안 규칙을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-118">The scenario covered in this article retrieves the effective and applied security rules for a given virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="5fdb4-119">ARMClient에 로그인</span><span class="sxs-lookup"><span data-stu-id="5fdb4-119">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="5fdb4-120">가상 컴퓨터 검색</span><span class="sxs-lookup"><span data-stu-id="5fdb4-120">Retrieve a virtual machine</span></span>

<span data-ttu-id="5fdb4-121">다음 스크립트를 실행하여 가상 컴퓨터를 반환합니다. 다음 코드에는 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-121">Run the following script to return a virtual machineThe following code needs variables:</span></span>

- <span data-ttu-id="5fdb4-122">**subscriptionId** - **Get-AzureRMSubscription** cmdlet으로 구독 ID도 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-122">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="5fdb4-123">**resourceGroupName** - 가상 컴퓨터를 포함하는 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-123">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="5fdb4-124">필요한 정보는 다음 예제에 볼 수 있는 것처럼 응답에서 `Microsoft.Compute/virtualMachines` 형식 아래의 **id**입니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-124">The information that is needed is the **id** under the type `Microsoft.Compute/virtualMachines` in response, as seen in the following example:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft
.Network/networkInterfaces/{nicName}"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Com
pute/virtualMachines/{vmName}/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute
/virtualMachines/{vmName}",
      "name": "{vmName}"
    }
  ]
}
```

## <a name="get-security-group-view-for-virtual-machine"></a><span data-ttu-id="5fdb4-125">가상 컴퓨터에 대한 보안 그룹 보기 가져오기</span><span class="sxs-lookup"><span data-stu-id="5fdb4-125">Get security group view for virtual machine</span></span>

<span data-ttu-id="5fdb4-126">다음 예제에서는 대상 지정된 가상 컴퓨터의 보안 그룹 보기를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-126">The following example requests the security group view of a targeted virtual machine.</span></span> <span data-ttu-id="5fdb4-127">구성 편차를 검색하기 위해 원본에서 정의한 규칙 및 보안을 비교하는 데 이 예제의 결과를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-127">The results from this example can be used to compare to the rules and security defined by the origination to look for configuration drift.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName

$requestBody = @"
{
    'targetResourceId': '${targetUri}'

}
"@
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/securityGroupView?api-version=2016-12-01" $requestBody -verbose
```

## <a name="view-the-response"></a><span data-ttu-id="5fdb4-128">응답 보기</span><span class="sxs-lookup"><span data-stu-id="5fdb4-128">View the response</span></span>

<span data-ttu-id="5fdb4-129">다음 샘플은 이전 명령에서 반환한 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-129">The following sample is the response returned from the preceding command.</span></span> <span data-ttu-id="5fdb4-130">결과는 **NetworkInterfaceSecurityRules**, **DefaultSecurityRules** 및 **EffectiveSecurityRules**라는 그룹으로 구분되는 가상 컴퓨터에서 효과적으로 적용된 보안 규칙을 모두 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-130">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json

{
  "networkInterfaces": [
    {
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "securityRules": [
            {
              "name": "default-allow-rdp",
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
              "properties": {
                "provisioningState": "Succeeded",
                "protocol": "TCP",
                "sourcePortRange": "*",
                "destinationPortRange": "3389",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*",
                "access": "Allow",
                "priority": 1000,
                "direction": "Inbound"
              }
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "name": "AllowVnetInBound",
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/",
            "properties": {
              "provisioningState": "Succeeded",
              "description": "Allow inbound traffic from all VMs in VNET",
              "protocol": "*",
              "sourcePortRange": "*",
              "destinationPortRange": "*",
              "sourceAddressPrefix": "VirtualNetwork",
              "destinationAddressPrefix": "VirtualNetwork",
              "access": "Allow",
              "priority": 65000,
              "direction": "Inbound"
            }
          },
          ...
        ],
        "effectiveSecurityRules": [
          {
            "name": "DefaultOutboundDenyAll",
            "protocol": "All",
            "sourcePortRange": "0-65535",
            "destinationPortRange": "0-65535",
            "sourceAddressPrefix": "*",
            "destinationAddressPrefix": "*",
            "access": "Deny",
            "priority": 65500,
            "direction": "Outbound"
          },
          ...
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="5fdb4-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5fdb4-131">Next steps</span></span>

<span data-ttu-id="5fdb4-132">[Network Watcher를 사용하여 NSG(네트워크 보안 그룹) 감사](network-watcher-security-group-view-powershell.md)를 방문하여 네트워크 보안 그룹의 유효성 검사를 자동화하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5fdb4-132">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>


